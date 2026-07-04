# Inter-VLAN Routing via Router-on-a-Stick (ROAS) with VLSM

A Cisco Packet Tracer project demonstrating the implementation of a multi-switch corporate Local Area Network (LAN). This project utilizes **Variable Length Subnet Masking (VLSM)** for efficient IP addressing and implements **Router-on-a-Stick (ROAS)** to achieve secure, scalable inter-VLAN routing.

## 📌 Project Overview
In an enterprise network, different departments are isolated into distinct broadcast domains (VLANs) for performance and security. However, these departments still need a way to communicate with each other. 

This project solves that challenge by using a single physical interface on a Cisco 2911 Router, carving it into logical subinterfaces, and trunking traffic across multiple Layer 2 switches (`SW1` and `SW2`) to route data seamlessly between three separate departments.

## 🛠️ Network Components & Technologies
* **Routing:** 1x Cisco 2911 Services Router (`R1`)
* **Switching:** 2x Cisco 2960 Layer 2 Switches (`SW1` & `SW2`)
* **Trunking Protocol:** IEEE 802.1Q (Dot1q)
* **IP Allocation:** Variable Length Subnet Masking (VLSM)
* **Endpoints:** 7x PCs split across different departments

## 📊 IP Addressing & VLSM Schema
The base network allocated for this design is **172.16.10.0/24**. Using a `/26` subnet mask (255.255.255.192), the network is optimized into blocks of 64 IP addresses per sub-network:

| VLAN ID | Department Name | Subnet Network | Subnet Mask | Usable Host Range | Default Gateway (Router Subinterface) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | Sales / Engineering | 172.16.10.0 /26 | 255.255.255.192 | 172.16.10.1 - 172.16.10.61 | **172.16.10.62** |
| **VLAN 20** | Human Resources | 172.16.10.64 /26 | 255.255.255.192 | 172.16.10.65 - 172.16.10.125 | **172.16.10.126** |
| **VLAN 30** | Marketing | 172.16.10.128 /26 | 255.255.255.192 | 172.16.10.129 - 172.16.10.189 | **172.16.10.190** |

## ⚙️ Key Configuration Highlights

### 1. Multi-Switch Trunking (802.1Q)
To pass tagged VLAN frames across the network infrastructure, trunk links were explicitly enabled on the interfaces connecting `SW1` to `SW2`, and `SW2` to `R1`:
```text
Switch(config)# interface <interface-id>
Switch(config-if)# switchport mode trunk
