[up](../index.md)

# Housekeeping

- Midterm on Monday
	- involves dhcp configuration
	- Crib-sheet
		- 8.5x11, **1 sided**
		- DHCP config
		- DHCP state machine
		- TCP state machine
- MyCourses Quiz this weekend

# TCP Timers

- Re-transmission Time Out (RTO) (Did you get that?)
	- How long to wait for an ACK before re-transmitting
	- Time based on SMA(Round Trip Time[RTT])
		- a * (last RTT) + (1-a)* (Current RTT)
		- alpha often 0.90
	- Timer activated when first item in queue sent
- Persistence Timer (Can I send more Data?)
	- On window size zero, the other end has no room to accept more data
	- If we wait, other side clears buffer, they send non-zero window size.
	- But what if we don't get the non-zero message?
	- after Persistence Timer, send "Probe", requesting window size.
- KEEP_ALIVE (Are you still there?)
	- If there's no traffic for a while, what do?
	- Send ACK probe (request repeat ACK) every two hours
		- expecting reply of repeat ack
	- No answer?
		- 10 attempts, 75 seconds apart, then drop connection.
- FIN_WAIT
	- Client sends FIN, moves to fin_wait_1 state
	- When server acks the fin, move to fin_wait_2
	- Wait for the server's ack for 10 mins before dropping
- TIME_WAIT
	- If the client recieves a FIN while in FIN_WAIT_2,
	- first of all, ack it
	- Wait for 2xMSL (Max time segment may live on network) before closing.
	- Allows client to receive delayed things or ack probes

# TCP finite state machine

Movement from one state to another depending on outside events.
