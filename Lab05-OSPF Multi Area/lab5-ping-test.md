 Lab 5: Ping Test Verification

Below are the complete ping results captured from PC0, PC1, and PC2 after finalizing IP configuration and OSPF multi-area routing. The output is preserved exactly as it appeared in Packet Tracer.

---

PC2 Ping Tests

PC2 → PC1 (192.168.20.10)

C:\>ping 192.168.20.10

Pinging 192.168.20.10 with 32 bytes of data:

Request timed out.
Reply from 192.168.20.10: bytes=32 time=18ms TTL=125
Reply from 192.168.20.10: bytes=32 time=53ms TTL=125
Reply from 192.168.20.10: bytes=32 time=12ms TTL=125

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 12ms, Maximum = 53ms, Average = 27ms

C:\>ping 192.168.20.10

Pinging 192.168.20.10 with 32 bytes of data:

Reply from 192.168.20.10: bytes=32 time=1ms TTL=125
Reply from 192.168.20.10: bytes=32 time=32ms TTL=125
Reply from 192.168.20.10: bytes=32 time=18ms TTL=125
Reply from 192.168.20.10: bytes=32 time=24ms TTL=125

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 32ms, Average = 18ms

---

PC2 → PC0 (192.168.10.10)

C:\>ping 192.168.10.10

Pinging 192.168.10.10 with 32 bytes of data:

Request timed out.
Reply from 192.168.10.10: bytes=32 time=35ms TTL=125
Reply from 192.168.10.10: bytes=32 time=41ms TTL=125
Reply from 192.168.10.10: bytes=32 time=33ms TTL=125

Ping statistics for 192.168.10.10:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 33ms, Maximum = 41ms, Average = 36ms

C:\>ping 192.168.10.10

Reply from 192.168.10.10: bytes=32 time<1ms TTL=125
Reply from 192.168.10.10: bytes=32 time=32ms TTL=125
Reply from 192.168.10.10: bytes=32 time=12ms TTL=125
Reply from 192.168.10.10: bytes=32 time=14ms TTL=125

Ping statistics for 192.168.10.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 32ms, Average = 14ms

---

PC1 Ping Tests

PC1 → Default Gateway (192.168.20.1)

C:\>ping 192.168.20.1

Pinging 192.168.20.1 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.20.1:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),

C:\>ping 192.168.20.1

Reply from 192.168.20.1: bytes=32 time<1ms TTL=255
Reply from 192.168.20.1: bytes=32 time<1ms TTL=255
Reply from 192.168.20.1: bytes=32 time<1ms TTL=255
Reply from 192.168.20.1: bytes=32 time=17ms TTL=255

Ping statistics for 192.168.20.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 17ms, Average = 4ms

---

PC1 → PC2 (192.168.30.10)

C:\>ping 192.168.30.10

Reply from 192.168.30.10: bytes=32 time=1ms TTL=125
Reply from 192.168.30.10: bytes=32 time=20ms TTL=125
Reply from 192.168.30.10: bytes=32 time=12ms TTL=125
Reply from 192.168.30.10: bytes=32 time=20ms TTL=125

Ping statistics for 192.168.30.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 20ms, Average = 13ms

---

PC1 → PC0 (192.168.10.10)

C:\>ping 192.168.10.10

Reply from 192.168.10.10: bytes=32 time=2ms TTL=125
Reply from 192.168.10.10: bytes=32 time=43ms TTL=125
Reply from 192.168.10.10: bytes=32 time=26ms TTL=125
Reply from 192.168.10.10: bytes=32 time=12ms TTL=125

Ping statistics for 192.168.10.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 43ms, Average = 20ms

---

PC0 Ping Tests

PC0 → Default Gateway (192.168.10.1)

C:\>ping 192.168.10.1

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.10.1:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),

C:\>ping 192.168.10.1

Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255
Reply from 192.168.10.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.10.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

---

PC0 → PC1 (192.168.20.10)

C:\>ping 192.168.20.10

Reply from 192.168.20.10: bytes=32 time=2ms TTL=125
Reply from 192.168.20.10: bytes=32 time=49ms TTL=125
Reply from 192.168.20.10: bytes=32 time=35ms TTL=125
Reply from 192.168.20.10: bytes=32 time=41ms TTL=125

Ping statistics for 192.168.20.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 2ms, Maximum = 49ms, Average = 31ms

---

PC0 → PC2 (192.168.30.10)

C:\>ping 192.168.30.10

Reply from 192.168.30.10: bytes=32 time=9ms TTL=125
Reply from 192.168.30.10: bytes=32 time=26ms TTL=125
Reply from 192.168.30.10: bytes=32 time=34ms TTL=125
Reply from 192.168.30.10: bytes=32 time=64ms TTL=125

Ping statistics for 192.168.30.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 9ms, Maximum = 64ms, Average = 33ms
