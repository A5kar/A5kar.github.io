---
layout: post
title: "Probability Models and Axioms"
---

General framework to calculate probability consists of the following steps:

- Specify the sample space $$\Omega$$.
- Specify the probability law
- Identify an event of interest
- Calculate...

## Sample Space

A sample space is legitimate when its elements are:
- mutually exclusive
- collectively exhaustive
- at the *right* granularity

## Probability Law

Can be:

- **discrete**, in which case $$\mathbb P(A)=\frac k n$$, where $$k$$ is the number of elements in $$A$$ and $$n$$ is the number of elements in $$\Omega$$.
- **continous**, in which case $$\mathbb P(A)$$ is the area/volume of the relevant range within which a variable can vary.

## Events

 Assuming $$A$$, $$B$$ and $$C$$ are events $$\subseteq\Omega$$, the following axioms are defined:

- **non-negativity**, $$\mathbb P(A)\geq 0$$
- **normalization**, $$\mathbb P(\Omega)=1$$
- **(finite) additivity**, $$A\cap B=\emptyset\implies\mathbb P(A\cup B)=\mathbb P(A)+\mathbb P(B)$$

From the above, the following results can be derived:

- \$$\mathbb P(A)\leq 1$$
- \$$\mathbb P(\emptyset)=0$$
- \$$A\subseteq B\implies \mathbb P(A)\leq\mathbb P(B)$$
- \$$\mathbb P(A\cup B)=\mathbb P(A)+\mathbb P(B)-\mathbb P(A\cap B)\leq\mathbb P(A)+\mathbb P(B)$$
- \$$\mathbb P(A\cup B\cup C)=\mathbb P(A)+\mathbb P(A^C\cap B)+\mathbb P(A^C\cap B^C\cap C)$$

In case you tend to forget them, you may also want to taking note of some basic [properties of set algebra](https://en.wikipedia.org/wiki/Algebra_of_sets). In particular, you should know by heart the commutative, associative and distributive properties of union/intersect operators, De Morgan's laws, as well as identity and complement relationships.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).