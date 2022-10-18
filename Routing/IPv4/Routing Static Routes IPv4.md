# Routing #
## Static Routes IPv4 ##

-   Static route using an Outbound interface. `ip route 192.168.1.0 255.255.255.0 (Usually we put the next HOP ADDRESS here), instad we can put the outbound interface, S 3/1.` That’s for a serial interface, doing that for fast eth or gig interfaces isn’t recommended. If we do that for ethernet, if a packet comes in and we tell it to use an exit interface and the router doesn’t know anyting about who the next hop is, it makes the router do something bad, it makes the router arp. If the next router has proxy arp enabled then it will forward the packet. That’s not optimal, we want to include the next hop when we are doing static routes. If it’s a serial point to point link, not including the next hop address is okay.
- `ip route 192.168.1.0 255.255.255.0 g 1/0 10.12.0.2 (next hop address)`
- `Show ip route static`
- To add a higher administrative distance, we put it add the end of a ip route command. `ip route 192.168.1.0 255.255.255.0 10.13.0.3 55`.

### Longest Prefix Match ###

- When you have two overlapping routes, the longest prefixt will be selected. The most specific match will win.

## Floating Static Routes

-   The default for administrative distance for static routes is 1.