[up](../index.md)

# Switch Statements Continued

```C
int i = 5;
switch (i) {
	case 1:
		//Code
		break;
	case 2:
		//Code
		break;
	default:
		//Code
}
```

Cases have addresses. We've got a table of case addresses.

We need to turn the switch argument into an index of the case table.

s1 = table[s0]
s1 = lw(table + s0 * 4)

## It's a hash map now.

The above isn't quite what java and C do. Oh no.

hashmaps are how switches actually work, but they're hard af

## Not a hash map anymore. How to build the table?

Mips standard puts text block at 400k, data block at 10M (Hex)

Directives tell the assembler what to do -or- where to put things -or- what to put.
Basically, put X at Y location in the Object module.

### Dot Directives

Kinda like assembler commands. They're indented one to line up with opcodes.

`.text`: Put stuff after here in the Text block.

`.data`: Put stuff after here in the Data block.

`.align` Takes a single parameter, n. It "Moves you ahead" to the next 2^n aligned
boundary. This isn't a toggle. Use this before putting words / data in the data section.

## 5 minutes to build this table in memory

`.byte, .half, and .word`: These allow us to allocate constants into the data section.

Each directive takes a comma separated list of any number of args, sets aside a chunk of memory
containing the specified constants.

```
.byte 1, 2, 4
```

The above creates a 3 byte section in memory, filled with 1, 2 and 4 contiguously.

Finally: Building the jump table. Addresses of cases are labels.

```
	.data
	.align 2
table:
	.word case0, case1, case2, case3
```
