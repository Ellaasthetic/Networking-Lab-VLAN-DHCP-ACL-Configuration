# Networking-Lab: VLAN-DHCP-NAT-ACL-Configuration
**Welcome to the Networking Lab Project to demonstrate VLAN, DHCP, NAT, and ACL Configuration**
## Project Overview
A comprehensive Packet Tracer project demonstrating core networking concepts, including:  
- VLANs (Virtual Land Area Networks)  
- Inter-VLAN Routing  
- DHCP (Dynamic Host Configuration Protocol)  
- NAT (Network Address Translation)  
- Wireless Network Configuration  
- ACLs (Access Control Lists)

This project demonstrates the configuration of a simulated network with VLANs, routing, DHCP, NAT, and ACLs. The objective of this project is to design and implement a network that meets the needs of a small organization with multiple departments. In this documentation, I will walk you through the step-by-step process of configuring the network, including VLANs, routing, DHCP, NAT, and ACLs.

## Brief Description of the used concepts and the Roles they play in the network
1. **VLANs (Virtual land Area Networks)**
- **Purpose:** Divide a network into smaller, isolated segments (VLANs) to improve organization, security, and management.
- **Role:** VLANs act as separate networks, allowing devices within a VLAN to communicate with each other but not with devices in other VLANs without routing.

2. **Routing Configuration**
- **Purpose:** Enable communication between VLANs and other networks.
- **Role:** Routers connect multiple VLANs and networks, allowing devices to communicate with each other across different VLANs.

3. **DHCP (Dynamic Host Configuration Protocol) Configuration**
- **Purpose:** Automatically assign IP addresses to devices on a network.
- **Role:** DHCP servers assign IP addresses, subnet masks, default gateways, and other network settings to devices, eliminating the need for manual configuration.

4. **NAT (Network Address Translation) Configuration**
- **Purpose:** Allow multiple devices on a private network to share a single public IP address when accessing the internet.
- **Role:** NAT translates private IP addresses to public IP addresses, enabling devices on a private network to communicate with devices on the internet.

5. **ACL (Access Control List) Configuration**
- **Purpose:** Control traffic flow between networks and devices.
- **Role:** ACLs filter traffic based on source and destination IP addresses, ports, and protocols, allowing or blocking traffic as needed.

## Tools used for this Lab
- Cisco Packet Tracer  
- Terminal (for documentation editing)  
- Git & GitHub (for version control)

## Network Topology
| Device | Quantity | 
|---------|--------|
|Router (Cisco 1941)| 1 |
|Switches (Cisco Catalyst 2960)| 2 |
|PCs | 6 |
|Server (DHCP)| 1 |
|Wireless Router (for wireless connectivity)| 1 |
|Laptop (to connect the wireless network)| 1|

## IP Address Scheme
| VLAN |	Subnet |	Gateway |	DHCP Range |
|-----------------|----------------|--------------|---------------------|
|VLAN 10(Product-Department)|192.168.10.0/24|192.168.10.1|	192.168.10.10 - 192.168.10.50|
|VLAN 20 (IT-Department)|	192.168.20.0/24|192.168.20.1|	192.168.20.10 - 192.168.20.50|
|VLAN 30 (Management)|	192.168.30.0/24|	192.168.30.1|	192.168.30.10 - 192.168.30.50|
|Wireless (VLAN 40)|	192.168.40.0/24|	192.168.40.1|	DHCP from Wireless Router|

