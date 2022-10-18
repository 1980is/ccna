# NTP #
## NTP-CLIENT ##
```show ntp associations```
```show clock```
Config t:
```clock ?```
```clock timezone ARIZONA -7```
Config t:
```ntp server ?```
```ntp server 203.0.113.1```
NTP-MASTER-SERVER:
Conf t:
```ntp master 5``` (number can be random).
To have clients talk to the NTP-MASTER-SERVER.
Conf t:
```ntp server 10.16.0.1``` (IP Address of the NTP server).
