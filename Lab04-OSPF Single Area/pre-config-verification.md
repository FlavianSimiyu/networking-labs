Lab 4: OSPF Single Area  
Pre-Configuration Verification

1. Router R0 – Interface and Routing Verification

I began by verifying the interface status and IP addressing on R0 using the `show ip interface brief` command. I confirmed that:

- **GigabitEthernet0/0** was configured with IP address **192.168.10.1** with status up/up.
- **GigabitEthernet0/1** was configured with IP address **10.0.1.1** with status up/up.
- Vlan1 was unassigned and administratively down, which was expected and not required for this lab.

Next, I checked the routing table using the `show ip route` command. I observed that:

- The **192.168.10.0/24** network was present as a connected route via **GigabitEthernet0/0**, and the local host route **192.168.10.1/32** was also installed.
- The **10.0.1.0/30** network was present as a connected route via **GigabitEthernet0/1**, and the local host route **10.0.1.1/32** was also installed.
- No dynamic routing protocols were running yet (no OSPF, RIP, or EIGRP routes were present).
- The gateway of last resort was not set, which was expected before configuring OSPF.

This confirmed that R0 had the correct IP addressing and directly connected routes before enabling OSPF.

---

2. Router R1 – Interface and Routing Verification

On R1, I ran the `show ip interface brief` command to verify the interface configuration. I confirmed that:

- **GigabitEthernet0/0** was configured with IP address **10.0.1.2** with status **up/up**.
- **GigabitEthernet0/1** was configured with IP address **10.0.2.1** with status **up/up**.
- **Vlan1** was unassigned and administratively down, which was acceptable for this lab.

I then checked the routing table with `show ip route`. I observed the following:

- The **10.0.1.0/30** network was installed as a connected route via **GigabitEthernet0/0**, along with the local host route **10.0.1.2/32**.
- The **10.0.2.0/30** network was installed as a connected route via **GigabitEthernet0/1**, along with the local host route **10.0.2.1/32**.
- Only directly connected and local routes were present; there were no OSPF or other dynamic routes yet.
- The gateway of last resort was not set, which was expected at this stage.

This confirmed that R1 was correctly configured with the two point-to-point subnets and was ready for OSPF configuration.

---

3. Router R2 – Interface and Routing Verification

For R2, I started with the `show ip interface brief` command. I verified that:

- **GigabitEthernet0/0** was configured with IP address **10.0.2.2** with status **up/up**.
- **GigabitEthernet0/1** was configured with IP address **192.168.30.1** with status **up/up**.
- **Vlan1** was unassigned and administratively down, which was not required for this lab.

I then examined the routing table using `show ip route` and observed:

- The **10.0.2.0/30** network was present as a connected route via **GigabitEthernet0/0**, and the local host route **10.0.2.2/32** was installed.
- The **192.168.30.0/24** network appeared as a connected route via **GigabitEthernet0/1**, along with the local host route **192.168.30.1/32**.
- No dynamic routing entries were present; only connected and local routes were shown.
- The gateway of last resort was not set, which matched the expected pre-OSPF state.

This confirmed that R2 had the correct addressing for both the point-to-point link and the LAN segment and was ready for OSPF deployment.

---

4. Summary of Pre-Configuration State

Before configuring OSPF, I verified that:

- All required router interfaces (**R0, R1, and R2**) were **up/up** with the correct IP addresses.
- Each router had only its **directly connected and local routes** in the routing table.
- There were **no OSPF routes** and **no gateway of last resort** configured yet.

This baseline verification ensured that Layer 3 connectivity on each individual router was correctly set up and that the network was ready for OSPF single-area configuration in the next stage of the lab.
