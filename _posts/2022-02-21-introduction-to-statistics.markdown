---
layout: post
title: "Introduction to statistics"
---

## Motivation

Statistics, Data Science, Machine Learning and Artificial Intelligence, they all use data to get insight and ultimately make decisions. Statistics is at the core of the data processing part, where data comes from a random process.

Accordingly, where **probability** studies randomness (a way of modeling lack of information) of a phenomenon{% if jekyll.environment == "development" %} (see [Stats L1 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s1_whatisstats/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s1_whatisstats-tab5), [Stats L1 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s1_whatisstats/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s1_whatisstats-tab8) and [Stats L1 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s1_whatisstats/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s1_whatisstats-tab9)){% endif %}, which may be completely known (e.g. tossing a coin), **statistics** focuses on processes where parameters are not known and need to be estimated from data{% if jekyll.environment == "development" %} (see [Stats L1 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s1_whatisstats/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s1_whatisstats-tab6)){% endif %}.

<p align="center">
  <img src="/assets/images/2022-02-21-introduction-to-statistics/27748.png"/>
</p>



## Basic inequalities {#basic}

Fundamental results in statistics are derived from certain inequalities, which attempt to explain probabilities of "*extreme events*", using only a bit of information about the underlying distribution (usually expectation and variance).

From the intuition that "*if $$X\ge0$$ and $$\mathbb E[X]$$ is small, then $$X$$ is unlikely to be large*", we derive the **Markov's inequality** which can be derived from observing that $$\mathbb E[X]\ge\int_{\varepsilon}^\infty\varepsilon f_X(x)dx$$.

$$\mathbb P(X\ge\varepsilon)\le\frac{\mathbb E[X]}{\varepsilon},\varepsilon>0$$

In the relation above, $$X$$ indicates *any* r.v. Hence, if $$g(X)$$ is another, non-negative r.v., an analogous relation can be derived in terms of $$\mathbb E[g(X)]$${% if jekyll.environment == "development" %} (see [Prob L18 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__18_Inequalities__convergence__and_the_Weak_Law_of_Large_Numbers/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s2-tab3)){% endif %}.

Another intuition, "*if the variance is small, then $$X$$ is unlikely to be far from the mean*", leads us to the **Chebyshev's inequality**, obtained from replacing $$X=(Y-\mathbb E[Y])^2$$ in the Markov's inequality{% if jekyll.environment == "development" %} (see [Prob L18 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__18_Inequalities__convergence__and_the_Weak_Law_of_Large_Numbers/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s2-tab5) and [Prob PS8 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab3)){% endif %}.

$$\mathbb P(\lvert Y-\mathbb E[Y]\lvert\ge\varepsilon)\le\frac{\text{var}(Y)}{\varepsilon^2}$$

One may be tempted to think that Chebyshev's inequality is *always* tighter than Markov's inequality; but this is not true{% if jekyll.environment == "development" %} (see [Prob L18 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__18_Inequalities__convergence__and_the_Weak_Law_of_Large_Numbers/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s2-tab6)){% endif %} and one should evaluate on a case-by-case basis. In general, Markov's and Chebyshev's inequalities are too conservative, but are important to prove other claims, including derivation of significantly tigher (exponentially decaying) inequalities.

Finally, let $$f(\cdot)$$ be a [convex](https://en.wikipedia.org/wiki/Convex_function) and [differentiable](https://en.wikipedia.org/wiki/Differentiable_function) function. Accordingly, for any $$c\in\mathbb R$$ constant, we have that $$f(x)\ge f(c)+f'(c)(x-c)$$. If we replace $$x=X$$, $$c=\mathbb E[X]$$, and apply expectation on both sides of inequality, we obtain the **Jensen's inequality**.

$$\mathbb E[f(X)]\ge f(\mathbb E[X])+\cancelto{=0}{f'(\mathbb E[X])(\mathbb E[X]-\mathbb E[X])}$$

Common derivations of the Jensen's inequality include $$\mathbb E[X^{2k}]\ge(\mathbb E[X])^{2k}$$ (where $$k=1,2,\dots$$), $$\mathbb E[-\ln(X)]\ge-\ln(\mathbb E[X])$$ and $$\mathbb E[e^X]\ge e^{\mathbb E[X]}$$.

## Exponentially decaying inequalities

Let $$S_n=\sum_{i=1}^n X_i$$, where $$X_i\overset{i.i.d.}{\sim}\mathcal P$$, $$\mathbb E[X_i]=0$$ and $$\text{var}(X_i)=\sigma_X^2$$. To compute $$\mathbb P(S_n\ge n\varepsilon)$$, one option is using Chebyshev's inequality, which yields $$\mathbb P(S_n\ge n\varepsilon)\le\frac{\sigma^2}{n\varepsilon^2}$$, or Markov's inequality, which brings us to $$\mathbb P(S_n\ge n\varepsilon)=\mathbb P(e^{tS_n}\ge e^{tn\varepsilon})\le\frac{\mathbb E[e^{tS_n}]}{e^{tn\varepsilon}}$$, where the exponential function is used to ensure that the r.v. stays always positive. Next, bearing in mind that $$\mathbb E[e^{tS_n}]=(\mathbb E[e^{tX_i}])^n$$, we compute as follows.

$$\mathbb P(S_n\ge n\varepsilon)\le\left(\frac{\mathbb E[e^{tX_i}]}{e^{t\varepsilon}}\right)^n=e^{nh(\varepsilon)}$$

Note that $$h(\varepsilon)=\ln\left(\mathbb E[e^{tX_i}]\right)-t\varepsilon\lt0$$ for $$\mathbb E[X_i]=0$$ and a suitably small $$t\gt0$$, which means that the probability decays exponentially with $$n$$ and this general result is known as **Chernoff's bound**.

A special case is obtained thanks to the [Hoeffding's lemma](https://en.wikipedia.org/wiki/Hoeffding%27s_inequality) that says that when $$X_i\in[a,b]$$ a.s., then $$\mathbb E[e^{tX_i}]\le e^{\frac{1}{8}t^2(b-a)^2}$$ (see [back-up](/2022/02/21/introduction-to-statistics.html#hoeffding_lemma)). This means that $$h(\varepsilon)\le\frac{1}{8}t^2(a-b)^2-t\varepsilon$$, with an upper bound at $$t=\frac{4\varepsilon^2}{(b-a)^2}$$. Accordingly, $$\mathbb P(S_n\ge n\varepsilon)\le e^{-\frac{2n\varepsilon^2}{(b-a)^2}}$$.

Last manipulation is to replace $$S_n$$ with $$S_n-\mathbb E[S_n]$$, so that we do not need to assume $$\mathbb E[X_i]=0$$ anymore, and  divide both hand sides within the probability by $$n$$ to obtain the **Hoeffding's inequality**{% if jekyll.environment == "development" %} (see [Stats L2 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab3)){% endif %}, which holds for any $$n\ge1$$.

$$\displaystyle\mathbb P(\lvert\bar X_n-\mathbb E[\bar X_n]\rvert\ge\varepsilon)\le2e^{-\frac{2n\varepsilon^2}{(b-a)^2}}$$

Observe that not necessarily Hoeffding's inequality is tighter than Chebyshev's inequality, especially for small $$n$${% if jekyll.environment == "development" %} (see [Stats L2 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab3)){% endif %}.

## Weak Law of Large Numbers {#wlln}

According to the weak law of large numbers (WLLN) states that the sample mean $$\bar X_n=\frac{1}{n}\sum_{i=1}^n X_i$$ (where $$X_i\overset{i.i.d.}{\sim}\mathcal P$$, with finite $$\mu=E[X_i]$$ and $$\sigma^2=\text{var}(X_i)$$) converges in probability to the true mean, or $$\bar X_n\xrightarrow[n\rightarrow\infty]{\mathbb P}\mathbb E[X_i]$$. To prove, one computes $$\mathbb E[\bar X_n]=\mu$$, $$\text{var}(\bar X_n)=\frac{\sigma^2}{n}$$, and plugs them into the Chebyshev's inequality to obtain as follows{% if jekyll.environment == "development" %} (see [Prob L18 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__18_Inequalities__convergence__and_the_Weak_Law_of_Large_Numbers/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s2-tab8)){% endif %}.

$$\lim_{n\rightarrow\infty}\mathbb P(\lvert\bar X_n-\mu\rvert\ge\varepsilon)\le\frac{\sigma^2}{n\varepsilon^2}=0$$

Worth mentioning that according to the strong law of large numbers (SLLN), convergence of the sample mean holds even under a stronger notion of convergence, known as convergence almost surely (or with certain probability), or $$\mathbb P(\lim_{n\rightarrow\infty}\bar X_n=\mu)=1$${% if jekyll.environment == "development" %} (see [Stats L2 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab7)){% endif %}.

## Types of convergences {#types_of_convergences}

Denoting $$T_n$$ a sequence of r.v. and $$T$$ a r.v. (which can also be deterministic), we define the following three convergences.

|Convergence|Notation|Requirement|
|-|:-:|:-:|
|**Almost surely**|$$\displaystyle T_n\xrightarrow[n\rightarrow\infty]{a.s.}T$$|$$\mathbb P(\{\omega:T_n(\omega)\xrightarrow[n\rightarrow\infty]{}T(\omega)\})=1$$|
|**In probability**|$$\displaystyle T_n\xrightarrow[n\rightarrow\infty]{\mathbb P}T$$|$$\mathbb P(\lvert T_n-T\rvert\ge\varepsilon)\xrightarrow[n\rightarrow\infty]{}0,\forall\varepsilon\gt0$${% if jekyll.environment == "development" %}<br>(see [Prob PS8 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab1)){% endif %}|
|**In distribution**|$$\displaystyle T_n\xrightarrow[n\rightarrow\infty]{(d)}T$$|$$\mathbb E[f(T_n)]\xrightarrow[n\rightarrow\infty]{}\mathbb E[f(T)],\forall f$$ continuous and bounded<br>or, equivalently<br>$$F_{T_n}(x)\xrightarrow[n\rightarrow\infty]{}F_T(x)$$, $$\forall x$$ at which $$F_T(x)$$ is continuous|
|**In $$L^r$$ norm**|$$T_n\xrightarrow[n\rightarrow\infty]{L^r}$$|$$\displaystyle\lim_{n\rightarrow\infty}\mathbb E[\lvert T_n-T\rvert^r]=0$$|

For ease of notation, note that $$T_n\xrightarrow[n\rightarrow\infty]{a.s./\mathbb P/(d)/L^r}T$$ may also be written as $$T_n\xrightarrow{a.s./\mathbb P/(d)/L^r}T$$. Follows an overview of mutual implications.

$$\begin{align}
T_n\xrightarrow{L^{s>r}}T\implies T_n&\xrightarrow{L^{r\ge1}}T\\
&\Downarrow\\
T_n\xrightarrow{a.s.}T\implies T_n&\xrightarrow{\mathbb P}T\implies T_n\xrightarrow{(d)}T
\end{align}$$

Difference between "*almost surely convergence*" and "*convergence in probability*" is subtle, and is not supposed to be obvious. Eventually, one could refer to a different order of appearance among the limit and probability. Think of the sample mean and rearrange the above requirements as follows.

$$\begin{cases}WLLN:&\displaystyle{\color{red}\lim_{n\rightarrow\infty}}\mathbb P(\lvert\bar X_n-\mu_X\rvert\le\varepsilon)=1\\SLLN:&\displaystyle\mathbb P({\color{red}\lim_{n\rightarrow\infty}}\lvert\bar X_n-\mu_X\rvert=0)=1\end{cases}$$

As we increase $$n$$: (a) the sample mean $$\bar X_n$$ *concentrates* arbitrarily close around the true mean $$\mu$$ in the WLLN; and (b) with certainty, the difference between the two vanishes in the SLLN.

Convergence in $$L^r$$ norm for any $$r\ge1$$ implies $$T_n\xrightarrow{\mathbb P}T$$, as $$\mathbb P(\lvert T_n-T\rvert\ge\varepsilon)\le\frac{\mathbb E[\lvert T_n-T\rvert]}{\varepsilon}\rightarrow0$$. So, $$\mathbb E[T_n]\rightarrow t$$ implies that $$T_n\xrightarrow{\mathbb P}t$$; the converse, however, **is not necessarily true**{% if jekyll.environment == "development" %} (see [Stats L2 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab7)){% endif %}.

## Convergence properties {#properties}

According to the [continuous mapping theorem](https://en.wikipedia.org/wiki/Continuous_mapping_theorem) (CMT), for $$X_n\xrightarrow{a.s./\mathbb P/(d)}X$$ and a continuous $$f(\cdot)$$, we have that $$f(X_n)\xrightarrow{a.s./\mathbb P/(d)}f(X)$$. Note that CMT can be proved even when $$X_n$$ and $$X$$ are vectors.

In particular, if we consider a random vector $$(X_n,Y_n)\xrightarrow{a.s./\mathbb P}(X,Y)$$, and a continuous function $$f(X_n,Y_n)$$, we can derive the following relationships{% if jekyll.environment == "development" %} (see [Stats L2 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab8)){% endif %}.

|$$f(\cdot)$$|Property|
|:-:|:-:|
|Addition|$$X_n+Y_n\xrightarrow{a.s./\mathbb P}X+Y$$|
|Multiplication|$$X_nY_n\xrightarrow{a.s./\mathbb P}XY$$|
|Division|$$\displaystyle\frac{X_n}{Y_n}\xrightarrow{a.s./\mathbb P}\frac X Y$$, if $$Y_n\neq0$$|

Some partial results can also apply for convergence in distribution. Thanks to [Slutsky's theorem](https://en.wikipedia.org/wiki/Slutsky%27s_theorem), we have that if $$X_n\xrightarrow{(d)}X$$ and $$Y_n\xrightarrow{a.s./\mathbb P}y$$, where $$y\in\mathbb R$$, then $$(X_n,Y_n)\xrightarrow{(d)}(X,y)$$. Next we apply CMT, again relying on a continuous $$f(\cdot)$${% if jekyll.environment == "development" %} (see [Stats HW1 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw1_u1intro/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw1_u1intro-tab7)){% endif %}.

|$$f(\cdot)$$|Property|
|:-:|:-:|
|Addition|$$X_n+Y_n\xrightarrow{(d)}X+y$$|
|Multiplication|$$X_nY_n\xrightarrow{(d)}Xy$$|
|Division|$$\displaystyle\frac{X_n}{Y_n}\xrightarrow{(d)}\frac X y$$, if $$y\neq 0$$|

## Central Limit Theorem {#clt}

The Central Limit Theorem (CLT) states that sum of i.i.d. r.v. tends towards a [Normal](/2022/01/13/continuous-random-variables.html#normal) distribution, as the sample size gets larger and regardless of the population's distribution. The remarkable thing is that not only this convergence (in distribution) is irrespective of the underlying distribution, but also that the sample size can be *moderate* (e.g. above 30), especially when the underlying distribution is unimodal and symmetric.

Formally, the CLT states that if $$X_i\overset{i.i.d.}{\sim}\mathcal P$$, with $$\mu_X=\mathbb E[X_i]$$ and $$\sigma_X^2=\text{var}(X_i)$$, then for the sum $$S_n=\sum_{i=1}^n X_i$$ we have that $$S_n\xrightarrow{(d)}\mathcal N(n\mu_X,n\sigma_X^2)$$, or $$Z_n=\frac{S_n-n\mu_X}{\sqrt n\sigma_X}\xrightarrow{(d)}\mathcal N(0,1)$${% if jekyll.environment == "development" %} (see [Prob L19 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__19_The_Central_Limit_Theorem__CLT_/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s3-tab3) and [Prob PS9 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab2)){% endif %}. This approximation allows us performing the following queries{% if jekyll.environment == "development" %} (see [Prob PS9 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab3)){% endif %}.

|Query|Application|
|-|:-:|
|Find $$\mathbb P(S_n\le a)$$|$$\Phi\left(\frac{a-n\mu_X}{\sqrt n\sigma}\right)$$|
|Find $${\color{red} a}$$ s.t. $$\mathbb P(S_n\le{\color{red}a})=b$$|$$\displaystyle\frac{ {\color{red}a}-n\mu_X}{\sqrt n\sigma}=\Phi^{-1}(b)$$|
|Find $${\color{red} n}$$ s.t. $$\mathbb P(S_{\color{red}n}\le a)=b$$|$$\displaystyle\frac{a-{\color{red} n}\mu_X}{\sqrt{\color{red} n}\sigma}=\Phi^{-1}(b)$${% if jekyll.environment == "development" %}<br>(see [Prob PS8 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab4)){% endif %}|

An additional application is estimating the probability that a sum of $$n$$ copies of $$X_i$$ stays below given $$a$$. This problem is very similar to describing the probability of $$k$$-th [arrival](/2022/02/08/bernoulli-and-poisson-processes.html#kth_arrival) and is formulated as follows.

Assume $$N$$ is a r.v. describing the first value for which $$S_N$$ **exceeds** $$a$$. At the same time, $$N-1$$ is a r.v. describing the last value for which $$S_{N-1}$$ is **below** $$a$$. Observing that $$\mathbb P(N>n)=\mathbb P(N-1\ge n)$$ we can exploit the arrivals equivalent formulation and derive $$\mathbb P(N>n)=\mathbb P(S_n\le a)$${% if jekyll.environment == "development" %} (see [Prob L19 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__19_The_Central_Limit_Theorem__CLT_/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s3-tab8)){% endif %}.

## CLT and the sample mean {#clt_mean}

Sample mean is a *consistent* estimator of the expectation ([WLLN](/2022/02/21/introduction-to-statistics.html#wlln)) and we know its distribution ([CLT](/2022/02/21/introduction-to-statistics.html#clt)). In particular, $$\bar X_n\xrightarrow{(d)}\mathcal N(\mu_X,\frac{\sigma_X^2}{n})$${% if jekyll.environment == "development" %} (see [Stats L2 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab2)){% endif %} can be conveniently rewritten in the following two equivalent forms, thanks to standardization{% if jekyll.environment == "development" %} (see [Stats L2 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s2_probredux/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s2_probredux-tab5)){% endif %}.

$$\begin{align}
\sqrt{n}(\bar X_n-\mu_X)&\xrightarrow{(d)}\mathcal N(0,\sigma_X^2)\\
\sqrt{n}\frac{(\bar X_n-\mu_X)}{\sigma_X}&\xrightarrow{(d)}\mathcal N(0,1)
\end{align}$$

## Multivariate CLT {#multivariate_clt}

In case of a [random vector](/2022/01/24/further-topics-on-RV.html#covariance_matrix) $$\mathbf X$$, such that $$\boldsymbol\mu_\mathbf X=\mathbb E[\mathbf X]$$ and $$\boldsymbol\Sigma_\mathbf X=\text{cov}(\mathbf X)$$, [WLLT](/2022/02/21/introduction-to-statistics.html#wlln) and [CLT](/2022/02/21/introduction-to-statistics.html#clt) can be generalized to a vector of averages $$\bar{\mathbf X}_n$$ as follows{% if jekyll.environment == "development" %} (see [Stats L10 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab10)){% endif %}.

$$\begin{align}
\bar{\mathbf X}_n&\xrightarrow{\mathbb P}\boldsymbol\mu_\mathbf X&\href{/2022/02/21/introduction-to-statistics.html#wlln}{\text{(WLLN)}}\\
\sqrt{n}(\bar{\mathbf X}_n-\boldsymbol\mu_{\mathbf X})&\xrightarrow{(d)}\mathcal N_d(\mathbf 0,\boldsymbol\Sigma_{\mathbf X})&\href{/2022/02/21/introduction-to-statistics.html#clt}{\text{(CLT)}}\\
\sqrt{n}\boldsymbol\Sigma_{\mathbf X}^{-\frac 1 2}(\bar{\mathbf X}_n-\boldsymbol\mu_{\mathbf X})&\xrightarrow{(d)}\mathcal N_d(\mathbf 0,\mathbf I_d)
\end{align}$$

## CLT and the binomial approximation {#clt_binomial}

Taking into account that $$S_n\sim\text{Bin}(n,p)$$ is equivalent to $$S_n=\sum_{i=0}^n X_i$$, where $$X_i\overset{i.i.d.}{\sim}\text{Ber}(p)$$, one observes that $$\frac{S_n-np}{\sqrt{np(1-p)}}\xrightarrow{(d)}\mathcal N(0,1)$${% if jekyll.environment == "development" %} (see [Prob PS8 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab2) and [Stats HW0 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab6)){% endif %}.

Above approximation suffers from Binomial and Normal living in different spaces: where the following holds true in discrete space $$\mathbb P(S_n\lt k+1)=\mathbb P(S_n\le k)$$, it may not be true in a continuous space. [De Moivre and Laplace](https://en.wikipedia.org/wiki/De_Moivre–Laplace_theorem) addressed this with *one-half* correction, and we compute $$\mathbb P(S_n\le k+\frac 1 2)$$ in the continuous space, which should be equivalent to the former two in the discrete space{% if jekyll.environment == "development" %} (see [Prob F Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab6)){% endif %}.

In particular, De Moivre-Laplace correction can be used to approximate binomial PMF as follows{% if jekyll.environment == "development" %} (see [Prob L19 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__19_The_Central_Limit_Theorem__CLT_/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s3-tab10)){% endif %}.

$$p_{S_n}(k)=\mathbb P(k-\frac 1 2\le S_n\le k+\frac 1 2)\xrightarrow{(d)}\Phi\left(\frac{k+\frac 1 2-np}{\sqrt{np(1-p)}}\right)-\Phi\left(\frac{k-\frac 1 2-np}{\sqrt{np(1-p)}}\right)$$

Try it out in R! (scroll down within the frame to see the result)

<iframe width='100%' height='300' src='https://rdrr.io/snippets/embed/?code=p%3C-1%2F2%0An%3C-200%0Ak%3C-105%0Ax1%3C-dbinom(k%2Cn%2Cp)%0Ax2%3C-pnorm((k%2B1%2F2-n*p)%2Fsqrt(n*p*(1-p)))-pnorm((k-1%2F2-n*p)%2Fsqrt(n*p*(1-p)))%0Asprintf(%22Exact%20PMF%20%25f%22%2C%20x1)%0Asprintf(%22Approx%20is%20%25f%2C%20(%25f%25%25)%22%2C%20x2%2C%20(x2%2Fx1-1)*100)' frameborder='0'></iframe>

## Sampling

In real-life experiments, collecting i.i.d. samples may be less trivial as it seems. Clearly, if samples $$X_i$$ are not i.i.d., then the normal approximation of $$S_n=\sum_{i=1}^n X_i$$ is not guaranteed.

To understand how the Normal approximation can be affected by dependency assume $$M\sim\text{Ber}(\frac 1 2)$$ and $$X_i\overset{i.i.d.}{\sim}\mathcal N(M,1)$$. In this example, even though $$Y_i$$ are i.i.d. the mode of all PDF will strongly depends on the **common** value of $$M$$, which has the same chances to be $$0$$ or $$1$$. Accordingly, the PDF of $$X$$ will not be a Normal, as it will have two modes, around $$0$$ and $$1$${% if jekyll.environment == "development" %} (see [Prob L19 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__19_The_Central_Limit_Theorem__CLT_/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s3-tab5) and [Prob PS8 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_8/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s7-tab6)){% endif %}. This, would have been avoided if $$X_i\overset{i.i.d.}{\sim}\mathcal N(M_i,1)$$, where $$M_i\overset{i.i.d.}{\sim}\text{Ber}(\frac 1 2)$$.

Now, imagine a different case, where $$X_i\sim\text{Ber}(p(t))$$, where $$p(t)$$ depends on a different variable (e.g. time of day). In this case, we cannot simply assume that all observations are identically distributed; and the solution would be collecting samples randomly over the hours of day, so that we could estimate $$p=\mathbb E[p(t)]$${% if jekyll.environment == "development" %} (see [Stats L1 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u1s1_whatisstats/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u1s1_whatisstats-tab10)){% endif %}.

From the above, we see that even where $$X_i$$ are not i.i.d. (think of polling), we can still make some assumptions about Normal approximation as long as samples collection is done randomly, uniformly and independently, the samples would appear *statistically* i.i.d.{% if jekyll.environment == "development" %} (see [Prob L18 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__18_Inequalities__convergence__and_the_Weak_Law_of_Large_Numbers/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch12-s2-tab10)).{% endif %}

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

## Convergence of a sequence

In this segment it is useful bearing in mind that a [sequence](https://en.wikipedia.org/wiki/Sequence) is an enumerated collection of elements in which repetitions are allowed and order matters (unlike in a set, where repetitions are not allowed and order does not matter). Formally a sequence can be defined as a function from natural numbers (the position of elements in the sequence) to the elements at each position.

A sequence $$x_n$$ is said to [converge](https://en.wikipedia.org/wiki/Limit_of_a_sequence#Formal_definition) to $$x$$ if for any $$\varepsilon>0$$, there exists $$N$$ s.t. $$\forall n\ge N, \lvert x_n-x\rvert\le\varepsilon$$. Common notation to indicate convergence is $$x_n\xrightarrow[n\rightarrow\infty]{}x$$, or simply $$x_n\rightarrow x$$.

Observe that if $$x_n\rightarrow x$$ and $$y_n\rightarrow y$$, then $$x_n+y_n\rightarrow x+y$$. To prove this, assume that $$\exists N,M$$ for which $$\forall n\ge N\implies\lvert x_n-x\rvert\lt\frac\varepsilon2$$ and $$\forall n\ge M\implies\lvert y_n-y\rvert\lt\frac\varepsilon2$$. This means that $$\forall n\ge\max\{N,M\}$$ we have that $$\lvert x_n+y_n-(x+y)\rvert\le\vert x_n-x\rvert+\lvert y_n-y\rvert\lt\varepsilon$$.

## Hoeffding's lemma {#hoeffding_lemma}

Observe that $$e^{tx}\le\left(\frac{b-x}{b-a}\right)e^{ta}+\left(\frac{x-a}{b-a}\right)e^{tb}$$ due to convexity of the exponential function. If we replace $$x=X$$ and compute exponential on both sides of the inequality we have the following relation.

$$\mathbb E[e^{tX}]\le\left(\frac{b-\mathbb E[X]}{b-a}\right)e^{ta}+\left(\frac{\mathbb E[X]-a}{b-a}\right)e^{tb}$$

Assuming for simplicity that $$\mathbb E[X]=0$$, and setting $$p=-\frac{a}{b-a}$$, the above can be rewritten as:

$$\begin{align}\mathbb E[e^{tX}]&\le e^{ta}(1-p+pe^{t(b-a)})&\text{replace $t(b-a)=u$}\\
&=e^{ta}(1-p+pe^{u})&\text{replace $ta=-up$}\\
&=e^{\ln(1-p+pe^u)-up}=e^{\varphi(u)}\end{align}$$

By [Taylor's expansion](https://en.wikipedia.org/wiki/Taylor_series), $$\varphi(u)=\varphi(0)+\varphi'(0)u+\frac 1 2 \varphi''(0)u^2+O(u^3)$$, and one can verify that $$\varphi(u)=\varphi'(u)=0$$ and $$\varphi''(0)=p(1-p)\le\frac 1 4$$, because $$0\le p\le1$$. This means that $$\varphi(u)\le\frac 1 8u^2$$ and therefore:

$$\mathbb E[e^{tX}]\le e^{\frac 1 8 t^2(b-a)^2}$$

If we drop our assumption that $$\mathbb E[X]=0$$, the above inequality still holds for the first centered moment.

$$\mathbb E[e^{t(X-\mathbb E[X])}]\le e^{\frac 1 8 t^2(b-a)^2}$$
