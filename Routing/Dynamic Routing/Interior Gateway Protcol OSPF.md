# OSPF #
-   `show ip ospf`.
-   `show ip protocols` to see all dynamic routing protocols that are running on the system.
-   OSPF has the same cost for 100Mbps as for 1Gbps. Both have the value of 1.
-   `show ip ospf interface intN0.`
-   To insert a default route into OSPF. `router ospf 1` then `default-information originate` the router that needs to have a default route itself, if it doesn’t, it wont put the default route into ospf. If we want to force it we can use `default-information originate always`.
- Different interfaces on a router can run in different instances of OSPF. Different instances have different Link State Databases. Only one instance is typically configured on OSPF routers - multiple Process IDs are very rarely used. The Process ID is locally significant. It does not have to match on the neighbour router to form an adjacency.
- `show ip ospf neighbor`
- ```show ip ospf database``` 
- It supports large networks and has very fast converge time and is supported on all vendors equipment.
- EIGRP can be simpler to implement and troubleshoot.
- Messages are sent using multicast.
- OSPF is an open standard protocol and is the most commonly used.
- It uses Dijkstra's Shortest Path First algorithm to determine the best path to learned networks.

#### Passive Interfaces ####
- ```router ospf 1```
- ```passive-interface loopback 0```
- ```passive-interface f2/0```
- You can make all interfaces passive by default. ```passive-interface default``` 
- To make an interface not passive. ```no passive-interface f0/0``` 
- The passive interface will be advertised in OSPF so other routers will learn how to get to that network but that interface will not form adjacencies on not give out any internal information.

#### When OSPF is enabled ####
- When OSPF is enabled this is what it does.
1) Discover neighbours
2) Form adjacencies
3) Flood Link State Database (LSDB)
4) Compute Shortest Path
5) Install best routes in routing table
6) Respond to network changes.

#### OSPF Packet Types ####
- **Hello:** A router will send out and listen for Hello packets when OSPF is enabled on an interface, and form adjacencies with other OSPF routers on the link.
- **DBD DataBase Description:** Adjacent routers will tell each other the networks they know about with the DBD packet.
- **LSR Link State Request:** If a router is missing information about any of the networks in the received DBD, it will send the neighbour an LSR.
- **LSA Link State ADvertisement:** A routing update.
- **LSU Link State Update:** Contains a list of LSA's which should be updated, used during flooding.
- **LSAck:** Receiving routers acknowledge LSAs.

#### Router ID ####

-   There are two big categories of routing protocols. One is **distance vector** protocol, the oldest routing protocol is a D.V. protocol RIP. D.V. don’t take into account the cost, it only looks at the hop counts. The other category is Link State. A popular example of a Link State Protocol is OSPF. OSPF uses link state advertisement which is forwarded to all other OSPF enabled routers so they can learn about the network and cost associated with a given path.
-   **OSPF Router ID**. Every router needs a unique identifier (RID). Router ID is 32 bits, it looks like an IP address. Before enabling OSPF, if there is no ROUTER ID configured, OSPF creates the ROUTER ID using three methods. **[NO1]** If there is a router ID configured, OSPF uses that. **[NO2]** IIf there is no router ID, OSPF uses a loopback address, the highest IP loopback address on the router. **[NO3]** If there are no loopback addresses it uses the highest IP address on any inferface.
- `show ip ospf`.
- To enable ospf. `router ospf 1`.
- To see the router ID. `show ip ospf`.

#### OSPF Areas ####
It's a link state protocol, each router describes itself and its interfaces to its directly connected neighbours. This information is passed unchanged from one router to another. **Every router learns the full picture of the network** including every router, its interfaces and what they connect to. OSPF router use LSA Link State Advertisements to pass on routing updates.
-  This can cause issues in large networks. Too many routes can use up too much router memory. Network changes cause all routers to reconverge which takes time and CPU resources. OSPF supports a hierarchical design which segments large networks into smaller areas to solve this problem. Each router maintains full information about its own area, but only summary information about other areas.

![[ospf-area-hierarchy.png]]
- The routers in between areas are known as Area Border Routers (ABRs).
	- An ABR has the following characteristics.
	- It seperates LSA flooding zones.
	- It becomes the primary point for area address summarization.
	- It functions regularly as the source for default routes.
	- It maintains the lSDB for each area with which it is connected.
	- The ideal design is to have each ABR connected to two areas only, the backbone and another area, with three areas being the upper limit.
- ABRs do not automatically summarise.
- **If you do not configure summarisation, all routes are flooded everywhere.**
- Summary statements don't use a wildcard mask, use a normal subnet mask.

- Routers which redistribute into OSPF are Autonomous System Boundary Routers (ASBR). 
	- That router is running OSPF, it might also be running RIP or EIGRP and redistributing them into OSPF or it's a static route that's injecting.

#### Bandwidth vs Clock Rate and Speed ####
- The rate that Ethernet interfaces physically transmit at is set by the 'speed' command.
- The rate that Serial interfaces physically transmit at is set by the 'clock rate' command. Serial interfaces transmit at 1.544 Mbps by default. If you use the 'clock rate 64000' command on a Serial interface it will physically transmit at 64Kbps.
- The bandwith command **does not** affect the physical transmission rate, that is set by the 'speed' or 'clock rate' command. If you set a bandwidth of 50 Mbps on a FastEthernet interface, it will still transmit at 100 Mbps.
- The bandwitch command affects software policy on the router, such as which path will be selected by EIGRP or OSPF, or how much bandwitdth will be guaranteed to a traffic type by QoS. You can influence software policy by setting the bandwitdh on an interface.

#### Cost Metric ####
- The overall cost = cumulative cost of all outgoing interfaces. You should ensure the cost is set the same on the interfaces on both sides of a link or you can get asymmetric routing.
- The cost is automatically derived from the interface bandwidth. Cost = Reference Bandwidth / Interface Bandwidth. The default reference bandwidth is 100 Mbps. FastEthernet link cost defaults to 1 (100/100). T1 link cost defaults to 64 (100 / 1.544).
- The problem with OSPF is that 1Gbps and 100Mbps both default to 1.
	- To change this we can change the reference bandwith. This needs to be done on all routers.
	- ```router ospf 1```
	- ```auto-cost reference-bandwidth 100000```
	- This makes the cost of 1Gbps = 1. It would probably be better to think ahead and make 1Gbps = 10 since 10Gbps and more is already here.
- You can manually change the cost of an interface.
	- ```interface F0/0```
	- ```ip ospf cost 50```
	- ```show ip ospf interface FastEthernet 0/0``` to see the Cost for that interface.

#### Link State Advertisements - How Adjacencies are formed ####

-   LSAs (link state advertisements type 1, all routers generate type 1, type 2 is only generated by the DR.
- **Hello:** A router will send out and listen for Hello packets when OSPF is enabled on an interface, and form adjacencies with other OSPF routers on the link.
- **DBD DataBase Description:** Adjacent routers will tell each other the networks they know about with the DBD packet.
- **LSR Link State Request:** If a router is missing information about any of the networks in the received DBD, it will send the neighbour an LSR.
- **LSA Link State ADvertisement:** A routing update.
- **LSU Link State Update:** Contains a list of LSA's which should be updated, used during flooding.
- **LSAck:** Receiving routers acknowledge LSAs.
- The protocol number for OSPF is 89.
- **You want to enable authentication for your OSPF.**
- A MTU mistmach between routers will cause them not to share OSPF routes with one another. They will form an adjacency but they will not share routes.

![[ospf-packet.png]]
- Hello packets are multicast to 224.0.0.5 ('all OSPF routers').
- Hello packets are sent every 10 seconds by default.

#### Wilcard Maks and Network Statements #### 
-   To see ospf interfaces. `sh ip ospf int brief`. To see OSPF neighbors, `sh ip ospf neighbor`
-   `show ip ospf int gig 0/0`

![[ospf-wildcards-for-subnets.png]]

#### DF and BDRs on Broadcast Networks ####
-   DR = Designated Router.
-   BDR = Backup Designated Router.
-   Other routers = DR-OTHER. ;)
    -   The designated router is selected by election and it’s done by looking at priority, and the default priority for routers is 1. If the priority is the same for all routers, the election process looks at the Router ID (RID) to chose a DR.
- If we don't want a router to become a DR we could set the ```ip ospf priority to 0```
- If we want a specific router to become the DR we would make sure it has the highest ospf priority. ```ip ospf priority 100```
- ```show ip ospf neighbors``` 
	- 2WAY/DROTHER relationship do not directly exchange routes with each other.



NOTES From David Bombal.
