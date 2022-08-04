[up](../index.md)

## The last four registers

- 28 - gp - Global Pointer
	- Ignore, we don't use it
- 29 - sp - Stack Pointer
	- Use it what it should be used for
	- Push to the stack
	- Pop from the stack
- 30 - fp - Frame Pointer
	- Used by standard stack frame
	- Not really sure what it does
- 31 - ra - return address
	- Where functions go to when they're done.
	- Set when you call a function
	- Two functions deep, gotta use the stack.

## A few more mathematical things

*Division, Multiplication, Mod*

These are much more complex than addition and subtraction.

`MULT rs,rt` writes its result to `hi` and `lo`, which are special purpose registers.

`MFHI rd` copies `hi` to `rd`.
`MFLO rd` does the same.

The simulator for this class does not support 64bit numbers, so we'll be ignoring `hi`.

## Mult pseudo - we can use this

`MUL rd,rs,rs2`. Multiplies rs and rs2, then copies lo into rd.

rs2, aka source 2, can be an immediate or a register. Either works here. If it's an immediate,
it loads it into $at, the assemblers reserved register.

## Division

`DIV rs,rt`. `lo=rs/rt`, `hi=rs%rt`

There are some pseudo instructions here that we can use, yay.

`DIV rd,rs,src2` rd = rs/src2. src2 can be an immediate if you want.

`REM rd,rs,src2` rd = rs%src2

Easy game, easy life.

## Load Immediate

Pseudo Instruction, we can use it. `li rd, imm` makes code more readable.

## Copy register to another register

There are a lot of ways to do this. To make code more readable, we have

`MOVE rd,rs` rd=rs

Arithmetic Operations complete! Now on to...

# Move to Memory

Memory is byte addressable - every byte has it's own address.

Multiple bytes in one unit

4 bytes makes a word

Next: how to read.
