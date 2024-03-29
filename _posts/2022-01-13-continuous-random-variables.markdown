---
layout: post
title: "Continuous Random Variables"
---

$$\newcommand{\ind}{\perp\kern-5pt\perp}$$

## Definition

A r.v. $$X$$ is continuous if it can be described by a probability density function (PDF) $$f_X(x)$$, where $$f_X(x)\delta\simeq\mathbb P(x\le X\le x+\delta)$$ for an arbitraty small $$\delta>0$$. It follows that continuous r.v. [almost never](https://en.wikipedia.org/wiki/Almost_surely) takes an exact value $$x$$ (formally, $$\mathbb P(X=x)=0$$){% if jekyll.environment == "development" %} (see [Prob L8 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab3)){% endif %}; indeed, in such case the probability is associated with an interval where it could lie, $$\mathbb P(a\le X\le b)=\int_a^b f_X(x)dx$${% if jekyll.environment == "development" %} (see [Prob L8 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab5)){% endif %}. Analogously to [discrete r.v.](/2022/01/08/discrete-random-variables.html#definition), the basic axioms apply.

- $$f_X(x)>0$$, non-negativity
- $$\int_{-\infty}^\infty f_X(x)dx=1$$, normalization{% if jekyll.environment == "development" %} (see [Prob L8 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab7)){% endif %}

## Expectation {#expectation}

Definition does not change with respect to [discrete r.v.](/2022/01/08/discrete-random-variables.html#expectation), except that integral replaces sum. Hence, $$\mu_X=\mathbb E[X]=\int_{-\infty}^\infty xf_X(x)dx$$, with the same assumption that $$\int_{-\infty}^\infty\vert x\rvert f_X(x)dx\le\infty$$.

|Property|Formula|
|-|:-:|
|Bounds|$$a\le X\le b\implies a\le\mathbb E[X]\le b$$|
|Non negativity|$$X\ge0\implies\mathbb E[X]\ge0$$|
|Non negativity, with $$X\ge0$$|$$\displaystyle\mathbb E[X]=\int_{0}^\infty\mathbb P(X>k)dx$${% if jekyll.environment == "development" %} (see [Prob PS5 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab5)){% endif %}|
|[Law Of The Unconscious Statistician](https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician) (LOTUS)|$$\displaystyle\mathbb E[g(X)]=\int_{-\infty}^\infty g(x)f_X(x)dx$${% if jekyll.environment == "development" %} (see [Prob L8 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab10)){% endif %}|
|Linearity|$$E[aX+b]=a\mathbb E[X]+b$$|

## Variance

Exactly same definitions and properties of a [discrete r.v.](/2022/01/08/discrete-random-variables.html#variance).

## Basic continuous r.v. distributions {#basic}

|r.v.|PDF<br>$$f_X(x)$$|Expectation<br>$$\mu_X=\mathbb E[X]$$|Variance<br>$$\sigma_X^2=\text{var}(X)$$|
|-|:-:|:-:|:-:|:-:|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\displaystyle\frac{1}{b-a}$$<br>where $$a\le x\le b$$|$$\displaystyle\frac{b+a}{2}$$|$$\displaystyle\frac{1}{12}(b-a)^2$$|
|Triangular<br>$$\text{Tri}(a,b,c)$$|$$\begin{cases}\frac{2}{(c-a)}\frac{(x-a)}{(b-a)}&a\le x\le b\\\frac{2}{(c-a)}\frac{(c-x)}{(c-b)}&b\lt x\le c\\0&\text{otherwise}\end{cases}$$|$$\displaystyle\frac{a+b+c}{3}$${% if jekyll.environment == "development" %}<br>(see [Prob PS5 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab4)){% endif %}|$$\displaystyle\frac{\begin{align}a^2+b^2+c^2\\-ab-ac-bc\end{align}}{18}$$|
|Exponential<br>$$\text{Exp}(\lambda)$${% if jekyll.environment == "development" %}<br>(see [Prob F Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab2)){% endif %}|$$\lambda e^{-\lambda x}$$<br>where $$x\ge0$$|$$\displaystyle\frac{1}{\lambda}$$|$$\displaystyle\frac{1}{\lambda^2}$$|
|[Normal](/2022/01/13/continuous-random-variables.html#normal)<br>$$\mathcal N(\mu,\sigma^2)$$|$$\displaystyle\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac12\left(\frac{x-\mu}{\sigma}\right)^2}$$|$$\mu$$|$$\sigma^2$$|
|Erlang order $$k$$<br>$$\text{Erlang}(k,\lambda)$$|$$\displaystyle\frac{\lambda^k}{(k-1)!}x^{k-1}e^{-\lambda x}$$<br>where $$x\ge0$$|$$\displaystyle\frac k{\lambda}$$|$$\displaystyle\frac k{\lambda^2}$$|
|[Gamma](/2022/01/13/continuous-random-variables.html#gamma)<br>$$\text{Gamma}(\alpha,\beta)$$|$$\displaystyle\frac{\beta^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\beta x}$$<br>where $$x\ge0$$|$$\displaystyle\frac\alpha{\beta}$$|$$\displaystyle\frac\alpha{\beta^2}$$|
|Laplace<br>$$\text{Laplace}(\mu,\gamma)$$|$$\displaystyle\frac 1 {2\gamma}e^{-\left\lvert\frac{x-\mu}{\gamma}\right\rvert}$$|$$\mu$$|$$2\gamma^2$$|
|Cauchy<br>$$\text{Cauchy}(\mu,\gamma)$$|$$\displaystyle\frac 1{\pi\gamma}\left(1+\left(\frac{x-\mu}{\gamma}\right)^2\right)^{-1}$$|$$\infty$$|$$\infty$$|
|[$$\chi^2$$ order $$k$$](/2022/07/15/hypothesis-testing.html#chisq)<br>$$\displaystyle\text{Gamma}\left(\frac k2,\frac12\right)$$|$$\displaystyle\frac{\left(\frac12\right)^{\frac k2}}{\Gamma\left(\frac k2\right)}x^{\frac k2-1}e^{-\frac12x}$$<br>where $$x\ge0$$|$$k$$|$$2k$$|
|[Beta](/2023/03/13/bayesian-statistics.html#beta)<br>$$\text{Beta}(\alpha,\beta)$$|$$\displaystyle\frac1{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1}$$<br>where $$0\le x\le1$$|$$\displaystyle\frac\alpha{\alpha+\beta}$$|$$\displaystyle\frac{\alpha\beta}{(\alpha+\beta+1)(\alpha+\beta)^2}$$|
|[Dirichlet](/2023/03/13/bayesian-statistics.html#dirichlet)<br>$$\text{Dir}(\boldsymbol{\alpha})$$|$$\displaystyle\frac1{B(\boldsymbol{\alpha})}\prod_{j=1}^d x_j^{\alpha_j-1}$$<br>where $$\mathbf x\ge\mathbf0_d$$, $$\mathbf1_d^T\mathbf x=1$$|$$\displaystyle\frac{\boldsymbol{\alpha}}{\alpha_0}$$|$$\href{/2023/03/13/bayesian-statistics.html#dirichlet}{\Sigma_\mathbf X}$$|
|[Inverse Gamma](/2023/03/13/bayesian-statistics.html#invgamma)<br>$$\text{InvGamma}(\alpha,\beta)$$|$$\displaystyle\frac{\beta^\alpha}{\Gamma(\alpha)}x^{-(\alpha+1)}e^{-\frac\beta x}$$<br>where $$x\gt0$$|$$\displaystyle\frac\beta{\alpha-1}$$<br>for $$\alpha\gt1$$|$$\displaystyle\frac{\beta^2}{(\alpha-1)^2(\alpha-2)}$$<br>for $$\alpha\gt2$$|
|[Inverse $$\chi_k^2$$](/2023/03/13/bayesian-statistics.html#invgamma)<br>$$\text{InvGamma}(\frac k2,\frac12)$$|$$\displaystyle\frac{\left(\frac12\right)^{\frac k2}}{\Gamma\left(\frac k2\right)}x^{-(\frac k2+1)}e^{-\frac1{2x}}$$<br>where $$x\gt0$$|$$\displaystyle\frac1{k-2}$$<br>for $$k\gt2$$|$$\displaystyle\frac2{(k-2)^2(k-4)}$$<br>for $$k\gt4$$|

In case of Exponential, Erlang and Gamma distributions, $$\lambda$$ and $$\beta$$ are commonly referred to as *rate*, while their inverse is *scale*. At the same time $$k$$ and $$\alpha$$ for Erlang and Gamma distributions are commonly called *shape*. This nomenclature is consistent with Cauchy and Laplace distributions, where $$\gamma$$ is *shape* and $$\mu$$ is *location*.

Analogously to Pascal r.v., computing expectation and variance for Erlang r.v. is easier if we [assume](/2022/02/08/bernoulli-and-poisson-processes.html#kth_arrival) $$X=\sum_{i=1}^k X_i$$, with $$X_i\sim\text{Exp}(\lambda)$$, in which case $$\mathbb E[X]=k\mathbb E[X_i]$$ and $$\text{var}(X)=k\text{var}(X_i)$$. Also, Gamma distribution is an extension of Erlang distribution for $$k\in\mathbb R$$. Furthermore, $$\chi^2_n$$ distribution is a [special case](/2022/07/15/hypothesis-testing.html#chisq) of Gamma distribution. In the above summary, $$\Gamma(\alpha)$$ and $$B(\alpha,\beta)$$ refer to [Gamma](/2022/01/13/continuous-random-variables.html#gamma) and [Beta](/2023/03/13/bayesian-statistics.html#beta) functions, respectively.

Parameters $$\mu$$ and $$\gamma$$ of [Laplace](https://en.wikipedia.org/wiki/Laplace_distribution) and [Cauchy](https://en.wikipedia.org/wiki/Cauchy_distribution) distributions are often referred to as *location* and *scale*. Furthermore, where $$\text{Laplace}(0,1)$$ can be interpreted as a *double* $$\text{Exp}(1)$$ symmetric around the origin, $$\text{Cauchy}(0,1)$$ is equivalent to [$$t$$ distribution](/2022/07/15/hypothesis-testing.html#tdist) with $$n=1$$.

## Conditioning

Aside from replacing sums with integrals, the conditioning of continuous r.v. is exactly the same as with [discrete r.v.](/2022/01/08/discrete-random-variables.html#conditioning){% if jekyll.environment == "development" %} (see [Prob L9 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab3)){% endif %}.

Unless indicated otherwise, integrations in the table below are from $$-\infty$$ to $$\infty$$. Again, we assume that $$\mathbb P(A)>0$$, as well as $$f_Y(x)>0$$, otherwise the conditioning is not defined{% if jekyll.environment == "development" %} (see [Prob L10 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab3) and [Prob L10 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab7)){% endif %}.

|Property|Conditional on event $$A$$|Conditional on r.v. $$Y$$|
|-|:-:|:-:|
|PDF|$$\displaystyle f_{X\lvert A}(x)\delta\simeq\mathbb P(x\le X\le x+\delta\lvert A)$$<br>$$\displaystyle f_{X\lvert X\in A}(x)=\begin{cases}\frac{f_X(x)}{\mathbb P(A)}&\text{if $x\in A$}\\0&\text{otherwise}\end{cases}$$|$$\begin{gather}\displaystyle f_{X\lvert Y}(x\lvert y)\delta\simeq\\\mathbb P(x\le X\le x+\delta\lvert y\le Y\le y+\varepsilon)\end{gather}$$<br>$$f_{X\lvert Y}(x\lvert y)=\frac{f_{X,Y}(x,y)}{f_Y(y)}$${% if jekyll.environment == "development" %}<br>(see [Prob L10 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab5) and [Prob L10 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab13)){% endif %}|
|Normalization|$$\displaystyle\int f_{X\lvert A}(x)dx=1$$|$$\displaystyle\int f_{X\lvert Y}(x\lvert y)dx=1$$|
|Expectation|$$\displaystyle\mathbb E[X\lvert A]=\int x f_{X\lvert A}(x)dx$$|$$\displaystyle\mathbb E[X\lvert Y=y]=\int x f_{X\lvert Y}(x\lvert y)dx$$|
|LOTUS|$$\displaystyle\mathbb E[g(X)\lvert A]=\int g(x)f_{X\lvert A}(x)dx$${% if jekyll.environment == "development" %}<br>(see [Prob PS5 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab7)){% endif %}|$$\displaystyle\mathbb E[g(X)\lvert Y=y]=\int g(x)f_{X\lvert Y}(x\lvert y)dx$${% if jekyll.environment == "development" %}<br>(see [Prob PS5 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab3)){% endif %}|
|[Total probability](/2022/01/05/conditioning-and-independence.html#main_three_tools)|$$\displaystyle f_X(x)=\sum_{i=1}^n\mathbb P(A_i)f_{X\lvert A_i}(x)$$|$$\displaystyle f_X(x)=\int f_Y(y)f_{X\lvert Y}(x\lvert y)dy$${% if jekyll.environment == "development" %}<br>(see [Prob PS5 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab4)){% endif %}|
|Total expectation|$$\displaystyle\mathbb  E[X]=\sum_{i=1}^n\mathbb P(A_i)\mathbb E[X\lvert A_i]$${% if jekyll.environment == "development" %}<br>(see [Prob MT2 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch11-s1-tab5)){% endif %}|$$\displaystyle\mathbb E[X]=\int f_Y(y)\mathbb E[X\lvert Y=y]dy$$|

## Independence

Subject to customary adjustments, independence for continuous r.v. is the same as for [discrete r.v.](/2022/01/08/discrete-random-variables.html#independence), and relevant relationships can be derived if $$f_{X,Y}(x,y)=f_X(x)f_Y(y)$${% if jekyll.environment == "development" %} (see [Prob L10 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab9) and [Prob L10 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab10)){% endif %}.

## Memorylessness {#memorylessness}

Exponential distribution can be seen as a continuous analog of the geometric distribution, which also enjoys [memorylessness](/2022/01/08/discrete-random-variables.html#memorylessness). Bearing in mind that $$\mathbb P(X>x)=e^{-\lambda x}$$, and given that $$X>y$$ (with $$y<x$$), then we can prove that $$\mathbb P(X>x\lvert X>y)=\mathbb P(X>x-y)$$. This also means that the probability of success in the interval $$x+\delta$$, given that $$X>x$$, is $$\mathbb P(x\le X\le x+\delta\lvert X>x)\simeq\lambda\delta$${% if jekyll.environment == "development" %} (see [Prob L9 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab6)){% endif %}.

## Joint PDF

Again, once sums have been replaced with integrals, joint PDF have the same properties as [joint PMF](/2022/01/08/discrete-random-variables.html#joint_pmf){% if jekyll.environment == "development" %} (see [Prob PS5 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab4)){% endif %}, including derivation of *marginal* distributions from the *joint* distribution{% if jekyll.environment == "development" %} (see [Prob L9 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab15) and [Prob L9 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab17)){% endif %}. Bearing in mind that $$\mathbb P((X,Y)\in A)=\int_{(X,Y)\in A}f_{X,Y}(x,y)dxdy$$, one should notice that the order of integration is not essential{% if jekyll.environment == "development" %} (see [Prob L9 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab13)){% endif %}.

It is important that the r.v. are jointly continuous, to be described by a joint PDF. Consider $$X$$ and $$Y$$ and assume that the entire probability is concentrated on a curve described by the two r.v. laying on the $$X-Y$$ plane. In this case, the two r.v. are **not** jointly continuous, because the entire probability is concentrated on top of that curve, which conflicts with the requirement that the relevant probability is associated with an area/volume{% if jekyll.environment == "development" %} (see [Prob L9 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab11)){% endif %}.

If you are having difficulties picturing it, think of one dimensional analogy where $$X\sim\mathcal N(c,0)$$. This means that all probability is concentrated in a single point and is incompatible with the definition of a continuous r.v. (it can be a discrete r.v., though).

## Mixed distributions

A mixed r.v. $$Z$$ can be conveniently seen as a combination of discrete r.v. $$X$$ and continuous r.v. $$Y$${% if jekyll.environment == "development" %} (see [Prob L9 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab8)){% endif %}. In this case $$\mathbb E[Z]=p\mathbb E[X]+(1-p)\mathbb E[Y]$${% if jekyll.environment == "development" %} (see [Prob L9 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab10)){% endif %}, where $$Z$$ is defined as:

$$Z=\begin{cases}X&\text{with probability $p$}\\Y&\text{with probability $(1-p)$}\end{cases}$$

## Cumulative distribution function {#cdf}

Probability that $$X$$ will take a value less than $$x$$ is defined as cumulative distribution function (CDF), or $$F_X(x)=\mathbb P(X\le x)$$. Note that CDF does not distinguish if $$X$$ is discrete or continuous (or mixed), and applies analogously except that with discrete r.v. it is calculated as $$F_X(x)=\sum_{k\le x}p_X(x)$$, while in the case of continuous r.v. we use $$F_X(x)=\int_{-\infty}^x f_X(x)dx$$. The latter clearly expresses that $$f_X(x)=\frac{\partial}{\partial x}F_X(x)$${% if jekyll.environment == "development" %} (see [Prob L8 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab12), [Prob PS5 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab2) and [Stats L16 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab2)){% endif %}.

|Property|Formula|
|-|:-:|
|Non decreasing|$$a\le b\implies F_X(a)\le F_X(b)$$|
|Equivalency|$$\mathbb P(a\le X\le b)=F_X(b)-F_X(a)$$|
|Bounds|$$\displaystyle\lim_{x\rightarrow-\infty} F_X(x)=0,\lim_{x\rightarrow\infty} F_X(x)=1$$|

CDF of a joint PDF is $$F_{X,Y}(x,y)=\mathbb P(X\le x, Y\le y)$$, where $$f_{X,Y}(x,y)=\frac{\partial^2}{\partial x\partial y}F_{X,Y}(x,y)$$. Thus, $$X\ind Y\iff F_{X,Y}(x,y)=F_X(x)F_Y(y)$${% if jekyll.environment == "development" %} (see [Prob L10 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab11)){% endif %}. If $$\mathbb P(X\lt a)=\mathbb P(Y\lt b)=0$$ then the CDF along those *lower* boundaries is zero $$F_{X,Y}(a,y)=F_{X,Y}(x,b)=0$$, due to continuity{% if jekyll.environment == "development" %} (see [Prob L9 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__9_Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s3-tab19)){% endif %}.

Under respective back-up sections, you will find CDF of the basic r.v. [discrete](/2022/01/08/discrete-random-variables.html#cdf) and [continuous](/2022/01/13/continuous-random-variables.html#basic) distributions.

## Normal distribution {#normal}

$$X$$ is a Normal r.v. with mean $$\mu_X$$ and variance $$\sigma_X^2$$ if $$X\sim\mathcal N(\mu_X,\sigma_X^2)$$. Even though $$\sigma^2_X=0$$ is permitted, it would turn $$X$$ into a [discrete r.v.](/2022/01/08/discrete-random-variables.html#basic){% if jekyll.environment == "development" %} (see [Prob L8 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab14)){% endif %}. Normal r.v. has a long list of properties, including:

- **invariant under affine transformations**, which means that $$Y=aX+b$$ is also Normal, $$Y\sim\mathcal N(a\mu_X+b, a^2\sigma_X^2)$$ (refer to [derived distributions](/2022/01/24/further-topics-on-RV.html#derived_distributions) for details){% if jekyll.environment == "development" %} (see [Prob PS5 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab1) and [Stats L2 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab4)){% endif %};
- **standardization / normalization / z-score**, as a direct consequence of the above, it means that any $$X$$ can be expressed in terms of $$Z\sim\mathcal N(0,1)$$ (commonly referred to as the *standard* Normal) and vice-versa, e.g. $$Z=\frac{X-\mu_X}{\sigma_X}$$; and
- **symmetry** around its mean, which also corresponds to its median and mode. This property, together with standardization, simplifies computation of CDF, using the **Normal tables** as the Normal CDF does not have a closed form solution. Once $$X$$ has been normalized, we use the tables to compute $$F_X(x)$$ as $$\Phi(\frac{x-\mu_X}{\sigma_X})$$, where $$\Phi(z)=F_Z(z)$$. Often, Normal tables are provided in the form of $$\Phi(q)=\mathbb P(z\le q), q>0$$, where other forms can be derived thanks to symmetry.

|Formula|Equivalent form|
|:-:|:-:|
|$$\mathbb P(Z\le q)$$|$$\Phi(q)$${% if jekyll.environment == "development" %} (see [Prob L8 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__8_Probability_density_functions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s2-tab16)){% endif %}|
|$$\mathbb P(Z\le -q)$$|$$1-\Phi(q)$$|
|$$\mathbb P(Z\ge q)$$|$$1-\Phi(q)$$|
|$$\mathbb P(Z\ge -q)$$|$$\Phi(q)$${% if jekyll.environment == "development" %} (see [Stats L2 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab5) and [Stats HW0 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab3)){% endif %}|
|$$\mathbb P(a\le Z\le b)$$|$$\Phi(b)-\Phi(a)$$|
|$$\mathbb P(\lvert Z\rvert\le q)$$|$$2\Phi(q)-1$$|
|$$\mathbb P(\lvert Z\rvert\ge q)$$|$$2(1-\Phi(q))$$|

In the above examples, $$q$$ is the quantile. Often, we use quantile of order $$1-\alpha$$, denoted $$q_\alpha$$, that indicates the number (specific to each underlying r.v. $$X$$) s.t. $$\mathbb P(X\le q_\alpha)=1-\alpha$${% if jekyll.environment == "development" %} (see [Stats L2 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab6)){% endif %}.

If $$X_i\overset{\text{i.i.d.}}{\sim}\mathcal N(\mu_X,\sigma_X^2)$$, their joint probability $$f_{X_1,\dots X_n}(x_1,\dots,x_2)$$ is as follows{% if jekyll.environment == "development" %} (see [Prob L10 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab15)){% endif %}.

$$\prod_{i=1}^n f_X(x)=\frac{1}{\sqrt{(2\pi\sigma_X^2)^n}}e^{-\frac12\sum_{i=1}^n\left(\frac{x_i-\mu_X}{\sigma_X}\right)^2}$$

Higher moments of a standard Normal are $$\mathbb E[Z^k]=(k-1)\mathbb E[Z^{k-2}]$$. Since $$\mathbb E[Z]=0$$, it follows that for *odd* $$k$$ we have $$\mathbb E[Z^k]=0$$, and for *even* $$k$$ we get $$\mathbb E[Z^k]=\prod_{i=1}^{k/2}(2i-1)$$ (that is a product of the first $$\frac{k}{2}$$ odd numbers){% if jekyll.environment == "development" %} (see [Stats HW0 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab3)){% endif %}. This result comes from the following observation.

$$\begin{align}
\mathbb E[Z^k]&=\int_{-\infty}^\infty z^k f_Z(z)dz=\int_{-\infty}^\infty (-z^{k-1})\overbrace{(-z) f_Z(z)}^{=\frac\partial{\partial z}f_Z(z)}dz\\
&=\cancelto{=0}{[f_Z(z)(-z^{k-1})]_{-\infty}^\infty}+\int_{-\infty}^\infty (k-1)z^{k-2} f_Z(z)dz=(k-1)\mathbb E[Z^{k-2}]
\end{align}$$

In the above, $$Z\sim\mathcal N(0,1)$$ and therefore $$f_Z(z)=\frac 1{\sqrt{2\pi}}\exp\{-\frac {z^2} 2\}$$.

Prior to concluding, note that **any PDF describing a negative exponential of a quadratic function of x is always a Normal PDF**. Consider $$f_X(x)=c\cdot e^{-(\alpha x^2+\beta x+\gamma)}$$ and observe that it has its peak where $$\frac\partial{\partial x}\ln f_X(x)=2\alpha x+\beta=0$$. As the PDF is symmetric, the peak corresponds to expectation and therefore $$\mu_X=-\frac\beta{2\alpha}$$. Furthermore, as $$\alpha$$ has to be equal to $$\frac1{2\sigma_X^2}$$, it follows that $$\sigma_X^2=\frac1{2\alpha}$${% if jekyll.environment == "development" %} (see [Prob L15 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab3)){% endif %}.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

|Formula|Equivalent form|
|:-:|:-:|
|$$\displaystyle\int_a^b f'(x)g(x)dx$$|$$\displaystyle\left[f(x)g(x)\right]_a^b-\int_a^b f(x)g'(x)dx$$|
|$$\displaystyle\int_a^b e^{-\lambda x}dx$$|$$\displaystyle\left[-\frac{1}{\lambda}e^{-\lambda x}\right]_a^b=\frac{1}{\lambda}(e^{-\lambda a}-e^{-\lambda b})$$|
|$$\displaystyle\int_{-\infty}^\infty e^{-ax^2}dx$$|$$\displaystyle\sqrt{\frac\pi a}$$|
|$$\displaystyle\int_0^\infty x^{\alpha-1}e^{-x}dx$$|$$\Gamma(\alpha)$$, where $$\Gamma(\alpha)=(\alpha-1)!$$ if $$\alpha\in\mathbb Z_+$$|
|$$\displaystyle\int_0^\infty x^{\alpha-1}e^{-\beta x}dx$$|$$\displaystyle\frac{\Gamma(\alpha)}{\beta^\alpha}$$|
|![pdf](/assets/images/2022-01-13-continuous-random-variables/pdf.png)<br>PDF|![cdf](/assets/images/2022-01-13-continuous-random-variables/cdf.png)<br>CDF|

### CDF of basic continuous r.v. {#cdf_continuous}

|r.v.|CDF<br>$$F_X(x)$$|
|-|:-:|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\begin{cases}0&x\lt a\\\displaystyle\frac{x-a}{b-a}&a\le x\lt b\\1& x\ge b\end{cases}$$|
|Triangular<br>$$\text{Tri}(a,b,c)$$||
|Exponential<br>$$\text{Exp}(\lambda)$$|$$\begin{cases}0&x\lt 0\\1-e^{\lambda x}& x\ge 0\end{cases}$${% if jekyll.environment == "development" %}<br>(see [Stats HW0 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab5)){% endif %}|
|Erlang<br>$$\text{Erlang}(k,\lambda)$$|$$\begin{cases}0&x\lt 0\\\displaystyle\int_{0}^x e^{-\lambda s}\frac{\lambda(\lambda s)^{k-1}}{(k-1)!}ds=1-e^{-\lambda x}\sum_{n=0}^{k-1}\frac{(\lambda x)^n}{n!}& x\ge 0\end{cases}$$|

### Gamma distribution and gamma function {#gamma}

Although Erlang distribution assumes $$k$$ being a positive integer, it is possible generalizing it for $$k\gt0$$. This generalization is referred to as **Gamma** distribution and when $$\alpha$$ is a positive integer, the PDF of $$X\sim\text{Gamma}(\alpha,\beta)$$, $$f_X(x)=\frac{\beta^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\beta x}$$, is the same as the PDF of $$X\sim\text{Erlang}(\alpha,\beta)$$, where the term $$\Gamma(\alpha)$$ is a [smooth curve](https://en.wikipedia.org/wiki/Gamma_function#Motivation) equal to $$(\alpha-1)!$$, when $$\alpha$$ is a positive integer number.

$$\Gamma(\alpha)=\int_0^\infty e^{-z}z^{\alpha-1}dz$$

One observes that $$\Gamma(\alpha)=\cancelto{=0}{[-e^{-z}z^{\alpha-1}]_0^\infty}+(\alpha-1)\int_0^\infty e^{-z}z^{\alpha-2}dz=(\alpha-1)\Gamma(\alpha-1)$$. As $$\Gamma(1)=1$$, it follows that $$\Gamma(\alpha)=(\alpha-1)(\alpha-2)\dots 1=(\alpha-1)!$$ for any integer and positive $$\alpha$$.

At this point, expectation and variance of a Gamma distribution are immediately derived, as they are the same as erlang, by simply replacing $$\alpha=k$$ and $$\beta=\lambda$$. $$\mathbb E[X]=\frac\alpha\beta$$, $$\text{var}(X)=\frac\alpha{\beta^2}$$. As for the mode, observe that the first derivative is equal to zero if $$x=0$$ for $$\alpha\lt1$$ and $$x=\frac{\alpha-1}\beta$$ for $$\alpha\ge1$$.

$$\frac\partial{\partial x}f_X(x)\propto x^{\alpha-1}e^{-\beta x}\left(\frac{\alpha-1}x-\beta\right)$$

The most notable value at a non-integer argument is $$\Gamma\left(\frac 1 2\right)=\sqrt\pi$$ (see [$$\chi^2$$ distribution](/2022/07/15/hypothesis-testing.html#chisq)). First notice the following.

$$\begin{align}
\Gamma\left(\frac 1 2\right)
&=\int_0^\infty e^{-z}z^{-\frac 1 2}dz&(z=x^2)\\
&=2\int_0^\infty e^{-x^2}dx=\int_{-\infty}^\infty e^{-x^2}dx&\text{($e^{-x^2}$ is an $\href{https://en.wikipedia.org/wiki/Even_and_odd_functions#Analytic_properties}{\text{even}}$ function)}
\end{align}$$

Now, consider the square of the above, and in particular observe that $$\Gamma^2\left(\frac 1 2\right)=\pi$$.

$$\begin{align}
\Gamma^2\left(\frac 1 2\right)=\left(\int_{-\infty}^\infty e^{-x^2}dx\right)^2
&=\int_{-\infty}^\infty e^{-x^2}dx\int_{-\infty}^\infty e^{-y^2}dy\\
&=\int_{-\infty}^\infty\int_{-\infty}^\infty e^{-(x^2+y^2)}dxdy&\text{(polar coordinates)}\\
&=\int_0^\infty\left(\int_0^{2\pi}e^{-r^2}rd\theta\right)dr&\text{(integrate w.r.t. $d\theta$)}\\
&=\int_0^\infty e^{-r^2}(2\pi)rdr&\text{(replace $r^2=t$)}\\
&=\pi\int_0^\infty e^{-t}dt=\pi
\end{align}$$

Accordingly, $$\displaystyle\int_{-\infty}^\infty e^{-x^2}dx=\sqrt\pi$$, and in particular $$\displaystyle\int_{-\infty}^\infty e^{-az^2}dz=\frac1{\sqrt{a}}\int_{-\infty}^\infty e^{-x^2}dx=\sqrt{\frac\pi a}$$, which is useful to prove $$\displaystyle\int_{-\infty}^\infty e^{-\frac1{2\sigma^2}z^2}dz=\sqrt{2\pi\sigma^2}$$, being the normalization factor for $$X\sim\mathcal N(\mu,\sigma^2)$$.
