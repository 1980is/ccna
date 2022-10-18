# Inter-VLAN Routing #

## Router With Seperate Interfaces ##
- There is typically a one-to-one relationship between an IP subnet and a VLAN in the LAN campus. For example, Engineering hosts are in IP subnet 10.10.10.0/24 and VLAN 10, and Sales hosts are in IP subnet 10.10.20.0/24 and VLAN 20. Hosts are segregated at Layer 3 by being in different IP subnets, and at Layer 2 by being in different VLANs. Hosts in different IP subnets need to send traffic via a router to communicate with each other.

## Router On A Stick ##
-   Let’s say we wanted to use fastEthernet 0/1. We could do `interface fastEthernet 0/1.?` To see the options. If it was being assigned to vlan 10, we would write: `int fastEthernet 0/1.10` We don’t have to use 10 but it’s good to have the number align with the vlan number it’s associated with.
-   Before we can assing an IP address to that subinterface we must do `encapsulation dot1Q 10` if the VLAN number is 10.
- The interface that hosts the subinterfaces does not need an IP address.
- ```interface FastEthernet 0/1```
- ```no ip address```
- ```no shutdown```
- ```interface FastEthernet 0/1.20```
- ```encapsulation dot1q 20```
- ```ip address 10.10.20.1 255.255.255.0```
- Remember to make the port on the switch that's connected to the Router a trunk port.
- If we want to route the native vlan 1 we need to do ```encapsulation dot1Q 1 native```
- **When we use ip default-gateway** on a switch we have to make sure that **ip routing** is disabled.

## Layer 3 Switch ##
- Uses SVI (Switch Virtual Interfaces) to route between different VLANs.
- ```ip routing```
- The port that's connected to the router needs to be configured as ```no switchport``` and have an IP address. No switchport convert the port to a layer 3 port so we can put an IP address on it, without it, we couldn't.
- 