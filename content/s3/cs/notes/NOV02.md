[up](../index.md)

# Housekeeping

- Project 1 exists
- Homework 6 is up, due next wednesday probably

# PLAs

A PLA has a lot of inputs into an AND array. Outputs from the AND array are fed into an OR array.

Every gate in every array is attached to every input via fuses. To program a PLA, we apply high voltage to burn out specific fuses.

PLAs are very small, very cheap to produce, and fit together really well. PLAs are tasty.

## ICs

An Integrated Circuit is like a PLA - but all the wires that wouldn't be used are never put in in the first place.
It looks like a PLA without any un-used circuits. ICs are cheaper and more efficient is massive numbers.

So, In general:
- PLAs for small batches of products
- ICs for huge batches

## Hard Left Turn -> ROM (Read Only memory)

You can't write to that.

ROM takes an address, and gives some data. That data doesn't change - Aha! It's a Truth Table!

It's a Truth table? It's a 2-level circuit! It's a PLA!

oh no.

# Sequential Circuits

A combinational circuit and memory

One of the inputs is from memory, and one of the outputs is to the same memory.

Output is based on input + saved state.

## Our first sequential circuit

Inverter 1 goes to:
- Output (lightbulb)
- And the input of Inverter 1.

### Asynch sequential circuit

An async seq circuit is continuously sampling it's input

This is rough, and really isn't good for all that much.

### Synchronous Sequential Ciruits

A control system tells sequential components when to smaple their inputs

All modern computers use synchronous sequential systems.

### The Clock Wave

The CPU Clock generates a Square^tm Wave

### Triggering

What identifiable part of the square wave will we use to say "Sample Input Now!"

- Rising / leading edge
- Falling / Trailing edge
- level

Rule - You are not allowed to change input while it is being sampled
- This creates "Hold Time" - the time you are not allowed to change the input.
- Other time is "Setup Time" - During the setup time, we can change inputs.

Propagation delay takes place during the setup time, while circuits are running.

Circuits are really easy to build if we use level triggering - but then the clock cycle time is double the longest propagation delay.

Edge triggering takes more gates, but allows very very small hold time, almost doubling the clock speed.
