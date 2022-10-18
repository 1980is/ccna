# EtherChannel #
## Oversubscription ##
- A starting rule-of-thumb recommendation for oversubscription is 20:1 from the access layer to the distribution layer. Meaning if you had 20 PCs connected with 1Gbps NICs at the access layer, you would require a single 1Gbps uplink to the distribution layer. The recommendation is 4:1 for the distribution to core layer links. These are general values, you should analyze the traffic on your network to verify links are not congested.

--------------------------
## Terminology ##
- EtherChannel is also know as:
	- A Port Channel
	- LAG Link Aggregation
	- A link bundle
- NIC Teaming is also known as:
	- Bonding
	- NIC Balancing
	- Link aggregation
--------------------------
## General Info ##
- **A Spanning Tree instance provides redundancy, but not load balancing.**
- If a switch has multiple equal cost paths via the same neighbour switch towards the Root Bridge, it will select the port with the lowest Port ID.
- Everyone except Cisco call EtherChannel LAG.
- `show etherchannel summary`
- Shutdown your interfaces when configuring EtherChannel. If you don’t do that there will be a broadcast storm on your network. If the port goes into a disabled state, we have to shutdown the port and no shutdown. Remember to check the port channel virtual interface as well if things blow up. See if it’s (err-disabled) as well. This only happens if we manually turn on EtherChannel. If we use LACP or PAgP that doesn’t happen.
- All changes such as adding or removing VLANs is no longer done on the physical interfaces themselves that are grouped together using EtherChannel, you do it on the Port-Channel interface instead.
- EtherChannel is a port “grouper”.
- You can load balance between 2, 4, 8(max) connections.
- Load balancing is done by using ASIC.
- The symbol for EtherChannel is a circle draw across the links.
- If an interface goes down its traffic will fail over to the remaining links in the EtherChannel.

## EtherChannel Protocols and Configuration ##
### Protocols ###
-  There are three available protocols. 
	- **LACP - Link Aggregation Control Protocol.**
		- It's an open standard.
		- The switches on both sides negotiate the port channel creation and maintenance.
		- This is the preferred method.
	- **PAgP Port Aggregation Protocol.**
		- Cisco proprietary.
		- The switches on both sides negotiate the port channel creation and maintenance.
	- **Static Etherchannel.**
		- The switches do not negotiate creation and maintenance but the settings must still match on both sides for the port channel to come up.
		- Use if LACP is not supported on both sides.
- All protocols are configure with the ```channel-group``` command.

### EtherChannel Parameters ###
- **The switches on both sides must have a matching configuration.**
- The member interfaces must have the same settings on both sides.
	- Speed and duplex.
	- Access or Trunk mode.
	- Native VLAN and allowed VLANs on trunks.
	- Access VLAN on access ports.

## Configuration ##

### LACP Configuration ###
- LACP interfaces can be set as either **Active** or **Passive**.
- If SW1's interfaces are set as Active and SW2's as Passive, the port channel will come up.
- If both sides are Passive, the port channel will not come up.
- If both sides are Active, the port channel will come up.
- It is **recommended to configure both sides as Active** so you don't have to think about which side is which
- It's recommended to shutdown the interfaces before making changes to the ether-channel.
- ```interface range f0/23 - 24```
- ```channel-group 1 mode active```
- This creates interface port-channel 1
- ```interface port-channel 1```
- ```switchport mode trunk```
- Configure the interface settings on the port channel.
- To optimize spanning-tree for the links in the etherchannel group we should configure the link-type as point-to-point. This will make spanning-tree converge quicker. ```spanning-tree link-type point-to-point``` This is done on the portchannel interface itself.

### PAgp Configuration ###
- PAgp interfaces can be set as either **Desirable** or **Auto**.
- If on side is Desirable and the other Auto, the port channel will come up.
- If both sides are Auto, the port channel will not come up.
- If both sides are Desirable, the port channel will come up.
- If you configure both sides as Desirable you don't have to think about which side is which.
- ```interface range f0/23 - 24```
- ```channel-group 1 mode desirable```
- ```interface port-channel 1```
- ```switchport mode trunk```

Verify that Spanning Tree is not shutting down ports.

```show spanning-tree vlan 1```

### StackWise, VSS and vPC ###
- Cisco supports Multi-chassis EtherChannel technologies on some switches. These switches support a shared EtherChannel from different switches. The switches must be configured with matching settings.
- The problem is that if you have an access switch that's connected to two core switches. Two connections from the access switch to Core1 and two connections to Core 2. One EtherChannel group to Core1 and another EtherChannel group to Core 2. Spanning-tree will see this as a loop and disable one EtherChannel group. So this doesn't happen we use one of the protocols mentioned in this section.
- If Multi-Chassis Etherchannel is enabled Spanning-tree does not detect any loops. This supports full load balancing and redundancy across all interfaces.

![[etherchannel-multichassis.png]]


### Layer 3 Etherchannel ###
- The config is the same as for layer 2.
- ``` interface range GigabitEthernet 1/0/1 - 2```
- ```no switchport``` So you can assign IP addresses.
- ```channel-group 1 mode | active | auto | desirable | on | passive```
- ```interface port-channel 1```
- ```ip address 192.168.0.1 255.255.255.252```
- ```no shutdown```
- 