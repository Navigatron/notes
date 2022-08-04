[up](../index.md)

# Housekeeping

- Lab 5 is in progress.

# DNS Day Two.

There are 13 ip addresses to the root DNS servers. Behind those addresses, there
are 919 physical machines.

All the root domain servers do is delegate to the correct top-level domain
name server. For example, root may delegate to edu.

The process of delegation continues until a server has the desired info.

For example, edu delegates to rit, rit delegates to cs, and cs returns the IP of
Glados. (glados.cs.rit.edu)

## Fully Qualified Domain Name

- contains all parts (rit, edu, etc.)
- is 255 or less chars
- each part is 63 or less chars
- is globally unique
- ends with a period

## Preparing for Lab

- Read DNS and BIND by Paul Albitz and Cricket Liu
	- chapters 1 and 2
	- chapters 3 and 4
	- chapter 11
- Watch BIND and DNS video on lynda
- Build some new VMs2
