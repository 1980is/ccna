# Interior Gateway Protocol #

## RIP ##
- RIP is a distance vector protocol.
- It uses hop count as its metric.
- The maximum hop count is 15.
- It will perform Equal Cost Multi Path, for up to 4 paths by default.
- RIP version 2 is the current version, not used very often.
- RIP will automatically summarise routes to the classful boundary by default.
- For example, 192.168.10.1/30 will be adverstised as 192.168.10.0/24.
- 172.16.10.1/30 will be advertised as 172.16.0.0/16.
- This is almost never desirable. To cancel this do ```router rip``` then ```no auto-summary```. 
- ```show ip rip database``` 

## EIGRP ##
- EIGRP (Enhanced Interior Gateway Routing Protocol) is an Advanced Distance Vector routing protocol.
- It support large networks.
- It has very fast converge time.
- It supports bounded updates where network topology change updates are only sent to routers affected by the change.
- Messages are sent using multicast.
- EIGRP will automatically perform equal cost load balancing on up to 4 paths by default.
- This can be increased up to 16 paths.
- EIGRP can also be configured to perform unequal cost load balancing.
- To enable ```router eigrp 100```. 100 in this example is the Autonomous System (AS), meaning an independent administrative domain. EIGRP routers need to have the same Autonomous System number to peer with each other.
- ```router eigrp 100```
- ```network 10.0.0.0 0.0.255.255```
- The network command uses a wildcard mask which is the inverse of a subnet mask.
- Subtract each octet in the subnet mask from 255 to calculate the wildcard mask.
- A subnet mask of 255.255.255.252 equals a wilcard mask of 0.0.0.3.
- EIGRP routers identify themselves using an EIGRP Router ID which is in the form of an IP address.
- This will default to being the highest IP address of any loopback interfaces configured on the router, or the highest other IP address if a loopback does not exist.
- Loopback interfaces never go down so the Router ID will not change.
- You can also manually specify the Router ID.
- Best practice is to use a Loopback or manually set the Router ID.
- ```show eigrp neighbors```
- ```show ip eigrp interfaces```

 