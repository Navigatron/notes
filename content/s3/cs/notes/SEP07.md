[up](../index.md)

## How do I get One?

Load it from memory - slow
Divide something by itself - slow

I really want some way of having literals. Please?

Data can be in:
- Registers
- Memory
- Can we have another please?

Yes! Constants in the Instructions!

## Immediate Values

A *short, signed* constant inside the instructions.

`ADD` uses registers, and
`ADDI` uses an immediate. Immediates must be third.

Can't use SUBI, it's just ADDI with a negative immediate.

I can use *any* real instructions.

floating point and double word instructions are not supported by our assembler.

- `ADDI`
- `ANDI`
- `ORI`
- `XORI`
- `NANDI`

How to put an immediate in a register?

Register zero (`$0`) always contains zero. It's literally wired into ground. You can read from it all day and dump data into it all day.

There's a pseudo-instruction called `li` - load immediate. It takes a destination and an immediate. It expands to `ADDI rt,$0,imm`. We are allowed to use this.

## Register Table

We must always use the Aliases. Precede aliases with `$`

Number | Alias | Purpose
---|---|---
0|zero|always zero
1|at|reserved for assembler
2->3|v0,v1|expression eval, function results.
4->7|a0->a3|(A)rguments passed to procedures and functions
8->15|t0->t7|(T)emp - can be overwritten by functions. Set->Used->Forgotten.
16->23|s0->s7|(S)torage - Saved by called functions. Save it, use it, then restore it.
24->25|t8->t9|(T)emp more
26->27|k0->k1| reserved for OS. Interrupts will eat these.
28|gp|Global Area Pointer
29|sp|Stack Pointer
30|fp|Frame Pointer
31|ra|Return Address Register
