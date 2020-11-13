---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Chapter 8 - PKI / Logs / DHKE

# Chapter 8 - PKI / Logs / DHKE

RSA uses factoring big things as its *one-way* function. There's another one-way function called the *Discrete Logarithm Problem* (DLP).

We're gonna hit:

- Diffie-Hellman key exchange
- Cyclic groups
- The discrete logarithm problem
- Encryption with the Elgamal scheme

## 8.1 - Diffie-Hellman Key Exchange

This lets two parties exchange keys over an insecure channel.

Exponentiation in $\Bbb Z_p^*$, where $p$ is prime, is a one-way function. Also, it's commutative:

$$
k = (\alpha ^x)^y \equiv (\alpha ^y)^x \bmod p
$$

The value $k$ can be used as a key.

**Setup**:

1. Choose a large prime $p$
2. Choose an integer $\alpha \in \{2,3,...,p-2\}$
3. Publish $p$ and $\alpha$

**Alice**:

1. Choose $a = k_{pr,A} \in \{2,...,p-2\}$
2. Compute $A = k_{pub,A} \equiv \alpha ^a \bmod p$
3. Send $A$, Receive $B$
4. Compute $k_{AB} = k_{pub,B}^{k_{pr,A}} \equiv B^a \bmod p$

**Bob**:

1. Choose $b = k_{pr,B} \in \{2,...,p-2\}$
2. Compute $B = k_{pub,B} \equiv \alpha ^b \bmod p$
3. Send $B$, Receive $A$
4. Compute $k_{AB} = k_{pub,A}^{k_{pr,B}} \equiv A^b \bmod p$

In english:

- Each side has $\alpha$ and $p$
- Each side chooses a secret value
- Each side crates a public value, which is $\alpha^{secret}$
- They trade public values
- Then, they raise the other's public value to their own secret.
- End result: Both sides have $\alpha$ raised to both secret values.

$p$ should be a big prime, Generated in a similar way to in RSA. 1024 bits or more is good. $\alpha$ needs to be a primitive element. We'll hit that soon.

## 8.2 - Algebra

### 8.2.1 - Groups

A group is a set of elements, $G$, and an operation $\circ$ that combines two elements.

- Closed: $a \circ b = c \in G$
- Associative: $(a \circ b) \circ c = a \circ (b \circ c)$
- Neutral Element: $a \circ 1 = 1 \circ a = a$ for all $a \in G$
- Inverse Element: $a \circ a^{-1} = 1$ for all $a \in G$
- Can be abelian, if $a \circ b = b \circ a$ for all $a,b \in G$
	- so basically, no division

Operation $\circ$ is typically either multiply or add.

> **Theorem 8.2.1**
>
> The set $\Bbb Z_n^*$, having all $i=0,1,...,n-1$ where $gcd(i,n)=1$ is an abelian group under multiplication modulo $n$.

So basically, a group $\Bbb Z_n^*$ has all the integers coprime to $n$. If $n$ is prime, then it's every int smaller than $n$, otherwise theres a few missing.

### 8.2.2 - Cyclic groups

A group is finite if it has a finite number of elements. The size of the group, $|G|$, is called its *order* or *cardinality*.

> It's whack that order can be written ord(G) or |G|.
> The book seems to use |G| for groups, and ord(a) for elements.

The group $\Bbb Z_n^*$ has all integers smaller than $n$ that are coprime to $n$. Recall that euler's phi function is defined as the count of all integers smaller than $n$ that are coprime to $n$. Therefore:

$$
order(\Bbb Z_n^*) = \phi(n)
$$

Recall that, if $n$ can be expressed as $p^a$, then:

$$
\phi(p^a) = p^a-p^{a-1}
$$

> **Definition 8.2.3**
>
> The order $ord(a)$ of an element is the smallest number $k$ such that $a^k=1$.

If you aren't using multiplication, define $a^k$ as $a \circ a$, $k$ times. Also replace 1 with the neutral element of whatever group you're using.

The biggest order an element can have is the order of the group its in.

Example: $Z_{11}^*$, and $a=3$.

Take a look at this shit:

$$
a^1 = 3
a^2 = a^1 \cdot a = 9
a^3 = a^2 \cdot a = 27 \equiv 5 \bmod 11
a^4 = a^3 \cdot a = 15 \equiv 4 \bmod 11
a^5 = a^4 \cdot a = 12 \equiv 1 \bmod 11
a^6 = a^1 \cdot 1 = 3 \equiv 3 \bmod 11
a^7 = a^2 \cdot 1 = 3 \equiv 9 \bmod 11
a^8 = a^3 \cdot 1 = 3 \equiv 5 \bmod 11
a^9 = a^4 \cdot 1 = 3 \equiv 4 \bmod 11
a^10 = 1 \cdot 1 = 3 \equiv 1 \bmod 11
a^11 = a^1 \cdot 1 = 3 \equiv 3 \bmod 11
$$

See how once we hit $k=5$, it became one, which meant increasing $k$ just means we repeat where we've already been. So - $a$ *GENERATES* the sequence $\{3,9,5,4,1\}$.

So, we have our group, and elements of said group can generate other sets.

> **Definition 8.2.4**
>
> A group $G$ is a *Cyclic group* is it has an element $\alpha$ where $ord(\alpha)=ord(G)$. Such elements are called *Primitive Elements*, and/or *Generators*.

Recall that $ord(G)$ is the biggest that $ord(\alpha)$ can be.

If $\alpha$ of $G$ has max order (is a generator), then every element in $G$ can be written as $\alpha^i$ - aka $\alpha$ *generates* the entire group it's in. Whack!

In the group $\Bbb Z_11^\*$, $a=2$ generates the whole group. So, the group is cyclical. Now look at *this*:

$i$ | $2^i$
---|---
1  | 2
2  | 4
3  | 8
4  | 5
5  | 10
6  | 9
7  | 7
8  | 3
9  | 6
10 | 1

2 is a generator of the group, but it generates it in a seemingly random order. This is the basis of DLP cryptosystems.

> **Theorem 8.2.2**
>
> For every prime $p$, Group $\Bbb Z_p^*$ is an abelian finite cyclic group.

Now that's pretty wild.

> **Theorem 8.2.3**
>
> If $G$ is a finite group, then for every $a \in G$:
>
> - $a^{|G|} = 1$
> - $ord(a)$ divides $|G|$

So, if we use our base 11 group again, and it has order 10, and only 1, 2, 5, and 10 divide 10, then we know the order of every element has to be either 1, 2, 5, or 10.

It's also really wild that any element to the 10th power is 1.

> **Theorem 8.2.4**
>
> If $G$ is a finite cyclic group, then...
>
> - The number of primitive elements is $\phi(|G|)$
> - If $|G|$ is prime, every element other than 1 is primitive.

So in our base-11 group, there are $\phi(10)=4$ primitive elements.

If the group cardinality were prime $p$, everything would be primitive (except 1). If everything is primitive, then the order of everything is the order of the group, which is $p$.

### 8.2.3 - Subgroups

> **Theorem 8.2.5**
>
> If $G$ is a cyclic subgroup, then every element $a \in G$ generates a cyclic subgroup with $ord(a)$ elements.

If the order of the group is prime $p$, then every element except for 1 has an order of $p$.

> **Theorem 8.2.6**: Lagrange's theorem
>
> If H is a subgroup of G, then $|H|$ divides $|G|$

Here's a big one:

> **Theorem 8.2.7**
>
> Let G be a finite cyclic group, order $n$. $\alpha$ is a generator of G.
>
> For every int k that divides n, there exists exactly one cyclic subgroup H of G of order k. H can be generated from $\alpha^{n/k}$
>
> H holds exactly the elements $a \in G$ where $a^k=1$.
>
> There are no other subgroups.

This makes it easy to generate a subgroup of a desired size (that divides n at least), if you have a generator of your starting group.

## 8.3 - The Discrete Logarithm Problem

Yep. Here we go.

### 8.3.1 - in prime fields

Consider $\Bbb Z_p^*$, where $p$ is prime.

> **Definition 8.3.1**
>
> Given $\Bbb Z_p^*$, primitive element $\alpha$, and vanilla element $\beta$,
> The DLP is finding integer $x$, where $1 \leq x \leq p-1$ such that:
>
> $$
> \alpha^x \equiv \beta \bmod p
> $$

Rename x to k and $\beta$ to 1 and this looks a lot like trying to find the order of $\alpha$. Hmmm.

Since $\alpha$ is a primitive element, we know that x must exist.

I failed the logarithm section in high school. This looks particularly scary:

$$
x = \log_{\alpha} \beta \bmod p
$$
