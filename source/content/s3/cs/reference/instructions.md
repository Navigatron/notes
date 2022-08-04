[up](../index.md)

# Quick Reference - Instructions

symbol | meaning
---|---
`dest` | destination, where results are stored to.  
`s1` | A source register used in a calculation.  
`imm` | an immediate value.

## Real instructions

### Easy ALU instructions

opcode | name
---|---
`add` | add
`sub` | subtract
`and` | bitwise and
`or` | bitwise or
`xor` | bitwise xor
`nand` | bitwise nand

All of the above take a destination and two sources, in that order. All of the above can be followed by an i to replace the second source with an immediate.

### not

`not` is an ALU instruction that only takes two operands - dest and source. There is no immediate version.

### Multiplication

`mult s1, s2`

Multiplies s1 and s2, stores the result in HI and LO. see `MUL` under legal pseudo instructions.

### Division

`div s1, s2`

Stores s1/s2 into LO. Stores the remainder, s1%s2, into HI. There are pseudo-instructions we can use here.

### Move from High/Low

`mfhi rd`

moves HI into the destination.

`mflo rd`

moves LO into the destination.

## Legal Pseudo Instructions

### Multiply

`mul dest, s1, s2`

multiplies s1 and s2, then moves LO into dest.

Expansion:

```
MULT s1, s2
MFLO dest
```

### Load Immediate

`li dest, imm`

Put an immediate value into a register.

Expansion:

```
addi dest, $zero, imm
```
