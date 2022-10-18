# Routing Protocol Types #
```show ip protocols```

- Routing protocols can be split into two main types:
	- Interior gateway protocols (IGPs)
	- Exterior gateway protocols (EGPs)
- Interior gateway protocols are used for routing within an organisation.
- Exterior gateway protocols are used for routing between organizations over the internet.
- The only EGP in use today is BGP (Border Gateway Protocol)

## Interior Gateway Protocols ##
- Interior gateway protocols can be split into two main types.
	- Distance Vector routing protocols
	- Link State routing protocols
- Both protocols only form adjacencies with directly connected neighbours.

![[Screenshot from 2022-02-04 16-12-25.png]]

### Distance Vector Routing Protocols ###
- In Distance Vector protocols, each router sends its directly connected neighbours a list of all its known networks along with its own distance to each of those networks.
- Distance vector routing protocols do not advertise the entire network topology.
- A router only knows its directly connected neighbours and the list of networks those neighbours have advertised. It doesn't have detailed topology information beyond its directly connected neighbours.
- Distance Vector routing protocols are often called 'Routing by rumour'.

### Link State Routing Protocols ###
- In Link State protocols, each router describes itself and its interfaces to its directly connected neighbours.
- This information is passed unchanged from one router to another.
- Every router learns the full picture of the network including every router, its interfaces and what they connect to.
- Links State Routing Protocols know the complete picture of the network.

### Metric ###
- Only the best path will make it into the routing table and be used.
- The lowest metric value is preferred.
- Distance Vector routers advertise to each other the networks they know about, and their metric to get to each of them.
- Link State routers advertise all the links in their area of the network to each other.
- Each router will take this information and then make an independent calculation of its own best path to get to each destination.

	#### RIP Metric ####
	- RIP uses Hop Count as the metric.
	- It's not really used in production networks.
	- The maximum hop count by default is 15.

	#### OSPF Metric ####
	- OSPF uses 'Cost' as the metric, which is automatically derived from interface bandwidth by default.
	- You can manually configure the cost of links if you want to manipulate the path.

	#### IS-IS Metric ####
	- IS-IS also uses 'Cost' as the metric, but its not automatically derived from interface bandwidth. All links have an equal cost by default.
	- You can manually configure the cost of links if you want to manipulate the path count will be used.

	#### EIGRP Metric ####
	- EIGRP uses the bandwidth and delay of links to calculate the metric.
	- (Load and reliability can also be considered but are ignored by default)
	- A fixed delay value is used based on the interface bandwidth, the protocol does not dynamically measure current delay.
	- You can manually configure the delay links if you want to manipulate the path.


![[Screenshot from 2022-02-04 16-51-23.png]]

### Equal Cost Multi Path (ECMP) ###
- If multiple paths to a destination have an equal metric, the router will enter all of the paths into the routing table.
- Equal Cost Multi Path will load balance the outbound traffic to the destination over the different paths.
- All IGP routing protocols will perform ECMP by default.
- EIGRP is the only routing protocol which is capable of UnEqual Cost Multi Path. It must be manually configured to support this.

### Administrative Distance ###
- A router will typically only learn routes to a particular destination from a single routing protocol.
- The administrative distance is a measure of how trusted the routing protcol is.
- If routes to the same destination are received via different routing protocols, the protocol with the best (lowest) AD wins.
- When multiple routes to a desntination are learned through a routing protocol, the router wil linstall the path or paths with the best (lowest) metric into the routing table.
- Different routing protocols use different methods to calcualte the metric.
	- **RIP** uses hopcount. Default administrative distance is 120.
	- **IS-IS**. Default administrative distance is 115.
	- **OSPF** uses cost. Default administrative distance is 110.
	- **EIGRP** uses hopcount. Default administrative distance is 90.
	- **External BGP**. Default administrative distance is 20.
	- **Static Route.** Default administrative distance is 1.
	- **Connected Interface.** Default administrative distance is 0.

- Administrative distance is used to choose between multiple paths learned via different routing protcols.
- Metric is used to choose between multiple paths learned via the same protcol.
- The administrative distance is considered first to narrow the choice down to the single best routing protocol.
- The metric is then considered to choose the best path or paths which make it into the routing table.


