---
layout: post
title: "Continuous Random Variables"
---

## Definition

A RV $$X$$ is continuous if it can be described by a probability density function (PDF) $$f_X(x)$$, where $$f_X(x)\cdot\delta\approx\mathbb P(x\le X\le x+\delta)$$ for an arbitraty small $$\delta>0$$. It follows that continuous RV [almost never](https://en.wikipedia.org/wiki/Almost_surely) takes an exact value $$x$$ (formally, $$\mathbb P(X=x)=0$$) (see [L8 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab3)); indeed, in such case the probability is associated with an interval where it could lie, $$\mathbb P(a\le X\le b)=\int_a^b f_X(x)dx$$ (see [L8 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab5)). Analogously to [discrete RV](/2022/01/08/discrete-random-variables.html#definition), the basic axioms apply.

- $$f_X(x)>0$$, non-negativity
- $$\int_{-\infty}^\infty f_X(x)dx=1$$, normalization (see [L8 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab7))

## Expectation

Definition does not change with respect to [discrete RV](/2022/01/08/discrete-random-variables.html#expectation), except that integral replaces sum. Hence, $$\mu_X=\mathbb E[X]=\int_{-\infty}^\infty xf_X(x)dx$$, with the same assumption that $$\int_{-\infty}^\infty\vert x\rvert f_X(x)dx\le\infty$$.

|Property|Formula|
|-|:-:|
|Bounds|$$a\le X\le b\implies a\le\mathbb E[X]\le b$$|
|Non negativity|$$X\ge0\implies\mathbb E[X]\ge0$$|
|Non negativity, with $$X\ge0$$|$$\displaystyle\mathbb E[X]=\int_{0}^\infty\mathbb P(X>k)dx$$ (see [PS5 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab5))|
|[Law Of The Unconscious Statistician](https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician) (LOTUS)|$$\displaystyle\mathbb E[g(X)]=\int_{-\infty}^\infty g(x)f_X(x)dx$$ (see [L8 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab10))|
|Linearity|$$E[aX+b]=a\mathbb E[X]+b$$|

## Variance

Exactly same definitions and properties of a [discrete RV](/2022/01/08/discrete-random-variables.html#variance).

## Basic continuous RV distributions

|RV|PMF<br>$$f_X(x)$$|Expectation<br>$$\mu_X=\mathbb E[X]$$|Variance<br>$$\sigma_X^2=\text{var}(X)$$|
|-|:-:|:-:|:-:|:-:|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\displaystyle\frac{1}{b-a}$$|$$\displaystyle\frac{b+a}{2}$$|$$\displaystyle\frac{1}{12}(b-a)^2$$|
|Exponential<br>$$\text{Exp}(\lambda)$$|$$\begin{cases}\lambda e^{-\lambda x}&x\ge0\\0&\text{otherwise}\end{cases}$$|$$\displaystyle\frac{1}{\lambda}$$|$$\displaystyle\frac{1}{\lambda^2}$$|
|Normal<br>$$\mathcal N(\mu_X,\sigma_X^2)$$|$$\displaystyle\frac{1}{\sqrt{2\pi\sigma_X^2}}\exp\left(-\frac{1}{2\sigma^2}(x-\mu_X)^2\right)$$|$$\mu_X$$|$$\sigma^2$$|

## Conditioning

Aside from replacing sums with integrals, one could argue that conditioning in case of continuous RV is exactly the same as with [discrete RV](/2022/01/08/discrete-random-variables.html#conditioning) (see [L9 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab3)).

Unless indicated otherwise, integrations in the table below are from $$-\infty$$ to $$\infty$$. Again, we assume that $$\mathbb P(A)>0$$, as well as $$f_Y(x)>0$$, otherwise the conditioning is not defined (see [L10 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab3) and [L10 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab7)).

|Property|Conditional on event $$A$$|Conditional on RV $$Y$$|
|-|:-:|:-:|
|PMF|$$\displaystyle f_{X\lvert A}(x)\delta\approx\mathbb P(x\le X\le x+\delta\lvert A)$$<br>$$\displaystyle f_{X\lvert X\in A}(x)=\begin{cases}\frac{f_X(x)}{\mathbb P(A)}&\text{if $x\in A$}\\0&\text{otherwise}\end{cases}$$|$$\begin{gather}\displaystyle f_{X\lvert Y}(x\lvert y)\delta\approx\\\mathbb P(x\le X\le x+\delta\lvert y\le Y\le y+\varepsilon)\end{gather}$$<br>$$f_{X\lvert Y}(x\lvert y)=\frac{f_{X,Y}(x,y)}{f_Y(y)}$$<br>(see [L10 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab5) and [L10 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab13))|
|Normalization|$$\displaystyle\int f_{X\lvert A}(x)dx=1$$|$$\displaystyle\int f_{X\lvert Y}(x\lvert y)dx=1$$|
|Expectation|$$\displaystyle\mathbb E[X\lvert A]=\int x f_{X\lvert A}(x)dx$$|$$\displaystyle\mathbb E[X\lvert Y=y]=\int x f_{X\lvert Y}(x\lvert y)dx$$
|LOTUS|$$\displaystyle\mathbb E[g(X)\lvert A]=\int g(x)f_{X\lvert A}(x)dx$$|$$\displaystyle\mathbb E[g(X)\lvert Y=y]=\int g(x)f_{X\lvert Y}(x\lvert y)dx$$
|[Total probability](2022-01-05-conditioning-and-independence.markdown#main_three_tools)|$$\displaystyle f_X(x)=\sum_{i=1}^n\mathbb P(A_i)f_{X\lvert A_i}(x)$$|$$\displaystyle f_X(x)=\int f_Y(y)f_{X\lvert Y}(x\lvert y)dy$$
|Total expectation|$$\displaystyle\mathbb  E[X]=\sum_{i=1}^n\mathbb P(A_i)\mathbb E[X\lvert A_i]$$|$$\displaystyle\mathbb E[X]=\int f_Y(y)\mathbb E[X\lvert Y=y]dy$$

## Independence

Subject to customary adjustments, independence for continuous RV is the same as for [discrete RV](/2022/01/08/discrete-random-variables.html#independence), and relevant relationships can be derived if $$f_{X,Y}(x,y)=f_X(x)f_Y(y)$$ (see [L10 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab9) and [L10 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab10)).

## Memorylessness

Exponential distribution can be seen as a continuous analog of the geometric distribution, which also enjoys [memorylessness](/2022/01/08/discrete-random-variables.html#memorylessness). Bearing in mind that $$\mathbb P(X>x)=e^{-\lambda x}$$, and given that $$X>y$$ (with $$y<x$$), then we can prove that $$\mathbb P(X>x\lvert X>y)=\mathbb P(X>x-y)$$. This also means that the probability of success in the interval $$x+\delta$$, given that $$X>x$$, is $$\mathbb P(x\le X\le x+\delta\lvert X>x)\approx\lambda\delta$$ (see [L9 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab6)).

## Joint PDFs

Again, once sums have been replaced with integrals, joint PDF have the same properties as [joint PMFs](/2022/01/08/discrete-random-variables.html#joint_pmfs), including derivation of *marginal* distributions from the *joint* distribution (see [L9 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab15) and [L9 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab17)). Bearing in mind that the probability of $$(X,Y)\in A$$ is $$\int_{(X,Y)\in A}f_{X,Y}(x,y)dxdy$$, one should notice that the order of integration is not essential (see [L9 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab13)).

It is important that the RVs are jointly continuous, to be described by a joint PDF. Consider $$X$$ and $$Y$$ and assume that the entire probability is concentrated on a curve described by the two RVs laying on the $$X-Y$$ plane. In this scenario, the two RVs are **not** jointly continuous, because the entire probability is concentrated on top of that curve, which is contraddictory with the assumption that in case of continuous RV, probabilities are associated with an area/volume (see [L9 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab11)).

If you are having difficulties picturing it, think of one dimensional analogy where $$X\sim\mathcal N(c,0)$$. This means that all probability is concentrated in a single point and is incompatible with the definition of a continuous RV (it can be a discrete RV, though).

## Mixed distributions

$$Z$$ is a mixed RV, if considering $$X$$ discrete and $$Y$$ continuous, we have as follows (see [L9 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab8)).

$$z=\begin{cases}X&\text{with probability $p$}\\Y&\text{with probability $(1-p)$}\end{cases}$$

Note that in this case $$\mathbb E[Z]=\mathbb P(X)\mathbb E[X]+\mathbb P(Y)\mathbb E[Y]$$ (see [L9 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab10)).

## Cumulative distribution function

Probability that $$X$$ will take a value less than $$x$$ is defined as cumulative distribution function (CDF), or $$F_X(x)=\mathbb P(X\le x)$$. Note that CDF does not distinguish if $$X$$ is discrete or continuous (or mixed), and applies analogously except that in case of discrete RV it is calculated as $$F_X(x)=\sum_{k\le x}p_X(x)$$, while in case of continuous RV we use $$F_X(x)=\int_{-\infty}^x f_X(x)dx$$. The latter clearly expresses that $$f_X(x)=\frac{\partial}{\partial x}F_X(x)$$ (see [L8 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab12)).

|Property|Formula|
|-|:-:|
|Non decreasing|$$a\le b\implies F_X(a)\le F_X(b)$$|
|Equivalency|$$\mathbb P(a\le X\le b)=F_X(b)-F_X(a)$$|
|Bounds|$$\displaystyle\lim_{x\rightarrow-\infty} F_X(x)=0,\lim_{x\rightarrow\infty} F_X(x)=1$$|

CDF can be calculated also for joint PMFs; in such case $$F_{X,Y}(x,y)=\mathbb P(X\le x, Y\le y)$$, where $$f_{X,Y}(x,y)=\frac{\partial^2}{\partial x\partial y}F_{X,Y}(x,y)$$. For $$X$$ and $$Y$$ independent, it is therefore $$F_{X,Y}(x,y)=F_X(x)F_(y)$$, and vice-versa (see [L10 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab11)). Also, note that if $$X\ge a$$ and $$Y\ge b$$, then $$F_{X,Y}(a,y)=0$$ and $$F_{X,Y}(x,b)=0$$, due to continuity (see [L9 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab19)).

## Normal distribution

$$X$$ is a normal RV with mean $$\mu_X$$ and variance $$\sigma_X^2$$ if $$X\sim\mathcal N(\mu_X,\sigma_X^2)$$, where $$Z\sim\mathcal N(0,1)$$ is a *standard* normal RV. Note that where $$\sigma^2_X=0$$ is permitted, this case would revert to a constant [discrete RV](/2022/01/08/discrete-random-variables.html#basic_discrete_distributions) (see [L8 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab14)).

Thanks to linearity, $$Y=aX+b$$ is also normal, $$Y\sim N(a\mu_X+b, a^2\sigma_X^2)$$ (see [PS5 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab1)). Accordingly, any $$X$$ can be expressed in terms of $$Z$$ and vice-versa; where $$Z=\frac{X-\mu_X}{\sigma_X}$$ is known as *standardization*. CDF of $$Z\sim\mathcal N(0,1)$$ is referred to as $$\Phi(z)=F_Z(z)$$, for which **normal tables** are provided. Thanks to standardization, $$F_X(x)$$ of any $$X\sim\mathcal(\mu_X,\sigma_X^2)$$ can be calculated as $$\Phi(\frac{x-\mu_X}{\sigma_X})$$. Considering that normal tables are provided in the form of $$\Phi(q)=\mathbb P(z\le q), q>0$$, other useful forms are as follows.

|Formula|Equivalent form|
|:-:|:-:|
|$$\mathbb P(Z\le q)$$|$$\Phi(q)$$ (see [L8 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab16))|
|$$\mathbb P(Z\le -q)$$|$$1-\Phi(q)$$|
|$$\mathbb P(Z\ge q)$$|$$1-\Phi(q)$$|
|$$\mathbb P(Z\ge -q)$$|$$\Phi(q)$$|
|$$\mathbb P(a\le Z\le b)$$|$$\Phi(b)-\Phi(a)$$|
|$$\mathbb P(\lvert Z\rvert\le q)$$|$$2\Phi(q)-1$$|
|$$\mathbb P(\lvert Z\rvert\ge q)$$|$$2(1-\Phi(q))$$|

In case $$X_i\overset{iid}{\sim}\mathcal N(\mu_X,\sigma_X^2)$$, their joint probability $$f_{X_1,\dots X_n}(x_1,\dots,x_2)$$ is as follows (see [L10 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab15)).

$$\prod_{i=1}^n f_X(x)=\frac{1}{\sqrt{(2\pi\sigma_X^2)^n}}e^{-\frac{1}{2\sigma_X^2}\sum_{i=1}^n(x_i-\mu_X)^2}$$

## Bayes' rule

This powerful [tools](/2022/01/05/conditioning-and-independence.html#main_three_tools) can be now reviewed in the following four flavors.

|Prior $$X$$|Conditioned $$Y$$|Posterior $$X$$|
|:-:|:-:|:-:|
|discrete|discrete|$$\displaystyle p_{X\lvert Y}(x\lvert y)=\frac{p_X(x)p_{Y\lvert X}(y\lvert x)}{\sum_x p_X(x)p_{Y\lvert X}(y\lvert x)}$$ (see [L10 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab17))|
|discrete|continuous|$$\displaystyle p_{X\lvert Y}(x\lvert y)=\frac{p_X(x)f_{Y\lvert X}(y\lvert x)}{\sum_x p_X(x)f_{Y\lvert X}(y\lvert x)}$$ (see [L10 Q20](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab20))|
|continuous|discrete|$$\displaystyle f_{X\lvert Y}(x\lvert y)=\frac{f_X(x)p_{Y\lvert X}(y\lvert x)}{\int_{-\infty}^\infty f_X(x)p_{Y\lvert X}(y\lvert x)dx}$$ (see [L10 Q22](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab22))|
|continuous|continuous|$$\displaystyle f_{X\lvert Y}(x\lvert y)=\frac{f_X(x)f_{Y\lvert X}(y\lvert x)}{\int_{-\infty}^\infty f_X(x)f_{Y\lvert X}(y\lvert x)dx}$$|

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

|Formula|Equivalent form|
|:-:|:-:|
|$$\displaystyle\int_a^b e^{-\lambda x}dx$$|$$\displaystyle\left[-\frac{1}{\lambda}e^{-\lambda x}\right]_a^b=\frac{1}{\lambda}(e^{-\lambda a}-e^{-\lambda b})$$|
|$$\displaystyle\sum_{k=1}^nk$$|$$\displaystyle\frac{k(k+1)(2k+1)}{6}$$|
|$$(X_1+\dots+X_n)^2$$|$$\displaystyle\underbrace{\sum_{i=1}^n X^2}_\text{$n$ terms}+\underbrace{\sum_{i\neq j}X_iX_j}_\text{$n^2-n$ terms}$$|