Lab 5: OSPF Multi-Area  
Pre-Configuration Verification

Before configuring OSPF on the routers, I verified the initial interface status and routing tables on all devices in the topology. At this point, no dynamic routing protocol had been enabled, so each router contained only directly connected routes. This verification helped establish a clear baseline before enabling multi-area OSPF.

---

1. Router R0 – Interface and Routing Verification

I began with R0 and issued the `show ip interface brief` command.  

The output confirmed that:

- **GigabitEthernet0/0** was up/up with IP address **192.168.10.1**, serving as the default gateway for PC0.  
- **GigabitEthernet0/1** was up/up with IP address **10.0.0.1**, forming the point-to-point link to R2.  
- No other interfaces were active.  
- VLAN1 was administratively down.

Next, I checked the routing table using `show ip route`.  
R0 displayed:

- Two **connected (C)** routes:
  - `192.168.10.0/24` on g0/0  
  - `10.0.0.0/30` on g0/1  
- Two corresponding **local (L)** routes for its interface IPs.  
- No OSPF, static, or inter-area routes were present.

This confirmed that R0 had only its local LAN and backbone link reachable, with no dynamic routing information learned yet.

---

2. Router R1 – Interface and Routing Verification

On R1, I ran `show ip interface brief`.

I observed:

- **GigabitEthernet0/0** was up/up with IP address **192.168.20.1**, serving as the default gateway for PC1.  
- **Serial0/0/0** was up/up with IP address **10.0.0.9**, forming the Area 1 connection toward R2.  
- The remaining interfaces were administratively down.

Running `show ip route`, R1 showed:

- A **connected** network `192.168.20.0/24` on g0/0.  
- A **connected** network `10.0.0.8/30` on s0/0/0.  
- Corresponding **local** routes.  
- No learned routes, since OSPF had not been enabled yet.

This verified that R1 had connectivity only to its LAN and to the serial link that would connect Area 1 to the ABR (R2).

---

3. Router R2 – Interface and Routing Verification

R2 acts as the future Area Border Router (ABR), so I closely verified its interface configuration.

From `show ip interface brief`, I confirmed:

- **GigabitEthernet0/0** was up/up with IP address **10.0.0.2**, linking to R0 in Area 0.  
- **GigabitEthernet0/1** was up/up with IP address **10.0.0.5**, linking to R3 in Area 0.  
- **Serial0/0/0** was up/up with IP address **10.0.0.10**, forming the Area 1 connection to R1.  
- A second serial interface existed but was not in use.  
- All interfaces that should participate in OSPF were operational.

Using `show ip route`, I verified that R2 contained:

- Connected routes for:
  - `10.0.0.0/30` (R0 link)  
  - `10.0.0.4/30` (R3 link)  
  - `10.0.0.8/30` (R1 link)  
- Local routes for each interface IP.  
- No dynamic or inter-area routes.

This confirmed that R2 had visibility only into its immediate physical networks prior to OSPF activation.

---

4. Router R3 – Interface and Routing Verification

On R3, the `show ip interface brief` output showed:

- **GigabitEthernet0/0** was up/up with IP address **10.0.0.6**, connecting R3 to R2 in Area 0.  
- **GigabitEthernet0/1** was up/up with IP address **192.168.30.1**, serving as the gateway for PC2.  
- All other interfaces were down or unassigned.

The routing table contained:

- Connected routes for:
  - `10.0.0.4/30` on g0/0  
  - `192.168.30.0/24` on g0/1  
- Local routes for interface IPs.  
- No OSPF or inter-area routes yet.

This confirmed that R3 was correctly positioned as an Area 0 router with only local connectivity.

---

5. Summary of Pre-OSPF State

Across all routers, I confirmed that:

- All point-to-point and LAN interfaces required for the OSPF topology were **up/up** and correctly assigned IP addresses.  
- All routers contained **only their directly connected networks** in the routing table.  
- No OSPF neighbor adjacencies or dynamic routes existed at this stage.  
- The serial link between R1 and R2 was operational and ready for use as the Area 1 boundary.

This pre-configuration verification ensured that the foundation for deploying OSPF multi-area routing was stable and correctly implemented.
