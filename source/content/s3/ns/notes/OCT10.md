[up](../index.md)

# Housekeeping

DHCP lab due monday

# Advanced DHCP Topics

If the server offers an addr, the client ARPs to see if its already in use. If it is,
client sends server DHCPDecline. Server marks addr as in use and notifies admin.

### Multiple NICs

Each NIC runs it's own DORA process and receives its own addr.

### DHCP Relay Servers

Relay picks up broadcast from client, converts to unicast to server. Relay fills in
giAddr field (default gateway).

Routers most commonly also act as a dhcp relay

Relays may support a threshold - only forward requests if the seconds field is above
a threshold.

Seconds field in DISCOVER messages tells how long it's been since the client started
searching for an addr.

Theshold can be used to only forward requests if a server doesn't respond in time.

### DHCP Failovers

split and mlt parameters are set on primary and communicated to secondary.

If one DHCP server goes down, the other takes over.

Their clocks must be synchronized, they must be able to communicate with each other.

In fact, almost everything needs to be the same so they can stand in for each other.

Five parameters defined on primary, 3 on secondary.

Max Response Delay - How long to wait for messages from peer before assuming the
peer is down.

Max Unacked Updates - How many messages I send without a response.

Maximum Client Lease Time - Primary Only - How long a peer can renew a lease
without informing the other peer.

Split - Load balancing between primary and secondary. Hash the client MAC, if it's
less than 128 then one peer does it, otherwise the other. 50/50 split load balancing.

Load Balance Max Seconds - Load balancing disabled after this much time, so a peer
can issue a lease while the other is down.

### Summary

Client sends DISCOVER via broadcast. Relay agents forward to both servers.

Servers determine which will handle the lease

If a server goes down, one peer may issue/renew leases.

### Windows

It's possible to configure this on windows, but it's more complicated.
