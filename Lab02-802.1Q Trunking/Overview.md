Lab 2 Overview – Router-on-a-Stick (802.1Q Trunking)

This lab demonstrates how to enable inter-VLAN communication using a single physical router interface configured with 802.1Q subinterfaces (Router-on-a-Stick). A Layer 2 switch is used to create VLANs, and the router provides Layer 3 routing between them over an 802.1Q trunk link.

Devices Used
- 1 × Router (G0/0 connected to the switch)
- 1 × Switch (Fa0/1 used as the trunk port)
- 2 × PCs (one in each VLAN)

VLANs and IP Networks
- VLAN 10 – 192.168.10.0/24 (PC1)
- VLAN 20 – 192.168.20.0/24 (PC2)

High-Level Steps
1. Create VLAN 10 and VLAN 20 on the switch.
2. Assign Fa0/2 (PC1) to VLAN 10 and Fa0/3 (PC2) to VLAN 20.
3. Configure Fa0/1 on the switch as an 802.1Q trunk carrying VLANs 10 and 20.
4. Configure G0/0.10 and G0/0.20 subinterfaces on the router with dot1Q encapsulation and IP addresses.
5. Configure PC IP addresses and default gateways.
6. Verify inter-VLAN communication using ping tests.
