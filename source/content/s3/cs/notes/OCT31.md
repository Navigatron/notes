[up](../index)

# Concepts - Haloween edition - spookiest class yet

*THE MULTIPLEXER.*


- n Select Inputs - as an N-bit binary number
- 2^n Data Inputs - numbered from 0 to 2^n-1
- 1 Output

Call this a "2^n by 1 mux".

Takes input n and sends it to the output.

We'll use a modified truth table, because a 4x1 mux has a lot of rows that don't do anything.

E | S1 | S0 | Y
--|----|----|---
1 | 0  | 0  | d0
1 | 0  | 1  | d1
1 | 1  | 0  | d2
1 | 1  | 1  | d3
0 | X  | X  | 0

## Block Diagram

```
  +---------+
  | 4x1 mux |
 -+s0       |
 -+s1       |
  |        Y+-
 -+0        |
 -+1        |
 -+2        |
 -+3   E    |
  +----+----+
       |
```

## Implementation

Each combination of S0 and S1 go to an AND. Each AND also attaches to one of the data. The output of all ands goes to an OR, which acts as a collector. We can't just wire all the outputs together because zero is not voltage zero.

## Using a mux to implement a function

A|B|C|F
---|---
0|0|0|1
0|0|1|1
0|1|0|0
0|1|1|0
1|0|0|1
1|0|1|0
1|1|0|0
1|1|1|1

8x1 Mux - Select S2 through S0, and Data 0 through 7.

A -> S2  
B -> S1  
C -> S0  

Then attach 1 or 0 to the data such that it works. This feels like bad programming, but it works I guess.

Aha, it is terrible - because Muxs use a lot of hardware. Almost every other method is more efficient.

# Other standard things

## Turning Corners is Hard

## PLA - Programmable Logic Array

Inputs to an AND array to an OR array - outputs many functions

Every AND is connected to every input by fuses - to program the PLA, you burn out the fuses you don't want.
