---
mathjax: true
---
[up](../../index.md)

# Method of Moments Example - Exponential Distribution

$X$ => Population Data.  
$X$ is exponentially distributed => There is one parameter, $\lambda$.

## Known:

$$
E(X) = \frac {1} {\lambda}
$$

$$
V(X) = \frac {1} {\lambda ^ 2}
$$

> $\lambda$ is the *rate* of events, aka $\frac {\text {Number of Events} } {\text {Unit of Time}}$

## Process

Estimate $\lambda$ using the method of moments. Since there's only one parameter, we only need one equation.

$$
\begin {align}

m_1 &= \mu _ 1 &&
\bar x &= \mu &&
\bar x &= \frac 1 \lambda &&
\lambda &= \frac 1 {\bar x} &&
\therefore \hat \lambda &= \frac 1 {\bar x} &&

\end {align}
$$

Note that $E(\frac 1 {\bar x}) \ne \lambda$. $\frac 1 {\bar x}$ is *not* an unbiassed estimator for $\lambda$.
