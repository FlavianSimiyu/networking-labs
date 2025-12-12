 HSRP Failover Test
First Hop Redundancy Protocol (HSRP)

Purpose
This document records the **HSRP failover testing** performed to verify gateway redundancy.
The objective was to confirm that the Standby router successfully assumes the Active role when the original Active router fails, and that connectivity for end hosts is maintained.

---

Initial HSRP State (Normal Operation)

- Active Router: R0 (192.168.10.2)
- Standby Router: R1 (192.168.10.3)
- Virtual IP: 192.168.10.1

---

Failover Event

Simulated Failure
The Active router (R0) was taken offline by shutting down interface **GigabitEthernet0/0**.

---

HSRP State During Failover

R1 – show standby brief
```
Interface   Grp  Pri P State    Active          Standby         Virtual IP
Gig0/0      1    100 P Active   local           unknown         192.168.10.1
```

Result: R1 successfully transitioned to the **Active** role after detecting the failure of R0.

---

End Host Connectivity Test During Failover

PC0 – Ping Test to Virtual IP
```
ping 192.168.10.1

Request timed out.
Reply from 192.168.10.1: bytes=32 time=14ms TTL=255
Reply from 192.168.10.1: bytes=32 time=15ms TTL=255
Reply from 192.168.10.1: bytes=32 time=5ms TTL=255

Packets: Sent = 4, Received = 3, Lost = 1 (25% loss)
```

Result: A brief packet loss was observed during the HSRP transition, after which connectivity was restored. This behavior is expected during gateway failover.

---

Recovery of Original Active Router

The failed router (R0) was brought back online by re-enabling interface **GigabitEthernet0/0**.

R0 – show standby brief
```
Interface   Grp  Pri P State    Active          Standby         Virtual IP
Gig0/0      1    110 P Active   local           192.168.10.3    192.168.10.1
```

Result: Due to higher priority and preemption, R0 reclaimed the **Active** role, and R1 returned to **Standby**.

---

Failover Test Summary
- HSRP correctly detected the failure of the Active router.
- The Standby router successfully became Active.
- End-host connectivity was maintained with minimal packet loss.
- Preemption allowed the preferred router to resume the Active role after recovery.

---

Conclusion
The HSRP failover test was successful. The network demonstrated resilience to gateway failure, validating the effectiveness of HSRP in providing default gateway redundancy.
