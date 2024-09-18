# Multiarea OSPF Configuration with Dualstack IPv4 and IPv6


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
## Device Overview
### Routers
* 5 Cisco Cisco 4321 ISR running Cisco IOS XE Software, Version 16.09.08 Universal K9
### Layer 3 Switch
* Cisco 3560 POE-38 running C3560-IPSERVICESK9-M Version 12.2(44)SE5
    * Version must be of IP Services, OSPF is not supported in IP Base
#
