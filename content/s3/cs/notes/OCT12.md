[up](../index.md)

# Housekeeping

- Exp 4 due tonight!
- Exp 5 (the hard one) due the 24th
	- Build and Traverse a binary tree (Hard)
		- Traverse must be recursive
		- Build doesn't have to be
- Exam 2
	- Next Wednesday, OCT 17th
	- In class
	- GOL 3435
	- Review
		- GOL 2590
		- 11 to noon
		- Oct 15th

# Methods of IO

## Interupt Driven IO

- Ask the OS to do some IO
- OS records that you want IO, moves your process to waiting
- You no longer get time slices
- When there's IO, OS moves your process to ready so you can run.

Advanced IO requests, like read_int, wait for more than one byte.

With high-speed devices, this creates hella interrupts.

## Direct Memory Access IO

Allows IO to be managed off of the main CPU.

Add a DMA CPU, an external cpu to manage devices. DMA devices can *directly access memory*.

1. You request IO
2. OS builds DMA program in Memory
3. OS sets aside memory for DMA device
4. OS puts your program to sleep.
5. When the DMA is done doing IO, it generated an interrupt.

DMA is used for any high-speed system. For humans, it could be super simple DMA
or maybe still interrupt based.

# Assembly

Take an assembly file, create an object file.

Use a two-pass assembler.

### Pass One

On pass one, find every label and their addresses.
This more or less builds the symbol table, aka symtab. Also, Perform
"Lexical Analysis" - convert text to a linked list of tokens so pass2 is easier.

Syntax Analysis checks for syntax errors

Semantic Analysis check for errors in the meaning of an instruction.

### Pass Two

On Pass two, build the text block. Every real instruction is converted to
machine code. Use the Directives to build the data block.
