---
layout: post
title: "Conditioning and Independence"
---

$$\newcommand{\ind}{\perp\!\!\!\perp}$$

## Conditioning

Conditional probability is defined as $$\mathbb P(A\lvert B)=\frac{\mathbb P(A\cap B)}{\mathbb P(B)}$$, assuming $$\mathbb P(B)>0$$. Conditioning makes the events outside of $$B$$ have *zero* probability{% if jekyll.environment == "development" %} (see [Prob L2 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab3)){% endif %}. Also note $$A\subseteq B\implies\mathbb P(A\lvert B)=\frac{\mathbb P(A)}{\mathbb P(B)}$${% if jekyll.environment == "development" %} (see [Prob L3 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab5) and [Prob MT1 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch7-s1-tab2)){% endif %}.

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
|Multiplication rule|$$\mathbb P(A_1\cap A_2\cap\dots A_n)=\mathbb P(A_1)\prod_{i=2}^n\mathbb P(A_i\lvert A_1\cap\dots A_{i-1})$${% if jekyll.environment == "development" %}<br>(see [Prob L2 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab9) and [Prob MT1 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch7-s1-tab3)){% endif %}|
|Total probability theorem|$$\mathbb  P(B)=\sum_{i=1}^n\mathbb P(A_i)\mathbb P(B\lvert A_i)$${% if jekyll.environment == "development" %}<br>(see [Prob L2 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab11)){% endif %}|
|Bayes' rule|$$\displaystyle\mathbb P(A_i\lvert B)=\frac{\mathbb P(A_i\cap B)}{\sum_{i=1}^n\mathbb P(A_i)\mathbb P(B\lvert A_i)}$${% if jekyll.environment == "development" %}<br>(see [Prob L2 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__2_Conditioning_and_Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s2-tab13)){% endif %}|

Bayesian inference, is a three step procedure:

- Draw an initial belief $$\mathbb P(A)$$ on possible causes of $$B$$
- Model $$B$$ under each $$A_i$$, that is $$\mathbb (B\lvert A_i)$$
- Draw conclusions about causes, $$\mathbb P(A_i\lvert B)$$

When building a model, create a separate branch for every combination events{% if jekyll.environment == "development" %} (see [Prob PS2 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab3)){% endif %}.

## Independence {#independence}

$$A$$ is independent from $$B$$ when $$\mathbb P(A\lvert B)=\mathbb P(A)$${% if jekyll.environment == "development" %} (see [Prob PS2 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab1) and [Prob PS2 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab4)){% endif %}. Accordingly, $$\mathbb P(A\cap B)=\mathbb P(A)\mathbb P(B)$${% if jekyll.environment == "development" %} (see [Prob L3 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab4), [Prob L3 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab6) and [Prob MT1 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch7-s1-tab5)){% endif %}. Often, independence is denoted with $$A\ind B$$, is symmetric ($$A\ind B\iff B\ind A$$), allows $$\mathbb P(B)=0$$ (as opposed to conditioning), and extends to complements ($$A\ind B\iff A\ind B^C$$){% if jekyll.environment == "development" %} (see [Prob L3 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab8)){% endif %}. 

Conditioning, however, affects independence, and $$\mathbb P(A\cap B\lvert C)=\mathbb P(A\lvert C)\mathbb P(B\lvert C)$$ **does not mean** that $$\mathbb P(A\cap B\lvert C^C)=\mathbb P(A\lvert C^C)\mathbb P(B\lvert C^C)$${% if jekyll.environment == "development" %} (see [Prob L3 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab10)){% endif %}.

Also, pairwise independence $$\mathbb P(A_i\cap A_j)=\mathbb P(A_i)\mathbb P(A_j), i\neq j$$ **does not imply** collective independence $$\mathbb P(A_1\cap A_2\cap\dots A_n)=\mathbb P(A_2)\mathbb P(A_2)\dots\mathbb P(A_n)$${% if jekyll.environment == "development" %} (see [Prob L3 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab13)){% endif %}.

## Reliability

Reliability is good example of *joint* probability of *independent* events. In the table below, $$U$$ and $$D$$ indicate that the *link* is up or down, respectively{% if jekyll.environment == "development" %} (see [Prob L3 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__3_Independence/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s3-tab16)){% endif %}.

|Mode|Diagram|Probability|
|-|:-:|:-:|
|Serial|![12457](/assets/images/2022-01-05-conditioning-and-independence/12457.png)|$$\mathbb P(U)=\mathbb P(U_1\cap U_2)=pq$$|
|Parallel|![21589](/assets/images/2022-01-05-conditioning-and-independence/21589.png)|$$\mathbb P(D)=\mathbb P(D_1\cap D_2)=(1-p)(1-q)$$<br>$$\mathbb P(U)=\mathbb P(U_1\cup U_2)=p+q-pq$$<br>(according to [inclusion-exclusion](/2022/01/03/probability-models-and-axioms.html#axioms) formula)|

Assuming $$L_i\in\{0,1\}$$ indicates that the *network* is up when the link $$i$$ has failed, then the probability of the *network* being up despite one element failing is $$\mathbb P(L)=\sum_{i=1}^n \frac{p_i}{\sum_{i=1}^np_i}L_i$${% if jekyll.environment == "development" %} (see [Prob PS2 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch4-s5-tab2)){% endif %}.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).
