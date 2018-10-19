[up](./index.md)

# Lab 4

*Start Early*

## Structure

### Network A

Name | OS | Role | IP
---|---
Flank | WServer2016 | DHCP Server, Relay | .2
Roger | W7 | DHCP Client | .12, reserved
Russet | CentOS | DHCP Client | dynamic

### Network B

Name | OS | Role | IP
---|---
Yukon | CentOS | DHCP Server | .2
Gold  | CentOS | DHCP Server Secondary | .200
sirloin | WServer2012 | DHCP Client | dynamic
Russet | CentOS | DHCP Client | .48, reserved

# Activity 2

## 2.4

Save a copy of the dhcpd.conf file for report question 4. The instructions do not mention this.

# Activity 3 - Capturing DORA

## 3.1 and 3.2 - DORA Capture

test | client | server | pcap
---|---
1 | WS2012 (sirloin) 	| WS2016 (Flank) | windowsunderwindows
2 | CentOS (Russet)		| WS2016 (Flank) | linuxunderwindows
3 | WS2012 (sirloin)	| CentOS (Yukon) | windowsunderlinux
4 | CentOS (Russet)		| CentOS (Yukon) | linuxunderlinux

## 3.3 - Broadcast Flags

1. Change registry keys on server and client
2. release, start capture, renew, stop capture on Roger

Test	| Client DhcpConnForceBroadcastFlag | Server IgnoreBroadcastFlag	| pcap
---|---
4 		| 1 - Broadcast						| 0								| 3.3.1
3		| 1 								| 1								| 3.3.2
2		| 0 - Unicast 						| 1								| 3.3.3
1 		| 0									| 0								| 3.3.4


# Activity 4 - release and renewal process

Recording bootp packets for 2 minutes to see the renewal process

## 4.1

Release and renew under windows DHCP server.

See table in 4.2 for packet captures

## 4.2

Release and renew under linux DHCP server.

Remember to clear arp on the server before renew

test | client | server | pcap
---|---
1 | W7 (Roger) | WServer (Flank) | windowsunderwindows
2 | CentOS (Russet) | WServer (Flank) | linuxunderwindows
3 | WS2012 (sirloin) | CentOS (Yukon) | windowsunderlinux
4 | CentOS (Russet) | CentOS (Yukon) | linuxunderlinux

## 4.3 - Lease information

dhclient.leases.txt from Russet  
windows.leases.txt from B-Sirloin

# Activity 5 - DHCP Relay

## 5.1 - linux dhcp relay

### Step D

The command here is incorrect. Instead of:
```
cp /libsystemd/system/dhcrelay.service /etc/system/system
```
It should be:
```
cp /lib/systemd/system/dhcrelay.service /etc/systemd/system
```

### Step E

The command here is incorrect. Instead of:
```
vim /etc/system/systemdhcrelay.service
```
It should be:
```
vim /etc/systemd/system/dhcrelay.service
```

### Step g/h

pcap on Yukon, as linuxrelay

They don't tell you until the end of 5.2, but you also need to dump dhclient.leases here to prove the ip came from the other server.

dhclient.leases.relay.txt on Russet



## 5.2 and 5.3 - windows dhcp relay

You need to setup the Windows relay for activity 6, but otherwise don't bother with captures here, the report doesn't ask for them.

# Activity 6 - DHCP Failover

*The Beginning of the End*

## 6.1 - Setup

### My VM Structure

#### Network A

OS | DHCP Role | Name
---|---
Windows | RELAY | flank
Windows | Client | sirloin

#### Network B

OS | DHCP Role | Name
---|---
Linux | PRIMARY | Yukon
Linux | SECONDARY | Gold
Linux | Client | Russet

### Configuration

### Allowing the failover servers to communicate

#### Attempt 1 - Firewall Rules

```
firewall-cmd --zone=public --add-port=321/udp –-permanent
firewall-cmd --zone=public --add-port=321/tcp –-permanent
```

This allows traffic through the port, but the OS might not allow DHCPD to bind to the port. SElinux is the likely culprit.

#### Attempt 2 - Disable SELinux

This sets SELinux to permissive mode, which only logs things, no blocking.
```
setenforce 0
```

For me, this wasn't enough.

#### Attempt 3 - Disable SELinux, for real this time.

```
tail -f /var/log/messages
```

The above command shows the system log in real time. SELinux, while permissive, was still denying DHCPD access to port 321.

```
vim /etc/selinux/config
```

and replace `enforcing` with `disabled`. Use `:wq` and then:

```
shutdown -r now
```

Refer to [lab1 - secret commands to make CentOS less terrible](./lab1.md) to turn networking back on.

Remember to do this on both VMs.

## 6.2 - Capture... what? Oh, everything.

Neither the report nor the Instructions provide what specifically needs to be done.

### Structure
Name | Meaning
---|---
PRIMARY | CentOS Primary dhcp server on network B
SECONDARY | CentOS Secondary dhcp server on network B
RELAY | windows server 2k16 dhcp relay agent on network A
WC | Windows client on network A
LC | Linux client on network B

### Steps

The windows DHCP relay is configured to send to PRIMARY. Add a second destination, SECONDARY.

1. Make sure both PRIMARY and SECONDARY and RELAY are working correctly.
2. skip 'The Loop' - go right to 10a. (You'll jump back to the loop from there.)

#### The Loop

If 10a hasn't told you to 'run the loop' yet, goto 10a.

- SETUP
	1. Release on WC
	2. release on LC
- CAPTURE WINDOWS
	3. Start wireshark on RELAY (Net A logger)
	3. Start wireshark on PRIMARY (Net B logger)
	4. renew on WC
	4. Stop wireshark on PRIMARY
	4. Stop wireshark on RELAY
	5. Dump `ipconfig /all` on WC to {A|B|C}.wc.ipall.txt
	4. save wireshark files as {A|B|C}.{RELAY|PRIMARY}.wc.pcap
	4. release on WC to prevent lease extensions
- CAPTURE LINUX
	11. Start wireshark on PRIMARY
	5. renew on LC
	2. Stop wireshark on PRIMARY
	5. Dump `/var/lib/dhclient/dhclient.leases` on LC
	4. save wireshark files as {A|B|C}.{RELAY|PRIMARY}.lc.pcap
	2. release on LC
	4. `echo > /var/lib/dhclient/dhclient.leases`

#### Report 10 a - Only Secondary
1. Stop DHCPD on PRIMARY
2. run the loop.


#### Report 10 b - Only Primary
1. start DHCPD on PRIMARY
2. stop DHCPD on SECONDARY
3. run the loop

#### Report 10 c - Both running
1. start DHCPD on SECONDARY
2. run the loop

#### Clean-Up
1. Extract all ipconfig captures to flash drive
2. Extract all RELAY pcaps to flash drive
3. Extract all dhcp.leases files to flash drive
4. Extract all PRIMARY pcaps to flash drive
5. Backup ALL vms used.

# Time

*God help you*

## Lab

Event | Action | Time Spent | Running Total
---|---
Class Lab 1 | Got signoff 1 | 2 hours | 2 hours
Class Lab 2 | Not enough to get signoff 2 | 2 hours | 4 hours
Oct 16th | up to act6, TA MIA though. | 6 hours | 10 hours
Oct 18th | saving and restoring VMS killed DHCPD. Fixed that. | 2 hours | 12 hours

## Lab Report

Haven't started yet, I'm guessing this will take 4 to 6 hours.

# Lab Setup Protocol

- Enter Lab, Locate Bench
- Restart Machines
- Unpack
- Switch cables from DHCP to VLAN
- Configure bench IPs as 71.1 and 72.1
- Add mapped network drive
- Determine what VMs on network A
- Copy those VMs to A
- Determine what VMs on network B
- Copy those VMs to B
- Start network A VMs
- Start network B VMs
- Configure IPs of all running VMS
