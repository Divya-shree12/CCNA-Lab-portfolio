# Enterprise Campus Core & High-Availability Network Simulation

> **Status:** 🚧 Active Development / Engineering In Progress  
> **Simulation Platform:** Cisco Packet Tracer  
> **Target Completion:** Under Active Sprint

---

## 📌 Project Overview
This project focuses on designing, staging, and verifying a multi-tier, fault-tolerant enterprise campus network from the access layer up to the simulated public edge. Built to demonstrate core competencies required for Junior Network Engineering and NOC roles, the topology follows standard enterprise design principles emphasizing redundancy, sub-second failover, protocol-driven segmentation, and secure perimeter translation.

---

## 📐 Network Architecture & Design Goals

### 1. High Availability & Switching Fabric
* **FHRP Gateway Redundancy:** Deploying **HSRP (Hot Standby Router Protocol)** across dual Cisco Catalyst 3560 Multilayer Switches (`MLS0` and `MLS1`) to provide zero-impact default gateway failover for end stations via shared Virtual IPs (VIPs).
* **Link Aggregation:** Bundling dual inter-switch links between distribution switches into an **IEEE 802.3ad LACP (Port-Channel)** trunk to increase throughput and eliminate single points of failure.
* **Layer 2 Segmentation:** Defining distinct broadcast domains for corporate users, management, and guests across access switch `Switch2` with IEEE 802.1Q trunking.

### 2. Layer 3 Routing & Transit
* **Routed Core Boundaries:** Establishing dedicated `/30` point-to-point Layer 3 transit links between distribution multilayer switches and the perimeter edge router (`Router1`).
* **Dynamic Interior Routing:** Deploying single-area **OSPFv2 (Area 0)** to distribute campus SVI networks and transit routes dynamically while suppressing unnecessary routing overhead on access VLANs via passive interfaces.

### 3. Edge Perimeter & Services
* **Perimeter NAT/PAT:** Configuring Port Address Translation (NAT Overload) on `Router1` to bridge internal RFC 1918 private subnets out to an ISP public boundary (`203.0.113.0/30`).
* **Centralized Network Services:** Integrating an internal enterprise services server providing dynamic IP configuration across broadcast domains via **DHCP Relay (`ip helper-address`)**, internal DNS resolution, and NTP synchronization.
* **Security Enforcement:** Implementing standard and extended Access Control Lists (ACLs) to enforce zero-trust isolation between guest users and core internal resources.

---

## 🗺️ Addressing Plan (RFC 1918 & Public Transits)

| Segment / Function | Subnet / Mask | Gateway / VIP | Notes |
| :--- | :--- | :--- | :--- |
| **ISP Transit (R0 - R1)** | `203.0.113.0/30` | `203.0.113.1` | Simulated public edge link |
| **External Services (R0 - SVR1)** | `203.0.113.4/30` | `203.0.113.5` | Public simulated test server |
| **Transit Link 1 (R1 - MLS0)** | `192.168.1.0/30` | Point-to-Point | Routed L3 connection |
| **Transit Link 2 (R1 - MLS1)** | `192.168.1.4/30` | Point-to-Point | Routed L3 connection |
| **VLAN 10 (Corporate Data)** | `192.168.10.0/24` | `192.168.10.254` | HSRP Active on MLS0 |
| **VLAN 20 (Management)** | `192.168.20.0/24` | `192.168.20.254` | HSRP Active on MLS0 |
| **VLAN 30 (Guest Network)** | `192.168.30.0/24` | `192.168.30.254` | HSRP Active on MLS0 |
| **VLAN 5 (Services / SVR0)** | `192.168.5.0/24` | `192.168.5.1` | Central DHCP / DNS Server |

---

## 🛠️ Implementation Roadmap & Current Progress

- [x] Topology placement and device cabling (2911 Routers, 3560 MLS, 2960 Access)
- [x] IPv4 subnetting plan and transit carve-outs
- [x] Layer 2 VLAN database creation and 802.1Q trunking
- [x] LACP EtherChannel (Po1) configuration and member synchronization
- [x] HSRP (v2) standby group initialization and virtual gateway definition
- [ ] Layer 3 routed uplink configuration to perimeter router
- [ ] OSPFv2 dynamic routing configuration and adjacency convergence
- [ ] DHCP Relay (`ip helper-address`) deployment for centralized IP management
- [ ] Edge PAT (NAT Overload) deployment on perimeter gateway
- [ ] Extended ACL deployment for network isolation and verification

---

## 📁 Repository Structure (Upcoming)
* `/configs/` — Full running configurations for all routers and switches (`.txt`)
* `/topology/` — Cisco Packet Tracer lab file (`.pkt`) and export diagrams
* `/verification/` — CLI validation logs (`show ip route`, `show standby brief`, `show etherchannel summary`, ping tests)
