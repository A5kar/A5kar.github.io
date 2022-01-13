---
layout: post
title: "Conditioning and Independence"
---

## Definition {#definition}

Conditional probability is defined as $$\mathbb P(A\lvert B)=\frac{\mathbb P(A\cap B)}{\mathbb P(B)}$$, assuming $$\mathbb P(B)>0$$. Conditioning makes the events outside of $$B$$ have *zero* probability (see [L2 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab3)). Also note $$A\subseteq B\implies\mathbb P(A\lvert B)=\frac{\mathbb P(A)}{\mathbb P(B)}$$ (see [L3 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab5)).

Conditional probabilities share properties of ordinary probabilities.

 |Axiom|Formula|
 |-|:-:|
 |Non negativity|$$\mathbb P(A\lvert B)\geq 0$$|
 |Normalization|$$\mathbb P(\Omega\lvert B)=1$$|
 |(finite) Additivity|$$\begin{align}A_i\cap A_j=\emptyset, i\neq&j\implies\\\mathbb P(A_1\cup A_2\cup\dots A_n\vert B)&=\sum_{i=1}^n\mathbb P(A_i\lvert B)\end{align}$$|

## Main three tools {#main_three_tools}

Obtained from application of the definition $$\mathbb P(A\cap B)=\mathbb P(A)\mathbb P(B\lvert A)$$.

|Name|Rule|
|-|:-:|
|Multiplication rule|$$\mathbb P(A_1\cap A_2\cap\dots A_n)=\mathbb P(A_1)\prod_{i=2}^n\mathbb P(A_i\lvert A_1\cap\dots A_{i-1})$$<br>(see [L2 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab9))|
|Total probability theorem|$$\mathbb  P(B)=\sum_{i=1}^n\mathbb P(A_i)\mathbb P(B\lvert A_i)$$<br>(see [L2 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab11))|
|Bayes' rule|$$\displaystyle\mathbb P(A_i\lvert B)=\frac{\mathbb P(A_i\cap B)}{\sum_{i=1}^n\mathbb P(A_i)\mathbb P(B\lvert A_i)}$$<br>(see [L2 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab13))|

Bayesian inference, is a three step procedure:

- Draw an initial belief $$\mathbb P(A)$$ on possible causes of $$B$$
- Model $$B$$ under each $$A_i$$, that is $$\mathbb (B\lvert A_i)$$
- Draw conclusions about causes, $$\mathbb P(A_i\lvert B)$$

When building a model, create a separate branch for every combination events (see [PS2 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab3)).

## Independence {#independence}

Intuitively, $$A$$ is independent from $$B$$ when $$\mathbb P(A\lvert B)=\mathbb P(A)$$ (see [PS2 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab1) and [PS2 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab4)). Accordingly, $$\mathbb P(A\cap B)=\mathbb P(A)\mathbb P(B)$$ (see [L3 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab4) and [L3 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab6)). It follows that independence is symmetric, allows $$\mathbb P(B)=0$$ and extends to complements, $$\mathbb P(A\cap B^C)=\mathbb P(A)\mathbb P(B^C)$$ (see [L3 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab8)). 

Conditioning, however, affects independence, and $$\mathbb P(A\cap B\lvert C)=\mathbb P(A\lvert C)\mathbb P(B\lvert C)$$ **does not mean** that $$\mathbb P(A\cap B\lvert C^C)=\mathbb P(A\lvert C^C)\mathbb P(B\lvert C^C)$$ (see [L3 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab10)).

Also, pairwise independence $$\mathbb P(A_i\cap A_j)=\mathbb P(A_i)\mathbb P(A_j), i\neq j$$ **does not imply** collective independence $$\mathbb P(A_1\cup A_2\cup\dots A_n)=\mathbb P(A_2)\mathbb P(A_2)\dots\mathbb P(A_n)$$ (see [L3 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab13)).

## Reliability

Reliability is good example of *joint* probability of *independent* events. In the table below, $$U$$ and $$D$$ indicate that the *link* is up or down, respectively (see [L3 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab16)).

|Mode|Diagram|Probability|
|-|:-:|:-:|
|Serial|![12457](/assets/images/2022-01-05-conditioning-and-independence/12457.png)|$$\mathbb P(U)=\mathbb P(U_1)\mathbb P(U_2)$$|
|Parallel|![21589](/assets/images/2022-01-05-conditioning-and-independence/21589.png)|$$\mathbb P(D)=\mathbb P(D_1)\mathbb P(D_2)$$|

Assuming $$L_i\in\{0,1\}$$ indicates that the *network* is up when the link $$i$$ has failed, then the probability of the *network* being up despite one element failing is $$\mathbb P(L)=\sum_{i=1}^n \frac{p_i}{\sum_{i=1}^np_i}L_i$$ (see [PS2 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab2)).

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).