[up](../index.md)

# The Standard Stack Frame

Stack starts at top of memory, and expands downwards.

## Caller

Caller places arguments 4..n on the stack (0,1,2,3 in a0, a1, a2, a3). Then the caller moves the stack pointer to the bottom of the stack.

TL;DR: Caller sets up args for callee via `A` registers and the stack.

After the callee returns, the caller removes the arguments from the stack. If the caller doesn't care about the args (most likely), just move the stack pointer.

## Callee

Callee stores `$ra`, saved registers, local vars in that order. `$sp` is adjusted.

Move the stack pointer first, then fill in via offsets.

When we're done with out things, we need to deconstruct our stack frame. Restore anything we care about (`S` regs, `$ra`, etc) and then move the stack pointer back up.

## The issue with arguments

The caller reserves space in the stack for the callee to save a0 through a3 if desired.

## Chew on This:

```
FunctionA:
	# Move SP down for all my stack frame (arguments already there)
	# Push RA
	# Push s0 to s7 for caller
	# Push FP for caller
	# Set FP to top of my stack frame.


	# We want to call functionB

	# If I want my a0 to a3 preserved, push em to space set aside by my caller
	# Adjust SP to make space for args
	# load a0 to a3 for the callee
	# Push args 4 through n, leaving space for 0->3
	jal	callee
	# Pop off args 4 through n, adjust sp
	# If needed, restore my own a0 through a3


	# We want to return from this function

	# Restore FP, s0->s7
	# restore RA
	# Move the stack pointer up, removing (most of) my stack frame
	jr	$ra

```

and now...

# System Calls

Hardware has at least two levels of privilege. The operating system and user-space are physically separated. This stops programs from killing each other, changing their own priority, messing with the OS, reading other users files, regulating fan speed, important stuff.

The MIPS instruction to do a system call:

```
	syscall
```
