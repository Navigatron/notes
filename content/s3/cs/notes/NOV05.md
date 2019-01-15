[up](../index.md)

# Housekeeping

- Lab 6 is due this Friday
	- There's discussion on X forwarding?
	- SSH clients?
	- sftp file transfer?
	- oh no
	- Note on experiment 2 - it starts at zero, that's not a typo
- Project one exists
	- Note: Backtracking is inherently slow. Prune early and often. Do every pruning you can possibly do.

# The One-Bit storage cell

## Async version - "The Latch"

### S.R. Latch

component | output goes to
---|---
input R | Nor1
input S | Nor 2
Nor1 | Output Q, and Nor 2
Nor2 | Output Qbar, and Nor 1

> I might have to switch to paper notes

Timing diagram:

Inputs | t0 | 1 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8
---|---
R  |   | 0 |   | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0
S  |   | 0 |   | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1
Q  | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1
Qb | 1 | 1 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 0 | 0

If the input is zero zero, the output does not change.

Characteristic Table

S | R | Q(T+1) | name
---|---
  0 | 0 | Qt | no change
  0 | 1 | 0  | reset state - R stands for reset
  1 | 0 | 1  | set state - S stands for Set
  1 | 1 |    | Undefined

  Just don't send a one one.

  Definitions:

  a synchronous 1-bit storage cell, is a flip-flop.

  add a control signal, C - if C is zero, we want to ignore input. sending zero zero has no effect on the state, so if C is zero, send zero.

  in short, and R with C and and S with C, so that they only pass through when C is high.

  
