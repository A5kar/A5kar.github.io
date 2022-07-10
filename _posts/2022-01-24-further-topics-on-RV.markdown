---
layout: post
title: "Further topics on r.v."
---

## Derived distributions {#derived_distributions}

Probability law on $$Y$$, where $$Y=g(X)$$ depends on whether $$X$$ is discrete or continuous r.v.{% if jekyll.environment == "development" %} (see [Prob L11 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__11_Derived_distributions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s2-tab5)){% endif %}. In the first case, our computations are based on the fact that $$p_Y(y)=\mathbb P(g(X)=y)$$. Else, we follow a two-step procedure: find $$F_Y(y)=\mathbb P(g(X)\le y)$$, and differentiate $$f_Y(y)=\frac{\partial}{\partial y}F_Y(y)$${% if jekyll.environment == "development" %} (see [Prob MT2 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch11-s1-tab2), [Prob MT2 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch11-s1-tab4) and [Prob MT2 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch11-s1-tab6)){% endif %}.

|$$g(X)$$|$$X$$ discrete|$$X$$ continuous|
|:-:|:-:|:-:|
|linear<br>$$g(X)=aX+b$$|$$\displaystyle p_Y(y)=p_X\left(\frac{y-b}{a}\right)$${% if jekyll.environment == "development" %}<br>(see [Prob L11 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__11_Derived_distributions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s2-tab3)){% endif %}|$$\displaystyle f_Y(y)=f_X\left(\frac{y-b}{a}\right)\frac{1}{\lvert a\rvert}$$|
|strictly monotonic<br>(hence invertible)<br>$$X=h(Y)$$|$$\displaystyle p_Y(y)=p_X(h(y))$$|$$\displaystyle f_Y(y)=f_X(h(y))\left\lvert\frac{\partial}{\partial y}h(y)\right\rvert$${% if jekyll.environment == "development" %}<br>(see [Prob L11 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__11_Derived_distributions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s2-tab8), [Prob L11 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__11_Derived_distributions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s2-tab10) and [Prob PS6 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab1)){% endif %}|
|general|$$\displaystyle p_Y(y)=\sum_{x:g(x)=y}p_X(x)$$|$$\displaystyle f_Y(y)=\sum_{h_i(y):g(h_i(y))=y}f_X(h_i(y))\left\lvert\frac{\partial}{\partial y}h_i(y)\right\rvert$${% if jekyll.environment == "development" %}<br>(see [Prob L11 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__11_Derived_distributions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s2-tab13) and [Prob PS6 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab2)){% endif %}|

Note that if $$X$$ is uniform (irrespective if discrete or continuous), a linear combination $$Y=aX+b$$ is still uniform, just with a different *scale* and *location*{% if jekyll.environment == "development" %} (see [Prob PS5 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab4) and [Stats HW0 Q4](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab4)){% endif %}.

The general continuous case assumes that the domain can be split into intervals within which $$g(X)$$ is still **strictly** monotonic, this to ensure that $$\nexists y:\mathbb P(Y=y)\neq0$$. Otherwise, we would fall into a mixed discrete/continuous r.v. case.

Finally, observe that if $$X\sim\mathcal N(\mu_X,\sigma_X^2)$$ then for any $$Y=aX+b$$, we have that $$Y\sim\mathcal N(a\mu_X+b,a^2\sigma_X^2)$$.

## Simulation

An approach similar to derived distributions can be used to simulate *any* distribution, starting from $$U\sim\text{Unif}(0,1)$$. In particular, by observing that $$\mathbb P(U\le F_X(x))=F_X(x)$$, we can adopt the following solutions, depending on whether $$X$$ is discrete or continuous.

- **Discrete case**: we assign to $$X$$ the $$k$$-th value that satisfies $$F_X(k-1)\lt u\le F_X(k)$$; and
- **Continuous case**: we assign to $$X$$ that $$x$$ that satisfies $$u=F_X(x)$$.

## Function of multiple r.v.

Calculating probability law on $$Z=g(X,Y)$$ is not different from the single r.v. case. If $$f_{Y\lvert X}(y\lvert x)$$ is available and $$\exists h:Y=h(Z,X)$$, we can compute $$f_{Z\lvert X}(z\lvert x)$$ in terms of $$f_{Y\lvert X}(y\lvert x)$$ and $$y=h(z,x)$$ bearing in mind that $$X=x$$ is given. In other words, we derive $$F_{Z\lvert X}(z\lvert x)=F_{Y\lvert X}(h(x,z)\lvert x)$$, and then differentiate $$f_{Z\lvert X}(z\lvert x)=f_{Y\lvert X}(h(x,z)\lvert x)\left\lvert\frac{\partial}{\partial z}h(x,z)\right\rvert$$. At this point, total probability theorem tells us that $$f_Z(z)=\int_{-\infty}^\infty f_X(x)f_{Z\lvert X}(z\lvert x)dx$$.

Sometimes, calculations can be simplified. Assume $$f_{X,Y}(x,y)=c$$ is constant and $$Z=g(X,Y)$$ is associated with area $$A(Z)$$ in the $$X$$---$$Y$$ plane. In this case, $$F_Z(z)=\mathbb P(g(X,Y)\le z)=cA(z)$${% if jekyll.environment == "development" %} (see [Prob L11 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__11_Derived_distributions/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s2-tab15)){% endif %}.

As for $$\max$$ and $$\min$$ functions, if $$X\perp Y$$, we have $$\mathbb P(\max\{X,Y\}\le z)=F_X(z)F_Y(z)$${% if jekyll.environment == "development" %} (see [Prob PS6 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab3) and [Prob F Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab5)){% endif %}, and $$\mathbb P(\min\{X,Y\}\le z)=1-(1-F_X(z))(1-F_Y(z))$$.

## Sum of independent r.v.

If $$X$$ and $$Y$$ are discrete r.v., with $$X\perp Y$$, the distribution of $$Z=X+Y$$ can be obtained by deriving $$p_{Z\lvert X}(z\lvert x)=p_Y(z-x)$$ and computing $$p_Z(z)=\sum_x p_X(x)p_Y(z-x)$${% if jekyll.environment == "development" %} (see [Prob L12 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab3)){% endif %}. If $$X$$ and $$Y$$ are continuous, use $$f_{Z\lvert X}(z\lvert x)=f_Y(z-x)$$ and $$f_Z(z)=\int_{-\infty}^\infty f_X(x)f_Y(z-x)dx$$ instead{% if jekyll.environment == "development" %} (see [Prob L12 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab5) and [Prob PS6 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab4)){% endif %}. Due to its widespread use, the aforementioned formula is referred to as [convolution](https://en.wikipedia.org/wiki/Convolution).

For the general case $$Z=aX+bY$$, where $$a,b\in\mathbb R$$, we get either $$p_Z(z)=\sum_x p_X(\frac{x}{a})p_Y(\frac{z-x}{b})$$ or $$f_Z(z)=\int_{-\infty}^\infty f_X(\frac{x}{a})\frac{1}{\lvert a\rvert}f_Y(\frac{z-x}{b})\frac{1}{\lvert b\rvert}dx$$, depending on whether $$X$$ and $$Y$$ are discrete or continuous.

## Sum of independent Normal r.v.

If $$X\sim\mathcal N(\mu_X,\sigma_X^2)$$, $$Y\sim\mathcal N(\mu_Y,\sigma_Y^2)$$, and $$X\perp Y$$, expectation and variance of $$Z=X+Y$$ are $$\mu_Z=\mathbb E[Z]=\mu_X+\mu_Y$$ and $$\sigma_Z^2=\text{var}(X+Y)=\sigma_X^2+\sigma_Y^2$$, respectively. Not only, the distribution of $$Z$$ is also normal and $$Z\sim\mathcal N(\mu_Z,\sigma_Z^2)$${% if jekyll.environment == "development" %} (see [Prob L12 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab7)){% endif %}, which can be proved by observing that $$f_X(x)f_Y(z-x)$$ can be rewritten as follows.

$$\begin{align}
f_X(x)f_Y(z-x)&=\frac{1}{\sqrt{2\pi\sigma_X^2}}\exp\left\{-\frac1{2\sigma_X^2}(x-\mu_X)^2\right\}\frac{1}{\sqrt{2\pi\sigma_Y^2}}\exp\left\{-\frac1{2\sigma_Y^2}(z-x-\mu_Y)^2\right\}\\
&=\frac{1}{2\pi\sigma_X\sigma_Y}\exp\left\{-\frac1 2 A\right\}\text{, where}\\
A&=\frac{(x-\mu_X)^2}{\sigma_X^2}+\frac{((z-\mu_Y)-\mu_X)^2}{\sigma_Y^2}\\
&=\frac{x^2\sigma_Z^2-2x((z-\mu_Y)\sigma_X^2+\mu_X^2\sigma_Y^2)+(z-\mu_Y)^2\sigma_X^2+\mu_X^2\sigma_Y^2}{\sigma_X^2\sigma_Y^2}\\
&=\frac{x^2-2x\mu_{X\lvert Z}+((z-\mu_Y)^2\sigma_X^2+\mu_X^2\sigma_Y^2)\sigma_Z^{-2}}{\sigma_{X\lvert Z}}\\
&=\frac{(x-\mu_{X\lvert Z})^2}{\sigma_{X\lvert Z}}+\frac{\mu_{X\lvert Z}^2+((z-\mu_Y)^2\sigma_X^2+\mu_X^2\sigma_Y^2)\sigma_Z^{-2}}{\sigma_{X\lvert Z}}\\
&=\frac{(x-\mu_{X\lvert Z})^2}{\sigma_{X\lvert Z}}+\frac{(z-\mu_Z)^2}{\sigma_Z^2}\text{, accordingly}
\end{align}$$
$$\begin{align}
f_X(x)f_Y(z-x)&=\underbrace{\frac{1}{\sqrt{2\pi\sigma_{X\lvert Z}^2}}\exp\left\{-\frac1{2\sigma_{X\lvert Z}^2}(x-\mu_{X\lvert Z})^2\right\}}_{=f_{X\lvert Z}(x\lvert z)}\underbrace{\frac{1}{\sqrt{2\pi\sigma_Z^2}}\exp\left\{-\frac1{2\sigma_Z^2}(z-\mu_Z)^2\right\}}_{f_Z(z)}
\end{align}$$

Where we applied the following substitutions, $$\begin{cases}\sigma_{X\lvert Z}=\frac{\sigma_X^2\sigma_Y^2}{\sigma_Z^2}\\\mu_{X\lvert Z}=\frac{\sigma_X^2(z-\mu_Y)+\sigma_Y^2\mu_X}{\sigma_Z^2}\end{cases}$$ and $$\begin{cases}\sigma_Z^2=\sigma_X^2+\sigma_Y^2\\\mu_Z=\mu_X+\mu_Y\end{cases}$$. If we apply the definition $$f_Z(z)=\int_{-\infty}^\infty f_X(x)f_Y(z-x)dx$$ we observe that indeed $$Z\sim\mathcal N(\mu_Z,\sigma_Z^2)$$.

$$\begin{align}
f_Z(z)&=\int_{-\infty}^\infty f_X(x)f_Y(z-x)dx=\int_{-\infty}^\infty f_Z(z)f_{X\lvert Z}(x\lvert z)dx\\
&=f_Z(x)\cancelto{=1}{\int_{-\infty}^\infty f_{X\lvert Z}f(x\lvert z)dx}=\frac{1}{\sqrt{2\pi\sigma_Z^2}}\exp\left\{-\frac1{2\sigma_Z^2}(z-\mu_Z)^2\right\}
\end{align}$$

## Covariance {#covariance}

Defined as $$\sigma_{XY}=\text{cov}(X,Y)=\mathbb E[(X-\mathbb E[X])(Y-\mathbb E[Y])]$$, covariance is a measure of the joint variability of two r.v.{% if jekyll.environment == "development" %} (see [Prob L12 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab11)){% endif %}.

|Property|Formula|
|-|:-:|
|Variance|$$\text{cov}(X,X)=\text{var}(X)$$|
|Symmetry|$$\text{cov}(X,Y)=\text{cov}(Y,X)$$|
|Independence|$$\text{cov}(X,a)=0$$, for any $$a$$ constant<br>$$X\perp Y\implies\text{cov}(X,Y)=0$$<br>(the converse is not true in general{% if jekyll.environment == "development" %} (see [Prob MT2 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch11-s1-tab2)){% endif %})|
|Bilinear|$$\text{cov}(aX,bY+cZ)=ab\cdot\text{cov}(X,Y)+ac\cdot\text{cov}(X,Z)$${% if jekyll.environment == "development" %}<br>(see [Stats HW0 Q3](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab3)){% endif %}|
|Variance|$$\displaystyle\text{var}\left(\sum_{i=1}^n a_iX_i\right)=\underbrace{\sum_{i=1}^n a_i^2\text{var}(X_i)}_{\text{$n$ terms}}+\underbrace{\sum_{i\neq j}a_ia_j\text{cov}(X_i,X_j)}_{\text{$n^2-n$ terms}}$${% if jekyll.environment == "development" %}<br>(see [Prob L12 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab13)){% endif %}<br>$$\text{var}(aX+bY)=a^2\text{var}(X)+b^2\text{var}(Y)+2ab\text{cov}(X,Y)$$|
|Equivalency|$$\begin{align}\text{cov}(X,Y)&=\mathbb E[XY]-\mathbb E[X]\mathbb E[Y]\\&=\mathbb E[(X-\mathbb E[X])Y]\\&=\mathbb E[\mathbb E[XY\lvert X]]-\mathbb E[X]\mathbb E[\mathbb E[Y\lvert X]]\end{align}$${% if jekyll.environment == "development" %}<br>(see [Prob L12 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab9), [Prob PS6 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab5) and [Prob F Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab4), [Stats L10 Q5](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab5) and [Stats HW5 Q1](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw5_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw5_u3methods-tab1)){% endif %}|

Assume $$A=X+Y$$ and $$B=X-Y$$ and $$\sigma_X^2=\sigma_Y^2$$. $$A$$ and $$B$$ are not independent, since they are both linear combinations of $$X$$ and $$Y$$; at the same time $$\sigma_{AB}=\text{cov}(A,B)=\sigma_X^2-\sigma_Y^2=0$$ and therefore $$\sigma_{AB}=0$$ **does not imply** $$A\perp B$${% if jekyll.environment == "development" %} (see [Stats L10 Q6](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab6)){% endif %}.

## Correlation

Correlation is a measure of the degree of **linear** association, whether causal or not, between two r.v. and is defined as $$\rho_{XY}=\mathbb E\left[\left(\frac{X-\mathbb E[X]}{\sigma_X}\right)\left(\frac{Y-\mathbb E[Y]}{\sigma_Y}\right)\right]=\frac{\text{cov}(X,Y)}{\sigma_X\sigma_Y}$${% if jekyll.environment == "development" %} (see [Prob L12 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab15)){% endif %}.

Main properties of the correlation coefficient are that $$\lvert\rho\rvert\le1$$ and that $$\lvert\rho\rvert=1\implies Y=aX$$, with $$a$$ constant, while others can be derived directly from covariance{% if jekyll.environment == "development" %} (see [Prob L12 Q18](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__12_Sums_of_independent_r_v_s__Covariance_and_correlation/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s3-tab18) and [Prob PS6 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab6)){% endif %}.

## Bivariate Normal r.v. {#bivariate_normal}

$$X$$ and $$Y$$ are said to be jointly bivariate Normal r.v. if their joint PDF is as follows.

$$\begin{align}
f_{XY}(x,y)&=\frac{1}{2\pi\sigma_X\sigma_Y\sqrt{1-\rho_{XY}^2}}\exp\left\{-\frac{1}{2}A\right\}\text{, where}\\
A&=\frac{1}{(1-\rho_{XY}^2)}\left(\frac{(x-\mu_X)^2}{\sigma_X^2}+\frac{(y-\mu_Y)^2}{\sigma_Y^2}-\frac{2\rho_{XY}(x-\mu_X)(y-\mu_Y)}{\sigma_X\sigma_Y}\right)
\end{align}$$

From the above, it follows that: (a) $$X\sim\mathcal(\mu_X,\sigma_X^2)$$ and $$Y\sim\mathcal N(\mu_Y,\sigma_Y^2)$$, and (b) that $$\text{cov}(X,Y)$$ is expressed as $$\rho_{XY}\sigma_X\sigma_Y$$. To this end, first notice that $$A$$ can be rewritten as follows.

$$\begin{align}
A&=\frac{(x-\mu_X)^2}{\sigma_X^2}+\frac{(y-\mu_{Y\lvert X})^2}{\sigma_{Y\lvert X}^2}\text{, where}\\
\mu_{Y\lvert X}&=\mu_Y+\rho_{XY}\frac{\sigma_Y}{\sigma_X}(x-\mu_X)\\
\sigma_{Y\lvert X}&=\sigma_Y^2(1-\rho_{XY}^2)
\end{align}$$

Which in turn allows splitting $$f_{XY}(x,y)=f_X(x)f_{Y\lvert X}(y\lvert x)$$.

$$\begin{align}
f_{XY}(x,y)
&=\frac{1}{2\pi\sigma_X\sigma_{Y\lvert X}}\exp\left\{-\frac 1 2\left(\frac{(x-\mu_X)^2}{\sigma_X^2}+\frac{(y-\mu_{Y\lvert X})^2}{\sigma_{Y\lvert X}^2}\right)\right\}\\
&=\underbrace{\frac1{\sqrt{2\pi\sigma_X^2}}\exp\left\{-\frac{1}{2\sigma_X^2}(x-\mu_X)^2\right\}}_{=f_X(x)}\underbrace{\frac1{\sqrt{2\pi\sigma_{Y\lvert X}^2}}\exp\left\{-\frac{1}{2\sigma_{Y\lvert X}^2}(y-\mu_{Y\lvert X})^2\right\}}_{=f_{Y\lvert X}(y\lvert x)}\\
\end{align}$$

At this point, one observes that $$X\sim\mathcal N(\mu_X,\sigma_X^2)$$ and the same logic applies to show normality of $$Y$$.

$$\begin{align}
f_X(x)
&=\int_{-\infty}^\infty f_{XY}(x,y)dy=\int_{-\infty}^\infty f_X(x)f_{Y\lvert X}(y\lvert x)dy\\
&=f_X(x)\cancelto{=1}{\int_{-\infty}^\infty f_{Y\lvert X}(y\lvert x)dy}=\frac1{\sqrt{2\pi\sigma_X^2}}\exp\left\{-\frac{1}{2\sigma_X^2}(x-\mu_X)^2\right\}
\end{align}$$

Incidentally, it is also comforting to see that covariance and correlation are bound by $$\rho_{XY}\sigma_X\sigma_Y$$.

$$\begin{align}
\text{cov}(X,Y)
&=\mathbb E[XY]-\mathbb E[X]\mathbb E[Y]=\mathbb E[X\mu_{Y\lvert X}]-\mu_X\mu_Y\\
&=\rho_{XY}\frac{\sigma_Y}{\sigma_X}(\mathbb E[X^2]-\mu_X^2)=\rho_{XY}\sigma_X\sigma_Y
\end{align}$$

## Covariance matrix {#covariance_matrix}

Assume a **random vector** $$\mathbf X=\begin{bmatrix}X^{(1)}&\dots&X^{(d)}\end{bmatrix}\in\mathbb R^d$$, where every $$X^{(i)}$$ is a r.v. A **covariance matrix** is defined as $$\Sigma_{\mathbf X}=\text{cov}(\mathbf X)=\mathbb E[(\mathbf X-\mu_{\mathbf X})(\mathbf X-\mu_{\mathbf X})^T]$$, where $$\mu_{\mathbf X}=\mathbb E[\mathbf X]$$.

|Property|Formula|
|-|:-:|
|Symmetry|$$\Sigma_{\mathbf X}=\Sigma_{\mathbf X}^T$$|
|Eigen-decomposition (diagonalization)|$$\mathbf P^T\Sigma_{\mathbf X}\mathbf P=\mathbf D$$, where $$\mathbf P$$ orthogonal ($$\mathbf P^T\mathbf P=\mathbf P\mathbf P^T=\mathbf I$$), and $$\mathbf D$$ diagonal matrix formed with eigenvalues of $$\Sigma_{\mathbf X}$$|
|Semi-positive definite|$$\mathbf x^T\Sigma_{\mathbf X}\mathbf x\ge0$$, $$\forall\mathbf x\in\mathbb R^d$$. If $$\mathbf x^T\Sigma_{\mathbf X}\mathbf x=0$$ for some $$\mathbf x$$, then $$\Sigma_{\mathbf X}$$ is not invertible, and $$\Sigma_{\mathbf X}^{-1}$$ does not exist{% if jekyll.environment == "development" %}<br>(see [Stats HW5 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@hw5_u3methods/block-v1:MITx+18.6501x+2T2021+type@vertical+block@hw5_u3methods-tab2) and [Stats L11 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s04_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s04_methodestimation-tab2)){% endif %}|
|Square root|$$\exists!\Sigma_{\mathbf X}^{\frac 1 2}$$ semi-positive definite, s.t. $$\Sigma_{\mathbf X}^{\frac 1 2}\Sigma_{\mathbf X}^{\frac 1 2}=\Sigma_{\mathbf X}$$|
|Scaled by the square|$$\text{cov}(\mathbf A^T\mathbf X)=\mathbf A^T\Sigma_{\mathbf X}\mathbf A$$|
|Invariant with respect to location|$$\text{cov}(\mathbf A^T\mathbf X+\mathbf B)=\mathbf A^T\Sigma_{\mathbf X}\mathbf A$${% if jekyll.environment == "development" %}<br>(see [Stats L10 Q8](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab8)){% endif %}|

Basic example of covariance matrix is in case of Categorical distribution, being a multivariate generalization of Bernoulli distribution. In case of $$\mathbf p=\begin{bmatrix}p_1&\dots&p_d\end{bmatrix}^T$$, covariance matrix $$\Sigma_{\mathbf X}$$ becomes as follows.

$$\Sigma_{\mathbf X}=\begin{bmatrix}p_1(1-p_1)&&-p_1p_d\\&\ddots&\\-p_1p_d&&p_d(1-p_d)\end{bmatrix}\text{ or }(\Sigma_{\mathbf X})_{ij}=\begin{cases}\text{var}(X_i)&i=j\\\text{cov}(X_i,X_j)&i\neq j\end{cases}$$

|r.v.|PMF<br>$$p_X(x)$$|Expectation<br>$$\mu_{\mathbf X}=\mathbb E[\mathbf X]$$|Variance<br>$$\Sigma_{\mathbf X}=\text{cov}(\mathbf X)$$|
|-|:-:|:-:|:-:|:-:|
|Categorical<br>$$\text{Cat}(\mathbf p)$$|$$\begin{cases}\prod_{j=1}^d p_j^{x_j}&x_j\in\{0,1\}\\0&\text{otherwise}\end{cases}$$<br>$$\sum_{j=1}^d x_j=1$$, $$\sum_{j=1}^d p_j=1$$|$$\mathbf p$$|$$\text{cov}(\mathbf X)$$|
|Multinomial<br>$$\text{Mult}(k,\mathbf p)$$|$$\begin{cases}{k \choose a_1,\dots,a_d}\prod_{j=1}^d p_j^{x_j}&x_j\in\{0,1,\dots,k\}\\0&\text{otherwise}\end{cases}$$<br>$$\sum_{j=1}^d x_j=k$$, $$\sum_{j=1}^d p_j=1$$|$$k\mathbf p$$|$$k\text{cov}(\mathbf X)$$|

## Multivariate Normal r.v. {#multivariate_normal}

$$\mathbf X=\begin{bmatrix}X^{(1)}&\dots&X^{(d)}\end{bmatrix}\in\mathbb R^d$$ is a **multivariate** Normal r.v., and is defined as $$\mathbf X\sim\mathcal N_d(\mu_\mathbf X,\Sigma_\mathbf X)$$ if $$\forall\mathbf A=\begin{bmatrix}a_1&\dots&a_d\end{bmatrix}^T\in\mathbb R^d$$, we have that $$\mathbf A^T\mathbf X\sim\mathcal N_d\left(\mathbf A^T\mu_\mathbf X,\mathbf A^T\Sigma_\mathbf X\mathbf A\right)$$.

If the above condition holds, then the PDF of $$\mathbf X$$ is as follows.

$$f_\mathbf X(\mathbf x)=\frac 1 {\sqrt{(2\pi)^d\det(\Sigma_\mathbf X)}}\exp\left\{-\frac 1 2(\mathbf x-\mu_\mathbf X)^T\Sigma_\mathbf X^{-1}(\mathbf x-\mu_\mathbf X)\right\}$$

Above definition implies that any linear combination of elements of $$\mathbf X$$ is *one-dimension* Normal r.v. (or a constant, that is a Normal r.v. with zero variance), which in turn requires every $$X^{(i)}$$ to be Normal r.v. and any pair $$(X^{(i)},X^{(j)})$$ to be a [bivariate](/2022/01/24/further-topics-on-RV.html#bivariate_normal) Normal r.v.{% if jekyll.environment == "development" %} (see [Stats L10 Q9](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@u03s03_methodestimation/block-v1:MITx+18.6501x+2T2021+type@vertical+block@u03s03_methodestimation-tab9)){% endif %}.

The latter condition should not be taken for granted. Assume $$X^{(i)}\sim\mathcal N(0,1)$$ and $$X^{(j)}=RX$$, where $$R=2B-1$$ and $$B\sim\text{Ber}(\frac 1 2)$$ (where $$R$$ is [Rademacher distribution](https://en.wikipedia.org/wiki/Rademacher_distribution)). In this case, despite both $$X^{(i)}$$ and $$X^{(j)}$$ are standard Normal r.v., their sum is not a Normal r.v.

$$X^{(i)}+X^{(j)}=\begin{cases}0&\text{with probability $\frac 1 2$}\\2X&\text{with probability $\frac 1 2$}\end{cases}$$

Conversely, any bivariate Normal r.v. can be derived from multivariate Normal r.v. with $$d=2$$. Assume $$Z_1,Z_2\overset{i.i.d.}{\sim}\mathcal N(0,1)$$ and $$\mathbf Z=\begin{bmatrix}Z_1&Z_2\end{bmatrix}^T$$. Note that any $$\mathbf X=\begin{bmatrix}X_1&X_2\end{bmatrix}$$ with covariance $$\rho\sigma_1\sigma_2$$can be expressed as $$\mathbf X=\mathbf A^T\mathbf Z+\mu_{\mathbf X}$$.

$$\mathbf A^T\mathbf Z+\mu_{\mathbf X}=\begin{bmatrix}\sigma_1&0\\\sigma_2\rho&\sigma_2\sqrt{1-\rho^2}\end{bmatrix}\begin{bmatrix}Z_1\\Z_2\end{bmatrix}+\begin{bmatrix}\mu_1\\\mu_2\end{bmatrix}=\begin{bmatrix}\sigma_1 Z_1+\mu_1\\\sigma_2(Z_1\rho+Z_2\sqrt{1-\rho^2})+\mu_2\end{bmatrix}$$

In particular, if $$\mathbf Z\sim\mathcal N_2(\mathbf 0,\mathbf I_2)$$, then $$\mathbf X\sim\mathcal N_2(\mu_\mathbf X,\Sigma_\mathbf X)$$, where the covariance matrix is as follows.

$$\Sigma_\mathbf X=\mathbf A^T\mathbf A=\begin{bmatrix}\sigma_1&0\\\sigma_2\rho&\sigma_2\sqrt{1-\rho^2}\end{bmatrix}\begin{bmatrix}\sigma_1&\sigma_2\rho\\0&\sigma_2\sqrt{1-\rho^2}\end{bmatrix}=\begin{bmatrix}\sigma_1^2&\rho\sigma_1\sigma_2\\\rho\sigma_1\sigma_2&\sigma_2^2\end{bmatrix}$$

Computing $$f_{X_1X_2}(x_1,x_2)$$ as PDF of a bivariate Normal r.v. from direct application of the definition of $$f_\mathbf X(\mathbf x)$$ should be straightforward. Prior to concluding, observe that standardization of $$\mathbf X$$ can be obtained as $$\mathbf Z=\Sigma_{\mathbf X}^{-\frac 1 2}(\mathbf X-\mu_{\mathbf X})$$, which in case of $$d=2$$ becomes $$\mathbf Z=(\mathbf A^T)^{-1}(\mathbf X-\mu_{\mathbf X})$$.

## Conditional expectation as r.v.

So far, we saw that for any r.v. $$X$$, $$\mathbb E[X]$$ is a number. Same thing happens with conditional expectation, as $$g(y)=\mathbb E[X\lvert Y=y]$$ is still a number, which depends on parameter $$y$$. However, since any function of a r.v. is a r.v. itself, it follows that $$g(Y)=\mathbb E[X\lvert Y]$$ is a r.v., with its own distribution, expectation and variance{% if jekyll.environment == "development" %} (see [Prob L13 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab3) and [Prob L13 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab7)){% endif %}. Same considerations apply to any other function $$\mathbb E[h(X)\lvert Y]$$, such as $$\text{var}(X\lvert Y)=\mathbb E[(X-\mathbb E[X\lvert Y])^2\lvert Y]$$, where the inner $$\mathbb E[X\lvert Y]$$ reminds us that all expectations are conditional on $$Y$${% if jekyll.environment == "development" %} (see [Prob L13 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab10), [Prob L13 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab11), [Prob L13 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab15) and [Prob MT2 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_2/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch11-s1-tab3)){% endif %}.

Assuming for simplicity discrete case, we observe that in accordance with the [total expectation theorem](/2022/01/08/discrete-random-variables.html#conditioning) we have that $$\mathbb E[\mathbb E[X\lvert Y]]=\sum_y p_Y(y)\mathbb E[X\lvert Y=y]=\mathbb E[X]$${% if jekyll.environment == "development" %} (see [Prob L13 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab5)){% endif %}. This is known as the **law of total expectation**, also referred to as the *law of iterated expectations*.

Analogously, one can derive $$\text{var}(X)=\mathbb E[\text{var}(X\lvert Y)]+\text{var}(\mathbb E[X\lvert Y])$$ known as the **law of total variance**. One way to remember the formula is that it calculates the average variance within sections and variance between sections.

A very common situation is when $$X=\sum_{i=1}^N X_i$$, with $$X_i\overset{\text{i.i.d.}}{\sim}\mathcal P$$, and $$N$$ another, independent r.v. In this scenario, $$\mathbb E[X]=\mathbb E[N]\mathbb E[X_i]$$ and $$\text{var}(X)=\mathbb E[N]\text{var}(X_i)+(\mathbb E[X_i])^2\text{var}(N)$${% if jekyll.environment == "development" %} (see [Prob L13 Q18](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__13_Conditional_expectation_and_variance_revisited__Sum_of_a_random_number_of_independent_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s4-tab18), [Prob PS6 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_6/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch9-s7-tab7) and [Prob F Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab6)){% endif %}.

Final remark is that $$\mathbb E[g(Y)X\lvert Y]=g(Y)\mathbb E[X\lvert Y]$$, which comes from the observation that given $$Y=y$$, $$g(Y)$$ is a constant and can be pulled out of the expectation. Also, for any invertible function $$h(Y)$$, we have that $$\mathbb E[X\lvert Y]=\mathbb E[X\lvert h(Y)]$$, due to the fact that $$\mathbb P(Y\le y)=\mathbb P(h(Y)\le h(y))$$.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

|Formula|Equivalent form|
|:-:|:-:|
|$$\sum_{i=1}^d\lambda_d$$<br>$$\lambda_d$$ eigenvalues of $$\mathbf A$$|$$\text{tr}(\mathbf A)$$|
|$$\prod_{i=1}^d\lambda_d$$<br>$$\lambda_d$$ eigenvalues of $$\mathbf A$$|$$\text{det}(\mathbf A)$$|
|$$\text{det}\left(\begin{bmatrix}a&b\\c&d\end{bmatrix}\right)$$|$$ad-bc$$|
|$$\text{det}\left(\begin{bmatrix}a&b&c\\d&e&f\\g&h&i\end{bmatrix}\right)$$|$$({\color{red}aei}+{\color{blue}bfg}+{\color{green}cdh})-({\color{red}ceg}+{\color{blue}afh}+{\color{green}bdi})$$<br>$$\left[\begin{array}{ccc:cc}\color{red}{a}&\color{blue}{b}&\color{green}{c}&a&b\\d&\color{red}{e}&\color{blue}{f}&\color{green}{d}&e\\g&h&\color{red}{i}&\color{blue}{g}&\color{green}{h}\end{array}\right]-\left[\begin{array}{ccc:cc}a&b&\color{red}{c}&\color{blue}{a}&\color{green}{b}\\d&\color{red}{e}&\color{blue}{f}&\color{green}{d}&e\\\color{red}{g}&\color{blue}{h}&\color{green}{i}&g&h\end{array}\right]$$|
|$$2\times 2$$ matrix $$\mathbf A$$ is strictly convex|$$\begin{cases}\text{tr}(\mathbf A)\lt0\\\text{det}(\mathbf A)\gt0\end{cases}$$|
