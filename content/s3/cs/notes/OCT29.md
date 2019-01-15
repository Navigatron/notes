[up](../index.md)

# Housekeeping

- Project exists
- Lab 6 not out yet

# More Circuits

- Combinational Circuits
	- Output completely defined by input
- Sequential Circuit
	- A circuit with state
	- Output depends on Input and Saved State
	- I wish I could draw pictures for these notes

# Well Known Circuits

## Decoder

*an n-to-2^n decoder*

Decoders have names, n is replaced with a constant.

- n Inputs (as n-bit binary number)
	- Input 0 (Low Order Bit)
	- Input 1
	- Input 2
	- ...
	- Input n-1
- 2^n Outputs
	- Output 0
	- Output 1
	- ...
	- Output ((2^n)-1)
- Action
	- Send a 1 to the output wire corresponding to the value of the inputs.
	- Send zeros to all others.

In a 2 to 4 decoder, we'd take 2 inputs to 4 outputs.

Send the Decoder a number (n) in binary, and it'll turn on output n.

### Truth Table

S = Select = Input

S1 | S0 | Y0 | Y1 | Y2 | Y3
---|---
0 | 0 | 1 | 0 | 0 | 0
0 | 1 | 0 | 1 | 0 | 0
1 | 0 | 0 | 0 | 1 | 0
1 | 1 | 0 | 0 | 0 | 1

### Implementation

A function is a column - so for the above 2-to-4 decoder, there are 4 functions.

Y0 = !s1 AND !S0  
Y1 = !S1 AND S0  
Y2 = S1 AND !S0  
Y3 = S1 AND S0  

Possible use: take 6 bit opcode to 6-to-64 decoder, each output activates a different circuit to do the thing.

### Draw this

Block Diagram: use Boxes with input lines and output lines so we don't have to draw all the internals.

- Label
	- "2-to-4 Decoder" in the box
	- "S0" and "S1" in the box to the right of their inputs
	- label outputs 0 through 3, drop the "Y"s

Logisim does not label for us. Logisim uses shapes to tell us what something is. We cannot do that - we need to label. Shape doesn't matter.

> A carefully labeled star will not loose points, but it'll make Prof. Grumpy.

### How to turn off the Decoder?

Standard Decoders cannot be turned off. However, there are special things.

Add another input, E. The decoder operates normally when E is 1. When E is 0, the decoder produces no input.

A "2-to-4 decoder with enable" typically has the E input at the top or bottom of the block diagram.

Tack on "AND E" to the end of all "Yn=" functions

### Any function can be implemented with a decoder and an OR gate

Pipe the inputs to the decoder, OR the outputs together to get the function.

In fact, you can use the same decoder to implement multiple different functions at the same time, as long as they use the same inputs.

If a function takes a lot of the decoder outputs, flip the function and invert the result. Same output with less decoder outputs.
