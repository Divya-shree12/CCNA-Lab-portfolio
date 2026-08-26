# Protocol Analysis: Complete TCP Session Lifecycle & Teardown

## Overview
This lab captures and analyzes a complete, unencrypted HTTP transaction to `example.com` over Port 80 using Wireshark. It tracks the full TCP Layer 4 state machine across three phases:
1. Three-way connection establishment
2. Data transfer with dynamic recovery (Retransmissions & Duplicate ACKs)
3. Graceful four-way connection teardown

---

## Capture Details
- **Capture Interface:** Wi-Fi (`IPv6`)
- **Display Filter:** `tcp.port == 80`
- **Client Endpoint:** `[2409:4091:3013:8808...]:56218`
- **Server Endpoint:** `[2606:4700:99e5:72db...]:80`
- **Artifact Image:** `tcp-handshake-teardown.png`

![TCP Handshake and Teardown Capture](tcp-handshake-teardown.png)

---

## Detailed Frame-by-Frame Breakdown

### 1. Three-Way Handshake (Connection Establishment)
* **Frame 31 (`[SYN]`):**
  * **Direction:** Client $\rightarrow$ Server
  * **Details:** `Seq=0`, `Len=0`, `Win=65535`, `MSS=1440`, `WS=256`, `SACK_PERM=1`
  * **Analysis:** The client initiates the socket connection. The packet header inspection confirms `Flags: 0x002 (SYN)` is set (`Syn: 1`, `Acknowledgment: 0`). Parameters like Maximum Segment Size (MSS) and Window Scaling (multiplier of 256) are negotiated.
* **Frame 32 (`[SYN, ACK]`):**
  * **Direction:** Server $\rightarrow$ Client
  * **Details:** `Seq=0`, `Ack=1`, `Len=0`, `Win=65535`, `MSS=1360`, `WS=8192`, `SACK_PERM=1`
  * **Analysis:** The server acknowledges the client's SYN (`Ack = 0 + 1 = 1`) and sends its own synchronize sequence (`Seq=0`).
* **Frame 33 (`[ACK]`):**
  * **Direction:** Client $\rightarrow$ Server
  * **Details:** `Seq=1`, `Ack=1`, `Len=0`, `Win=65280`
  * **Analysis:** Client acknowledges the server's SYN. The connection enters the **`ESTABLISHED`** state.

---

### 2. HTTP Request, Response & TCP Reliability Handling
* **Frame 34 (`HTTP GET`):**
  * **Direction:** Client $\rightarrow$ Server
  * **Details:** `GET / HTTP/1.1` (`Len=149`)
  * **Analysis:** Client transmits the HTTP Layer 7 request payload.
* **Frame 35 (`[ACK]`):**
  * **Direction:** Server $\rightarrow$ Client
  * **Details:** `Seq=1`, `Ack=76`, `Len=0`, `Win=131072`
  * **Analysis:** Server confirms receipt of the initial request stream.
* **Frames 36–38 (Out-of-Order Handling & Fast Retransmission):**
  * **Frame 36:** Server sends a segment continuation (`Len=79`), but an intermediate segment was dropped/delayed on the link (`[TCP Previous segment not captured]`).
  * **Frame 37:** Server triggers a retransmission (`[TCP Retransmission]`, `Len=943`, `[PSH, ACK]`) delivering the missing HTTP payload.
  * **Frame 38:** Client emits a Duplicate Acknowledgment (`[TCP Dup ACK 33#1]`, `Ack=1`, with SACK edges `SLE=870 SRE=875`) acknowledging receipt of out-of-order blocks while waiting for missing bytes.

---

### 3. Four-Way Connection Teardown (Graceful Close)
* **Frame 39 (`[ACK]`):**
  * **Direction:** Client $\rightarrow$ Server
  * **Details:** `Seq=76`, `Ack=875`, `Len=0`
  * **Analysis:** Client acknowledges all remaining inbound application data up to byte 874.
* **Frame 40 (`[FIN, ACK]`):**
  * **Direction:** Client $\rightarrow$ Server
  * **Details:** `Seq=76`, `Ack=875`, `Len=0`
  * **Analysis:** Client signals it has finished transmitting data and requests closure of its side of the half-duplex channel (`FIN_WAIT_1`).
* **Frame 41 (`[FIN, ACK]`):**
  * **Direction:** Server $\rightarrow$ Client
  * **Details:** `Seq=875`, `Ack=77`, `Len=0`
  * **Analysis:** Server acknowledges the client's FIN (`Ack = 76 + 1 = 77`) and sends its own FIN to close the server-to-client half-duplex channel.
* **Frame 42 (`[ACK]`):**
  * **Direction:** Client $\rightarrow$ Server
  * **Details:** `Seq=77`, `Ack=876`, `Len=0`
  * **Analysis:** Client acknowledges the server's FIN (`Ack = 875 + 1 = 876`). Sockets transition to `TIME_WAIT` $\rightarrow$ `CLOSED`.

---

## Key Takeaways
1. **Header Bit Verification:** Captured raw flags confirm that `SYN` and `FIN` flags consume exactly **1 byte of sequence number space** (`Ack = Seq + 1`), even when the payload length is `0`.
2. **Selective Acknowledgment (SACK):** Wireshark shows SACK options preventing unnecessary retransmission of already-buffered out-of-order segments during network jitter.
3. **Window Scaling (RFC 7323):** Demonstrates how scale factors (e.g., $2^8 = 256$) allow modern endpoints to expand the 16-bit window size field beyond the legacy 64 KB limit.
