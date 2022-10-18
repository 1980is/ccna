# IPv6 #
## Basics ##
-   To transition from IPV4 to IPV6 you can startout with using a dual stack.
-   [YouTube Ipv6 Playlist](https://youtu.be/X8RxRr7KNl8)
-   Base 2 is binary, Base 10 is decimal, Base 16 is hex.
-   **Broadcast is not used in Ipv6**. See Document [here](../files/30-05+IPv6+Global+Unicast+Addresses+Lab+Demo.pdf) about IPv6 about multicast and DHCP servers.
-   Every address is supposed to use a /64 mask. Half of the address is going to be the network portion, the other half the host portion.
-   In an IPv6 address the first three hextets are first 48 bits (block) that was assigned to the company. The next hextet, the fourth is divided up into different subnets. The last 4 hextets are assigned to the individual host.

## How it’s constructed

IPV4 uses octets, each octet has 8 bits. IPV6 uses hextets and each hextet contains 16 bits. That means each hex character in a IPV6 address contains 4 bits, hence 16 bits in each nibble (4 bits).

## Addresses ##
### Three Types of IPv6 Addresses ###
- IPv6 Address Types Document [here](../files/30-04+IPv6+Global+Unicast+Addresses.pdf).
- Unlike IPv4, you can have multiple IPv6 addresses on an interface.

- **Global Unicast**.
	- Global Unicast Addresses are similar to IPv4 public addresses.
	- They are assigned to an individual host and have global reachability (unless blocked by security policy such as on a firewall).
	- They are assigned from the range 2003::/3.
	- Internet authorities assign block from the overall 2003::/3 range to organisations.
	- A common assignment for a company is a /48 block, eg., 2001:10:10::/48.
	- A smaller or larger size block can be assigned depending on the size of the company.
	- IPv6 standards state that addresses assigned to individual hosts should use a /64 mask.
	- The IPv6 address is 128 bits so /64 splits it in half for the network and host portions of the address.
	- If a company is assigned a /48 address by the Internet authorities and uses /64 host addresses, that leave 16 bits the company can assign to its internal subnets.
	- For example, if the company was assigned 2001:10:10::/48 by the Internet authorities, it can assign subnets 2001:10:10:0::/64 to 2001:10:10:FFFF::/64 to its internal network segments.
	- 16 bits = 65,535 possible subnets.
	- 64 bits left over = 18,446,744,073,709,551,616 hosts per subnet.

- **Unique Local**
	-  Unique Local Addresses are similar to IPv4 RFC 1918 private adresses.
	- They are not publicly reachable.
	- They are assigned from the range FC00::/7.
	- Hosts should be assigned /64 addresses.

- **Link Local**
	- Link local addresses are valid from communications on that link only.
	- They are assigned from the range FE80::/10 - FEB0::/10.
	- Hosts should be assigned /64 addresses.
	- These addresses are not routed outside of their local link.
	- Link local addresses can be used for communications which should not be forwarded beyond the local link, like routing protocol hello packets and updates.
	- They are mandatory on IPv6 enabled Cisco router interfaces.
	- Link Local addresses are automatically generated with EUI-64 addresses on IPv6 enabled Cisco router interfaces.
	- EUI-64 address can be overridden with manual configuration.

### EUI-64 Addresses ###
- A Cisco router can generate full IPv6 addresses for itself when given the interface and /64 network to use.
- The host portion of the address is derived from the interface's MAC address, which is guaranteed to be globally unique.
- A MAC address is a /48 address compared to the /64 host portion of the IPV6 address.
- FF:FE is injected in the middle of the /48 MAC address to bring it up to 64 bits. Also, the 7th bit is inverted.
- To create EUI-64 addresses
	- ```ipv6 address 2001:db8:0:1::/64 eui-64```
- It's not recommended to use EUI-64 on router interfaces. It is better to use a memorable address such as 2001:db8:0:1::1.

### SLAAC Stateless Address AutoConfiguration ###
- Hosts can be assigned IPv6 addresses through static addressing, DHCPv6, or SLAAC.
- DHCP servers track their MAC address to IP address assignments, so this is 'stateful' addressing.
- With SLAAC, hosts learn the /64 subnet their interface is on from their local router and then use this information to generate their own IPv6 EUI-64 address.
- Modern Operating Systems randomise the host portion of the address rather than using standard EUI-64 for privacy reasons.
- The router does not track which hosts have which IP address so this is 'stateless' addressing.

#### SLAAC - Router Advertisements ####
- When a global unicast IPv6 address is configured on an interface then Router Advertisements advertising the network prefix are sent out by default.
- These ICMP messages are sent to the 'All Nodes' multicast address from the interface's link-local address.
- Hosts can also send a 'Router Solicitation' message to request the information.
- As well as telling the hosts which subnet to generate their IP address on, the router tells the hosts to use itself as their default gateway.
- The original implementation did not support any information other than the default gateway address.
- In practice a DHCP server is still required to give out information such as DNS server.
- If the IP address is assigned by SLAAC and the DNS server is assigned by DHCP this results in a stateless configuration, where the DHCP server does no retain information about the hosts.

#### The Unspecified Address ####
- :: is the Unspecified address or Unknown address.
- An IPv6 router to ::/0 is a default route equivalent to 0.0.0.0.0.0.0.0 in IPv4.
- Also, :: is used as the source when an interface is trying to acquire an address.

#### Neighbor Discovery ####
- Neighbor Discovery is the IPv6 version of ARP and works in the same way.
- Rather than using ARP requests and replies, Neighbor Discovery uses ICMP Neighbor Solicitations and Neighbor Advertisements. 
- Neighbor Solicitation Messages are sent to the Solicited-Node multicast address which reaches all hosts on the subnet.

### CLI  Commands ###

-   You have to substitude ip commands with ipv6. E.g., ```show ipv6 interface brief```
-   **You must enable IPv6 routing on routers**. `ipv6 unicast-routing`.
-   ```show ipv6 brief ``` to see ipv6 information on interfaces.
-   ```ipv6 address``` to give an interface an address.
-   `Show ipv6 protocols`
-   `Show ipv6 route`
-   `Show run | in ipv6`

## Routing ##
- IPv6 routing works the same way as IPv4 routing, but the processes are separate, and there are separate IPv4 and IPv6 routing tables.
- If a router receives an IPv4 packet, it will route it according to its IPv4 routing table.
- If a router receives and IPv6 packet, it will route it according to its IPv6 routing table.
- The routing tables are built in the same way, through static routes or dynamic routing protocols.

#### IPv6 Routing Protocol Support ####
- Updated versions of the existing IPv4 routing protocols were released to support IPv6.
- The configuration and operation is very similar for IPv6 as for IPv6.
	- RIPng (RIP next generation)
	- EIGRP for IPv6.
	- OSPFv3.
	- IS-IS
	- MP-BGP4 (MultiProtocol BGP-4)
- IPv4 routing is enabled by default on a Cisco Router.
- IPv6 routing is disabled by default.
- ```ipv6 unicast-routing``` To enable it.
- You can still configure IPv6 addresses on a router without IPv6 unicast-routing enabled and send and receive IPv6 traffic, but the router will not forward IPv6 traffic to other networks.