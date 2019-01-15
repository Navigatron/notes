[up](../index.html)

# August 29th - Abstract

### CPU
- Internal Parts
    - Control Unit
        - Instructions from Program (x=a+b)
            - what to do (+) [opcode]
            - when to do it (Get ab, add, store)
            - what data to work with [operands] (a and b -> x)
    - Data Path
        - User data lives here
            - Stuff currently in use
        - Store User Data
            - Registers
                - Physically inside the cpu
        - Move User Data
            - on wires
        - Manipulate Data
            - Gates, transistors.
- External Components
    - memory
        - 3 layers of cache on the cpu
        - maybe ssd buffer
        - Ram
        - Swap on disk
        - For our purposes, it doesn't matter.
            - Program works with virtual memory - 2^64
            - hardware knows where things actually are
    - input devices
        - Keyboard
        - anything is fine
    - output devices
        - Screen
        - Whatever, it's all the same to the computer.

1. Put the instruction in the control unit
2. control unit decides what to do
3. data path carries out the action

add A and B, store to X

Hardware detects things, tells the OS via interrupt / exception.
(Such as integer overflow, or division by zero.)

ISA - the language - binary run by hardware

### Layers:
1. Hardware
    - Understands an ISA
2. Machine Code / Machine Language
    - Instruction Set Architecture
        - Rules that define the language of commands
        - Opcodes
        - Sysntax
        - Operands
        - Encoding
            - Converting ADD to binary
3. Assembly

### MIPS
- Instructions based on fields
- first field opcode
- last sometimes opcode

Addition:
```
| 6 bits | 5 bits  | 5 bits  | 5 bits      | 5 bits | 6 bits |  
|--------|---------|---------|-------------|--------|--------|  
| 000000 | source1 | source2 | destination | ?????? | 100000 |
```

Multiply in assembly becomes two instructions in machine code
