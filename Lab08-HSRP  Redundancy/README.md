Overview
This lab demonstrates the implementation and verification of **First Hop Redundancy Protocols (FHRPs)** in a routed network. I configured and tested **HSRP** to provide default gateway redundancy and, in the case of GLBP, gateway load balancing. The objective was to ensure uninterrupted end-host connectivity during gateway failures.

---

Objectives
- Configure HSRP to provide default gateway redundancy
- Verify correct protocol operation using show commands
- Test failover behavior and confirm end-to-end connectivity

---

Network Topology
The topology consists of:
- Two Layer 3 devices acting as default gateways
- One or more access switches
- End hosts configured with a virtual IP as the default gateway

The topology diagram is included in the repository.

---

Addressing Scheme
All end hosts are configured to use the **virtual IP address** provided by the redundancy protocol as their default gateway.  
Detailed addressing information is documented in the addressing table file.

---

Lab Tasks Performed

1. Pre-Configuration Verification
Before applying any redundancy configuration, I verified:
- Interface status and IP addressing
- VLAN and SVI configuration
- Routing table entries
- End-to-end connectivity using ping tests

---

2. HSRP Configuration
I configured HSRP on the two gateway devices by:
- Assigning a shared virtual IP address
- Setting device priorities to determine the Active and Standby roles
- Enabling preemption to ensure the preferred router regains Active status

I verified HSRP operation using appropriate show commands and confirmed successful failover by simulating a gateway failure.



Verification and Testing
Throughout the lab, I verified protocol behavior using:
- Interface and routing show commands
- FHRP-specific show commands
- End-host ping tests before and after simulated failures

All redundancy mechanisms functioned as expected, and no loss of connectivity was observed during failover tests.

---

