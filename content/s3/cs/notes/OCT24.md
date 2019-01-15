[up](../index.md)

# Housekeeping

- Exp 5 due tonight
- Exp 6 comes out sometime next week
- Proj 1 on the to-do list.

# Hardware!

## Converting bases

When converting between bases that are powers of each other, it's easy.

Converting base 2 to things - base 8 (octal) was popular, but it split
stuff into 3 bit chunks. This is why base 16 (Hexadecimal) became prevalent.

## BOOOL

Data is boolean data on a wire. Gates perform boolean operations on the data.

And so, we must...

### Review of Boolean Operations

> "Is that a beer?"

*It was a non-alcoholic ginger beer.*

Operation | Definition | Notation
---|---
AND | True only when all are true | [A \cdot B] or [AB]
OR | False only when all are false | [A+B]
NOT | True only if false | [\bar A] or [!(A)]
XOR | True if odd number of inputs are true | [A {plus in circle?} B] or probably [A XOR B]

### Boolean Expressions...

Boolean operators working on boolean data to create a boolean result.

These can (and often are) built in hardware. Diagrams of this stuff are called
"logic Diagram" or "circuit Diagram".

In this class, all circuits must operate from left to right.

Logisim ignores unconnected wires.

> "I teach for the love, and 1.6 million is a lot of love"

Operator | Symbol
---|---
And | Capital D ish thing. Any number of inputs, one output.
Or | Curved D with a point. Like `)>` kinda?
Not | Triangle with a circle on the point. `-->o--`
Xor | OR with a second left side. `))>`

> "How many things will we be drawing?"  
> Hundreds. First question on the test: Draw 300 OR gates.

### Order of Operations

1. NOT
2. ()
3. AND
4. OR, XOR

## Wires

- Connect wires in diagrams with a large dot. Cross wires with no dot.
- ALL wires must move vertically or horizontally
	- This makes wires cross at right angles
- Inputs and Inverted inputs across the top going down looks nice - not required
