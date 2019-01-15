[up](../index.md)

# housekeeping

Experiment 1 is up. It's written to be very simple, no worries.

The goal is to learn the debugger.

# Print debugging is rough

it takes 3 lines of code, and 2 registers (which change), to print something.

Printing a newline takes another 3 lines of code.

*Use the Debugger.*

# displacement mode

The Effective Address is equal to a register value plus a constant.

This was designed to allow access to a struct.

```
lw rt,imm(rs) # rt = mem(rs+imm)
```

*Add imm and the value of rs. Get the memory from there. Store it in rt.*

```
sw rt,imm(rs) # mem(rs+imm) = rt
```

The above is the only command where the destination is second.

# Sign extension

When we load a half-word or a byte into a 32bit register, we don't change the magnitude or sign.

AKA positives are padded with zeroes and negatives are padded with... ones?

To keep unsigned things from turning negative, we use `lhu` and `lbu`, which only zero extend.

There are no unsigned variants of store, because there is no need.

# Swap function for Bubble-Sort

## in C

```C
// Swap a[k] with a[k+1]
void swap(int a[], int k){
    int t = a[k];
    a[k] = a[k+1];
    a[k+1] = t
}
```

## in MIPS

```
swap:
        # a0 = address of a
        # a1 = value of k
        # Elements of a are integers, 4 bytes.
        # Find address of a[k]
        MUL     $t0,$a1,4       # k*4 to get offset
        ADD     $t1,$a0,$t0     # offset + base = address
        LW      $t2,0($t1)      # t2 = a[k]
        LW      $t3,4($t1)      # t3 = a[k+1]
        SW      $t3,0($t1)      # a[k+1] = a[k]
        SW      $t2,4($t1)      # ?
```
