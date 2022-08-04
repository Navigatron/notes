[up](../index.html)

## Housekeeping
- No labs up yet

## Assembly

Fixed line syntax
- Every assembly statement must be on one line
- that line will be rigidly formatted
	- Label
		- Name it whatever you want
		- Use good names, this is the only place you can name things
		- Names must be globally unique, because there is no scope
		- when compiled, becomes 32 bit constant equal to its memory location
		- More constant than C constants. *Very* constant
	- opcode
	- operands
	- comment

```
[label:][opcode[operand][,operand][,operand]...] [#comment]
```

### The Standards Guide

- No lines over 80 characters
- No indentation, because there is no scope
- Labels begin on left margin
	- No opcodes on lines with a label
- All opcodes begin 8 spaces from left (~1 tab)
- All operands begin 16 spaces from left (~2 tabs)
	- aka 8 spaces from where opcodes begin
- Once in the operand land, do whatever, as long as consistent.
- At least one space between last operand and comment
- All comments must align
	- Proff. is happy as long as they line up in a block
- If there's just one very long line, put that line's comment above it
	- add whitespace above/below long line + comment
- Block comments
	- for functions, left side.
	- within functions, 8 spaces from left.

### Comments are vitally important

- Graders read them to see what we're trying to do
- We need them to remember what we're trying to do

# Assembly!

MIPS is a load/store machine.
- LOAD moves from mem to register
- STOR moves from register to mem

## ALU Instructions

Arithmetic Logic Unit

*bitwise is become all.* There is no logical operations here, only bitwise.

All binary operators take 3 operands, which must be in registers.

Format for all ALU commands:
```
OPCODE $destination,$source1,$source2
```
The above performs the below:
```
destination = source1 (operator) source2
```

register format: `$x`, where x is the number of the register.

meaning | opcode
--- | ---
addition | `ADD`
subtraction | `SUB`
Bitwise And | `AND`
Bitwise Or | `OR`
bitwise XOR | `XOR`
nand | `NAND`

`NOT` takes two operands, destination and source. Meanwhile, `NAND`ing anything with itself (or `NOR`ing) does the same thing.

`NOT` is a pseudo-instruction. At assemble time, it expands to something else. Pseudo-instructions don't teach us the ISA, so they are forbidden, except for 7. `NOT` is one of the exceptions.

### i = i + 1; aka Constants.

grrr, cliffhanger. Come back next time.
