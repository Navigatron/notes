[up](../index.md)

# Housekeeping

Experiment 4 due Friday
Experiment 5 - The Big One - Coming out this Friday probably

- Exam 2
	- Next Wednesday, week 8
	- October 17th
	- GOL-3435
	- Review
		- October 15th
		- 11 to noon
		- Gol 2590

# System calls and MIPS IO

System calls are how we request a service from the OS. The OS provides secure,
complex, and/or efficient services.

`syscall` is a real instruction.

### Registers
- v0 - which service to request
- a0 and a1 - to pass arguments.
- v0 contains return value if there is one.

### What can we do?


syscall | v0 | arg | return
---|---
print int | 1 | a0 is val to print |
print string | 4 | a0 is the string (char*) |
read int | 5 |  | v0 is val read as decimal
read string | 8 | a0 is addr of string buffer to overwrite, a1 is number of chars to read |
exit | 10 | |

We are encouraged to not use exit. In Java, `System.exit(0);` immediately kills all threads.

# Equal Directives

Just like dot directives, these give instructions to the assembler about stuff.

They work kinda like `#define` in C.

```
symbol = constant value
```

These are typically used to declare the magic numbers for syscalls.

```
PRT_INT = 1
PRT_STR = 4
```

> And that is the last Assembly thing we will teach you.

# IO

## In the beginning

### Polled IO

ready flag and single byte buffer. When a key is pressed, ready flag is set and buffer populated. Program clears flag and consumes the buffer.

```C
do{
	while(!ready){
		// Do Nothing
		// We spend a lot of time in here.
		// As long as there's nothing better to do,
		// this doesn't actually waste any time.
	}
	// Get Buffer
	// Clear Ready Flag
}while(/*I want more data*/);
```

### Interrupt Driven IO

When the process wants IO, it's swapped out until the input is ready. This lets other things run while the user decides what key to press.

More on this on Friday.
