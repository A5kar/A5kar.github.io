---
layout: post
title: "Methods of estimation"
---

## Introduction

We saw earlier that [natural estimators](/2022/03/24/foundation-of-inference.html#estimation) can easily apply to a large set of parameters, when used in conjunction with the [Delta method](/2022/03/24/foundation-of-inference.html#delta). However, not always the (unknown) parameter $$\theta$$ is a function of $$\mu_X=\mathbb E[X]$$. In such cases, we can rely on the following general approaches:

- **Method of moments** (MM), which leverages on the consistency of natural estimators of population moments;
- **Maximum likelihood estimation** (MLE), which will be developed around the concept of *distance* between [probability measures](https://en.wikipedia.org/wiki/Probability_measure); and
- **M-estimators** (ME), which represent a generalization of MLE and provide an insight into estimators which do not require any prior assumption on the probability family.

## Method of moments

Method of moments (MM) derives estimators from *population moments* $$m_k(\theta)=\mathbb E_{\mathcal P_\theta}[X^k]$$. Recall that for any $$\mathbb E[X^k]$$ we can compute *empirical moments* $$\hat m_k=\frac 1 n\sum_{i=1}^n X_i^k$$. Therefore, creating a **consistent** estimator for the vector of the first $$d$$ moments is immediate.

$$\hat M=\begin{bmatrix}\hat m_1\\\vdots\\\hat m_d\end{bmatrix}=\begin{bmatrix}\frac 1 n\sum_{i=1}^n X\\\vdots\\\frac 1 n\sum_{i=1}^n X^d\end{bmatrix}\xrightarrow{\mathbb P}\begin{bmatrix}\mathbb E[X]\\\vdots\\\mathbb E[X^d]\end{bmatrix}=\begin{bmatrix}m_1(\theta)\\\vdots\\m_d(\theta)\end{bmatrix}=M(\theta)$$

In particular, thanks to multivariate [CLT](/2022/02/21/introduction-to-statistics.html#multivariate_clt), we should be able to make the following statement, provided that $$\Sigma(\theta)=\text{cov}(M(\theta))$$ exists.

$$\sqrt n(\hat M-M(\theta))\xrightarrow{(d)}\mathcal N_d(0,\Sigma(\theta))$$

Assuming $$M(\theta)$$ is *bijective* and $$\theta\in\mathbb R^d$$, unknown $$\theta$$ can be estimated as $$\hat\Theta_n=M^{-1}(\hat m_1,\dots,\hat m_d)$$. In particular, if $$M^{-1}(\hat m_1,\dots,\hat m_d)$$ exists and is continuously differentiable, [Delta method](/2022/03/24/foundation-of-inference.html#multivariate_delta) allows us obtaining the following **asymptotic normality**, with asymptotic variance $$\Gamma(\theta)=S^T\Sigma(\theta)S$$ where $$S=\frac{\partial}{\partial\theta}M^{-1}(M(\theta))$$.

$$\sqrt n(\hat\Theta_n-\theta)\xrightarrow{(d)}\mathcal N_d(0,\Gamma(\theta))$$

Below are few examples of MM estimators for basic distributions{% if jekyll.environment == "development" %} (see [Stats HW6 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw6_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw6_u3methods-tab3)){% endif %}.

|Distribution and unknown parameter|$$\hat\Theta_n=M^{-1}(\hat m_1,\dots,\hat m_d)$$|$$\Gamma(\theta)$$|
|-|:-:|:-:|
|Bernoulli with parameter $$p$$|$$\hat p=\bar X_n$$|$$p(1-p)$$|
|Binomial with parameters $$(k,p)$$|$$\hat p=\frac {\bar X_n} k$$|$$\frac {p(1-p)}k$$|
|Categorical with parameter $$\mathbf p$$|$$\hat{\mathbf p}=\bar{\mathbf X}_n$$|$$\begin{bmatrix}p_1(1-p_1)&&-p_1p_d\\&\ddots&\\-p_1p_d&&p_d(1-p_d)\end{bmatrix}$$|
|Geometric with parameter $$p$$|$$\hat p=\frac 1 {\bar X_n}$$|$$p^2(1-p)$$|
|Poisson with parameter $$\lambda$$|$$\hat\lambda=\bar X_n$$|$$\lambda$$|
|Continuous uniform over $$[0,\theta]$$|$$\hat\theta=2\bar X_n$$|$$\frac 1 3\theta^2$$|
|Exponential with parameter $$\lambda$$|$$\hat\lambda=\frac 1{\bar X_n}$$|$$\lambda^2$$|
|Normal with parameters $$(\mu,\sigma^2)$$|$$\begin{bmatrix}\hat\mu\\\widehat{\sigma^2}\end{bmatrix}=\begin{bmatrix}\bar X_n\\\overline{X_n^2}-(\bar X_n)^2\end{bmatrix}$$|$$\begin{bmatrix}\sigma^2&0\\0&2\sigma^4\end{bmatrix}$$|

Note that MM could also work for any custom collection of $$g_1,\dots,g_d:\Omega\rightarrow\mathbb R$$ functions, provided that the combined $$M(\theta)$$, where $$m_k(\theta)=\mathbb E[g_k(X)]$$, is *bijective* and invertible---in this case, we would be dealing with the **generalized method of moments** (GMM), where MM is a special case with $$g_k(x)=x^k$$.

## Moment generating function

The moment generating function (MGF) is a function that becomes handy for the computation of the first $$m_1,\dots,m_d$$ moments. MGF is defined as $$M_X(t)=\mathbb E[e^{tX}]$$. Bearing in mind Taylor expansion of $$e^x=\sum_{i=1}^\infty\frac{x^i}{i!}$$, it follows that $$M_X(t)=\sum_{i=1}^\infty\frac{t^i}{i!}\mathbb E[X^i]$$ and, in particular, that $$\frac{\partial^k}{\partial t^k}M_X(0)=m_k$$, or $$k$$-th moment of r.v. $$X$$.

Properties of MGF include linear transformations, $$M_Y(t)=e^{\beta t}M_X(\alpha t)$$ if $$Y=\alpha X+\beta$$, and linear combination of independent r.v., $$M_{X+Y}(t)=M_X(t)M_Y(t)$$ if $$X\perp Y$$.

$$\begin{align}
M_X(t)=\sum_x e^{tx}p_X(x)&&M_X(t)=\int_{-\infty}^\infty e^{tx}p_X(x)dx\\
\text{(discrete r.v.)}&&\text{(continuous r.v.)}
\end{align}$$

Few examples of MGF for basic [discrete](/2022/01/08/discrete-random-variables.html#basic) and [continuous](/2022/01/13/continuous-random-variables.html#basic) r.v.

|Distribution|$$M_X(t)$$|
|-|:-:|
|Constant $$c$$|$$e^{tc}$$|
|Bernoulli with parameter $$p$$|$$1-p+e^tp$$|
|Binomial with parameters $$(k,p)$$|$$(1-p+e^tp)^k$$|
|Geometric with parameter $$p$$|$$\displaystyle\frac{e^tp}{1-e^t(1-p)}$$<br>where $$t\lt-\ln(1-p)$$|
|Pascal with parameters $$(k,p)$$|$$\displaystyle\left(\frac{e^tp}{1-e^t(1-p)}\right)^k$$<br>where $$t\lt-\ln(1-p)$$|
|Poisson with parameter $$\lambda$$|$$e^{\lambda(e^t-1)}$$|
|Discrete uniform over $$[a,b]$$|$$\displaystyle\frac{e^{ta}}{n}\frac{1-e^{tn}}{1-e^t}$$<br>where $$n=b-a+1$$<br>|
|Continuous uniform over $$[a,b]$$|$$\displaystyle\frac{e^{tb}-e^{ta}}{\theta t}$$<br>where $$\theta=b-a$$|
|Exponential with parameter $$\lambda$$|$$\displaystyle\frac\lambda{\lambda-t}$$<br>where $$t\lt\lambda$$|
|Erlang with parameters $$(k,\lambda)$$|$$\displaystyle\left(\frac\lambda{\lambda-t}\right)^k$$<br>where $$t\lt\lambda$$|
|Gamma with parameters $$(\alpha,\beta)$$|$$\displaystyle\left(\frac{\beta}{\beta-t}\right)^\alpha$$<br>where $$t\lt\beta$$|
|Normal with parameters $$(\mu,\sigma^2)$$|$$e^{\mu t+\frac12\sigma^2t^2}$$|

As for the derivation of Binomial, Pascal (or Negative Binomial), Erlang and even Gamma, consider that $$M_{X_1+\dots+X_n}(t)=(M_X(t))^n$$ where $$X_i$$ are $$n$$ i.i.d. r.v., therefore their derivation is immediate from Bernoulli, Geometric and Exponential MGFs.

## Total variation distance

Before introducing MLE, let us review the concept of *distance* between distributions, namely total variation distance and Kullback-Leibler divergence.

Assume $$(\Omega,\{\mathcal P_\theta\}_{\theta\in\Theta})$$ is a [statistical model](/2022/03/24/foundation-of-inference.html#model) and $$\theta^\star$$ is the true parameter. Recall that $$\theta^\star$$ is identifiable if $$\mathcal P_\theta=\mathcal P_{\theta^\star}\implies\theta=\theta^\star$$, or alternatively if $$\lvert\mathcal P_{\theta}-\mathcal P_{\theta^\star}\rvert=0$$. Hence, the intuition is that as soon as we find $$\theta$$, s.t. $$\lvert\mathcal P_{\theta}-\mathcal P_{\theta^\star}\rvert=0$$, then we found the true parameter $$\theta^\star$$. This leads to to the definition of **total variation** (TV){% if jekyll.environment == "development" %} (see [Stats L8 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab4)){% endif %}.

$$\text{TV}(\mathcal P,\mathcal Q)=\sup_{A\subseteq\Omega}\lvert\mathcal P(A)-\mathcal Q(A)\rvert$$

Mathematically speaking, TV a [distance](https://en.wikipedia.org/wiki/Metric_(mathematics)), thanks to the following properties{% if jekyll.environment == "development" %} (see [Stats L8 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab7)){% endif %}.

|Property|Formula|
|-|:-:|
|Identity of indiscernibles|$$\text{TV}(\mathcal P,\mathcal Q)=0\iff\mathcal P=\mathcal Q$$|
|Symmetry|$$\text{TV}(\mathcal P,\mathcal Q)=\text{TV}(\mathcal P,\mathcal Q)$$|
|Triangle inequality|$$\text{TV}(\mathcal P,\mathcal Q)\le\text{TV}(\mathcal P,\mathcal R)+\text{TV}(\mathcal R,\mathcal Q)$$|

Based on the above, we can derive that $$0\le\text{TV}(\mathcal P,\mathcal Q)\le1$$.

|Property|Formula|
|-|:-:|
|Non negativity|$$0=\text{TV}(\mathcal P,\mathcal P)\le\text{TV}(\mathcal P,\mathcal Q)+\text{TV}(\mathcal Q,\mathcal P)=2\text{TV}(\mathcal P,\mathcal Q)$$<br>therefore, $$\text{TV}(\mathcal P,\mathcal Q)\ge0$$|
|Upper bound|$$\text{TV}(\mathcal P,\mathcal Q)=\sup_{A\subseteq\Omega}\lvert\mathcal P(A)-\underbrace{\mathcal Q(A)}_{\ge0}\rvert\le\mathcal P(A)\le1$$<br>therefore, $$\text{TV}(\mathcal P,\mathcal Q)\le1$${% if jekyll.environment == "development" %}<br>(see [Stats L8 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab8)){% endif %}|

When $$\Omega$$ is countable, TV is closely related to $$L^1$$ norm.

$$\lVert\mathcal P-\mathcal Q\rVert_1=\sum_{x\in\Omega}\lvert p(x)-q(x)\rvert=2\sup_{A\subseteq\Omega}\lvert\mathcal P(A)-\mathcal Q(A)\rvert=2\text{TV}(\mathcal P,\mathcal Q)$$

Assume $$\Omega=A\cup A^C$$, with $$A=\{x\in\Omega:p(x)\ge q(x)\}$$, and observe that $$\lvert\mathcal P(A)-\mathcal Q(A)\rvert$$ is the same as $$\lvert\mathcal Q(A^C)-\mathcal P(A^C)\rvert$$. Therefore, $$\lvert\mathcal P(\Omega)-\mathcal Q(\Omega)\rvert=2\lvert\mathcal P(A)-\mathcal Q(A)\rvert$$, which explains why we need to divide by $$2$$ the cumulative variation calculated over the entire $$\Omega$$.

||$$\Omega$$ discrete|$$\Omega$$ continuous|
|:-:|:-:|:-:|
|$$\text{TV}(\mathcal P,\mathcal Q)$$|$$\displaystyle\frac 1 2\sum_{x\in\Omega}\lvert p(x)-q(x)\rvert$${% if jekyll.environment == "development" %}<br>(see [Stats L8 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab5)){% endif %}|$$\displaystyle\frac 1 2\int_{x\in\Omega}\lvert p(x)-q(x)\rvert dx$${% if jekyll.environment == "development" %}<br>(see [Stats L8 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab6)){% endif %}|

For simplicity of notation, $$p(x)$$ and $$q(x)$$ indicate PDF (or PMF, as applicable) of the probability measures $$\mathcal P$$ and $$\mathcal Q$$, respectively.

Notice when support of $$\mathcal P$$ does not intersect support of $$\mathcal Q$$, $$\text{TV}(\mathcal P,\mathcal Q)=1$${% if jekyll.environment == "development" %} (see [Stats L8 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab9)){% endif %}, which is one of the drawbacks of TV. It does not capture proximity of support spaces, and regardless if they are *infinitely* close or distant, it will always yield $$1$$ until they are disjoint{% if jekyll.environment == "development" %} (see [Stats HW4 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw4_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw4_u3methods-tab2)){% endif %}.

For our purposes, consider $$\mathcal P=\mathcal P_{\theta^\star}$$ and $$\mathcal Q$$ any other probability measure (including $$\mathcal P_\theta$$ of the same family as $$\mathcal P_{\theta^\star}$$, but with a different parameter $$\theta$$). From the above, it comes natural that one way to find $$\theta^\star$$ is be by manipulating $$\theta$$ until we see that $$\text{TV}(\mathcal P_{\theta^\star}, \mathcal P_\theta)$$ is minimized; but here is the issue---how do we estimate $$\text{TV}(\mathcal P_{\theta^\star}, \mathcal P_\theta)$$, and try minimizing it, without knowing $$\theta^\star$$?

From earlier introduction to [estimation](/2022/03/24/foundation-of-inference.html#estimation), we learnt that we can estimate $$\mathbb E[X_i]$$ or $$\mathbb E[f(X_i)]$$ thanks to the [sample mean](/2022/02/21/introduction-to-statistics.html#clt_mean) and [Delta method](/2022/03/24/foundation-of-inference.html#delta). This means that we could estimate $$\text{TV}(\mathcal P_{\theta^\star}, \mathcal P_\theta)$$ if KL was in turn a sort of $$\mathbb E[f(\mathcal P_{\theta^\star}, \mathcal P_\theta)]$$. As this is not the case, we need an alternative *distance* function in the form of estimation.

## Kullback-Leibler divergence

The solution to the above dilemma comes from [information theory](https://en.wikipedia.org/wiki/Information_theory), under the name of [Kullback-Leibler divergence](https://en.wikipedia.org/wiki/Kullback–Leibler_divergence) (KL), defined as follows{% if jekyll.environment == "development" %} (see [Stats HW4 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw4_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw4_u3methods-tab1)){% endif %} (replace integral with sum, in case of $$\Omega$$ discrete).

$$\text{KL}(\mathcal P,\mathcal Q)=\begin{cases}\displaystyle\int_{x\in\Omega}p(x)\ln\left(\frac{p(x)}{q(x)}\right)dx&q(x)=0\implies p(x)=0\\+\infty&\exists x:q(x)=0,p(x)\neq0\end{cases}$$

Where thanks to [L'Hôpital's rule](https://en.wikipedia.org/wiki/L%27Hôpital%27s_rule) we have that $$\lim_{p(x)\rightarrow0^+}p(x)\ln(p(x))=0$$ and therefore the term $$p(x)\ln\left(\frac{p(x)}{q(x)}\right)=0, \forall x\in\Omega:p(x)=0$${% if jekyll.environment == "development" %} (see [Stats L8 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab9)){% endif %}.

When $$\text{KL}(\mathcal P,\mathcal Q)\lt\infty$$, it indicates the expected logarithmic distance between $$p(x)$$ and $$q(x)$$, where the expectation takes probabilities $$p(x)$$, $$\text{KL}(\mathcal P,\mathcal Q)=\mathbb E_\mathcal P\left[\ln\left(\frac{p(X)}{q(X)}\right)\right]=\mathbb E_\mathcal P\left[-\ln\left(\frac{q(X)}{p(X)}\right)\right]$$, with the following properties{% if jekyll.environment == "development" %} (see [Stats L8 Q11](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab11)){% endif %}.

|Property|Formula|
|-|:-:|
|Identity of indiscernibles|$$\text{KL}(\mathcal P,\mathcal Q)=0\iff\mathcal P=\mathcal Q$$|
|Non negativity|$$\begin{align}\text{KL}(\mathcal P,\mathcal Q)&=\mathbb E_\mathcal P\left[-\ln\left(\frac{q(X))}{p(X)}\right)\right]&\href{/2022/02/21/introduction-to-statistics.html#basic}{\text{(Jensen's inequality)}}\\&\ge-\ln\left(\mathbb E_\mathcal P\left[\frac{q(X)}{p(X)}\right]\right)&\href{/2022/01/13/continuous-random-variables.html#expectation}{\text{(Expectation)}}\\&\ge\ln(1)=0\end{align}$$|

On the other hand, KL **does not** satisfy symmetry $$\text{KL}(\mathcal P,\mathcal Q)\neq\text{KL}(\mathcal P,\mathcal Q)$$ and triangular inequality $$\text{KL}(\mathcal P,\mathcal Q)\nleq\text{KL}(\mathcal P,\mathcal R)+\text{KL}(\mathcal R,\mathcal Q)$$. For this reason, KL is not a distance but a [divergence](https://en.wikipedia.org/wiki/Divergence_(statistics)). Lack of symmetry, however, is not a flaw but a feature of KL.

By expanding $$\text{KL}(\mathcal P,\mathcal Q)=\mathbb E_\mathcal P\left[-\ln\left(\frac{q(X)}{p(X)}\right)\right]=\mathbb E_\mathcal P[-\ln(q(X))]-\mathbb E_\mathcal P[-\ln(p(X))]$$ we observe that KL can be written as the difference $$\text H(\mathcal P,\mathcal Q)-\text H(\mathcal P)$$, where:

- $$\text H(\mathcal P,\mathcal Q)=\mathbb E_\mathcal P[-\ln(q(X))]$$ is **cross entropy** of $$\mathcal Q$$ relative to $$P$$;
- $$\text H(\mathcal P)=\mathbb E_\mathcal P[-\ln(p(X))]$$ is **entropy** and is *constant* for each specific $$\mathcal P$$.

Therefore, assuming we want to compute $$\text{KL}(\mathcal P_{\theta^\star},\mathcal P_\theta)$$, with $$\mathcal P_{\theta^\star}$$ and $$\mathcal P_\theta$$ being two distributions from the same family with different parameters ($$\theta^\star$$ being the true, unknown parameter), we conclude that even though we would not be able to estimate the true $$\text{KL}(\mathcal P_{\theta^\star},\mathcal P_\theta)$$, we should be able to find $$\theta$$ that minimizes it, which would occur when $$\theta=\theta^\star$$. Considering that entropy $$\text H(\mathcal P_{\theta^\star})$$ for any given $$\mathcal P_{\theta^\star}$$ is constant, we can therefore focus on minimization of cross entropy only.

Considering that cross entropy $$\text H(\mathcal P_{\theta^\star},\mathcal P_\theta)=\mathbb E_{\mathcal P_{\theta^\star}}[-\ln(p_\theta(X))]$$ is an expectation of a function, we can build a natural (and consistent) [estimator](/2022/03/24/foundation-of-inference.html#estimation) $$\widehat{\text H}(\mathcal P_{\theta^\star},\mathcal P_\theta)=\frac 1 n\sum_{i=1}^n[-\ln(p_\theta(X_i))]$$. This is possible because [WLLN](/2022/02/21/introduction-to-statistics.html#wlln) and [CMT](/2022/02/21/introduction-to-statistics.html#properties) do not require the knowledge of the true $$\mathcal P_{\theta^\star}$$, only a random sample from the same{% if jekyll.environment == "development" %} (see [Stats L8 Q12](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab12)){% endif %}. Finally, notice that $$\widehat{\text H}(\mathcal P_{\theta^\star},\mathcal P_\theta)$$ is minimum when $$\ln\left(\prod_{i=1}^n p_\theta(X_i)\right)$$ achieves its maximum{% if jekyll.environment == "development" %} (see [Stats L8 Q13](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab13)){% endif %}. Follows a brief comparison table between TV and KL.

||$$\text{TV}(\mathcal P, \mathcal Q)$$|$$\text{KL}(\mathcal P, \mathcal Q)$$|
|-|:-:|:-:|
|Non negative, $$\text{d}(\mathcal P, \mathcal Q)\ge0$$|$$\color{green}\checkmark$$|$$\color{green}\checkmark$$|
|Definite, $$\text{d}(\mathcal P, \mathcal Q)=0\iff\mathcal P=\mathcal Q$$|$$\color{green}\checkmark$$|$$\color{green}\checkmark$$|
|Symmetric, $$\text{d}(\mathcal P, \mathcal Q)=\text{d}(\mathcal Q, \mathcal P)$$|$$\color{green}\checkmark$$|$$\color{red}\times$$|
|Triangular Inequality, $$\text{d}(\mathcal P, \mathcal Q)\le\text{d}(\mathcal Q, \mathcal R)+\text{d}(\mathcal R, \mathcal Q)$$|$$\color{green}\checkmark$$|$$\color{red}\times$$|
|Amenable to estimation, $$\text{d}(\mathcal Q, \mathcal R)=\mathbb E[f(\mathcal Q, \mathcal R)]$$|$$\color{red}\times$$|$$\color{green}\checkmark$$|

The term $$\prod_{i=1}^n p_\theta(X_i)=\mathcal L_n(X_1,\dots,X_n,\theta)$$ is referred to as the **likelihood** and it represents the joint probability of drawing $$n$$ copies of $$X_i\overset{i.i.d.}{\sim}\mathcal P_\theta$${% if jekyll.environment == "development" %} (see [Stats L9 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab2) and [Stats L9 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab3)){% endif %}. This means that for any fixed sample $$(x_1,\dots,x_n)$$, we can manipulate $$\theta$$ until we find the maximum likelihood, and this process of finding $$\max_{\theta}\mathcal L_n(X_1=x_1,\dots,X_n=x_n,\theta)$$ is known as the **maximum likelihood principle**{% if jekyll.environment == "development" %} (see [Stats L8 Q14](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab14)){% endif %}. Properties of the likelihood are indicated below{% if jekyll.environment == "development" %} (see [Stats L8 Q15](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s01_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s01_methodestimation-tab15)){% endif %}.

|Property|Formula|
|-|:-:|
|Symmetry|$$\mathcal L_n(X_1,\dots,X_n,\theta)=\mathcal L_n(X_j,\dots,X_k,\theta)$$<br>where $$(X_j,\dots,X_k)$$ is any possible permutation of $$(X_1,\dots,X_n)$$|
|Sequential update|$$\mathcal L_n(X_1,\dots,X_n,\theta)=\mathcal L_{n-1}(X_1,\dots,X_{n-1},\theta)\mathcal L(X_n,\theta)$$, for any $$n>1$$|

For ease of notation, we often use $$\mathcal L_n(\theta)$$, instead of the longer $$\mathcal L_n(X_1,\dots,X_n,\theta)$$, provided that one bears in mind that $$\mathcal L_n(\theta)$$ is random, as it depends on the random collection $$(X_1,\dots,X_n)$$.

## Maximization of concave functions {#maximization}

Maximization of arbitrary functions can be difficult and we usually focus on strictly concave functions. A function $$f:\mathbb R\rightarrow\mathbb R$$ is **strictly concave** if it is twice differentiable and $$\frac{\partial^2}{\partial\theta^2}f(\theta)\lt0$$, $$\forall\theta\in\Theta$${% if jekyll.environment == "development" %} (see [Stats L9 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab7)){% endif %}. Strictly concave functions are easy to maximize, because if $$\exists \theta^\star=\arg\max_{\theta\in\Theta} f(\theta)$$, then $$\theta^\star$$ is unique and $$\frac{\partial}{\partial\theta}f(\theta^\star)=0$${% if jekyll.environment == "development" %} (see [Stats HW4 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw4_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw4_u3methods-tab4)){% endif %}. Also, any linear combination $$\sum a_i f_i(\theta)$$ of strictly concave functions $$f_i(\theta)$$, with $$a_i\gt0$$ is also strictly concave{% if jekyll.environment == "development" %} (see [Stats L9 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab9)){% endif %}.

More generally, a multivariate function $$f:\mathbb R^d\rightarrow\mathbb R$$, with $$d\ge2$$, is strictly concave if the [Hessian matrix](https://en.wikipedia.org/wiki/Hessian_matrix) $$\mathbf H_\theta f(\theta)$$ is **negative definite**, that is $$x^T\mathbf H_\theta f(\theta)x\lt0$$, $$\forall x\in\mathbb R^d$$ and $$\theta\in\Theta$$. This definition is equivalent to all eigenvalues $$\lambda_i$$ of $$\mathbf H_\theta f(\theta)$$ being negative{% if jekyll.environment == "development" %} (see [Stats L9 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab10)){% endif %}, which in turn requires that all elements on the main diagonal are also negative{% if jekyll.environment == "development" %} (see [Stats L9 Q11](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab11)){% endif %}. If that is the case, and $$\mathbf H_\theta f(\theta)$$ is indeed negative definite, then the solution $$\theta^\star\in\mathbb R^d$$ is located where the [gradient](https://en.wikipedia.org/wiki/Gradient) is zero, or $$\nabla f(\theta^\star)=0$$. Thanks to [convex optimization theory](https://en.wikipedia.org/wiki/Convex_optimization), there are many algorithms that find closed form solutions to this problem, and this is an additional reason that make MLE particularly appealing. Recall that:

$$\begin{align}\nabla f(\theta)=\left[\begin{array}{}\frac{\partial}{\partial\theta_1}f(\theta)\\\vdots\\\frac{\partial}{\partial\theta_d}f(\theta)\end{array}\right]\in\mathbb R^d&&\mathbf H_\theta f(\theta)=\left[\begin{array}{ccc}\frac{\partial^2}{\partial\theta_1^2}f(\theta)&\dots&\frac{\partial^2}{\partial\theta_1\partial\theta_d}f(\theta)\\\vdots&\ddots&\vdots\\\frac{\partial^2}{\partial\theta_d\partial\theta_1}f(\theta)&\dots&\frac{\partial^2}{\partial\theta_d^2}f(\theta)\end{array}\right]\end{align}\in\mathbb R^{d\times d}$$

For completeness, function $$f(\theta)$$ is concave (without *strictly*) if $$f''(x)\le0$$, or in case of multivariate function $$x^T\mathbf H_\theta f(\theta)x\le0$$ (matrix is negative *semi*-definite). To avoid confusion, bear in mind that strictly concave $$\implies$$ concave, and negative definite $$\implies$$ negative semi-definite{% if jekyll.environment == "development" %} (see [Stats L9 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab8)){% endif %}. Maximization is to concave the same way minimization is to **convex**, and all analogous considerations can be made with respect to convex functions{% if jekyll.environment == "development" %} (see [Stats HW4 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw4_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw4_u3methods-tab3)){% endif %}.

## Maximum likelihood estimation

Since maximization of likelihood is equivalent to minimization of KL, **maximum likelihood estimator** (MLE) of $$\theta$$ is defined as $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\mathcal L_n(\theta)$$, provided that $$\mathcal L_n(\theta)$$ is strictly concave in $$\theta$$. Maximization is often performed in the log-space, as $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\ln(\mathcal L_n(\theta))$$, because of the same concavity considerations and the convenience in manipulating [exponential family](https://en.wikipedia.org/wiki/Exponential_family) distributions.

In practice, the term $$\ln(\mathcal L_n(\theta))$$ is commonly referred to as $$\ell_n(\theta)$$, or **log-likelihood**, and once we confirm that $$x^T\mathbf H_\theta\ell(\theta)x\lt0$$, $$\forall x\in\mathbb R^d$$, $$\hat\Theta_n$$ is determined by solving the equation $$\nabla_\theta\ell_n(\hat\Theta_n)=0$$. In case of $$\theta\in\mathbb R$$ (univariate), the afore mentioned procedure becomes as follows:

- compute $$\mathcal L_n(\theta)=\mathcal L_n(X_1,\dots,X_n,\theta)$$
- compute $$\ell_n(\theta)=\ln\mathcal L_n(\theta)$$ and $$\ell_n'(\theta)=\frac \partial {\partial\theta}\ell_n(\theta)$$, if exists
- verify that $$\ell_n''(\theta)=\frac{\partial^2}{\partial\theta^2}\ell_n(\theta)\lt0$$, $$\forall\theta\in\Theta$$
- derive $$\hat\Theta_n$$, s.t. $$\ell_n'(\hat\Theta_n)=0$$

Follow few examples of likelihood functions $$\mathcal L_n(\theta)$$ and estimators $$\hat\Theta_n$$ for the earlier [statistical models](/2022/03/24/foundation-of-inference.html#model).

|Distribution and unknown parameter|$$\mathcal L_n(\theta)$$|$$\displaystyle\hat\Theta_n=\arg\max_{\theta\in\Theta} \ell_n(\theta)$$|
|-|:-:|:-:|
|Bernoulli with parameter $$p$$|$$p^{\sum_{i=1}^n X_i}(1-p)^{n-\sum_{i=1}^n X_i}$$|$$\hat p=\bar X_n$${% if jekyll.environment == "development" %}<br>(see [Stats L9 Q12](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab12)){% endif %}|
|Binomial with parameters $$(k,p)$$|$$\left(\prod_{i=1}^n{k\choose X_i}\right)p^{\sum_{i=1}^n X_i}(1-p)^{nk-\sum_{i=1}^n X_i}$$|$$\hat p=\frac {\bar X_n}k$$|
|Categorical with parameter $$\mathbf p$$|$$\prod_{j=1}^d p_j^{a_j}$$<br>$$a_j=\sum_{i=1}^n\mathbb 1(X_i=j)$$|$$\left(\frac {a_1}n,\dots,\frac{a_d}n\right)$${% if jekyll.environment == "development" %}<br>(see [Stats L10 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab3)){% endif %}|
|Geometric with parameter $$p$$|$$p^n(1-p)^{\sum_{i=1}^n X_i-n}$$|$$\hat p=\frac 1 {\bar X_n}$$|
|Poisson with parameter $$\lambda$$|$$\displaystyle e^{-n\lambda}\frac{\lambda^{\sum_{i=1}^n X_i}}{\prod_{i=1}^n X_i!}$$|$$\hat\lambda=\bar X_n$${% if jekyll.environment == "development" %}<br>(see [Stats L9 Q13](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab13)){% endif %}|
|Continuous uniform over $$[0,\theta]$$|$$\frac{1}{\theta^n}\mathbb 1(X_{(n)}\le\theta)$$|$$X_{(n)}$${% if jekyll.environment == "development" %}<br>(see [Stats L10 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab2)){% endif %}|
|Exponential with parameter $$\lambda$$|$$\lambda^n e^{-\lambda\sum_{i=1}^n X_i}$$|$$\hat\lambda=\frac 1 {\bar X_n}$$|
|Normal with parameters $$(\mu,\sigma^2)$$|$$(2\pi\sigma^2)^{-\frac n 2}e^{-\frac{1}{2\sigma^2}\sum_{i=1}^n (X_i-\mu)^2}$$|$$\begin{bmatrix}\hat\mu\\\widehat{\sigma^2}\end{bmatrix}=\begin{bmatrix}\bar X_n\\\overline{X_n^2}-(\bar X_n)^2\end{bmatrix}$${% if jekyll.environment == "development" %}<br>(see [Stats L9 Q14](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab14)){% endif %}|

As for the Categorical estimator, consider that $$\frac 1 n\ln\mathcal L_n(X_1,\dots,X_n,p_1,\dots,p_d)=\sum_{j=1}^d\frac {a_j}n\ln(p_j)$$ (negative cross entropy) and that $$\mathbb E[\ln(p(X))]=\sum_{j=1}^d p_j\ln(p_j)$$ (negative entropy). This means that when $$p_j=\frac {a_j}n$$, cross entropy and entropy will coincide and therefore KL divergence will be zero.

## Score and Fisher information {#score}

MLE can also be explained through the **score** function, defined as $$s_n(\theta)=\nabla_\theta\ell_n(\theta)$$, which in case of a single observation of a continuous r.v. $$X$$ becomes $$s(\theta)=\nabla_\theta\ln f_\theta(X)$$. Note that $$s_n(\theta)$$ can also be expressed as the sum of single scores per observation $$s_n(\theta)=\sum_{i=1}^n s_i(\theta)$$.

Considering that $$X$$ is random, $$s(\theta)$$ is also random, with a defined expectation and variance. Let us consider the univariate case and assume that $$\theta\in\mathbb R$$ is the true, unknown parameter, for which we are able to compute $$s(\theta)=\frac\partial{\partial\theta}\ln f_\theta(X)$$. Our first observation is that $$\mathbb E[s(\theta)]=0$${% if jekyll.environment == "development" %} (see [Stats L11 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s04_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s04_methodestimation-tab3)){% endif %}.

$$\begin{align}
\mathbb E[s(\theta)]
&=\int_{-\infty}^\infty\left(\frac\partial{\partial\theta}\ln f_{\theta}(x)\right)f_{\theta}(x)dx=\int_{-\infty}^\infty\frac{\frac\partial{\partial\theta}f_{\theta}(x)}{f_{\theta}(x)}f_{\theta}(x)dx\\
&=\int_{-\infty}^\infty\frac\partial{\partial\theta}f_{\theta}(x)dx=\frac\partial{\partial\theta}\int_{-\infty}^\infty f_{\theta}(x)dx=\frac\partial{\partial\theta}1=0
\end{align}$$

This means that if we collect $$X_i\overset{i.i.d.}{\sim}\mathcal P_{\theta}$$ and compute $$s_i(\theta)$$ for each of $$X_i$$, their average will be zero. Considering that $$\bar s_n(\theta)=\frac 1 n\sum_{i=1}^n s_i(\theta)\xrightarrow{\mathbb P}\mathbb E[s(\theta)]=0$$ (see [WLLN](/2022/02/21/introduction-to-statistics.html#wlln)), it makes sense that $$\theta$$ can be estimated with $$\hat\Theta_n$$ s.t. $$\bar s_n(\hat\Theta_n)=0$$. By construction, it will also mean that $$\ell_n'(\hat\Theta_n)=0$$.

Variance of the score is known as [Fisher information](https://en.wikipedia.org/wiki/Fisher_information), $$I(\theta)=\text{var}(s(\theta))$$, which can be proved to be equivalent to the average curvature around the true, unknown $$\theta$$, that is $$I(\theta)=\mathbb E[-\ell''(\theta)]$$.

$$\begin{align}
\mathbb E[-\ell''(\theta)]
&=-\int_{-\infty}^\infty\frac\partial{\partial\theta}\left(\frac\partial{\partial\theta}\ln f_{\theta}(x)\right)f_{\theta}(x)dx\\
&=\cancelto{=0}{-\int_{-\infty}^\infty\frac{\partial^2}{\partial\theta^2}f_{\theta}(x)dx}+\int_{-\infty}^\infty\frac{\left(\frac\partial{\partial\theta}f_{\theta}(x)\right)^2}{f_{\theta}(x)}dx\\
&=\int_{-\infty}^\infty\left(\frac{\frac\partial{\partial\theta}f_{\theta}(x)}{f_{\theta}(x)}\right)^2f_{\theta}(x)dx=\mathbb E[s(\theta)^2]=\text{var}(s(\theta))
\end{align}$$

Wrapping up, $$\sqrt n\bar s_n(\theta)\xrightarrow{(d)}\mathcal N(0,I(\theta))$$ ([CLT](/2022/02/21/introduction-to-statistics.html#clt)), and if one performs Taylor expansion of $$\bar s_n(\hat\Theta_n)=0$$ (by definition of $$\hat\Theta_n$$), then one can achieve the following result.

$$\begin{align}
\sqrt n 0=\sqrt n \frac 1 n\sum_{i=1}^n s_i(\hat\Theta_n)&\approx\sqrt n \frac 1 n\sum_{i=1}^n\left(s_i(\theta)+(\hat\Theta_n-\theta)s_i'(\theta)\right)\\
&=\underbrace{\sqrt n\frac 1 n\sum_{i=1}^ns_i(\theta)}_{\xrightarrow{(d)}\mathcal N(0,I(\theta))}+\sqrt n(\hat\Theta_n-\theta)\underbrace{\frac 1 n\sum_{i=1}^n s_i'(\theta)}_{\xrightarrow{\mathbb P}\mathbb E[\ell''(\theta)]=-I(\theta)}\\
\sqrt n(\hat\Theta_n-\theta)I(\theta)&\xrightarrow{(d)}\mathcal N(0,I(\theta))\\
\sqrt n(\hat\Theta_n-\theta)&\xrightarrow{(d)}\mathcal N(0,I^{-1}(\theta))
\end{align}$$

Above derivation is informal, but is sufficient to highlight that MLE can be asymptotically Normal, with Fisher information determining asymptotic variance. Another important fact, is that Fisher information is associated with the lowest possible variance of an *unbiased* estimator, known as [Cramér–Rao bound](https://en.wikipedia.org/wiki/Cramér–Rao_bound), $$\text{var}(\hat\Theta_n)\ge I^{-1}(\theta)$$. Finally, bear in mind that if $$\theta$$ is multivariate, then $$I(\theta)=\mathbb E[-\mathbf H_\theta\ell(\theta)]$$.

Again, few examples of score functions $$s(\theta)$$ and Fisher information $$I(\theta)$${% if jekyll.environment == "development" %} (see [Stats HW6 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw6_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw6_u3methods-tab1) and [Stats HW6 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw6_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw6_u3methods-tab2)){% endif %}.

|Distribution and unknown parameter|$$s(\theta)=\nabla_\theta\ell(X,\theta)$$|$$I(\theta)=\mathbb E[-\mathbf H_\theta\ell(\theta)]$$|
|-|:-:|:-:|
|Bernoulli with parameter $$p$$|$$\frac X p-\frac{1-X}{1-p}$$|$$\frac 1 {p(1-p)}$$|
|Binomial with parameters $$(k,p)$$|$$\frac X p-\frac{k-X}{1-p}$$|$$\frac k {p(1-p)}$$|
|Categorical with parameter $$\mathbf p$$|$$\begin{bmatrix}\frac{\mathbb 1(X=1)}{p_1}\\\vdots\\\frac{\mathbb 1(X=d)}{p_d}\end{bmatrix}$$|$$\begin{bmatrix}\frac 1{p_1}&&0\\&\ddots&\\0&&\frac 1{p_d}\end{bmatrix}$$|
|Geometric with parameter $$p$$|$$\frac 1 p-\frac{X-1}{1-p}$$|$$\frac 1 {p^2(1-p)}$$|
|Poisson with parameter $$\lambda$$|$$-1+\frac X \lambda$$|$$\frac 1 \lambda$$|
|Continuous uniform over $$[0,\theta]$$|$$\begin{cases}-\frac n \theta&X_{(n)}\le\theta\\-\infty&\text{otherwise}\end{cases}$$|does not exist|
|Exponential with parameter $$\lambda$$|$$\frac 1 \lambda-X$$|$$\frac 1 {\lambda^2}$$|
|Normal with parameters $$(\mu,\sigma^2)$$|$$\begin{bmatrix}-\frac 1{\sigma^2}(X-\mu)\\-\frac 1 {2\sigma^2}+\frac 1 {2\sigma^4}(X-\mu)^2\end{bmatrix}$$|$$\begin{bmatrix}\frac 1{\sigma^2}&0\\0&\frac 1 {2\sigma^4}\end{bmatrix}$$|

Above shows that $$I(\theta)$$ associated with the a continuous Uniform does not exist, which is justified by $$\mathcal P_\theta$$ depending on $$\theta$$. This does not mean that $$X_{(n)}$$ has no variance, in fact $$\text{var}(X_{(n)})=\frac{n\theta^2}{(n+1)^2(n+2)}$$. Also, $$\text{MSE}(X_{(n)})=\frac{2\theta^2}{(n+1)(n+2)}$$ is smaller than $$\text{MSE}(2\bar X_n)=\frac{\theta^2}{3n}$$ for $$n>2$$, despite the latter is an unbiased estimator found via the MM.

Regarding the Categorical with parameter $$\mathbf p=\begin{bmatrix}p_1&\dots&p_d\end{bmatrix}^T$$; although $$I(p_1,\dots\,p_d)$$ exists, it is not invertible over $$\Theta=\{(p_1,\dots,p_d):\sum_{j=1}^d p_j-1=0\}\subset\mathbb R^{d-1}$$, because of the lower dimensionality of $$\Theta$$ with respect to the dimension of $$p\in\mathbb R^d$$.

## Consistency and asymptotic normality of MLE

When all of the following conditions are satisfied{% if jekyll.environment == "development" %} (see [Stats MT1 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm1-tab3) and [Stats MT1 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm1-tab5)){% endif %}:

- The true parameter $$\theta$$ is identifiable;
- The support of $$\mathcal P_\theta$$ does not depend on $$\theta$$;
- True parameter $$\theta$$ is not on the boundary of $$\Theta$$;
- $$I(\theta)$$ is invertible in the neighborhood of true parameter $$\theta$$; and
- few more technical conditions.

MLE is **consistent** and **asymptotically Normal**, that is:

$$\sqrt n(\hat\Theta_n-\theta)\xrightarrow{(d)}\mathcal N_d(0,I^{-1}(\theta))$$

Without excessive formality, consistency of MLE can be argued that some *mild regularity conditions* (that hold almost always) allow transferring convergence from natural estimator as below, provided that $$\theta^\star$$ is identifiable{% if jekyll.environment == "development" %} (see [Stats L9 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s02_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s02_methodestimation-tab5) and [Stats L10 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab4)){% endif %}.

$$\begin{align}\frac 1 n\ell_n(X_1,\dots_,X_n,\theta)&\xrightarrow{\mathbb P}-\text H(\mathcal P_{\theta^\star},\mathcal P_\theta)=-\text H(\mathcal P_{\theta^\star})-\text{KL}(\mathcal P_{\theta^\star},\mathcal P_\theta)\\
\hat\Theta_n=\arg\max_{\theta\in\Theta}\ell_n(X_1,\dots_,X_n,\theta)&\xrightarrow{\mathbb P}\arg\min_{\theta\in\Theta}\text{KL}(\mathcal P_{\theta^\star},\mathcal P_\theta)=\theta^\star\end{align}$$

As for the asymptotic normality, note that the distribution of $$\hat\Theta_n$$ cannot be symmetric if $$\theta^\star$$ sits on the boundary of $$\Theta$$ or if $$\mathcal P_\theta$$ depends on $$\theta$$.

When MLE is constrained to a region $$\Theta\subset\mathbb R^d$$ which does not capture the global maximum (e.g. does not cover the entire $$\mathbb R^d$$ space), then $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\ell_n(X_1,\dots,X_n,\theta)$$ will fall on the boundary of $$\Theta$${% if jekyll.environment == "development" %} (see [Stats HW4 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw4_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw4_u3methods-tab5)){% endif %}, and MLE will not be asymptotically Normal.

## M-estimation

Reviewing MLE, one could say that the estimator was determined as follows:

- define $$\rho(X,\theta)=-\ell(X,\theta)$$ and $$\mathcal Q(\theta)=\mathbb E[\rho(X,\theta)]$$;
- rely on the fact that if $$\rho(X,\theta)$$ is convex in $$\theta$$, then $$\mathcal Q(\theta)$$ is also convex in $$\theta$$;
- define $$\mathcal Q_n(\theta)=\frac 1 n\sum_{i=1}^n\rho(X_i,\theta)$$, a consistent estimator of $$\mathcal Q(\theta)$$;
- find $$\hat\Theta_n$$, that is $$\arg\min_{\theta\in\Theta}\mathcal Q_n(\theta)$$, by solving the equation $$\nabla_\theta\mathcal Q_n(\hat\Theta_n)=0$$.

The above steps can be generalized setting a different **loss function** in the first step. This change will lead to a different minimizer (not limited to $$\theta^\star$$ in $$\mathcal P_{\theta^\star}$$) and this generalized approach is known as **M-estimation** (ME). Flexible approach of the ME can used to approximate relevant quantities of interest *to a distribution*, such as its moments. This flexibility permits its application even outside of parametric statistical models as no statistical model needs to be assumed to perform M-estimation, unlike in the MLE case{% if jekyll.environment == "development" %} (see [Stats L12 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab2)){% endif %}.

||Loss function<br>$$\rho(X,\theta)$$|Minimizer<br>$$\displaystyle\theta^\star=\arg\min_{\theta}\mathcal Q(\theta)$$
|-|:-:|:-:|
|negative log-likelihood|$$-\ell(X,\theta)$$|true parameter of $$X$$|
|quadratic norm|$$\lVert X-\theta\rVert^2_2$$|$$\mathbb E[X]$$|
|absolute value|$$\lvert X-\theta\rvert$$|median $$\text{med}(X)$$<br>($$\frac 1 2$$ quantile of $$X$$)|
|check function|$$C_\alpha(X-\theta)=\begin{cases}\alpha(X-\theta)&X\ge\theta\\(1-\alpha)(\theta-X)&X\lt\theta\end{cases}$$|$$q$$<br>($$\alpha$$ quantile of $$X$$)|

Derivation of $$q$$ as minimizer of $$\mathbb E[C_\alpha(X-\theta)]$$ in the univariate case is as follows, although other derivations can be obtained analogously.

$$\begin{align}
\frac\partial{\partial\theta}\mathbb E[C_\alpha(X-\theta)]&=\frac\partial{\partial\theta}\left(\int_{-\infty}^\theta(1-\alpha)(\theta-x)f(x)dx+\int_{\theta}^\infty\alpha(x-\theta)f(x)dx\right)\\
&=(1-\alpha)\int_{-\infty}^\theta f(x)dx-\alpha\int_\theta^\infty f(x)dx=\mathbb P(X\lt\theta)-\alpha\end{align}$$

Since $$\frac\partial{\partial\theta}\mathbb E[C_\alpha(X-\theta^\star)]=0$$, it follows that $$\mathbb P(X\lt\theta^\star)-\alpha=0$$, which has solution for $$\theta^\star$$ being the $$q$$ of $$X\sim\mathcal P$$. Derivation of $$\text{med}(X)$$ as minimizer of $$\mathbb E[\lvert X-\theta\rvert]$$ can also be obtained by setting the loss function to $$C_{\frac 1 2}(X-\theta)$$, which will lead to $$\arg\min_\theta\frac 1 2\mathbb E[\lvert X-\theta\rvert]=\arg\min_\theta\mathbb E[\lvert X-\theta\rvert]$$.

As for the variance of quantile estimators (including median), consider $$X_i\overset{i.i.d.}{\sim}\mathcal P$$, where $$F_X(x)$$ is the CDF of such $$\mathcal P$$, and $$Y_i=\mathbb 1(X_i\le x)$$. Accordingly, $$Y_i(x)\overset{i.i.d.}{\sim}\text{Ber}(p)$$, where $$p=F_X(x)$$, and its sample mean is distributed as $$\sqrt n(\bar Y_n(x)-p)\xrightarrow{(d)}\mathcal N(0,p(1-p))$$. Considering that $$\frac{\partial p}{\partial x}=f_X(x)$$, it follows that $$\frac{\partial x}{\partial p}=\frac{\partial F_X^{-1}(p)}{\partial p}=\frac1{f_X(x)}$$. Therefore, thanks to [Delta method](/2022/03/24/foundation-of-inference.html#delta) we obtain that $$X_{(np)}$$, that is $$np$$-th order statistic, used as estimator of $$q$$ ($$\alpha$$ quantile of $$X$$), is distributed as follows.

$$\sqrt n(X_{(np)}-q)\xrightarrow{(d)}\mathcal N\left(0,\frac{p(1-p)}{f_X^2(q)}\right)$$

In particular, if we consider $$p=\frac 1 2$$ and $$q=\text{med}(X)$$, we have the following convergence.

$$\sqrt n(X_{\left(\frac n2\right)}-\text{med}(X))\xrightarrow{(d)}\mathcal N\left(0,\frac{1}{4f_X^2(\text{med}(X))}\right)$$

For a practical example consider two particular cases, [Laplace distribution](https://en.wikipedia.org/wiki/Laplace_distribution) (or double exponential) and [Cauchy distribution](https://en.wikipedia.org/wiki/Cauchy_distribution) (or $$t$$-distribution with $$n=1$$){% if jekyll.environment == "development" %} (see [Stats L12 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab6) and [Stats L12 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab8)){% endif %}.

|r.v.|PDF<br>$$f_X(x)$$|Expectation<br>$$\mu_X=\mathbb E[X]$$|Variance<br>$$\sigma_X^2=\text{var}(X)$$|
|-|:-:|:-:|:-:|:-:|
|Laplace<br>$$\text{Laplace}(\mu,\gamma)$$|$$\displaystyle\frac 1 {2\gamma}\exp\left\{-\left\lvert\frac{x-\mu}{\gamma}\right\rvert\right\}$$|$$\mu$$|$$2\gamma^2$$|
|Cauchy<br>$$\text{Cauchy}(\mu,\gamma)$$|$$\displaystyle\frac 1{\pi\gamma}\left(1+\left(\frac{x-\mu}{\gamma}\right)^2\right)^{-1}$$|$$\infty$$|$$\infty$$|

Assuming $$\gamma$$ are known, below are examples of sample median used to estimate $$\mu$$.

|Distribution and unknown parameter|$$\hat\Theta_n$$|$$n\text{var}(\hat\Theta_n)$$|
|-|:-:|:-:|
|$$\text{Laplace}(\mu,\gamma)$$|$$\hat\mu=X_{\left(\frac n 2\right)}$$|$$\gamma^2$$|
|$$\text{Cauchy}(\mu,\gamma)$$|$$\hat\mu=X_{\left(\frac n 2\right)}$$|$$\displaystyle\frac{\pi^2\gamma^2}4$$|

By the same argument applied in case of MLE, one could claim that *mild regularity conditions* allow transferring **consistency** from $$\mathcal Q_n(\theta)$$ to estimator $$\hat\Theta_n=\arg\min_{\theta\in\Theta}\mathcal Q_n(\theta)$${% if jekyll.environment == "development" %} (see [Stats L12 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab3)){% endif %}.

$$\begin{align}\mathcal Q_n(\theta)=\frac 1 n\sum_{i=1}^n\rho(X_i,\theta)&\xrightarrow{\mathbb P}\mathbb E[\rho(X,\theta)]=\mathcal Q(\theta)\\
\hat\Theta_n=\arg\min_{\theta\in\Theta}\mathcal Q_n(\theta)&\xrightarrow{\mathbb P}\arg\min_{\theta\in\Theta}\mathcal Q(\theta)=\theta^\star\end{align}$$

Moving forward, define $$s(\theta)=\nabla_\theta\rho(X,\theta)$$ and replicate the steps carried out with [MLE](/2022/04/26/methods-of-estimation.html#score) to prove that $$\bar s_n(\theta)\xrightarrow{(d)}\mathcal N_d(0,K(\theta))$$, where $$K(\theta)=\text{cov}(s(\theta))$$, and that **asymptotic normality** of ME is given by{% if jekyll.environment == "development" %} (see [Stats L12 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab5)){% endif %}:

$$\sqrt n(\hat\Theta_n-\theta)\xrightarrow{(d)}\mathcal N(0,J^{-1}(\theta)K(\theta)J^{-1}(\theta))$$

In the above relationship, $$J(\theta)=\mathbb E[\mathbf H_\theta\rho(X,\theta)]$$. If $$\rho(X,\theta)=-\ell(X,\theta)$$ then the estimator is the MLE and $$J(\theta)=K(\theta)=I(\theta)$${% if jekyll.environment == "development" %} (see [Stats L12 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab4)){% endif %}. Finally, note that asymptotic normality of ME is subject to:

- $$\theta$$ is the only minimizer of $$\mathcal Q(\theta)$$;
- $$J(\theta)$$ is invertible $$\forall\theta\in\Theta$$; and
- few more technical conditions (see MLE).

Thanks to their generality and efficiency, today ME dominate the field of [robust statistics](https://en.wikipedia.org/wiki/Robust_statistics#M-estimators), which focus on emulating common statistical methods, without being unduly affected by outliers (which often occur in practice, due to data error or measurement limitations). Usually, robust statistics provide methods to find location, scale and regression parameters.

## Huber loss

Asymptotic normality may be difficult to derive when our estimator minimizes a non differentiable function, such as the absolute value. In such case, one could rely on [Huber loss](https://en.wikipedia.org/wiki/Huber_loss) $$h_\delta(x)$$, which can be assimilated to a quadratic function for small values of $$x$$ and linear for large values of $$x$$, as follows{% if jekyll.environment == "development" %} (see [Stats L12 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab7)){% endif %}.

||$$h_\delta(x)$$|$$\frac\partial{\partial x}h_\delta(x)$$|$$\frac{\partial^2}{\partial x^2}h_\delta(x)$$|
||:-:|:-:|:-:|
|definition|$$\begin{cases}\frac 1 2 x^2&\lvert x\rvert\le\delta\\\delta\lvert x\rvert-\frac 1 2\delta^2&\lvert x\rvert\gt\delta\end{cases}$$|$$\begin{cases}x&\lvert x\rvert\le\delta\\\delta\text{sign}(x)&\lvert x\rvert\gt\delta\end{cases}$$|$$\begin{cases}1&\lvert x\rvert\le\delta\\0&\lvert x\rvert\gt\delta\end{cases}$$|
|synonym||$$\text{clip}_\delta(x)$$|$$\mathbb 1(\lvert x\rvert\le\delta)$$|

Accordingly, finding $$\theta^\star=\arg\min_{\theta\in\Theta}\mathbb E[h_\delta(X-\theta)]$$ means finding $$\theta^\star$$ s.t. $$\mathbb E[\text{clip}_\delta(X-\theta^\star)]=0$$. If $$\delta\rightarrow\infty$$, we are minimizing the quadratic norm, and $$\theta^\star=\mathbb E[X]$$ is the solution of $$\mathbb E[(X-\theta^\star)^2]=0$$. On the other hand, if $$\delta\rightarrow 0$$, then we are minimizing the absolute value and $$\theta^\star=\text{med}(X)$$ is the solution of $$\mathbb E[\delta\text{sign}(X-\theta^\star)]=\delta(\mathbb P(X\lt\theta^\star)-\mathbb P(X\ge\theta^\star))=0$$.

Now, we can attempt computing the asymptotic normality (again, in the univariate case) as follows.

$$\Gamma_\delta(\theta)=J^{-1}(\theta)K(\theta)J^{-1}(\theta)=\frac{K(\theta)}{J^2(\theta)}=\frac{\text{var}\left(\frac{\partial}{\partial\theta}h_\delta(X-\theta)\right)}{\left(\mathbb E\left[\frac{\partial^2}{\partial\theta^2}h_\delta(X-\theta)\right]\right)^2}=\frac{\mathbb E\left[(\text{clip}_\delta^2(X-\theta))\right]}{\left(\mathbb E\left[\mathbb 1(\lvert X-\theta\rvert\le\delta)\right]\right)^2}$$

In case of a PDF symmetric around true parameter $$\theta$$, the above can be conveniently rewritten as follows, where $$A=\left\{\lvert X-\theta\rvert\le\delta\right\}$$.

$$\Gamma_\delta(\theta)=\frac{\mathbb E[(X-\theta)^2\lvert A]\mathbb P(A)+\delta^2(1-\mathbb P(A))}{(\mathbb P(A))^2}$$

Let us revisit estimation of the location $$\mu$$ in case of Laplace and Cauchy distributions, by calculating the associated $$\Gamma_\delta(\mu)$$, as well as the two limits ($$\delta\rightarrow0$$ and $$\delta\rightarrow\infty$$) associated with the sample median and sample mean as estimators{% if jekyll.environment == "development" %} (see [Stats L12 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s05_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s05_methodestimation-tab9)){% endif %}.

|Distribution and unknown parameter|$$\Gamma_\delta(\mu)$$|$$\displaystyle\lim_{\delta\rightarrow0}\Gamma_\delta(\mu)$$|$$\displaystyle\lim_{\delta\rightarrow\infty}\Gamma_\delta(\mu)$$|
|-|:-:|:-:|:-:|
|$$\text{Laplace}(\mu,\gamma)$$|$$\displaystyle2e^{\frac\delta\gamma}\frac{\gamma^2(e^{\frac\delta\gamma}-1)-\gamma\delta}{\left(e^{\frac\delta\gamma}-1\right)^2}$$|$$\gamma^2$$|$$2\gamma^2$$|
|$$\text{Cauchy}(\mu,\gamma)$$|$$\displaystyle\frac{\pi^2}4\frac{\delta^2+\frac2\pi(\gamma\delta-(\gamma^2+\delta^2)\arctan\frac\delta\gamma)}{\arctan^2\frac\delta\gamma}$$|$$\displaystyle\frac{\pi^2\gamma^2}4$$|$$\infty$$|

Computations of $$\lim_{\delta\rightarrow0}$$ rely on Taylor expansions, namely $$e^\delta\approx 1+\delta+\frac 1 2\delta^2+O(x^3)$$ and $$\arctan x\approx x-\frac{x^3}3+\frac{x^5}5+O(x^7)$$.

## Wrap-up

In this segment, we saw three main methodologies to develop an estimator. All three of them proved to be **consistent**, and **asymptotically Normal** subject to certain conditions.

Considering performance and robustness against mis-specified models, MLE is usually the first choice for constructing an estimator. However, designing MLE requires solving complex problems and sometimes become intractable. When this happens, MM estimators provide a good alternative as they are simpler to derive. Occasionally, MM cannot be applied, in particular when the expectation does not exist, or when there are challenges in assuming a particular statistic model. In that case, ME can also become an option.

||(G)MM|MLE|ME|
|-|:-:|:-:|:-:|
|Easy to compute|$$\color{green}\checkmark$$|$$\color{red}\times$$|$$\color{red}\times$$|
|Best accuracy (see [Cramér–Rao bound](/2022/04/26/methods-of-estimation.html#cramer-rao))|$$\color{red}\times$$|$$\color{green}\checkmark$$|$$\color{red}\times$$|
|Robust with mis-specified models|$$\color{red}\times$$|$$\color{green}\checkmark$$|$$\color{green}\checkmark$$|
|No need to assume any statistical model|$$\color{red}\times$$|$$\color{red}\times$$|$$\color{green}\checkmark$$|

Final observation is that occasionally we may not be able be able to access the original data, such as $$X\sim\mathcal P_\theta$$, but rather a censored variable like $$Y_i=\mathbb 1(X_i\le y)$$. In such case, it is comforting to know that access to original data will always lead to more accurate estimators, which can be ascertained by observing that $$I_X(\theta)\gt I_Y(\theta)$${% if jekyll.environment == "development" %} (see [Stats HW6 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw6_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw6_u3methods-tab5)){% endif %}.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

|Formula|Equivalent form|
|:-:|:-:|
|$$\prod_{i=1}^n\mathbb 1(X_i\ge\alpha)$$|$$\mathbb 1(X_{(1)}\ge\alpha)$$|
|$$\prod_{i=1}^n\mathbb 1(X_i\le\alpha)$$|$$\mathbb 1(X_{(n)}\le\alpha)$$|
|$$\displaystyle C(k)=\int_0^{\frac\pi2}\cos^k(x)dx$$|$$\displaystyle\left(\frac{k-1}{k}\right)C(k-2)$$, where $$\displaystyle C(0)=\frac\pi2$$|
|L'Hôpital's rule|$$\displaystyle\lim_{x\rightarrow x_0}\frac{f(x)}{g(x)}=\lim_{x\rightarrow x_0}\frac{f'(x)}{g'(x)}$$<br>where $$x_0$$ is point of indetermination|
|Cauchy-Schwartz inequality|$$\begin{align}\left(\int_{\mathbb R^d}f(x)g(x)dx\right)^2\le\int_{\mathbb R^d}\left(f(x)\right)^2dx\int_{\mathbb R^d}\left(g(x)\right)^2dx\end{align}$$|

## Entropy {#entropy}

Assume eight disjoint events $$\Omega=\{A_1,\dots,A_8\}$$, with $$\mathbb P(A_1)=\dots=\mathbb P(A_8)=\frac 1 8$$. In this scenario, an encoder would need $$\log_2(8)=3$$ bits (basic unit of information) to indicate unambiguously which of the eight events has occurred. The term $$\log_2(8)$$ comes from $$-\log_2(\mathbb P(A_i))=-\log_2(\frac 1 8)$$, known as [information content](https://en.wikipedia.org/wiki/Information_content), which indicates the number of bits necessary to assign a different code to $$\frac 1 {\mathbb P(A_i)}$$ separate events.

Therefore this encoder would be using $$3$$ bits for any possible event and the average number of bits per event is also $$\sum_{i=1}^8\mathbb P(A_i)[-\log_2(\mathbb P(A_i))]=3$$. In [information theory](https://en.wikipedia.org/wiki/Information_theory), this quantity is defined as [entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory)) and is denoted as $$\text H(\mathcal P)=\mathbb E_\mathcal P[-\log_2(\mathbb P_\mathcal P(A))]$$, where $$\mathcal P$$ is the uniform distribution across the eight events described above.

Now imagine another encoder, that was designed to indicate $$32$$ different events (including $$8$$ we have seen earlier), with a different uniform distribution $$\mathcal Q$$. The second encoder would need $$5$$ bits to encode unambiguously each event, and for some reason we decide to encode our eight events with this other encoder. If we used the second encoder (which is able to distinguish $$32$$ different events) in the first scenario, average bits used would be $$\sum_{i=1}^8\mathbb P_\mathcal P(A_i)[-\log_2(\mathbb P_\mathcal Q(A_i))]=\sum_{i=1}^8\frac 1 8[-\log_2(\frac 1 {32})]=5$$, which is $$2$$ bits more than entropy of the first encoder.

The latter is called [cross entropy](https://en.wikipedia.org/wiki/Cross_entropy), defined as $$\text H(\mathcal P,\mathcal Q)=\mathbb E_\mathcal P[-\log_2(\mathbb P_\mathcal Q(A))]$$, and the difference between cross entropy and entropy is the [relative entropy](https://en.wikipedia.org/wiki/Kullback–Leibler_divergence), also referred to as the Kullback-Leibler divergence, defined as $$\text{KL}(\mathcal P,\mathcal Q)=\text H(\mathcal P,\mathcal Q)-\text H(\mathcal P)$$, which indicates the **excess** of bits needed to store the information using the second encoder that assumed $$\mathcal Q$$ when the real probabilities are $$\mathcal P$$.

Changing the base of the logarithm does not change the general considerations. In statistics, we usually rely on natural base, or $$\ln(\cdot)$$.

## Lagrange multipliers

Occasionally, [maximization](/2022/04/26/methods-of-estimation.html#maximization) of concave function $$f(\theta) $$ needs to be carried out under constraints, e.g. we need to find $$\max_{\theta\in\Theta}f(\theta)$$, provided that $$g(\theta)=0$$. In such case, instead of looking for a point where $$\nabla_\theta f(\hat\theta_n)=0$$, we look for a point where $$\nabla_\theta f(\hat\theta_n)=\lambda\nabla_\theta g(\hat\theta_n)$$, with $$\lambda\in\mathbb R$$. Accordingly, $$\hat\theta_n$$ is found by solving the following system of equations.

$$\begin{cases}\nabla_\theta f(\hat\theta_n)=\lambda\nabla_\theta g(\hat\theta_n)\\g(\hat\theta_n)=0\end{cases}$$

The above relies on the fact that (a) two vectors $$\mathbf x,\mathbf y\in\mathbb R^d$$ are parallel if $$\mathbf x=\lambda\mathbf y$$, where $$\lambda$$ is defined as **Lagrange multiplier**, and that (b) gradients are perpendicular to contour lines (a curve along which the function has constant value).

For a practical example, consider the Categorical distribution. Assuming $$a_j=\sum_{i=1}^n\mathbb 1(X_i=j)$$ (i.e. number of $$j$$ occurrences, out of $$n$$ draws), we have that $$\ell_n(p)=\sum_{j=1}^d a_j\ln(p_j)$$:

- if we ignore the constraint $$g(p)=\sum_{j=1}^d p_j-1$$, and compute the $$\hat p$$ s.t. $$\nabla_p\ell_n(\hat p)=0$$, we will obtain $$\hat p_j=\infty$$ as the only solution for $$\frac {a_j}{\hat p_j}=0$$;
- if, on the other hand, we compute $$\hat p$$ s.t. $$\nabla_p\ell_n(\hat p)=\nabla_p g(\hat p)$$, then we will obtain $$\hat p_j=\frac {a_j}\lambda$$ and in particular $$\hat p_j=\frac {a_j}n$$, where $$\lambda=n$$ is obtained by plugging $$\hat p$$ in the constraint $$\sum_{j=1}^d\hat p_j=1$$.

Note that if $$a_j\gt0$$ then $$\mathbf H_p\ell_n(p)$$ is negative definite, because it is a diagonal matrix with $$-\frac{a_j}{p_j^2}$$ entries. Therefore, $$\hat p_j=\frac {a_j}n$$ is global maximum. When $$a_j=0$$, $$\mathbf H_p\ell_n(p)$$ is negative **semi**-definite, yet $$\hat p_j=0$$ is still global maximum because $$a_j=0$$ neutralizes the effect of $$\hat p_j=0$$ on $$\ell_n(\hat p)=\sum_{j=1}^d a_j\ln(\hat p_j)$$, while any other $$\hat p_j\gt0$$ will reduce other probabilities and therefore reduce the likelihood.

Final remark is that $$I^{-1}(p)$$ computed this way **will not** coincide with $$\Sigma(\theta)=\text{cov}(\hat\Theta_n)$$. The reason is that the constraint $$g(p)=0$$ reduces the dimensions of $$\Omega$$ from $$d$$ to $$d-1$$. Thus, $$I(\theta)$$ is not invertible in the neighborhood of $$p^\star$$.

$$I^{-1}(p)=\begin{bmatrix}\frac 1 {p_1}&&0\\&\ddots&\\0&&\frac 1 {p_d}\end{bmatrix}^{-1}=\begin{bmatrix}p_1&&0\\&\ddots&\\0&&p_d\end{bmatrix}\neq\begin{bmatrix}p_1(1-p_1)&&-p_1p_d\\&\ddots&\\-p_1p_d&&p_d(1-p_d)\end{bmatrix}=\Sigma(p)$$

A possible workaround is reducing the problem to the search of $$d-1$$ parameters. In such case, $$s(p)$$ and $$I(\theta)$$ are as follows.

|Distribution and unknown parameter|$$s(\theta)=\nabla_\theta\ell(X,\theta)$$|$$I(\theta)=\mathbb E[-\mathbf H_\theta\ell(\theta)]$$|
|-|:-:|:-:|
|Categorical with parameter $$\mathbf p$$|$$\begin{bmatrix}\frac{\mathbb 1(X=1)}{p_1}\\\vdots\\\frac{\mathbb 1(X=d-1)}{p_{d-1}}\end{bmatrix}-\frac{1-\sum_{j=1}^{d-1}{\mathbb 1(X=j)}}{1-\sum_{j=1}^{d-1}p_j}$$|$$\begin{bmatrix}\frac 1{p_1}&&0\\&\ddots&\\0&&\frac 1{p_{d-1}}\end{bmatrix}+\frac 1 {1-\sum_{j=1}^{d-1}p_j}$$|

In case of $$d=3$$, using the above approach we obtain that $$I^{-1}(p)=\Sigma(p)$$, where $$p=(p_1,p_2)$$.

$$I^{-1}(p)=\left(\frac 1 {1-p_1-p_2}\begin{bmatrix}\frac{1-p_2}{p_1}&1\\1&\frac{1-p_1}{p_2}\end{bmatrix}\right)^{-1}=\begin{bmatrix}p_1(1-p_1)&-p_1p_2\\-p_1p_2&p_2(1-p_2)\end{bmatrix}=\Sigma(p)$$

## Power inequalities

Among notable [inequalities](https://en.wikipedia.org/wiki/Inequality_(mathematics)), the following ones are particularly useful (in the context of these notes).

- $$e^x-1\ge x$$, where $$x\in\mathbb R$$
- $$e^x-1\ge x^2$$, where $$x\ge0$$
- $$\frac{x^p-1}{p}\ge\ln(x)\ge\frac{1-\frac 1{x^p}}{p}$$, where $$x,p\gt0$$

For the first one, observe that $$f(x)=e^x-1-x$$ is strictly convex because $$f''(x)=e^x\gt0$$. Also, it has the minimum at $$x=0$$, being as the solution of $$f'(x)=e^x-1=0$$. Therefore, since $$f(0)=0$$, which incidentally is also the global minimum, it follows that at any point, $$e^x-1-x\ge0$$.

For the second, assume $$f(x)=e^x-1-x^2$$ and notice that $$f(0)=0$$ and that $$f'(x)=e^x-2x$$ is always positive because $$f'(x)=\underbrace{1+x+\frac 1 2 x^2+O(x^3)}_{\approx e^x}-2x\gt\frac 1 2\left((1-x)^2+1\right)\gt0$$, $$\forall x\ge0$$.

Regarding the last one, replace $$t=x^p-1$$ and $$s=1-\frac 1{x^p}$$ and observe as follows.

$$\frac{x^p-1}{p}=\underbrace{\frac t{\ln(1+t)}}_{\ge1}\ln(x)\ge\ln(x)\ge\underbrace{\frac{-s}{\ln(1-s)}}_{\le1}\ln(x)=\frac{1-\frac 1{x^p}}{p}$$

Where $$\lim_{t\rightarrow 0^+}\frac{t}{\ln(1+t)}=\lim_{t\rightarrow 0^+}(1+t)\ge1$$, and $$\lim_{s\rightarrow 0^+}\frac{-s}{\ln(1-s)}=\lim_{s\rightarrow 0^+}(1-s)\le1$$ can be derived according to L'Hôpital's rule.

## Cramér–Rao bound {#cramer-rao}

By definition of the unbiased estimator, $$\text{bias}(\hat\Theta_n)=\mathbb E[\hat\Theta_n]-\theta=0$$ and $$\text{var}(\hat\Theta_n)=\mathbb E[\hat\Theta_n^2]$$.

$$\begin{align}
0=\frac\partial{\partial\theta}\text{bias}(\hat\Theta_n)&=\frac\partial{\partial\theta}\left(\int_{-\infty}^\infty\hat\theta_n f_{\theta}(x)dx-\theta\right)=\int_{-\infty}^\infty\hat\theta_n\frac\partial{\partial\theta}f_{\theta}(x)dx-1\\
&=\int_{-\infty}^\infty\hat\theta_n\left(\frac\partial{\partial\theta}\ln f_{\theta}(x)\right)f_{\theta}(x)dx-1\\
&=\int_{-\infty}^\infty\left(\hat\theta_n\sqrt{f_{\theta}(x)}\right)\left(\sqrt{f_{\theta}(x)}\frac\partial{\partial\theta}\ln f_{\theta}(x)\right)dx-1
\end{align}$$

Now, considering [Cauchy–Schwarz inequality](https://en.wikipedia.org/wiki/Cauchy–Schwarz_inequality) for $$L^2$$ spaces, we obtain as follows.

$$\begin{align}
1^2&=\left(\int_{-\infty}^\infty\left(\hat\theta_n\sqrt{f_{\theta}(x)}\right)\left(\sqrt{f_{\theta}(x)}\frac\partial{\partial\theta}\ln f_{\theta}(x)\right)dx\right)^2\\
&\le\int_{-\infty}^\infty\left(\hat\theta_n\sqrt{f_{\theta}(x)}\right)^2dx\int_{-\infty}^\infty\left(\sqrt{f_{\theta}(x)}\frac\partial{\partial\theta}\ln f_{\theta}(x)\right)^2dx\\
&\le\int_{-\infty}^\infty\hat\theta_n^2 f_{\theta}(x)dx \int_{-\infty}^\infty s(\theta)^2f_{\theta}(x)dx=\mathbb E[\hat\Theta_n^2]\mathbb E[s(\theta)^2]=\text{var}(\hat\Theta_n)I(\theta)
\end{align}$$

In conclusion, according to Cramér–Rao bound, $$1\le\text{var}(\hat\Theta_n)I(\theta)$$ or $$\text{var}(\hat\Theta_n)\ge I^{-1}(\theta)$$, which means that no other estimator can do a job more accurately than MLE.

## Location estimation of Cauchy distribution

Deriving the MLE for location parameter $$\mu$$, when $$\gamma=1$$, is straightforward. With the usual process, one obtains that $$\hat\mu$$ is the solution of $$\ell_n'(\hat\mu)=2\sum_{i=1}^n\frac{X_i-\hat\mu}{1+(X_i-\hat\mu)^2}=0$$, which however can only be solved through dedicated algorithms such as [Newton's method](https://en.wikipedia.org/wiki/Newton%27s_method). Associated Fisher information is $$I(\mu)=\frac1{2\gamma^2}$$ (see below derivation).

Alternatively, one can observe that Cauchy distribution is symmetric around $$\mu$$ and therefore consider the median as its estimator. We know that $$X_{\left(\frac n2\right)}\xrightarrow{\mathbb P}\text{med}(X)$$, which has asymptotic variance equal to:

$$\frac1{4f_X^2(\text{med}(X))}=\frac{\pi^2\gamma^2}4$$

Note that $$\frac{\pi^2\gamma^2}4\gt I^{-1}(\mu)=2\gamma^2$$, which is in line with the [Cramér–Rao bound](/2022/04/26/methods-of-estimation.html#cramer-rao). Therefore, the sample median does not seem to be the most efficient estimator, however computation of $$X_{\left(\frac n2\right)}$$ is much easier, if compared with the MLE described above.

To derive Fisher information, recall that $$I(\mu)=\mathbb E[-\ell''(\mu)]$$, where $$\ell''(\mu)=-\frac2{\gamma^2}\frac{1-\left(\frac{X-\mu}\gamma\right)^2}{\left(1+\left(\frac{X-\mu}\gamma\right)^2\right)^2}$$.

$$\begin{align}
I(\mu)
&=\int_{-\infty}^\infty\frac2{\gamma^2}\frac{1-\left(\frac{x-\mu}\gamma\right)^2}{\left(1+\left(\frac{x-\mu}\gamma\right)^2\right)^2}\frac1{\pi\gamma}\frac1{1+\left(\frac{x-\mu}\gamma\right)^2}dx\\
&=\frac2{\pi\gamma^3}\int_{-\infty}^\infty\frac{1-\left(\frac{x-\mu}\gamma\right)^2}{\left(1+\left(\frac{x-\mu}\gamma\right)^2\right)^3}dx&\left(\frac{x-\mu}\gamma=\tan y\right)\\
&=\frac2{\pi\gamma^2}\int_{-\frac\pi2}^{\frac\pi2}\frac{1-\tan^2y}{(1+\tan^2y)^3}\frac1{\cos^2y}dy&\left(\tan^2y=\frac1{\cos^2y}-1\right)\\
&=\frac2{\pi\gamma^2}\int_{-\frac\pi2}^{\frac\pi2}\left(2\cos^4y-\cos^2y\right)dy&\left(C(k)=\int_0^{\frac\pi2}\cos^k(y)dy\right)\\
&=\frac4{\pi\gamma^2}(2C(4)-C(2))&\left(C(k)=\left(\frac{k-1}k\right)C(k-2)\right)\\
&=\frac4{\pi\gamma^2}\left(2\frac 3 4\frac 1 2\frac\pi2-\frac 1 2\frac\pi2\right)=\frac1{2\gamma^2}
\end{align}$$

## Moment generating function