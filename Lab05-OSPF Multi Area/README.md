Lab 5: OSPF Multi-Area

Overview
In this lab, I implement a multi-area OSPF design consisting of Area 0 (backbone) and one or more additional areas. This demonstrates hierarchical routing, reduces LSDB size on routers, and improves scalability compared to the single-area OSPF design used in the previous lab.

Objectives
- Build a Packet Tracer topology with multiple OSPF areas.
- Configure OSPF on routers using Area 0 and at least one non-backbone area.
- Identify and configure an Area Border Router (ABR).
- Verify LSDB reduction across areas.
- Observe how inter-area routes appear in routing tables.
- Test end-to-end connectivity across all areas.
- Document pre- and post-configuration states.

Tasks
1. Create the multi-area topology in Packet Tracer.
2. Define the addressing scheme and area assignments.
3. Perform pre-configuration interface and routing verification.
4. Configure:
   - Area 0
   - One or more additional areas (e.g., Area 1, Area 2)
   - The ABR connecting those areas
5. Verify:
   - Neighbor adjacencies by area
   - LSDB contents and inter-area routes
   - Router roles (DR, BDR, ABR)
6. Test connectivity between hosts in separate areas.
7. Generate documentation files for GitHub.


