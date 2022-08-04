---
mathjax: true
---
[up](../index.html)

### ISA

*Instruction Set .... something*

The spectrum of ISAs:  
- CISC
    - Complex Instruction Set Computer
    - Some instructions do a lot of work
    - not all of them have to be complicated
- RISC
    - Reduced Instruction Set Computer
    - All instructions do little work
    - Reduced = Reduction in Complexity, simpler.

MIPS is almost as RISC as it gets.

VAX is an ISA that is almost as CISC as it gets. VAX has string copy, other string ops,
and an instruction to calc the roots of a polynomial. Why?  
- Pre-written
- Tested
- Optimized

Other ISAs:  
- ARM
    - A little more complex than MIPS
- x86
    - A little simpler than VAX
    - String copy is awesome, check it out.

### Important Formula Time
*It is very difficult to measure execution time.* Magic Formula here mathematically estimates the execution time of a program.

Variable | Meaning
--- | ---
E | Total Execution Time
I | Instruction Count
C | Cycles Per Instruction
T | Clock Cycle Time

$$E=I*C*T$$

RISC will have:
- Much Higher Instruction Count
- Much fewer cycles per instruction

Example: VAX 32k string copy instruction. VAX Hardware can check if the char is null and write the char at the same time. This is very cool.

In a vacuum, in a nanosecond, travels 11.5 inches. Electricity travels about half that, slower if the wire is hot. This puts a cap on Clock Cycle Time.

Clock Speed is primarily affected by Chip Size.

### Pipelining

CISC is really hard to pipeline, but Intel cares about backwards compatibility. x86 is entirely backwards compatible.

New Intel Chips, in hardware, take x86 and translate to a different ISA. This works and it is great.

X-assemble is part of the pipeline. It's wicked fast.
