---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Chinese Remainder Theorem

# Chinese Remainder Theorem

There is some number, like 8, that we want to mod by some other number, like 35.

In this case, 35 happens to be $5*7$, so we're going to use CRT to split the 8 mod 35 problem into two smaller mod problems.

8 mod 5 is 3, and 8 mod 7 is 1, so 8 in the "standard domain" (mod 35) is the ordered pair (3,1) in the "CRT Domain" (mod 5 and 7).

Math works in both domains - 8 + 6 = 14, and the CRT versions of 8 and 6, when added, are the CRT version of 14. cool.

Converting back to normal space requires "Basis Vectors":

$$
(1,0) = q * (q^{-1} \bmod p)
(0,1) = p * (p^{-1} \bmod q)
$$

Now, any pair can be computed:

$$
(a,b) = a \cdot (1,0) + b \cdot (0,1) mod n
$$

Example converting (2,1):

$$
(1,0) = 7 * (7^{-1} \bmod 5) = 7 * 3 = 21
(0,1) = 5 * (5^{-1} \bmod 7) = 5 * 3 = 15
(2,1) = a \cdot (1,0) + b \cdot (0,1) mod n
(2,1) = 2 \cdot 21 + 1 \cdot 15 mod 35
(2,1) = 42 + 15 mod 35
(2,1) = 57 mod 35
(2,1) = 22
$$
