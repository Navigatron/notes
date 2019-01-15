[up](../index.md)

# Housekeeping

Lab6 typo, ohno.

- LambSauce
	- Primary for myco
	- secondary for theirco
- Wisdom
	- Primary for theirco
	- Secondary for myco

Question 8 adds host records - these need to go into theirco, not myco.

There's an incorrect middle picture, but the final result pictures are correct.

New centOS machine for mngmnt.myco primary

> Generating dnssec keys takes 2 hours due to lack of entropy.

Lab6 won't be due until after break. Woohoo!

# VoIP - Voice over IP

Instead of using the phone system, sound data is send over the internet.

pots - Plain Old Telephone System

Voip attempts to do the same thing as pots, but with packet-based switching instead of circuit based. Voip typically has PoE, Power over Ethernet, so voip phones don't need independent power.

There are typically two connections - TCP sets up and sends control signals - UDP or other protocol is used for the realtime, low-latency part.

Voip converts analog sound signal to digital format via a *codec*. At the other end, the same *codec* converts the digital back into sound.
