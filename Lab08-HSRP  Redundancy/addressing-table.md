 Addressing Table
HSRP

This addressing table documents the IP addressing used in the Lab 8 redundancy topology.

---

Network Summary
- LAN Network: 192.168.10.0/24
- Virtual Default Gateway: 192.168.10.1

---

Router Addressing

| Device | Interface | IP Address | Subnet Mask | Notes |
|------|----------|------------|-------------|-------|
| R0 | GigabitEthernet0/0 | 192.168.10.2 | 255.255.255.0 | LAN-facing interface |
| R1 | GigabitEthernet0/0 | 192.168.10.3 | 255.255.255.0 | LAN-facing interface |

---

End Device Addressing

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|------|----------|------------|-------------|-----------------|
| PC0 | FastEthernet0 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC1 | FastEthernet0 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC2 | FastEthernet0 | 192.168.10.12 | 255.255.255.0 | 192.168.10.1 |
| PC3 | FastEthernet0 | 192.168.10.13 | 255.255.255.0 | 192.168.10.1 |

---

Virtual IP Addressing

| Protocol | Group | Virtual IP |
|---------|------|------------|
| HSRP | 1 | 192.168.10.1 |

---

Notes
- All end devices use the virtual IP address as their default gateway.
- The virtual IP is not statically assigned to any physical interface.
- VRRP and GLBP were not implemented due to Packet Tracer IOS limitations.

---

Conclusion
This addressing scheme supports first-hop redundancy using HSRP and provides a stable baseline for verification and failover testing.
