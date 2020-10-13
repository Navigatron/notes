---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Groups

# Groups

A group is a set of elements. There is an *operation*, represented by $\cdot$, that could be anything (add, multiply, etc).

A group has four properties:

## Closure

For all $a, b \in G$, $a \cdot b \in G$

AKA do the operation on any two elements, and the result is also in the group.

## Associativity

For all $a, b, c \in G$, we have:

$$
(a \cdot b) \cdot c = a \cdot (b \cdot c)
$$

AKA you can apply the operation in any order, and the result is the same.

## Existence of identity

For all $a \in G$, There is an element $e \in G$, such that:

$$
e \cdot a = a \cdot e = a
$$

So, like, $a+0=a$, or $a*1=a$

## Existence of inverse

For all $a \in G$, there is an element $b \in G$, such that:

$$
a \cdot b = b \cdot a = e
$$

So, if $e$ were 1 for multiply, then $b$ is whatever multiplies $a$ to 1. $b=1/a$

If $\cdot $ is plus, then b is whatever gets a to zero, like $-a$.

# Commutative Groups / Abelian Groups

These are regular groups with one more property:

## Commutativity

This basically means the operands can *commute* / move around.

For all $a, b \in G$, we have:

$$
(a \cdot b) = (b \cdot a)
$$

## Example

Take $Z_{15}^{*}$ - this is a group, under the multiplication operator, and all the elements are less than 15. If we only include the elements where $gcd(a,15)=1$, then it is an Abelian group:

- a * b * c mod n is associative
- It guess a * b = c is in the group?
	- I mean it makes sense
- 1 is a member of the group, so an identity element exists
- Since they're all coprime to 15, they have inverses, which I guess are also in the group apparently? Are all inverses also coprime to n?
- And yes $a*b = b*a$ so it's abelian

# Finite Groups

Finite groups have a finite number of elements.

The sizeof operator looks like two bars on either side of the text, like |G|, idk if that's the tex way?

$$
|G| < Inf.
$$

# Subgroups

A subset of a group that is also a group is called a subgroup. Notation:

- Group G under operator: $(G, \cdot )$
- Group G prime is a subset of G: $G' \subset G$

I hope this mathjax works lol

## Generating Subgroups over Addition

I'm not sure where this formula came from:

$$
a^k \equiv ka \bmod n
$$

Looking at the group $Z_6$ (no op means addition?), generating from zero:

$$
\langle 0 \rangle = \{0\}
$$

Zero to any power is zero, and zero times anything is zero. So, this subgroup has zero in it.

Let's try two: Two times anything is an even number. Mod 6, we can only get 0, 2, and 4 out. That's the subgroup then.

$$
\langle 2 \rangle = \{0,2,4\}
$$

## Generating Subgroups over Multiplication

The magic formula is:

$$
a^k \equiv a^k \bmod n
$$

# Cyclic Subgroups

yeet
