# CDP #
- CDP is a layer 2 protocol.
- It is used to share information with other directly connected Cisco equipment, such as operating system version and IP address.
- This is a helpful tool to map out a diagram of the network.
- It sends CDP packets every 60 seconds.
- It is supported on physical interfaces and sub virtual interfaces.

```show cdp```
```show cdp neighbors detail```

- If you want to disable cdp becaus of security concerns.
```no cdp enable``` // this is done on the interface, not global config.
```no cdp run``` // this is done in global configuration, it disables it on all interfaces.


# LLDP #
- Link Layer Discovery Protocol.
- It's an open standard.
- LLDP is only supported on physical interfaces.
- Can discover Linux servers, CDP does not.

```show lldp```
```show lldp neighbors```
```show lldp neighbors detail```

```lldp run``` // done in global config
```no lldp run``` //done in global config
```no lldp transmit``` //done on the interface
```no lldp receive``` //done on the interface

