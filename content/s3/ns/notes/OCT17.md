[up](../index.md)

# Housekeeping

- Exam during Lab next Monday
	- Finish early? Lab 5 released.
- VMware was updated without testing the labs
	- Troubleshooting guide coming out eventually

# TCP

## Preview

- control mechanisms
	- Flow control
		- sliding window
		- silly window syndrome
	- Error Control
	- Congestion Control
		- Slow Start
		- Fast Re-transmit
		- Fast Recovery

## Flow Control

Flow control prevents the sender from overwhelming the receiver.

"Sliding window" is TCP's flow control mechanism.

The window size on the sender is determined by available buffer space on receiver.

### Sliding Window

Sender does not have to send a full segment - source can send what they've got
at any time.

The receiver can decide at any time to increase or decrease the sender's window
size. This is accomplished though specific TCP flags.

Bytes in the window are sent from left to right. As the ones on the left are
acked, the window slides to the right, revealing more bytes to send.

### Silly Window Syndrome

Consider typing in a terminal emulator over ssh. Each keystroke generates
1 byte. Sending 1 byte takes 58 bytes of overhead, which is silly.

Either the sender has small data, or the receiver can't process fast enough. In
either case, the sender is sending very small pieces, which is inefficient.

#### Nagle's Algorithm

1. Send the first byte
2. Wait until one of two conditions is true:
	- I have an mss of data
	- I receive an ACK from that first byte

#### Clark's Solution

Consider a receiver that has broadcast a window size of zero.

If the receiver sends small window sizes, silly window syndrome occurs.

Clark's solution says to keep sending a window size of zero until either:
- I have enough buffer to receive an MSS
- My buffer is now 50% free

#### Delayed Ack

Delaying ACKS reduces the amount of traffic - but we must avoid unnecessary
re-transmissions.

## Error Control

### Checksum

Checksums verify data integrity. Corrupted segments are thrown away, treated the
same as lost segments.

### Acks

Acks let the sender know that the message was received.

Cumulative acks ack continuous, contiguous chunks of data.

Selective acks allow the acking of non-in-order segments.

- This moves less data, though it sends more acks.
- Uses the TCP options field

Interesting thing - Later Acks help recover from earlier acks if RTO hasn't happened yet.

### Time-Out

If the data gets lost, or the ack gets lost on the way back, the RTO kicks in.

RTO tells us to re-transmit data if we don't hear back within a timeframe.

#### Fast RT

If we're using cumulative ACKs and we get 3 acks in a row for the same data,
we re-transmit that data.

## Congestion Control

When network load is greater than network capacity, there is congestion.
