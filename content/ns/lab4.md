[up](./index.md)

# Lab 4

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

## 6.1

I'll put the configs here when I figure out what they need to be


1. Clone Yukon, name the new VM Gold.

Gotta punch a hole in the firewall
```
firewall-cmd –-zone=public –-add-port=321/udp –-permanent
firewall-cmd –-zone=public –-add-port=321/tcp –-permanent
```


## 6.2

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

Remember to add backup server as destination in windows relay

#### Report 10 a
1. Stop DHCPD on PRIMARY
1. Release on WC
2. release on LC
3. Start wireshark on RELAY and PRIMARY
4. renew on WC
5. renew on LC
6. Stop + Save Captures
5. Dump `ipconfig /all` on WC
5. Dump `/var/lib/dhclient/dhclient.leases`

#### Report 10 b
Stop SECONDARY, restart PRIMARY. Run above, skipping step 1.

#### Report 10 c
Restart SECONDARY, Run 10A, skipping step 1.


# TODO before leaving Lab

- get windowsunderlinux from network B sirloin for 4.2
- get linuxunderlinux from network B Russet for 4.2
- get 4.3 files
- Backup A-Flank due to major changes
- Backup B-Yukon
- get dhclient.leases.txt from B-Russet
- get dhclient.leases.relay.txt from B-Russet
- get windows.leases.txt from B-Sirloin
- Make the dhcpd.conf file from the end of Activity 2
- I ate the caffeine, I have to finish now
