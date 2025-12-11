Lab 4: OSPF Single Area  
Post-Configuration OSPF Verification

1. Router R0 – OSPF Neighbors and Routes

After configuring OSPF on R0, I verified neighbor adjacencies using the `show ip ospf neighbor` command. I observed that:

- R0 had one OSPF neighbor with **Router ID 2.2.2.2** (R1).
- The neighbor state was **FULL/BDR** on interface **GigabitEthernet0/1** with neighbor IP address **10.0.1.2**.
- The FULL state confirmed that the adjacency between R0 and R1 was fully established and that LSAs had been successfully exchanged.

Next, I checked the routing table using `show ip route ospf`. I confirmed that:

- The **10.0.2.0/30** network was learned via OSPF with an administrative distance/metric of **[110/2]**, reachable via **10.0.1.2** on **GigabitEthernet0/1**.
- The **192.168.30.0/24** LAN behind R2 was also learned via OSPF with metric **[110/3]**, reachable through R1 at **10.0.1.2**.
- These OSPF-learned routes indicated that R0 had full reachability to the far-end point-to-point network and remote LAN through the OSPF domain.

I then ran `show ip ospf` to verify the OSPF process details. I confirmed that:

- The routing process was **"ospf 1"** with **Router ID 1.1.1.1**.
- The router was operating in a single OSPF area, **Area 0 (BACKBONE)**.
- There were **2 interfaces** participating in Area 0.
- The SPF algorithm had been executed multiple times, which indicated that OSPF had computed the shortest-path tree based on the link-state database.
- The area had **no authentication** configured, and a total of **5 LSAs** were present in the database.

This verification confirmed that R0 was fully participating in OSPF and had learned remote networks correctly.

---

2. Router R1 – OSPF Neighbors and Routes

On R1, I started by checking neighbor relationships using `show ip ospf neighbor`. I observed that:

- R1 had two OSPF neighbors:
  - Neighbor **1.1.1.1** (R0) on **GigabitEthernet0/0** in **FULL/DR** state.
  - Neighbor **3.3.3.3** (R2) on **GigabitEthernet0/1** in **FULL/BDR** state.
- The FULL state on both adjacencies confirmed that R1 had successfully formed complete OSPF neighbor relationships with both R0 and R2.

I then inspected the OSPF-learned routes using `show ip route ospf`. I confirmed that:

- The **192.168.10.0/24** LAN behind R0 was learned via OSPF with metric **[110/2]**, reachable via **10.0.1.1** on **GigabitEthernet0/0**.
- The **192.168.30.0/24** LAN behind R2 was also learned via OSPF with metric **[110/2]**, reachable via **10.0.2.2** on **GigabitEthernet0/1**.

This showed that R1 had full visibility of both remote LANs and was acting as the central transit router between R0 and R2.

Using the `show ip ospf` command, I verified that:

- The OSPF process was **"ospf 1"** with **Router ID 2.2.2.2**.
- R1 was participating in **Area 0 (BACKBONE)** with **2 OSPF-enabled interfaces**.
- The SPF algorithm had been executed multiple times, and the area contained **5 LSAs**.
- No authentication was configured in the area, and there were no external LSAs since this was a single-area internal OSPF design.

This confirmed that R1 was correctly acting as the central OSPF router, maintaining full adjacencies and routing for all internal networks.

---

3. Router R2 – OSPF Neighbors and Routes

For R2, I verified neighbor relationships with `show ip ospf neighbor`. I observed that:

- R2 had one OSPF neighbor with **Router ID 2.2.2.2** (R1).
- The neighbor state was **FULL/DR** on **GigabitEthernet0/0** with neighbor address **10.0.2.1**.
- The FULL/DR state confirmed that the adjacency between R2 and R1 was fully established and that R1 was acting as the Designated Router on that segment.

Next, I checked the OSPF routes using `show ip route ospf`. I confirmed that:

- The **10.0.1.0/30** network between R0 and R1 was learned via OSPF with metric **[110/2]**, reachable via **10.0.2.1** on **GigabitEthernet0/0**.
- The **192.168.10.0/24** LAN behind R0 was learned via OSPF with metric **[110/3]**, also reachable via **10.0.2.1** on **GigabitEthernet0/0**.

These entries showed that R2 had full reachability to the networks on the R0 side through the OSPF domain.

I then ran `show ip ospf` to inspect OSPF process details. I verified that:

- The routing process was **"ospf 1"** with **Router ID 3.3.3.3**.
- R2 was operating within **Area 0 (BACKBONE)** and had **2 interfaces** participating in the area.
- The SPF algorithm had run multiple times and the area contained **5 LSAs**, matching the other routers.
- There was no area authentication configured and no external LSAs present.

This confirmed that R2 was fully integrated into the OSPF single-area design and had complete visibility of all internal networks.

---

4. Summary of Post-OSPF State

After configuring OSPF on R0, R1, and R2, I confirmed that:

- All routers successfully formed **FULL OSPF adjacencies** with their neighbors.
- R1 had neighbor relationships with both R0 and R2, acting as the central transit router in the topology.
- Each router installed **OSPF-learned routes** in its routing table, providing full reachability between:
  - The **192.168.10.0/24** LAN behind R0, and
  - The **192.168.30.0/24** LAN behind R2.
- The OSPF process on all routers was running in a single area, **Area 0 (BACKBONE)**, with consistent LSA counts and no authentication configured.

This verification confirmed that the OSPF single-area configuration was functioning correctly and that dynamic routing was successfully providing end-to-end connectivity across the lab network.
