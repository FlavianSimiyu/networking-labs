(After Static NAT, Dynamic NAT, and PAT are fully configured)

1. NAT Interface Roles – R0
interface GigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.0
 ip nat inside

interface GigabitEthernet0/1
 ip address 203.0.113.1 255.255.255.252
 ip nat outside


Verification:

show ip interface g0/0
 → Interface is up
 → IP 192.168.10.1/24
 → NAT Inside enabled

show ip interface g0/1
 → Interface is up
 → IP 203.0.113.1/30
 → NAT Outside enabled

2. Static NAT Mapping (R0)
ip nat inside source static 192.168.10.20 203.0.113.10


Verification:

show ip nat translations
Pro  Inside global     Inside local
---  203.0.113.10      192.168.10.20


Connectivity test (from R1):

ping 203.0.113.10 = Success

3. Dynamic NAT Mapping (Earlier Stage)

Pool configured:

ip nat pool DYNPOOL 203.0.113.20 203.0.113.20 netmask 255.255.255.0
access-list 10 permit 192.168.10.0 0.0.0.255


Dynamic rule (used before PAT):

ip nat inside source list 10 pool DYNPOOL


R1 route for dynamic pool:

ip route 203.0.113.20 255.255.255.255 203.0.113.1


Verification (when tested):

show ip nat translations
icmp 203.0.113.20:x   192.168.10.10:x   198.51.100.10:x

4. PAT / NAT Overload (Final Active Configuration)

Final NAT rule:

ip nat inside source list 10 interface g0/1 overload


Verification:

From PC0 and PC1:

ping 198.51.100.10 = Success


NAT table on R0:

show ip nat translations

Pro   Inside global       Inside local        Outside local
icmp  203.0.113.1:XX       192.168.10.10:XX    198.51.100.10:XX
icmp  203.0.113.1:YY       192.168.10.11:YY    198.51.100.10:YY
---   203.0.113.10         192.168.10.20       ---


Interpretation:

Both PCs borrow 203.0.113.1 with unique ports → PAT confirmed

Static NAT mapping remains active → Server0 is reachable via 203.0.113.10

5. Routing Table Verification (Final State)
R0
show ip route

C   192.168.10.0/24  is directly connected, G0/0
C   203.0.113.0/30   is directly connected, G0/1
L   192.168.10.1/32  is directly connected
L   203.0.113.1/32   is directly connected
S*  0.0.0.0/0 [1/0] via 203.0.113.2

R1
show ip route

C   198.51.100.0/24 is directly connected, G0/1
C   203.0.113.0/30  is directly connected, G0/0
L   203.0.113.2/32  is directly connected
S   192.168.10.0/24 [1/0] via 203.0.113.1
S   203.0.113.10/32 [1/0] via 203.0.113.1
S   203.0.113.20/32 [1/0] via 203.0.113.1

6. Final Connectivity Verification
Inside LAN
PC0 → 192.168.10.1 = Success
PC1 → 192.168.10.1 = Success
Server0 → 192.168.10.1 = Success

Between Routers
R0 → 203.0.113.2 = Success
R1 → 203.0.113.1 = Success

Static NAT Test (Server0)
R1 → 203.0.113.10 = Success

PAT Test
PC0 → 198.51.100.10 = Success
PC1 → 198.51.100.10 = Success