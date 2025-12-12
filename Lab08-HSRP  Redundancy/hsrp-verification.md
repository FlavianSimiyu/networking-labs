HSRP Verification
First Hop Redundancy Protocol (HSRP)

Purpose
This document verifies the successful configuration and operation of **HSRP** on the LAN network.
The objective was to confirm that a virtual default gateway is operational and reachable by end devices.

---

Network Summary
- LAN Network: 192.168.10.0/24
- HSRP Group: 1
- Virtual IP Address: 192.168.10.1
- Active Router: R0 (192.168.10.2)
- Standby Router: R1 (192.168.10.3)

---

HSRP Configuration Overview

- R0 was configured with a higher priority (110) and preemption enabled, making it the Active router.
- R1 was configured with a lower priority (100) and preemption enabled, making it the Standby router.
- Both routers share the same virtual IP address (192.168.10.1).

---

HSRP Status Verification

R1 – show standby brief
```
Interface   Grp  Pri P State    Active          Standby         Virtual IP
Gig0/0      1    100 P Standby  192.168.10.2    local           192.168.10.1
```

Result: R1 is correctly operating in the **Standby** state, while R0 is the **Active** router.

---

End Device Connectivity Test

PC0 – Ping Test to Virtual IP
```
ping 192.168.10.1

Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time=12ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time=14ms TTL=255

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

Result: The virtual IP address is reachable, confirming successful HSRP operation.

---

Verification Summary
- HSRP is correctly configured on both routers.
- One router is operating as Active and the other as Standby.
- The virtual default gateway (192.168.10.1) is reachable from end devices.
- The network is operating normally under HSRP.

---

Conclusion
HSRP has been successfully implemented and verified. The network is now protected against single-gateway failure at the default gateway level and is ready for failover testing or further redundancy protocol configuration.
