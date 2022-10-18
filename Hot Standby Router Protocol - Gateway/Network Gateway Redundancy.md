# Network Gateway Redundancy #
- The most popular of the First Hope Redundancy Protocols is Hot Standby Router Protocol.

### FHRP First Hop Redundancy Protocol ###
- The purpose of FHRPs is to provide fault tolerant gateways.
- First Hop Redundancy Protocols (HSRP) use a Virtual IP (VIP) and MAC address to allow for automated gateway failover. The hosts use the VIP as their default gateway address.
- If a physical gateway fails, another gateway will take over.


### HSRP Hot Standby Router Protocol ###
-   It’s a Cisco protocol.
-   To enable it, go into the the interface or VLAN.
	- `conf t, standby ?` `standby 10 ?` `standby 10 ip 10.16.0.3`
- To put a custom priority on the router. ```standby 10 priority 110``` The default priority is 100. The higher number wins in this case.
- To enable pre-empt. ```standby 1 preempt``` This is done on the router with the higher priority.
-   After the command has been issued we wait, the router checks if the other routers are active for that standby group.
-   `show standby` or `show standby brief`
- It's deployed in an **active/standby** pair.
- The router with the higher IP address wins the election.
- You can choose which one will be actibe by setting priority on the routers.
- The router with the higher priority will be preferred (default 100).
- In the event of a tie the hightest IP address wins.
- If pre-emption is also enabled, when a higher priority router comes back online after a failure it will transtition back to active.
- If pre-emption is not enabled (default), the lower priority router will remain active when the failed router comes back online.
- This can be more stable if a higher priority router is flapping.
- The default version is 1, **HSRP version 2** introduced a few minor improvements. Both routers must be running the same version.



### VVRP Virtual Router Redundancy Protocol ###
-   `vrrp ?`
-   `vrrp 10 ip 10.16.0.5`
-   HSRP uses the term active, VVRP uses master.
-   The master is selected from who has the higher priority, if both routers have a priority of 100, the router with the higher IP address wins, the other is a backup.
- VRRP is an open standard. Deployed in an **active/standby** pair, very similar to HSRP.

### GLBP Gateway Load Balancing Protocol ###
-   GLBP responds with ARP requests by using roundrobin. Computer 1 sends a ARP request and the virtual gateway responds with MAC address #1, computer two sends a ARP request and the virtual gateway responds with MAC address #2.
- Cisco proprietary, support **active/active** load balancing across multiple routers.
-   `glbp 10 ip 10.16.0.5`