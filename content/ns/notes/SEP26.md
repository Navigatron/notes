[up](../index.md)

# Housekeeping

- Lab Report Questions
    - STATE
        - netstat after the experiment
        - Server side
    - ACKS
        - standalone
        - piggyback with data

# TCP Teardown

In this example, client initiates teardown. In reality, either party can initiate teardown.

This differs from handshake, where server listenss and client must initiate.

1. client FIN
2. server ACK
3. Server sends data until it's done - connection is in "half-closed" state.
4. server FIN
5. client ACK

Look closely at sequence and ack numbers to determine exactly what is acking what.

If, at any point, something goes terribly wrong, an RST is sent.

# TCP option negotiation

options identified by `KIND` number - 1 byte in length - 256 possibilities.

Options are either single byte or multi-byte.

Single byte options consist of only their KIND number.

- EOP
    - end of option field
    - KIND 0
    - used as padding to move data to 32 bit boundary
- NOP
    - No Operation
    - KIND 1
    - used to pad options list

Multibyte options have KIND, length, data

- MSU
    - Maximum Segment Size
    - KIND 2
    - default is 536
- WSF
    - Window Scaling Factor
    - KIND 3
    - window size is set to 2^n, where n is WSF
- Timestamp functions
    - Used to calculate round trip time
    - KIND 8
- SACK
    - Selective Acknowledgment
    - KIND 5
    - If both send SACK-permitted during handshake, then SACK is set for duration of data transfer.
    - Useful for recovery from dropped/missing packets.

# TCP Timers

Timers control a lot of flow.

- Re-transmission Timer
    - Timer is set for every segment sent.
    - Segments stay in queue
    - Time based on round-trip time [SMA(4)]
        - \alpha (last RTT) + (1-\alpha )(Current RTT)
    - If the timer expires, restart the timer and re-transmit.
    - Once the ACK is received, segment leaves queue.
    - There's only one timer.
