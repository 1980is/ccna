# SDN Software Defined Networking #

-   Three types of Enterprise Networking Controller.
    -   SD-Wan
    -   DNA Center
    -   Meraki

## Fabrics

-   The types of underlay fabric.
    -   EIGRP
    -   OSPF
    -   IS-IS
    -   BGP
-   The overlay fabric.
    -   Uses different protocols than the underlay.
    -   Protocols like IPSec and GRE.
    -   This makes it seem like the next device is just one hop away, it creates a tunnel.
    -   The overlay depends on the underlay.
-   Fabric = overlay on top of an underlay that’s managed by a controller.

## Planes

-   Data Plane.
    -   How devices send data from one node to the next.
-   Control Plane
    -   How they know how to send data from one node to the next.
    -   OSPF, EIGRP, BGP, etc. Routing table, hey where is my next hop? These protocols make up the control plane.
-   Management Plane
    -   Where we make the policies.

## DNA Center - SD ACCESS Fabric

-   SD Access focuses on people and groups. Much like AD does.