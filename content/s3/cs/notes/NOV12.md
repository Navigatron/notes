[up](../index.md)

# housekeeping

There is a test next class, wednesday. Exam 3. Room 3435, same as last times.

Block diagrams need:
- Labels
- Inputs
- Outputs

Project1 oh no, try test is now up and running.

Experiment 7 will be released today, due Monday of thanksgiving week.

# nov12 - ALU continued

Ai and Bi go into many different things, and the multiplexer decides what gets shipped out. So far, we have and, or, and addition.

## Subtraction

A-B = A+(-B) = A+((!B)+1), due to Two's Complement

Why build a new circuit when we could just hijack the input to addition?

Use the magic of XOR:

A XOR 0 = A
A XOR 1 = !A

Therefore, B XOR (subtraction flag) makes B correct for the ADDer function - with the exception of the +1.

Oh no, getting very clever. Send the subtraction flag to the Carry-In of the low order bit. This handles the +1 when subtracting, and lets addition still have a zero.

## Truth Table so far

Add/Sub | S1 | s0 | Function
---|---
 0 | 0 | 0 | And
 0 | 0 | 1 | Or
 0 | 1 | 0 | Add
 0 | 1 | 1 | ???
 1 | 0 | 0 | And
 1 | 0 | 1 | Or
 1 | 1 | 0 | Subtract
 1 | 1 | 1 | ???

There's some lost opportunity in that there's two ANDs and ORs, but this isn't a big problem. There's two slots we have left to define.

## Overflow

If the carry in does not match the carry out of the high-order bit, there is overflow.

The XOR comes back! carry-in XOR carry-out returns 1 if overflow.

ALU has two outputs now - n-bit number, and overflow flag.

This only has meaning when using the full-adder - otherwise it's useless.

## Other things?

Jumps don't need math, just appending. Shifting is done somewhere else.

Load word adds a register and a constant - we've already got addition.

How about slt? Set Less Than?

`slt	rd, rs, rt`

Subtract rt from rs into temp, and set rd to 1 if temp < 0, aka if the sign bit is 1.

## Set if Less Than

Send a zero to input 3 of all multiplexers except the low-order bit.

While input 3 is selected, the full-adder is still running. We can take the output of Full-adder 31 and send it to input 3 of the low order bit multiplexer.

That's complicated. Bit 31's full-adder also goes to the SLT line of bit 0. Everyone elses SLT line is zero - output of SLT is either 0000..0001 or 0000...0000

Now filling in the truth table.

## Truth Table so far, again

Add/Sub | S1 | s0 | Function
---|---
 0 | 0 | 0 | And
 0 | 0 | 1 | Or
 0 | 1 | 0 | Add
 0 | 1 | 1 | *ERR - nothing useful.*
 1 | 0 | 0 | And
 1 | 0 | 1 | Or
 1 | 1 | 0 | Subtract
 1 | 1 | 1 | **SLT**

## There's another one. BEQ - branch if equal.

In this case, it does a full subtraction of the two args. They're equal if the result is all zeros. NOR together all the output wires, and we get a 1 if equal and a zero otherwise.

That output wire goes back to the control unit, so it can decide what to set $PC to next.

## That's the ALU. Here's the Block Diagram

Should look like pants.

```
       S:123
         |||
       |-+++-\
 A(32)-| ALU  \
       \       \
        \ IsZero|-1  (On if inputs are the same)
         |   Res|-32 (Result of operation)
    	 |OvrFlw|-1  (Flag if there was overflow)
        /       |
       /       /
 B(32)-|      /
       |-----/
```

## Register File

```
MIPS 32x32bit register file
   +--------------+
 5-|RA1           |
 5-|RA2         R1|-32
  -|Write         |
 5-|WA          R2|-32
32-|Wdata         |
   |              |
   +--------------+
```

RA1 decides what register to output R1
RA2 decides what register to output R2

Write is a flag - weather or not to write a register

WA decides what register to write to
Wdata is the data to write to register WA, if write is on.

Tune in next time for more register file
