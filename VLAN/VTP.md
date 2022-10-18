# VTP VLAN TRUNKING PROTOCOL#
-   VTP is not a trunking protocol!
-   `Show vtp status`
    -   The default VTP operating mode is server.
    -   There are three modes: Server, client, and transparent. Server can do anything, client can’t add or delete VLANs, transparent passes VTP updates but it doesn’t do anything with them. That mode basically disables VTP.
-   Conf t: `vtp ?` to see options.
- Be careful if using VTP - if you accidentally introduce a switch with a higher VLAN database revision number into the domain it can wipe out all your production VLANs.
- If using both DTP and VTP, the VTP domain name has to match on neighbour switches for trunks to be formed by VTP.
- ```show vtp password``` To see if a VTP password is set. 
- ```show vtp counters``` To see if the error counter is growing.