# Upgrading #
- https://software.cisco.com
- ```show flash```
- copy tftp flash
	- insert tftp ip address.
	- source filename.
- ```show flash```
- You should see the new one.
- Under global config: ```boot system flash:systemimage-filename.bin```
- ```copy run start```
- ```reload```
- 