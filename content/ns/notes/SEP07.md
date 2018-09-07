[up](../index.md)

# Review of IRS

## housekeeping

- read unofficial scapy guide
- read lab 2 instructions
- submit lab1 report before 7am
- Get screenshots of lab1 for signoffs

## Layer 1 - Physical

Wires connecting NICS. Possibly Radio Waves.

## Layer 2 - Data Link

MAC addresses. IEEE assigns vendor prefixes.

Ethernet Frames. Everyone hears them.

Destination is first so frames can be discarded quickly.

Type field tells what protocol to go to at layer 3.

IEEE Standard | What is it
--- | ---
802.5 | token ring
802.11 | wifi
802.3 | mac sublayer of data link + physical layer

MTU := max transmission unit

ethernet MTU is 1518

Switches learn where messages come from.
