Lab 4: OSPF Single Area  
IP Addressing Table

Topology Overview

The lab uses a linear topology with two end hosts and three routers:

`PC0 — R0 — R1 — R2 — PC1`

---

Addressing Table

| Device | Interface | IP Address      | Subnet Mask       | Default Gateway  | Network          | Description              |
|--------|-----------|-----------------|-------------------|------------------|------------------|--------------------------|
| PC0    | fa0/0     | 192.168.10.10   | 255.255.255.0     | 192.168.10.1     | 192.168.10.0/24  | End host in LAN 1        |
| R0     | g0/0      | 192.168.10.1    | 255.255.255.0     | —                | 192.168.10.0/24  | Default gateway for PC0  |
| R0     | g0/1      | 10.0.1.1        | 255.255.255.252   | —                | 10.0.1.0/30      | Point-to-point to R1     |
| R1     | g0/0      | 10.0.1.2        | 255.255.255.252   | —                | 10.0.1.0/30      | Point-to-point to R0     |
| R1     | g0/1      | 10.0.2.1        | 255.255.255.252   | —                | 10.0.2.0/30      | Point-to-point to R2     |
| R2     | g0/0      | 10.0.2.2        | 255.255.255.252   | —                | 10.0.2.0/30      | Point-to-point to R1     |
| R2     | g0/1      | 192.168.30.1    | 255.255.255.0     | —                | 192.168.30.0/24  | Default gateway for PC1  |
| PC1    | fa0/0     | 192.168.30.10   | 255.255.255.0     | 192.168.30.1     | 192.168.30.0/24  | End host in LAN 2        |

---

 Notes

- The **10.0.1.0/30** and **10.0.2.0/30** networks are used as point-to-point links between routers to conserve IP address space.
- The **192.168.10.0/24** and **192.168.30.0/24** networks are used for the end-host LANs behind R0 and R2 respectively.
- Default gateways are configured only on the PCs; routers do not require a default gateway in this OSPF single-area design because dynamic routing is used.
