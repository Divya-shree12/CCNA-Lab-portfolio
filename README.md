# Cisco CCNA Networking Lab Portfolio

Welcome to my centralized CCNA laboratory and project portfolio. This repository serves as a comprehensive record of my technical progression, architectural designs, and practical implementation files as I advance through the Cisco Certified Network Associate curriculum.

All topologies are designed, configured, and validated using Cisco Packet Tracer, focusing on industry best practices, efficient VLSM IP subnetting, and robust network design.

---

## ⚡ Core Competencies Demonstrated
* **Advanced IPv4 VLSM & Subnetting:** Carved unified address spaces into precise `/26` host subnets and `/30` point-to-point transit links to optimize host efficiency and eliminate address wastage.
* **Layer 2 Switching Configuration:** Custom VLAN databases, static access ports, and 802.1Q frame tagging across transit trunk links.
* **Inter-VLAN Routing & Layer 3 Switching:** Configured Multi-Interface, Router-on-a-Stick (ROAS), and high-speed Switch Virtual Interface (SVI) models for wire-rate inter-VLAN traffic routing.
* **Dynamic Enterprise Routing (OSPFv2):** Deployed single-area OSPF across multi-site routed backbones, optimizing routing tables with passive interfaces and default route injection.

---

## 📁 Active Laboratory Projects

### 📁 01-Multi-Interface Inter-VLAN Routing Architecture
* **Directory:** `01-Multi_Interface_Inter_VLAN_Routing`
* **Status:** 🟢 Completed & Validated
* **Description:** Designed a baseline multi-subnet architecture utilizing custom IPv4 VLSM blocks across separate switches. Implemented segmented gateway routing across multiple physical interfaces (GigabitEthernet0/0 and 0/1) on a Cisco 2911 Services Router to facilitate inter-subnet communication.
* **🔗 [Click here to view the full lab documentation, screenshots, and topology files](./01-Multi_Interface_Inter_VLAN_Routing)**

### 📁 02-Router-on-a-Stick Trunk Consolidation
* **Directory:** `02-Router-on-a-Stick-Trunk-Consolidation`
* **Status:** 🟢 Completed & Validated
* **Description:** Advanced the local infrastructure by migrating to a consolidated Router-on-a-Stick (ROAS) topology. Optimized hardware usage by establishing a single-interface 802.1Q trunk link between the switch framework and a single router interface (Gig0/0), leveraging logical subinterfaces to route traffic dynamically across Sales, HR, and Marketing domains.
* **🔗 [Click here to view the full lab documentation, screenshots, and topology files](./02-Router_on_a_Stick_Trunk_Consolidation)**

### 📁 03-Multilayer Switching SVI and Cloud Integration
* **Directory:** `03-Multilayer_Switching_SVI_and_Cloud_Integration`
* **Status:** 🟢 Completed & Validated
* **Description:** Implemented high-speed Layer 3 switching using Switch Virtual Interfaces (SVIs) on a Cisco 3650 Multilayer Switch. Established a point-to-point routed transit link (`172.16.10.192/30`) to an edge router, integrating local VLAN networks with external WAN and Cloud connectivity for end-to-end reachability.
* **🔗 [Click here to view the full lab documentation, screenshots, and topology files](./03-SVI_Multilayer_Switch_Inter_Vlan_Routing)**

### 📁 04-Single-Area OSPFv2 Dynamic Routing & Multi-Site Enterprise Scalability
* **Directory:** `04-Single_Area_OSPFv2_Dynamic_Routing`
* **Status:** 🟢 Completed & Validated
* **Description:** Scaled the enterprise architecture to support a multi-site WAN deployment using dynamic Single-Area OSPFv2 (Area 0). Interconnected a Campus Core Multilayer Switch to an Edge Gateway and a remote Branch Office via dedicated `/30` routed links, incorporating default route propagation (`default-information originate`), passive interface security boundaries, and simulated ISP return routing.
* **🔗 [Click here to view the full lab documentation, screenshots, and topology files](./04-Single_Area_OSPFv2_Dynamic_Routing)**

---

## 🛠️ Tools & Environments Used
* **Simulation Software:** Cisco Packet Tracer
* **Hardware Architectures Modeled:** Cisco Catalyst 2960 Switches, Cisco Catalyst 3650 Multilayer Switches, Cisco ISR 2911 Routers
* **Protocols & Standards:** IEEE 802.1Q, IPv4 VLSM, OSPFv2 (RFC 2328), SVI Layer 3 Switching, ICMP
* **Configuration Interface:** Cisco IOS CLI
