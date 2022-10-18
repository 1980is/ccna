
# Dynamic Trunking Protocol (DTP)

-   Trunking allows you to send multiple VLANs across a single port.
-   `show interfaces trunk`.
-   Cisco calls it trunking, every other vendor calls it tagging.
-   When enabling trunk ports we should use manual
-   Dynamic Trunking Protocol (DTP) is the default state on many Cisco switches.
-   The default mode of DTP is Dynamic Desirable. It sends out DTP packets that it desires to be a trunk port. Most devices such as computers, servers etc., respond with, I can’t be that so I’ll be an access port instead and this is the security risk. If an attacker puts a switch in between the computer and the switch that’s sending out the DTP packets, then they have the trunk port. A VLAN hopping attack is then possible.
-   Switchportmode, only use either access or trunk.
-   Switchportmode dynamic has two options, if you write `switchport mode dynamic ?` You will see both options.
-   Dynamic auto is the port saying “I sure something happens”. I’m not sending any DTP packets, if there is a switch on the other end that has DTP Desirable enabled it will send out DTP packets that it desires to a be a DTP port and the Dynamic Auto will respond, thank you for sending the packets, that’s what I want, let’s be a trunk. **Two switches set to auto will never trunk**, they are both passive, one needs to be the active one.
-   Both sides are desirable, you have a trunk.
-   One side is auto, the other side is desirable, you have a trunk.
-   Both sides are auto, you don’t have a trunk.
-   If one side is set to trunk manually, it will send out DTP packets and if the other side is set to auto, desirable or trunk, you have a trunk.
-   Best method is to set it **manually** to trunk and set the port to **nonegotiate**, no DTP packets.

```switchport nonegotiate``` distables DTP.

#### Voice ####
- ```interface FastEthernet 0/10```
- ```description IP Phone```
- ```switchport mode access```
- ```switchport mode vlan 10```
- ```switchport voice vlan 20```
- It doesnt need to be configured as a trunk port, this is a special case where both can be on the same port and we want to seperate voice from data, we don't want it on the same VLAN.

### Limiting or Adding VLANs to Trunk ###

-   Go under the interface and type `switchport mode allowed vlan xx` (**and the complete list of allowed VLANs**) don’t add just one!