[up](../index.md)

# Housekeeping

- Exam 1
    - Wednesday 26th
    - GOL 3435
    - Review Session
        - 24th
        - GOL 2590
- Experiment 2
    - Do the things
        - Returns
        - etc.

# Branch Instructions

Branch if Equal (`beq`) and Branch if Not Equal (`bne`)

```
beq rs,rt,dest (as label)
```

if rs is exactly equal to rt, goto dest.

```
bne rs,rt,dest (as label)
```

if rs is not equal to rt, goto dest.

## Instruction Format

I type instruction, and can't use absolute address mode. Create PC Relative Address Mode - dest can be anywhere within 32k of the branch. dest is computed to be the offset from the program counter.

## Inequalities

*Set if Less Than*

```
slt rd, rs, rt
```

If rs is less than rt, rd will be set to exactly 1. Otherwise, it will be zero.

```
slti rt,rs,imm
```

The above detects if rs is less than the specified immediate.

## You don't need greater than.

Just flip the less than. `sgt` is a pseudo instruction that we can use on the project, but not until then.

## You don't need leq or geq either

geq = !(less)

leq = !(greater)

> "For the project, ya'll can use any pseudo instruction you want." - Prof

## Aight loops real quick

```
loop:
    if !conditional goto done
    # body
    j loop
done:
```
