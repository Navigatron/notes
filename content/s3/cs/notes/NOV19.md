[up](../index.md)

# Housekeeping

- Reality is not in quantum state
- Experiment 7 is due tonight
- Extra credit project submit is tomorrow evening

# Register Transfer Language (RTL)

How data moves around

There is no standard, every book has their own version

Store, Move, Manipulate

Stand Alone Registers
- Alphanumeric names, A, B, PC, etc.

In a register file, use array notation, reg[31], tells what register we care about. Normally, rather than a number, we'll have a variable - Reg[rs] or such

Use subscripts to specify a part of a register - IR_31-26 specifies bits 31 through 26 of the instruction register, aka the opcode.

Moving data uses a left arrow `A <--- B`, this shows data from B is copied into A

Parallel ops are important

Ima make a table

Item | Notation | Example
---|---
Stand Alone Registers | Alpha-numeric name | A, B, PC
Register File | Array notation | Reg[A], Reg[rs]
Parts of a Register | Subscripts, Parenths | A_31, IR(31-26)
Move Data | Left Arrow | `A <---- B`
Parallel Ops | Comma | `A <--- B , C <--- D`
ALU ops | 'C' syntax | +, -, &, pipe, <, ==
Conditional | if,then | if *condition* then *transfer* , conditional must be *simple*
memory | array | Mem[effective address]
load | composite of above | `A <-- Mem[EA]`

Parallel swap, `A<--B, B<--A`, works perfectly fine.

The above is all we need for working with mips

> Phil city is a city just for Phil. It's a small city. It has his house, his job, and wegmans. That is life in phil city.

Instructions to Consider:
- ALU-R
- ALU-I
- Memory
	- sw
	- lw
- beq

Hardware to consider:
- Register file
- ALU
- Memory
- Program Counter

## ALU-R

- Fetch
	- IR <-- Mem[PC]
	- PC <-- PC+4
- Decode
	- Take the instruction, tear it into parts, send the parts away
	- A <-- Reg[rs]
	- B <-- Reg[rt]
- Exec
	- ALUout <-- A (operation) B
- WriteBack
	- Reg[rd] <-- ALUout

## ALU-I

- Fetch
	- IR <-- Mem[PC]
	- PC <-- PC+4
- Decode
	- A <-- Reg[rs]
	- IMM <-- S.E.(IR(15-0)) // ohno. "This will be trivial"
- Execution
	- ALUout <-- A (operation) Imm
- Writeback
	- Reg[rt] <-- ALUout

## Memory

- Fetch
	- IR <-- Mem[PC]
	- PC <-- PC+4
- Decode
	- A <-- Reg[rs]
	- Imm <-- S.E.(IR(15-0))
	- B <-- Reg[rt]
- Exec
	- ALUout <-- A + Imm
- Mem
	- Load Word
		- MDR <-- Mem[ALUout]
	- Store Word
		- Mem[ALUout] <-- B
- Writeback
	- Load Word
		- Reg[rt] <-- MDR
	- Store Word
		- None, doesn't do anything.

## BEQ

- Fetch as before
- Decode as in Memory
- Exec
	- isZero <-- A==B // sets isZero to 1 if a is equal to B
	- NPC <-- PC+Imm
- Mem
	- if(isZero), then PC <-- NPC

Rada rada rada

Tune in next time for... time!
