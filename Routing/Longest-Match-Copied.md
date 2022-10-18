Comparing Two Routes Based on Longest Match

Say you want to get to a host, 192.168.4.17. You as the source do cannot know anything about the network this host lives on, but the routers will need to make a decision about which network to send it towards.

Say your router has the following networks in the routing table that it could send it to:

0.0.0.0 /0 - Gi0/1
192.168.4.0 /24 - Gi0/2
192.168.4.16 /28 - Gi0/3

To determine which route is best based on the longest match, you need to know which network and mask will match the most bits while including the source IP you want to reach. Start with your destination IP: 192.168.4.17: 11000000.10101000.00000100.00001001. You want to match the most bits without being in a network that cannot include this IP. Any bits in a destination network that are on must match the destination host bits.

0.0.0.0 /0: 00000000.00000000.00000000.00000000
• This matches all hosts because all bits are off, any bit can match. This is the least specific IPv4 route you can make.
192.168.4.0 /24: 11000000.10101000.00000100.00000000
• This matches the first three octets in this case. Any IP in the last octet can be anything.
192.168.4.16 /28: 11000000.10101000.00000100.00001000
• This matches the first three octets like the previous one, in addition to also matching the first 5 bits of the last octet. From left to right, this matches the most bits hence is the longest match.

Note that you cannot skip bits, it must be the longest contiguous match from left to right, not the most exact match.
