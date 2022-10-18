# Physical Layer #
## Copper Cables ##
- Cat 5 and 5+ are max 1 gigabit per second.
- Cat 6 goes up to 10 gigabit per second.
- UTP Ethernet goes max to 100 meters.
- If you have T-568A on both sides or T-568B on both sides it’s considered a straight through cable. **Standard MDI-X** is a part of GIG Ethernet and it has the possibility of figuring out the cabling so it doesn’t matter if it’s a straight through cable or crossover.
-  Wires 1,2,3,4,6 are used for transmission. 4,5,7,8 are not used for data transmission for regular gig ethernet.

## Fiber Cables ##
- Support longer distances and higher bandwith requirements.
- Two types of fiber.
	- Single mode or Multi mode.
	- Single mode supports higher bandwidth and longer distances but is more expensive.

## Power over Ethernet ##

 - Cisco Inline Power er ekki POE. Really old technology.
 - 24v er passive POE. 48 v is Standard POE.
 - If something uses Passive POE, you need to manually set the port to POE, the switch doesn’t detect that it should send out POE.
 - **Command to verify POW**: show power inline, can also use “power inline ?” to see option

 ![[CCNA/OSI Model/Layer 1/Untitled.png]]
 