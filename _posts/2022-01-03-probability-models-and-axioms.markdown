---
layout: post
title: "Probability Models and Axioms"
---

General framework to calculate probability consists of the following steps:

- Specify the sample space $$\Omega$$.
- Specify the probability law/distribution
- Identify an event of interest
- Calculate...

## Sample Space

A sample space is legitimate (see [L1 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab4)) when its elements are:

- mutually exclusive
- collectively exhaustive
- at the *right* granularity

## Probability Law/Distribution

The mathematical function that describes the probabilities of different possible outcomes are mainly of two types:

- **discrete**, in which case $$\mathbb P(A)=\frac{k}{n}$$, where $$k$$ is the number of elements in $$A$$ and $$n$$ is the number of elements in $$\Omega$$ (e.g. uniform, geometric...).
- **continuous**, in which case $$\mathbb P(A)$$ is the area/volume of the relevant range within which a variable can vary (e.g. uniform, exponential...).

## Axioms {#axioms}

 Assuming $$A$$, $$B$$ and $$C$$ are events $$\subseteq\Omega$$, the following axioms are defined:

|Axiom|Formula|
|-|:-:|
|Non negativity|$$\mathbb P(A)\geq 0$$|
|Normalization|$$\mathbb P(\Omega)=1$$ (see [L1 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab19))|
|(finite) Additivity|$$\begin{align}A_i\cap A_j=\emptyset, i\neq&j\implies\\\mathbb P(A_1\cup A_2\cup\dots A_n)&=\sum_{i=1}^n\mathbb P(A_i)\end{align}$$<br>(applies if $$A_i$$ are countable, see [L1 Q20](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab20))|

It follows that $$\mathbb P(A)\leq 1$$ and $$\mathbb P(\emptyset)=0$$, as well as relationships below (see [PS1 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s4-tab6)).

- $$A\subseteq B\implies\mathbb P(A)\leq\mathbb P(B)=\mathbb P(A)+\mathbb P(B\cap A^C)$$ (see [L1 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab10))
- $$\mathbb P(A)+\mathbb P(B)-\mathbb P(A\cap B)=\mathbb P(A\cup B)\leq\mathbb P(A)+\mathbb P(B)\le1$$ (see [L1 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab8))
- $$\mathbb P(A\cup B\cup C)=\mathbb P(A)+\mathbb P(A^C\cap B)+\mathbb P(A^C\cap B^C\cap C)$$ (see [L1 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab12))

Note that the second bullet can be rewritten as $$\mathbb P(A)+\mathbb P(B)-1\le \mathbb P(A\cap B)$$, or in a more general fashion $$\mathbb P(A_1\cap A_2\cap\dots A_n)\le\mathbb P(A_1)+\mathbb P(A_2)+\dots+\mathbb P(A_n)-(n-1)$$, which is known as [Bonferroni's inequality](https://en.wikipedia.org/wiki/Boole%27s_inequality#Bonferroni_inequalities).

## Miscellanea

Worthy of mention is the De Morgan's law (see [PS1 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s4-tab2))

$$\begin{align}(A\cap B)^C&=A^C\cup B^C\\ (A\cup B)^C&=A^C\cap B^C\end{align}$$

Finally, refreshing memory on the geometric series is also a good thing (see [L1 Q18](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab18))

$$\begin{align}
\sum_{i=0}^n q^i&=\frac{1-q^{n+1}}{1-q}\\
\sum_{i=0}^\infty q^i&=\frac{1}{1-q}, \lvert q\rvert<1\\
\sum_{i=1}^\infty q^i&=\frac{q}{1-q}, \lvert q\rvert<1
\end{align}$$

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

---

## Back-up

The properties below come from the basic [properties of set algebra](https://en.wikipedia.org/wiki/Algebra_of_sets). You should know them by heart (especially the De Morgan's law). You may add them in case you have some spare space and if they keep slipping out of your mind.

|Property|Formula|
|-|:-:|
|Commutative|$$\begin{align}A\cup B&=B\cup A\\ A\cap B&=B\cap A\end{align}$$|
|Associative|$$\begin{align}A\cup(B\cup C)&=(A\cup B)\cup C\\ A\cap (B\cap C)&=(A\cap B)\cap C\end{align}$$|
|Distributive|$$\begin{align}A\cup(B\cap C)&=(A\cup B)\cap(A\cup C)\\ A\cap (B\cup C)&=(A\cap B)\cup(A\cap C)\end{align}$$|
|Identity|$$\begin{align}A\cap\Omega&=A\\ A\cup\emptyset&=A\end{align}$$|
|Complement|$$\begin{align}A\cup A^C&=\Omega\\ A\cap A^C&=\emptyset\\\Omega^C&=\emptyset\\\emptyset^C&=\Omega\end{align}$$|
|Idempotent|$$\begin{align}A\cup A&=A\\ A\cap A&=A\end{align}$$|
|Domination|$$\begin{align}A\cup\Omega&=\Omega\\ A\cap\emptyset&=\emptyset\end{align}$$|
|Absorption law|$$\begin{align}A\cup(A\cap B)&=A\\ A\cap (A\cup B)&=A\end{align}$$|
