# Networking-Lab: VLAN-DHCP-NAT-ACL-Configuration
**Welcome to the Networking Lab Project to demonstrate VLAN, DHCP, NAT, and ACL Configuration**
## Project Overview
A comprehensive Packet Tracer project demonstrating core networking concepts, including:  
- VLANs (Virtual Land Area Networks)  
- Inter-VLAN Routing  
- DHCP (Dynamic Host Configuration Protocol)   
- ACLs (Access Control Lists)

This project demonstrates the configuration of a simulated network with VLANs, routing, DHCP, and ACLs. The objective of this project is to design and implement a network that meets the needs of a small organization with multiple departments. In this documentation, I will walk you through the step-by-step process of configuring the network, including VLANs, routing, DHCP,and ACLs.

## Brief Description of the used concepts and the Roles they play in the network
1. **VLANs (Virtual land Area Networks)**
- **Purpose:** Segment a network into smaller, isolated segments (VLANs) to improve organization, security, and management.
- **Role:** VLANs act as separate networks, allowing devices within a VLAN to communicate with each other but not with devices in other VLANs without routing.

2. **Routing Configuration**
- **Purpose:** Enable communication between VLANs and other networks.
- **Role:** Routers connect multiple VLANs and networks, allowing devices to communicate with each other across different VLANs.

3. **DHCP (Dynamic Host Configuration Protocol) Configuration**
- **Purpose:** Automatically assign IP addresses to devices on a network.
- **Role:** DHCP servers assign IP addresses, subnet masks, default gateways, and other network settings to devices, eliminating the need for manual configuration.

4. **ACL (Access Control List) Configuration**
- **Purpose:** Control traffic flow between networks and devices.
- **Role:** ACLs filter traffic based on source and destination IP addresses, ports, and protocols, allowing or blocking traffic as needed.

## Tools used for this Lab
- Cisco Packet Tracer  
- Virtual Studio Code Terminal (for documentation editing)  
- Git & GitHub (for version control)

## Network Topology
| Device | Quantity | Purpose |
|---------|--------|------------------|
|Router (Cisco 2911)| 1 | Inter-VLAN Routing, DHCP & ACLs Configurations |
|Multilayer Switch (3650-24PS) | Central distribution/trunk switch
|Switches (Cisco Catalyst 2960)| 3 | Connect end devices, assign VLANs, forward traffic to trunk uplinks
|Laptops | 8 | End devices |

## IP Address Scheme
| VLAN |	Subnet |	Gateway |	DHCP Range |
|-----------------|----------------|--------------|---------------------|
|VLAN 10(Operations-Department)|192.168.10.0/24|192.168.10.1|	192.168.10.11 - 192.168.10.50|
|VLAN 20 (Finance-Department)|	192.168.20.0/24|192.168.20.1|	192.168.20.11 - 192.168.20.50|
|VLAN 30 (HR-Department)|	192.168.30.0/24|	192.168.30.1|	192.168.30.11 - 192.168.30.50|

# Step-by-Step Configuration of the Simulated Network in Cisco Packet Tracer
## I. Network Design
### STEP 1: Open Cisco Packet Tracer and Set Up the Topology
- Launch Cisco Packet Tracer.
On the open blank space: 
- Click "End Devices" > click and drop 8 Laptops into the setup 
- Click "Switches" under Networking devices > click and drop:
    - 1 Multilayer Switch (3650-24PS)
    - 3 Access Switches (2960-24TT)
- Click "Routers" under Networking devices> click and drop Router (2911)

### STEP 2: Physically connect the devices 
Use the “Connections” lightning icon on the left:
Choose "first cable" to automatically choose connection type for the devices (Access Switches and laptops connection) 

**Connect:**
Each PC to a port on an Access Switch 
   - 3 Laptops to Switch 1
   - 2 Laptops to Switch 2 
   - 3 Laptops to Switch 3

**Connect:** 
Each Access Switch to the Multilayer Switch using a Copper Cross-Over cable 
   - Switch 1 - Fa0/1  to Multilayer Switch - Gig1/0/1
   - Switch 2 - Fa0/1  to Multilayer Switch - Gig1/0/2
   - Switch 3 - Fa0/1  to Multilayer Switch - Gig1/0/3

**Connect:** 
Multilayer Switch to the Router using a copper straight-through cable 
   - Router - (Gig0/1) to Multilayer Switch  - (Gig1/0/4)

### STEP 3: Turn on the Multilayer Switch 
 - Click on the Multilayer Switch 
 - On the physical session, click on AC-POWER-SUPPLY and drag to an empty space in the Switch Physical Device View

### STEP 4: Create VLANs and assign ports on the Access Switches (2960-24TT)
**Create VLAN 10 on Switch 1**
- Click on the Switch1 device 
- enter into the CLI 

``` Switch>enable 
Switch # configure terminal 
Switch (config) #vlan 10
Switch (config-vlan)# name Operations-Department 
Switch (config-vlan)# exit ```

**Assign Ports to VLAN 10 - Fa0/1 -The port you choose on the Access Switch that connects to the Multilayer Switch** 

```Switch # configure terminal
Switch (config)# int range fa0/2-24
Switch (config-if-range)# switchport mode access 
Switch (config-if-range)# switchport access vlan 10
Exit```

**Make the port on the switch a trunk (Switch 1)**  

```Switch (config)# int fa0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Switch (config)# do wr
Switch (config)# exit```

**Create VLAN 20 on Switch 2** 
- Click on the Switch 2 device 
- enter into the CLI

```Switch>enable 
Switch # configure terminal 
Switch (config)# vlan 20
Switch (config-vlan)# name Finance-Department
Switch (config-vlan)# exit```

**Assign Ports to VLAN 20 - Fa0/1 -( The port you choose on the Access Switch that connects to the Multilayer Switch)**

```Switch # configure terminal
Switch (config)# int range fa0/2-24
Switch (config-if-range)# switchport mode access 
Switch (config-if-range)# switchport access vlan 20
Exit```

**Make the port on the switch a trunk  (Switch 2)** 

Switch (config)# int fa0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Switch (config)# do wr
Switch (config)# exit

Create VLAN 30 on Switch 3
- Click on the Switch 2 device 
- enter into the CLI

Switch>enable 
Switch # configure terminal 
Switch (config)# vlan 30
Switch (config-vlan)# name HR-Department
Switch (config-vlan)# exit
Switch (config) #exit
Switch # show vlan brief (to see your created vlans)

Assign Ports to VLAN 30 - Fa0/1 -( The port you choose on the Access Switch that connects to the Multilayer Switch)

Switch # configure terminal
Switch (config)# int range fa0/2-24
Switch (config-if-range)# switchport mode access 
Switch (config-if-range)# switchport access vlan 10
Exit

Make the port on the switch a trunk (Switch 3) 

Switch (config)# int fa0/1
Switch(config-if)# switchport mode trunk
Switch(config-if)# exit
Switch (config)# do wr
Switch (config)# exit

STEP 5: Configure all VLANs on the Multilayer Switch 

Create VLANs: Multilayer Switch 
- click on the Multilayer Switch device 
- enter into the CLI 

Switch >enable 
Switch # configure terminal 
Switch (config) #vlan 10
Switch (config-vlan)# name Operations-Department 
Switch (config-vlan)# exit
Switch (config)# vlan 20
Switch (config-vlan)# name Finance-Department
Switch (config-vlan)# exit
Switch (config)# vlan 30
Switch (config-vlan)# name HR-Department
Switch (config-vlan)# exit
Switch (config) #exit
Switch # show vlan brief (to see your created vlans)

STEP 6: Configure the link ports on the Multilayer Switch as Trunks
(The port you choose on the Multilayer that connects to the Access Switches and Router)

Switch (config) int range gig1/0/1-4 
Switch (config-if-range)# switchport mode trunk
Switch (config-if-range)# exit 
Switch (config) do wr
Exit

STEP 7 : Create Subinterfaces on the Router
Identify the interface connected to the Router  (Gig0/1) 

Router > enable
Router # configure terminal
Router (config) # int gig0/1
Router (config-if) no shutdown 
Router (config-if) exit

Create Subinterfaces according to the VLAN IDs (10, 20, 30)

Router CLI 

Subinterface for VLAN 10: 

Router > enable
Router # configure terminal
Router (config) # int gig0/1.10 
encapsulation dot1Q 10
Ip address 192.168.10.1 255.255.255.0 

Subinterface for VLAN 20:

Router (config) # int gig0/1.20 
encapsulation dot1Q 20
Ip address 192.168.20.1 255.255.255.0 

Subinterface for VLAN 30:

Router (config) # int gig0/1.30 
encapsulation dot1Q 30
Ip address 192.168.30.1 255.255.255.0 

STEP 8: CREATE DHCP POOLS ON THE ROUTER CLI

Operations-Department Pool for VLAN 10

Router > enable
Router # configure terminal
Router (config) # service dhcp
Ip dhcp pool operations-depart
network 192.168.10.0 255.255.255.0 
default-router 192.168.10.1 
dns-server 192.168.10.1 
exit 

Finance-Department Pool for VLAN 20

Router > enable
Router # configure terminal
Router (config) # service dhcp
Ip dhcp pool operations-depart
network 192.168.20.0 255.255.255.0 
default-router 192.168.20.1 
dns-server 192.168.20.1 
exit 

HR-Department Pool for VLAN 30

Router > enable
Router # configure terminal
Router (config) # service dhcp
Ip dhcp pool operations-depart
network 192.168.30.0 255.255.255.0 
default-router 192.168.30.1 
dns-server 192.168.30.1 
exit 
do wr 

STEP 9: Exclude ranges of Ip addresses that should not be assigned dynamically. 

Router (config)# ip dhcp excluded-address 192.168.10.1 192.168.10.10
Router (config)# ip dhcp excluded-address 192.168.20.1 192.168.20.10
Router (config)# ip dhcp excluded-address 192.168.30.1 192.168.30.10
do wr 
exit

STEP 10 : Enable DHCP on the End devices (Laptops) 
Click on the laptop device > Choose Desktop > IP Configuration > change from static to DHCP 

STEP 11: Test Connectivity (intervlan routing) by Pinging devices within and outside of a vlan.  

Click on the laptop device > Choose Desktop > Command Line 

Ping 192.168.10.12 
Ping 192.168.20.11
Ping 192.168.30.13

From laptop 1 >

Repeat for other laptop devices to test connectivity across the vlans. 

STEP 12: Access Control  Lists  (ACLs ) Configuration on Router

Goal: 
- Blocks HTTP traffic from HR (VLAN 30) to both Operations (VLAN 10) and Finance (VLAN 20)
-  Allows all other traffic (including pings, DNS, HTTPS, file shares, etc.) between all VLANs

We will be configuring an extended ACLs. 

On Router: 

Router> enable
Router# configure terminal

! Deny HTTP from HR to Operations

Router(config)# access-list 110 deny tcp 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255 eq 80

! Deny HTTP from HR to Finance

Router(config)# access-list 110 deny tcp 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255 eq 80

! Allow all other traffic

Router(config)# access-list 110 permit ip any any

Apply the ACL to the HR VLAN Interface (Subinterface on Router)

Router(config)# interface gig0/1.30
Router(config-subif)# ip access-group 110 in
Router(config-subif)# exit

STEP 13: Test the ACLs Rules 

From a laptop in the HR department (VLAN 30):

Open Desktop > Web Browser

Enter http://192.168.10.12 (an assumed web server in the Operations VLAN)

Result: Request Timeout
Interpretation: ACL rule successfully blocking http traffic to vlan 10 & 20

Ping Tests: 

ping 192.168.10.12 → should work (ICMP is allowed) from the HR laptop in the command line
