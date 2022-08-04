[up](../index.md)

# Alignment

Memory is like an array of bytes - its very hard to control which bytes we're reading.

Solution: Don't get individual byte control. Memory is stored in 4byte groups.

To read 4 bytes, if the bytes are stored at a +0, that's one read.

If the stuff is at a+2, then it takes two reads.

Compilers put data at good locations.

# Data Alignment Defenition

a piece of data is aligned if addr%len==0

If data is aligned, it can be accessed in the minimum number of memory calls.

If we try and read/write to an un-aligned address, rsim will give us an error.

# Three Load Instructions

`lw` - Load Word
`lh` - Load Half Word
`lb` - Load Byte

Words are typically the width of the bus.

Ints are at least as big as a short, which is at least as big as a byte, which is 8 bits.

C wanted everyone to use ints. Ints are typically as long as a word. This causes problems.

If you turn on backwards compatibility on all x86 C compilers, you get 16bit ints.

Microsoft has int_128, int_64, etc.

# Three store instructions
`sw, sh, and sb`.

Each command takes two things: a register and a memory locaiton. Memory locations do not fit in registers.

# Address Modes

Mathematical formulas that compute a location in memory, aka an effective address, or EA.

High languages have syntax to get parts of an array - assembly has address modes.

High Level Language | Address Mode | Math Formula
---|---
Global Variable | Absolute AM | EA = constant
Pointer | Indirect AM | EA = value of a register.
Array index | Scaled | EA = reg + reg * constant
Structure | Displacement | EA = reg + constant

We cant use Absolute AM in MIPS because we cant put a 32bit thing in the instructions.

Scaled mode can simulate Displacement mode, but it cant work the other way.
