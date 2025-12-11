1. Lab Purpose

This lab introduces Network Address Translation (NAT) concepts and demonstrates how to configure and verify three NAT mechanisms on a Cisco router:
a)Static NAT
b)Dynamic NAT
c)PAT (NAT Overload)
The lab reinforces how NAT enables internal hosts to access external networks while conserving public IPv4 addresses.

2. Learning Outcomes
Upon completing this lab, the learner should be able to:
-Identify inside and outside NAT interfaces
-Configure Static NAT mappings
-Create Dynamic NAT pools and apply ACLs for traffic selection
-Configure PAT using interface overload
-Verify NAT translations and NAT statistics
-Test internal-to-external connectivity across NAT boundaries

3. Network Topology
A simple routed topology is used consisting of:
-An inside LAN network (e.g., 192.168.10.0/24)
-A Cisco router acting as the NAT device
-An outside network (e.g., 203.0.113.0/24)

Interface roles:
Interface	IP Address	NAT Role
G0/0	192.168.10.1/24	Inside
G0/1	203.0.113.1/24	Outside

4. Lab Tasks
Task 1: Configure Interface IPv4 Settings
Assign IP addresses to inside and outside interfaces
Enable the interfaces
Mark each interface with the correct NAT direction (inside/outside)

Task 2: Configure Static NAT
Map a single inside local IP (e.g., 192.168.10.10) to a dedicated public IP
Verify the static NAT entry using NAT translation commands

Task 3: Configure Dynamic NAT
Create a NAT pool of public IP addresses
Define an ACL to match inside LAN traffic
Bind the ACL to the pool using ip nat inside source list
Generate traffic and observe dynamic NAT translations

Task 4: Configure PAT (NAT Overload)
Use the router’s outside interface as the public translation address
Apply overload to support many inside hosts simultaneously
Verify PAT using translation tables and NAT statistics

Task 5: Verification and Testing
Use the following commands to confirm NAT functionality:
show ip interface brief
show ip nat translations
show ip nat statistics
ping or browser testing from inside hosts

5. Expected Results
Static NAT should create a permanent one-to-one mapping
Dynamic NAT should allocate public IPs only when traffic flows
PAT should allow multiple inside hosts to share the same global IP
NAT translation entries should appear and update during traffic
Inside hosts should successfully reach external destinations