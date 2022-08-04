[up](../index.md)

# Housekeeping

- Experiment 1 due tonight at 11:59:59PM
- First exam next Wednesday, SEP 26
    - GOL 3435
- Review session for the exam
    - SEP 24
    - 11 -> Noon
    - GOL 2590
    - Q/A Session, no prepared material.

# Instructions that change execution location
*AKA "Flow Control"*

## The Fetch/Execute Cycle

1. Fetch Instruction from Memory
2. Decode the instruction
    - considers encoding
3. Execute the instruction
4. repeat, heckin' quick.

**Question**: Which instruction do we fetch?

Every instruction lives at an address - we've got a "Program Counter" that points at the next instruction to run.

## Types of change

- unconditional change
    - Jumps
- Conditional change
    - Branches

## Jump

name | opcode | operands
---|---
jump! | `j` | label as destination

goes to the label.

## quick break for a new instruction format

J Type - Built just for Jumps.

section|size
---|---
Opcode|6 bits
Destination|26 bits

We're trying to get a 32 bit address with 26 bits of instruction.

All addresses that are *aligned* are multiples of 4 - the last two bits are always 00. Now we represent 28 bits.

Jump instructions don't represent the upper 4 bits - we just don't overwrite them. Because our code will be less than 256Megs in size, this isn't a problem for us. I'm not sure what would happen if we wanted to jump between 256M sections.

## Jump Register

- Jump Register
    - `jr rs`
    - takes one register as target.
    - Uses R-Type encoding.

JR is used to return from a function. `$ra` contains return address, so we `jr $ra`

## Calling a Function

All we gotta do is put the program counter into the return address. But we can't mess with the program counter - so we get two more instructions that mirror the other jump instructions.

### Jump and Link

`jal label`

Goto the label, copy program counter into return address.

### Jump and Link Register

`jalr rs`

Goto address in register, copy program counter into return address.
