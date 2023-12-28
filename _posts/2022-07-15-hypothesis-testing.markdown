---
layout: post
title: "Hypothesis Testing"
---

$$\newcommand{\ind}{\perp\kern-5pt\perp}$$

## Parameter Hypothesis Testing {#parameter_testing}

Having seen the main ideas behind [parameters estimation](/2022/04/26/methods-of-estimation.html#intro), it is time to test if evidence obtained from actual observations can match a given hypothesis. Common questions are---Is the unknown parameter $$\theta=\theta_0$$? Based on what criteria, can the hypothesis $$\theta=\theta_0$$ be rejected? What are the chances of false positives based on that criteria?

To answer those questions, one can define an estimator (e.g. (G)MM, MLE or ME), determine the corresponding probability distribution, plug it into the framework of the [Hypothesis Testing](/2022/03/24/foundation-of-inference.html#testing), while setting the desired parameters such as the rejection region associated with the desired level $$\alpha$$.

In this segment, we will see non asymptotic and asymptotic tests. Where the former methods are applicable only when the underlying distribution is Normal, the latter either relies on the properties of CLT or explores the properties of an MLE.

## Non asymptotic tests

### Relationship between sample mean and variance

Distribution of $$\sum_{i=1}^k Z_i^2$$, where $$Z_i\overset{\text{i.i.d.}}{\sim}\mathcal N(0,1)$$, is defined as $$\chi^2$$ distribution with $$k$$ degrees of freedom and is indicated as $$\sum_{i=1}^k Z_i^2\sim\chi^2_k$$. If $$k=1$$, we have $$Z^2\sim\chi^2_1$$ and $$F_{Z^2}(t)=2\Phi(\sqrt t)-1$$, with the quantile of order $$1-\alpha$$ that can be computed from a quantile of a Normal distribution as $$q_\alpha(\chi_1^2)=q_{\frac\alpha2}^2(\mathcal N(0,1))$${% if jekyll.environment == "development" %} (see [Stats L14 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab7)){% endif %}.

Any collection of $$X_i\overset{\text{i.i.d.}}{\sim}\mathcal N(\mu,\sigma^2)$$ can match $$\chi^2$$ distribution, if properly [standardized](/2022/01/13/continuous-random-variables.html#normal){% if jekyll.environment == "development" %} (see [Stats L13 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab7)){% endif %}. For this reason, $$\chi_n^2$$ is also referred to as a [pivotal quantity](https://en.wikipedia.org/wiki/Pivotal_quantity), because its distribution does not depend on unknown parameters.

$$\sum_{i=1}^n\left(\frac{X_i-\mu}{\sigma^2}\right)^2\sim\chi_n^2$$

Note that $$\sum_{i=1}^n(X_i-\mu)^2$$ can be rewritten as $$\sum_{i=1}^n((X_i-\bar X_n)+(\bar X_n-\mu))^2$$, which allows rearranging the above as follows{% if jekyll.environment == "development" %} (see [Stats L13 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab8)){% endif %}.

$$\sum_{i=1}^n\left(\frac{X_i-\mu}{\sigma}\right)^2=\underbrace{\sum_{i=1}^n\left(\frac{X_i-\bar X_n}{\sigma}\right)^2}_{\sim\chi_{n-1}^2}+\underbrace{\left(\sqrt n\frac{\bar X_n-\mu}{\sigma}\right)^2}_{\sim\chi_1^2}\sim\chi_n^2$$

In accordance with [Cochran's theorem](/2022/07/15/hypothesis-testing.html#cochran), the above relation contains two important considerations. First, that the term distributed as $$\chi_{n-1}^2$$ is independent from the one distributed as $$\chi_1^2$$. Second, the term distributed as $$\chi_{n-1}^2$$ is strictly associated with the [MLE of variance](/2022/04/26/methods-of-estimation.html#mle). Bearing in mind that $$\hat{\sigma}^2=\frac 1 n\sum_{i=1}^n(X_i-\bar X_n)^2$$, it follows that:

- MLE of variance is distributed according to $$\frac n{\sigma^2}\hat{\sigma}^2\sim\chi_{n-1}^2$$; and that
- MLE of variance and MLE of mean are **independent for any** $$n$$, that is $$\hat{\sigma}^2\ind\bar X_n$$.

Occasionally, the unbiased sample variance $$s^2=\frac{1}{n-1}\sum_{i=1}^n(X_i-\bar X_n)^2=\frac n{n-1}\hat{\sigma}^2$$ is used instead; despite this change, the above considerations remain unchaged, except that $$\frac{(n-1)}{\sigma^2}s^2\sim\chi^2_{n-1}$$.

### One-sample Student's $$t$$ test {#ttest}

Recall that when we built MLE to estimate parameters of $$X\sim\mathcal N(\mu,\sigma^2)$$, we relied on [Slutsky's theorem](/2022/02/21/introduction-to-statistics.html#properties) to assume $$\sqrt n\frac{\bar X_n-\mu}{\sqrt{\hat{\sigma}^2}}\xrightarrow{(d)}\mathcal N(0,1)$$, by exploiting the fact that $$\hat{\sigma}^2\xrightarrow{\mathbb P}\sigma^2$$.

But what if $$n\lt\infty$$ and Slutsky's theorem cannot be applied? Gosset studied the problems of small samples and noticed that even though the distribution of $$\bar X_n$$ cannot be approximated with Normal distribution for small $$n$$, it could still be approximated with another pivotal quantity.

Having observed that the ratio between $$Z$$ and $$\sqrt{V_d/d}$$, where $$Z\sim\mathcal N(0,1)$$ and $$V_d\sim\chi^2_d$$, has a probability law that depends exclusively on $$n$$ if $$Z\ind V_d$$, Gosset defined the following test statistic and [derived its PDF](/2022/07/15/hypothesis-testing.html#tdist), which depends exclusively on its $$d$$ degrees of freedom.

$$T_n=\frac Z{\sqrt{\frac{V_d}{d}}}\sim t_d$$

$$V_d\sim\chi_d^2$$ can be assimilated with $$\sum_{i=1}^d Z^2$$, therefore $$\frac{V_d}d=\frac1d\sum_{i=1}^d Z_i^2\xrightarrow{\mathbb P}\mathbb E[Z^2]=1$$, which in turn means that $$T_n=\frac Z{\sqrt{\frac{V_d}d}}\xrightarrow{(d)}\frac Z{\sqrt{1}}\sim\mathcal N(0,1)$$, thanks to [Slutsky's theorem](/2022/02/21/introduction-to-statistics.html#properties){% if jekyll.environment == "development" %} (see [Stats L13 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab9)){% endif %}.

At this point, one can observe that the non asymptotic distribution of $$\bar X_n$$, in which we use the unbiased sample variance $$s^2$$ can be arranged in a way to resemble the above ratio, where the presence (or the absence) of the *true* variance becomes irrelevant, as it will disappear due to division.

$$T_n=\frac{\bar X_n-\mu}{\sqrt{\frac{s^2}n}}=\frac{\sqrt n\frac{\bar X_n-\mu}{\sigma}}{\sqrt{\frac{s^2}{\sigma^2}}}\sim\frac Z{\sqrt{\frac{V_{n-1}}{n-1}}}\sim t_{n-1}$$

This means that if we want to test $$H_0:\mu_X=\mu^\star$$ our **non asymptotic** test statistic can be either of the following forms, keeping in mind that $$(n-1)s_X^2=n\sigma_X^2$${% if jekyll.environment == "development" %} (see [Stats L13 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab10)){% endif %}.

$$T_n=\sqrt n\frac{\bar X_n-\mu^\star}{\sqrt{s_X^2}}=\sqrt{n-1}\frac{\bar X_n-\mu^\star}{\sqrt{\sigma_X^2}}\sim t_{n-1}$$

Analogously to the [previous case](/2022/07/15/hypothesis-testing.html#two_proportions), a test of level $$\alpha$$ is $$\psi_\alpha=\mathbb 1(\lvert T_n\rvert\gt q_{\frac\alpha2})$$, with the only difference that $$q_{\frac\alpha2}$$ indicates here the $$1-\frac\alpha2$$ quantile of $$t$$ distribution with $$n-1$$ degrees of freedom.

The $$t$$ test makes the strong assumption that the sample is Normally distributed, because in order to be distributed according to $$t_{n-1}$$, we need to have $$\bar X_n\ind\hat\sigma^2$$, which the [Cochran's](/2022/07/15/hypothesis-testing.html#cochran) theorem guarantees only if $$X_i\overset{\text{i.i.d.}}{\sim}\mathcal N(\mu,\sigma^2)$${% if jekyll.environment == "development" %} (see [Stats MT2 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm2-tab2)){% endif %}. For this, [KL test](/2022/07/15/hypothesis-testing.html#kl) (or other normality tests) are performed first, to ensure that normality is not rejected.

### Welch–Satterthwaite approximation {#ws}

Assume observing two sample variables $$s_X^2\sim\frac{\sigma_X^2}{(n-1)}\chi_{n-1}^2$$ and $$s_Y^2\sim\frac{\sigma_Y^2}{(m-1)}\chi_{m-1}^2$$, with $$s_X^2\ind s_Y^2$$. In general, the distribution of $$s_Z^2=s_X^2+s_Y^2$$ cannot be expressed analytically. However, it may be reasonable approximating it with another $$\chi^2$$ distribution, such as $$s_Z^2\sim\frac{\sigma_Z^2}d\chi_d^2$$, where $$\sigma_Z^2=\mathbb E[s_Z^2]$$ and therefore $$\sigma_Z^2=\sigma_X^2+\sigma_Y^2$$. As for the effective degrees of freedom $$d$$ of $$s_Z^2$$, its determination can be obtained by equating the relations (1) and (2) below.

$$\begin{align}
\text{var}(s_Z^2)&\approx\text{var}\left(\frac{\sigma_Z^2}d\chi^2_d\right)=2\frac{(\sigma_X^2+\sigma_Y^2)^2}d&(1)\\
\text{var}(s_Z^2)&=\text{var}(s_X^2)+\text{var}(s_Y^2)=2\frac{\sigma_X^4}{(n-1)}+2\frac{\sigma_Y^4}{(m-1)}&(2)\\
2\frac{(\sigma_X^2+\sigma_Y^2)^2}d&\approx2\frac{\sigma_X^4}{(n-1)}+2\frac{\sigma_Y^4}{(m-1)}\\
\implies d&\approx\frac{(\sigma_X^2+\sigma_Y^2)^2}{\frac{\sigma_X^4}{(n-1)}+\frac{\sigma_Y^4}{(m-1)}}
\end{align}$$

Since we do not know true variances, effective degrees of freedom $$d$$ are estimated by replacing true variances with observed sample variances.

$$\hat d\approx\frac{(s_X^2+s_Y^2)^2}{\frac{s_X^4}{(n-1)}+\frac{s_Y^4}{(m-1)}}$$

The above approach can be generalized to any linear combination $$\sum_{i=1}^k a_i s_i^2$$, where $$a_i\gt0$$. In such case, the degrees of freedom of the pooled sample variances are estimated via **Welch-Satterthwaite** (WS) equation below, where $$d_i$$ are the degrees of freedom associated with sample variance $$s_i^2$$.

$$\hat d\approx\frac{\left(\sum_{i=1}^k a_i s_i^2\right)^2}{\sum_{i=1}^k \frac{(a_i s_i^2)^2}{d_i}}$$

### Two-sample Welch's $$t$$ test

Consider $$X\sim\mathcal N(\mu_X,\sigma_X^2)$$ and $$Y\sim\mathcal N(\mu_Y,\sigma_Y^2)$$ and assume a test on $$\mu_X-\mu_Y$$, where a number of i.i.d. observations $$X_i$$ and $$Y_j$$ are available. Also, assume that $$X_i\ind Y_j$$ for any $$i\in\{1,\dots,n\}$$ and $$j\in\{1,\dots,m\}$$. For example a test $$H_0:\mu_X=\mu_Y$$ would be a two-sided two-sample test{% if jekyll.environment == "development" %} (see [Stats L13 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab3)){% endif %}.

If true variances are known, then $$\bar X_n-\bar Y_m\sim\mathcal N(\mu_X-\mu_Y, \frac{\sigma_X^2}n+\frac{\sigma_Y^2}m)$${% if jekyll.environment == "development" %} (see [Stats L13 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab4)){% endif %}. If not, but $$n$$ and $$m$$ are sufficiently large, we can still use [Slutsky's theorem](/2022/02/21/introduction-to-statistics.html#properties) and CMT to replace true variances with sample variances and obtain the following approximation{% if jekyll.environment == "development" %} (see [Stats L13 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab5)){% endif %}.

$$\frac{(\bar X_n-\bar Y_m)-(\mu_X-\mu_Y)}{\sqrt{\frac{s_X^2}n+\frac{s_Y^2}m}}\xrightarrow{(d)}\mathcal N(0,1)$$

If $$n,m\lt\infty$$, Slutsky's theorem does not apply{% if jekyll.environment == "development" %} (see [Stats L13 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s03_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s03_hypotesting-tab6)){% endif %}. However, it turns out that the above ratio has an approximately $$t$$ distribution with $$d$$ degrees of freedom.

$$T_n=\frac{(\bar X_n-\bar Y_n)-(\mu_X-\mu_Y)}{\sqrt{\frac{s_X^2}n+\frac{s_Y^2}m}}\sim t_d$$

Computation of $$d$$ relies on the [WS](/2022/07/15/hypothesis-testing.html#ws) equation, where we consider $$s_Z^2=\frac{s_X^2}n+\frac{s_Y^2}m$$. Hence the degrees of freedom in this test is as follows.

$$d\approx\frac{\left(\frac{s_X^2}n+\frac{s_Y^2}m\right)^2}{\frac{s_X^4}{n^2(n-1)}+\frac{s_Y^4}{m^2(m-1)}}$$

Note that this makes relies on the fact that $$X_i$$ and $$Y_j$$ are drawn from Normal distributions. Therefore, Welch's $$t$$ cannot be universally applied.

## Introduction to likelihood ratio test (LRT) {#lrt}

Before we move to the next segment, there is an additional framework used for parameter Hypothesis Testing that is based on the intuition that the likelihood $$\mathcal L_n(X_1,\dots,X_n,\theta)$$ is [maximum](/2022/04/26/methods-of-estimation.html#kl) for $$\theta=\theta^\star$$, or the true, unknown parameter. In this case we expect that $$T_n=\frac{\mathcal L_n(\theta)}{\mathcal L_n(\theta^\star)}\le1$$ for any other $$\theta\in\Theta$$.

Put differently, one could test if under the null $$H_0:\theta=\theta_0$$, a test statistic $$T_n=\frac{\mathcal L_n(\hat{\Theta}_n)}{\mathcal L_n(\theta_0)}\gt c$$ in which case one could say that with probability of error $$\alpha$$ the sample has not been drawn from a distribution with parameter $$\theta_0$$. Hence the name of the LRT, which foresees the test of the form $$\mathbb 1(T_n\gt c_\alpha)$$,  where $$c_\alpha$$ is set in a way so that chances of false positive does not exceed level $$\alpha$${% if jekyll.environment == "development" %} (see [Stats L14 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab10)){% endif %}. If we deal with an asymptotically Normal MLE, and sufficiently large sample size, [Wilks' test](/2022/07/15/hypothesis-testing.html#wilks) may be more appropriate.

## Asymptotic tests

### Two-sample comparison of proportions {#two_proportions}

Assume collecting two sets of observations, $$X_i\overset{\text{i.i.d.}}{\sim}\text{Ber}(p_X)$$ and $$Y_i\overset{\text{i.i.d.}}{\sim}\text{Ber}(p_Y)$$, for $$i=1,\dots,n$$, with $$n\rightarrow\infty$$. A very common exercise is to test if there is significant difference between $$p_X$$ and $$p_Y$$.

According to [CLT](/2022/02/21/introduction-to-statistics.html#clt_mean), $$\bar X_n\xrightarrow{(d)}\mathcal N(p_X,\frac{p_X(1-p_X)}n)$$ and $$\bar Y_n\xrightarrow{(d)}\mathcal N(p_Y,\frac{p_Y(1-p_Y)}n)$$, which means that $$\bar X_n-\bar Y_n\xrightarrow{(d)}\mathcal N(p_X-p_Y,\frac{p_X(1-p_X)+p_Y(1-p_Y)}n)$$. To test $$H_0:p_X=p_Y$$, one can check $$\bar X_n-\bar Y_n$$ and see if it fits the null hypothesis, provided that the variance is based on $$\hat p=\bar X_n$$, $$\hat p=\bar Y_n$$, or better, the average of the two $$\hat p=\frac{\bar X_n+\bar Y_n}{2}$$.

$$T_n=\sqrt n\frac{\bar X_n-\bar Y_n}{\sqrt{2\hat p(1-\hat p)}}\xrightarrow{(d)}\mathcal N(0,1)$$

To test $$H_0:p_X=p_Y$$ we use $$\psi_\alpha=\mathbb 1(\lvert T_n\rvert\gt q_{\frac\alpha2})$$, where $$q_{\frac\alpha2}$$ is the quantile of order $$1-\frac\alpha2$$. Another way of looking at it is by observing the associated rejection region.

$$R_{\psi_\alpha}=\{(\bar X_n,\bar Y_n)\in\mathbb R^2:(\bar X_n\lt\bar Y_n-s)\cup(\bar X_n\gt\bar Y_n+s)\}$$

In the above $$s=\sqrt{\frac{2\hat p(1-\hat p)}n}\xrightarrow{\mathbb P}0$$, which means that $$R_{\psi_\alpha}\xrightarrow{\mathbb P}\{(\bar X_n,\bar Y_n)\in\mathbb R^2:\bar X_n\neq\bar Y_n\}$$. Hence, if we assume $$H_1:p_X\neq p_Y$$, the pair $$(\bar X_n,\bar Y_n)$$ will not lead to $$\lvert\bar X_n-\bar Y_n\rvert=0$$ and will be rejected. In other words, the probability of **false negative** is $$\beta_\psi(\theta)\xrightarrow{\mathbb P}0$$ that in turn means that the probability of detecting **true positive** is $$\pi=\inf_{\theta\in\Theta_1}(1-\beta_\psi(\theta))\xrightarrow{\mathbb P}1$$ (review [here](/2022/03/24/foundation-of-inference.html#testing) for definitions){% if jekyll.environment == "development" %} (see [Stats L14 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab8)){% endif %}.

### MLE-based tests

In light of various advantages of the MLE, it is natural building a test that exploits its properties. [Recall](/2022/04/26/methods-of-estimation.html#score) that in the univariate case, the MLE is distributed as follows (assuming [MLE technical conditions](/2022/04/26/methods-of-estimation.html#mle_properties) are satisfied, including the existence of [Fisher information](/2022/04/26/methods-of-estimation.html#score)).

$$\sqrt{nI(\theta)}(\hat\Theta_n-\theta)\xrightarrow{(d)}\mathcal N(0,1)$$

Intuitively, by squaring both LHS and RHS, we obtain the following basic relation.

$$nI(\theta)(\hat\Theta_n-\theta)^2\xrightarrow{(d)}\chi_1^2$$

In the multivariate case, the above is generalized as follows, where $$\boldsymbol\theta\in\mathbb R^d$$.

$$n(\hat{\boldsymbol\Theta}_n-\boldsymbol\theta)^TI(\boldsymbol\theta)(\hat{\boldsymbol\Theta}_n-\boldsymbol\theta)\xrightarrow{(d)}\chi_d^2$$

Based on the above, we have the following (asymptotically equivalent) tests: Rao's (score) test, Wald's test, and Wilks' (likelihood ratio) test; again, provided that in each case MLE technical conditions and Fisher information exist{% if jekyll.environment == "development" %} (see [Stats L15 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab2)){% endif %}.

The main difference between them is that Rao's test depends exclusively on some $$\boldsymbol{\theta}=\boldsymbol{\theta}_0$$, where Wald's test (in its form as implicit test) depends exclusively on $$\hat{\boldsymbol{\Theta}}_n$$. Finally, Rao's and Wald's tests are an approximation of Wilks' test, which considers both $$\boldsymbol{\theta}_0$$ and $$\hat{\boldsymbol{\Theta}}_n$$.

### Rao's (score) test

As the average score function of a univariate $$\theta$$ is asymptotically Normal, $$\sqrt n\bar s_n(\theta)\xrightarrow{(d)}\mathcal N(0,I(\theta))$$, we can test $$H_0:\theta=\theta_0$$, by defining a test statistic as its quadratic form and assuming $$\theta=\theta_0$$. In particular, replace $$\bar s_n(\theta_0)=\frac1n\ell_n'(\theta_0)$$ and $$\frac1n\left(-\ell_n''(\theta_0)\right)\xrightarrow{\mathbb P}I(\theta_0)$$, apply [Slutsky's theorem](/2022/02/21/introduction-to-statistics.html#properties) and and define the following test statistic, which *under the null* will converge to a $$\chi^2$$ distribution.

$$T_n=\frac{(\ell_n'(\theta_0))^2}{(-\ell_n''(\theta_0))}=n\frac{\bar s_n^2(\theta)}{I(\theta)}\xrightarrow{(d)}\chi_1^2$$

If $$\boldsymbol{\theta}\in\mathbb R^d$$ is multivariate, our test statistic will take the following form.

$$T_n=(\nabla_\theta\ell_n(\boldsymbol{\theta}_0))^T(-\nabla_\theta^2\ell(\boldsymbol{\theta}_0))^{-1}(\nabla_\theta\ell_n(\boldsymbol{\theta}_0))\xrightarrow{(d)}\chi_d^2$$

### Wald's test {#wald}

Considering that under certain technical conditions, the [MLE](/2022/04/26/methods-of-estimation.html#mle) is asymptotically Normal, it follows that its quadratic form is $$\chi^2$$ distributed, if properly scaled. In particular, assuming $$H_0:\boldsymbol{\theta}=\boldsymbol{\theta}_0$$ one can test if $$\lVert\sqrt{nI(\boldsymbol{\theta})}\left(\hat{\boldsymbol{\Theta}}_n-\boldsymbol{\theta}_0\right)\rVert_2^2$$ is sufficiently large to reject the null. This is straightforward, if one considers the univariate case first, bearing in mind that $$I(\theta)$$ is the [Fisher information](/2022/04/26/methods-of-estimation.html#score).

$$T_n=nI(\hat\Theta_n)(\hat\Theta_n-\theta_0)^2\xrightarrow{(d)}nI(\theta)(\hat\Theta_n-\theta_0)^2=nI(\theta)(\hat\Theta_n-\theta)^2\xrightarrow{(d)}\chi_1^2$$

Note that $$T_n$$ is a quadratic form of a random variable that otherwise is Normally distributed. Hence, $$T_n$$ is employed in **two-sided** tests and proper care is necessary in the selection of quantiles{% if jekyll.environment == "development" %} (see [Stats HW7 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw7_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw7_u4hyptest-tab4)){% endif %}. Apart from this, note that the above test may use $$I(\theta_0)$$ instead of $$I(\hat\Theta_n)$${% if jekyll.environment == "development" %} (see [Stats MT2 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm2-tab6)){% endif %}. In principle, either can be used, although $$I(\hat\Theta_n)$$ may be preferred when available or if no additional information is provided{% if jekyll.environment == "development" %} (see [Stats L14 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab9)){% endif %}. When in doubt, [simulation studies](/2022/07/15/hypothesis-testing.html#sstudies) can provide a better insight on the more appropriate test to consider.

If $$\boldsymbol{\theta}\in\mathbb R^d$$ is multivariate, our test statistic will take the following form{% if jekyll.environment == "development" %} (see [Stats L14 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab6)){% endif %}.

$$T_n=n(\hat{\boldsymbol\Theta}_n-\boldsymbol\theta_0)^TI(\hat{\boldsymbol\Theta}_n)(\hat{\boldsymbol\Theta}_n-\boldsymbol\theta_0)\xrightarrow{(d)}\chi_d^2$$

Wald's test can be naturally extended to test **implicit hypotheses**, e.g. when one parameter space is a linear combination of other parameter dimensions.

Assume $$\boldsymbol{A}$$ that maps $$\boldsymbol{\theta}$$ into $$\mathbb R^k$$, where $$k<d$$, and $$H_0:\boldsymbol{A}\boldsymbol{\theta}=\boldsymbol{0}$$. Since $$\hat{\boldsymbol{\Theta}}_n\xrightarrow{(d)}\mathcal N(\boldsymbol{\theta},I^{-1}(\boldsymbol{\theta}))$$, its [linear transformation](/2022/01/24/further-topics-on-RV.html#multivariate_normal) under the null is $$\boldsymbol{A}\hat{\boldsymbol{\Theta}}_n\xrightarrow{(d)}\mathcal N(\boldsymbol{0},\boldsymbol{\Gamma}(\boldsymbol{\theta}))$$, where $$\boldsymbol{\Gamma}(\boldsymbol{\theta})=\boldsymbol{A}I^{-1}(\boldsymbol{\theta})\boldsymbol{A}^T$$. This means that the test statistic in the lower-dimension space can be defined as follows, keeping in mind that $$\hat{\boldsymbol{\Theta}}_n\xrightarrow{\mathbb P}\boldsymbol{\theta}$${% if jekyll.environment == "development" %} (see [Stats L14 Q13](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab13)){% endif %}.

$$T_n=n(\boldsymbol{A}\hat{\boldsymbol{\Theta}}_n)^T\boldsymbol{\Gamma}^{-1}(\hat{\boldsymbol{\Theta}}_n)(\boldsymbol{A}\hat{\boldsymbol{\Theta}}_n)\xrightarrow{(d)}\chi_k^2$$

The above approach can be generalized to any function $$g:\mathbb R^d\rightarrow\mathbb R^k$$, at the condition that $$g(\cdot)$$ is continuously differentiable. In its **general form**, the Wald's test assumes $$H_0:g(\boldsymbol{\theta})=\mathbf0$$ (or any of the associated inequalities){% if jekyll.environment == "development" %} (see [Stats L14 Q12](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab12) and [Stats HW7 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw7_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw7_u4hyptest-tab1)){% endif %} and the test statistic takes the following form.

$$T_n=n(g(\hat{\boldsymbol{\Theta}}_n))^T\boldsymbol{\Gamma}^{-1}(\hat{\boldsymbol{\Theta}}_n)(g(\hat{\boldsymbol{\Theta}}_n))\xrightarrow{(d)}\chi_k^2$$

Where $$\boldsymbol{\Gamma}(\boldsymbol{\theta})=(\nabla_\theta g(\boldsymbol{\theta}))^T I^{-1}(\boldsymbol{\theta})(\nabla_\theta g(\boldsymbol{\theta}))$$ is the result of [multivariate Delta](/2022/03/24/foundation-of-inference.html#multivariate_delta) method.

### Wilks' (likelihood ratio) test {#wilks}

Bearing in mind the introduction to [LRT](/2022/07/15/hypothesis-testing.html#lrt), consider the following statistic, which according to [Wilks' theorem](https://en.wikipedia.org/wiki/Wilks%27_theorem) is asymptotically $$\chi^2$$ distributed under the null.

$$T_n=2\ln\frac{\mathcal L_n(\hat{\boldsymbol{\Theta}}_n)}{\mathcal L_n(\boldsymbol\theta_0)}=2(\ell_n(\hat{\boldsymbol{\Theta}}_n)-\ell_n(\boldsymbol\theta_0))\xrightarrow{(d)}\chi_d^2$$

To see that, take the univariate case and the second order Taylor expansion of $$\ell_n(\theta_0)$$ near $$\ell_n(\hat\Theta_n)$$.

$$\begin{align}
2(\ell_n(\hat\Theta_n)-\ell_n(\theta_0))
&\approx2(\ell_n(\hat\Theta_n)-(\ell_n(\hat\Theta_n)+(\theta_0-\hat\Theta_n)\cancelto{=0}{\ell_n'(\hat\Theta_n)}+\frac1 2(\theta_0-\hat\Theta_n)^2\ell_n''(\hat\Theta_n)))\\
&=n(\theta_0-\hat\Theta_n)^2\frac1n(-\ell_n''(\hat\Theta_n))\xrightarrow{(d)}nI(\hat\Theta_n)(\hat\Theta_n-\theta_0)^2\xrightarrow{(d)}\chi_1^2
\end{align}$$

Again, if $$\boldsymbol{\theta}\in\mathbb R^d$$ is multivariate, the test statistic becomes as follows (see Wald's test for analogy){% if jekyll.environment == "development" %} (see [Stats HW7 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw7_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw7_u4hyptest-tab2) and [Stats HW7 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw7_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw7_u4hyptest-tab3)){% endif %}.

$$T_n=2(\ell_n(\hat{\boldsymbol\Theta}_n)-\ell_n(\boldsymbol{\theta}_0))\approx n(\hat{\boldsymbol\Theta}_n-\boldsymbol\theta_0)^TI(\hat{\boldsymbol\Theta}_n)(\hat{\boldsymbol\Theta}_n-\boldsymbol\theta_0)\xrightarrow{(d)}\chi_d^2$$

Wilks' theorem applies as well to a more general problem, which considers a **constrained** MLE, that is $$\hat{\boldsymbol{\Theta}}_n^c=\arg\max_{\theta\in\Theta_0}\ell_n(\boldsymbol\theta)$$. To give an idea, consider the following unconstrained and constrained MLEs, respectively.

$$\begin{align}
\hat{\boldsymbol{\Theta}}_n=\begin{bmatrix}\hat{\boldsymbol\Theta}_n^\star\\\hat{\boldsymbol{\Theta}}_n'\end{bmatrix}&&\hat{\boldsymbol{\Theta}}^c_n=\begin{bmatrix}\hat{\boldsymbol\Theta}_n^\star\\\boldsymbol\theta_0'\end{bmatrix}
\end{align}$$

In the above, $$\hat{\boldsymbol\Theta}_n^\star\in\mathbb R^r$$ indicates the *common* unconstrained element of both MLEs, where $$r$$ indicates the unconstrained dimensions. Since $$(\hat{\boldsymbol{\Theta}}_n-\hat{\boldsymbol{\Theta}}^c_n)=\begin{bmatrix}\boldsymbol0^T&(\hat{\boldsymbol\Theta}_n'-\boldsymbol\theta_0')^T\end{bmatrix}$$, we have the following result.

$$T_n=2(\ell_n(\hat{\boldsymbol\Theta}_n)-\ell_n(\hat{\boldsymbol\Theta}_n^c))\xrightarrow{(d)}\chi_{d-r}^2$$

The above considers a special case, when $$\hat{\boldsymbol{\Theta}}_n^\star$$ is part of both $$\hat{\boldsymbol{\Theta}}_n$$ and $$\hat{\boldsymbol{\Theta}}_n^c$$, which may not be true in general. The formal proof considers $$T_n=2(\ell_n(\hat{\boldsymbol\Theta}_n)-\ell_n(\boldsymbol{\theta})+\ell_n(\boldsymbol{\theta})-\ell_n(\hat{\boldsymbol{\Theta}}_n^c))$$, where certain quadratic elements in the first two terms $$(\ell_n(\hat{\boldsymbol\Theta}_n)-\ell_n(\boldsymbol{\theta}))$$ will cancel out $$r$$ quadratic terms in the last two terms $$(\ell_n(\boldsymbol{\theta})-\ell_n(\hat{\boldsymbol{\Theta}}_n^c))$$.

Finally, since unconstrained MLE is the maximizer of the likelihood in a *larger* space, it is not possible for a constrained MLE to be a maximizer better than that. In other words, $$\ell_n(\hat{\boldsymbol{\Theta}}_n)\ge\ell_n(\hat{\boldsymbol{\Theta}}_n^c)$$ always{% if jekyll.environment == "development" %} (see [Stats L14 Q11](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s04_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s04_hypotesting-tab11)){% endif %}.

## Goodness of fit test {#gof}

So far, we saw the [parameters estimation](/2022/04/26/methods-of-estimation.html#intro) and [parameter Hypothesis Testing](/2022/07/15/hypothesis-testing.html#parameter_testing), and in both cases we could develop methods based on the assumption that the underlying probability law is known and is fixed. However, there is a family of methods that aim at solving a more general problem, where they test if the probability law governing our observations is an exact candidate distribution. Indeed, the parameter Hypothesis Testing is a special case of **goodness of fit** testing, which is also a topic in non parametric statistics.

As a practical example, assume that a random sequence $$X_1,\dots,X_n\sim\mathcal P$$ is observed. Probability law $$\mathcal P$$ is unknown, but we can test if $$\text{Cat}(\mathbf p_0)$$ could have generated $$X_1,\dots,X_n$$, with certain probability or, alternatively, with some statistical evidence{% if jekyll.environment == "development" %} (see [Stats L15 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab4)){% endif %}. In other words, we test a null hypothesis of the form $$H_0:\mathbf p=\mathbf p_0$$. Note that $$\mathbf p_0$$ can in turn be a function of a smaller set of parameters $$\boldsymbol\theta$$, that is $$\mathbf p_0=\mathbf p_0(\boldsymbol\theta)$$, where the unknown $$\boldsymbol{\theta}$$ can be estimated as $$\boldsymbol\theta=\hat{\boldsymbol{\Theta}}_n$$.

### $$\chi^2$$ test

Considering that [Categorical distribution](/2022/01/24/further-topics-on-RV.html#categorical) can generalize any [discrete distribution](/2022/01/08/discrete-random-variables.html#basic) over a size $$d$$ sample space, and that [MLE](/2022/04/26/methods-of-estimation.html#mle) of $$\text{Cat}(\mathbf p)$$ is $$\hat{\mathbf p}=\bar{\mathbf X}_n$${% if jekyll.environment == "development" %} (see [Stats L15 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab5)){% endif %}, we can rely on the [Pearson's theorem](/2022/07/15/hypothesis-testing.html#pearson) to perform a test of the form $$H_0:\mathbf p=\mathbf p_0$$, by defining the following test statistic{% if jekyll.environment == "development" %} (see [Stats L15 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab9) and [Stats HW8 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw8_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw8_u4hyptest-tab4)){% endif %}.

$$T_n=\sum_{j=1}^d n\frac{(\hat p_j-p_j)^2}{p_j}\xrightarrow{(d)}\chi_{d-1}^2$$

It is comforting to see that when $$d=2$$, $$T_n=n\frac{(\hat p-p)^2}{p(1-p)}\xrightarrow{(d)}\chi_1^2$$, which is exactly the same as with [Wald's test](/2022/07/15/hypothesis-testing.html#wald) for Bernoulli case{% if jekyll.environment == "development" %} (see [Stats L15 Q10](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab10)){% endif %}. One may be tempted to say that it is just a matter of plugging $$\text{diag}^{-1}(\mathbf p_0)$$ into the Wald test. However, in a separate discussion we already saw that the diagonal matrix computed in this way is not the correct Fisher information{% if jekyll.environment == "development" %} (see [Stats L15 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab6)){% endif %}.

If $$\mathbf p_0=\begin{bmatrix}p_1(\boldsymbol{\theta}_0)&\dots&p_d(\boldsymbol{\theta}_0)\end{bmatrix}^T$$ depends on some $$\boldsymbol{\theta}_0\in\mathbb R^r$$ that comes from an assumed statistical model, $$(\Omega,\{\mathcal P_\theta\}_{\theta\in\Theta})$$, then the degrees of freedom are reduced because of the additional constraints imposed on $$p_j$$. The additional constraints are $$r$$, which means that $$T_n$$ will be tested against a $$\chi^2_{d-1-r}$${% if jekyll.environment == "development" %} (see [Stats L15 Q11](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab11) and [Stats HW8 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw8_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw8_u4hyptest-tab1)){% endif %}.

$$T_n=\sum_{j=1}^d n\frac{(\hat p_j-p_j(\boldsymbol{\theta}_0))}{p_j(\boldsymbol{\theta}_0)}\xrightarrow{(d)}\chi_{d-1-r}^2$$

Note that if we set $$\boldsymbol\theta_0$$ to some desired constants, then we would be performing a goodness of fit test, together with a parameter estimation. If, on the other hand, $$\boldsymbol{\theta}_0$$ is not pre-determined and is defined as $$\boldsymbol{\theta}_0=\hat{\boldsymbol{\Theta}}_n$$, then we would be performing a pure goodness of fit test{% if jekyll.environment == "development" %} (see [Stats L15 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s05_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s05_hypotesting-tab2)){% endif %}.

### Empirical CDF {#ecdf}

Natural estimator of $$F_X(x)=\mathbb P(X\le x)=\mathbb E[\mathbb 1(X\le x)]$$ is $$F_n(x)=\frac1n\sum_{i=1}^n\mathbb 1(X_i\le x)$$, known as **empirical CDF** (ECDF){% if jekyll.environment == "development" %} (see [Stats L16 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab3)){% endif %}. Using [LLN](/2022/02/21/introduction-to-statistics.html#wlln) result, we can claim that $$F_n(x)\xrightarrow{a.s.}F_X(x)$$, for any $$x\in\mathbb R$$, where $$F_X(x)$$ is deterministic number $$\in[0,1]$$, while $$F_n(x)$$ is random because it depends on the sample{% if jekyll.environment == "development" %} (see [Stats L16 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab4)){% endif %}. This property can also be referred to as the **pointwise** convergence.

However, if the objective is to analyze the convergence of $$F_n(x)$$ to $$F_X(x)$$ *simultaneously* over the entire real line, we are looking for a stronger, **uniform** convergence. In particular, [Glivenko-Cantelli theorem](/2022/07/15/hypothesis-testing.html#gc) (GC) proves that $$F_n(x)$$ converges towards $$F_X(x)$$ at a rate that is *uniform* throughout the entire domain $$x\in\mathbb R$$, or $$\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\xrightarrow{a.s.}0$$.

Recall that according to [CLT](/2022/02/21/introduction-to-statistics.html#clt_mean), $$\sqrt n(F_n(x)-F_X(x))\xrightarrow{(d)}\mathcal N(0,F_X(x)(1-F_X(x)))$${% if jekyll.environment == "development" %} (see [Stats L16 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab5)){% endif %}. Functional extension of the CTL to uniform can be obtained by applying $$\sup_{x\in\mathbb R}\lvert\cdot\rvert$$ on both sides, and define $$T_n$$ as the relevant test statistic.

$$\begin{align}
\sqrt n(F_n(x)-F_X(x)&\xrightarrow{(d)}\mathcal N(0,F_X(x)(1-F_X(x)))\\
\sup_{x\in\mathbb R}\lvert\sqrt n(F_n(x)-F_X(x))\rvert&\xrightarrow{(d)}\sup_{x\in\mathbb R}\lvert\mathcal N(0,F_X(x)(1-F_X(x)))\rvert\\
T_n=\sqrt n\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert&\xrightarrow{(d)}\sup_{t\in[0,1]}\lvert\mathcal N(0,t(1-t))\rvert=\sup_{t\in[0,1]}\lvert\mathbb B(t)\rvert\\
T_n&\xrightarrow{(d)}\sup_{t\in[0,1]}\lvert\mathbb B(t)\rvert
\end{align}$$

The above result is one of the consequences of the [Donsker's theorem](/2022/02/08/bernoulli-and-poisson-processes.html#donsker), where $$\mathbb B(t)$$ is the [Brownian bridge](/2022/07/15/hypothesis-testing.html#bbridge) on $$t\in[0,1]$$. Distribution of the Brownian bridge, as well as the supremum of its absolute, is *pivotal* and does not depend on the distribution of $$X$$ nor any of its parameters. It is worthy noting that where $$\mathbb B(t)$$ is a random curve, its **supremum** is a r.v. and that $$T_n$$ will converge to it only under the null $$H_0:F_n=F_X$${% if jekyll.environment == "development" %} (see [Stats L16 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab6)){% endif %}.

### Kolmogorov-Smirnov test {#ks}

The supremum of the absolute value of the Brownian bridge is useful to determine the *asymptotic* distribution of $$T_n=\sqrt n\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert$$, which becomes viable as an approximation for $$n$$ greater than $$35-50$$, depending on the reference literature. Kolmogorov and Smirnov, on the other hand, came up with a method to derive appropriate critical value $$c_\alpha$$, even for small $$n$$. To this end, assume that we collect $$X_i\sim\mathcal P$$ of size $$n$$ and determine their *order statistics* $$X_{(j)}$$.

Since $$F_n(x)$$ is piecewise constant and $$F_X(x)$$ is monotonically increasing, for $$x\in[X_{(j-1)},X_{(j)})$$, $$\lvert F_n(x)-F_X(x)\rvert\le\max\{\lvert F_n(X_{(j-1)})-F_X(X_{(j-1)})\rvert,\lvert F_n(X_{(j)}^-)-F_X(X_{(j)}^-)\rvert\}$$, where $$X_{(j)}^-$$ is the leftmost limit of $$X_{(j)}$$. Collecting intervals from $$[-\infty,X_{(1)}^-]$$ to $$[X_{(n)},\infty]$$, the overall maximum becomes as follows.

$$\begin{align}
\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\le\max\{
    &\overbrace{\lvert F_n(-\infty)-F_X(-\infty)\rvert}^{=0},{\color{red}\lvert F_n(X_{(1)}^-)-F_X(X_{(1)}^-)\rvert},\\
    &{\color{red}\lvert F_n(X_{(1)})-F_X(X_{(1)})\rvert},{\color{blue}\lvert F_n(X_{(2)}^-)-F_X(X_{(2)}^-)\rvert},\\
    &\dots\\
    &{\color{blue}\lvert F_n(X_{(n-1)})-F_X(X_{(n-1)})\rvert},{\color{green}\lvert F_n(X_{(n)}^-)-F_X(X_{(n)}^-)\rvert},\\
    &{\color{green}\lvert F_n(X_{(n)})-F_X(X_{(n)})\rvert},\underbrace{\lvert F_n(\infty)-F_X(\infty)\rvert}_{=0}\}
\end{align}$$

$$\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\le\max_{j=1,\dots,n}\{\max\{\lvert F_n(X_{(j)}^-)-F_X(X_{(j)}^-)\rvert,\lvert F_n(X_{(j)})-F_X(X_{(j)})\rvert\}\}$$

Finally, replace $$F_n(X_{(j)}^-)=\frac{j-1}n$$, $$F_n(X_{(j)})=\frac{j}n$$ and $$F_X(X_{(j)}^-)=F_X(X_{(j)})$$.

$$\begin{gather}
\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert=\max_{j=1,\dots,n}\left\{\max\left\{\left\lvert\frac{j-1}n-F_X(X_{(j)})\right\rvert,\left\lvert\frac{j}n-F_X(X_{(j)})\right\rvert\right\}\right\}\\
\implies T_n=\sqrt n\max_{j=1,\dots,n}\left\{\max\left\{\left\lvert\frac{j-1}n-F_X(X_{(j)})\right\rvert,\left\lvert\frac{j}n-F_X(X_{(j)})\right\rvert\right\}\right\}
\end{gather}$$

The above computation of $$T_n$$ is fairly efficient, because we are computing $$2n$$ comparisons, instead of infinite theoretically required by $$\sup_{x\in\mathbb R}$$. Furthermore, the distribution of $$T_n$$ is pivotal and does not depend on $$F_X(x)$$. For this reason, we can rely on dedicated [KS tables](http://fcaglp.unlp.edu.ar/~observacional/papers/PDFs/statistics/app3.pdf) which report [critical values](/2022/03/24/foundation-of-inference.html#testing) $$c_\alpha$$ in function of desired $$n$$ and $$\alpha$$. Be aware that most KS tables omit the $$\sqrt n$$ scaling factor{% if jekyll.environment == "development" %} (see [Stats L16 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab9)){% endif %}.

If the tables are not available, one can *simulate* the distribution of $$T_n$$ and derive $$c_\alpha$$ independently (which is how KS tables were derived in the first place). To do this, note that $$F_X(X)\sim\text{Unif}(0,1)$$ for [any distribution](/2022/01/24/further-topics-on-RV.html#simulation) with invertible CDF{% if jekyll.environment == "development" %} (see [Stats L16 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab8)){% endif %}. If $$F_X(x)$$ is not invertible, similar result can be obtained with proper adjustments. Therefore, one can collect $$U_i\overset{\text{i.i.d.}}{\sim}\text{Unif}([0,1])$$ and find $$c_\alpha$$ s.t. $$\mathbb P(D_n\ge c_\alpha)\approx\alpha$$, where $$D_n=\sqrt n\max_{j=1,\dots,n}\left\{\max\left\{\left\lvert\frac{j-1}n-U_{(j)}\right\rvert,\left\lvert\frac{j}n-U_{(j)}\right\rvert\right\}\right\}$$.

As for the computational complexity, this method requires generating $$n$$ Uniform r.v., computing $$2n$$ differences and choosing the maximum one, which has a fair linear requirement in time and space on a regular computer{% if jekyll.environment == "development" %} (see [Stats L16 Q7](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab7)){% endif %}. Follows a simulation for $$n=10$$ and $$\alpha=0.05$$. From KS tables, we observe that the critical value is $$0.40925$$, excluding the scaling factor $$\sqrt n$$. Accordingly, $$c_\alpha=\sqrt{10}\times0.40925=1.294162$$ is what should be obtained (approximately) from the simulation below.

<iframe width='100%' height='950' src='https://rdrr.io/snippets/embed/?code=n%3C-10%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20trials%0Ak%3C-1e5%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20experiments%0Aa%3C-0.05%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20test%20level%0AU%3C-matrix(runif(n*k)%2Cnrow%3Dk)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20generate%20experiments%0Aj%3C-t(apply(U%2C1%2Crank))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20order%20vectors%0ADn%3C-apply(pmax(abs((j-1)%2Fn-U)%2Cabs(j%2Fn-U))%2C1%2Cmax)%20%20%20%20%20%20%20%20%23%20compute%20Dn%0Ahg%3C-hist(Dn%2Cfreq%3DFALSE%2Cbreaks%3D1%3A100%2F100)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20distribution%20of%20Dn%0Aca%3C-quantile(Dn%2Cprobs%3D1-a)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20test%20threshold%0A%0A%23%20critical%20value%20as%20shown%20in%20tables%0Asprintf(%22%25.2f%20quantile%20for%20simulated%20KS%20%3D%20%25f%20%2F%20rescaled%20%3D%20%25f%22%2C%0A%20%20%20%20%20%20%20%201-a%2Cca%2Csqrt(n)*ca)' frameborder='0'></iframe>

### Kolmogorov-Lilliefors (normality) test {#kl}

KS test is appropriate when all parameters of the reference distribution $$F_X(x)$$ are known, which is more [parameters Hypothesis Testing](/2022/07/15/hypothesis-testing.html#parameter_testing) than [goodness of fit](/2022/07/15/hypothesis-testing.html#gof) test. What happens in practice is that we assume a family of probability laws and estimate associated parameters, eventually usng the most suitable [MLE](/2022/04/26/methods-of-estimation.html#mle).

Assume we observe a sample $$X_i\overset{\text{i.i.d.}}{\sim}\mathcal P$$. We have no idea what $$\mathcal P$$ might be, and we assume it could follow a Normal distribution. However, as we are not aware of its parameters we decide to estimate them using an MLE of the form $$\begin{bmatrix}\hat\mu&\hat{\sigma}^2\end{bmatrix}^T$$. For this reason, our null becomes $$H_0:\mathcal P=\mathcal N(\hat\mu,\hat\sigma^2)$$.

If we use a statistic of the form $$T_n=\sqrt n\sup_{x\in\mathbb R}\lvert F_n(x)-\Phi_{\hat\mu,\hat s^2}(x)\rvert$$ we cannot use the KS table anymore, because $$\Phi_{\hat\mu,\hat s^2}(x)$$ has been already **tailored to fit best the data**. In this cases, Lilliefors proposed a [different table](https://d3i71xaburhd42.cloudfront.net/4aad1756e88dba86399a75891895e00b160f5460/3-Table1-1.png), which foresees smaller critical values to better react in the case of departure from the reference distribution{% if jekyll.environment == "development" %} (see [Stats L16 Q11](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab11)){% endif %}.

In practice, Lilliefors simulated a random sample from the standard Normal distribution, he computed empirical means and variances and finally derived the distribution of $$T_n$$. In this setting, he observed that at any given $$\alpha$$ level the critical values are visibly lower. For example, at $$n=10$$ and $$\alpha=0.05$$, $$c_\alpha=\sqrt{10}\times0.258=0.8158676$$.

<iframe width='100%' height='950' src='https://rdrr.io/snippets/embed/?code=n%3C-10%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20trials%0Ak%3C-1e5%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20experiments%0Aa%3C-0.05%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20test%20level%0AU%3C-matrix(runif(n*k)%2Cnrow%3Dk)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20generate%20experiments%0Aj%3C-t(apply(U%2C1%2Crank))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20order%20vectors%0ADn%3C-apply(pmax(abs((j-1)%2Fn-U)%2Cabs(j%2Fn-U))%2C1%2Cmax)%20%20%20%20%20%20%20%20%23%20compute%20Dn%0Ahg%3C-hist(Dn%2Cplot%3DFALSE%2Cbreaks%3D0%3A100%2F100)%0Aca%3C-quantile(Dn%2Cprobs%3D1-a)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20test%20threshold%0A%0A%23%23%23%20compute%20Dn1%20against%20a%20tailored%20normal%20distribution%20%20%23%23%23%0AR%3C-matrix(rnorm(n*k)%2Cnrow%3Dk)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20generate%20normal%20sample%0Am%3C-apply(R%2C1%2Cmean)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20MLE%20mean%0As%3C-sqrt(apply(R%2C1%2Cvar))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20MLE%20var%2Fsd%0AU1%3C-t(sapply(1%3Anrow(R)%2Cfunction(i)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20Phi%0A%20%20pnorm(R%5Bi%2C%5D%2Cmean%3Dm%5Bi%5D%2Csd%3Ds%5Bi%5D)))%0Aj1%3C-t(apply(U1%2C1%2Crank))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20order%20vectors%0ADn1%3C-apply(pmax(abs((j1-1)%2Fn-U1)%2Cabs(j1%2Fn-U1))%2C1%2Cmax)%20%20%20%23%20compute%20Dn%0Ahg1%3C-hist(Dn1%2Cplot%3DFALSE%2Cbreaks%3D0%3A100%2F100)%0Aca1%3C-quantile(Dn1%2Cprobs%3D1-a)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20test%20threshold%0A%0Aplot(hg%2Cfreq%3DFALSE%2Cxlim%3Drange(c(Dn%2CDn1))%2Cxlab%3D%22%22%2C%0A%20%20%20%20%20ylim%3Dc(0%2Cmax(hg%24density%2Chg1%24density))%2Ccol%3D%22grey%22%2C%0A%20%20%20%20%20main%3D%22KS%2FKL%20statistic%20distributions%22)%0Aplot(hg1%2Cfreq%3DFALSE%2Ccol%3Drgb(1%2C0%2C0%2C.5)%2Cadd%3DTRUE)%0Alegend(.5%2C4%2Clegend%3Dc(%22KS%22%2C%22KL%22)%2Cfill%3Dc(%22grey%22%2Crgb(1%2C0%2C0%2C.5)))%0A%0Asprintf(%22%25.2f%20quantile%20for%20simulated%20KS%20%3D%20%25f%20%2F%20rescaled%20%3D%20%25f%22%2C%0A%20%20%20%20%20%20%20%201-a%2Cca%2Csqrt(n)*ca)%0Asprintf(%22%25.2f%20quantile%20for%20simulated%20KL%20%3D%20%25f%20%2F%20rescaled%20%3D%20%25f%22%2C%0A%20%20%20%20%20%20%20%201-a%2Cca1%2Csqrt(n)*ca1)' frameborder='0'></iframe>

Lilliefors' approach can be extended to other distributions, provided that the appropriate MLE is used to estimate its parameters and new $$c_\alpha$$ are determined via simulation. Anyhow, the KL tables are usually the first step in testing normality of a sample, before carrying out a [$$t$$ test](/2022/07/15/hypothesis-testing.html#ttest) on its parameter $$\mu$$.

### QQ plots {#qq}

Another (less formal) goodness of fit test is given by quantile-quantile (QQ) plot, where alternatively to comparing $$F_n(X_i)$$ with $$F_X(X_i)$$ one draws points $$\left(F_X^{-1}(\frac in),F_n^{-1}\left(\frac in\right)\right)$$, which is the same as $$\left(q_{1-\frac in},X_{(i)}\right)$$, and inspects how they stack up together **visually**{% if jekyll.environment == "development" %} (see [Stats L16 Q13](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab13) and [Stats HW8 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw8_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw8_u4hyptest-tab2)){% endif %}.

QQ plot is particularly handy to test the normality of a distribution, which is the default method in many software applications. In essence, if QQ points are distributed along the $$y=x$$ line, then the sample is likely drawn from a Normal distribution{% if jekyll.environment == "development" %} (see [Stats L16 Q15](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab15)){% endif %}. To achieve this, some software packages normalize the sample by taking $$X_i'=\frac{X_i-\bar X_n}s$$ and then compare it with quantiles from $$\mathcal N(0,1)$$, by drawing a scatter plot with points $$\left(\Phi^{-1}(\frac in),X_{(i)}'\right)$${% if jekyll.environment == "development" %} (see [Stats HW8 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw8_u4hyptest/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw8_u4hyptest-tab3)){% endif %}.

To get the idea, consider the following cases in which the sample is drawn from $$\mathcal N(0,1)$$ (Normal distribution), $$t_5$$ (distribution with tails heavier than Normal), $$\text{Unif}(0,1)$$ (distribution with tails thinner than Normal), $$\text{Exp}(1)$$ (right skewed distribution), and $$\chi_1^2$$ (left skewed distribution). Uncomment the appropriate assignment to `X` variable and try the various cases{% if jekyll.environment == "development" %} (see [Stats L16 Q16](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab16), [Stats L16 Q17](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u04s06_hypotesting/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u04s06_hypotesting-tab17) and [Stats MT2 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@midterm2/block-v1:MITx+18.6501x+2T2021+type@vertical+block@midterm2-tab4)){% endif %}.

<iframe width='100%' height='950' src='https://rdrr.io/snippets/embed/?code=zs%3C-seq(-3%2C3%2C.01)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20points%20for%20N(0%2C1)%0Az%3C-dnorm(zs)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20PDF%20of%20N(0%2C1)%0An%3C-1e4%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20sample%20size%0A%0AX%3C-rnorm(n%2Cmean%3D0%2Csd%3Dsqrt(1))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20X~N(0%2C1)%0A%23%20X%3C-rt(n%2Cdf%3D5)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20X~t_5%0A%23%20X%3C-runif(n)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20X~U(0%2C1)%0A%23%20X%3C-rexp(n)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20X~Exp(1)%0A%23%20X%3C--rchisq(n%2Cdf%3D1)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20X~-ChiSq(1)%0A%0Apar(pty%3D%22s%22%2Cmfrow%3Dc(1%2C2))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20side-by-side%20graphs%0Ahist(X%2Cfreq%3DFALSE%2Cxlim%3Dc(-4%2C4)%2Cylim%3Dc(0%2C1.2))%20%23%20hist%20of%20X%0Alines(zs%2Cz%2Ccol%3D%22red%22)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20N(0%2C1)%20line%0Aqqnorm(X)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20QQ%20plot%20of%20X%0Aqqline(X%2Ccol%3D%22red%22)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20reference%20line' frameborder='0'></iframe>

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

### $$\chi^2$$ distribution {#chisq}

Consider the case when $$\sum_{i=1}^k Z_i^2\sim\chi_k^2$$ with $$k=1$$, that is $$Z^2\sim\chi_1^2$$. To compute $$F_{Z^2}(t)$$, where $$t\ge0$$, observe as follows.

$$\begin{align}
F_{Z^2}(t)=\mathbb P(Z^2\le t)
&=\mathbb P(\lvert Z\rvert\le\sqrt t)=2\mathbb P(0\le Z\le\sqrt t)\\
&=2(\mathbb P(Z\le\sqrt t)-2\mathbb P(Z\le0))\\
&=2\Phi(\sqrt t)-2\Phi(0)=2\Phi(\sqrt t)-1
\end{align}$$

Accordingly, $$f_{Z^2}(t)$$ can be [derived](/2022/01/24/further-topics-on-RV.html#derived_distributions) as $$\frac\partial{\partial t}F_{Z^2}(t)$$.

$$\begin{align}
f_{Z^2}(t)
&=\frac\partial{\partial t}F_{Z^2}(t)=\frac\partial{\partial t}(2\Phi(\sqrt t)-1)\\
&=2f_Z(\sqrt t)\frac 1{2\sqrt t}=\frac1{\sqrt{2\pi}}e^{-\frac 1 2 t}t^{-\frac 1 2}\\
&=\frac{\left(\frac 1 2\right)^{\frac 1 2}}{\Gamma\left(\frac 1 2\right)}t^{\frac 1 2-1}e^{-\frac 1 2 t}
\end{align}$$

The last equation can be written as $$f_{Z^2}(t)=\frac{\beta^\alpha}{\Gamma(\alpha)}t^{\alpha-1}e^{-\beta t}$$, with $$\alpha=\beta=\frac 1 2$$, that is the PDF of $$\text{Gamma}(\alpha,\beta)$$. In other words, $$Z^2\sim\chi^2_1=\text{Gamma}\left(\frac 1 2,\frac 1 2\right)$$ and therefore $$M_{\chi_1^2}(t)=(1-2t)^{-\frac12}$$. Since, [MGF](/2022/04/26/methods-of-estimation.html#mgf) of sum of $$k$$ i.i.d. copies of $$\chi_1^2$$ distributed r.v. is $$M_{\chi_k^2}(t)=(M_{\chi_1^2}(t))^k=(1-2t)^{-\frac 1 2 k}$$, it follows that $$\chi_k^2$$ distribution is essentially a $$\text{Gamma}\left(\frac12k,\frac12\right)$$ distribution.

It is beneficial recalling that Gamma is a generalization of an [Erlang](/2022/01/13/continuous-random-variables.html#basic) distribution, where $$k\ge0$$ is not necessarily integer. In particular, this means that if $$k=2l$$, then $$\chi_k^2\sim\text{Erlang}\left(l,\frac 1 2\right)$$, including the special case $$\chi_2^2\sim\text{Exp}\left(\frac 1 2\right)$$. This means that expectation and variance of $$\chi_k^2$$ are immediately available as $$\mathbb E[\chi_k^2]=\frac{\frac 1 2 k}{\frac 1 2}=k$$ and $$\text{var}(\chi_k^2)=\frac{\frac 1 2 k}{\left(\frac 1 2\right)^2}=2k$$.

Often, we consider vector notation, that is $$\mathbf Z=\begin{bmatrix}Z_1&\dots&Z_n\end{bmatrix}^T\sim\mathcal N_n(\mathbf 0,\mathbf I_n)$$; in such case, *norm* is an alternative way of indicating $$\lVert\mathbf Z\rVert_2^2=\mathbf Z^T\mathbf Z=\sum_{i=1}^k Z_i^2\sim\chi_n^2$$.

### Cochran's theorem (sample mean and variance) {#cochran}

Consider [orthogonal matrices](/2022/01/24/further-topics-on-RV.html#orthogonal_matrix) $$\mathbf V\in\mathbb R^{n\times n}$$ and $$\mathbf W\in\mathbb R^{n\times n-1}$$, such that $$\mathbf V=\begin{bmatrix}\mathbf v_1&\mathbf W\end{bmatrix}$$, where $$\mathbf v_1=\frac1{\sqrt n}\mathbf 1_n$$ and observe that $$\mathbf W\mathbf W^T=\sum_{i=2}^n \mathbf v_i\mathbf v_i^T=\mathbf I_n-\mathbf v_1\mathbf v_1^T$$ and that $$\mathbf W^T\mathbf W=\mathbf I_{n-1}$$.

Consider also $$\mathbf Z\sim\mathcal N_n(\mathbf 0_n,\mathbf I_n)$$ and note that $$\mathbf V^T\mathbf Z\sim\mathcal N_n(\mathbf 0_n,\mathbf I_n)$$ and $$\mathbf W^T\mathbf Z\sim\mathcal N_{n-1}(\mathbf 0_{n-1},\mathbf I_{n-1})$$. Therefore, $$\lVert\mathbf V^T\mathbf Z\rVert_2^2\sim\chi_n^2$$ and $$\lVert\mathbf W^T\mathbf Z\rVert_2^2\sim\chi_{n-1}^2$$, respectively. In addition $$\mathbf v_1^T\mathbf Z\ind\mathbf W^T\mathbf Z$$, since $$\text{cov}(\mathbf v_1^T\mathbf Z,\mathbf W^T\mathbf Z)=\mathbb E[\mathbf v_1^T\mathbf Z\mathbf Z^T\mathbf W]-\mathbb E[\mathbf v_1^T\mathbf Z]\mathbb E[\mathbf Z^T\mathbf W]=\mathbf 0$$, which stems from $$\text{cov}(\mathbf Z)=\mathbf I_n$$ and $$\mathbf v_1^T\mathbf W=\mathbf 0$$, because $$\mathbf v_1$$ is orthogonal to each column of $$\mathbf W$$.

Bearing in mind that the sample mean and the sample variance can be rewritten in matrix notation as $$\hat\mu_Z=\bar Z_n=\frac1n\sum_{i=1}^n Z_i=\frac1{\sqrt n}\mathbf v_1^T\mathbf Z$$ and $$\hat\sigma_Z^2=\frac1n\sum_{i=1}^n(Z_i-\bar Z_n)^2=\frac1n\lVert(\mathbf I_n-\mathbf v_1\mathbf v_1^T)\mathbf Z\rVert_2^2$$, we can now reach the following conclusions of the Cochran's tehorem:

- $$n\hat\sigma_Z^2=\lVert\mathbf W\mathbf W^T\mathbf Z\rVert_2^2=\lVert\mathbf W^T\mathbf Z\rVert_2^2\sim\chi_{n-1}^2$$; and
- $$\mathbf v_1^T\mathbf Z\ind\mathbf W^T\mathbf Z\implies\hat\mu_Z\ind\hat\sigma_Z^2$$.

The above can be generalized for any $$\mathbf X\sim\mathcal N_n(\mu_X\mathbf 1_n,\sigma_X^2\mathbf I_n)$$. In particular, we would have as follows.

$$\begin{align}
n\hat\sigma_X^2&=\lVert\mathbf X-\mathbf v_1\mathbf v_1^T\mathbf X\rVert_2^2=\lVert(\mathbf X-\mu_X\mathbf 1_n)-(\mathbf v_1\mathbf v_1^T\mathbf X-\mu_X\mathbf 1_n)\rVert_2^2\\
&=\lVert(\mathbf I_n-\mathbf v_1\mathbf v_1^T)(\mathbf X-\mu_X\mathbf 1_n)\rVert_2^2=\sigma_X^2\left\lVert(\mathbf I_n-\mathbf v_1\mathbf v_1^T)\left(\frac{\mathbf X-\mu_X\mathbf 1_n}{\sigma_X}\right)\right\rVert_2^2\\
\implies\frac{n\hat\sigma_X^2}{\sigma_X^2}&=\lVert\mathbf W^T\mathbf Z\rVert_2^2\sim\chi_{n-1}^2
\end{align}$$

Where $$\mathbf X$$ has been [standardized](/2022/01/24/further-topics-on-RV.html#multivariate_normal) as a multivariate Normal r.v. with $$\mathbf Z=\frac{\mathbf X-\mu_X\mathbf1_n}{\sigma_X}$$.

### Cochran's theorem (general form)

In general, Cochran's theorem says that if $$\mathbf Z^T\mathbf Z=\sum_{j=1}^k \mathbf Q_j$$, with $$\mathbf Q_j=\mathbf Z^T\mathbf A_j\mathbf Z$$ and $$\mathbf A_j=\mathbf A_j^T$$, then any of the following three conditions implies the other two:

- $$\sum_{j=1}^k\text{rank}(\mathbf A_j)$$ is $$n$$;
- $$\mathbf Q_1,\dots,\mathbf Q_k$$ are independent;
- $$\mathbf Q_j\sim\chi_{\text{rank}(\mathbf A_j)}^2$$.

For simplicity, let's consider the case where the first statement implies the other two.

First, observe that $$\mathbf Z^T\mathbf Z=\sum_{j=1}^k\mathbf Z^T\mathbf A_j\mathbf Z\implies\sum_{j=1}^k\mathbf A_j=\mathbf I_n$$. Second, by [spectral theorem](/2022/01/24/further-topics-on-RV.html#spectral), $$\mathbf A_j$$ can be expressed as $$\mathbf U\mathbf D_j\mathbf U^T$$, where $$\mathbf D_j$$ and $$\mathbf U$$ are [diagonal](/2022/01/24/further-topics-on-RV.html#back-up) and [orthogonal](/2022/01/24/further-topics-on-RV.html#orthogonal_matrix) matrices, respectively. This means that $$\mathbf Z^T\mathbf Z=\mathbf X^T\mathbf X=\sum_{j=1}^k\mathbf X^T\mathbf D_j\mathbf X$$, with $$\mathbf X=\mathbf U^T\mathbf Z\sim\mathcal N_n(\mathbf 0_n,\mathbf I_n)$$, and therefore $$\sum_{j=1}^k\mathbf D_j=\mathbf I_n$$ as well.

Now, consider $$k=2$$ with $$\mathbf Q_1=\mathbf X^T\mathbf D\mathbf X$$ and $$\mathbf Q_2=\mathbf X^T(\mathbf I_n-\mathbf D)\mathbf X$$. Since $$\mathbf D=\text{diag}(\lambda_1,\dots,\lambda_n)$$, with $$\lambda_i$$ being eigenvalues of $$\mathbf A_1$$, it follows that if $$\text{rank}(\mathbf A_1)=r$$ then $$\mathbf D$$ will has $$r$$ non zero elements. Conversely, $$\text{rank}(\mathbf A_2)=n-r$$, that is the number of non zero elements of $$\mathbf I_n-\mathbf D$$. With proper arrangement, the two matrices can be expressed as follows.

$$\begin{align}
\mathbf D=\begin{bmatrix}\text{diag}(\lambda_1,\dots,\lambda_r)&0\\0&0\end{bmatrix}&&
\mathbf I_n-\mathbf D=\begin{bmatrix}\mathbf I_r-\text{diag}(\lambda_1,\dots,\lambda_r)&0\\0&\mathbf I_{n-r}\end{bmatrix}
\end{align}$$

By inspection, one should realize that $$\lambda_1=\dots=\lambda_r=1$$ is necessary so that both matrices are compatible with the assumed ranks. At the same time, this also means that eigenvalues of $$\mathbf D$$ can only be of the form $$\lambda_i\in\{0,1\}$$, which means that every $$X_i$$ is exclusive to either $$\mathbf Q_1$$ or $$\mathbf Q_2$$, which means that $$\mathbf D$$, $$\mathbf I_n-\mathbf D$$, $$\mathbf A_1$$ and $$\mathbf A_2$$ are all symmetric and [idempotent](/2022/01/24/further-topics-on-RV.html#back-up). Finally, the conclusion that can be generalized to any $$k\gt2$$ by induction.

$$\begin{gather}
\chi_r^2\sim\mathbf X^T\mathbf D\mathbf X\ind\mathbf X^T(\mathbf I_n-\mathbf D)\mathbf X\sim\chi_{n-r}^2\\
\chi_r^2\sim\mathbf Z^T\mathbf A_1\mathbf X\ind\mathbf Z^T\mathbf A_2\mathbf Z\sim\chi_{n-r}^2\\
\end{gather}$$

For a practical example, recall that $$\sqrt n\bar Z_n\xrightarrow{(d)}\mathcal N(0,1)$$. Therefore, $$n(\bar Z_n)^2\xrightarrow{(d)}\chi_1^2$$. At the same time, $$n(\bar Z_n^2)=\mathbf Z^T\mathbf A_1\mathbf Z$$, where $$\mathbf A_1=\frac1n\mathbf 1_n\mathbf 1_n^T$$. Since $$\mathbf A_1$$ is idempotent, $$\text{rank}(\mathbf A_1)=\text{tr}(\mathbf A_1)=1$$. On the other hand, $$\mathbf A_2=\mathbf I_n-\mathbf A_1$$ and $$\text{rank}(\mathbf A_2)=n-1$$. Finally, if we consider $$\mathbf Z^T\mathbf A_2\mathbf Z$$, it turns out that it is equal to $$\sum_{i=1}^n(Z_i-\bar Z_n)^2$$. Therefore, we conclude that $$\mathbf Z^T\mathbf A_1\mathbf Z\ind\mathbf Z^T\mathbf A_2\mathbf Z$$, which means that sample mean is independent from sample variance, and that the sample variance is distributed according to $$\chi_{n-1}^2$$.

$$\begin{align}
\mathbf Z^T\mathbf Z
&=\mathbf Z^T\mathbf A_1\mathbf Z+\mathbf Z^T(\mathbf I_n-\mathbf A_1)\mathbf Z\\
&=\underbrace{n(\bar Z_n)^2}_{\sim\chi_1^2}+\underbrace{\sum_{i=1}^n(Z_i-\bar Z_n)^2}_{\sim\chi_{n-1}^2}
\end{align}$$

### Derivation of the $$t$$ distribution {#tdist}

Derivation of the $$t_d$$ distribution can follow the same process described for [functions of multiple](/2022/01/24/further-topics-on-RV.html#derived_distributions_multiple) r.v. In this case, $$T_d=\frac Z{\sqrt{\frac{V_d}d}}$$ and assuming $$V_d$$ is given, we can compute the conditional CDF of $$T_d$$.

$$F_{T_d\lvert V_d}(t\lvert v)=\mathbb P(T_d\le t\lvert V_d)=\mathbb P\left(\left.\frac Z{\sqrt{\frac v d}}\le t\right\vert V_d\right)=\mathbb P\left(Z\lt\left.t\sqrt{\frac v d}\right\vert V_d\right)=F_{Z\lvert V_d}\left(t\sqrt{\frac v d}\right)$$

On the other hand, if $$Z\ind V_d$$, we have that $$F_{Z\lvert V_d}\left(t\sqrt{\frac v d}\right)=F_Z\left(t\sqrt{\frac v d}\right)$$. Now, differentiate the CDF and derive the associated conditioned PDF.

$$f_{T_d\lvert V_d}(t\lvert v)=\frac\partial{\partial t}F_{T_d\lvert V_d}(t\lvert v)=\frac\partial{\partial t}F_Z\left(t\sqrt{\frac v d}\right)=f_Z\left(t\sqrt{\frac v d}\right)\sqrt{\frac v d}$$

Finally, integrate over the sample space of $$V_d$$ and compute the PDF of $$T_d$$.

$$\begin{align}
f_{T_d}(t)
&=\int_0^\infty f_{T_d,V_d}(t,v)dv=\int_0^\infty f_{V_d}(v)f_{T_d\lvert V_d}(t\lvert v)dv=\int_0^\infty{\color{red}f_{V_d}(v)}f_Z\left(t\sqrt{\frac v d}\right)\sqrt{\frac v d}dv\\
&=\int_0^\infty{\color{red}\frac{\left(\frac 1 2\right)^{\frac d 2}}{\Gamma\left(\frac d 2\right)}v^{\frac d 2-1}e^{-\frac 1 2 v}}\frac 1{\sqrt{2\pi}}e^{-\frac 1 2 t^2\frac v d}\sqrt{\frac v d}dv=\frac{2^{-\frac d 2}}{\sqrt d\sqrt{2\pi}\Gamma(\frac d 2)}\int_0^\infty v^{\frac{d-1}2}e^{-\frac 1 2\left(1+\frac {t^2}d\right)v}dv
\end{align}$$

Replace $$s=\frac 1 2\left(1+\frac{t^2}d\right)v$$, and recall that $$\Gamma(\alpha)=\int_0^\infty s^{\alpha-1}e^{-s}ds$$, and that $$\Gamma\left(\frac 1 2\right)=\sqrt\pi$$. Accordingly, the above integral can be simplified as follows.

$$\begin{align}
f_{T_d}(t)
&=\frac{2^{-\frac d 2}}{\sqrt d\sqrt{2\pi}\Gamma(\frac d 2)}\int_0^\infty\left(2\left(1+\frac{t^2}d\right)^{-1}s\right)^{\frac{d-1}2}e^{-s}2\left(1+\frac{t^2}d\right)^{-1}ds\\
&=\frac 1{\sqrt d\sqrt\pi\Gamma\left(\frac d 2\right)}\left(1+\frac{t^2}d\right)^{-\frac{d+1}2}\int_0^\infty s^{\frac{d+1}2-1}e^{-s}ds\\
&=\frac 1{\sqrt d}\frac{\Gamma\left(\frac{d+1}2\right)}{\Gamma\left(\frac 1 2\right)\Gamma\left(\frac d 2\right)}\left(1+\frac{t^2}d\right)^{-\frac{d+1}2}=\frac 1{\sqrt d}\frac 1{B\left(\frac d 2,\frac 1 2\right)}\left(1+\frac{t^2}d\right)^{-\frac{d+1}2}
\end{align}$$

The last equality exploits the definition of the [Beta](/2023/03/13/bayesian-statistics.html#beta) function, $$\text{B}(\alpha,\beta)=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$$. Finally, if $$d=1$$, then the PDF becomes $$\frac 1\pi\frac{1}{1+t^2}$$, which is a [Cauchy distribution](/2022/04/26/methods-of-estimation.html#me), with location $$\mu=0$$ and scale $$\gamma=1$$.

### Simulation studies {#sstudies}

When the choice between different test formulations is discretionary, such as $$I(\hat\Theta_n)$$ and $$I(\theta_0)$$ in the Wald's test, an educated decision can be taken by simulating type I and II errors that can be obtained with both tests, and selecting the one that fits best the purpose.

Assume we observe $$X_1,\dots,X_n\overset{\text{i.i.d.}}{\sim}\mathcal P_{\theta_0}$$, derive its [MLE](/2022/04/26/methods-of-estimation.html#mle) $$\hat\Theta_n$$, and employ it in different test statistics $$T_n^1=nI({\color {blue}\theta_0}){(\hat\Theta_n-\theta_0)^2}$$ and $$T_n^2=nI({\color{red}\hat\Theta_n}){(\hat\Theta_n-\theta_0)^2}$$, each of which leading to a different test $$\psi^l=\mathbb 1(T_n^l\gt c_\alpha)$$. Now, if we perform $$k$$ experiments, we expect that $$\frac1k\sum_{j=1}^k\psi_j^l\xrightarrow{\mathbb P}\alpha$$, because that is the error where a sample drawn under the null results in a rejection. However, one of the tests may perform better (i.e. yield smaller errors) than the other, determining the better candidate for a real test on the actual data. Simulating type II error is exactly the same, except that we will draw the samples from an alternative distribution.

Below toy example is based on the [Hardy–Weinberg equilibrium model](https://en.wikipedia.org/wiki/Hardy–Weinberg_principle) with the following PMF.

$$f_X(x)=\begin{cases}
(1-\theta)^2&x=-1\\
2\theta(1-\theta)&x=0\\
\theta^2&x=1
\end{cases}$$

The associated likelihood is $$\mathcal L_1(X,\theta)=(1-\theta)^{2\mathbb 1(x=-1)}(2\theta(1-\theta))^{\mathbb 1(x=0)}\theta^{2\mathbb 1(x=1)}$$, based on which we can derive MLE $$\hat\Theta_n=\frac{\bar X_n+1}2$$, and the corresponding Fisher information $$I(\theta)=\frac2{\theta(1-\theta)}$$. Under the null, $$nI(\hat\Theta_n)(\hat\Theta_n-\theta_0)^2\xrightarrow{(d)}nI(\theta_0)(\hat\Theta_n-\theta_0)^2\xrightarrow{(d)}\chi_1^2$$. Assuming $$q_\alpha$$ is the $$1-\alpha$$ quantile of a $$\chi_1^2$$ distribution, follow the two possible tests to assess whether $$H_0:\theta=\theta_0$$ can be rejected or not.

$$\begin{align}
\psi_\alpha^1=\left(T_n^1\gt q_\alpha\right)&&\psi_\alpha^2=\left(T_n^2\gt q_\alpha\right)
\end{align}$$

To chose the best candidate to run on actual data, one could simulate the possible type I and type II errors and select the one that fits best its purpose.

<iframe width='100%' height='450' src='https://rdrr.io/snippets/embed/?code=n%3C-100%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20size%20of%20the%20samples%0Ak%3C-1e4%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20simulations%0At0%3C-.2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20H0%20hypothesis%0At1%3C-.1%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20H1%20hypothesis%0Aa%3C-.05%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20design%20type%20I%20error%0Aqa%3C-qchisq(1-a%2C1)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20design%20critical%20value%0Ap0%3C-c((1-t0)%5E2%2C2*t0*(1-t0)%2Ct0%5E2)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20H0%20PMFs%0Ap1%3C-c((1-t1)%5E2%2C2*t1*(1-t1)%2Ct1%5E2)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20H1%20PMFs%0AX%3C-matrix(sample(-1%3A1%2Cn*k%2Cprob%3Dp0%2Creplace%3DTRUE)%2Cnrow%3Dk)%20%23%20draw%20Xs%20under%20H0%0AY%3C-matrix(sample(-1%3A1%2Cn*k%2Cprob%3Dp1%2Creplace%3DTRUE)%2Cnrow%3Dk)%20%23%20draw%20Ys%20under%20H1%0Athata%3C-(apply(X%2C1%2Cmean)%2B1)%2F2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20MLE%20for%20Xs%0Athatb%3C-(apply(Y%2C1%2Cmean)%2B1)%2F2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20MLE%20for%20Ys%0A%0ATn1a%3C-n*2%2F(t0*(1-t0))*(thata-t0)%5E2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20various%20Walds%0Apsi1a%3C-Tn1a%3Eqa%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20test%20statistics%20and%0ATn1b%3C-n*2%2F(t0*(1-t0))*(thatb-t0)%5E2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20perform%20associated%0Apsi1b%3C-Tn1b%3Cqa%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20tests%0ATn2a%3C-n*2%2F(thata*(1-thata))*(thata-t0)%5E2%0Apsi2a%3C-Tn2a%3Eqa%0ATn2b%3C-n*2%2F(thatb*(1-thatb))*(thatb-t0)%5E2%0Apsi2b%3C-Tn2b%3Cqa%0A%0Asprintf(%0A%20%20%22simulated%20type%20I%2Ftype%20II%20errors%20for%20test%201%3A%20%25f%2F%25f%22%2C%0A%20%20mean(psi1a)%2Cmean(psi1b))%0Asprintf(%0A%20%20%22simulated%20type%20I%2Ftype%20II%20errors%20for%20test%202%3A%20%25f%2F%25f%22%2C%0A%20%20mean(psi2a)%2Cmean(psi2b))' frameborder='0'></iframe>

### Pearson's theorem {#pearson}

Consider $$\mathbf X_i\overset{\text{i.i.d.}}{\sim}\text{Cat}(\mathbf p)$$ and recall that its [MLE](/2022/04/26/methods-of-estimation.html#mle_categorical) is $$\hat{\mathbf p}=\bar{\mathbf X}_n$$ has the following distribution (see [MM](/2022/04/26/methods-of-estimation.html#mm)).

$$\begin{align}
\sqrt n(\hat{\mathbf p}-\mathbf p)\xrightarrow{(d)}\mathcal N_d(\mathbf 0_d,\Sigma_\mathbf X)&&\Sigma_\mathbf X=\begin{bmatrix}p_1(1-p_1)&\dots&-p_1p_d\\\vdots&\ddots&\\-p_1p_d&&p_d(1-p_d)\end{bmatrix}
\end{align}$$

Observe that $$\Sigma_\mathbf X\mathbf 1_d=\mathbf 0_d$$, which means that $$\Sigma_\mathbf X$$ has an eigenvalue $$0$$ associated with eigenvector $$\mathbf 1_d$$. Therefore, $$\Sigma_\mathbf X$$ is not invertible and Fisher information cannot be determined as $$I(\mathbf p)=\Sigma_\mathbf X^{-1}$$.

Taking $$\mathbf v_1=\begin{bmatrix}\sqrt{p_1}&\dots&\sqrt{p_d}\end{bmatrix}^T$$ and $$I(\mathbf p)^{\frac12}=\text{diag}^{-1}(\mathbf v_1)$$, then $$I(\mathbf p)^{\frac12}\Sigma_\mathbf X I(\mathbf p)^{\frac12}=\mathbf I_d-\mathbf v_1\mathbf v_1^T$$ which means that $$I(\mathbf p)^{\frac12}\sqrt n(\hat{\mathbf p}-\mathbf p)\xrightarrow{(d)}\mathcal N_d(\mathbf 0_d,\mathbf W\mathbf W^T)$$, where $$\mathbf v_1$$ and $$\mathbf W$$ form an [orthogonal basis](/2022/01/24/further-topics-on-RV.html#orthogonal_matrix) $$\mathbf V=\begin{bmatrix}\mathbf v_1&\mathbf W\end{bmatrix}^T$$, s.t. $$\mathbf V\mathbf V^T=\mathbf I_d$$ and therefore $$\mathbf W\mathbf W^T=\mathbf I_d-\mathbf v_1\mathbf v_1^T$$.

$$\begin{align}
\mathbf W\mathbf W^T=\begin{bmatrix}1-p_1&\dots&-\sqrt{p_1 p_d}\\\vdots&\ddots&\\-\sqrt{p_1 p_d}&&1-p_d\end{bmatrix}=\begin{bmatrix}1&\dots&0\\\vdots&\ddots&\\0&&1\end{bmatrix}-\begin{bmatrix}\sqrt{p_1}\sqrt{p_1}&\dots&\sqrt{p_1}\sqrt{p_d}\\\vdots&\ddots&\\\sqrt{p_1}\sqrt{p_d}&&\sqrt{p_d}\sqrt{p_d}\end{bmatrix}
\end{align}$$

Therefore, $$I(\mathbf p)^{\frac12}\sqrt n(\hat{\mathbf p}-\mathbf p)$$ is equivalent to $$\mathbf W\mathbf Z\sim\mathcal N_d(\mathbf 0_d,\mathbf W\mathbf W^T)$$, with $$\mathbf Z\sim\mathcal N_{d-1}(\mathbf 0_{d-1},\mathbf I_{d-1})$$ and accordingly $$\lVert I(\mathbf p)^{\frac12}\sqrt n(\hat{\mathbf p}-\mathbf p)\rVert_2^2=\lVert\mathbf W\mathbf Z\rVert=(\mathbf W\mathbf Z)^T\mathbf W\mathbf Z=\mathbf Z^T\mathbf I_{d-1}\mathbf Z\sim\chi_{d-1}^2$$. In other words, we have the following statement, known as the **Pearson's theorem**.

$$\sum_{j=1}^d n\frac{(\hat p_j-p_j)^2}{p_j}=n(\hat{\mathbf p}-\mathbf p)^TI(\mathbf p)(\hat{\mathbf p}-\mathbf p)=\lVert I(\mathbf p)^{\frac12}\sqrt n(\hat{\mathbf p}-\mathbf p)\rVert_2^2\xrightarrow{(d)}\chi_{d-1}^2$$

### Pearson's theorem vs Wald test {#pearson_wald}

[Pearson's theorem](2022-07-15-hypothesis-testing.markdown#pearson) result can be achieved by attempting Wald's test. Since $$\Sigma_\mathbf X$$ is not invertible, we re-parametrize the problem by setting $$\mathbf b=\begin{bmatrix}p_1&\dots&p_{d-1}\end{bmatrix}^T$$ and $$p_d=1-\mathbf 1_{d-1}^T\mathbf b$$ and develop $$s(\mathbf b)$$ and $$I(\mathbf b)$$ from $$\ell_1(\mathbf b)=\sum_{j=1}^d X_j\ln(p_j)=\sum_{j=1}^{d-1}X_j\ln(p_j)+X_d\ln(1-\sum_{j=1}^{d-1}p_j)$$.

|Distribution and unknown parameter|$$s(\mathbf b)=\nabla_b\ell(\mathbf X,\mathbf b)$$|$$I(\mathbf b)=\mathbb E[-\mathbf H_b\ell(\mathbf b)]$$|
|-|:-:|:-:|
|Categorical with parameter $$\mathbf b$$|$$\begin{bmatrix}\frac{X_1}{p_1}\\\vdots\\\frac{X_{d-1}}{p_{d-1}}\end{bmatrix}-\frac{X_d}{p_d}\mathbf 1_{d-1}$$|$$\text{diag}^{-1}(\mathbf b)+\frac1{p_d}\mathbf 1_d\mathbf 1_d^T$$|

If $$d=3$$, using the above approach we obtain that $$I^{-1}(\mathbf b)=\Sigma(\mathbf b)$$, where $$\mathbf b=(p_1,p_2)$$.

$$I^{-1}(\mathbf b)=\left(\frac 1 {1-p_1-p_2}\begin{bmatrix}\frac{1-p_2}{p_1}&1\\1&\frac{1-p_1}{p_2}\end{bmatrix}\right)^{-1}=\begin{bmatrix}p_1(1-p_1)&-p_1p_2\\-p_1p_2&p_2(1-p_2)\end{bmatrix}=\Sigma(\mathbf b)$$

In the reduced space, all necessary technical conditions of [MLE](/2022/04/26/methods-of-estimation.html#mle_properties) are satisfied, we can make the following claim.

$$\sqrt n(\hat{\mathbf b}-\mathbf b)\xrightarrow{(d)}\mathcal N_{d-1}(\mathbf 0_{d-1},I^{-1}(\mathbf b))$$

At this point, square both sides, and derive as follows.

$$\begin{align}
I^{\frac12}(\mathbf b)\sqrt n(\hat{\mathbf b}-\mathbf b)&\xrightarrow{(d)}\mathcal N_{d-1}(\mathbf 0_{d-1},\mathbf I_{d-1})\\
n(\hat{\mathbf b}-\mathbf b)^T I(\mathbf b)(\hat{\mathbf b}-\mathbf b)&\xrightarrow{(d)}\chi_{d-1}^2\\
n(\hat{\mathbf b}-\mathbf b)^T\left(\text{diag}^{-1}(\mathbf b)+\frac1{p_d}\mathbf 1_d\mathbf 1_d^T\right)(\hat{\mathbf b}-\mathbf b)&\xrightarrow{(d)}\chi_{d-1}^2\\
n(\hat{\mathbf b}-\mathbf b)^T\text{diag}^{-1}(\mathbf b)(\hat{\mathbf b}-\mathbf b)+\frac n{p_d}(\hat{\mathbf b}-\mathbf b)^T\mathbf 1_d\mathbf 1_d^T(\hat{\mathbf b}-\mathbf b)&\xrightarrow{(d)}\chi_{d-1}^2\\
\sum_{j=1}^{d-1}n\frac{(\hat p_j-p_j)^2}{p_j}+\frac n{p_d}\left(\sum_{j=1}^{d-1}\hat p_j-\sum_{j=1}^{d-1} p_j\right)^2&\xrightarrow{(d)}\chi_{d-1}^2\\
\sum_{j=1}^{d-1}n\frac{(\hat p_j-p_j)^2}{p_j}+n\frac{(\hat p_d-p_d)^2}{p_d}=\sum_{j=1}^d n\frac{(\hat p_j-p_j)^2}{p_j}&\xrightarrow{(d)}\chi_{d-1}^2
\end{align}$$

### Symmetrization methods {#symmetrization}

Objective of the symmetrization methods is to provide a bound to a given probability, by comparing it to a probability of somehow related random variable. They are useful to increase the concentration of measure of random variable, when simpler methods cannot apply.

For example, the [Hoeffding's inequality](/2022/02/21/introduction-to-statistics.html#exp) results in the following bound for sample mean (if $$X_i\in[a,b]$$).

$$\mathbb P(\lvert\bar X_n-\mu_X\rvert\ge\varepsilon)\le2e^{-\frac{2n\varepsilon^2}{(b-a)^2}}$$

However, the above cannot apply to $$\mathbb P(\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\ge\varepsilon)$$, with $$F_n(x)$$ being an [ECDF](/2022/07/15/hypothesis-testing.html#ecdf), because the distribution of $$\sup_{t\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert$$ is not known in closed form, as it depends on the function $$F_X(x)$$, and the underlying distribution generating the data. In this case, symmetrization can be applied to bound the distribution in terms of simpler quantities, by employing an additional *virtual* sample that combined with the original results in a new random variable symmetric around $$0$$.

Before proceeding further, assume $$A,B\overset{\text{i.i.d.}}{\sim}\mathcal P$$ and [recall](/2022/01/05/conditioning-and-independence.html#sum) the following relations ($$A$$ and $$B$$ are interchangeable).

$$\begin{cases}
\mathbb P(A+B\ge\varepsilon)\left(1-\mathbb P\left(A\ge\frac12\varepsilon\right)\right)\le\mathbb P(B\ge\frac12\varepsilon)\\
\mathbb P(A+B\ge\varepsilon)\le2\mathbb P\left(A\ge\frac12\varepsilon\right)
\end{cases}$$

Above applies $$\forall(x,y,z)\in\mathbb R^3$$, s.t. $$A$$, $$B$$ and $$A+B$$ can be of the form $$\lvert x-y\rvert$$, $$\lvert y-z\rvert$$ or $$\lvert x-z\rvert$$. Formulations can be used *in chain* to create more sophisticated bounds, as further described below.

#### Symmetrization by ghost sample

In the first case, we want to bound the probability of $$\sup_{x\in\mathbb X}\lvert F_n(x)-F_X(x)\rvert\ge\varepsilon$$, in terms of a symmetric r.v. $$F_n(t)-F_n'(t)$$, where $$F_n'(t)$$ is a **ghost sample**, i.i.d. with $$F_n(t)$$. By defining $$A=\sup_{x\in\mathbb R}\lvert F_n(t)-F_X(t)\rvert$$ and $$B=\sup_{x\in\mathbb R}\lvert F_n'(t)-F_X(t)\rvert$$, then $$A\ind B$$. Also, assuming $$C=\sup_{x\in\mathbb R}\lvert F_n(t)-F_n'(t)\rvert$$, in the first equation above, and applying [Chebyshev's inequality](/2022/02/21/introduction-to-statistics.html#basic), we obtain the following bound.

$$\begin{align}
\mathbb P(A\ge\varepsilon)\left(1-\underbrace{\mathbb P\left(B\ge\frac12\varepsilon\right)}_{\le\frac4{n\varepsilon^2}\text{var}(\mathbb 1(X_i\le x))}\right)\le\mathbb P\left(C\ge\frac12\varepsilon\right)
\end{align}$$

Assuming $$n\varepsilon^2\ge2$$, and noting that $$\text{var}(\mathbb 1(X_i\le x)\text{Ber}(p))\le\frac14$$, the above becomes as follows.

$$\mathbb P(A\ge\varepsilon)\le2\mathbb P\left(C\ge\frac12\varepsilon\right)$$

#### Symmetrization by sign

Observe that $$F_n(x)-F_n'(x)=\frac1n\sum_{i=1}^n(\mathbb 1(X_i\le x)-\mathbb 1(X_i'\le x))$$ is symmetric around $$0$$ (because $$F_n(x)$$ and $$F_n'(x)$$ are i.i.d.), and has the same distribution as $$\frac1n\sum_{i=1}^n\rho_i[\mathbb 1(X_i\le x)-\mathbb 1(X_i'\le x)]$$, where $$\rho_i\overset{\text{i.i.d.}}{\sim}\text{Rad}$$. If we define $$D=\sup_{x\in\mathbb R}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\le x)-\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i'\le x)\right\rvert$$, as well as $$E=\sup_{x\in\mathbb R}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\le x)\right\rvert$$ and $$F=\sup_{x\in\mathbb R}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i'\le x)\right\rvert$$, it seems logical that $$D\le E+F$$, and that the associated probabilities can be bounded as follows.

$$\mathbb P(D\ge\epsilon)\le\mathbb P(E+F\ge\epsilon)\le2\mathbb P\left(E\ge\frac12\epsilon\right)=2\mathbb P\left(F\ge\frac12\epsilon\right)$$

Combining both symmetrization methods leads to the following conclusion.

$$\begin{align}
\mathbb P(A\ge\varepsilon)
&\le2\mathbb P\left(C\ge\frac12\varepsilon\right)\\
&=2\mathbb P\left(D\ge\frac12\varepsilon\right)\\
&\le4\mathbb P\left(E\ge\frac14\varepsilon\right)\\
\mathbb P(\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\ge\varepsilon)&\le4\mathbb P\left(\sup_{x\in\mathbb R}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\le x)\right\rvert\ge\frac14\varepsilon\right)
\end{align}$$

### Glivenko-Cantelli theorem {#gc}

Let us consider the continuous case and split the real line into $$k$$ partitions, that is $$A_j=[x_{j-1},x_j^-]$$ with $$j=1,\dots,k$$, s.t. $$\mathbb P(A_j)=\frac1k$$ for $$j=1,\dots,k$$. In particular, the points $$x_j$$ are placed in a way s.t. $$F_X(x_j)=\mathbb P(X\le x_j)=\frac j k$$ and $$x_j^-$$ are the points where $$F_X(x_j^-)=\mathbb P(X\lt x_j)$$.

Note that where $$F_n(\cdot)$$ is **random**, $$F_X(\cdot)$$ is not. Accordingly, $$F_X(x_j^-)-F_X(x_{j-1})\le\frac1k$$ does not depend on samples and is always true. Furthermore, with bit of algebra $$F_n(x_{j-1})\le F_n(x_j^-)$$ can also be proved correct. For any $$x\in\mathbb R$$, we can find $$j$$ s.t. $$x_{j-1}\le x\le x_j^-$$ and the following holds.

$$\begin{gather}
F_n(x_{j-1})\le F_n(x)\le F_n(x_j^-)\\
F_X(x_{j-1})\le F_X(x)\le F_X(x_j^-)\\
\hline\\
F_n(x_{j-1})-F_X(x_j^-)\le F_n(x)-F_X(x)\le F_n(x_j^-)-F_X(x_{j-1})
\end{gather}$$

At this point, we can add and remove some terms, to simplify the inequality.

$$\begin{align}
F_n(x_{j-1}){\color{red}+F_X(x_{j-1})-F_X(x_{j-1})}-F_X(x_j^-)&\le\dots\\
\dots\le F_n(x)-F_X(x)&\le F_n(x_j^-){\color{blue}+F_X(x_j^-)-F_X(x_j^-)}-F_X(x_{j-1})\\
F_n(x_{j-1})-F_X(x_{j-1})-\frac1k\le F_n(x)-F_X(x)&\le F_n(x_j^-)-F_X(x_j^-)+\frac1k
\end{align}$$

Considering that $$a\le b\le c\implies\lvert b\rvert\le\max\{-a,c\}$$, the earlier inequality can be further simplified.

$$\begin{align}
\lvert F_n(x)-F_X(x)\rvert
&\le\max\left\{-\left(F_n(x_{j-1})-F_X(x_{j-1})-\frac1k\right),F_n(x_j^-)-F_X(x_j^-)+\frac1k\right\}\\
&\le\max\left\{\lvert F_X(x_{j-1})-F_n(x_{j-1})\rvert,\lvert F_n(x_j^-)-F_X(x_j^-)\rvert\right\}+\frac1k=\Delta_j+\frac1k
\end{align}$$

In the above $$\Delta_j=\max\{\lvert F_n(x_{j-1})-F_X(x_{j-1})\rvert,\lvert F_n(x_j^-)-F_X(x_j^-)\rvert\}\xrightarrow{a.s.}0$$ due to the fact that $$\lvert F_n(x_{j-1})-F_X(x_{j-1})\rvert\xrightarrow{a.s.}0$$ and $$\lvert F_n(x_j^-)-F_X(x_j^-)\rvert\xrightarrow{a.s.}0$$ as $$F_n(x)\xrightarrow{a.s.}F_X(x)$$ for any $$x\in\mathbb R$$ thanks to [SLLN](/2022/02/21/introduction-to-statistics.html#wlln). Note that $$\lvert F_n(x)-F_X(x)\rvert\le\Delta_j+\frac1k$$ is valid as far as $$x\in A_j$$. To extend this result to the entire real line, we need to consider $$\Delta=\max_{j=1,\dots,k}\Delta_j$$, which also $$\xrightarrow{a.s.}0$$.

$$\begin{align}
\lvert F_n(x)-F_X(x)\rvert\le\Delta+\frac1k&\xrightarrow{a.s.}\frac1k,\forall t\in\mathbb R=\bigcup_{j=1}^k A_j\\
\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert&\xrightarrow{a.s.}\frac1k
\end{align}$$

Hence, $$\forall\varepsilon>0$$ exists $$N$$ s.t. for any $$n\ge N$$, $$\lvert F_n(t)-F_X(t)\rvert\le\varepsilon=\frac1k$$, that proves the point.

Alternatively to the above, one could rely on the [symmetrization method](/2022/07/15/hypothesis-testing.html#symmetrization) and obtain as follows.

$$\mathbb P(\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\ge\varepsilon)\le4\mathbb P\left(\sup_{x\in\mathbb R}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\le x)\right\rvert\ge\frac14\varepsilon\right)$$

Given sample $$\mathbf X$$, for any $$x\in\mathbb R$$, vector $$\begin{bmatrix}\mathbb 1(X_i\le x)&\dots&\mathbb 1(X_n\le x)\end{bmatrix}^T$$ will take at most $$(n+1)$$ combinations. By defining $$B_i=(-\infty,X_{(i)}]$$, $$B_{n+1}=(-\infty,+\infty)$$ and $$\mathcal B=\{B_1,\dots,B_{n+1}\}$$, we can replace $$\sup_{x\in\mathbb R}\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\le x)\rvert$$ with $$\max_{j}\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\in B_j)\rvert$$. Also, bearing in mind that $$\mathbb P(\max_{j=1,\dots,k}\{u_j\}\ge a)=\mathbb P(\bigcup_{j=1}^k(u_j\ge a))\le\sum_{j=1}^k\mathbb P(u_j\ge a)$$ the following conclusion can be reached.

$$\begin{align}
\mathbb P(\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\ge\varepsilon)
&\le4\mathbb P\left(\sup_{x\in\mathbb R}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\le x)\right\rvert\ge\frac14\varepsilon\right)\\
&\le4\mathbb P\left(\max_{j=1,\dots,n+1}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\in A_j)\right\rvert\ge\frac14\varepsilon\bigg\vert\mathbf X\right)\\
&=4\mathbb P\left(\bigcup_{j=1}^{n+1}\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\in A_j)\right\rvert\ge\frac14\varepsilon\bigg\vert\mathbf X\right)\\
&\le\sum_{j=1}^{n+1}4\mathbb P\left(\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\in A_j)\right\rvert\ge\frac14\varepsilon\bigg\vert\mathbf X\right)\\
&\le(n+1)\max_{j=1,\dots,n+1}4\mathbb P\left(\left\lvert\frac1n\sum_{i=1}^n\rho_i\mathbb 1(X_i\in A_j)\right\rvert\ge\frac14\varepsilon\bigg\vert\mathbf X\right)
\end{align}$$

Bearing in mind that $$\rho_i\mathbb 1(X_i\in A_j)\in[-1,1]$$, the above is bounded by the [Hoeffding's inequality](/2022/02/21/introduction-to-statistics.html#exp).

$$\mathbb P\left(\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\ge\varepsilon\right)\le(n+1)8e^{-\frac{n\varepsilon^2}{32}}$$

### Brownian bridge {#bbridge}

A [Wiener process](/2022/02/08/bernoulli-and-poisson-processes.html#donsker) (i.e. the mathematical model describing the Brownian motion) $$B(t)$$ defined over $$0\le t\le T$$ and subject to the condition $$B(T)=B(0)=0$$ is known as **Brownian bridge** $$\mathbb B(t)$$.

Considering that $$B(T)=B(t)+B(T-t)$$, and that $$B(T-t)\ind B(t)$$, it follows that $$\text{cov}(B(t),B(T))=t$$, bearing also in mind that $$B(t)=\sqrt tZ$$, where $$Z\sim\mathcal N(0,1)$$.

$$\begin{align}
\text{cov}(B(t),B(T))
&=\mathbb E[B(t)B(T)]-\cancelto{=0}{\mathbb E[B(t)]\mathbb E[B(T)]}\\
&=\mathbb E[B(t)(B(t)+B(T-t))]=\mathbb E[B^2(t)]+\cancelto{=0}{\mathbb E[B(t)B(T-t)]}\\
&=\mathbb E[B^2(t)]=t\mathbb E[Z^2]=t
\end{align}$$

Accordingly, one possible representation of the Brownian bridge is $$\mathbb B(t)=B(t)-\frac tT B(T)$$:

- $$\mathbb B(T)=B(T)-\frac TTB(T)=W(0)=0$$, as required by the definition;
- $$\mathbb B(t)\sim\mathcal N\left(0,t\left(1-\frac tT\right)\right)$$, due to linearity of the Normal distribution, bearing in mind:

$$\begin{align}
\mathbb E[B(t)-\frac tTB(T)]&=0\\
\text{var}\left(B(t)-\frac tT B(T)\right)
&=\text{var}(B(t))+\frac{t^2}{T^2}\text{var}(B(T))-2\frac tT\text{cov}(B(t),B(T))\\
&=t+\frac{t^2}T-2\frac{t^2}T=t-\frac{t^2}T=t\left(1-\frac tT\right)
\end{align}$$

When *standardized* (i.e. $$T=1$$), the Brownian bridge takes a simpler form $$\mathbb B(t)\sim\mathcal N(0,t(1-t))$$, referred to as the [Kolmogorov distribution](https://en.wikipedia.org/wiki/Kolmogorov–Smirnov_test), and which is also the limiting distribution of [ECDF](/2022/07/15/hypothesis-testing.html#ecdf).

$$T_n=\sup_{x\in\mathbb R}\lvert\sqrt n(F_n(x)-F_X(x))\rvert\xrightarrow{(d)}\sup_{t\in[0,1]}\lvert\mathbb B(t)\rvert$$

Critical values for Kolmogorov distribution are available in the original [Kolmogorov-Smirnov table](https://luk.staff.ugm.ac.id/jurnal/freepdf/Smirnov1948-euclid.aoms.1177730256.pdf). On the other hand, considering that Brownian bridges can be simulated, one could use random sampling methods to extract an approximation of the underlying distribution. Consider the code below, and bear in mind that it will start converging for $$n$$ sufficiently large ($$n\gt40$$) and that any increase in the number of experiments $$k$$ will improve the granularity of the distribution. Finally, bear in mind that for $$n\rightarrow\infty$$ and $$\alpha=0.05$$, $$c_\alpha\approx 1.36$$ (which however is difficult to reach with limited memory capacity).

<iframe width='100%' height='950' src='https://rdrr.io/snippets/embed/?code=n%3C-1e2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20steps%20per%20experiment%0Ak%3C-1e3%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20experiments%0Aa%3C-0.05%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20test%20level%0At%3C-0%3An%2Fn%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20time%20intervals%0AR%3C-matrix((rbinom(n*k%2C1%2C.5)*2-1)%2Cnrow%3Dk)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20Rademacher%20steps%0ASn%3C-cbind(rep(0%2Ck)%2Ct(apply(R%2C1%2Ccumsum)))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20random%20walks%0AWn%3C-Sn%2Fsqrt(n)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20standardization%0ABB%3C-Wn-matrix(Wn%5B%2Cn%2B1%5D%2Cncol%3D1)%25*%25matrix(t%2Cnrow%3D1)%20%20%20%20%20%20%20%23%20condition%20W(0)%3D0%0AMn%3C-apply(abs(BB)%2C1%2Cmax)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20sup(abs(BB))%0Ahist(Mn%2Cfreq%20%3D%20FALSE%2Cbreaks%3D100)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20sup(abs(BB))%20distribution%0Aca%3C-quantile(Mn%2Cprobs%3D1-a)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20c_alpha%0Asprintf(%22%25.2f%20quantile%20for%20simulated%20sup%7CB(t)%7C%20%3D%20%25f%22%2C%0A%20%20%20%20%20%20%20%201-a%2Cca)' frameborder='0'></iframe>

## KS variations

Prior to wrapping up, one may have noticed that [KS statistic](/2022/07/15/hypothesis-testing.html#ks) quantifies a distance between the [ECDF](/2022/07/15/hypothesis-testing.html#ecdf) $$F_n(x)$$ and the [CDF](/2022/01/13/continuous-random-variables.html#cdf) $$F_X(x)$$. In fact, if $$d(F_n,F_X)=\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert$$ satisfies all three distance axioms, which can be proved similarly as we did for [TV distance](/2022/04/26/methods-of-estimation.html#tv), except that KS statistic relies on the [uniform norm](https://en.wikipedia.org/wiki/Uniform_norm) (also known as maximum norm or infinity norm) between different (E)CDF.

$$\begin{align}
d(F_n,F_X)
&=\lVert F_n(x)-F_X(x)\rVert_\infty\\
&=\sup_{x\in\mathbb R}\lvert F_n(x)-F_X(x)\rvert\\
T_n&=\sqrt n d(F_n,F_X)&\text{(KS statistic)}
\end{align}$$

However, many functions could satisfy the definition of a distance function. [Cramér-von Mises](https://en.wikipedia.org/wiki/Cramér–von_Mises_criterion) (CVM) test is an alternative to KS test that employs the [Euclidean norm](https://en.wikipedia.org/wiki/Euclidean_distance) squared. Note that representing the integral in terms of $$dF_X(x)$$ turns the distance into a *pivotal* function.

$$\begin{align}
d^2(F_n,F_X)
&=\int_{x\in\mathbb R}\lVert F_n(x)-F_X(x)\rVert_2^2 dF_X(x)\\
&=\int_{x\in\mathbb R}(F_n(x)-F_X(x))^2 dF_X(x)\\
&=\mathbb E_{F_X(X)}\left[\left(F_n(x)-F_X(x)\right)^2\right]
\end{align}$$

CVM was further improved by [Anderson-Darling](https://en.wikipedia.org/wiki/Anderson–Darling_test) (AD) test, which introduced on a weighting function $$w(x)$$ to manipulate tails contributions in the distance computation and therefore improve the [power](/2022/03/24/foundation-of-inference.html#testing) of the test.

$$d^2(F_n,F_X)=\int_{x\in\mathbb R}w(x)\left(F_n(x)-F_X(x)\right)^2d F_X(x)$$

In particular, AD recalled that $$\sqrt n\frac{F_n(x)-F_X(x)}{\sqrt{F_X(1-F_X(x))}}\sim\mathcal N(0,1)$$, or $$n\frac{(F_n(x)-F_X(x))^2}{F_X(x)(1-F_X(x))}\sim\chi_1^2$$, and therefore a distance function of the form $$w(x)(F_n(x)-F_X(x))^2$$, with $$w(x)=[F_x(1-F_X(x))^{-1}]$$, was assumed and which captured tail probability distances with much more evidence.

$$d^2(F_n,F_X)=\int_{x\in\mathbb R}\frac{\left(F_n(x)-F_X(x)\right)^2}{F_X(x)(1-F_X(x))}d F_X(x)$$

CVM and AD test statistic is $$T_n=d^2(F_n,F_X)$$, where $$w(x)=1$$ reduces the AD statistic to CVM. Critical values can be again derived thorough simulations.

# Two sample KS test

KS test can be promptly adjusted to test if two samples have been drawn from the same distribution $$F(x)$$.

Assume collecting two samples of size $$n$$ and $$m$$ with $$F_n(x)$$ and $$G_m(x)$$ as respective [ECDF](/2022/07/15/hypothesis-testing.html#ecdf). [GC](/2022/07/15/hypothesis-testing.html#gc) tells us that that both $$F_n(x)$$ and $$G_m(x)$$ with converge uniformly to the same *unknown* CDF $$F(x)$$. Thus, we expect that $$\sup_{x\in\mathbb R}\lvert F_n(x)-G_m(x)\rvert\xrightarrow{a.s.}0$$. Also, as $$F_n(x)\sim\frac1{\sqrt n}\mathcal N(F(x),F(x)(1-F(x)))$$ and $$G_m(x)\sim\frac1{\sqrt m}\mathcal N(F(x),F(x)(1-F(x)))$$, we can reach the following conclusion.

$$\begin{align}
\sqrt{\frac{nm}{n+m}}(F_n(x)-G_m(x))&\xrightarrow{(d)}\mathcal N(0,F_X(x)(1-F_X(x)))\\
T_{n,m}=\sqrt{\frac{nm}{n+m}}\sup_{x\in\mathbb R}\lvert F_n(x)-G_m(x)\rvert&\xrightarrow{(d)}\sup_{t\in[0,1]}\lvert\mathbb B(t)\rvert
\end{align}$$

To find the critical values of $$T_{n,m}$$ statistic one can again rely on the simulations. The simulation below estiamtes $$c_\alpha$$ for $$\alpha=0.05$$, $$n=5$$ and $$m=8$$. As mentioned above, the tables usually report the number without the scaling factor $$\sqrt{\frac{nm}{n+m}}$$.

<iframe width='100%' height='950' src='https://rdrr.io/snippets/embed/?code=n%3C-8%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20size%20of%20the%20sample%20X%0Am%3C-5%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20size%20of%20the%20sample%20Y%0Ak%3C-1e4%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20simulations%0AX%3C-matrix(runif(n*k)%2Cnrow%3Dk)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20X~U(0%2C1)%0AY%3C-matrix(runif(m*k)%2Cnrow%3Dk)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20Y~U(0%2C1)%0AgetSup%3C-function(A%2CB)%20%7B%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20gets%20supremum%20of%0A%20%20j%3C-t(apply(A%2C1%2Crank))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20sup%7CF_A(t)-F_B(t)%7C%0A%20%20U%3C-t(%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20for%20t%3DA_i%0A%20%20%20%20sapply(1%3Anrow(A)%2Cfunction(s)%0A%20%20%20%20%20%20sapply(1%3Ancol(A)%2Cfunction(t)%20sum(B%5Bs%2C%5D%3C%3DA%5Bs%2Ct%5D))%0A%20%20%20%20)%0A%20%20)%2Fncol(B)%0A%20%20return(sqrt(n*m%2F(n%2Bm))*%0A%20%20%20%20apply(pmax(abs((j-1)%2Fn-U)%2Cabs(j%2Fn-U))%2C1%2Cmax))%0A%7D%0AD%3C-getSup(X%2CY)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20differences%20at%20X_i%0AD%3C-pmax(D%2CgetSup(Y%2CX))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20differences%20at%20Y_j%0Ahist(D%2Cfreq%3DFALSE)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20D%20statistic%20histogram%0Ac_alpha%3C-quantile(D%2Cprobs%3D.95)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20compute%20c_alpha%0Asprintf(%220.95%20quantile%20for%20simulated%20KS%20%3D%20%25f%22%2C%20%20%20%20%20%20%20%20%20%20%20%23%20c_alpha%20with%20scaling%0A%20%20%20%20%20%20%20%20c_alpha)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20converting%20to%20BB(t)%0Anum%3C-c_alpha*sqrt(n*m*(n%2Bm))%0Aden%3C-n*m%0Asprintf(%22same%20quantile%20without%20scaling%20%3D%20%25.2f%2F%25.2f%22%2C%20%20%20%20%20%23%20compute%20without%20scaling%0A%20%20%20%20%20%20%20%20num%2Cden)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20as%20reported%20in%20KS%20tables' frameborder='0'></iframe>
