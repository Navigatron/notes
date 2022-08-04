---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Galois Fields

# Galois Fields

> A field is a set of integers, such that operations on the integers result in other elements of the set.
>
> Aka, A field is like a group but it has both the addition and multiplication operations.

Galois showed that for a field to be finite, the number of elements should be some power of a *prime*, aka $p^n$.

A Galois Field $GF(p^n)$ is a finite field with $p^n$ elements.

When $n=1$:

$$
GF(p^n) = GF(p) = Z_p = \{0,1,...,p-1\}
$$

There is a common field, $GF(2) = \{0,1\}$. It has two operations, + and *.

Multiplication:

X | 0 | 1
---|---|---
0 | 0 | 0
1 | 0 | 1

Addition:

\+ | 0 | 1
---|---|---
0 | 0 | 1
1 | 1 | 0

Inverses:

a | -a | $a^{-1}$
---|---|---
0 | 1 | -
1 | 0 | 1

# Prime fields

When $GF(p^m)$
