[up](../index.md)

# Housekeeping

Lab6 delayed for a while, exactly when not clear.

Lab5 still due monday.

# DNS

> Finishing going over message headers and such

## Pull and Notify

Secondary servers will re-check for updates when the TTL of their data expires. When an update is made on the Primary, there is a period of time where the secondary still serves the old info, until the TTL expires and it re-checks.

RFC 1996 implements NOTIFY, where primary servers can tell secondaries to do an early re-check.

## Incremental Transfer

When the secondary detects an updated serial number, it re-pulls the entire zone file. This can be a lot. RFC 1995 implements Incremental Zone Transfer, where the primary keeps track of changes and the secondary only requests the changes it needs. When starting up, secondaries pull the entire zone file - then on each re-check, they get only the recent changes.

## Dynamic update

DNS assumes IPs are static, and changes are infrequent.

However, in a dynamic dns, or with dhcp, this is not the case.

DDNS, dynamic domain name system, allows clients to edit the database. There are big security problems, but it's still pretty cool.

Tune in next time for VOIP, maybe?
