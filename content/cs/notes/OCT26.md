[up](../index.md)

# Housekeeping

- Project 1 exists
- Lab 6 not yet released

# Circuits

Electricity moving through a wire is slowed down by resistance.

Resistance is based mainly on heat, and wire diameter.

Electricity travels about half the speed of light.

Circuit time is based on wire time and propagation time.

Wire time is just the time through the wires.

Propagation time is the time it takes for output to be stable after inputs are
introduced.

The circuit has a propagation time, as do all components / gates.

In this class, we're going to ignore wire length.

## Levels of a circuit

The maximum number of gates the input has to travel through to make it to the
output.

Note - we ignore inverters.

levels of a circuit is a very very rough estimation of how long a circuit will
take.

We won't do simplification - simplification involves decreasing the levels of a
circuit so that it may run faster.

## Standard Forms

Any function can be converted into one of two standard forms.

### Sum Of Product (SOP) [we'll use this one mostly]

- An expression that uses only product terms and ors them together
- At most two levels
- `F= {\bar A} AND B OR {\bar A} AND B AND C`

### Product of Sum (POS)

- pretty much the same thing as above, but flip the order.
- Expression of sum terms anded together

### minterms and maxterms

A minterm is a product term with every variable in problem is either
complemented or uncomplemented. `A AND B AND C; {\bar A} AND B AND C`

a maxterm is a sum term with all the vars in either complemented or
uncomplemented form. `A OR {\bar B} OR C`

minterms and maxterms are a stepping stone to turn any function into a SOP
function.

## Truth Tables

In the world, truth tables are way too unrestricted. In this class, there are
rules.

- Inputs listed in alphabetical order.
	- As long as the variables are independent.
	- Otherwise, leave em in the order of the most sense.
- List values in base 2 order.

A | B | C | !A AND B AND C | !A AND B AND !C | minterm 1 OR minterm 2 | Minterm that owns this row
---|---
0|0|0|0|0|0
0|0|1|0|0|0
0|1|0|0|1|1
0|1|1|1|0|1
1|0|0|0|0|0
1|0|1|0|0|0
1|1|0|0|0|0
1|1|1|0|0|0

Every row corresponds to a minterm. By ORing minterms, we can create any function output by ORing minterms.

This creates a large upsetting function expression - this is where simplificaiton would come in if we were going to worry about that.

"Carnomap"s are the magic of how simplification happens.

Maxterms, or an OR of inputs, are zero for only one row. similar logic as above applies.

Result: Anything is a two-level circuit.
