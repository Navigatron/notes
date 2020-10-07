---
mathjax: true
---

[Home](../../../index.md) > [Crypto](./index.md) > Tikz

# Extended Euclidean Algorithm (EEA)

Given two integers $a$ and $b$, The EEA finds $x$, $y$, and $z$, such that:

$$
z = ax+by = gcd(a, b)
$$

## What is the algorithm?

In javascript:

```js
// ax + by = gcd(a,b) = d
// function: a,b -> x, y, d
function xgcd(a, b) {
	if (b === 0) {
		return [1, 0, a];
	}
	let [x, y, d] = xgcd(b, a % b);
	return [y, x-y*Math.floor(a/b), d];
}
```

## Finding multiplicative inverses

Consider $a \bmod b$:

A multiplicative inverse $a^{-1}$ only exists if $a$ and $b$ are coprime, aka $gcd(a,b)=1$. Therefore, the EEA results can be simplified:

$$
z = ax+by = gcd(a, b)
1 = ax+by = gcd(a, b)
ax+by = 1
ax-1=-yb
ax \equiv 1 \bmod b
a^{-1}=x
$$
