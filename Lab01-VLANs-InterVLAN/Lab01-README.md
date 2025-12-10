# Lab 01 – VLANs + Inter-VLAN Routing (Single Multilayer Switch)

## Concept Demonstrated
This lab demonstrates:
- Creating VLANs on a multilayer switch
- Assigning switchports to VLANs
- Configuring Switch Virtual Interfaces (SVIs) for gateway IPs
- Enabling inter-VLAN routing directly on a multilayer (Layer 3) switch
- Testing communication between devices in different VLANs

## Task
Build a simple network using a single Cisco 3560 multilayer switch:

- Assign two VLANs:
  - **VLAN 10 → Sales**
  - **VLAN 20 → IT**

- Connect four PCs directly to the multilayer switch:
  - Ports for VLAN 10: **Fa0/1**, **Fa0/2**
  - Ports for VLAN 20: **Fa0/3**, **Fa0/4**

- Create SVIs on the 3560 to act as the default gateways:
  - VLAN 10 → 192.168.10.1/24
  - VLAN 20 → 192.168.20.1/24

- Enable `ip routing` to allow the multilayer switch to route between VLANs.

- Assign appropriate IP addresses and gateways to each PC.

- Verify successful inter-VLAN communication by performing ping tests between:
  - A Sales PC and an IT PC
  - PCs and their default gateways
