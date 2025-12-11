Addressing Table

1. Router Interfaces

R0 – NAT Router

| Interface | IP Address       | Subnet Mask        | Default Gateway | NAT Role |
|-----------|------------------|--------------------|-----------------|----------|
| G0/0      | 192.168.10.1     | 255.255.255.0      | —               | Inside   |
| G0/1      | 203.0.113.1      | 255.255.255.252    | —               | Outside  |
| G0/2      | Unassigned       | —                  | —               | —        |

R1 – ISP Router

| Interface | IP Address       | Subnet Mask        | Default Gateway | Role     |
|-----------|------------------|--------------------|-----------------|----------|
| G0/0      | 203.0.113.2      | 255.255.255.252    | —               | Transit  |
| G0/1      | 198.51.100.1     | 255.255.255.0      | —               | Outside  |
| G0/2      | Unassigned       | —                  | —               | —        |

2. End Device Addressing

Inside Network

| Device   | IP Address       | Subnet Mask        | Default Gateway  |
|----------|------------------|--------------------|------------------|
| PC0      | 192.168.10.10    | 255.255.255.0      | 192.168.10.1     |
| PC1      | 192.168.10.11    | 255.255.255.0      | 192.168.10.1     |
| Server0  | 192.168.10.20    | 255.255.255.0      | 192.168.10.1     |

Outside Network

| Device   | IP Address        | Subnet Mask        | Default Gateway   |
|----------|-------------------|--------------------|-------------------|
| Server1  | 198.51.100.10     | 255.255.255.0      | 198.51.100.1      |

3. NAT Addressing

Static NAT Mapping

| Inside Local      | Inside Global     | Purpose          |
|------------------|-------------------|------------------|
| 192.168.10.20     | 203.0.113.10      | Published server |

Dynamic NAT Pool

| Pool Name | Start IP       | End IP         | Subnet Mask        | Notes                     |
|-----------|----------------|----------------|---------------------|---------------------------|
| DYNPOOL   | 203.0.113.20   | 203.0.113.20   | 255.255.255.0       | Single-host dynamic pool |

PAT (NAT Overload)

| Inside Network Range   | PAT Global IP      | Method     |
|------------------------|---------------------|------------|
| 192.168.10.0/24        | 203.0.113.1 (G0/1)  | Overload   |

4. Network Summary

| Network Name         | Network Address     | Subnet Mask        | Notes                                |
|----------------------|----------------------|--------------------|--------------------------------------|
| Inside LAN           | 192.168.10.0/24      | 255.255.255.0      | PCs + Server0 + R0 G0/0              |
| R0–R1 Transit Link   | 203.0.113.0/30       | 255.255.255.252    | R0 G0/1 ↔ R1 G0/0                    |
| Outside Network      | 198.51.100.0/24      | 255.255.255.0      | R1 G0/1 + Server1                    |
| Static NAT Public IP | 203.0.113.10/32      | Host Route         | Mapped to Server0                    |
| Dynamic NAT Global IP| 203.0.113.20/32      | Host Route         | Used during Dynamic NAT testing      |
