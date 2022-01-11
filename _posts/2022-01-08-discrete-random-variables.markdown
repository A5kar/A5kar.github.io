---
layout: post
title: "Discrete Random Variables"
---

## Definition

A random variable (RV) $$X$$ is a function that associates a value with every possible outcome $$\omega\in\Omega$$. A random variable $$X(\omega)=x$$ can map into discrete (e.g. $$x\in\mathbb Z$$) or continuous (e.g. $$x\in\mathbb R$$) values. There could be multiple RVs associated with the same sample space; and a function of one or more RV is in turn a RV.

Probability mass function (PMF) $$p_X(x)$$, on the other hand, is a function that associates a real number to every possible outcome $$\omega\in\Omega$$. Or, more formally, $$p_X(x)=\mathbb P(\omega\in\Omega: X(\omega)=x)$$. Usual [axioms](/2022/01/03/probability-models-and-axioms.html#axioms) still apply:

- $$p_X(x)\ge0$$, non-negativity
- $$\sum_x p_X(x)=1$$, normalization

## Expectation

Expected value of $$X$$ is defined as $$\mathbb E[X]=\sum_x xp_X(x)$$ (see [PS4 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab6)) and it can be interpreted as the [arithmetic mean](https://en.wikipedia.org/wiki/Arithmetic_mean) (referred by some as "*statistical hammer*") of a large number of [independent](/2022/01/05/conditioning-and-independence.html#independence) realizations. For infinite sums, expectation needs to be [well defined](https://en.wikipedia.org/wiki/Well-defined_expression) (read unambiguous, especially if $$X$$ can also take negative numbers), hence we assume that $$\sum_x \lvert x\rvert p_X(x)<\infty$$.

|Property|Formula|
|-|:-:|
|Bounds|$$a\le X\le b\implies a\le\mathbb E[X]\le b$$|
|Non negativity|$$X\ge0\implies\mathbb E[X]\ge0$$|
|Non negativity, with $$X\in\{0,1,\dots,\infty\}$$|$$\mathbb E[X]=\sum_{k=0}^\infty\mathbb P(X>k)$$|
|[Law Of The Unconscious Statistician](https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician) (LOTUS)|$$\mathbb E[Y]=\mathbb E[g(X)]=\sum_x g(x)p_X(x)$$|
|Indicator, $$g(X)=\begin{cases}1&\text{$A$ occurs}\\0&\text{otherwise}\end{cases}$$|$$\mathbb E[I_A]=\mathbb P(A)$$|
|Linearity|$$E[aX+b]=a\mathbb E[X]+b$$|

## Variance

Defined as $$\text{var}(X)=\mathbb E[(X-\mathbb E[X])^2]$$, variance measures the spread of a PMF.

|Property|Formula|
|-|:-:|
|Non negativity (*zero* only for constants)|$$\text{var}(X)\ge0$$|
|Equivalency|$$\text{var}(X)=\mathbb E[X^2]-(\mathbb E[X])^2$$ (see [PS4 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab5))|
|Joint PMF|$$\text{var}(aX+bY)=a^2\text{var}(X)+b^2\text{var}(Y)+ab\text{cov}(X,Y)$$|

## Conditioning

Conditioning to an event $$A$$ does not alter the main properties of PMF or the expectation. Note that conditioning could also include another discrete RV, e.g. $$A=\{Y=y\}$$ (see [PS4 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab4)).

|Property|Conditional on event $$A$$|Conditional on RV $$Y$$|
|-|:-:|:-:|
|PMF|$$\displaystyle p_{X\lvert A}(x)=\frac{\mathbb P(X=x\cap A)}{\mathbb P(A)}$$|$$\displaystyle p_{X\lvert Y}(x\lvert y)=\frac{p_{X,Y}(x,y)}{p_Y(y)}$$|
|Normalization|$$\sum_x p_{X\lvert A}(x)=1$$|$$\sum_x p_{X\lvert Y}p(x\lvert y)=1$$|
|Expectation|$$E[X\lvert A]=\sum_x xp_{X\lvert A}(x)$$|$$\mathbb E[X\lvert Y=y]=\sum_x xp_{X\lvert Y}(x\lvert y)$$
|LOTUS|$$\mathbb E[g(X)\lvert A]=\sum_x g(x)p_{X\lvert A}(x)$$|$$\mathbb E[g(X)\lvert Y=y]=\sum_x g(x)p_{X\lvert Y}(x\lvert y)$$
|[Total probability](2022-01-05-conditioning-and-independence.markdown#main_three_tools)|$$p_X(x)=\sum_{i=1}^n\mathbb P(A_i)\mathbb P(X\lvert A_i)$$|$$p_X(x)=\sum_y p_Y(y)p_{X\lvert Y}(x\lvert y)$$
|Total expectation|$$\mathbb  E[X]=\sum_{i=1}^n\mathbb P(A_i)\mathbb E[X\lvert A_i]$$|$$\mathbb E[X]=\sum_y p_Y(y)\mathbb E[X\lvert Y=y]$$

## Independence

Analogously to [independence](/2022/01/05/conditioning-and-independence.html#independence) of two events, we say that if RV $$X$$ is independent from event $$A$$ if $$p_{X\lvert A}(x)=p_X(x)\mathbb P(A), \forall x$$ (see [PS4 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab1)). Similarly, $$X$$ is independent from $$Y$$ if $$p_{X,Y}(x,y)=p_X(x)p_Y(y), \forall x,y$$.

Other effects of $$X$$ being independent from $$Y$$.

|Property|Formula|
|-|:-:|
|Expectations|$$\mathbb E[XY]=\mathbb E[X]\mathbb E[Y]$$|
|Independence of functions|$$\mathbb E[g(X)h(Y)]=\mathbb E[g(X)]\mathbb E[h(Y)]$$|
|Variance|$$\text{var}(aX+bY)=a^2\text{var}(X)+b^2\text{var}(Y)$$|
|Covariance|$$\text{cov}(X, Y)=0$$|

## Memorylessness

Geometric distribution has a remarkable property. Given that initial $$k$$ tosses of a coin were all tails, the probability of having a head in subsequent tosses is exactly the same as if the first $$k$$ tosses never occurred; in other words $$\mathbb P(X\lvert X>k)=\mathbb P(X-k)$$. Replacing $$k=1$$ we obtain the following relationships:

$$\begin{align}
\mathbb E[X\lvert X>1]&=\mathbb E[1+X]\\
\mathbb E[X^2\lvert X>1]&=\mathbb E[(1+X)^2]
\end{align}$$

## Basic discrete RV

|RV|PMF<br>$$p_X(x)$$|Expectation<br>$$\mu_X=\mathbb E[X]$$|Second moment<br>$$\mathbb E[X^2]$$|Variance<br>$$\sigma_X^2=\text{var}(X)$$|
|-|:-:|:-:|:-:|:-:|
|Bernoulli<br>$$\text{Bin}(1,p)$$|$$p^x(1-p)^{1-x}$$|$$p$$|$$p$$|$$p(1-p)$$|
|Binomial<br>$$\text{Bin}(n,p)$$|$$\displaystyle{n\choose k}p^k(1-p)^{n-k}$$|$$np$$|$$np(1-p)+n^2p^2$$|$$np(1-p)$$|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\displaystyle\frac{1}{b-a+1}=\frac{1}{n+1}$$|$$\displaystyle\frac{n}{2}$$|$$\displaystyle\frac{1}{6}n(2n+1)$$|$$\displaystyle\frac{1}{12}n(n+2)$$|
|Constant<br>$$\text{Unif}(c,c)$$|$$\begin{cases}1&\text{if $x=c$}\\0&\text{otherwise}\end{cases}$$|$$c$$|$$c^2$$|$$0$$|
|Geometric<br>$$\text{Geom}(p)$$|$$(1-p)^{k-1}p$$|$$\displaystyle\frac{1}{p}$$|$$\displaystyle\frac{2-p}{p^2}$$|$$\displaystyle\frac{1-p}{p^2}$$|

Occasionally, an indicator RV $$I_A\in\{0,1\}$$ is used to indicate if an event $$A$$ has occurred. In other words, Indicator RV is a Bernoulli RV with $$p=\mathbb P(A)$$.

## Joint PMFs

Taking two discrete RV, each having its own *marginal* distribution, say $$p_X(x)=\mathbb P(X=x)$$ and $$p_Y(y)=\mathbb P(Y=y)$$, their *joint* distribution is defined as $$p_{X,Y}(x,y)=\mathbb P(X=x\cap Y=y)$$. *Marginal* distributions can be derived again from the *joint* distribution as $$p_X(x)=\sum_y p_{X,Y}(x,y)$$ and $$p_Y(y)=\sum_x p_{X,Y}(x,y)$$.

Given $$Z=g(X,Y)$$, we have $$p_Z(z)=\mathbb P(Z=z)=\mathbb P(g(x,y)=z)=\sum_{(x,y):g(x,y)=z}p_{X,Y}(x,y)$$ (see [PS4 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab2)). Therefore, $$\mathbb E[Z]=\mathbb E[g(X,Y)]=\sum_x\sum_y g(x,y)p_{X,Y}(x,y)$$  (see [PS4 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab3)).

Considering $$g(X,Y)=aX+bY$$, the earlier relationship proves that expectation is a linear operator, $$\mathbb E[g(X,Y)]=g(\mathbb E[X],\mathbb E[Y])=a\mathbb E[X]+b\mathbb E[Y]$$.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

## Back-up

In deriving the various relations, it may be useful bearing in mind the following relations.

|Formula|Equivalent form|
|:-:|:-:|
|$$\displaystyle\sum_{k=1}^nk$$|$$\displaystyle\frac{k(k+1)}{2}$$|
|$$\displaystyle\sum_{k=1}^nk$$|$$\displaystyle\frac{k(k+1)(2k+1)}{6}$$|
|$$(X_1+\dots+X_n)^2$$|$$\displaystyle\underbrace{\sum_{i=1}^n X^2}_\text{$n$ terms}+\underbrace{\sum_{i\neq j}X_iX_j}_\text{$n^2-n$ terms}$$|