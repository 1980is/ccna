# DHCP #
### Cisco DHCP Server ###
- To see a summary of DHCP leases.
- ```show ip dhcp binding ```//To see DHCP leases.
To clear out a binding: ```clear ip dhcp binding *```
That clears out everything. If you want to clear out a specific ip, swap out the * for the IP address.
```show ip dhcp pool ``` //shows us the dhcp and the configuration //Remember to exlude IP addresses before creating the DHCP server.

To exclude addresses: ```ip dhcp exluded-address 10.16.0.1 10.16.0.3 ```

To setup DHCP Server: 
```ip dhcp pool SERVERS(V10) network 10.16.0.0 ?```
```network 10.16.0.0 /24```
```default-router 10.16.0.1 dns-server 8.8.8.8 (secondary server) 4.4.4.4```
```domain-name cbt-nuggets.com```
This automatically suffixes for dns searches See the running config:
```sh run | section dhcp```

- Many companies are now doing DHCP for their devices with static reservations because that makes it easier if we need to change network addresses. They can all be changed on the DHCP server instead of logging into all the devices and changing them.

### External DHCP Server ###
- Routers do not forward DHCP traffic by default. This needs to be done one switches as well.
- To enable this we need to enable this **on the interface** that will be receiving the DHCP requests.
- ```ip helper-address 10.10.20.10```

### Cisco DHCP Client ###
- The exception to the rule of static IP addresses for networking devices and server is a router that receives a dynamic IP address from the ISP if the company hasn't bought any valid IP addresses. 
- On the interface that's facing the ISP.
-  ``` ip address dhcp```
