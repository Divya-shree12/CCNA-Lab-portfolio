# Cisco CCNA Networking Lab Portfolio

Welcome to my centralized CCNA laboratory and project portfolio. This repository serves as a comprehensive record of my technical progression, architectural designs, and practical implementation files as I advance through the Cisco Certified Network Associate curriculum.

All topologies are designed, configured, and validated using Cisco Packet Tracer, focusing on industry best practices, efficient subnetting, and robust network design.

---

## 🚀 Core Competencies Demonstrated
* **Advanced IPv4 VLSM & Subnetting:** Carved a unified block into precise `/26` custom subnets to optimize host efficiency.
* **Layer 2 Switching Configuration:** Custom VLAN databases, static access ports, and 802.1Q frame tagging across transit trunk links.
* **Inter-VLAN Routing Architecture:** Implemented Router-on-a-Stick using virtual router subinterfaces to orchestrate traffic handling across localized broadcast domains.

---

## 📁 Portfolio Projects Index

### 📁 01-Multi-Interface-Inter-VLAN-Routing
* **Directory:** `01-Multi-Interface-Inter-VLAN-Routing`
* **Status:** 🟢 Completed & Validated
* **Description:** Designed a baseline multi-subnet architecture utilizing custom IPv4 VLSM (`/26` precision blocks) across distributed switches. Implemented segmented gateway routing across multiple physical interfaces (GigabitEthernet0/0 and 0/1) on a Cisco 2911 Services Router to facilitate inter-subnet communication.
* **🔗 [Click here to view the full lab documentation, screenshots, and topology files](./01-Multi-Interface-Inter-VLAN-Routing)**

### 📁 02-Router-on-a-Stick-Trunk-Consolidation
* **Directory:** `02-Router-on-a-Stick-Trunk-Consolidation`
* **Status:** 🟢 Completed & Validated
* **Description:** Advanced the local infrastructure by migrating to a consolidated Router-on-a-Stick (ROAS) topology. Optimized physical hardware usage by establishing a single-interface 802.1Q trunk link between the switch framework and a single router interface (Gig0/0), leveraging logical subinterfaces to route traffic dynamically across Sales, HR, and Marketing.
* **🔗 [Click here to view the full lab documentation, screenshots, and topology files](./02-Router-on-a-Stick-Trunk-Consolidation)**
---

## 🛠️ Tools & Environments Used
* **Simulation Software:** Cisco Packet Tracer
* **Hardware Architectures Modeled:** Cisco Catalyst 2960 Switches, Cisco ISR 2911 Routers
* **Configuration Interface:** Cisco IOS CLI
