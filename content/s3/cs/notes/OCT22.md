[up](../index.md)

# Housekeeping

- Exp 5 due Wednesday
- Proj 1 due eventually

# Number System

We're used to sign magnitude. We have a sign, and then a magnitude. If missing,
sign is assumed to be positive.

> "16" represents the concept of the quantity 16.  
> "Negative Numbers Don't Exist."

Agree from here-forth that the preceding negative sign multiplies the magnitude
by -1. It's important to separate representation from concept, as we'll be working
through many representations.

`713 = 7*100+1*10+3*10 = 7*10^2 + 7*10^1 + 7*10^0`

## Algorithm - Base 10 to Base 2.

136 to base 10
```
136 % 10 = 6
    / 10
 13 % 10 = 3
    / 10
  1 % 10 = 1
    / 10
  0 % 10 = 0 -> Read number upwards

136(base 10), in base 10, is 136.

```
136 to base 2
```

136 % 2 = 0
    / 2
 68 % 2 = 0
    / 2
 34 % 2 = 0
    / 2
 17 % 2 = 1
    / 2
  8 % 2 = 0
    / 2
  4 % 2 = 0
    / 2
  2 % 2 = 0
  	/ 2
  1 % 2 = 1

  136 in base 2 is 10001000

```

## Negatives - What do they do? Do they do things? Let's find out

Due to the magic if fixed-length number systems, we can do this:

```
+------+-----------+
| sign | Magnitude |
+------+-----------+
```

However, this makes negative zero possible.

This also makes math hard. Adding with different signs is complicated.

Therefore, sign-magnitude is problematic and slow in computers.

## It doesn't have to be this way

*The joy of 2's Complement*

To convert + to - OR - to +:
1. Flip the Bits
2. Add 1

3 bits represents 0 to 7, or 8 numbers total.

Make this signed with 2's complement:

```
  0 1 2 3   4 5 6 7
+---------+---------+
| 0 0 0 0 | 1 1 1 1 |
| 0 0 1 1 | 0 0 1 1 |
| 0 1 0 1 | 0 1 0 1 |
+---------+---------+
  0 1 2 3  -4-3-2-1
```

-3 plus 2 is now -1 very easily

> Computers only deal with translation when working with squishies

## Now sign extension makes sense

Converting 4 bit numbers to 8 bits:
```
 5 =     0101
 5 = 00000101
-5 =     1011
-5 = 11111011
```

# Hexadeximexical

Dealing with Binary is hard for "Squishies". So we use Hex.

Converting binary to hex is easy - we'll get to that next time.
