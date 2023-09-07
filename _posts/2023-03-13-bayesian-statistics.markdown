---
layout: post
title: "Bayesian statistics"
---

$$\newcommand{\ind}{\perp\kern-5pt\perp}$$

## Bayesian inference framework

So far, we tackled the inference topic with the *frequentist* approach, which assumes as follows:

- data is random and parameter is fixed, i.e. $$X_i\overset{\text{i.i.d.}}{\sim}\mathcal P_\theta$$, with $$\theta$$ unknown constant; and
- probability is the limiting frequency of an event, e.g. $$\frac1n\sum_{i=1}^n\mathbb P(X_i\le x)\xrightarrow{a.s./\mathbb P}\mathbb P_\theta(X\le x)$$.

**Bayesian statistics** is an alternative approach which gained popularity with the recent advent of computers and the availability of data. Recall that Bayesian inference employs the following [steps](/2022/01/05/conditioning-and-independence.html#main_three_tools):

- based on assumptions, **prior** belief about $$\theta$$ can be modeled as a probability distribution $$\pi(\theta)$${% if jekyll.environment == "development" %} (see [Stats L17 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab5)){% endif %};
- observations conditioned on parameter are modeled as **likelihood**, $$\mathcal L_n(X_1,\dots,X_n\lvert\theta)$$; and
- the **posterior** is obtained by applying the [Bayes' rule](/2023/03/13/bayesian-statistics.html#bayes), $$\pi(\theta\lvert X_1,\dots,X_n)=\frac{\pi(\theta)\mathcal L_n(X_1,\dots,X_n\lvert\theta)}{\mathbb P(X_1,\dots,X_n)}$$.

For ease of notation, $$\mathbf X_n$$ indicates the sequence of observations $$X_1,\dots,X_n$$. Accordingly, once the posterior $$\pi(\theta\lvert\mathbf X_n)$$ is available, two common estimators{% if jekyll.environment == "development" %} (see [Prob L14 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab6)){% endif %} are considered:

- **maximum a posteriori** ([MAP](/2023/03/13/bayesian-statistics.html#map)) estimator, $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\pi(\theta\lvert\mathbf X_n)$$; and
- **least mean square** ([LMS](/2023/03/13/bayesian-statistics.html#lms)) estimator, $$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]$$.

Considering that in the Bayesian framework the parameter is modeled as a r.v., the term $$\Theta$$ may indicate both---the parameter space and the r.v., depending on the circumstances.

## Problem types

Recall that statistical inference starts from the following [three main problems](/2022/03/24/foundation-of-inference.html#trinity): (a) estimation; (b) Confidence Interval; and (c) Hypothesis Testing. The same problems can be addressed in the framework of the Bayesian inference, however as the two frameworks start from philosophically different assumptions, they could yield different results. Arguably, Bayesian inference methods can be used when classical inference methods become too complex or tractable; on the other, they may be more computationally intensive, which explains their stronger traction in the recent times.

Below are some illustrative examples of problem types, divided in two main categories{% if jekyll.environment == "development" %} (see [Prob L14 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab4)){% endif %}: (a) **Hypothesis Testing**, which is generally the case when $$\Theta$$ are discrete, and possibly can take few possible values; and (b) **estimation** when $$\Theta$$ assumes numerical values, including also when $$\Theta$$ is continuous.

||$$\Theta$$ discrete<br>(e.g. Hypothesis Testing)|$$\Theta$$ continuous<br>(e.g. estimation)|
|-|-|-|
|**$$X$$ discrete**|$$\Theta=\{\theta_0,\theta_1\}$$ and $$X\lvert\Theta\sim\text{Bin}(n,\Theta)$$. We design a rule $$(x\ge c)\implies(\hat\Theta_n=\theta_1)$$ and the conditional probability of error is either $$\mathbb P(x\ge c\lvert\Theta=\theta_0)$$ or $$\mathbb P(x\lt c\lvert\Theta=\theta_1)$${% if jekyll.environment == "development" %} (see [Prob PS7a Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7a/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s4-tab2) and [Stats L17 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab6)){% endif %}|$$\Theta\in(0,1)$$ and $$X\lvert\Theta\sim\text{Bin}(n,\Theta)$$. We design an estimator $$\hat\Theta_n$$ and $$\text{MSE}(\hat\Theta_n)=\mathbb E[(\Theta-\hat\Theta_n)^2]$${% if jekyll.environment == "development" %} (see [Prob PS7b Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7b/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s7-tab2)){% endif %}|
|**$$X$$ continuous**|$$\Theta=\{\theta_0,\theta_1\}$$ and $$X\lvert\Theta\sim\mathcal N(\Theta,\sigma^2)$$. We design a rule $$(x\ge c)\implies(\hat\Theta_n=\theta_1)$$ and the conditional probability of error is either $$\mathbb P(x\ge c\lvert\Theta=\theta_0)$$ or $$\mathbb P(x\lt c\lvert\Theta=\theta_1)$${% if jekyll.environment == "development" %} (see [Prob PS7a Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7a/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s4-tab3), [Prob PS7a Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7a/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s4-tab5) and [Prob PS7b Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7b/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s7-tab1)){% endif %}|$$\Theta\in(0,1)$$ and $$X\lvert\Theta\sim\mathcal N(\Theta,\sigma^2)$$. We design an estimator $$\hat\Theta_n$$ and $$\text{MSE}(\hat\Theta_n)=\mathbb E[(\Theta-\hat\Theta_n)^2]$${% if jekyll.environment == "development" %} (see [Prob PS7b Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7b/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s7-tab5)){% endif %}|

Hypothesis testing usually rely on [MAP](/2023/03/13/bayesian-statistics.html#map) estimator, mainly because MAP estimators result in the lowest possible probability of error. Estimation, on the other hand, can rely on either [MAP](/2023/03/13/bayesian-statistics.html#map), [LMS](/2023/03/13/bayesian-statistics.html#lms), or even LLMS, depending on our objective and bearing in mind that LMS is the estimator with lowest MSE.

Note that computations of probability of error $$\mathbb P(\text{error})=\mathbb P(\Theta\neq\hat\Theta_n)$$, and mean square error $$\text{MSE}(\hat\Theta_n)=\mathbb E[(\Theta-\hat\Theta_n)^2]$$ benefit from the [total probability / total expectation theorem](/2022/01/05/conditioning-and-independence.html#main_three_tools).

$$\mathbb P(\Theta\neq\hat\Theta_n)=\begin{cases}
\displaystyle\sum_x\mathbb P(\Theta\neq\hat\theta_n\lvert X=x)p_X(x)&\text{$X$ discrete}\\
\displaystyle\int_x\mathbb P(\Theta\neq\hat\theta_n\lvert X=x)f_X(x)dx&\text{$X$ continuous}
\end{cases}$$

Probability of error can also be computed as $$\mathbb P(\text{error})=\sum_\theta\mathbb P(\text{error}\lvert\Theta=\theta)\pi(\theta)$$, which becomes handy in case of Hypothesis Testing (i.e., $$\Theta$$ is discrete and can take few values){% if jekyll.environment == "development" %} (see [Prob L14 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab10)){% endif %}.

## Bayes' rule {#bayes}

By replacing events with r.v. in the basic [Bayes' rule](/2022/01/05/conditioning-and-independence.html#main_three_tools), the following general form can be obtained, which represents the posterior belief regarding parameter $$\Theta$$ after a single observation $$X$$.

$$\pi(\theta\lvert X)=\frac{\pi(\theta)\mathcal L_1(X\lvert\theta)}{\mathbb P(X)}$$

The denominator $$\mathbb P(X)$$ is referred to as the [marginal likelihood](https://en.wikipedia.org/wiki/Marginal_likelihood) and it represents the probability of observing $$X$$ from priori $$\pi(\theta)$$. Marginal distribution can be computed using [total probability theorem](/2022/01/05/conditioning-and-independence.html#main_three_tools), as either $$\mathbb P(X)=\sum_{\theta\in\Theta}\pi(\theta)\mathcal L_1(X\lvert\theta)$${% if jekyll.environment == "development" %} (see [Prob L10 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab17), [Prob L10 Q20](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab20) and [Prob PS5 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab6)){% endif %}, or $$\mathbb P(X)=\int_{\Theta}\pi(\theta)\mathcal L_1(X\lvert\theta)d\theta$${% if jekyll.environment == "development" %} (see [Prob L10 Q22](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__10_Conditioning_on_a_random_variable__Independence__Bayes_rule/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s4-tab22)){% endif %}, depending on whether $$\Theta$$ is discrete or continuous.

In case of $$X_i$$ discrete, the likelihood is a product of PMF $$\mathcal L_n(\mathbf X_n\lvert\theta)=\prod_{i=1}^n p_{X_i\lvert\Theta}(x\lvert\theta)$$ (or of PDF $$f_{X_i\lvert\Theta}(x\lvert\theta)$$ if $$X_i$$ continuous). Therefore, the posterior after $$n$$ observations becomes the following.

$$\pi(\theta\lvert \mathbf X_n)=\frac{\pi(\theta)\mathcal L_n(\mathbf X_n\lvert\theta)}{\mathbb P(\mathbf X_n)}$$

Furthermore, because the likelihood of i.i.d. observations is the product of individual likelihoods, that is $$\mathcal L_n(\mathbf X_n\lvert\theta)=\mathcal L_{n-1}(\mathbf X_{n-1}\lvert\theta)\mathcal L_1(X_n\lvert\theta)$$, we conclude that our belief about the distribution of $$\Theta$$ updates with every new observation, $$\pi(\theta\lvert \mathbf X_n)\propto\pi(\theta\lvert\mathbf X_{n-1})\mathcal L_1(X_n\lvert\theta)$${% if jekyll.environment == "development" %} (see [Prob PS7a Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7a/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s4-tab1) and [Stats L17 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab10)){% endif %}.

## MAP estimation {#map}

Maximum a posteriori (MAP) estimator is defined as $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\pi(\theta\lvert \mathbf X_n)$$ and since the marginal likelihood $$\mathbb P(X)$$ does not depend on $$\theta$$, we observe that $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\pi(\theta)\mathcal L_n(\mathbf X_n\lvert\theta)$$. Hence, under proper technical conditions on $$\pi(\theta\lvert\mathbf X_n)$$, $$\hat\Theta_n$$ is the solution of $$\frac\partial{\partial\theta}\pi(\theta)\mathcal L_n(\mathbf X_n\lvert\theta)=0$${% if jekyll.environment == "development" %} (see [Prob PS7a Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7a/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s4-tab4)){% endif %}. Note that the same optimization can be performed in the log-space as well, where the posterior can be simplified up to a normalizing constant, which is irrelevant in the optimization process{% if jekyll.environment == "development" %} (see [Stats L17 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab8)){% endif %}.

Finally, recall that [MLE](/2022/04/26/methods-of-estimation.html#mle) is $$\hat\Theta_n=\arg\max_{\theta\in\Theta}\mathcal L_n(\mathbf X_n,\theta)$$, therefore MLE is MAP with $$\pi(\theta)=1$$, and may also read this as if MAP were a [regularization](https://en.wikipedia.org/wiki/Maximum_a_posteriori_estimation) of MLE. Incidentally, while MLE is the most [efficient estimator](/2022/04/26/methods-of-estimation.html#wrapup), MAP results in the smallest probability of error. By definition, $$\pi(\hat\theta_n\lvert\mathbf x_n)$$ is highest with MAP that means that $$\mathbb P(\Theta\neq\hat\theta_n\lvert\mathbf x_n)=1-\pi(\hat\theta_n\lvert\mathbf x_n)$$ is the **smallest with MAP** for any given $$\mathbf X_n=\mathbf x_n$$.

Before moving on, estimators determined based on the joint posterior $$\pi(\boldsymbol{\theta}\lvert\mathbf X_n)$$ when $$\boldsymbol{\Theta}\in\mathbb R^d$$ may differ from the individual estimator components obtained from the posterior's marginal distributions{% if jekyll.environment == "development" %} (see [Prob L14 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab8)){% endif %}.

## LMS estimation {#lms}

Considering that expectation [minimizes](/2022/04/26/methods-of-estimation.html#me) the quadratic norm, or $$\mathbb E[\Theta]=\arg\min_{\theta}\mathbb E\left[\lVert\Theta-\theta\rVert_2^2\right]$$, we conclude that in the conditional universe the alternative estimator candidate can be as follows, referred to as the least mean  (LMS).

$$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]=\arg\min_{\theta}\mathbb E\left[\lVert\Theta-\theta\rVert_2^2\lvert\mathbf X_n\right]$$

By generalizing its [definition](/2022/03/24/foundation-of-inference.html#estimation), consider $$\text{MSE}(\hat\Theta_n\lvert\mathbf X_n)=\mathbb E[(\hat\Theta_n-\Theta)^2\lvert\mathbf X_n]$$ and observe that in the conditional universe $$\text{MSE}(\hat\Theta_n\lvert\mathbf X_n)=\text{var}(\Theta\lvert\mathbf X_n)$$, because contrary to classical statistics, in the Bayesian framework $$\Theta$$ is a r.v. and $$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]$$ is a constant{% if jekyll.environment == "development" %} (see [Prob L16 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__16_Least_mean_squares__LMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s5-tab4) and [Prob Q16 L8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__16_Least_mean_squares__LMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s5-tab8)){% endif %}. Furthermore, as $$\text{MSE}(\hat\Theta_n\lvert\mathbf X_n)=\text{var}(\hat\Theta_n-\Theta\lvert\mathbf X_n)+\text{bias}^2(\hat\Theta_n\lvert\mathbf X_n)$$, for any fixed $$\mathbf X_n=\mathbf x_n$$, $$\text{MSE}(\hat\Theta_n\lvert\mathbf X_n)$$ is the **smallest with the LMS**{% if jekyll.environment == "development" %} (see [Prob L14 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab12)){% endif %}, because $$\text{bias}(\hat\Theta_n\lvert\mathbf X_n)=0$$ and $$\text{var}(\hat\Theta_n-\Theta\lvert\mathbf X_n)=\text{var}(\Theta\lvert\mathbf X_n)$$ does not depend on the estimator. By the [law of total expectations](/2022/01/24/further-topics-on-RV.html#total_expectation), $$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]$$ is the minimizer of $$\text{MSE}(\hat\Theta_n)=\mathbb E[\text{var}(\Theta\lvert\mathbf X_n)]$${% if jekyll.environment == "development" %} (see [Prob L16 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__16_Least_mean_squares__LMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s5-tab6) and [Prob L16 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__16_Least_mean_squares__LMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s5-tab10)){% endif %}.

It is worth noting that even though $$\mathbb E[\Theta\lvert\mathbf X_n]$$ involves an ordinary (univariate) integral, $$\mathbb E[\text{var}(\Theta\lvert\mathbf X_n)]$$ requires computing a multiple integral, because we need to compute the variance over all possible combinations of $$\mathbf x_n\in\mathbb R^n$${% if jekyll.environment == "development" %} (see [Prob L16 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__16_Least_mean_squares__LMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s5-tab12)){% endif %}. If $$\boldsymbol{\Theta}_n\in\mathbb R^d$$, then LMS is applied to each component separately, $$\hat{\boldsymbol{\Theta}}_{n,j}=\mathbb E[\Theta_j\lvert\mathbf X_n]$$, which in turn needs us computing the marginal distribution $$\pi(\theta_j\lvert\mathbf X_n)$$.

Assuming $$\tilde\Theta=\hat\Theta_n-\Theta$$, observe that $$\mathbb E[\tilde\Theta\lvert\mathbf X_n]=0$$, $$\mathbb E[\tilde\Theta]=\mathbb E[\mathbb E[\tilde\Theta\lvert\mathbf X_n]]=0$$, $$\text{var}(\tilde\Theta)=\mathbb E[\tilde\Theta^2]$$, which by the earlier definition is essentially $$\text{MSE}(\hat\Theta_n)=\mathbb E[\text{var}(\Theta\lvert\mathbf X_n)]$$. Also, considering that $$\text{cov}(\hat\Theta_n,\tilde\Theta)=\mathbb E[\mathbb E[\hat\Theta_n \tilde\Theta\lvert\mathbf X_n]]-\mathbb E[\hat\Theta_n]\cancel{\mathbb E[\tilde\Theta]}=\mathbb E[\hat\Theta_n\cancel{\mathbb E[\tilde\Theta\lvert\mathbf X_n]}]=0$$, we have the following relationship{% if jekyll.environment == "development" %} (see [Prob L16 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__16_Least_mean_squares__LMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s5-tab14)){% endif %}, which on one hand confirms the [law of total variation](/2022/01/24/further-topics-on-RV.html#total_expectation), on the other provides an alternative bias-variance decomposition.

$$\begin{align}
\text{var}(\Theta)
&=\text{var}(\hat\Theta_n-\tilde\Theta)=\text{var}(\hat\Theta_n)+\text{var}(\tilde\Theta)-2\cancelto{=0}{\text{cov}(\hat\Theta_n,\tilde\Theta)}\\
&=\text{var}(\mathbb E[\Theta\lvert\mathbf X_n])+\mathbb E[\text{var}(\Theta\lvert\mathbf X_n)]
\end{align}$$

Finally, MAP and LMS coincide if the **posterior** is unimodal and symmetric (e.g., Normally distributed). Among the two, LMS is usually preferred for the estimation problems. Indeed, it is often referred to as the **Bayesian estimator**{% if jekyll.environment == "development" %} (see [Stats MT2 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm2-tab7)){% endif %}.

## Choice of the prior

The ability to chose a **prior** is the main characteristic that distinguishes the Bayesian statistics from the frequentist approach{% if jekyll.environment == "development" %} (see [Stats L17 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab3)){% endif %}. As the term suggests, the latter assumes the possibility of potentially repeating exactly the same experiment times, to obtain a sufficiently narrow confidence interval, based on which draw its own conclusion. Bayesian statistics tries to approach a different set of problems, including cases when **only one experiment is available**, in which case concepts like frequency become inapplicable.

In case of classical statistics we started from the [statistical model](/2022/03/24/foundation-of-inference.html#model), by setting constraints such as observations being i.i.d. and by making assumptions about the underlying distributions. For the Bayesian statistics the extra element we are adding is the [prior](https://en.wikipedia.org/wiki/Prior_probability) (and posterior) distribution, which we are able to update through observations. It seems obvious at this point that Bayesian statistics are most effective when experts have a lot of prior knowledge about a particular phenomenon{% if jekyll.environment == "development" %} (see [Stats L17 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab9)){% endif %}. Choosing a prior may be influenced by various factors, and the following ones could be used as an initial (non exhaustive) point of consideration.

- **Earlier studies** may have allowed building some prior belief regarding the unknown parameter $$\theta$$. To this end, an understanding of the known range (or support of $$\theta$$) allows us setting probability equal to zero for any $$\theta$$ outside that range{% if jekyll.environment == "development" %} (see [Stats L18 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab10)){% endif %} and the prior can also be made more flexible if it can be described with a parametric probability law. Finally, additional observations will refine that existing knowledge{% if jekyll.environment == "development" %} (see [Stats L18 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab2)){% endif %};
- **Conjugate priors** that have the property of belonging to the same family of distributions as the posterior. This is attractive as it allows some analytical computation of the posterior distribution (e.g. mean or mode), in a computationally convenient way.
- **Non-informative priors**, which could be based either on a simple *symmetry argument* (i.e., when there is a number of possible choices and there is no reason to believe one particular choice is more likely than the other), leading to a uniform prior or Jeffreys prior; and

On the other hand, as the additional observations update the prior and give place to a posterior, it follows that different choices of the prior may lead to a different posterior, and therefore different estimators and conclusions, despite the observations are the same{% if jekyll.environment == "development" %} (see [Stats L17 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab7)){% endif %}. This is the main historical criticism moved against the Bayesian statistics, although for $$n\rightarrow\infty$$ the difference between two estimators (e.g. MAP and MLE) vanishes. For this reason, some of the asymptotic frequentist properties of a Bayesian estimator (i.e. [consistency and asymptotic normality, but not bias](/2022/03/24/foundation-of-inference.html#estimation)) are the same as those of the MLE to which it will converge{% if jekyll.environment == "development" %} (see [Stats HW9 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw9_u5bayes/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw9_u5bayes-tab5)){% endif %}.

### Conjugate priors

The main convenience of a conjugate prior is the possibility of obtaining a closed-form of the posterior, thus avoiding numerical integration to compute the normalizing constant. Below are some basic examples.

|Prior|Likelihood<br>([Discrete](/2022/01/08/discrete-random-variables.html#basic))|Posterior|
|:-:|:-:|:-:|
|$$P\sim\text{Beta}(\alpha,\beta)$$|$$\text{Ber}(p)$$|$$\text{Beta}(\alpha+\sum_{i=1}^n X_i,\beta+n-\sum_{i=1}^n X_i)$${% if jekyll.environment == "development" %}<br>(see [Prob L14 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab14), [Prob L14 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__14_Introduction_to_Bayesian_inference/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s2-tab16) and [Stats L17 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab4)){% endif %}|
|$$P\sim\text{Beta}(\alpha,\beta)$$|$$\text{Bin}(k,p)$$|$$\text{Beta}(\alpha+\sum_{i=1}^n X_i,\beta+nk-\sum_{i=1}^n X_i)$$|
|$$P\sim\text{Beta}(\alpha,\beta)$$|$$\text{Geom}(p)$$|$$\text{Beta}(\alpha+n,\beta+\sum_{i=1}^n X_i-n)$$|
|$$P\sim\text{Beta}(\alpha,\beta)$$|$$\text{NBin}(k,p)$$|$$\text{Beta}(\alpha+nk,\beta+\sum_{i=1}^n X_i-nk)$$|
|$$\mathbf P\sim\text{Dir}(\boldsymbol{\alpha})$$|$$\text{Cat}(\mathbf p)$$|$$\text{Dir}(\boldsymbol{\alpha}+\sum_{i=1}^n\mathbf X_i)$$|
|$$\mathbf P\sim\text{Dir}(\boldsymbol{\alpha})$$|$$\text{Mult}(k,\mathbf p)$$|$$\text{Dir}(\boldsymbol{\alpha}+\sum_{i=1}^n\mathbf X_i)$$|
|$$\Lambda\sim\text{Gamma}(\alpha,\beta)$$|$$\text{Pois}(\lambda)$$|$$\text{Gamma}(\alpha+\sum_{i=1}^n X_i,\beta+n)$$|

|Prior|Likelihood<br>([Continuous](/2022/01/13/continuous-random-variables.html#basic))|Posterior|
|:-:|:-:|:-:|
|$$\Lambda\sim\text{Gamma}(\alpha,\beta)$$|$$\text{Exp}(\lambda)$$|$$\text{Gamma}(\alpha+n,\beta+\sum_{i=1}^n X_i)$${% if jekyll.environment == "development" %}<br>(see [Stats L17 Q11](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s1_Bayes1/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s1_Bayes1-tab11)){% endif %}|
|$$M\sim\mathcal N(\mu_0,\sigma_0^2)$$|$$\mathcal N(\mu,\sigma_i^2)$$<br>$$\sigma_i^2$$ known|$$\displaystyle\mathcal N\left(\frac{\sum_{i=0}^n\frac{\mu_i}{\sigma_i^2}}{\sum_{i=0}^n\frac1{\sigma_i^2}},\frac1{\sum_{i=0}^n\frac1{\sigma_i^2}}\right)$${% if jekyll.environment == "development" %}<br>(see [Stats L18 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab5)){% endif %}|
|[$$\Sigma^2\sim\text{InvGamma}(\alpha,\beta)$$](/2023/03/13/bayesian-statistics.html#invgamma)|$$\mathcal N(\mu,\sigma^2)$$<br>$$\mu$$ known|$$\displaystyle\text{InvGamma}\left(\alpha+\frac n2,\beta+\frac{\sum_{i=1}^n(X_i-\mu)^2}2\right)$$|

Feel free to refer to the [linear model](/2023/06/30/linear-regression.html#lm) with Normal noise for the derivation of the posterior if the prior and likelihood are both Normal.

Considering that the posterior have the form of well known distributions, they provide closed-form expressions for [MAP](/2023/03/13/bayesian-statistics.html#map) and [LMS](/2023/03/13/bayesian-statistics.html#lms) estimators, where the choice of the estimator may depend on whether the objective is minimizing the expected error or the MSE, respectively. In case the requirement is minimizing the expected absolute distance, median is an [appropriate estimator](/2022/04/26/methods-of-estimation.html#me){% if jekyll.environment == "development" %} (see [Stats HW9 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw9_u5bayes/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw9_u5bayes-tab2)){% endif %}.

|Posterior|MAP (mode)<br>$$\hat\Theta_n=\arg\max_\theta\pi(\theta\lvert\mathbf X_n)$$|[LMS](/2022/01/13/continuous-random-variables.html#basic) (mean)<br>$$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]$$|
|:-:|:-:|:-:|
|$$\mathcal N(\mu,\sigma^2)$$|$$\mu$$|$$\mu$$|
|$$\text{Beta}(\alpha,\beta)$$|[$$\displaystyle\frac{(\alpha-1)}{(\alpha-1)+(\beta-1)}$$](/2023/03/13/bayesian-statistics.html#beta)<br>for $$\alpha\gt1$$ and $$\beta\gt1$$|$$\displaystyle\frac\alpha{\alpha+\beta}$$|
|$$\text{Dir}(\boldsymbol{\alpha})$$|[$$\displaystyle\frac{\boldsymbol{\alpha}-1}{\alpha_0-d}$$](/2023/03/13/bayesian-statistics.html#dirichlet)<br>for $$\boldsymbol{\alpha}\gt\mathbf1_d$$|$$\displaystyle\frac{\boldsymbol{\alpha}}{\alpha_0}$$|
|$$\text{Gamma}(\alpha,\beta)$$|[$$\displaystyle\frac{\alpha-1}\beta$$](/2022/01/13/continuous-random-variables.html#gamma)<br>for $$\alpha\ge1$$|$$\displaystyle\frac\alpha\beta$$|
|$$\text{InvGamma}(\alpha,\beta)$$|[$$\displaystyle\frac\beta{\alpha+1}$$](/2023/03/13/bayesian-statistics.html#invgamma)|$$\displaystyle\frac\beta{\alpha-1}$$<br>for $$\alpha\gt1$$|

It is a common convention that to be a conjugate prior, the prior should not be a *strict* subset of probability distribution families. For this, a conjugate prior is easier obtained when the prior has a more general distribution parametrization and the likelihood has a more specific form{% if jekyll.environment == "development" %} (see [Stats HW9 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw9_u5bayes/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw9_u5bayes-tab1)){% endif %}.

### Non-informative priors

As opposed to a prior based on existing knowledge, non-informative (or objective) priors do not incorporate any subjective or expert knowledge, and they do not favor any particular value or range of values. Non-informative priors may be chosen to avoid affecting conclusions that can be drawn from the observations alone (i.e. when the data is expected to be highly informative) or because the prior information is weak or nonexistent. As non-informative priors reflect frequentist properties of Bayesian estimators (consider [Jeffreys priors](/2023/03/13/bayesian-statistics.html#jeffreys_prior) relying on Fisher information), they are considered the bridging element between the frequentist and Bayesian approaches{% if jekyll.environment == "development" %} (see [Stats HW9 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw9_u5bayes/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw9_u5bayes-tab4)){% endif %}.

### Uniform prior {#uniform_prior}

A trivial choice of non-informative prior is the a uniform PDF over the entire $$\Theta$$, that is $$\pi(\theta)\propto1$$. If cardinality of $$\Theta$$ is infinite, this will be an **improper prior**, because if $$\pi(\theta)=k\gt0$$ for $$\theta\in\mathbb R$$, then $$\int_\Theta\pi(\theta)d\theta=\infty\neq1$$. However, improper priors are acceptable, as far as the posterior is proper. Indeed, if $$\pi(\theta)=1$$ then [MAP](/2023/03/13/bayesian-statistics.html#map) estimator coincides with [MLE](/2022/04/26/methods-of-estimation.html#mle){% if jekyll.environment == "development" %} (see [Stats L18 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab3) and [Stats L18 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab4)){% endif %}, which is completely fine. The uniform prior is particularly justified when the parameter space $$\Theta$$ is discrete. Assume $$\Theta=\{\theta_i\}$$ and $$p_\theta(\theta_i)=\frac1k$$ for $$i=1,\dots,k$$. Note that if we replace the original parameter $$\theta_i=h(\eta_i)$$, with $$h(\cdot)$$ invertible, the new parameter space $$H=\{\eta_1,\dots,\eta_k\}$$ would still be characterized by *no-preference* as $$p_\eta(\eta_i)=p_\theta(h(\eta_i))=\frac1k$$. In other words, regardless of the parameter space, $$\Theta$$ or $$H$$, we there is no-preference for any particular value of $$\theta$$ or $$\eta$$.

### Jeffreys prior {#jeffreys_prior}

When $$\Theta$$ is continuous, conservation of the above no-preference principle as described above cannot be taken for granted. Assume $$\theta\in[0,1]$$ and $$\pi(\theta)=1$$. If $$\theta=h(\eta)=\frac1{1+e^{-\eta}}$$, with $$h(\cdot)$$ invertible, a prior PDF of $$\eta$$ can be [derived](/2022/01/24/further-topics-on-RV.html#derived_distributions) as $$\tilde\pi(\eta)=\pi(h(\eta))\cdot\left\lvert\frac\partial{\partial\eta}h(\eta)\right\rvert=1\cdot\frac{e^{-\eta}}{(1+e^{-\eta})^2}$$ which is not uniform over $$H\subseteq\mathbb R$$. To address this, Jeffreys proposed that an acceptable non-informative prior should remain invariant under monotone transformations of the parameter. In particular, we say that $$\pi(\theta)$$ is **Jeffreys prior** if for $$X\sim f(x\lvert\theta)$$ and $$\theta=h(\eta)$$, $$X\sim f(x\lvert h(\eta))$$ and $$\tilde\pi(\eta)=\pi(h(\eta))\left\lvert\frac\partial{\partial\eta}h(\eta)\right\rvert$$, obtained via [derivation](/2022/01/24/further-topics-on-RV.html#derived_distributions){% if jekyll.environment == "development" %} (see [Stats L18 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab8)){% endif %}.

It turns out that the prior that satisfies such principle has the form of $$\pi(\theta)\propto\sqrt{I(\theta)}$$, with $$I(\theta)$$ being [Fisher information](/2022/04/26/methods-of-estimation.html#score). To see why, recall that $$s(\theta)=\frac\partial{\partial\theta}\ell(\theta)$$ and assume $$\theta=h(\eta)$$, with $$h(\cdot)$$ invertible. Re-parametrized score function can be obtained by applying the [chain rule](https://en.wikipedia.org/wiki/Chain_rule).

$$\tilde s(\eta)=\frac\partial{\partial\eta}\ell(h(\eta))=s(h(\eta))\frac\partial{\partial\eta}h(\eta)$$

Re-parametrized Fisher information is derived accordingly.

$$\begin{align}
\tilde I(\eta)
&=\mathbb E[\tilde s^2(\eta)]=\mathbb E\left[\left(s(h(\eta))\frac\partial{\partial\eta}h(\eta)\right)^2\right]\\
&=\mathbb E[s^2(h(\eta))]\left(\frac\partial{\partial\eta}h(\eta)\right)^2=I(h(\eta))\left(\frac\partial{\partial\eta}h(\eta)\right)^2
\end{align}$$

From the above, it follows that $$\sqrt{\tilde I(\eta)}=\sqrt{I(h(\eta))}\left\lvert\frac\partial{\partial\eta}h(\eta)\right\rvert$$ satisfies $$\tilde\pi(\eta)=\pi(h(\eta))\left\lvert\frac\partial{\partial\eta}h(\eta)\right\rvert$$.

Furthermore, one realizes that Jeffreys prior $$\pi(\theta)$$ is indeed uniform over the parameter space $$\Theta$$, just not under the Euclidean geometry. Recall that Fisher information is the inverse of the MLE asymptotic variance, if it exists. This means that for any given $$\alpha$$, we can fix an interval $$\mathcal I$$ s.t. $$\mathbb P(\theta\in\mathcal I)\ge1-\alpha$$, with $$\mathcal I=\left\{\hat\Theta_n-q_{\frac\alpha2}\text{var}(\hat\Theta_n),\hat\Theta_n+q_{\frac\alpha2}\text{var}(\hat\Theta_n)\right\}$$ and $$\text{var}(\hat\Theta_n)=(nI(\hat\Theta_n))^{-\frac12}$$, or essentially a [CI](/2022/03/24/foundation-of-inference.html#ci) of level $$\alpha$$ in the classical statistics view.

It follows that the width of $$\mathcal I$$ will be narrower where Fisher information is higher and *vice-versa* wider where Fisher information is lower. At the same time, as $$n\rightarrow\infty$$, we have that $$\hat\Theta_n\xrightarrow{\mathbb P}\theta$$ and the curve $$\sqrt{I(\hat\Theta_n)}$$ becomes approximately constant over the entire interval $$\mathcal I$$. In conclusion, the area under the aforementioned curve is also approximately constant, no matter where $$\hat\Theta_n$$ is placed, and no mater what parametrization is used{% if jekyll.environment == "development" %} (see [Stats L18 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab6)){% endif %}.

Note that changing parametrization was not an issue in the classical statistics framework; the reason being that if the unknown $$\theta$$ is [identifiable](/2022/03/24/foundation-of-inference.html#model), there is no particular concern in finding a different parameter $$\eta^\star=h^{-1}(\theta)$$, as far as $$h(\cdot)$$ is a one-to-one map{% if jekyll.environment == "development" %} (see [Stats HW9 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw9_u5bayes/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw9_u5bayes-tab3)){% endif %}.

Finally, if $$\boldsymbol{\theta}\in\mathbb R^d$$, then $$\pi_\theta(\boldsymbol{\theta})\propto\sqrt{\det(I(\boldsymbol{\theta}))}$${% if jekyll.environment == "development" %} (see [Stats L18 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab7)){% endif %}. An intuitive explanation comes from the fact that at the asymptote an MLE $$\hat{\boldsymbol{\Theta}}_n$$ is distributed according to $$\mathcal N_d(\boldsymbol{\theta},I^{-1}(\boldsymbol{\theta}))$$. This means that $$f_{\hat{\boldsymbol{\Theta}}_n}(\boldsymbol{\theta})=\sqrt{(2\pi)^{-d}\det(I(\boldsymbol{\theta}))}\propto\sqrt{\det(I(\boldsymbol{\theta}))}$$.

Follow few examples of Jeffreys priors for some common distributions{% if jekyll.environment == "development" %} (see [Stats MT2 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm2-tab3)){% endif %}. Even though conjugate and Jeffreys priors are not strictly related, the wide generality of conjugate priors allows interpreting Jeffreys priors as limiting functions of the conjugate families---which, again, facilitates computing the various estimators (MAP, LMS, media) based on the newly observed data.

|Likelihood|Jeffreys Prior|Proper|Conjugate analogy (if exists)|
|:-:|:-:|:-:|:-:|
|$$\text{Ber}(p)$$|$$\displaystyle\pi(p)\propto\frac1{\sqrt{p(1-p)}}$$|$$\color{green}\checkmark$$|$$\displaystyle\text{Beta}\left(\frac12,\frac12\right)$$|
|$$\text{Bin}(k,p)$$|$$\displaystyle\pi(p)\propto\frac1{\sqrt{p(1-p)}}$$|$$\color{green}\checkmark$$|$$\displaystyle\text{Beta}\left(\frac12,\frac12\right)$$|
|$$\text{Cat}(\mathbf p)$$|$$\displaystyle\pi(\mathbf p)\propto\prod_{j=1}^d\frac1{\sqrt{p_j}}$$|$$\color{green}\checkmark$$|$$\displaystyle\text{Dir}\left(\frac12\mathbf 1_d\right)$$|
|$$\text{Mult}(k,\mathbf p)$$|$$\displaystyle\pi(\mathbf p)\propto\prod_{j=1}^d\frac1{\sqrt{p_j}}$$|$$\color{green}\checkmark$$|$$\displaystyle\text{Dir}\left(\frac12\mathbf 1_d\right)$$|
|$$\text{Geom}(p)$$|$$\displaystyle\pi(p)\propto\frac1{p\sqrt{1-p}}$$|$$\color{red}\times$$|$$\displaystyle\lim_{\alpha\to0}\text{Beta}\left(\alpha,\frac12\right)$$|
|$$\text{NBin}(k,p)$$|$$\displaystyle\pi(p)\propto\frac1{p\sqrt{1-p}}$$|$$\color{red}\times$$|$$\displaystyle\lim_{\alpha\to0}\text{Beta}\left(\alpha,\frac12\right)$$|
|$$\text{Pois}(\lambda)$$|$$\displaystyle\pi(\lambda)\propto\frac1{\sqrt{\lambda}}$$|$$\color{red}\times$$|$$\displaystyle\lim_{\beta\to0}\text{Gamma}\left(\frac12,\beta\right)$$|
|$$\text{Exp}(\lambda)$$|$$\displaystyle\pi(\lambda)\propto\frac1{\lambda}$$|$$\color{red}\times$$|$$\displaystyle\lim_{\alpha,\beta\to0}\text{Gamma}\left(\alpha,\beta\right)$$|
|$$\mathcal N(\mu,\sigma^2)$$<br>$$\sigma^2$$ known|$$\displaystyle\pi(\mu)\propto1$$|$$\color{red}\times$$|$$\displaystyle\lim_{\tau\to\infty}\mathcal N(0,\tau)$$|
|$$\mathcal N(\mu,\sigma^2)$$<br>$$\mu$$ known|$$\displaystyle\pi(\sigma^2)\propto\frac1{\sigma^2}$$|$$\color{red}\times$$|$$\displaystyle\lim_{\alpha,\beta\to0}\text{InvGamma}\left(\alpha,\beta\right)$$|

For the the Categorical distribution, recall that according to an [earlier](/2022/04/26/methods-of-estimation.html#mle_categorical) derivation $$I(\mathbf p)=\text{diag}^{-1}(\mathbf p)$$. Therefore, $$\pi(\mathbf p)\propto\sqrt{\det(I(\mathbf p))}=\prod_{j=1}^d\frac1{\sqrt{p_j}}$$. Since Multinomial r.v. is a sum of $$k$$ i.i.d. Categorical r.v., the associated Jeffreys prior is exactly the same, up to a proportional constant.

Note that $$\pi(\sigma^2)\propto\frac1{\sigma^2}$$ is equivalent to $$\pi(\sigma)\propto\frac1\sigma$$, which can also be obtained through the invariance described earlier. In addition, in accordance with the standard approach, the Jeffreys prior for the two-parameter $$\mathcal N(\mu,\sigma^2)$$, will result in $$\pi(\mu,\sigma^2)\propto\sqrt{\det(I(\mu,\sigma^2))}=\sqrt{\frac1{2\sigma^6}}\propto\frac1{\sigma^3}$$, which however has poor convergence properties. Jeffreys himself proposed that $$\pi(\mu,\sigma^2)=\pi(\mu)\pi(\sigma^2)\propto\frac1{\sigma^2}$$ arguing that ignorance about $$\mu$$ and $$\sigma^2$$ implies independence between their prior belief. However, rather than providing a solution, this argument highlighted **one of the limits** of the Jeffreys priors; that in the multivariate case, one may again introduce some discretion in assuming independence between parameters.

## Bayesian confidence region

According to the classical statistics, $$\mathcal I$$ is a [CI](/2022/03/24/foundation-of-inference.html#ci) of level $$\alpha$$ if $$\mathbb P(\theta\in\mathcal I)\ge1-\alpha$$. The frequentist nature of this definion implies that $$\mathcal I$$ either contains or not $$\theta$$, and the probability is given by the frequency of this event, that is $$\frac1n\sum_{i=1}^n\mathbb 1(\theta\in\mathcal I_i)\xrightarrow{\mathbb P}\mathbb E[\mathbb 1(\theta\in\mathcal I)]=\mathbb P(\theta\in\mathcal I)$$.

On the other hand, Bayesian confidence region of level $$\alpha\in(0,1)$$ is as a random subset $$\mathcal R$$ of the parameter space $$\Theta$$, s.t. $$\mathbb P(\theta\in\mathcal R\lvert X_1,\dots,X_n)\ge1-\alpha$$. Although the definitions of the CI and the Bayesian confidence region are very similar, the two notions are distinct---with the main difference being that $$\Theta$$ is a r.v. with its own conditional distribution $$\pi(\theta\lvert X_1,\dots,X_n)$$, which in turn will depend on the prior $$\pi(\theta)$$ which was not part of the classical statistics framework.

Analogously to the CI, the Bayesian confidence region of level $$\alpha_1\le\alpha_2$$ is also a Bayesian confidence region of level $$\alpha_2$${% if jekyll.environment == "development" %} (see [Stats L18 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u5s2_Bayes2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u5s2_Bayes2-tab9)){% endif %}, due to the inequality sign in its definition.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

### Beta distribution and beta function {#beta}

A continuous r.v. $$X$$ is distributed according to $$\text{Beta}(\alpha,\beta)$$ if $$f_X(x)=\frac1{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1}$$ for $$x\in[0,1]$$, and $$B(\alpha,\beta)$$ is the normalizing constant known as the **Beta function**. Assuming $$\alpha$$ and $$\beta$$ are positive integers, one can prove that $$B(\alpha,\beta)=\frac{(\alpha-1)!(\beta-1)!}{(\alpha+\beta-1)!}$$. Considering that Beta distribution is defined for $$x\in[0,1]$$ it is particularly suitable to describe the distribution of a probability parameter $$p$$.

Bearing in mind that $$\mathbb E[X^k]=\int_0^1f_X(x)dx$$, the first two moments of $$X\sim\text{Beta}(\alpha,\beta)$$ result in ratios between Beta functions, $$\mathbb E[X]=\frac{B(\alpha+1,\beta)}{B(\alpha,\beta)}=\frac\alpha{\alpha+\beta}$$ and $$\mathbb E[X^2]=\frac{B(\alpha+2,\beta)}{B(\alpha,\beta)}=\frac\alpha{\alpha+\beta}\frac{\alpha+1}{\alpha+\beta+1}$$. Hence, $$\text{var}(X)=\frac{\alpha\beta}{(\alpha+\beta+1)(\alpha+\beta)^2}$$.

The modes of Beta distribution can be determined as follows:

|$$\alpha$$|$$\beta$$|**mode(s)**|
|:-:|:-:|:-:|
|$$\alpha\lt1$$|$$\beta\lt1$$|$$x\in\{0,1\}$$|
|$$\alpha=1$$|$$\beta=1$$|$$x\in[0,1]$$|
|$$\alpha\le1$$|$$\beta\ge1$$|$$x=0$$|
|$$\alpha\ge1$$|$$\beta\le1$$|$$x=1$$|
|$$\alpha\gt1$$|$$\beta\gt1$$|$$x=\frac{\alpha-1}{(\alpha-1)+(\beta-1)}$$|

Assuming $$\alpha,\beta\gt0$$ are integers, Beta function can be derived by applying calculus, while bearing in mind that $$B(\alpha,1)=\int_0^1x^{\alpha-1}dx=\frac1\alpha$$.

$$\begin{align}
B(\alpha,\beta)&=\int_0^1x^{\alpha-1}(1-x)^{\beta-1}dx\\
&=\cancelto{=0}{\left[\frac1\alpha x^\alpha(1-x)^{\beta-1}\right]_0^1}+\frac{\beta-1}\alpha\int_0^1x^\alpha(1-x)^{\beta-2}dx\\
&=\frac{\beta-1}\alpha B(\alpha+1,\beta-1)=\\
&=\frac{(\beta-1)!}{\alpha(\alpha+1)\dots(\alpha+\beta-2)}{\color{red}B(\alpha+\beta-1,1)}\\
&={\color{blue}\frac{(\alpha-1)!}{(\alpha-1)!}}\frac{(\beta-1)!}{\alpha(\alpha+1)\dots(\alpha+\beta-2)}{\color{red}\frac1{(\alpha+\beta-1)}}\\
&=\frac{(\alpha-1)!(\beta-1)!}{(\alpha+\beta-1)!}
\end{align}$$

One can also use a probabilistic argument to reach the same conclusion. Assume a sequence of r.v. $$X_1,\dots,X_{\alpha+\beta-1}\overset{\text{i.i.d.}}{\sim}\text{Unif}(0,1)$$ and observe that the event $$E$$ of arranging them in the following order $$\underbrace{X_1\lt\dots\lt X_{\alpha-1}}_{\text{$\alpha-1$ terms}}\lt X_{\alpha}\lt\underbrace{X_{\alpha+1}\lt\dots\lt X_{\alpha+\beta-1}}_{\text{$\beta-1$ terms}}$$ is $$\mathbb P(E)=\frac1{(\alpha+\beta-1)!}$$.

Nevertheless, $$\mathbb P(E)$$ can also be written as $$\int_0^1\mathbb P(E\lvert X_\alpha=x)f_X(x)dx$$, where $$\mathbb P(E\lvert X_\alpha=x)$$ is the probability of observing $$\{X_1\lt\dots X_{\alpha-1}\lt x\}$$ and $$\{x\lt X_{\alpha+1}\lt\dots\lt X_{\alpha+\beta-1}\}$$, for any given $$X_\alpha=x\in(0,1)$$ and is equal to the following.

$$\begin{align}
\mathbb P(E\lvert X_\alpha=x)
&={\color{red}\mathbb P(\max\{X_1,\dots,X_{\alpha-1}\}\lt x)\mathbb P(X_1\lt\dots\lt X_{\alpha-1})}\\
&\times{\color{blue}\mathbb P(\min\{X_{\alpha+1},\dots,X_{\alpha+\beta-1}\}\gt x)\mathbb P(X_{\alpha+1}\lt\dots\lt X_{\alpha+\beta-1})}\\
&={\color{red}x^{\alpha-1}\frac1{(\alpha-1)!}}{\color{blue}(1-x)^{\beta-1}\frac1{(\beta-1)!}}\\
\frac1{(\alpha+\beta-1)!}
&=\int_0^1\mathbb P(E\lvert X_\alpha=x)f_X(x)dx=\frac1{(\alpha-1)!(\beta-1)!}\int_0^1x^{\alpha-1}(1-x)^{\beta-1}dx\\
\frac{(\alpha-1)!(\beta-1)!}{(\alpha+\beta-1)!}&=\int_0^1x^{\alpha-1}(1-x)^{\beta-1}dx=B(\alpha,\beta)
\end{align}$$

Even though above derivations assume $$\alpha$$ and $$\beta$$ integer, the normalizing factor $$B(\alpha,\beta)$$ can be generalized for any continuous $$\alpha,\beta\gt0$$ by replacing factorials with [Gamma](/2022/01/13/continuous-random-variables.html#gamma) functions, such that $$B(\alpha,\beta)=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$$. Properties of the Beta function include:

- $$B(1,1)=\frac{\Gamma(1)\Gamma(1)}{\Gamma(2)}=1$$;
- $$B(1,\alpha)=B(\alpha,1)=\frac{\Gamma(\alpha)\Gamma(1)}{\Gamma(\alpha+1)}=\frac{\Gamma(\alpha)}{\alpha\Gamma(\alpha)}=\frac1\alpha$$;
- $$B(\alpha+1,\beta)=\frac{\alpha\Gamma(\alpha)\Gamma(\beta)}{(\alpha+\beta)\Gamma(\alpha+\beta)}=\frac\alpha{\alpha+\beta}B(\alpha,\beta)$$; and
- $$B\left(\frac12,\frac12\right)=\pi$$.

Finally, if $$\boldsymbol{\alpha}\in\mathbb R^d$$, a more generic form of Beta function is $$B(\boldsymbol{\alpha})=B(\alpha_1,\dots,\alpha_d)=\frac{\prod_{j=1}^d\Gamma(\alpha_j)}{\Gamma(\sum_{j=1}^d\alpha_j)}$$.

- $$\frac{B(\beta,\gamma)}{B(\alpha,\beta,\gamma)}=\frac{\Gamma(\alpha+\beta+\gamma)}{\Gamma(\alpha)\Gamma(\beta)\Gamma(\gamma)}\frac{\Gamma(\beta)\Gamma(\gamma)}{\Gamma(\beta+\gamma)}=\frac{\Gamma(\alpha+\beta+\gamma)}{\Gamma(\alpha)\Gamma(\beta+\gamma)}=\frac1{B(\alpha,\beta+\gamma)}$$.

### Dirichlet distribution {#dirichlet}

As [Beta](/2023/03/13/bayesian-statistics.html#beta) is conjugate to the Binomial distribution, Dirichlet is conjugate to the [Multinomial distribution](/2022/01/24/further-topics-on-RV.html#categorical). Considering below relationship table, alternative view is that Dirichlet is also a multivariate extension of the Beta distribution.

|Parameter dimensions|single copy|$$k$$ i.i.d. copies|conjugate|
|:-:|:-:|:-:|:-:|
|$$p\in[0,1]\subset\mathbb R$$|$$X\lvert P\sim\text{Ber}(P)$$|$$\displaystyle\sum_{i=1}^k X_i\lvert P\sim\text{Bin}(k,P)$$|$$P\sim\text{Beta}(\alpha,\beta)$$|
|$$\mathbf p\in\Delta_p\subset\mathbb R^d$$|$$\mathbf X\lvert\mathbf P\sim\text{Cat}(\mathbf P)$$|$$\displaystyle\sum_{i=1}^k\mathbf X_i\lvert\mathbf P\sim\text{Mult}(k,\mathbf P)$$|$$\mathbf P\sim\text{Dir}(\boldsymbol{\alpha})$$|

Bearing in mind the following forms of [Binomial PMF](/2022/01/08/discrete-random-variables.html#basic) and [Beta PDF](/2022/01/13/continuous-random-variables.html#basic):

$$\begin{align}
p_{X\lvert P}(x\lvert p)={k\choose x}p^x(1-p)^{k-x}&&\pi(p)=\frac1{B(\alpha,\beta)}p^{\alpha-1}(1-p)^{\beta-1}
\end{align}$$

By pure analogy and inspection, one may conclude without rigorous proof that starting from [Multinomial PMF](/2022/01/24/further-topics-on-RV.html#categorical), one can obtain a conjugate $$\pi(\mathbf p)$$ of the following form.

$$\begin{align}
p_{\mathbf X\lvert\mathbf P}(\mathbf x\lvert\mathbf p)={k\choose\mathbf x}\prod_{j=1}^d p_j^{x_j}&&\pi(\mathbf p)=\frac1{B(\boldsymbol{\alpha})}\prod_{j=1}^d p_j^{\alpha_j-1}
\end{align}$$

Bearing in mind that $$\mathbf1_d^T\mathbf p=1$$ and $$\mathbf1_d^T\boldsymbol{\alpha}=\alpha_0$$, one realizes that $$\text{Beta}(\alpha,\beta)$$ is a special case of the Dirichlet distribution with $$d=2$$ and $$\boldsymbol{\alpha}=\begin{bmatrix}\alpha&\alpha_0-\alpha\end{bmatrix}^T$$. Furthermore, one legitimate question may be if $$P_i\sim\text{Beta}(\alpha_i,\alpha_0-\alpha_i)$$ for any $$1\le i\le d$$. It turns out this is true and can be observed by deriving the marginal distribution.

First, recall that for $$\mathbf p\in\Delta_d$$, one of the dimensions depends on the others (e.g. $$p_d=1-\sum_{j=1}^{d-1}p_j$$). Therefore, analogously to what we did [earlier](/2022/07/15/hypothesis-testing.html#pearson_wald), Dirichlet can be expressed in terms of $$d-1$$ variables.

$$\pi(p_1,\dots,p_{d-1})=\frac1{B(\boldsymbol{\alpha})}\prod_{j=1}^{d-1}p_j^{\alpha_j-1}{\underbrace{\left(1-\sum_{j=1}^{d-1}p_j\right)}_{=p_d}}^{\alpha_d-1}$$

Second, observe that if we want to compute the distribution of the first $$d-2$$ terms only, by marginalizing out $$p_{d-1}$$, this can be achieved as follows (where $$1-\xi=1-\sum_{j=1}^{d-2}p_j$$).

$$\begin{align}
\pi(p_1,\dots,p_{d-2})
&=\int_0^{1-\xi}\pi(p_1,\dots,p_{d-1})dp_{d-1}\\
\end{align}$$

Finally, take note of the following integral, which may be useful on various occasions.

$$\begin{align}
\int_0^{1-\xi}p^{\alpha-1}(1-\xi-p)^{\beta-1}dp
&=\int_0^{1-\xi}p^{\alpha-1}\left(1-\frac p{1-\xi}\right)^{\beta-1}(1-\xi)^{\beta-1}dp&\left(t=\frac p{1-\xi}\right)\\
&=(1-\xi)^{\alpha+\beta-1}\int_0^1 t^{\alpha-1}(1-t)^{\beta-1}dt\\
&=(1-\xi)^{\alpha+\beta-1}B(\alpha,\beta)
\end{align}$$

Now, if we plug in the above result in the marginal distribution we saw earlier.

$$\begin{align}
\pi(p_1,\dots,p_{d-2})
&=\int_0^{1-\xi}\pi(p_1,\dots,p_{d-1})dp_{d-1}\\
&=\int_0^{1-\xi}\frac1{B(\boldsymbol{\alpha})}\prod_{j=1}^{d-1}p_j^{\alpha_j-1}\left(1-\sum_{j=1}^{d-1}p_j\right)^{\alpha_d-1}dp_{d-1}\\
&=\frac1{B(\boldsymbol{\alpha})}\prod_{j=1}^{d-2}p_j^{\alpha_j-1}{\int_0^{1-\xi}p_{d-1}^{\alpha_{d-1}-1}(1-\xi-p_{d-1})^{\alpha_d-1}dp_{d-1}}\\
&=\frac1{B(\boldsymbol{\alpha})}\prod_{j=1}^{d-2}p_j^{\alpha_j-1}(1-\xi)^{\alpha_{d-1}+\alpha_d-1}B(\alpha_{d-1},\alpha_d)\\
&=\frac{B(\alpha_{d-1},\alpha_d)}{B(\alpha_1,\dots,\alpha_{d-1},\alpha_d)}\prod_{j=1}^{d-2}p_j^{\alpha_j-1}(1-\xi)^{\alpha_{d-1}+\alpha_d-1}\\
&=\frac1{B(\alpha_1,\dots,\alpha_{d-2},\alpha_{d-1}+\alpha_d)}p_1^{\alpha_1-1}\dots p_{d-2}^{\alpha_{d-2}-1}{\underbrace{(1-\xi)}_{=p'_{d-1}}}^{\overbrace{\alpha_{d-1}+\alpha_d}^{=\alpha'_{d-1}}-1}
\end{align}$$

That is basically a $$\text{Dir}(\alpha_1,\dots,\alpha_{d-2},\alpha'_{d-1})$$, with the last hyper-parameter $$\alpha'_{d-1}=\alpha_{d-1}+\alpha_d$$ (or $$\alpha'_{d-1}=\alpha_0-\sum_{j=1}^{d-2}\alpha_j$$) associated with the *aggregated* parameter $$p'_{d-1}=1-\xi=1-\sum_{j=1}^{d-2}p_j$$.

If applied recursively, one observes that $$i$$-th entry of $$\mathbf P$$ is distributed $$P_i\sim\text{Beta}(\alpha_i,\alpha_0-\alpha_i)$$, and that the marginal expectation and variance are $$\mathbb E[P_i]=\frac{\alpha_i}{\alpha_0}=\tilde\alpha_i$$ and $$\text{var}(P_i)=\frac{\tilde\alpha_i(1-\tilde\alpha_i)}{\alpha_0+1}$$. Using vector notation, the expectation and [covariance matrix](/2022/01/24/further-topics-on-RV.html#covariance_matrix) are as follows.

$$\begin{align}
\mathbb E[\mathbf P]=\frac1{\alpha_0}\begin{bmatrix}\alpha_1\\\vdots\\\alpha_d\end{bmatrix}=\begin{bmatrix}\tilde\alpha_1\\\vdots\\\tilde\alpha_d\end{bmatrix}&&\Sigma_\mathbf P=\text{cov}(\mathbf P)=\frac1{\alpha_0+1}\begin{bmatrix}\tilde\alpha_1(1-\tilde\alpha_1)&\dots&-\tilde\alpha_1\tilde\alpha_d\\\vdots&\ddots&\\-\tilde\alpha_d\tilde\alpha_1&&\tilde\alpha_d(1-\tilde\alpha_d)\end{bmatrix}
\end{align}$$

To derive covariance entries, observe that $$\text{cov}(P_i,P_j)=\mathbb E[P_iP_j]-\mathbb E[P_j]\mathbb E[P_j]$$. While $$\mathbb E[P_i]=\frac{\alpha_i}{\alpha_0}$$ and $$\mathbb E[P_j]=\frac{\alpha_j}{\alpha_0}$$, the term $$\mathbb E[P_iP_j]$$ relies on the fact that $$(P_i,P_j)\sim\text{Dir}(\alpha_i,\alpha_j,\alpha_0-\alpha_i-\alpha_j)$$.

$$\begin{align}
\mathbb E[P_iP_j]
&=\int_0^1\left(\int_0^{1-p_i}p_ip_j\pi(p_i,p_j)dp_j\right)dp_i\\
&=\int_0^1\left(\int_0^{1-p_i}\frac1{B(\alpha_i,\alpha_j,\alpha_0-\alpha_i-\alpha_j)}p_i^{\alpha_i}p_j^{\alpha_j}(1-p_i-p_j)^{\alpha_0-\alpha_i-\alpha_j-1}dp_j\right)dp_i\\
&=\frac1{B(\alpha_i,\alpha_j,\alpha_0-\alpha_i-\alpha_j)}\int_0^1 p_i^{\alpha_i}\left(\int_0^{1-p_i}p_j^{\alpha_j}(1-p_i-p_j)^{\alpha_0-\alpha_i-\alpha_j-1}dp_j\right)dp_i\\
&=\frac1{B(\alpha_i,\alpha_j,\alpha_0-\alpha_i-\alpha_j)}\int_0^1 p_i^{\alpha_i}(1-p_i)^{\alpha_0-\alpha_i}B(\alpha_j+1,\alpha_0-\alpha_i-\alpha_j)dp_i\\
&=\frac{\alpha_j}{(\alpha_0-\alpha_i+1)}\frac{B(\alpha_j,\alpha_0-\alpha_i-\alpha_j)}{B(\alpha_i,\alpha_j,\alpha_0-\alpha_i-\alpha_j)}\int_0^1 p_i^{\alpha_i}(1-p_i)^{\alpha_0-\alpha_i}dp_i\\
&=\frac{\alpha_j}{(\alpha_0-\alpha_i+1)}\frac1{B(\alpha_i,\alpha_0-\alpha_i)}B(\alpha_i+1,\alpha_0-\alpha_i+1)\\
&=\frac1{B(\alpha_i,\alpha_0-\alpha_i)}\frac{\alpha_j}{(\alpha_0-\alpha_i+1)}\frac{\alpha_i}{(\alpha_0+1)}\frac{(\alpha_0-\alpha_i+1)}{\alpha_0}B(\alpha_i,\alpha_0-\alpha_i)\\
&=\frac{\alpha_i\alpha_j}{\alpha_0(\alpha_0+1)}
\end{align}$$

In the above passages, we used the integral described earlier, together with Beta function [properties](/2023/03/13/bayesian-statistics.html#beta).

$$\begin{align}
\text{cov}(P_i,P_j)
&=\frac{\alpha_i\alpha_j}{\alpha_0(\alpha_0+1)}-\frac{\alpha_i\alpha_j}{\alpha_0^2}\\
&=-\frac{\alpha_i\alpha_j}{\alpha_0^2(\alpha_0+1)}=-\frac{\tilde\alpha_i\tilde\alpha_j}{\alpha_0+1}
\end{align}$$

To find the mode, analogously to what we did forthe [MLE](/2022/04/26/methods-of-estimation.html#mle_categorical) we can exploit the [Lagrange multiplier](/2022/04/26/methods-of-estimation.html#lagrange_multiplier). Considering that $$\arg\max_{\mathbf p}\pi(\mathbf p)=\arg\max_{\mathbf p}\ln\pi(\mathbf p)$$ is subject to $$g(\mathbf p)=\mathbf 1_d^T\mathbf p-1=0$$, vector $$\mathbf p$$ that maximizes the PDF is the solution of the following equation.

$$\begin{align}
\nabla_p\ln\pi(\hat{\mathbf p})&=\nabla_p\lambda g(\hat{\mathbf p})\\
\text{diag}^{-1}(\hat{\mathbf p})(\boldsymbol{\alpha}-1)&=\lambda\mathbf 1_d\\
(\boldsymbol{\alpha}-1)&=\lambda\text{diag}(\hat{\mathbf p})\mathbf 1_d\\
(\boldsymbol{\alpha}-1)&=\lambda\hat{\mathbf p}\\
\end{align}$$

By observing that $$\mathbf 1_d^T(\boldsymbol{\alpha}-1)=\alpha_0-d=\mathbf 1_d^T\hat{\mathbf p}=1$$ it follows that $$\lambda=(\alpha_0-d)$$. Accordingly, the solution to the above maximization is $$\hat{\mathbf p}=\frac{\boldsymbol{\alpha}-1}{\alpha_0-1}$$

### Inverse Gamma distribution {#invgamma}

Assuming $$Y\sim\text{Gamma}(\alpha,\beta)$$, the distribution of $$X=Y^{-1}$$ is known as the **Inverse Gamma**, PDF can be [derived](/2022/01/24/further-topics-on-RV.html#derived_distributions) as $$f_X(x)=f_Y\left(\frac1x\right)\frac1{x^2}=\frac{\beta^\alpha}{\Gamma(\alpha)}x^{-(\alpha+1)}e^{-\frac\beta x}$$. The moments of $$\text{InvGamma}(\alpha,\beta)$$ are in accordance with the following formula.

$$\begin{align}
\mathbb E[X^n]&=\int_0^\infty x^n\frac{\beta^\alpha}{\Gamma(\alpha)}x^{-(\alpha+1)}e^{-\frac\beta x}dx=\frac{\beta^\alpha}{\Gamma(\alpha)}\int_0^\infty x^{-(\alpha-n+1)}e^{-\frac\beta x}dx\\
&=\frac{\beta^\alpha}{\Gamma(\alpha)}\int_\infty^0 z^{\alpha-n+1}e^{-\beta z}(-z^{-2})dz=\frac{\beta^\alpha}{\Gamma(\alpha)}\int_0^\infty z^{(\alpha-n)-1}e^{-\beta z}dz\\
&=\frac{\beta^\alpha}{\Gamma(\alpha)}\frac{\Gamma(\alpha-n)}{\beta^{\alpha-n}}=\frac{\beta^n}{(\alpha-1)(\alpha-2)\dots(\alpha-n)}
\end{align}$$

Thus for $$\alpha\gt1$$, $$\mathbb E[X]=\frac\beta{(\alpha-1)}$$, while for $$\alpha\gt2$$, $$\mathbb E[X^2]=\frac{\beta^2}{(\alpha-1)(\alpha-2)}$$, and $$\text{var}(X)=\frac{\beta^2}{(\alpha-1)^2(\alpha-2)}$$.

Considering that $$\chi_k^2$$ distribution is equivalent to $$\text{Gamma}(\frac k2,\frac12)$$, it follows that if $$Z\sim\text{Inv}\chi_k^2$$ then $$Z\sim\text{InvGamma}(\frac k2,\frac12)$$. Therefore, for $$k\gt2$$, $$\mathbb E[Z]=\frac1{k-2}$$, and for $$k\gt4$$, $$\text{var}(Z)=\frac2{(k-2)^2(k-4)}$$.

As for the mode of the Inverse Gamma, analogously to what we did for [Gamma](/2022/01/13/continuous-random-variables.html#gamma) distribution, observe that the derivative of PDF is equal to zero when $$x=\frac\beta{\alpha+1}$$.

$$\frac\partial{\partial x}f_X(x)\propto x^{-\alpha-2}e^{-\frac\beta x}\left(-(\alpha+1)+\frac\beta x\right)$$
