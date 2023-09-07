---
layout: post
title: "Linear Regression"
---

$$\newcommand{\ind}{\perp\kern-5pt\perp}$$

## Linear model with Normal noise {#lm}

By expanding on the Bayesian statistics, there is a large field in estimation that treats exclusively linear models with [Normal](/2022/01/13/continuous-random-variables.html#normal) noise. Assume that $$\theta$$ is an unknown value to which we have no direct access. We have some prior belief that $$\Theta\sim\mathcal N(x_0,\sigma_0^2)$$ and that observations are obtained as $$X_i=\Theta+W_i$$, where $$W_i\ind\Theta$$ is noise with $$W_i\overset{\text{i.i.d.}}{\sim}\mathcal N(0,\sigma_i^2)$$ for $$i=1,\dots,n$$. Thus, even though $$X_i$$ and $$X_j$$ are dependent, in general they are i.i.d. in the conditional space, $$X_i\lvert\Theta\overset{\text{i.i.d.}}{\sim}\mathcal N(\Theta,\sigma_i^2)$${% if jekyll.environment == "development" %} (see [Prob L15 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab7)){% endif %}.

<p align="center">
  <img src="/assets/images/2023-06-30-linear-regression/23530.png"/>
</p>

Since $$X_i$$ is a [sum of independent Normal r.v.](/2022/01/24/further-topics-on-RV.html#proof_sum_normal), it follows that upon the first observation $$X_1$$, we can derive that $$\Theta\lvert X_1\sim\mathcal N(\mu_{\Theta\lvert X_1},\sigma_{\Theta\lvert X_1}^2)$$, where $$\sigma_{\Theta\lvert X_1}^2$$ is the harmonic mean of $$\sigma_0^2$$ and $$\sigma_1^2$$, and $$\mu_{\Theta\lvert X_1}$$ is a weighted average of $$x_0$$ and $$x_1$$.

$$\begin{cases}
\displaystyle\sigma_{\Theta\lvert X_1}^2=\frac1{\frac1{\sigma_0^2}+\frac1{\sigma_1^2}}\\
\displaystyle\mu_{\Theta\lvert X_1}=\frac1{\frac1{\sigma_0^2}+\frac1{\sigma_1^2}}\left(\frac1{\sigma_0^2}x_0+\frac1{\sigma_1^2}X_1\right)=\sigma_{\Theta\lvert X_1}^2\left(\frac1{\sigma_0^2}x_0+\frac1{\sigma_1^2}X_1\right)
\end{cases}$$

Notice that with additional observation $$X_2$$, the parameters of $$\Theta\lvert X_1,X_2\sim\mathcal N(\mu_{\Theta\lvert X_1,X_2},\sigma_{\Theta\lvert X_1,X_2}^2)$$ can be obtained in the same way as above, as if $$\Theta\lvert X_1$$ was our new prior.

$$\begin{cases}
\displaystyle\sigma_{\Theta\lvert X_1,X_2}^2=\frac1{\frac1{\sigma_{\Theta\lvert X_1}^2}+\frac1{\sigma_2^2}}=\frac1{\frac1{\sigma_0^2}+\frac1{\sigma_1^2}+\frac1{\sigma_2^2}}\\
\displaystyle\mu_{\Theta\lvert X_1,X_2}=\sigma_{\Theta\lvert X_1,X_2}^2\left(\frac1{\sigma_{\Theta\lvert X_1}^2}\mu_{\Theta\lvert X_1}+\frac1{\sigma_2^2}X_2\right)=\sigma_{\Theta\lvert X_1,X_2}^2\left(\frac1{\sigma_0^2}x_0+\frac1{\sigma_1^2}X_1+\frac1{\sigma_2^2}X_2\right)
\end{cases}$$

At this point, the common structure becomes evident and one can generalize that after $$n$$ observations, the posterior will be distributed as follows.

$$\Theta\lvert\mathbf X_n\sim\mathcal N(\mu_{\Theta\lvert\mathbf X_n},\sigma_{\Theta\lvert\mathbf X_n}^2)=\mathcal N\left(\frac{\frac1{\sigma_0^2}x_0+\sum_{i=1}^n\frac1{\sigma_i^2}X_i}{\sum_{i=0}^n\frac1{\sigma_i^2}},\frac1{\sum_{i=0}^n\frac1{\sigma_i^2}}\right)$$

Key conclusions from the above are:

- LMS estimator is $$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]=\mu_{\Theta\lvert\mathbf X_n}$$ and is the average of observations $$x_i$$ ($$x_0$$ being treated as an observation), with weights determined by the respective variances $$\sigma_i^2$$;
- As $$\Theta\lvert\mathbf X_n$$ is Normal, [LMS](/2023/03/13/bayesian-statistics.html#lms) (or Bayesian) estimator and [MAP](/2023/03/13/bayesian-statistics.html#map) estimator coincide; and
- $$\text{MSE}(\hat\Theta_n)=\mathbb E[\text{var}(\Theta\lvert\mathbf X_n)]=\sigma_{\Theta\lvert\mathbf X_n}^2$$ is constant and does not depend on observations. If *some* $$\sigma_i^2$$ are small, then MSE is also small. Conversely, if *all* $$\sigma_i$$ are large, then MSE is also large{% if jekyll.environment == "development" %} (see [Prob L15 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab10)){% endif %}.

Last remark is that if $$\sigma_i^2=\sigma$$, then $$\sigma_{\Theta\lvert\mathbf X_n}^2=\frac{\sigma}n\rightarrow0$$, confirming the consistency of the estimator.

### Generalizations of the linear model with Normal noise {#generalizations}

If $$X_i=y_i\Theta+W_i$$, we can simply revise it as $$\tilde X_i=\Theta+\tilde W_i$$, with observations $$\tilde X_i=\frac{X_i}{y_i}$$ and noise $$\tilde W_i\sim\mathcal N\left(0,\frac{\sigma_i^2}{y_i^2}\right)$${% if jekyll.environment == "development" %} (see [Prob L15 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab5), [Prob L15 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab8) and [Prob L15 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab11)){% endif %}.

If $$\boldsymbol{\Theta}=\begin{bmatrix}\Theta_1&\dots&\Theta_d\end{bmatrix}^T\sim\mathcal N_d(\begin{bmatrix}x_{01}&\dots&x_{0d}\end{bmatrix}^T,\text{diag}(\sigma_{01}^2,\dots,\sigma_{0d}^2))$$ and $$X_i=\mathbf y_i^T\boldsymbol{\Theta}+W_i$$, with $$\mathbf y_i=\begin{bmatrix}y_{i1}&\dots&y_{id}\end{bmatrix}^T$$, we have that $$X_i\lvert\boldsymbol{\Theta}\sim\mathcal N(\mathbf y_i^T\boldsymbol{\Theta},\sigma_i^2)$$. In the multivariate case, $$\boldsymbol{\Theta}\lvert\mathbf X_n$$ is still Normally distributed, according to $$\mathcal N_d(\mu_{\boldsymbol{\Theta}\lvert\mathbf X_n},\sigma_{\boldsymbol{\Theta}\lvert\mathbf X_n}^2)$$ and the good thing is that for any given $$j=1,\dots,d$$, the [posterior distribution](/2023/06/30/linear-regression.html#multivariate_lm) of $$\Theta_j\lvert\mathbf X_n,\boldsymbol{\Theta}_{k\neq j}$$ is Normal with the same structure as above, provided that $$\tilde X_{ij}=\frac{X_i-\sum_{k\neq j}y_{ik}\Theta_k}{y_{ij}}$$ and $$\tilde\sigma_{ij}=\frac{\sigma_i}{y_{ij}}$$ for $$i\ge1$$ (note that $$\tilde\sigma_{0j}=\sigma_0$$).

$$\Theta_j\lvert\mathbf X_n,\boldsymbol{\Theta}_{k\neq j}\sim\mathcal N(\mu_{\Theta_j\lvert\mathbf X_n,\boldsymbol{\Theta}_{k\neq j}},\sigma_{\Theta_j\lvert\mathbf X_n,\boldsymbol{\Theta}_{k\neq j}}^2)=\mathcal N\left(\frac{\frac1{\sigma_0^2}x_0+\sum_{i=1}^n\frac1{\tilde\sigma_{ij}^2}\tilde X_{ij}}{\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}},\frac1{\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}}\right)$$

If $$y_{ij}=0$$, then $$\frac1{\tilde\sigma_{ij}^2}=\frac1{\tilde\sigma_{ij}^2}\tilde x_{ij}=0$$, then $$x_i$$ is irrelevant for the estimation $$\Theta_j$${% if jekyll.environment == "development" %} (see [Prob L15 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__15_Linear_models_with_normal_noise/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s3-tab13)){% endif %}. Finally, $$\hat{\boldsymbol{\Theta}}=\begin{bmatrix}\hat\Theta_1&\dots&\hat\Theta_d\end{bmatrix}^T=\begin{bmatrix}\mu_{\Theta_1\lvert\mathbf X_n}&\dots&\mu_{\Theta_d\lvert\mathbf X_n}\end{bmatrix}^T$$, where marginal estimators $$\mu_{\Theta_j\lvert\mathbf X_n}$$ are the solution of a system of $$d$$ linear equations.

## Linear LMS (LLMS) estimation

Recall that the [LMS](/2023/03/13/bayesian-statistics.html#lms) $$\hat\Theta_n=\mathbb E[\Theta\lvert\mathbf X_n]$$ is the best possible solution if our objective is to minimize $$\text{MSE}(\hat\Theta_n)$$. However, not always $$\Theta\lvert\mathbf X_n$$ is easy to compute, or unlike in the [linear model](/2023/06/30/linear-regression.html#lm), the LMS may be a non-linear function of observations $$\mathbf X_n$$.

LLMS estimator provides a compromise, that on one hand is relatively simple in terms of computations involved, while having small (if not the smallest) mean squared error. On the other hand, be aware that while the LMS estimate will always remain within the parameter space, the LLMS estimator cannot provide the same guarantee{% if jekyll.environment == "development" %} (see [Prob L17 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab9)){% endif %}.

### Single observations

In this case, one possible approach is **restricting** the estimator to be linear in observation. With a single observation $$X$$, this means that the estimator should have the form of $$\hat\Theta=a X+b$$ and determine $$a$$ and $$b$$ that minimize $$\text{MSE}(\hat\Theta)=\mathbb E[(\hat\Theta-\Theta)^2]=\mathbb E[(aX+b-\Theta)^2]$$. The estimator so determined is called the **linear least mean square** (LLMS) estimator, and the parameters $$a$$ and $$b$$ can be determiend as as follows:

- **first**, notice that the MSE can be rewritten as $$\mathbb E[(b-(\Theta-aX))^2]$$ and recall that $$b=\mathbb E[\Theta-aX]$$ is what will [minimize](/2022/04/26/methods-of-estimation.html#me) the expectation of a quadratic norm;
- **second**, bearing in mind that $$\mathbb E[(\mathbb E[\Theta-aX]-(\Theta-aX))^2]=\text{var}(\Theta-aX)$$, which in turn can be [expanded](/2022/01/24/further-topics-on-RV.html#covariance) as $$\text{var}(\Theta)+a^2\text{var}(X)-2a\text{cov}(\Theta,X)$$, find $$a=\arg\min_a\text{MSE}(\hat\Theta)$$ by setting $$\frac\partial{\partial a}\text{MSE}(\hat\Theta)=0$$ and deriving that $$a=\frac{\text{cov}(\Theta,X)}{\text{var}(X)}$${% if jekyll.environment == "development" %} (see [Prob L17 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab5)){% endif %}; and
- **finally**, all pieces together bring us $$\hat\Theta=\mathbb E[\Theta]+\frac{\text{cov}(\Theta,X)}{\text{var}(X)}(X-\mathbb E[X])$${% if jekyll.environment == "development" %} (see [Prob L17 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7b/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s7-tab3), [Prob PS7b Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7b/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s7-tab3), [Prob PS7b Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_7b/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s7-tab4) and [Prob F Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab3)){% endif %}.

MSE of LLMS estimator is $$\text{var}(\Theta)(1-\rho_{\Theta X}^2)$$, where $$\rho_{\Theta X}=\frac{\text{cov}(\Theta,X)}{\sqrt{\text{var}(\Theta)\text{var}(X)}}$$ indicates [correlation](/2022/01/24/further-topics-on-RV.html#correlation) between $$\Theta$$ and $$X$$.

$$\begin{align}
\text{MSE}(\hat\Theta)
&=\mathbb E[(\hat\Theta-\Theta)^2]\\
&=\mathbb E\left[\left(\mathbb E[\Theta]+\frac{\text{cov}(\Theta,X)}{\text{var}(X)}(X-\mathbb E[X])-\Theta\right)^2\right]\\
&=\mathbb E\left[\left(\frac{\text{cov}(\Theta,X)}{\text{var}(X)}(X-\mathbb E[X])-(\Theta-\mathbb E[\Theta])\right)^2\right]\\
&=\frac{\text{cov}^2(\Theta,X)}{\text{var}^2(X)}\text{var}(X)+\text{var}(\Theta)-2\frac{\text{cov}(\Theta,X)}{\text{var}(X)}\text{cov}(\Theta,X)\\
&=\text{var}(\Theta)-\frac{\text{cov}^2(\Theta,X)}{\text{var}(X)}\\
&=\text{var}(\Theta)(1-\rho_{\Theta X}^2)
\end{align}$$

Main highlights:

- LLMS estimator is linear in observations:
  - we do not require complete knowledge of distriutions of $$\Theta$$ and $$X$$;
  - only means, variances and covariance (or correlation) matter;
- MSE of the LLMS estimator is driven by covariance (or correlation) as follows:
  - if $$\lvert\rho_{\Theta X}\rvert=1$$, then $$\Theta$$ has a linear relation to $$X$$ and MSE is zero;
  - if $$\rho_{\Theta X}=0$$, then observations are irrelevant (e.g. the relationship between $$X$$ and $$\Theta$$ cannot be described as linear, or $$\Theta\ind X$$), and MSE is the same as variance of $$\Theta$$;
- if $$\mathbb E[\Theta\lvert X]$$ is linear in $$X$$, then LMS and LLMS [coincide](/2023/06/30/linear-regression.html#lms_llms){% if jekyll.environment == "development" %} (see [Prob L17 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab3) and [Prob L17 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab11)){% endif %}.

### Multiple observations

In case of $$n$$ observations of $$X_i$$, the only change in the above formula would be that we have to find $$\mathbf a=\begin{bmatrix}a_1&\dots&a_n\end{bmatrix}^T$$ and $$b$$, such that $$\hat\Theta_n=\mathbf a^T\mathbf X_n+b$$ minimizes $$\text{MSE}(\hat\Theta_n)$$. To find all elements of $$\mathbf a$$, we can follow the same steps we did above.

- set $$b=\mathbb E[\Theta-\mathbf a^T\mathbf X_n]$$; and
- compute $$a_i=\frac{\text{cov}(\Theta,X_i)-\sum_{j\neq i}a_j\text{cov}(X_i,X_j)}{\text{var}(X_i)}$$ by setting $$\nabla_\mathbf a\text{var}(\Theta-\mathbf a^T\mathbf X_n)=0$${% if jekyll.environment == "development" %} (see [Prob L17 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab13)){% endif %}.

$$\begin{align}
\text{var}(\Theta-\mathbf a^T\mathbf X_n)
&=\text{var}(\Theta)+\sum_{i=1}^na_i^2\text{var}(X_i)\\
&-2\sum_{i=1}^na_i\text{cov}(\Theta,X_i)+2\sum_{j\neq i}^na_i a_j\text{cov}(X_i,X_j)
\end{align}$$

- derive $$\hat\Theta_n=\mathbb E[\Theta]+\mathbf a^T(\mathbf X_n-\mathbb E[\mathbf X_n])$$.

Recall that the LMS estimator in the [linear model](/2023/06/30/linear-regression.html#lm) with Normal noise is linear in observations $$\mathbf X_n$$. In particular, if $$X_i=\Theta+W_i$$, after $$n$$ observations the LMS estimator is as follows.

$$\hat\Theta_n^{LMS}=\frac{\frac1{\sigma_0^2}x_0+\sum_{i=1}^n\frac1{\sigma_i^2}X_i}{\sum_{i=0}^n\frac1{\sigma_i^2}}$$

At the same time, we know that if we were to find the LLMS, it will have the form of $$\mathbf a^T\mathbf X_n+b$$, with $$b=\mathbb E[\Theta-\mathbf a^T\mathbf X_n]$$ and $$a_i=\frac{\text{cov}(\Theta,X_i)-\sum_{j\neq i}a_j\text{cov}(X_i,X_j)}{\text{var}(X_i)}$$. Considering that $$\mathbb E[X_i]=\mathbb E[\Theta]=x_0$$, $$\text{var}(X_i)=\sigma_0^2+\sigma_i^2$$ and $$\text{cov}(\Theta,X_i)=\text{cov}(X_i,X_j)=\sigma_0^2$${% if jekyll.environment == "development" %} (see [Prob L17 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab8)){% endif %}, it follows that $$b=(1-\sum_{i=1}^n a_i)x_0$$ and $$a_i=\frac{\sigma_0^2}{\sigma_0^2+\sigma_i^2}(1-\sum_{j\neq i}a_j)$$, which leads to a system of $$n$$ equations with the following solution.

$$\begin{align}
a_j=\frac{\frac1{\sigma_j^2}}{\sum_{i=0}^n\frac1{\sigma_i^2}}&&b=\frac{\frac1{\sigma_0^2}}{\sum_{i=0}^n\frac1{\sigma_i^2}}&&\hat\Theta_n^{LLMS}=\frac{\frac1{\sigma_0^2}x_0+\sum_{i=1}^n\frac1{\sigma_i^2} X_i}{\sum_{i=0}^n\frac1{\sigma_i^2}}
\end{align}$$

Remarkably, in addition to confirming that LMS and LLMS coincide in case of a linear model, the above solution is valid even if $$\Theta$$ and $$W_i$$ are not Normally distributed, provided that they are uncorrelated, and have the same means and variances as in the Normal case.

As LMS and LLMS estimators coincide for the [linear model](/2023/06/30/linear-regression.html#lm), their [generalizations](/2023/06/30/linear-regression.html#generalizations) solutions coincide as well. In particular, if our linear model is of the form $$X_i=\mathbf y_i^T\boldsymbol{\Theta}+W_i$$, then $$\hat{\boldsymbol{\Theta}}$$ becomes as follows.

$$\begin{align}
\hat{\boldsymbol{\Theta}}=\begin{bmatrix}\hat\Theta_1&\dots&\hat\Theta_d\end{bmatrix}^T&\text{, where }\hat\Theta_j=\frac{\frac1{\sigma_0^2}x_0+\sum_{i=1}^n\frac1{\tilde\sigma_{ij}^2}\tilde X_{ij}}{\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}}=\frac{\frac1{\sigma_0^2}x_0+\sum_{i=1}^n\frac1{\sigma_i^2}y_{ij}X_i}{\sum_{i=0}^n\frac{y_{ij}^2}{\sigma_i^2}}
\end{align}$$

Final remark is regarding the meaning of the term "*linear*" in LLMS. The term refers to the linear relation of $$\hat{\boldsymbol{\Theta}}$$ and the coefficients $$\mathbf a$$ and $$b$$ that we need to determine. If, instead of observing $$X_i$$, we observe $$X_i^k$$, or $$e^{X_i}$$ (and treat them as different observations), it will not change the linear nature of the estimator{% if jekyll.environment == "development" %} (see [Prob L17 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__17_Linear_least_mean_squares__LLMS__estimation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch10-s6-tab16)){% endif %}. However, in this case LLMS may not coincide with the LMS, unless it is also linear in $$X_i^k$$ or $$e^{X_i}$$, as the case may be.

## Linear Regression

## Exponential families

## Generalized Linear Models (GLM)

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

### Multivariate linear model {#multivariate_lm}

While glossing over the details, derivation of $$\mathbf H\lvert\mathbf X_n$$ for $$X_i=\mathbf a_i\mathbf H+W_i$$ can be done in the same way we [derived](/2023/06/30/linear-regression.html#lm) $$\Theta\lvert\mathbf X_n$$, which means taking note of what happens with a single observation $$X_1$$ and then adding subsequent observations. To this end, observe the [posterior](/2023/03/13/bayesian-statistics.html#bayes) after a single observation $$X_1$$ and isolate $$\eta_j$$, for any given $$j$$.

$$\begin{align}
\pi(\boldsymbol{\eta}\lvert X_1)&\propto\pi(\boldsymbol{\eta})\mathcal L_1(X_1\lvert\boldsymbol{\eta})=\pi(\eta_j)\pi(\boldsymbol{\eta}_{k\neq j})\mathcal L_1(X_1\lvert\eta_j,\boldsymbol{\eta}_{k\neq j})\\
&\propto\exp\left\{-\frac12\left(\frac{\eta_j-x_{0j}}{\sigma_{0j}}\right)^2\right\}\pi(\boldsymbol{\eta}_{k\neq j})\exp\left\{-\frac12\left(\frac{x_1-\sum_{k\neq j}a_{1k}\eta_k-a_{1j}\eta_j}{\sigma_1}\right)^2\right\}\\
&=\exp\left\{-\frac12\left[\left(\frac{\eta_j-x_{0j}}{\sigma_{0j}}\right)^2+\left(\frac{\tilde x_{1j}-\eta_j}{\tilde\sigma_{1j}}\right)^2\right]\right\}\pi(\boldsymbol{\eta}_{k\neq j})
\end{align}$$

Bearing in mind that $$\tilde x_{1j}=\frac{x_1-\sum_{k\neq j}a_{1k}\eta_k}{a_{1j}}$$ and $$\tilde\sigma_{1j}=\frac{a_{1j}}{\sigma_1}$$, by inspecting one should be able to see that using the same approach as in the [sum of independent Normal r.v.](/2022/01/24/further-topics-on-RV.html#proof_sum_normal), we can further split the exponent.

$$\begin{align}
\pi(\boldsymbol{\eta}\lvert X_1)
&\propto\exp\left\{-\frac12\left[\left(\frac{\eta_j-\mu_{H_j\lvert X_1,\mathbf H_{k\neq j}}}{\sigma_{H_j\lvert X_1,\mathbf H_{k\neq j}}}\right)^2+\left(\frac{x_1-\mu_{X_1\lvert\mathbf H_{k\neq j}}}{\sigma_{X_1\lvert\mathbf H_{k\neq j}}}\right)^2\right]\right\}\pi(\boldsymbol{\eta}_{k\neq j})\\
&\propto\pi(\eta_j\lvert X_1,\mathbf H_{k\neq j})\mathcal L_1(X_1\lvert\mathbf H_{k\neq j})\pi(\boldsymbol{\eta}_{k\neq j})
\end{align}$$

Since $$H_j\lvert X_1,\mathbf H_{k\neq j}$$ is Normally distributed, with parameters $$\mu_{H_j\lvert X_1,\mathbf H_{k\neq j}}$$ and $$\sigma_{H_j\lvert X_1,\mathbf H_{k\neq j}}^2$$, observe how the strcture of the said parameters has not changed with respect to the [simple linear model](/2023/06/30/linear-regression.html#lm), that can be promptly extended for any $$n\ge1$$ (bearing in mind that $$\tilde x_{0j}=x_{0j}$$ and $$\tilde\sigma_{0j}^2=\sigma_{0j}^2$$).

$$\begin{align}\begin{cases}
\displaystyle\sigma_{H_j\lvert X_1,\mathbf H_{k\neq j}}^2=\frac1{\frac1{\sigma_{0j}^2}+\frac{a_{1j}^2}{\sigma_1^2}}=\frac1{\sum_{i=0}^1\frac1{\tilde\sigma_{ij}^2}}\\
\displaystyle\mu_{H_j\lvert X_1,\mathbf H_{k\neq j}}=\sigma_{H_j\lvert X_1,\mathbf H_{k\neq j}}^2\left(\frac1{\sigma_{0j}^2}x_{0j}+\frac{a_{1j}^2}{\sigma_1^2}\frac{x_1-\sum_{k\neq j}a_{1k}\eta_k}{a_{1j}}\right)=\sigma_{H_j\lvert X_1,\mathbf H_{k\neq j}}\sum_{i=0}^1\frac1{\tilde\sigma_{ij}^2}\tilde x_{ij}
\end{cases}\end{align}$$

So, in the above derivation we showed that we can split the posterior and segregate individual $$\eta_j$$ to derive respective Bayesian estimations, that is $$\hat H_j=\mathbb E[H_j\lvert\mathbf X_n,\mathbf H_{k\neq j}]=\mu_{H_j\lvert\mathbf X_n,\mathbf H_{k\neq j}}$$. Considering that $$\hat{\mathbf H}=\begin{bmatrix}\hat H_1&\dots&\hat H_d\end{bmatrix}^T$$, we will need to solve $$d$$ linear equations with $$d$$ variables.

Remarkably, we would have come to the same conclusion if we derived $$\hat{\mathbf H}=\arg\max_{\boldsymbol{\eta}\in\mathbb R^d}\pi(\boldsymbol{\eta}\lvert\mathbf X_n)$$, s.t. $$\nabla_{\boldsymbol{\eta}}\ln(\pi(\hat{\boldsymbol{\eta}}\lvert\mathbf X_n))=\mathbf 0_d$$. This can be achieved by taking note of the term in the following term in the exponent of the posterior and setting to zero its partial derivatives, with respect to each $$\eta_j$$.

$$\begin{align}
\frac\partial{\partial\eta_j}\ln(\pi(\boldsymbol{\eta}\lvert\mathbf X_n))
&=\frac\partial{\partial\eta_j}\left(\sum_{j=1}^d\left(\frac{\eta_j-x_{0j}}{\sigma_{0j}}\right)^2+\sum_{i=1}^n\left(\frac{x_i-\sum_{j=1}^da_{ij}\eta_j}{\sigma_i}\right)^2\right)\\
&=-\frac1{\sigma_{0j}^2}(\eta_j-x_{0j})+\sum_{i=1}^n\frac{a_{ij}}{\sigma_i^2}\left(x_i-a_{ij}\eta_j-\sum_{k\neq j}a_{ik}\eta_k\right)\\
&=-\eta_j\left(\frac1{\sigma_{0j}^2}+\sum_{i=1}^n\frac{a_{ij}^2}{\sigma_i^2}\right)+\left(\frac1{\sigma_{0j}^2}x_{0j}+\sum_{i=1}^n\frac{a_{ij}^2}{\sigma_i^2}\frac{x_i-\sum_{k\neq j}a_{ik}\eta_k}{a_{ij}}\right)\\
&=-\eta_j\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}+\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}\tilde x_{ij}=0\\
\implies\hat H_j&=\frac{\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}\tilde x_{ij}}{\sum_{i=0}^n\frac1{\tilde\sigma_{ij}^2}}=\mu_{H_j\lvert\mathbf X_n,\mathbf H_{k\neq j}}
\end{align}$$

### LMS linear in observation vs LLMS {#lms_llms}

Recall that the LLMS is an estimator constrained to have the form $$\hat\Theta^{LLMS}=aX+b$$, where $$a$$ and $$b$$ are determined in a way to minimize $$\text{MSE}(\hat\Theta)=\mathbb E[(\hat\Theta-\Theta)^2]$$. At the same time, observe that if the LMS estimator, defined as $$\hat\Theta^{LMS}=\mathbb E[\Theta\lvert X]$$, i.e. the [minimizer](/2022/04/26/methods-of-estimation.html#me) of quadratic norm $$\mathbb E[\lVert\hat\Theta-\Theta\rVert_2^2]$$, turns out to be linear in observations, or $$\hat\Theta^{LMS}=\alpha X+\beta$$, then necessarily $$a=\alpha$$, and $$b=\beta$$. Thus, we may conclude that if $$\mathbb E[\Theta\lvert X]$$ is linear in $$X$$, then LMS and LLMS necessarily coincide.

For a practical example, assume that $$\Theta\sim\text{Unif}(0,1)$$, and that our observations $$X$$ are distributed according to $$X\lvert\Theta\sim\text{Bin}(n,\theta)$$. Since the prior $$\pi(\theta)=1$$, it [follows that](/2023/03/13/bayesian-statistics.html#bayes) $$\pi(\theta\lvert x)\propto\theta^{x}(1-\theta)^{n-x}$$, which essentially means that $$\Theta\lvert X\sim\text{Beta}(X+1,n-X+1)$$. [Hence](/2023/03/13/bayesian-statistics.html#lms), $$\hat\Theta^{LMS}=\mathbb E[\Theta\lvert X]=\frac{X+1}{n+2}$$. Since $$\hat\Theta$$ is linear in $$X$$, we expect that the LMS and LLMS estimators will coincide.

As for the LMS, recall that $$\hat\Theta^{LLMS}=\mathbb E[\Theta]+\frac{\text{cov}(\Theta,X)}{\text{var}(X)}(X-\mathbb E[X])$$. As $$\mathbb E[\Theta]=\frac12$$, $$\text{var}(\Theta)=\frac1{12}$$, $$\mathbb E[\Theta^2]=\frac13$$, $$\mathbb E[X\lvert\Theta]=n\Theta$$, $$\text{var}(X\lvert\Theta)=n\Theta(1-\Theta)$$, we can promptly determine the missing pieces, such as $$\mathbb E[X]=\mathbb E[\mathbb E[X\lvert\Theta]]=\frac n2$$, $$\text{var}(X)=\href{/2022/01/24/further-topics-on-RV.html#total_expectation}{\mathbb E[\text{var}(X\lvert\Theta)]+\text{var}(\mathbb E[X\lvert\Theta])}=\frac{n(n+2)}{12}$$, and $$\text{cov}(\Theta,X)=\href{/2022/01/24/further-topics-on-RV.html#covariance}{\mathbb E[\Theta\mathbb E[X\lvert\Theta]]-\mathbb E[\Theta]\mathbb E[X]}=\frac n{12}$$. Hence, $$\hat\Theta^{LLMS}=\frac{X+1}{n+2}$$, as expected.
