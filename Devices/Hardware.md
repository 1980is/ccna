# Devices #

## Memory ##
- ROM - Read Only Memory
	- That is used when the device is powered on, it will first load from ROM.
	- Two main functions are performed:
		- Power On Self Test (POST)
		- Load bootstrap. The bootstrap will ook in Flash for an IOS software image to load.
		- If an IOS image cannot be found the device will show the ROMMON prompt at the command line.
		- The ROM Monitor can be used to recover a missing or corrupted software image.
		- In this case you can boot from USB or an external TFTP server.
- Flash - newer devices use removable CompactFlash
	- The system wil load the first IOS image found in Flash by default.
	- You can override this with the ```boot system``` command.
	- You can copy additional IOS system images to Flash via TFTP or USB.
	- ```show flash``` 
	- ```delete flash:nameoffile.bin```  //don't do. :) 
- NVRAM - Non-Volatile Ram.
	- When the system has finished loading the IOS system image from Flash, it will load the startup-config configuration file from NVRAM.
	- The saved startup-config becomes the current running-config in RAM.
	- If no startup-config file is found, the device will load the Setup Wizard.
- RAM - Random Access Memory
	- RAM is volatile memory, its contents are lost when the device is powered off.

- VLAN database (vlan.dat) is saved in either Flash or NVRAM, depending on the model of switch.

## The Config Register
- ```write erase``` // Factory resets a router of switch. It removes the startup-config.
- ```config register``` in global configuration mode or ```confreg``` at the rommon prompt.
- Eg ```config-register 0x2142```
- 0x2102: boot normally (default).
- 0x2120: boot into rommon.
- 0x2142: ignore contents of NVRAM (startup-config).

## Password Recovery Procedure ##
![[Screenshot from 2022-02-03 19-14-54.png]]
![[Screenshot from 2022-02-03 19-16-36.png]]
