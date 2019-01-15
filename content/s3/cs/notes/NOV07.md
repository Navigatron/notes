[up](../index.md)

# Housekeeping

- Test 1 week from today, in the same room we're used to.

# More Latches and such

## D-Latch

The (1, 1) input causes problems for the SR latch.

What if we have input D, and send D to S and !D to R?

D | Q
---|---
0|0
1|1

This seems useless, but with clock cycles, it can remember one bit for one clock cycle.

If we take Q and pipe it back into D, we can remember a bit for as long as we want.

`D` can also mean delay, but we won't use it for that - for us, D is Data.

```
 +---------+
 | D-Latch |
-+D       Q|-
 |       !Q|-
 +---/\----+
```

Add a C input to the above to make it a D flip-flop.

## T-latch - (T is for Toggle)

T | Q(t+1)
---|---
0 | Q(t)
1 | !Q(t)

Every time it gets a one, it flips.

## JK Flip Flop

J | K | Q(t+1)
---|---
 0 | 0 | Q(t)
 0 | 1 | 0
 1 | 0 | 1
 1 | 1 | !Q(t)

 This is the master of all flip-flops. It can emulate any other flip-flop.

This is, however, complicated - so it's rarely used in real circuitry.

## what even is a register

N data wires in, N data wires out.

```
      +n
  +---+------------+
  | n-bit register |
 -+Load            |
  >                |
  +---+------------+
      +n
```

### The yell and ignore model

All components will be shouting their output at all times. Results will be calculated and piped to inputs - where they're either listened to or piped to nowhere.

The load input sets the register value if it's one - otherwise, input is ignored.

## Here's a 1 bit register to store bit i

- 2x1 mux, component A
	- load to select
	- in to data 1
	- Q to data 0
	- Output to D
- D flipflop
	- D from output of 2x1 mux
	- output Q to out, and data 0 of mux
	- !Q to nowhere

### You can turn this into a T flip flop.

replace data 1 of the mux with !Q from the D flippyflop

### You can turn this into a shift-register

take data 1 from Q of another register, and send Q to another register as well.

## Spaghetti for days

In mips, we have 32x 32bit registers.

This is an absurd amount of wires.

so we don't - we can't. Instead, we use:

## The Fleet of Buses

A bus is a "Common communication medium"

Some kind of control decides who may board the bus.

All registers read from the bus and write to the bus. Control decides who reads and who writes.

## Register File

The package of the registers - limits ins and outs to what's needed by ISA.

In MIPS, two buses come out and one bus goes in.

Next time, we'll build a register file and start the ALU.
