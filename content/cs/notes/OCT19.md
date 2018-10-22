[up](../index.md)

# Housekeeping

- Exp 5 due next wednesday
- Project is posted
	- submit by 11/20 for 10% bonus - this is worth more than 2 labs
	- 12:01 on monday is 20% off

# Linker

Major Tasks:
1. Combine all our little modules into a **SUPER MODULE!**
	- Code Relocation
2. Resolve extRefs to extDefs

How?

1. Init Load points TLP=400K DLP=10M
2. Loop through all Object Modules
	- Append Text to Global Text
	- Append Data to Global Data
	- Loop through all entries in reltab, reftab, deftab, symtab
		- Add correct load point, put in global table
	- Loop global ref tab
		- Update code addresses
	- Update load points with size of this OM's text and Data
3. Loop through Global Ref Tab
	- Each line here is a line of code where we used an extRef.
	- Look up label in global deftab, replace in code.
	- Remove unneeded reftab entries.
	- If deftab doesn't tell us where the label is,
		- It's still an external reference. Let it sit.
4. If deftab has at least 1 entry, mark built file as executable.
	- If there's anything left in the reftab, Fail.

	
