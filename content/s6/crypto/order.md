---
mathjax: true
---

[up](./index.md)

# order and primitive root

the order of a mod n is the smallest power of a that makes it 1 (mod n). Typically denoted as K.

AKA:

$$
a^k \bmod n \equiv 1
$$

It's pretty much just a guess and check operation, but have no fear! K will be less than or equal to n. If no K is found, then we say the order of a is infinity.

if order(a,n)=phi(n), then a is a primitive root of n.
