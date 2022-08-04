[up](../index.md)

# Housekeeping

- Exp 3 due Wednesday 11:59PM
- Despite the career fair, there will be class on Wednesday.
	- It won't be too rough to skip though.

# Dot directives (Cont.)

`.ascii`

`.asciiz`

Both take a quoted string. They initialize one byte per char and initialize each
byte to their char. The `.asciiz` adds another byte at the end and adds a `\0`.

The C escape sequences are supported.

code | meaning
---|---
\t|tab
\n|newline
\\|\
\"|"
\0|null

## .space

Takes a single number, n, and sets aside n bytes of *uninitialized* memory. This lets you allocate large chunks of memory easily.

## .globl

Yes, it's spelled that way on purpose. It takes one thing, a label.

This involves assembling multiple files.

There are two things:

`.globl extref` - a label you use but don't define. "Here's a function label, it goes somewhere else."

`.globl extdef` - Labels you define for others to use.

# Structures

*A collection of heterogeneous data*

In C:

```C
struct foo{
	int x;
	int y;
	int z;
}bar;
```

Bar is an address, at which there are 3 contiguous ints.

In MIPS:

```
	.data
	.align 2
bar:
	.word	1		# X
	.word	2		# Y
	.word	3		# Z
bar2:
	.word	1, 2, 3		# X, Y, Z
```

acessing bar.2:

```
	LA	$t0, bar
	LW	$t1, 0($t0)	# t1 has bar[0]
	LW	$t2, 4($t0)	# t2 has bar[1]
	LW	$t3, 8($t0)	# t3 has bar[2]
```

Oh no, Y is now one byte. The struct could be 9, 12, or 24 bytes in size. In assembly, because things cannot be misaligned, we pad Y to be 2 bytes long?

```
bar:
	.word 	1	# X
	.ascii	"a"	# Y
	.align	2	# pad for alignment
	.word	3	# Z
```

Okay, okay... but now how do we read Z if we don't know the size of Y?
