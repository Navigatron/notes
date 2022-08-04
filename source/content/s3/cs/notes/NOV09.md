[up](../index.md)

# Housekeeping

- It's the last day to withdraw
- Lab 6 is due tonight
- Exam 3, Nov 14th, next Wednesday, GOL3435
	- Review sesh, monday nov12, gol2590, 11am
	- Linkers through ALU, code is on the table

# A side-track - the ALU - Arithmetic and Logic unit

In preparation for the next lab, we're putting off register files - right now, we're talking about the ALU.

The ALU is a combinational circuit - so we can represent it as boolean expressions, and/or a truth table.

This truth table has 2^64 rows. It's impossible to build.

Rules to make it possible to build:
- No solving 64bit problems
	- Instead, it can be broken into 32 2-bit problems.
	- This makes it solvable - but it's still messy
- Build functions as separate circuits, and use a mux to choose output

To find Result(bit i), take A(i) and B(i)

Doing bitwise operations is trivial. A(AND)B -> mux, done. Let's do addition.

A | B | C(in) | C(out) | R
---|---
0|0|0|0|0
0|0|1|0|1
0|1|0|0|1
0|1|1|1|0
1|0|0|0|1
1|0|1|1|0
1|1|0|1|0
1|1|1|1|1

This truth table matches 3-input xor exactly.

R = A XOR B XOR Cin
Cout = AB+AC+BC

This is a circuit called a full-adder.

```
       |
  +----+--------+
  |    C-in     |
  |  Full-Adder |
--+A            |
  |            R+--
--+B            |
  |    C-out    |
  +----+--------+
       |
```

Putting all these in a row creates a 64xPropogation delay system. It turns out, this is okay. In this class, this is how it will be done.

In the real world, carry lookaside buffers are very cool and work much better.
