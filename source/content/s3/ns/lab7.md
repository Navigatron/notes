[up](./index.md)

# Lab 7 - VoIP

# Activity 1 - Vlan setup

Note from Prof:

> Use pc 1 as your client pc, use pc2 as your monitor

## Step 1 - Activate switch

- Grab some cables
- turn on your rack
- Connect switch D to pc console 1
- Open putty
- Select serial
- Select serial on the left, turn flow control off
- Connect!
	- No - do not enter initial configuration dialog
	- Yes - terminate autoinstall
	- `enable` - give yourself superpowers
	- `config t` - activate config mode
- Use the "Command Cheat Sheet"
	- "Configure the VLans" section configures the VLans
	- "Configure monitoring" sets up monitoring

# Activity 2 - Activate Router

## Part 1 - route between VLans
- Router on a stick, while cool, is not what we'll be using
- Use a cable to attach router B console to PC2
- putty, serial, no flow control, connect
	- No initial config dialog
- `enable`, then `config t`
- Follow "Command Cheat Sheets - Router interface configuration"
	- interface fa0/0
		- vlan 101
	- interface fa0/1
		- vlan 102


## Part 2 - Make the router a dhcp server
- enter config terminal mode
- Follow "Command cheat sheets - dhcp router config"
	- voice vlan
		- network defines the network
		- option 150 defines the tftp server address - in this case, the router.
		- default router sets the gateway of dhcp clients
	- data vlan
		- same as above minus option 150

## Part 3 - verify file presence
- use `exit` to leave config t or whatever, get back to `enable` level
- `dir`

# Activity 3 - Test Connectivity

## Step 1 - Can we do the ping?
- Use more cables, lol
	- port 1 - Voice monitor
	- port 2 - PC1
	- ports 3 through 5 - Voice vlan, nothing yet
	- port 6 - Voice vlan connection to router interface fa0/0
	- port 7 - monitor output
	- port 8 - PC2, for now
	- ports 6, 10, 11 - data vlan, nothing yet
	- port 12 - data vlan connection to router fa0/1
- On each PC
	- Open command prompt with admin
	- run `ipconfig /renew`
	- Ping from pc1 to pc2 (101.1 to 102.1)
- If ping works, continue
	- Unplug PCs from switch (Switch ports 2 and 8)

## Step 2 - spanning-tree portfast
I didn't need to do this.

## Step 3 - config phone lines

- Go get two phones from the cage
	- The one with the lower number yellow sticker will be called phone 1
	- Phone 1 SW port to switch port 1
	- Phone 2 SW port to switch port 2
- Once they boot, settings -> network, scroll down to MAC
- Write the MACS down
- **unplug the phones.**
	- Otherwise they steal registration slots from each other.
- Run: `ip tftp source-interface fa0/1`
	- This seems very wrong, and I don't know why it works, but it does

"Command cheat sheets - Config the lines for the phones" has enough errors with it that I'm re-writing the instructions here.

Yes, you have 7960s instead of 7961s. This still works. I tried it with 7960 and it didn't.

Obviously, replace the MACs in the instructions with the MACs you wrote down earlier.

```
enable
config t

telephony-service
max-ephones 8
max-dn 8
ip source-address 192.168.101.254 port 2000
load 7961 term41.7-0-3-05
max-conferences 8 gain -6
transfer-system full-consult
create cnf-files version-stamp jan 01 2002 00:00:00

ephone-dn 1 dual-line
number 1001

ephone-dn 2 dual-line
number 1002

ephone 1
mac-address 001B.D584.60E1 // replace
button 1:2

ephone 2
mac-address 001B.D584.603F // replace
button 1:1
```

- Hit CTRL+Z to apply changes
- Plug the phones back in and hope for the best

# How to get the signoffs

These will be out of order - that's okay.

## 2B

Take a screenshot of PuTTY when the router says the phones are registered.

## 2Signoff

Show an instructor that you can call the other phone

## 2C

Run a cable from switch output 7 to PC2 NIC. Start wireshark on PC2.

Call from one phone to the other.



# I had issues on attempt 1.

Below here are misc notes I took while troubleshooting.


`Show Run` on the router should reveal this:

```
telephony-service
 load 7961 term41.7-0-3-0S
 max-ephones 8
 max-dn 8
 ip source-address 192.168.101.254 port 2000
 create cnf-files version-stamp jan 01 2002 00:00:00
 max-conferences 8 gain -6
 transfer-system full-consult
 ```

> TROUBLESHOOTING

Phone | MAC
---|---
1 | 001B.D584.60E1
2 | 001B.D584.603F

- TERM41.7-0-3-05.loads
- term41.default.loads
- term61.default.loads
- Jar41.2-9-2-26.sbn
- cnu41.2-7-6-26.sbn
- CVM41.2-0-2-26.sbn



- tried tftp source 0/1, which sounds wrong
- oh no
- "host not found", says the phones, as they sit there sadly.
- They have IPs via dhcp, so that's good at least.
- Why cannot contact tftp server? Why cannot contact CME?

- IP dhcp pool is correct
	- Phones are getting ip addresses
- Option 150 is set
	- phones are getting tftp server address
- tftp-server [file]
	- Sets the file the tftp server is pushing
	- Phones load, I think this works?
	- Prof helping selected random file, idk which file to use?
	- Why is ip tftp source-address set to the data network? There's nothing there
- telephony-service
	-

`load 7961 [file]` in case I messed up in loading 7960

Lucas goes to switch config
Lucas re-runs my vlan commands
