---
mathjax: true
---
[up](./index.md)

# Properties of Expectation

The Expectation of the Population is the Mean.

$$E(X)=\mu$$

Expectation has some Linear-ness

$$E(KX)=K\cdot E(X)$$

$$E(aX + bY)=a\cdot E(X)+b\cdot E(Y)$$

# Simplify Variance

$$
\begin{align}
V(X) & = \sigma ^2 \\
& = E(X-\mu)^2 \\
& = E(X^2)-E(X)^2 \\
& = E(X^2) - \mu ^2
\end{align}
$$

Magic Formula:

$$E(X^2)=\sigma^2+\mu^2$$

# CDF Definition

where $f(x)$ is the PDF of $X$.

$$
F_X(t)=P(X\leq t) = \int_{-\infty}^t f(x)\,dx
$$

# Definitions

Term | Explanation | Example
--- | --- | ---
Parameter | Summary measure of a Population | $\mu$, $\sigma$
Statistic | Summary measure of a Sample | $\bar x$, $s$ (sample std dev)
Estimator | Statistic to Estimate a Parameter | $\bar x$ estimates $\mu$
Estimate | Value of an Estimator for a Sample | 4
Point Estimation | Estimating a Param via a Statistic | N/A
Point Estimator | Estimator used in the above | N/A