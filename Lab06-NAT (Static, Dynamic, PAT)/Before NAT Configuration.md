Before NAT Configuration

1. Interface Status – Router R0
show ip interface brief

Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     203.0.113.1     YES manual up                    up
GigabitEthernet0/2     unassigned      YES unset  administratively down down
Vlan1                  unassigned      YES unset  administratively down down

2. Interface Status – Router R1
show ip interface brief

Interface              IP-Address       OK? Method Status                Protocol
GigabitEthernet0/0     203.0.113.2      YES manual up                    up
GigabitEthernet0/1     198.51.100.1     YES manual up                    up
GigabitEthernet0/2     unassigned       YES unset  administratively down down
Vlan1                  unassigned       YES unset  administratively down down

3. Routing Table – R0
show ip route

Gateway of last resort is 203.0.113.2 to network 0.0.0.0

     192.168.10.0/24 is directly connected, GigabitEthernet0/0
     203.0.113.0/30 is directly connected, GigabitEthernet0/1
L    192.168.10.1/32 is directly connected, GigabitEthernet0/0
L    203.0.113.1/32 is directly connected, GigabitEthernet0/1

S*   0.0.0.0/0 [1/0] via 203.0.113.2

4. Routing Table – R1
show ip route

     198.51.100.0/24 is directly connected, GigabitEthernet0/1
     203.0.113.0/30 is directly connected, GigabitEthernet0/0
L    198.51.100.1/32 is directly connected, GigabitEthernet0/1
L    203.0.113.2/32 is directly connected, GigabitEthernet0/0

S    192.168.10.0/24 [1/0] via 203.0.113.1

5. End Device IP Configuration
Inside Network

PC0

IP Address:     192.168.10.10
Subnet Mask:    255.255.255.0
Default Gateway:192.168.10.1


PC1

IP Address:     192.168.10.11
Subnet Mask:    255.255.255.0
Default Gateway:192.168.10.1


Server0

IP Address:     192.168.10.20
Subnet Mask:    255.255.255.0
Default Gateway:192.168.10.1

Outside Network

Server1

IP Address:     198.51.100.10
Subnet Mask:    255.255.255.0
Default Gateway:198.51.100.1

6. Connectivity Tests (Before NAT)
R0 → R1
ping 203.0.113.2   = Success

R1 → R0
ping 203.0.113.1   = Success

R1 → Server1
ping 198.51.100.10 = Success

PCs → Gateway
PC0 → 192.168.10.1 = Success
PC1 → 192.168.10.1 = Success
Server0 → 192.168.10.1 = Success

Inside → Outside (expected to fail before NAT)
PC0 → 198.51.100.10 = Success (routing allows it in this lab)
PC1 → 198.51.100.10 = Success (same reason)
Server0 → 198.51.100.10 = Success



7. NAT Status (Before Configuration)
show ip nat translations
(no entries)

show ip nat statistics
Total translations: 0