# Multiarea OSPF Configuration with Dualstack IPv4 and IPv6

## Topology
<p align="center">
    <img src="./images/Topology.svg" align:center>
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

## Device Overview
### Routers
* 5 Cisco Cisco 4321 ISR running Cisco IOS XE Software, Version 16.09.08 Universal K9
### Layer 3 Switch
* Cisco 3560 POE-38 running C3560-IPSERVICESK9-M Version 12.2(44)SE5
    * Version must be of IP Services, OSPF is not supported in IP Base
#
