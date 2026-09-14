# Network Topology Project
## Overview
This project models a scalable enterprise network architecture using Cisco Packet Tracer. The design features two distinct Local Area Networks (LANs) connected across a redundant, four-router core network. Utilizing a `/27` CIDR subnet mask across all network segments, the architecture demonstrates efficient IP address space management, gateway configuration, and path redundancy.
## Key Features & Architecture
* **Variable Length Subnet Masking (VLSM):** Implemented `/27` subnets (`255.255.255.224`), providing up to 30 usable host IP addresses per subnet segment to prevent address wastage.
* **Redundant Core Network:** Configured a diamond-shaped router topology (`Router3`, `Router0`, `Router2`, `Router1`) to enable dynamic path selection and failover capability in the event of a link failure.
* **LAN Segmentation:** 
  * **LAN A (Left):** Connects workstations (`PC0`, `PC1`) via `Switch0` to local default gateway `192.168.1.1` (`Router3`).
  * **LAN B (Right):** Connects workstations (`PC2`) and shared network peripherals (`Printer0`) via `Switch1` to default gateway `192.168.1.97` (`Router1`).

## Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway | Subnet Range |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PC0** | FastEthernet0 | `192.168.1.2` | `255.255.255.224` | `192.168.1.1` | `192.168.1.0/27` |
| **PC1** | FastEthernet0 | `192.168.1.3` | `255.255.255.224` | `192.168.1.1` | `192.168.1.0/27` |
| **Router3** | FastEthernet1/0 | `192.168.1.1` | `255.255.255.224` | N/A | LAN Gateway |
| **Router3** | FastEthernet0/0 | `192.168.1.33` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router0** | FastEthernet0/0 | `192.168.1.34` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router3** | FastEthernet7/0 | `192.168.1.162` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router2** | FastEthernet1/0 | `192.168.1.161` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router0** | FastEthernet1/0 | `192.168.1.65` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router1** | FastEthernet0/0 | `192.168.1.66` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router2** | FastEthernet0/0 | `192.168.1.129` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router1** | FastEthernet5/0 | `192.168.1.130` | `255.255.255.224` | N/A | Point-to-Point Link |
| **Router1** | FastEthernet1/0 | `192.168.1.97` | `255.255.255.224` | N/A | LAN Gateway |
| **PC2** | FastEthernet0 | `192.168.1.98` | `255.255.255.224` | `192.168.1.97` | `192.168.1.96/27` |
| **Printer0** | FastEthernet0 | `192.168.1.99` | `255.255.255.224` | `192.168.1.97` | `192.168.1.96/27` |

## Technologies Used

* **Simulator:** Cisco Packet Tracer
* **Addressing Scheme:** IPv4 / VLSM (`/27` Class C Subnetting)
* **Routing Protocols:** Static / Dynamic Routing (OSPF / EIGRP / RIP)
* **Hardware Simulated:** Cisco Routers (`Router-PT`), Cisco Switches (`Switch-PT`), End Devices (PCs, Printer)

## Verification & Testing

1. **ICMP Connectivity:** Executed `ping` commands from `PC0` to `PC2` and `Printer0` to verify full end-to-end packet transmission across the core routers.
2. **Path Tracing:** Used `traceroute` (`tracert`) to map packet traversal through redundant paths (`Router3` -> `Router0` -> `Router1`).
3. **Failover Simulation:** Manually disabled interface `Fa0/0` on `Router0` to confirm traffic dynamically rerouted through `Router2` to reach `Router1` without network outage.
