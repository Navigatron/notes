[up](../index.md)

# Quick Reference - Registers

## Standard Registers.

Number | Alias | Purpose
---|---|---
0|zero|always zero
1|at|reserved for assembler
2 | v0 | Function Return Values
3 | v1 |
4 | a0 | (A)rguments - data passed to functions or Procedures.
5 | a1 |
6 | a2 |
7 | a3 |
8 | t0 | (T)emporary - not preserved by functions. Set, Use, Forget.
9 | t1 |
10 | t2 |
11 | t3 |
12 | t4 |
13 | t5 |
14 | t6 |
15 | t7 |
16 | s0 | (S)ystem or (S)torage. Preserved across function calls, longer term than temp.
17 | s1 |
18 | s2 |
19 | s3 |
20 | s4 |
21 | s5 |
22 | s6 |
23 | s7 |
24 | t8 | More temporary storage
25 | t9 |
26 | k0 | Reserved for Operating System. See Below.
27 | k1 |
28 | gp | Global Area Pointer
29 | sp | Stack Pointer
30 | fp | Frame Pointer
31 | ra | Return Address Register

### zero

This one is a physical wire to ground. It always reads as zero, no matter how much data you dump into it.

### at

Reserved for the Assembler.

//TODO - show la and la expansion.

### v0 and v1

Values returned from functions.

### a0 through a3

Arguments passed to functions

### t0 through t9

Temporary storage. Use 'em, abuse 'em, but don't expect the values to stick around if you call a function.

### s0 through s7

Long term storage. If you're going to alter one of these in a function, remember to save the original value and restore it before you return.

### k0 and k1

The OS uses these registers whenever there is an interrupt. Interrupts can happen at any time. You could write to k0 and read from it in the very next instruction, and it wouldn't be what you set. Don't touch these.

### Global Area Pointer

Prof says to ignore this one, we won't be using it.

### Stack Pointer

Used to keep track of the stack. Change this when pushing or popping from the stack.

### Frame Pointer

"Used by Standard Stack Frame"

I'm not sure what this does, gotta fill this in.

```java
//TODO
```

### Return Address

Functions return to this address when they're done executing. Set it before you call a function, and use the stack when going more than 1 function deep.

## Special registers

### HI and LO

### PC
