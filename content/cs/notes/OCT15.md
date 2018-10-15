[up](../index.md)

# Housekeeping

- Exam 2 Wednesday
	- GOL 3435
	- a bunch of code
	- read the lecture notes
- Exp 5 is up
- Project coming out late this week or next week!

# Assembling

Pass1 parses the file, pass2 uses the parsed file to build the object file.

## paper handout

Text location counter and data location counter both start at zero.
As we move through the code, we increment the counters to determine where things go.

When we encounter `.data`, we know we're working with the DLC (data location counter)

deftab - table of all external definitions and their addresses. There are also
flags, but we aren't going to learn about those right now.

`.byte 0` writes a zero byte, aka a null-terminator.

REFTAB - table of external references and lines of code that use them.
This is so the linker can fill in some labels later on.

RELTAB - tells everywhere in the code that an absolute address was used.
Linker adds load point offset to each of these.

The Linker:
- uses the deftab to tell others where my defs are
- uses the reftab to fill in other's definitions
- uses the reltab

## The linker is on the test

Linker takes multiple Obj modules and squishes them together. This is quite litteraly
appending t2 to t1 and d3 to d2 to d1 and so on.

- Linker Major Tasks
	- Merge multiple obj modules together.
	- Fix the resulting address changes
		- aka relocate all abs addr in each OM by their load point.
			- aka update all addresses
	- Resolve External References to external definitions
		- uses the reftab

To be executable, all references must be resolved, and
there must be an entry point.

We don't need a main if we're building a library, but we still need an external def
so that something can run.
