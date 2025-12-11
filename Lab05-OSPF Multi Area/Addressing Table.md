Lab 5: OSPF Multi-Area  
Addressing Table

This table defines all IP addressing used in the multi-area OSPF topology.  
The design includes three LANs, two GigabitEthernet backbone links (Area 0), and one serial link used for Area 1.

---

1. End Devices (PCs)

| Device | Interface | IP Address       | Subnet Mask       | Default Gateway   |
|--------|-----------|------------------|-------------------|--------------------|
| PC0    | fa0/0     | 192.168.10.10    | 255.255.255.0     | 192.168.10.1       |
| PC1    | fa0/0     | 192.168.20.10    | 255.255.255.0     | 192.168.20.1       |
| PC2    | fa0/0     | 192.168.30.10    | 255.255.255.0     | 192.168.30.1       |

---

2. Router Interfaces

| Router | Interface       | IP Address       | Subnet Mask        | Network / Purpose                         |
|--------|------------------|------------------|----------------------|--------------------------------------------|
| **R0** | g0/0            | 192.168.10.1     | 255.255.255.0        | LAN for PC0                                |
|        | g0/1            | 10.0.0.1         | 255.255.255.252      | Link to R2 (Area 0)                        |
|        | Serial          | —                | —                    | Not used                                   |
|        | g0/1            | —                | —                    |                                            |

| **R1** | g0/0            | 192.168.20.1     | 255.255.255.0        | LAN for PC1                                |
|        | s0/0/0          | 10.0.0.9         | 255.255.255.252      | Serial link to R2 (Area 1)                 |
|        | g0/1            | —                | —                    | Not used                                   |

| **R2** *(ABR)* | g0/0    | 10.0.0.2         | 255.255.255.252      | Link to R0 (Area 0)                        |
|                | g0/1    | 10.0.0.5         | 255.255.255.252      | Link to R3 (Area 0)                        |
|                | s0/0/0  | 10.0.0.10        | 255.255.255.252      | Serial link to R1 (Area 1)                 |

| **R3** | g0/0            | 10.0.0.6         | 255.255.255.252      | Link to R2 (Area 0)                        |
|        | g0/1            | 192.168.30.1     | 255.255.255.0        | LAN for PC2                                |
|        | Serial          | —                | —                    | Not used                                   |

---

3. Network Summary

| Network Address | Subnet Mask        | Purpose                                 |
|-----------------|--------------------|------------------------------------------|
| 192.168.10.0    | 255.255.255.0      | PC0 LAN (R0 LAN)                         |
| 192.168.20.0    | 255.255.255.0      | PC1 LAN (R1 LAN)                         |
| 192.168.30.0    | 255.255.255.0      | PC2 LAN (R3 LAN)                         |
| 10.0.0.0        | 255.255.255.252    | R0 ↔ R2 (Area 0)                         |
| 10.0.0.4        | 255.255.255.252    | R2 ↔ R3 (Area 0)                         |
| 10.0.0.8        | 255.255.255.252    | R1 ↔ R2 (Area 1, serial link)            |

---

4. Area Assignments

| Router | Interface(s) in Area 0                   | Interface(s) in Area 1                  |
|--------|-------------------------------------------|-------------------------------------------|
| R0     | g0/1                                      | —                                         |
| R1     | —                                         | g0/0, s0/0/0                              |
| R2     | g0/0, g0/1                                | s0/0/0                                    |
| R3     | g0/0, g0/1                                | —                                         |

R2 serves as the **Area Border Router (ABR)**, participating in both Area 0 and Area 1.

---

This addressing table provides a clear reference for configuring and validating the OSPF multi-area topology.
