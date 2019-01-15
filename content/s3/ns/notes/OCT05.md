[up](../index.md)

# DHCP

- dhcpdecline
	- DORA complete, client sends ARP and someone is using the offered addr.
	- sends DHCPDecline, restarts DORA
- DHCPRelease
	- Client sends when done with IP
	- server returns address to pool

## Discover

- Options
	- magic cookie
	- others
	- end

## Offer

- Hop Count - how many relay agents to get to the server
- Other fields, like offered IP, client mac, etc.
- Only the first relay agent updates the relay agent IP field

## Request

## Acknowledgement

## Oh No

Client discovers, asking for an ip. IP is not available, server offers something else.
If the client wants to take the offer, it requests it.
If the client really wants what it asked for, it'll ask again.
