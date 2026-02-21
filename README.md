Enterprise Network Simulation

VLAN Segmentation, Inter-VLAN Routing, OSPF & Extended ACL

📌 Project Overview

This project simulates a small enterprise network consisting of a Head Office (HQ) and a Branch Office.

The network is designed with:

VLAN segmentation per department

Inter-VLAN routing using Router-on-a-Stick

Dynamic routing using OSPF

Traffic filtering using Extended Access Control List (ACL)

The simulation was built using Cisco Packet Tracer.

🏢 Network Architecture
HQ Network
VLAN	Department	Network Address	Gateway
10	HR	192.168.10.0/24	192.168.10.1
20	IT	192.168.20.0/24	192.168.20.1
30	GUEST	192.168.30.0/24	192.168.30.1
Branch Network
VLAN	Department	Network Address	Gateway
40	STAFF	192.168.40.0/24	192.168.40.1
🔹 VLAN Segmentation & Inter-VLAN Routing

VLANs were configured on the switch to logically separate departments.

Inter-VLAN routing was implemented using the Router-on-a-Stick method by creating subinterfaces on R1.

Example configuration:

interface fa1/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

Result:

Devices from different VLANs within HQ can communicate successfully.

🔹 OSPF Dynamic Routing

OSPF (Area 0) was implemented between R1 (HQ) and R2 (Branch) to enable dynamic route advertisement.

Reasons for using OSPF:

Scalable for larger networks

Automatic route learning

Faster convergence when topology changes

Reduced manual configuration compared to static routing

Verification commands:

show ip ospf neighbor
show ip route

Result:

R1 and R2 formed OSPF adjacency

HQ and Branch networks can communicate successfully

🔹 Extended ACL Implementation

An Extended ACL was configured to enhance network security.

Security Policy:

VLAN 30 (GUEST) is NOT allowed to access:

VLAN 10 (HR)

VLAN 20 (IT)

VLAN 30 is allowed to access Branch network

Configuration:

access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255
access-list 100 permit ip any any

interface fa1/0.30
 ip access-group 100 in

Result:

Guest VLAN traffic to HR and IT is blocked

Guest VLAN traffic to Branch remains permitted

🧪 Testing & Verification

Successful tests performed:

Inter-VLAN ping within HQ

HQ to Branch connectivity

OSPF adjacency verification

ACL restriction validation

🛠️ Skills Demonstrated

VLAN Configuration

Trunking (802.1Q)

Router-on-a-Stick

OSPF Configuration & Troubleshooting

Extended ACL Implementation

Network Design & Segmentation

Interface & Routing Troubleshooting

🚀 Conclusion

This project demonstrates the implementation of a segmented and scalable enterprise network using dynamic routing and access control policies. The design can be extended with additional services such as DHCP, NAT, redundancy, and enhanced security mechanisms.
