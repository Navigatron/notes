[up](../index.md)

# Housekeeping

- IBM has a thing going on outside Golisano, check it out?
	- Mobile X-Com unit demo tomorrow 9 am to 11 am

# DNS Configuration

- SOA (Start of Authority) Record
	- The serial number is checked at startup and every 15 minutes.
	- If the serial number on disk is larger than the one in memory, the zone record is reloaded from disk.

## Record Types

- NS
	- defines name of nameserver for a domain.
- A
	- defines IPv4 address for a name
- CNAME
	- defines the actual name for an alias name
- MX
	- define the name of a mailserver for a domain
- TXT
	- records plain text for a name

HINFO and WKS also exist, but are rarely used.

## Shortcuts

`$TTL` can be used to declare a default time to live
`$ORIGIN` is pretty cool

Leave any field empty, and it takes the value of the above field.

## Slave Zones

Slave DNS polls a master server. The master transfers a zone file to the slave, which then
serves records from memory exactly like the master does.

This can be used to easily distro zone files between a network of DNS servers, and
easily enable backups - to keep DNS online, all the time.

## Forwarding

If, say, a DNS server cannot get through a firewall - it can forward to a specific other server if it cannot answer a request itself.
