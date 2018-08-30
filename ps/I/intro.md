---
mathjax: true
---
[up](../index.md)
# Groundwork and Discrete Probability

## Set Theory

A capital letter denotes a set. Sets are collections of... stuff.
- Numbers
- Strings
- Shoe Sizes
- Shoes
- Whatever, physical or symbolic.

Below, the set $$A$$ contains some numbers.

$$ A = \{ 5, 10, 15, 20, 2 \} $$

There are some symbols involved for operations.

 Symbolic | Meaning | Explanation
 --- | --- | ---
 $$X \in A$$ | Element Of | X is a thing in set A
 $$A \subset B$$ | Subset | A is a subset of B. If it's in A, it must be in B.
 $$A \cup B$$ | Union | Set of all things in A or B. Give me Both.
 $$A \cap B$$ | Intersection | Set of things in both A and B. The Overlap part of the Venn-Diagram

### Probability

Sets contain possible outcomes. In flipping a coin, there are two possible outcomes: Heads, and Tails.

$$ Flip = \{Heads, Tails\}$$

Sets in probability are *Evaluated*. When the experiment is performed, we get a result. The Probability that Set F (for flip) evaluates to Heads is as follows:

$$P(F = Heads)$$

The set of ping-pong balls in the lottery machine contains the numbers 1 to 30. You've bet on 7.

$$P(L = 7) = \frac {1} {30}$$

## Axioms of Probability

1. The Probability of an Event is Greater than or Equal to Zero.

    $$P(A) \geq 1$$

2. The Probability of Everything is 1.

    $$P(\varepsilon) = 1$$

3. The probability of something in a group occurring, is equal to the sum of the probabilities of each thing.

    $$P(\cup_{k}A_{k}) = \Sigma P(A_{k})$$

The last one is a *little* confusing. Take the union of a bunch of things.

> Combine all our little sets... INTO A **SUPER SET.**

This is just the same as adding them all together - *As long as they don't overlap.*

## Conditional Probability

$A$ and $B$ are possible events. They could both happen, or maybe only one. If B has already happened, What's the probability that A will also happen?

The following is read as "The Probability of $A$ given $B$."

$$P(A \| B)$$

You're falling from the sky. You're going to land in B. What's the probability that you also land in A? Think of it as Overlap of A and B divided by total area of B.

In fancy notation, it looks like this:

$$P(A \| B) = \frac {P(A \cap B)} {P(B)}$$

## Magic Formulas

1. The Probability that something will happen Plus the Probability that it wont Equals One. It either will or wont, there's no other option.

    $$P(A)+P(A^k)=1$$

2. `A Union B` equals `A+B-overlap`. Don't count the overlap twice.

    $$P(A \cup B) = P(A) + P(B) - P(A \cap B)$$

3. If B is only defined in relation to A, use this.

    $$P(B)=P(X\cap A)+P(X\cap A^c)$$

It's worth noting that $A^c$ is "A Complement", or the probability that a *won't* happen, aka $1-P(A)$

## Discrete Probability - PMF

PMF = Probability Mass Function

For Discrete Probability (drawing from a set), this is more of a lookup table than a function.

Sum of two coin flips (heads=1, tails=0):

event | $P(event)$
--- | ---
0 | $\frac {1} {4}$
1 | $\frac {1} {2}$
2 | $\frac {1} {4}$

## Expectation

### Definition

The Weighted average of all possible outcomes. The weights are the probabilities of the outcome.

$$E(X)=\Sigma x*P(X=x)$$

A function of a random variable evaluates to... a random variable. Fortunately, it's the same idea.

$$E(g(X))=\Sigma g(x)\*P(X=x)$$

What is $E(X^2)$? Think of it as $E(g(x))$, where $g(x)=x^2$

$$E(X^2)=\Sigma x^2*P(X=x)$$

### Mean

The Mean is what you expect the results to be on average. This greek letter is pronounced "mew".

$$\mu = E(X)$$

### Variance

Take each Data Point, find it's distance from the center. Square it. Find the expectation of that.

Variance tells you how far data points will be, on average, from the mean.

Hard but understandable:

$$V(X)=E((X-\mu)^2)$$

Simplified:

$$V(X)=E(X^2)-(E(X))^2$$
