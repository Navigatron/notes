[up](../index.md)

# Housekeeping

- Experiment 7 due Monday, 11:59PM
- Project
	- Early submission Tuesday, 11:59PM
	- On-Time: Monday the 26th, arrival back from break.
	- Late: Tuesday the 27th, 11:59PM
	- The program must pass build and link, in order for try to save it.
	- It's possible to get a 40% with only input and output. *Make sure try saves what you submit - Pass build and link using any method needed. Comment out everything. Jump to end. Whatever it takes - Give Phil something to grade.*
	- New submissions delete old submissions.

# Register File Circuit

Inside, there are 32 32-bit registers. Each register has two inputs, LOAD, and IN - in is a 32-bit number. Each register has one output, OUT, which is a 32-bit number.

Send load to a register and it'll remember whatever is on IN. A register always outputs what it's remembering.

Copy/Paste of the register file block diagram from my last notes:

```
MIPS 32x32bit register file
   +--------------+
 5-|RA1           |
 5-|RA2         R1|-32
  -|Write         |
 5-|WA          R2|-32
32-|Wdata         |
   |              |
   +--------------+
```

- RA1 - which register goes to R1
- RA2 - which register goes to R2
- Write - single bit flag, 1=write, 0=do nothing.
- WA - which register to write to, if we're writing
- Wdata - The value to be written to a register, if we're writing.
- R1 - output from a register, RA1 decides which one
- R2 - output from another register, RA2 decides which one.

Here's how we get these inputs and outputs to and from the actual registers inside the register file.

`Wdata`, the data to write, goes everywhere - because the registers won't do anything with it. We can send the `Write` flag to only the register we want to write to.

`WA`, aka Write Address, decides what register we want to send the `Write` flag to. A Decoder takes a number and outputs one flag. `WA` goes into a 5-to-32 decoder, which has an output for every register, tied to the register's `LOAD`.

So far, `Wdata` goes everywhere. `WA` goes through a decoder to trigger the correct register to read the `Wdata`. However, sometimes we do not want to write to a register. If the `Write` flag is off, we do not want to write - the `Write` input to the register file goes to the Enable input of the decoder.

Now reading.

It's time for a big-ass, very special multiplexer. For now, we'll pretend each register only outputs 1 bit.

Use `RA1` as the 5-bit select on the MUX. Each register is a data input to the MUX. The output of the MUX goes to register file output R1.

What if each register output 2 bits? All we need is another 32bit MUX.

And then another. Anotha one. Anotha one. Anotha one. Until there are 32 multiplexers, each one picking 1 bit from each register, and sending it to output 1.

Output2 is another 32 multiplexers.

In logisim, it's so much easier - multiplexers can take multi-bit wires.

# CPU

A cpu is made of a control unit, and a data path.

The Control unit decides:
1. What to do
2. When to do it
3. What data to use

Questions 1 and 3 are answered by the instruction. Question 2 is harder - Things need to happen in order.

The Data Path:
1. Moves data around (Busses!)
2. Manipulates Data (ALU and some dark magic)
3. Stores the data (Registers)

The data path sends some things to the control unit - instructions read from memory, and results from branches.
