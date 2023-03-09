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

A sample space is legitimate{% if jekyll.environment == "development" %} (see [Prob L1 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab4)){% endif %} when its elements are:

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
|Normalization|$$\mathbb P(\Omega)=1$${% if jekyll.environment == "development" %} (see [Prob L1 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab19)){% endif %}|
|(finite) Additivity|$$\begin{align}A_i\cap A_j=\emptyset, i\neq&j\implies\\\mathbb P(A_1\cup A_2\cup\dots A_n)&=\sum_{i=1}^n\mathbb P(A_i)\end{align}$$<br>(applies if $$A_i$$ are countable){% if jekyll.environment == "development" %} (see [Prob L1 Q20](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab20)){% endif %}|

Putting together the three axioms above, it follows that $$\mathbb P(A)\leq 1$$ and $$\mathbb P(\emptyset)=0$$. Further relationships are summarized below{% if jekyll.environment == "development" %} (see [Prob PS1 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s4-tab6)){% endif %}.

|Formula|Equivalent form|
|:-:|:-:|
|$$\mathbb P(A)$$|$$\mathbb P(A\cap B)+\mathbb P(A\cap B^C)$$|
|$$\mathbb P(A^C)$$|$$1-\mathbb P(A)$$|
|$$\mathbb P(A\cup B)$$|$$\begin{cases}\mathbb P(B),&\text{if }A\subseteq B\\\mathbb P(A)+\mathbb P(B)-\mathbb P(A\cap B),&\text{otherwise}\end{cases}$$<br>(it follows that $$\mathbb P(A)\le\mathbb P(B)$$ if $$A\subseteq B$$){% if jekyll.environment == "development" %} (see [Prob L1 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab8) and [Prob L1 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab10)){% endif %}|
|$$\mathbb P(A\cap B)$$|$$\begin{cases}\mathbb P(A),&\text{if }A\subseteq B\\\mathbb P(A)+\mathbb P(B)-\mathbb P(A\cup B),&\text{otherwise}\end{cases}$$|

From $$\mathbb P(A\cup B)=\mathbb P(A)+\mathbb P(B)-\mathbb P(A\cap B)$$ we can derive two inequalities: (a) the **union bound**, $$\mathbb P(A\cup B)\le\mathbb P(A)+\mathbb P(B)$$, because $$\mathbb P(A\cap B)\ge0$$; and (b) the **Bonferroni inequality**, that is obtained by swapping the union with the intersection, $$\mathbb P(A\cap B)\ge\mathbb P(A)+\mathbb P(B)-1$$, because $$\mathbb P(A\cup B)\le1$$. Both inequalities can be generalized using the method of [mathematical induction](https://en.wikipedia.org/wiki/Mathematical_induction).

|Formula|Equivalent form|
|:-:|:-:|
|**union bound**|$$\displaystyle\mathbb P\left(\bigcup_{i=1}^n A_i\right)\le\sum_{i=1}^n\mathbb P(A_i)$$|
|**Bonferroni inequality**|$$\displaystyle\mathbb P\left(\bigcap_{i=1}^n A_i\right)\ge\sum_{i=1}^n\mathbb P(A_i)-(n-1)$$|

Since $$\mathbb P(B)-\mathbb P(A\cap B)=\mathbb P(A^C\cap B)$$, then $$\mathbb P(A\cup B)=\mathbb P(A)+\mathbb P(A^C\cap B)$$ is an alternative expression of the union, using complements{% if jekyll.environment == "development" %} (see [Prob L1 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab12)){% endif %}. Note that if we join another event, we have $$\mathbb P((A\cup B)\cup C)=\mathbb P(A\cup B)+\mathbb P(C)-\mathbb P((A\cup B)\cap C)$$, which can be further expanded into $$\mathbb P(A)+\mathbb P(B)+\mathbb P(C)-\mathbb P(A\cap B)-\mathbb P(B\cap C)-\mathbb P(A\cap C)+\mathbb P(A\cap B\cap C)$$. In general, this relationship is known as the [inclusion-exclusion](https://en.wikipedia.org/wiki/Inclusion–exclusion_principle) formula.

$$\mathbb P\left(\bigcup_{i=1}^n A_i\right)=\sum_{i=1}^n\mathbb P(A_i)-\sum_{i\lt j}\mathbb P(A_i\cap A_j)+\sum_{i\lt j\lt k}\mathbb P(A_i\cap A_j\cap A_k)+\dots(-1)^{n+1}\mathbb P\left(\bigcap_{i=1}^n A_i\right)$$

## Miscellanea

Worthy of mention is the De Morgan's law{% if jekyll.environment == "development" %} (see [Prob PS1 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s4-tab2)){% endif %}

$$\begin{align}(A\cap B)^C&=A^C\cup B^C\\ (A\cup B)^C&=A^C\cap B^C\end{align}$$

Finally, refreshing memory on the geometric series is also a good thing{% if jekyll.environment == "development" %} (see [Prob L1 Q18](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__1_Probability_models_and_axioms/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch3-s1-tab18)){% endif %}.

$$\begin{align}\sum_{i=0}^n q^i&=\frac{1-q^{n+1}}{1-q}&\sum_{i=0}^\infty q^i&=\frac{1}{1-q}, \lvert q\rvert<1\end{align}$$

Which leads to the following general formula{% if jekyll.environment == "development" %} (see [Prob MT1 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch7-s1-tab7)){% endif %}.

$$\sum_{i=k}^\infty q^i=\sum_{i=0}^\infty q^i-\sum_{i=0}^{k-1} q^i=\frac{1}{1-q}-\frac{1-q^{k-1+1}}{1-q}=\frac{q^k}{1-q}$$

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

### Set algebra

The properties below come from the basic [properties of set algebra](https://en.wikipedia.org/wiki/Algebra_of_sets). You should know them by heart (especially the De Morgan's law). You may add them in the case you have some spare space and if they keep slipping out of your mind.

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
