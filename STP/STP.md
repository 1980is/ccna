# Spanning Tree Protocol #
- Spanning Tree watches the network redundancy.
- ```show spanning-tree vlan 1```
    
- It makes sure that broadcast storms don’t happen. Dyanmic routing protocols have built-in loop prevention mechanisms and TTL acts as a final failsafe.
    
- Spanning tree sends out **BPDU** packets. Every two seconds it sends them out to check if any of the primary links have failed, if it detects a link down it unblocks the link that was blocked.
    
- The root bridge should be the center of the network, but often it’s not. The oldest switch is picked as the root, oldest manufacturing date is selected as the root bridge of the whole network.

- Legacy Spanning Tree can take up to 50 seconds to converge.
    
- To change the root bridge to the switch you are on. `spanning-tree vlan 1,10,20,30,40 priority 4096`.

### How Spanning Tree Works ###
- Spanning Tree is an industry standard protocol and is enably by default on all vendor's switches. Switches send Bridge Protocol Data Units (BPDU) out all ports when they come online. These are used to detect other switches and potential loops. The switch will not forward traffic out any port until it is certain it is loop free.
- Bridges = Switches. Switches where called bridges back in the early days when networks were made up of hubs and switches were used as bridges to segment off hub networks. 
-  When a switch comes online it will be in a Blocking state. Spanning Tree will detect if the port forms a potential loop. If there is no loop the port will transtition to Forwarding. The process can take up to 50 seconds. 
	- #### Speed up Spanning-Tree's converge ####
	- To make the process faster we can enable Spanning Portfast. This is done on the interface level ```spanning-tree portfast```.  You can make all the ports on the switch to be Portfast ports by ```spanning-tree portfast default``` in global config. If that is done we need to make sure any ports that are connected to switches have ```no spanning-tree portfast``` configured. Enabling portfast on most ports is dangerous if someone brings a switch from home and plugs it into the wall. 
	- We can enable BPDU Guard on Portfast ports to guard against this happening. If a BPDU is received the port will be shut down.
	- This is done on the interface level. ```spanning-tree bpduguard enable``` This can also be done in global config, ```spanning-tree portfast bpduguard default```
	- #### Spanning Tree Root Guard ####
	- Spanning Tree Root Guard prevents an unintended switch from becoming the root bridge. If a port where Root Guard is enabled receives BPDU's that are superior than the current root bridge, it will transition the port to root-inconsistent and not forward any traffic over the port.
	- This is done on the interface level. ```spanning-tree guard root```
- The BDPU contains the switch's Bridge ID which uniquely identifies the switch on the LAN. The Bridge ID is comprised of the switch's unique MAC addressa and an administrator defined Bridge Priority value. The Bridge Priority can be from 0 - 65535, with 32768 being the defult. 
- A root Bridge is elected based on the switches' Bridge ID value. The switch with the **lowest** Bridge Priority value is preferred (16384 is better than 49152). In the case of a tie the switch with the lowest MAC address will be selected. The swtiches build a loop free forwarding path Tree leading back to the Root Bridge.

#### Cost ####
![[stp-cost.png]]
- Each switch's exit interface on the lowest cost path to the Root Bridge is selected as its Root Port.
- **Spanning Tree does not do load balancing.**
- If a switch has multiple equal cost paths towards the Root Bridge, it will select the neighbour switch with the lowest Bridge ID.

### Spanning Tree Bridge Election ###
- Because Spanning Tree selects paths pointing towards the root bridge, it acts as a centre point of the LAN.
- Best practice is to ensure a pair of high-end core switches are selected as the 1st and 2nd most preferred Root Bridge.
- You can manipulate the Root Bridge election by setting the Bridge priority. The default value is 32768, with the lowest number being most preferred. In the case of a tie the switch with the lowest MAC address will be selected. This is liable to be the oldest switch.
- ```spanning-tree vlan 1 root primary``` Done in global config and it sets a Bridge priority of 24576 on that switch. If the core switch fails we would want core switch 2 to be the failover Bridge switch. Do do that, ```spanning-tree vlan 1 root secondary``` This will set a Bridge Priority of 28672.

### Designated Ports and Root Ports ###
- Ports on the neighbour switch opposite to the Root Port are Designated Ports. Root Ports point towards the Root Bridge, Designated Ports point away from it. All port on the Root Bridge are always Designated Ports.
-  All ports on the Root Bridge are always Designated Ports.
- Root Ports and Designated Ports are the most direct paths to and from the Root Bridge and transition to a forwarding state.
- On the remaining links, the switches determine which of them has the least-cost path to the root. If they have equal cost paths then the Bridge ID is used as a tiebreaker. The port connecting this switch to the link is selected as a Designated Port.
- Any ports which have not been selected as a Root Port or Designated Port pair would potentially form a loop.
- These are selected as Blocking Ports.

#### Figure out which ports are Root, Designated and Blocking ####
1) Determine the Root Bridge first (best Bridge ID).
2) All ports on the Root Bridge are Designated Ports.
3) Determine the Root Ports on the other switches (lowest cost to Root Bridge).
4) The ports on the other side of those links are Designated Ports.
5) On the links which are left, one port will be blocking.
6) Determine the Blocking Port (highest cost path to Root Brideg or highest Bridge ID).
7) The ports on the other side of those links are Designated Ports.

### Spanning Tree Versions ###
- IEEE Open Standards.
	- 802.1D Spanning Tree Protocol (STP). The original Spanning Tree implementation. Uses one Tree for all VLANs in the LAN.
	- 802.1w Rapid Spanning Tree Protocol (RSTP). Significantly improved convergence time. Uses one Spanning Tree for all VLANs in the LAN.
	- 802.1s Multiple Spanning Tree Protocol (MSTP). Enables grouping and mapping VLANs into different spanning tree instances for load balancing.
- Cisco released enhancements to the open standards.
	- Per VLAN Spanning Tree Plus (**PVST+**). Cisco enhancement to 802.1D. Uses a seperate Spanning Tree instance for every VLAN. This is the default on Cisco switches.
	- Rapid Per Vlan Spanning Tree Plus (**RPVST+**). Cisco enchancement to 802.1w RSTP. Significantly improved convergence time over PVST+. Uses a separate Spanning Tree instance for every VLAN.
	- The Cisco versions do not support grouping multiple VLANs into the same instance.

### Spanning Tree and HSRP Relationship ###
- HSRP should be configure to match the Spanning Tree path.
- In this example R1 should be given a higher HSRP priority than R2 so that it is selected as the HSRP active Router since it's directly connected to the Root Bridge. This allows traffic from the PCs to take the most direct path to their default gateway. If R2 was the HSRP active router, traffic would have to transit vi an extra device over the Core 1 and Core 2 link.