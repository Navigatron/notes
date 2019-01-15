[up](../index.md)

# RARP / BOOTP / DHCP

Arp connects layer two to layer three - finding MAC address of IP address.

RARP = reverse arp. send mac, recieve ip

boostrap proto, aka bootp.
built to move more than just ip - dns, gateway, etc.
server tables built manually

dhcp was built on bootp

Bootp server replies to client request with stuff, one of which things is called the "Magic Cookie"

In DHCP, there's another message type: DHCP Message, code 53.

BOOTP relays! relays relay from the current subnet to the subnet with the bootp server.
This allows one server to serve multiple subnets.


Windows caches protocol stack info.

## DHCP

remember DORA.

there are 8 dhcp messages. 4 are used in the handshake.

- (D)iscover  
	- client -> server
	- opcode 1
	- discover dhcp servers
- (O)ffer  
	- server -> client
	- opcode 2
	- "I'll serve you"
- (R)equest  
	- client -> server
	- opcode 1
	- "Please Serve me"
- (A)cknowledge
	- server -> client
	- opcode 2
	- Actually served the client info

Magic cookie to start options, option code 53 tells that it's DHCP, code tells which DHCP message it is.
