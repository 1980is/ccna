# Wide Area Networks #
- A private network uses links which are dedicated for an individual organisation.
- Local Area Networks are private networks.
- Wide Area Networks can also use physical links which are dedicated for an individual organisation.

## VPN ##
### IPsec VPN Configuration Options ###
1) **IPsec Tunnel**: open standard IPsec tunnel, does not support multicast.
2) **GRE (Generic Routing Encapsulation)**: over IPsec tunnel: adds support for multicast.
3) **IPsec VTI (Virtual Tunnel Interface)**: Cisco proprietary simplified configuration, supports multicast.
4) **DMVPN (Dynamic Multipoint VPN)**: Cisco proprietary. Scalable simple hub and spoke style configuration enables direct full mesh connectivity between all offices.
5) **FlexVPN**: Cisco proprietary. Very similar to DMVPN, newer technology.
6) **GETVPN (Group Encrypted Transport VPN)**: Cisco proprietary. Scalable centralised policy for VPN over non-public infrastructure eg., MPLS.

- Two major categories of VPN are Site-To-Site and Remote-Access. Remote-Access is a client connecting in, Site-To-Site is a VPN tunnel between data-centers or routers, etc.
- VPN used SSL/TLS for remote access VPNs. The problem with that is that it’s TCP based and there is some overhead with acknowledgments, etc. VPNs can use DTLS instead and the biggest difference is that it uses UTP and uses less overhead. Some use IPSEC (IKEv1 or IKEv2). PPTP and L2TP are other protocols that can be use.
- Split tunneling.
    -   It tells the VPN only to tunnel traffic for certain networks.

![[vpn.png]]

## Cryptomap ##
- Confidentiality is achieved by using cryptography. Cryptography uses a key or a method to encrypt and decrypt the message.
- Two major protocols that do hashing are SHA-(VERSION) and MD5.
- For successful Security Association (SA), which of the following do VPN peers on both ends of a tunnel need to agree on? What traffic not to encrypt, What traffic to encrypt, The hashing algorithm(s) to use, The encryption algorithm(s) to use, all of these.
- IPSEC is a collection of protocols and tools that IPSEC adopts to keep current with changes.

![[vpn-crypto.png]]

## WAN Connectivity Options ##
- **Leased Lines.**
	- A leased line is a dedicated physical connection between two locations. It has fixed, reserved bandwidth which is not shared with anyone else. The same bandwidth is available in both directions. The company may own the cable infrastructure but more commonly it is leased from a service provider for a monthly fee, hence the name 'leased line'.

- **MPLS Multi Protocol Label Switching**.
	- MPLS uses a shared core infrastructure at the service provider. It can be used for connectivity to the Internet and/or connectivity between offices over VPN.
	- Wan connectivity can be provided over an MPLS infrastructure, usually operated by a service provider.
	- Traffic from multiple customers can travel over the providers shared MPLS network, so this is a VPN service.
	- Different levels of SLA for uptime and traffic delay and loss are often available at different price points.
	- Ethernet connections are typically used to the customer router.
	- MPLS VPNs provide a full mesh topology by default.

- **Satellite**.
	- They are typically expensive and low bandwidth.
	- They may be the only option in hard to reach areas.

- **DWDM Dense Wavelength Division Multiplexing**.
	- DWDM combines ('multiplexes') multiple optical signals into one optical signal transmitted over a single fiber strand.
	- Each signal is assigned a different wavelength.
	- DWDM allows more capacity to be added to existing infrastructure without expensive upgrades.
	- DWDM is used in all modern long haul optical connections.

- **Dark Fiber**.
	- Many service providers laid optical fiber cabling in the past and then found they didn't require it.
	- DWDM was a major reason for this.
	- The unused cabling can be offered to customers as 'Dark Fiber'. 

- **PPPoE Point to Point Protocol over Ethernet**
- Less expensive options often aimed at home user Internet access are often used as Internet VPN WAN backup options in corporate environments.
- These can also be used as the primary WAN connection method to the corporate network from smaller offices and for home users.
	- DSL Digital Subscriber Line.
	- Cable.
	- Wireless eg., 4G.
- There will typically be no corporate level SLA with these services.

## Wan Topology Options  ##
### Hub and Spoke (Star) ###
- Advantages: Simplicity, centralised security policy.
- Disadvantages: Single point of failure, suboptimal traffic flow.

### Redundant Hub and Spoke ###
- Advantages: Remove single point of failure, centralised security policy.
- Disadvantages: Higher cost, suboptimal traffic flow.

### Full Mesh ###
- Here, every office is connected to every other office.
- Advantages: Optimal traffic flow.
- Disadvantages: Higher complexity and cost.

### Partial Mesh ###
- ...
