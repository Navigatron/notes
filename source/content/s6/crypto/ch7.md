---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Chapter 7 - RSA

# Chapter 7 - RSA

RSA relies on multiplying two large primes. It's easy to do, but very hard to reverse.

## 7.2 - Encryption / Decryption

Done in ring $\Bbb Z_n$ - so $x$ (as a bitstring) has to be smaller than n.

Given:

- Plaintext $x$
- Public key $k_{pub}=(n,e)$

Encryption is:

$$
y = e_{k_{pub}}(x) \equiv x^e \bmod n
$$

Where $x, y \in \Bbb Z_n$

Given:

- Ciphertext $y$
- Private key $k_{pr} = d$

Decryption is:

$$
x = d_{k_{pr}}(y) \equiv y^d \bmod n
$$

> How does the decrypter get n? Ah, that's part of their public key?

Where $x, y \in \Bbb Z_n$

So, plain to the $e$ is cipher, which then to the $d$ is plain again. In the ring ofc.

## 7.3 - Key Generation

1. Choose two large primes $p$ and $q$
2. $n=p \cdot q$
3. Compute $\phi (n) = (p-1)(q-1)$
4. Select public exponent $e \in \{1,2,...,\phi(n)-1\}$, such that:\
$$
gcd(e, \phi(n))=1
$$
(so that we know $d$ will exist)
5. Compute $d$ such that\
$$
d \cdot e \equiv 1 \bmod \phi(n)
$$

You can use the EEA to find the inverse of $e$ - call that $t$.

You can use $t$ to find $d$ using:

$$
d = t \bmod \phi(n)
$$

## 7.4 - Fast Exponentiation

$x^8 = x * x * x * x * x * x * x * x$

That's a lot, and if we had a number that's 1024 bits long, this would take absolutely forever. However, $x^8 = ((x^2)^2)^2$, which is only 3 operations.

Through combinations of squaring and multiplying, we can get big fast.

Start with y=1, and scan the bits of the exponent from most to least significant.

- if the bit is 0, $y = y^2$
- if the bit is 1, $y=y^2*y$

Basically, squaring left-shifts the exponent (in binary), and multiplying switches the rightmost bit from zero to 1.

> BigInt.toString(2) will print your bigint as binary.

## 7.5 - Going *FASTER*

tl;dr: doing big math is hard

### 7.5.1 - fast encryption with short public exponents

make e small, like 3, 17, and 2^16+1. These are easy to do fast exponentiation with.

### 7.5.2 - Fast decryption with CRT

[The Chinese Remainder Theorem](./crt.md)

While $e$ can be small, $d$ cannot - otherwise attackers can brute-force it pretty easily. $d$ should be at least $0.3t$, where $t$ is the bit length of $n$.

Goal: $x^d \bmod n$

But, $x^d$ is gonna be absolutely absurdly big, and $n$ is also huge.

So, use [CRT](./crt.md) to get $x_d$ and $x_p$, and do $y_p = {x_p}^d_p \bmod p$, and the $q$ version, and then bring it back to the real world.

## 7.6 - Finding big primes

$p$ and $q$ should have about half the bitlength of the desired bitlength of $n$. So if $n$ should have a bitlength of 1024, $p$ and $q$ should be about 512.

Generate random big numbers, and see if they're prime tho.

### 7.6.1 - Are there big primes?

yes.

### 7.6.2 - Tests

**Fermat**

Basically, $a^{p-1} \equiv 1 \bmod p$ if p is prime. $a$ can be anything from 2 to $p-2$. We generally test a bunch of a's, and if they all pass, it's probably fine.

**Charmichael Numbers**

These are composite ints that behave like primes - they'll pass the Fermat test if $gcd(a,p)=1$. That's a lot of a's. They're sneaky.
