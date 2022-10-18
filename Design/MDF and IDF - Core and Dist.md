# Design #
- Main distribution frame - is the main COMM room that holds main router(s) and switches among other gear.
- Intermediate Distribution Frame - smaller version of Comm room further down from MDF to interconnect devices that cannot reach MDF - over 100 meters.   IDF usually connects to MDF via fiber optic cables for greater length and faster speeds.  at workplace, IDF is a smaller room with fewer devices (usually switches) or IDF can be a rack mounted (lifted) on the wall out of reach of public access.

![[CCNA/Design/Untitled.png]]
- Link: https://study-ccna.com/collapsed-core-and-three-tier-architectures/
- **Two-Tier:** (Collapsed Core). Usually described as north-south traffic flow.
- **Three-Tier:** Usually described as north-south traffic flow.
- Spine-Leaf: East-West traffic flow. Datacenter design.

![[Untitled(1).png]]
![[Untitled(2).png]]

- Core switches are only for critical devices such as the router and access switches.
- Core switches should never be singular. “Two is one, one is none.”
- Qos and any software policy should be implemented on the Distribution layer. Implementing it on the Core Layer slows down the switch and should be avoided. Core layer is about speed and resiliency.
- Smaller campuses don't need the scalability of three seperate layers, in these cases a Collapsed Distribution and Core layer is used, where the distribution and Core layer functions are performed on the same hardware device.
- 


