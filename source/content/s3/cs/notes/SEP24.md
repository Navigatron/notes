[up](../index.md)

# Housekeeping

- Exam 1
    - Next Class
    - GOL 3435

# Do-While loop

### Java:

```java
do{
    // Code
}while(condition);
```

### MIPS pseudo Code:

```
loop:
    # body
    # update
    if(condition) goto loop
```
or
```
    addi    $s0, $zero, 0
loop:
    # body
    addi    $s0, $s0, 1
    slti    $t0, $s0, 10
    bne     $t0, $zero, loop
```

Do while loops are real tasty. But if it can't be persuaded into a do-while, don't force it.

# Compound Conditionals

Just take more code

# Switch Statements

```java
switch(s0){
    case 0:
        // code
        break;
    case 1:
        // code
        break;
    default:
        // code
}
```

Just a bunch of if-else stuff - kinda. Switch has more requirements than if, but runs faster.

> Linked list as a constant, idk, put quotes around it!

Cases are right next to each other in mem. When one is done, you fall through into the next one.

> Elves like helping people, we all should know that

We've got an elf.

We give the elf s0 and it returns the address of the correct case.

> The elf doesn't do error checking, it's sailing away to an island in the west.

> Hint: Writing a switch statement on the Exam.

```
# Goal: Switch $s0
# Hello I am Elf
# Given s0, elf returns case address in s1
    # if s0 < 0, goto default
    slti    $t0, $s0, 0
    bne     $t0, $zero, default
    # if so > 2, goto default
    li      $t1, 2
    slt     $t0, $t1, $s0
    bne     $t0, $zero, default
```

> Arrays are almost as good as elven magic, they just don't bake cookies.

Tune in next time for the elv magic - It's gonna look a lot like array accessing.
