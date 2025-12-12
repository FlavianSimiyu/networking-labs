Pre-Configuration Verification
HSRP Redundancy

Purpose
This document records the **network state before configuring any First Hop Redundancy Protocols (FHRPs)**.
The objective was to confirm correct physical connectivity, IP addressing, and basic Layer 2/Layer 3 communication prior to introducing HSRP, VRRP, or GLBP.

---

Device Inventory
- Routers: R0, R1
- Switch: S0
- End Devices: PC0, PC1, PC2, PC3

---

IP Addressing (Baseline)

LAN Network
- Network: 192.168.10.0/24
- Intended Virtual Gateway (not yet configured): 192.168.10.1

Router Interfaces
| Device | Interface | IP Address | Status |
|------|----------|------------|--------|
| R0 | G0/0 | 192.168.10.2/24 | Up / Up |
| R1 | G0/0 | 192.168.10.3/24 | Up / Up |

PCs
| PC | IP Address | Subnet Mask | Default Gateway |
|----|-----------|-------------|-----------------|
| PC0 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC1 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC2 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| PC3 | 192.168.10.13 | 255.255.255.0 | 192.168.10.1 |

---

Router Interface Status Verification

R0 – show ip interface brief
```
GigabitEthernet0/0     192.168.10.2    up     up
GigabitEthernet0/1     unassigned      down   down
GigabitEthernet0/2     unassigned      down   down
Vlan1                  unassigned      down   down
```

R1 – show ip interface brief
```
GigabitEthernet0/0     192.168.10.3    up     up
GigabitEthernet0/1     unassigned      down   down
GigabitEthernet0/2     unassigned      down   down
Vlan1                  unassigned      down   down
```

---

Connectivity Verification (Before FHRP)

PC0 Ping Tests

**Ping R0**
```
ping 192.168.10.2
Success rate: 100%
```

**Ping R1**
```
ping 192.168.10.3
Success rate: 100%
```

**Ping Another PC**
```
ping 192.168.10.11
Success rate: 100%
```

**Ping Virtual IP (Expected Failure)**
```
ping 192.168.10.1
Request timed out (100% loss)
```

---

Pre-Configuration Summary
- Physical connectivity between routers, switch, and PCs is correct.
- IP addressing is correctly applied to all devices.
- End-to-end LAN communication is functional.
- The virtual gateway address (192.168.10.1) is not reachable, as expected.

The network is in a stable baseline state and ready for FHRP configuration.

---

Next Step
Proceed to configure **HSRP** to introduce the virtual default gateway and redundancy.
