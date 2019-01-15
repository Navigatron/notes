[up](../index.md)

# Instruction Encoding

## R-Type

ALU instructions look like:

`ADD rd,rs,rt`

We've got 32 bits to work with

opcode | rs | rt | rd | shift amount | function code
---|---
6 bits = 0x0 | 5 bits | 5 bits | 5 bits | 5 bits | 6 bits

> "Decisions are bad"

The goal is to keep the number of instruction formats as low as possible. But we have to have big immediates, so there is a second one.

## I-Type

opcode | rs | rt | immediate
---|---
6 bits | 5 bits | 5 bits | 16 bits

We can't have 32 bits for the immediate. 16 is the next best number, leaving 6 bits for the opcode. This means 64 opcodes - that's not enough.

> The way they chose to went

R type instructions start with six zero bits. The last 6 bits are the 'function' code, aka opcode at the end.

I type opcodes cannot be all zeros. There are 63 I type opcodes.

## Building a 32 bit constant in a register.

Assemblers are capable of doing simple math on constants at assemble time.

32 bit constant goal - split into lower 16 bits and higher 16 bits.

```
High = constant >> 16
Low = constant & 0xFFFF
```

### The old way: building with 3 instructions.

```
ADDI $to,$zero,const>>16    # assembler handles shift at assemble time
SLL $t0,$t0,16              # Shift Left Logical, move the high bits to the left
ORI $t0,$t0,const&0xFFFF    # OR the low bits into the register as well. Done!
```

### The New Way: Building with 2 instructions.

Use this fancy thing:
```
LUI rt,imm
```

Load Upper Immediate: Put an immediate into the top 16 bits, and zero out the lower 16.

```
LUI $t0,const>>16           # Put the top 16 bits into the top 16 bits, prep the lower.
ORI $t0,$t0,const&00xFFFF   # Put the lower 16 bits of the constant into the lower 16 bits
```

### The Not-Yet-Banned pseudo instruction: Load Address

*Unlike all other load instructions, this does * ***not*** *load from memory.*

This puts a 32 bit constant into a register.

`LA rt,32-bit-constant`

> I will Hound on this for weeks. Someone will get it wrong on the test. Load Address does not pull from memory.

using LA without a constant becomes something different. Prof won't tell us what happens.
