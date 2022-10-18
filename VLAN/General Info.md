# VLANs #

## Basic Knowledge ##

-   Vlan’s were created to segment off different parts of the network. In the past this problems was solved by using routers to segment off networks. Vlan’s provide security.
-   Networks, Subnets, Broadcast Domains, are all synonims for Vlan’s.
-   To send VLAN’s between switches you must configure a trunk (tag) port. Cisco calls it a trunk port, other vendors call it tagged port. Whenever a frame is sent between switches on a trunk port it’s tagged with a vlan-id (802.1QTAG), a layer is added between the data-link layer and the network layer called the 802.1Q.
-   Go to the port you want to change. If you do `switchport mode ?` You see the three options a port can have. Access, Dynamic or Trunk. Dynamic is not best practice or recommended. To make a port an access port you do: `switchport access vlan vlan-number`. To assign multiple port at a time. `interface range g1/0/1 - 18`.
-   We can also break it up. `interface range g1/0/1 - 18 , g1/0/20 - 24 , g3/0/5 - 48 , g5/0/5 , g 7/0/22 - 24`.
-   To make enable trunk on a port: `switchport trunk encapsulation dot1q`. Remember to also tell the port it’s a trunk port. `switchport mode trunk`. By default this allows all VLANs to be transmitted over the trunk link. To restrict the link to carry only specific VLANs us the VLAN allow command: `switchport trunk allowed vlan 1,2,3,4`.
-   To see trunks: `show interfaces trunk`.
-   To get a **VLAN status report**. `show interface fastEthernet 0/1 switchport`.
-  Routers do not forward broadcast traffic by default but switched do by default.

## Native VLAN ##

- Packets can go across a trunk without being tagged with 802.1Q tags in the following scenarios.
	- Switch originated the traffic. E.g., all Cisco switches out of the box run CDP, Cisco Device Discovery Protocol. Every 60 seconds it sends out a multicast message to discover neighbors. This goes over the native vlan. Telnet or SSH goes over the native vlan. Native VLAN = 1.
	- Pass-through devices. VOIP is a passthrough device. A computer is connected to the phone which has an internal switch. A computer doesn’t know anything about VLANs, it drops VLAN packets. The phone needs to be on its own VLAN, and the traffic from the computer is not tagged, so it goes to the default VLAN interface.
	- Virtualized servers.
- 
