[up](../index.md)

# TCP

## Congestion Control

TCP assumes lost segments are caused by congestion.

Re-transmitting creates more congestion.

Slowing down the sender happens through the receiver's advertised window size
and the "congestion" window.

### Methods of congesiton handling / avoidance

These are terrible notes, gotta look this up online.

1. Slow Start
	- CWMND size = 1 mss
	- On each ACK, CWND++
	- As soon as there's a re-transmission,
		- Set the "threshold" to half of current CWND
		- re-start slow start
	- If we hit the threshold, switch to additive increase
2. Additive Increase - Congestion Avoidance
	- Increase CWND by 1 for every full CWND we send and get back.
	- If we get three acks for the same thing, fast-retransmit.
		- half CWND
3. Multiplicative Decrease - Congestion alleviation
	- Half CWND?
