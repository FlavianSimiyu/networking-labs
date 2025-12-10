Lab 01 – VLANs and Inter-VLAN Routing Using a Multilayer Switch

This lab demonstrates how to segment a network using VLANs on a Cisco 3560 multilayer switch and enable communication between those VLANs using Switch Virtual Interfaces (SVIs) and Layer 3 routing.

Objectives
- Create and name VLANs on a multilayer switch  
- Assign switchports to the correct VLANs  
- Configure SVIs to act as default gateways  
- Enable Layer 3 routing using `ip routing`  
- Verify device connectivity across VLANs using ICMP  

Concepts Demonstrated

1. VLAN Segmentation
VLANs allow logical segmentation of devices into separate broadcast domains, even when they share the same physical switch.  
In this lab:
- VLAN 10 → Sales
- VLAN 20 → IT

This reduces unnecessary broadcast traffic and improves network organization.

2. Switch Virtual Interfaces (SVIs)
SVIs provide an IP interface for each VLAN, enabling the switch to route traffic between VLANs.  
Configured:
- VLAN 10 SVI: 192.168.10.1/24
- VLAN 20 SVI: 192.168.20.1/24

These serve as the default gateways for hosts.

3. Inter-VLAN Routing
By enabling:  ip routing

…the 3560 performs Layer 3 routing, allowing devices in different VLANs to communicate.

4. Device Configuration and Verification
The lab involves:
- Assigning IP addresses and gateways  
- Testing same-VLAN and cross-VLAN communication  
- Troubleshooting gateway issues  

Outcomes
The lab demonstrated the following:

- VLAN segmentation was successfully implemented, creating two isolated broadcast domains for Sales and IT.  
- Switch Virtual Interfaces were configured correctly and functioned as operational default gateways for each subnet.  
- Inter-VLAN routing was enabled, and the multilayer switch routed traffic between VLAN 10 and VLAN 20 as expected.  
- Connectivity tests confirmed that devices could communicate both within their VLANs and across VLANs after proper gateway configuration.  
- Troubleshooting identified incorrect gateway settings on hosts as the root cause of initial inter-VLAN ping failures; correcting these settings restored full connectivity.  

These results confirm that the network behaved as designed and validated the correct implementation of VLANs, SVIs, and inter-VLAN routing.
