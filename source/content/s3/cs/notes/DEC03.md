[up](../index.md)

# Housekeeping

none I guess

# Dec03

handout for mips single-cycle control unit handed out

ALU-op discussed, woohoo truth tables

## multi-cycle

RTL had to be modified, to make things fit.

There are 11 different "things" to do, each of which is just a state of the 16 control points.

The job of the control unit is to walk through the states in a logical order.

State diagram built - where each state can go, based on what.

> If the control point has nothing to do with whatever's going on, you can assume the value is zero. Items that have to be zero must be specified.

## Do state 1

a <- reg[rs]
B <- reg[rt]
Imm <- S.E.(imm)

ALoad = 1;
BLoad = 1;

## Do state 8
zero <- A==B

ALUsrc1 = 1
ALUsrc2 = 0
ALUop = Subtraction

if(zero) PC <- ALUout

PCload = zero
PCSource = zero

> overspecify

ALUoutLoad = 0

It's possible to do this for every state - we'll get the handout next class.

Now, we have the set of outputs for each state. Now, how to decide what state we're in? What hardware?

All we need is an output wire for each state

We need hardware to determine the state, that is all

Stage of execution = row, instruction = column; of state diagram as table.

*Time to Draw*
