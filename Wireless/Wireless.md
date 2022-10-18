# Wireless #
## Network Types ##
- WiFi services are defined in the IEEE 802.11 standard.
- IEEE: Institute of Electrical and Electronics Engineers.
- WPAN: Wireless Personal Area Network.
	- Devices are within 10 meters of each others.
	- Bluetooth is often used.
- WLAN: Wireless Local Area Network.
	- Devices within 100m of a Wireless Access Point.
- WMAN: Wireless Metropolitan Area Network.
	- Covers a large area such as a city.

### Ad Hoc Networks ###
- Two or more wireless stations communicate directly with each other.
- IBSS Independent Basic Service Set. Peer to peer network.

### Infrastructure Mode ###
- Stations communicate via a Wireless Access Point (AP).
- This can provide acces to a wired network.
- Multiple Access Points can be deployed to provide the required coverage area.

- Wireless stations work in either Ad-Hoc or Infrastructure Mode. They can not operate in both at the same time.
- WiFi Direct allows devices to be connected to an Access Point and also be part of a peer-to-peer wireless network. It does not operate in Ad-Hoc IBSS mode, it is an extension to Infrastructure Mode.
- WPS WiFi Protected Setup enables connection setup by pushing a button. It is WPAN Wireless Personal Area Network.

- Wireless Bridges can be used to connect areas which are not reachable via cable to the network.

## Wireless Access Points ##
- Wireless is half-duplex. Only one device can communicate at a time.
- BSS - Basic Service Set. The devices connected to a wireless access point make up a BSS.
- DS - A distribution system connects Wireless Access Point to the wired network.
- SSID - Service Set Identifier.
- BSA - Basic Service Area. The BSA is the wireless coverage area of an Access Point. Also known as a wireless cell.

## WLC and CAPWAP ##
- Autonomous WAP can function as standalone WAP’s.
- Lightweigh WAP are designed to be managed by a wireless controller.
- Lightweight Access Points support Zero Touch Provisioning. They discover their Wireless Lan Controller via these options:
	- DHCP - option 43 gives the IP address of the WLC.
	- DNS - 'cisco-capwap-controller' resolves the IP address of the WLC.
	- Local subnet broadcast.
- Split-MAC Design. See pic. If you are connected to one WAP and you are walking around, the CAPWAP tunnel means that you can transition from one WAP to another without renegotiating security keys if the WAPs are autonomous.
- The wireless controller will have a management/service port. It will also have a distribution (LAG) port where you can bundle multiple interfaces together to form a single high bandwith interface.

## Security ##
- WEP. 1999.
- WPA. 2003. WiFi Protected Access. 
- WPA2. 2004. AES encryption, CCMP Counter Cipher MOde with Block Chaining Message Authentication Code protocol.
- WPA3. 2018. AES encryption, CCMP, Protection against KRACK attack.
- PSK or Pre-Shared key should not be used in big environments.
- WPA3 is backwards compatible with WPA2.
- Personal VS Enterprise.
- Personal refers to how we are going to get the key, how the client will get the key. This means that we have configured a pre-shared-key for that client, a password.
- Enterprise means that we are using a centralized AAA server. The AP talks either directly or indirectly through a Controller to the AAA server.