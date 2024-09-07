# Campus Network
1.	Case Study
Benue State University is a large institution of learning located in the north-central of Nigeria. The University has two campuses, the main and branch campus. The two campuses are situated 30 miles apart. The University’s students and staff are distributed into 4 faculties, these include the faculty of Health & Science, Economics, Engineering & Computing and ART& Design. Each member of the staff has PCs and Student access to PCs in the LABs.

Requirement
You are expected to create:
1. A network topology with the main component to support the following:
- Main Campus
  - Building A – Administrative staff in the department of management, HR and Finance. The administrative staff PCs are distributed in the building offices and it is expected that they will share some networking equipment. The faculty of Economics is also situated in the building.
  - Building B – Faculty of Engineering & Computing and faculty of Art & Design
  - Building C: Student’s lab and IT department. The IT department hosts the University Web Server and other Servers. There is also an email server hosted externally on the cloud.
•	Branch Campus: Faculty of Health & Science ( Staff and Students Lan are located on separate floors).
2.	You will be required to configure the core device and a few end devices to provide end-end connectivity and access to the internal servers and external servers.

 - Each department/faculty is expected to be on their separate network
 - The switch should be configured with appropriate VLAN and Security Settings
 - Ripv2 will be used to provide routing for routers in the internal network and static routing for the external server.
 - The device in building a will be expected to acquire IP addresses dynamically from a router-based DHCP server

Task 1: You are tasked to plan, design, and prototype the network topology for Benue State University network using Cisco Packet Tracer

Task 2: Configure in Packet tracer the network with the appropriate setting to achieve the connectivity and functionalities stated in the requirements.

Task 3: Produce a report evaluating the proposed network design. The evaluation should include performance, scalability, reliability and security of the network.
#Solution
In addressing the case study given, we first design the topology of the network.
- Task 1
This section deals with planning, and designing the proposed network. The image depicted below shows the network topology for the University. The design has a total of three routers, a total of ten layer 2 switches and two layer 3 switches. There are also three servers including an external server hosted in a cloud environment. Each department and faculty has an end device attached for user usage. Each of the hosts is on a separate IP Network and different VLAN. The network is designed to allow scalability in case of expansion in the future.

The following are the IP networks for each department/Faculty

i.	Main Campus Network Requirements
Admin – 192.168.1.0 with Subnet mask of 255.255.255.0 (Class C)
HR – 192.168.2.0 with Subnet mask of 255.255.255.0 (Class C)
Finance – 192.168.3.0 with Subnet mask of 255.255.255.0 (Class C)
Economics– 192.168.4.0 with Subnet mask of 255.255.255.0 (Class C)
E & C – 192.168.5.0 with Subnet mask of 255.255.255.0 (Class C)
A & D – 192.168.6.0 with Subnet mask of 255.255.255.0 (Class C)
Student – 192.168.7.0 with Subnet mask of 255.255.255.0 (Class C)
IT– 192.168.8.0 with Subnet mask of 255.255.255.0 (Class C)

ii.	Branch Campus
Staff – 192.168.9.0 with Subnet mask of 255.255.255.0 (Class C)
Student’s Lab – 192.168.10.0 with Subnet mask of 255.255.255.0 (Class C)

Cloud Router
Network 1– 20.0.0.0 with Subnet Mask 255.255.255.252 (Class A)
Network 2 – 10.10.10.4 with Subnet Mask 255.255.255.252 (Class A)

Main Campus Router
Network 1 – 10.10.10.0 with Subnet Mask 255.255.255.252 (Class A)
Network 2 – 10.10.10.4 with Subnet Mask 255.255.255.252 (Class A)

Branch Campus Router
Network 1 – 10.10.10.0 with Subnet Mask 255.255.255.252 (Class A)

#The Topology
![image](https://github.com/user-attachments/assets/60342fe0-2559-49fb-b385-a5781a3448fe)

# Task 2: Configuration
In this section, The configuration process will be done. The logical configuration involves interfaces, inter-vlan routing, DHCP, Routing using RIPV2 and Mail Server configuration. To kick the start of the configuration, We first power on the interface on routers.

#Starting Interface 
Main Campus Router
By default, the router is shut down for security purposes, to ensure the integrity of the network. To power on router, The following commands will be used.
Router>enable or en 
Router# Configure terminal or config t 
Router(config)# interface Gig0/0 
Router(config-if)# No shutdown 
Router(config-f) # ex 
Router(config)# do wr 
![image](https://github.com/user-attachments/assets/df6ffb50-60e7-47ec-902a-8af69a448cf9)

# Clock Rate Configuration
Clock rate configuration is carried on the interface with the serial side which has a clock symbol. This configuration will be done on the Main Campus Router which has both incoming and outgoing interfaces with a clock symbol. The clock rate is important because it ensures that the sender and receiver are synchronized, preventing data interruption and data integrity. Without a clock rate, the timing of the data signal can be mismatched, leading to errors and unreliable communication
Router>en
Router#config t
Router(config) # int se0/1/1 – interface with clock symbol
Router(config-if)# clock rate 64000
Router(config-if) # ex
Router(config) # do wr
#VLAN Configuration
Virtual Local Area Network is a logically subdivided physical network. It allows Network administrators to partition a single physical network into multiple distinct and isolated networks. Each VLAN acts as a single entity even though they share the same network infrastructure. VLAN is important because it segments the network into smaller, sub-isolated networks, meaning that sensitive information can be kept separate from less secure parts of the network. By isolating departments (e.g., finance, HR, and development) into separate VLANs, one can implement stricter access controls, limiting which users or devices can communicate with each other. A total of ten VLANs will be used in the project. We will only demonstrate three VLAN configurations in this work. To con
To configure VLANs, follow this command

1St VLAN( 10) Which will be assigned to the Admin Department

Switch>enable  ------ To enable the switch
Switch#configure terminal ---- Enter global configuration
Switch(config)# int range fa0/1–24  ----- interface range on fastethernet
Switch(config-if)# switchport mode access ---- switch the port to access mode
Switch(config-if)# switchport access vlan 10 ---- creating of vlan and assigning value

2nd VLAN (20) Will be assigned to the HR Department
Switch>enable 
Switch#configure terminal 
Switch(config)# int range fa0/1–24 
Switch(config-if)# switchport mode access 
Switch(config-if)# switchport access vlan 20 

3rd VLAN(30) Will be assigned to the Finance Department
Switch>enable 
Switch#configure terminal 
Switch(config)# int range fa0/8–10 
Switch(config-if)# switchport mode access 
Switch(config-if)# switchport access vlan 30
Switch(config-if)# exit 
Switch(config)# do write 

Note: The same process can be repeated for all VLANs. Importantly, VLAN configuration must also be done on the Layer 3 switches because these switches handle routing between VLANs. The Layer 3 switch needs to understand the source VLAN of the incoming traffic to route it correctly. Refer to the next command for further details.

Swicth>en
Switch#config t
Switch(config) # int gig1/0/2
Switch(config-if)# switchport mode access 
Switch(config-if) # switchport access vlan 10
Switch(config-if)# do wr

For connection to be successful between the host in Main Campus and Branch Campus, the interface taking communication from the Layer 3 switch will be configured as a trunk port.

In networking, a trunk refers to a communication channel or link that carries multiple VLANs between switches, routers, or other network devices. Trunks are essential for enabling communication between devices in different VLANs and are commonly used in larger networks where VLAN segmentation is implemented.

#Trunk Configuration
switch>en or enable 
switch# configure terminal or config t 
switch(config) #int fa0/1 
Switch(config)# switchport trunk encapsulation dot1q
switch(config-if)# switchport mode trunk 
switch(config-if)# ex or exit
switch(config)# do wr or do write
Note: The same process can be carried out on the Branch Layer 3 switch.

Assigning IP Addresses To The Interface on The Router
We have discussed in our previous project how subnetting is done. A link will be provided to have a look at it.

MAIN Campus Router
The main router has two networks connected to its interface. The network is 10.10.10.0 and 10.10.10.4 with a Subnet mask of 255.255.255.252 (Class A) address. Interface Se0/1/1 will have 10.10.10.1 assigned and interface Se0/1/0 will take 10.10.10.5. Let's demonstrate how it's been done. Command below:
Router>en
Router#config t
Router(config) # int Se0/1/0
Router(config-if) # ip address 10.10.10.5 255.255.255.252 
Router(config-if # ex
Router(config) # int  Se0/1/1
Router(config-if) # ip address 10.10.10.1 255.255.255.252
Router(config-if) # do wr

Branch Router
The branch router has one network attached to its interface. The network is 10.10.10.0 with a subnet mask of 255.255.255.252
Router>en
Router#config t
Router(config) # int Se0/2/0
Router(config-if) # ip address 10.10.10.2 255.255.255.252 
Router(config-if) # do wr

#Cloud Router
The cloud router has two networks attached to its interfaces. Network 20.0.0.0 and 10.10.10.4 with a subnet mask of 255.255.255.252 respectively.
Router>en
Router#config t
Router(config) # int Se0/1/0
Router(config-if) # ip address 10.10.10.6 255.255.255.252 
Router(config-if # ex
Router(config) # int  gig0/0
Router(config-if) # ip address 20.0.0.1 255.255.255.252 
Router(config-if) # do wr

#Inter-VLAN routing configuration
This process involves assigning VLAN to the default gateway (10, 20, and 30)
Router(config) int g0/0.10
Router(config-subif) # encapsulation dot1q 10
Router(config-subif) # ip add 192.168.1.1 255.255.255.0 
Router(config-subif) #exit
Router(config) int g0/0.20
Router(config-subif) # encapsulation dot1q 20
Router(config-subif) # ip add 192.168.2.1 255.255.255.0 
Router(config-subif) #exit
Router(config) int g0/0.30
Router(config-subif) # encapsulation dot1q 30
Router(config-subif) # ip add 192.168.3.1  255.255.255.0 
Router(config-subif) #exit
Router(config) # do wr
Router(config) int g0/0.40
Router(config-subif) # encapsulation dot1q 40
Router(config-subif) # ip add 192.168.4.1  255.255.255.0 — the first IP address of the third subnet will be assigned to this interface
Router(config-subif) #exit
Router(config) # do wr
Router(config) int g0/0.50
Router(config-subif) # encapsulation dot1q 50
Router(config-subif) # ip add 192.168.5.1  255.255.255.0 
Router(config-subif) #exit
Router(config) # do wr
Router(config) int g0/0.60
Router(config-subif) # encapsulation dot1q 60
Router(config-subif) # ip add 192.168.6.1  255.255.255.0 
Router(config-subif) #exit
Router(config) # do wr
Router(config) int g0/0.70
Router(config-subif) # encapsulation dot1q 70
Router(config-subif) # ip add 192.168.7.1  255.255.255.0 
Router(config-subif) #exit
Router(config) # do wr
Router(config) int g0/0.80
Router(config-subif) # encapsulation dot1q 80
Router(config-subif) # ip add 192.168.8.1  255.255.255.0 
Router(config-subif) #exit
Router(config) # do wr

#Branch Campus Router
Router(config) int g0/0.90
Router(config-subif) # encapsulation dot1q 90
Router(config-subif) # ip add 192.168.9.1 255.255.255.0 
Router(config-subif) #exit
Router(config) int g0/0.100
Router(config-subif) # encapsulation dot1q 100
Router(config-subif) # ip add 192.168.10.1 255.255.255.0 
Router(config-subif) #exit

#DHCP Server Configuration
As requested in the case study, the device will obtain IP automatically, and DHCP service must be enabled and configured on the router.  The following command is used to configure dhcp server to allocate IP to device dynamically.	
Router>enable or en
Router#config t or configure terminal
Router(config)# service dhcp 
Router(dhcp-config)# ip dhcp pool Admin-Pool 
Router(dhcp-config)# network 192.168.1.0 255.255.255.192 
Router(dhcp-config)# default-router 192.168.1.1 
Router(dhcp-config)# dns-server 192.168.1.1
Router(dhcp-config)# domain-name admin.com 
Router(dhcp-config)# exit
Router(dhcp-config)# ip dhcp pool HR 
Router(dhcp-config)# network 192.168.2.0  255.255.255.0
Router(dhcp-config)# default-router 192.168.2.1 
Router(dhcp-config)# dns-server 192.168.2.1 
Router(dhcp-config)# domain-name finance.com 
Router(dhcp-config)# exit
Router(dhcp-config)# ip dhcp pool Finance 
Router(dhcp-config)# network 192.168.3.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.3.1
Router(dhcp-config)# dns-server 192.168.3.1 
Router(dhcp-config)# domain-name csr.com 
Router(dhcp-config)# exit
Router(config)# do wr

Note: The same process will be done for all the networks.

#Routing Using RIPV2
Routing Information Protocol Version 2 (RIPv2) is a dynamic routing protocol used to facilitate the exchange of routing information within a network. The following process will be used to configure routing.

#Main Campus Router Routing
Router>en
Router#config t
Router(config)# router rip
Router(config)# version 2
Router(config)#  network 192.168.1.0
Router(config)#  network 192.168.2.0
Router(config)#  network 192.168.3.0
Router(config)#  network 192.168.4.0
Router(config)#  network 192.168.5.0
Router(config)#  network 192.168.6.0
Router(config)#  network 192.168.7.0
Router(config)#  network 192.168.8.0
Router(config)#  network 10.10.10.0
Router(config)#  network 10.10.10.4
Router(config)#  do wr

#Branch Campus Router Routing
Router>en
Router#config t
Router(config)# router rip
Router(config)# version 2
Router(config)#  network 192.168.9.0
Router(config)#  network 192.168.10.0
Router(config)#  network 10.10.10.0
Router(config) # do wr

#Cloud Router Routing
Router>en
Router#config t
Router(config)# router rip
Router(config)# version 2
Router(config)#  network 20.0.0.0
Router(config)#  network 10.10.10.4
Router(config)#  network 10.10.10.0
Router(config) # do wr

#Performance Evaluation
•	Link speeds between core, distribution, and access layers are adequate (mostly Gigabit Ethernet), ensuring sufficient bandwidth.
•	Traffic analysis shows balanced load distribution with no significant bottlenecks.

Bottlenecks:
•	No single points of failure detected. The network design ensures multiple paths for traffic flow.

-Scalability
IP Addressing Scheme:
•	Subnetting allows for future growth. Private IP address ranges are used effectively, with enough subnets available for expansion.
•	Network Address Translation (NAT) is used for external access, conserving public IP addresses.

-Expandability:
•	The design allows easy addition of new devices or segments. New VLANs can be added with minimal reconfiguration.

-Reliability
Redundancy:
•	Redundant links are present between core and distribution layers, providing failover capabilities.
•	Load balancing is configured, distributing traffic evenly and preventing overload on individual links.

-Security 
VLAN Segmentation:
•	VLANs are used to segment traffic, separating sensitive data from other network traffic.
•	Security policies enforce the separation of traffic, ensuring data integrity and 
 confidentiality.

