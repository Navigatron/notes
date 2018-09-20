---
mathjax: true
---
[up](../../index.md)

# Maximum Likelyhood Estimators - Principles

MoM Estimators are okay... but these are better.

## Theory:

Maximize the Following Function:

$$ L(\theta)=P(\text{our sample appearing}) $$

We'll find the value of $\theta$ that maximizes the probability of our sample appearing.

In reality, the likelyhood function is composed more like this:

$$
f(x) = \theta X ^ {\theta - 1}
$$

$$
L(\theta _ 1 , \theta _ 2 , ... \theta _ k ; x_1, x_2, ... x_n) = f(x_1) \dot f(x_2) \dot ... \dot f(x_n)
$$

## Process:

1. Identify the PMF/PDF of the population.
2. Write the Likelyhood Function
    - Either a joint PMF or joint PDF
3. Simplify! If needed, simplify further with $ln()$
4. Maximize the function:
    1. Take Derivative
    2. Set equal to zero to find critical points
    3. Verify crit points are max by showing the second derivative is negative
5. Write conclusion in complete sentences.

## Log Rules

These are helpful.

$ln(a\dot b)=ln(a)+ln(b)$

$ln(a^b) = b\dot ln(a)$
