---
mathjax: true
---
[up](./index.md)

> This page doubles as a personal reference for MathJax commands

# What is a Ring?

A *Ring* is a set of integers ($\Bbb Z$) with a size ($m$).

$$\Bbb Z_m = \{ 0,1,2,\dots m-1 \}$$

*Rings* have associated *Operators* with special rules.

- Addition: '+'
- Multiplication: '*'

For all $a,b\in \Bbb Z_m$:

- $a + b \equiv c \bmod m$
- $a * b \equiv d \bmod m$

# Properties of Rings

## Closure

Note that $c,d \in \Bbb Z_m$

## Associative

- $(a+b)+c=a+(b+c)$
- $(a\cdot b)\cdot c=a\cdot (b\cdot c)$

## Identity

- $a+0=a\mod m$
- $a\cdot 1=a\mod m$

## Inverse

- $a+(-a)=0\mod m$
- $a\cdot a^{-1}=1\mod m$

Note that $a^{-1}$ only exists when $\gcd (a, m)=1$
