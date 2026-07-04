# Lab 01: Multi-Interface Inter-VLAN Routing Architecture

## ## The Network Topology
This is the full visual workspace layout with all interface links fully converged.
![Network Architecture](network_topology.png)

## ## Verification & Proof of Concept

### ### Core Routing Table (`show ip route`)
The routing engine dynamically populates its routing table using directly connected interface logic across the virtual subinterfaces.
![Routing Table](router_routing_table.png)

### ### End-to-End ICMP Ping Success Verification
Successful execution of cross-department and cross-site pings originating from PC0.
![Successful Pings](successful_pings.png)
