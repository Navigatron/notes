[up](./index.md)

# Lab 4

## Structure

- Network A
	- Bench 1
		- 71.1
	- Flank
		- Windows Server 2k16
		- DHCP Server
			- Pool of 1 through 30
			- exclusions of 1 through 16
			- reservation of .12 for sirloin
		- 71.2
	- Tenderloin
		- Windows server 2012
		- DHCP Relay Agent
		- 71.3
	- Sirloin
		- Windows dhcp client
		- reservation for .12
		- WindowsUnderWindows DORA analysis capture
	- Russet
		- Linux dhcp client
		- Dynamically assigned from DHCP
		- LinuxUnderWindows DORA analysis capture
- Network B
	- Bench 2
		- 72.1
	- Yukon
		- CentOS
		- DHCP server
			- Subnet 1
				- 40 to 42
			- subnet 2
				- 46 to 60
			- reservation of .48 for russet
		- 72.2
	- Sirloin
		- windows dhcp client
		- Dynamically assigned via DHCP
		- WindowsUnderLinux DORA analysis capture
	- Russet
		- Linux dhcp client
		- reservation for 72.48
		- LinuxUnderLinux DORA analysis capture

# Activity 3.3

Creating new temp VM named roger, windows 7

1. Change registry keys on server and client
2. release, start capture, renew, stop capture on Roger

Test	| Client DhcpConnForceBroadcastFlag | Server IgnoreBroadcastFlag	| Capture
4 		| 1 - Broadcast						| 0								| 3.3.1
3		| 1 								| 1								| 3.3.2
2		| 0 - Unicast 						| 1								| 3.3.3
1 		| 0									| 0								| 3.3.4


# Activity 4.1

4.1.WindowsUnderWindows on Roger, network A
4.1.LinuxUnderWindows on Russet, network A

# Activity 4.2

This is where it all goes to hell, config file is incorrect.
