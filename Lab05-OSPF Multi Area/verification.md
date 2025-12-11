Lab 5: OSPF Multi-Area  
Post-Configuration OSPF Verification

1. Router R0 – OSPF Neighbors and Inter-Area Routes

After configuring OSPF on R0, I started by checking neighbor adjacencies using the `show ip ospf neighbor` command. I observed that:

- R0 had one OSPF neighbor with **Router ID 3.3.3.3** (R2).
- The neighbor state was **FULL/BDR** on interface **GigabitEthernet0/1** with neighbor address **10.0.0.2**.

The FULL state confirmed that R0 had successfully formed a complete adjacency with R2 over the backbone (Area 0) link.

Next, I examined the OSPF-learned routes using the `show ip route ospf` command. I saw the following entries:

- The **10.0.0.4/30** network between R2 and R3 was installed as an OSPF intra-area route (**O**) with metric **[110/2]**, reachable via **10.0.0.2** on **GigabitEthernet0/1**.
- The **10.0.0.8/30** network (R1–R2 serial link in Area 1) appeared as an inter-area OSPF route (**O IA**) with metric **[110/65]**, reachable via **10.0.0.2**.
- The **192.168.20.0/24** LAN behind R1 (Area 1) was also present as an **O IA** route with metric **[110/66]**, reachable via **10.0.0.2**.
- The **192.168.30.0/24** LAN behind R3 (Area 0) was learned as an intra-area OSPF route (**O**) with metric **[110/3]**, reachable via **10.0.0.2**.

These entries confirmed that R0, as an Area 0 router, viewed networks in Area 1 as **inter-area (O IA)** routes and networks within Area 0 as **intra-area (O)** routes. This behavior matched the expected hierarchical design of multi-area OSPF.

---

2. Router R1 – OSPF Neighbors and Inter-Area Routes

On R1, which resides entirely in **Area 1**, I first checked neighbor relationships using `show ip ospf neighbor`. I observed that:

- R1 had a single OSPF neighbor with **Router ID 3.3.3.3** (R2) on **Serial0/0/0**.
- The state was **FULL**, with neighbor address **10.0.0.10**.

This confirmed that R1 had correctly formed an adjacency with the ABR (R2) over the Area 1 serial link.

I then inspected the OSPF routes with `show ip route ospf` and noted the following:

- The backbone point-to-point networks **10.0.0.0/30** (R0–R2) and **10.0.0.4/30** (R2–R3) were present as **inter-area routes (O IA)** with metric **[110/65]**, reachable via **10.0.0.10**.
- The **192.168.10.0/24** LAN behind R0 and the **192.168.30.0/24** LAN behind R3 also appeared as **O IA** routes with metric **[110/66]**, both reachable via **10.0.0.10** on **Serial0/0/0**.

Since R1 is located in Area 1, it learned all Area 0 networks, as well as the LANs behind R0 and R3, as **inter-area (O IA)** routes from the ABR at R2. This confirmed that inter-area route propagation from the backbone to Area 1 was functioning correctly.

---

3. Router R2 – Area Border Router (ABR) Verification

R2 was configured as the **Area Border Router (ABR)**, connecting **Area 0** and **Area 1**. To verify its role, I started with `show ip ospf neighbor`. I observed:

- A FULL adjacency with **Router ID 4.4.4.4** (R3) on **GigabitEthernet0/1** with neighbor address **10.0.0.6**.
- A FULL adjacency with **Router ID 1.1.1.1** (R0) on **GigabitEthernet0/0** with neighbor address **10.0.0.1**.
- A FULL adjacency with **Router ID 2.2.2.2** (R1) on **Serial0/0/0** with neighbor address **10.0.0.9**.

This confirmed that R2 successfully maintained OSPF neighbor relationships in **both Area 0 and Area 1**, which is a key characteristic of an ABR.

Next, I examined the OSPF-learned routes using `show ip route ospf`:

- The **192.168.10.0/24** LAN behind R0 was present as an OSPF route (**O**) with metric **[110/2]**, reachable via **10.0.0.1** on **GigabitEthernet0/0**.
- The **192.168.20.0/24** LAN behind R1 was present as an OSPF route with metric **[110/65]**, reachable via **10.0.0.9** on **Serial0/0/0**.
- The **192.168.30.0/24** LAN behind R3 was present as an OSPF route with metric **[110/2]**, reachable via **10.0.0.6** on **GigabitEthernet0/1**.

As an ABR, R2 participates in both areas and therefore does not mark these as inter-area routes in the same way that pure Area 0 or Area 1 routers do. Instead, it learns and advertises routes appropriately into each area. This confirmed that R2 was performing its ABR role correctly by exchanging summary information between Area 0 and Area 1.

---

4. Router R3 – OSPF Neighbors and Inter-Area Routes

On R3, another Area 0 router, I verified neighbor adjacencies with `show ip ospf neighbor`. I observed that:

- R3 had one OSPF neighbor with **Router ID 3.3.3.3** (R2).
- The neighbor state was **FULL/DR** on interface **GigabitEthernet0/0** with neighbor address **10.0.0.5**.

This confirmed that R3 had a fully established OSPF adjacency with R2 on the Area 0 backbone link.

I then checked the OSPF routes with `show ip route ospf` and saw the following:

- The **10.0.0.0/30** network between R0 and R2 was present as an OSPF intra-area route (**O**) with metric **[110/2]**, reachable via **10.0.0.5** on **GigabitEthernet0/0**.
- The **10.0.0.8/30** Area 1 serial link (R1–R2) appeared as an **inter-area route (O IA)** with metric **[110/65]**, reachable via **10.0.0.5**.
- The **192.168.10.0/24** LAN behind R0 was present as an **O** route with metric **[110/3]**, reachable via **10.0.0.5**.
- The **192.168.20.0/24** LAN behind R1 appeared as an **O IA** route with metric **[110/66]**, also reachable via **10.0.0.5**.

These results confirmed that R3, as an Area 0 router, treated Area 1 networks (both the R1–R2 serial link and the R1 LAN) as **inter-area (O IA)** routes, while routes within Area 0 remained **intra-area (O)**.

---

5. Summary of Multi-Area OSPF Operation

After completing the OSPF configuration on all routers, I confirmed that:

- All routers formed the expected **FULL OSPF neighbor adjacencies**:
  - R0 ↔ R2 in Area 0  
  - R2 ↔ R3 in Area 0  
  - R1 ↔ R2 in Area 1  
- **R2 correctly acted as the Area Border Router (ABR)**, participating in both Area 0 and Area 1 and exchanging routing information between them.
- Routers located entirely within a single area (R0, R1, and R3) displayed **inter-area routes (O IA)** for networks that belonged to other areas, demonstrating the hierarchical nature of multi-area OSPF.
- All LAN networks behind R0, R1, and R3 were reachable across the OSPF domain using dynamically learned routes.

This verification confirmed that the multi-area OSPF design was working as intended, with proper area separation, ABR behavior, and inter-area route propagation across the lab topology.
