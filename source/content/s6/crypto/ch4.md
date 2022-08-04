---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Chapter 4 - AES

# Chapter 4 - AES

It's a block cipher!

- block size of 128 bits (16 bytes)
- Key can be 128, 192, or 256 bits

Consists of many rounds, depending on the key length:

key length | rounds
---|---
128 | 10
192 | 12
256 | 14

Each round goes through some *layers*.

> The first and last rounds don't do *all* the layers.

- **Key Addition Layer**
	- XOR with the key for that round
- **Byte Substitution Layer**
	- This is the S-Boxes
- **Diffusion: two sub-layers**
	- ShiftRows: permutes by bytes
	- MixColumn: matrix op that mixes 4-byte blocks.

There is a *key Schedule*, aka $k_{bigboi} -> k_0, k_1, k_2 ...$

## 4.3 - Galois Fields

A group is a set of elements, and we can do operations between them, and the result is in the group. There must be a neutral (does not modify) and inverse (causes to become the neutral) element.

> *abelian* groups mean a op b = b op a; so like, op probably isn't divide.

A field is a wombo combo of an *additive group* and a *multiplicative group*.

The *order* or *cardinality* of a field is the number of things in it.

There are plenty of infinite fields, but finite ones are harder to find. There's a theorem that says finite fields have to have an order of $p^n$, where p is a prime.

### 4.3.2 - Prime Fields

Galois field $GF(p)$ has $p$ elements: $\{0,1,...,p-1\}$, and has two operations:

- Addition *mod p*
- Multiplication *mod p*

### 4.3.3 - Extension Fields

The finite field in AES is $GF(256) = GF(2^8)$. Since $2^8$ isn't prime, but is a power of a prime, it's called an *extension field*. We need new notation and new rules for operations.

Each element can be represented by a polynomial:

$$
GF(p^m)\_A = \sigma_{i=0}^m-1 a_i x^i
$$

For $GF(2^8)$ where $m=8$:

$$
A(x) = a_7x^7 + a_6x^6 + ... + a_1x^1 + a_0x^0, a_i \in \{0,1\}
$$

There are exactly $2^8=256$ possible polynomials. Each can be stored by just the coefficients:

$$
A = (a_7,a_6,a_5,a_4,a_3,a_2,a_1,a_0)
$$

Cool! so elements in $GF(p^m)$ are represented by polynomials.

### 4.3.4 - Addition and Subtraction in Extension Fields

This is easy, just add the coefficients and mod 2.

$$
c_i = a_i + b_i mod 2
$$

Subtraction actually does exactly the same thing.

### 4.3.5 - Multiplication in Extension Fields

> help

$$
A(x)\cdot B(x) = (a_{m-1}x^{m-1}+...+a_0)\cdot (b_{m-1}x^{m-1}+...+b_0)
$$

Just distribute to send it, you can multiply like that, it's not bad.

Dividing is a bitch and a half, actually wait it's not bad.

There's a lookup table on page 99 of the book for finding inverses. It's nice.

*Manually* finding inverses is **work**. You gotta use the EEA.

## 4.4 - Internals of AES

AES operates on 16 bytes at a time. You could lay these out as a 4x4 matrix.

The key is also a 4x4 matrix - or a 4x6, or 4x8 (getting wider) as the key changes.

### 4.4.1 - Byte-Sub Layer - S Boxes

Every byte is replaced by a new one.

**Inversion**

Byte A becomes B-Prime by finding its inverse under $GF(2^8)$. This is the intermediary result.

**Affine Mapping**

Byte B-Prime is multiplied by a matrix, added to another matrix, and modded by 2. This "destroys" the algebraic properties from the GF.

> To multiply matrices, it's row * column, so row1 * col1 = out1,
> first * first + second * second + third * third...

### 4.4.2 - Diffusion Layer

There's two sublayers:

- ShiftRows
- MixColumns

**Shift Rows**

It moves row 2 by 3, row 3 by 2, and row 4 by 1 - to the right.

```
0  4  8  12
1  5  9  13
2  6  10 14
3  7  11 15
```

```
0  4  8  12
5  9  13 1
10 14 2  6
15 3  7  11
```

**Mix Columns**

Every column is considered a vector, and is multiplied by a matrix. All the multiplication and addition takes place in GF(2^8).

All the constants are given in hex.

Constants:

```
02 03 01 01 - b0
01 02 03 01 - b5
01 01 02 03 - b10
03 01 01 02 - b15
```

### 4.4.3 - Key Addition Layer

Ya just XOR the key in.
