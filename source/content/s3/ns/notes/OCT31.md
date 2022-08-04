[up](../index.md)

# Housekeeping

- DNS 2 will be released tomorrow
- DNS1 AND DNS2 (labs 5 and 6) are both due on the same date,
three weeks from now.
- VOIP1 and 2 will be due on the last monday of this semester

# DNS Components

- Name Servers
	- contains info about a specific part of the db
	- holds resource records in zone files
- Resolver
	- Queries the DNS system
	- Get an RR, store for TTL
- Resource Records
	- Key value pairs with types
	- Name -> IP
	- IP -> Name

The DNS database is distributed across the planet. Each server only needs to
know the names and IPs of it's own machines and subdomains.

## Steps of Resolving

### Iterative

Ask a name server for an IP for a name - it tells you the ip of the next name
server to ask.

### Recursive

Ask a name server for an IP for a name - it asks another name server - it asks
another name server - and so on until an answer is sent all the way back up the
chain.

## Cache

The server that owns the namespace may respond with authoritative answers with a TTL.

Intermediate servers may cache the response, and reply pre-emptively with a non-authoritative answer.

Clients can request authoritative answers only, telling intermediate servers to
not respond with their cached data, and instead run the request all the way to
the authoritative server.

## servers

- Primary
	- Authoritative on one or more zones
	- Loads zone info from local
	- info is authoritative
- Secondary
	- Contains authoritative info
	- Gets info from a primary
		- Checks for larger serial number on primary, copies zone file.
- Caching Only
	- contains no authoritative info for any zones
	- Knows how to resolve names

## Linux Config

- named.conf contains info on what zones this server has info on
	- Tells where zone files are stored

```
options{
	directory "/var/names";
};
zone "supersecretsoysauce.com" {
	type master;
	file "supersecretsoysauce.com.dns";
};
```
