# Multiarea OSPF Configuration with Dualstack IPv4 and IPv6

## Implementing Automatic Routing Protocols in Modern Networks
While routing protocols are never required to be implemented in any network, there is a reason almost every modern network with more than 2 or 3 routers implements one. Open Shortest Path First (OSPF) is one of many automatic routing protocols, protocols developed to provide a solution to ever-changing networks where static routes may not be a maintainable option. OSPF is one of the most popular Interior Gateway Protocols (IGP), protocols that define routes internal to a domain or autonomous system. 
<br><br>
OSPF networks are logically split into group of routers called areas. While implementing single-area OSPF is relatively simple, it does not scale well in very large networks with hundreds of routers. Areas take the burden off of each individual router by reducing the number of routers each individual must store in memory. As all areas are connected to the backbone area, a default-gateway like approach can be taken to routing where a router in one area does not know the topology in another area, sending packets over the connected interface and letting the routers in the other area finish routing the packet. 
<br>
<br>
This project is an example of a simple 3 area OSPF network and the bare-minimum configurations required to allow simple pings across networks.


## Topology
<p align="center">
    <img src="./images/Topology.svg" width="75%">
</p>

## IP Address Configuration

| Device | Interface  | IPv4         | IPv6                |
|:-------|:-----------|:------------:|:-------------------:|
| R1     | S0/1/0     | 10.0.0.5/30  | 2001:db8:1:0::5/64  |
|        | S0/1/1     | 10.0.0.1/30  | 2001:db8:0:0::1/64  |
| R2     | S0/1/0     | 10.0.0.6/30  | 2001:db8:1:0::6/64  |
|        | G0/0/1     | 10.0.0.9/30  | 2001:db8:2:0::9/64  |
| R3     | Loopback 1 | 10.1.1.1/24  | 2001:db8:1:1::1/64  |
|        | S0/1/0     | 30.0.0.1/30  | 2001:db8:3:0::1/64  |
| R4     | S0/1/0     | 30.0.0.2/30  | 2001:db8:3:0::2/64  |
|        | S0/1/1     | 10.0.0.2/30  | 2001:db8:0:0::2/64  |
| R5     | Loopback 1 | 10.2.2.2/24  | 2001:db8:2:2::2/64  |
|        | G0/0/1     | 20.0.0.1/30  | 2001:db8:20:0::1/64 |
| S1     | F0/1       | 10.0.0.10/30 | 2001:db8:2:0::10/64 |
|        | F0/2       | 20.0.0.2/30  | 2001:db8:20:0::2/64 |
## Device Overview
### Routers
* 5 Cisco 4321 ISRs running Cisco IOS XE Software, Version 16.09.08 Universal K9
### Layer 3 Switch
* Cisco 3560 POE-38 running C3560-IPSERVICESK9-M Version 12.2(44)SE5
    * Version must be of IP Services, OSPF is not supported in IP Base
#

### ICMPv4 Ping Across Network
```
Sending 5, 100-byte ICMP Echos to 10.2.2.2, timeout is 2 seconds:
Packet sent with a source address of 10.1.1.1
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 4/4/5 ms
``` 
#
### ICMPv6 Ping Across Network
```
Sending 5, 100-byte ICMP Echos to 2001:DB8:2:2::2, timeout is 2 seconds:
Packet sent with a source address of 2001:DB8:1:1::1
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 3/4/5 ms
``` 

#
### IPv4 Routing Table from Router5
```
Router5#show ip route ospf
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override, p - overrides from PfR

Gateway of last resort is not set

      10.0.0.0/8 is variably subnetted, 6 subnets, 3 masks
O IA     10.0.0.0/30 [110/26] via 20.0.0.2, 00:01:22, GigabitEthernet0/0/1
O IA     10.0.0.4/30 [110/14] via 20.0.0.2, 00:01:22, GigabitEthernet0/0/1
O        10.0.0.8/30 [110/2] via 20.0.0.2, 00:01:22, GigabitEthernet0/0/1
O IA     10.1.1.1/32 [110/76] via 20.0.0.2, 00:01:22, GigabitEthernet0/0/1
      30.0.0.0/30 is subnetted, 1 subnets
O IA     30.0.0.0 [110/75] via 20.0.0.2, 00:01:22, GigabitEthernet0/0/1
```
#
### IPv6 Routing Table from Router5
```
Router5#show ipv6 route ospf
IPv6 Routing Table - default - 10 entries
Codes: C - Connected, L - Local, S - Static, U - Per-user Static route
       B - BGP, R - RIP, I1 - ISIS L1, I2 - ISIS L2
       IA - ISIS interarea, IS - ISIS summary, D - EIGRP, EX - EIGRP external
       ND - ND Default, NDp - ND Prefix, DCE - Destination, NDr - Redirect
       O - OSPF Intra, OI - OSPF Inter, OE1 - OSPF ext 1, OE2 - OSPF ext 2
       ON1 - OSPF NSSA ext 1, ON2 - OSPF NSSA ext 2, a - Application
OI  2001:DB8::/64 [110/26]
     via FE80::224:F9FF:FE61:3EC2, GigabitEthernet0/0/1
OI  2001:DB8:1::/64 [110/14]
     via FE80::224:F9FF:FE61:3EC2, GigabitEthernet0/0/1
OI  2001:DB8:1:1::1/128 [110/75]
     via FE80::224:F9FF:FE61:3EC2, GigabitEthernet0/0/1
O   2001:DB8:2::/64 [110/2]
     via FE80::224:F9FF:FE61:3EC2, GigabitEthernet0/0/1
OI  2001:DB8:3::/64 [110/75]
     via FE80::224:F9FF:FE61:3EC2, GigabitEthernet0/0/1
```
