---
layout: post
title: "Discrete Random Variables"
---

## Definition {#definition}

A random variable (RV) $$X$$ is a function that associates a value with every possible outcome $$\omega\in\Omega$$. A random variable $$X(\omega)=x$$ can map into discrete (e.g. $$x\in\mathbb Z$$) or continuous (e.g. $$x\in\mathbb R$$) values. There could be multiple RV associated with the same sample space; and a function of one or more RV is in turn a RV{% if jekyll.environment == "development" %} (see [L5 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab3) and [L5 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab6)){% endif %}.

Probability mass function (PMF) $$p_X(x)$$, on the other hand, is a function that associates a real number to every possible outcome $$\omega\in\Omega$$. Or, more formally, $$p_X(x)=\mathbb P(\omega\in\Omega: X(\omega)=x)$$. Usual [axioms](/2022/01/03/probability-models-and-axioms.html#axioms) apply:

- $$p_X(x)\ge0$$, non negativity
- $$\sum_x p_X(x)=1$$, normalization

## Expectation {#expectation}

Expected value of $$X$$ is defined as $$\mu_X=\mathbb E[X]=\sum_x xp_X(x)$${% if jekyll.environment == "development" %} (see [L5 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab15) and [PS4 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab6)){% endif %} and it can be interpreted as the [arithmetic mean](https://en.wikipedia.org/wiki/Arithmetic_mean) (referred by some as "*statistical hammer*") of a large number of [independent](/2022/01/05/conditioning-and-independence.html#independence) realizations. For infinite sums, expectation needs to be [well defined](https://en.wikipedia.org/wiki/Well-defined_expression) (read unambiguous, especially if $$X$$ can also take negative numbers), hence we assume that $$\sum_x \lvert x\rvert p_X(x)<\infty$$.

|Property|Formula|
|-|:-:|
|Bounds|$$a\le X\le b\implies a\le\mathbb E[X]\le b$$|
|Non negativity|$$X\ge0\implies\mathbb E[X]\ge0$$|
|Non negativity, with $$X\in\{0,1,\dots,\infty\}$$|$$\displaystyle\mathbb E[X]=\sum_{k=0}^\infty\mathbb P(X>k)$$|
|[Law Of The Unconscious Statistician](https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician) (LOTUS)|$$\displaystyle\mathbb E[g(X)]=\sum_x g(x)p_X(x)$${% if jekyll.environment == "development" %}<br>(see [L5 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab19)){% endif %}|
|Indicator, $$g(X)=\begin{cases}1&\text{$A$ occurs}\\0&\text{otherwise}\end{cases}$$|$$\mathbb E[I_A]=\mathbb P(A)$$|
|Linearity|$$E[aX+b]=a\mathbb E[X]+b$${% if jekyll.environment == "development" %}<br>(see [L5 Q21](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab21), [L6 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab17) and [L6 Q18](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab18)){% endif %}|

Observe that where $$I_{A\cap B}=I_A\cdot I_B\in\{0,1\}$$ is still an indicator RV, $$I=I_A+I_B\in\{0,1,2\}$$ is not{% if jekyll.environment == "development" %} (see [L5 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab8)){% endif %}. In this case, $$I_{A\cup B}=I_A+I_B-I_AI_B$$, given by the [inclusion-exclusion](/2022/01/03/probability-models-and-axioms.html#axioms) formula.

## Variance {#variance}

Defined as $$\sigma_X^2=\text{var}(X)=\mathbb E[(X-\mathbb E[X])^2]$$, variance measures the spread of a PMF and is invariant to location{% if jekyll.environment == "development" %} (see [L6 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab12)){% endif %}. $$\sigma_X=\sqrt{\sigma_X^2}$$ is referred to as standard deviation.

|Property|Formula|
|-|:-:|
|Non negativity (*zero* only for constants)|$$\text{var}(X)\ge0$$|
|Upper bound|$$a\le X\le b$$, $$\displaystyle\text{var}(X)\le\frac{(b-a)^2}{4}$${% if jekyll.environment == "development" %}<br> (see [PS5 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_5/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch8-s7-tab5)){% endif %}|
|Equivalency|$$\text{var}(X)=\mathbb E[X^2]-(\mathbb E[X])^2$${% if jekyll.environment == "development" %}<br>(see [L6 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab8) and [PS4 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab5)){% endif %}|

Variance is always non negative, therefore $$\mathbb E[X^2]\ge\mathbb (E[X])^2$$ is always true{% if jekyll.environment == "development" %} (see [L6 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab4)){% endif %}. In general, for any convex function $$g(x)$$, we have that $$g(\mathbb E[X])\le\mathbb E[g(X)]$$. This is known as [Jensen's Inequality](https://en.wikipedia.org/wiki/Jensen%27s_inequality).

## Basic discrete RV distributions {#basic_discrete_distributions}

|RV|PMF<br>$$p_X(x)$$|Expectation<br>$$\mu_X=\mathbb E[X]$$|Variance<br>$$\sigma_X^2=\text{var}(X)$$|
|-|:-:|:-:|:-:|:-:|
|Bernoulli<br>$$\text{Bin}(1,p)$$|$$\begin{cases}p^x(1-p)^{1-x}&x\in\{0,1\}\\0&\text{otherwise}\end{cases}$$|$$p$$|$$p(1-p)$$|
|Binomial<br>$$\text{Bin}(n,p)$$|$$\begin{cases}\displaystyle{n\choose x}p^x(1-p)^{n-x}&x\in\mathbb Z_{\ge0}\\0&\text{otherwise}\end{cases}$${% if jekyll.environment == "development" %}<br>(see [L5 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab11)){% endif %}|$$np$$|$$np(1-p)$$|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\begin{cases}\displaystyle\frac{1}{n+1}&a\le x\le b\\0&\text{otherwise}\end{cases}$$<br>for simplicity, $$n=b-a$$|$$\displaystyle a+\frac{n}{2}$$|$$\displaystyle\frac{1}{12}n(n+2)$$|
|Constant<br>$$\text{Unif}(c,c)$$|$$\begin{cases}1&\text{if $x=c$}\\0&\text{otherwise}\end{cases}$$|$$c$$|$$0$$|
|Geometric<br>$$\text{Geom}(p)$$|$$\begin{cases}(1-p)^{x-1}p&x\in\mathbb Z_{\ge1}\\0&\text{otherwise}\end{cases}$$|$$\displaystyle\frac{1}{p}$$|$$\displaystyle\frac{1-p}{p^2}$$|
|Pascal<br>$$\text{NBin}(k,p)$$|$$\begin{cases}\displaystyle{x-1\choose k-1}p^k(1-p)^{x-k}&x\in\mathbb Z_{\ge k}\\0&\text{otherwise}\end{cases}$$|$$\displaystyle k\frac{1}{p}$$|$$\displaystyle k\frac{(1-p)}{p^2}$$|
|Poisson<br>$$\displaystyle\text{Pois}(\lambda)$$|$$\begin{cases}e^{-\lambda}\displaystyle\frac{\lambda^k}{k!}&k\in\mathbb Z_{\ge0}\\0&\text{otherwise}\end{cases}$$|$$\lambda$$|$$\lambda$$|

Second moment of $$X$$ can be derived as $$\mathbb E[X^2]=\text{var}(X)+(\mathbb E[X])^2=\sigma_X^2+\mu_X^2$$.

Computing expectation and variance for Pascal RV (a.k.a. negative binomial), is easier if we [assume](/2022/02/08/bernoulli-and-poisson-processes.html#kth_arrival) $$X=\sum_{i=1}^k X_i$$, with $$X_i\sim\text{Geom}(p)$$, in which case $$\mathbb E[X]=k\mathbb E[X_i]$$ and $$\text{var}(X)=k\text{var}(X_i)$$.

As for Poisson RV, its PMF can be computed as Binomial with $$n\rightarrow\infty$$ and $$\lambda=np$$.

$$\displaystyle p_X(k)=\lim_{n\rightarrow\infty}{n\choose k}\left(\frac{\lambda}{n}\right)^k\left(1-\frac{\lambda}{n}\right)^{n-k}=e^{-\lambda}\frac{\lambda^k}{k!}$$

Accordingly, derivation of $$\mathbb E[X]=np=\lambda$$ and $$\text{var}(X)=np(1-p)=\lambda-\frac{\lambda^2}{n}\approx\lambda$$ is immediate.

If you are curious about distributions and want to experiment with various parameters, check out this [great resource](https://share.streamlit.io/kaykozaronek/distributed/main/app.py) built by a fellow edX learner!

## Conditioning {#conditioning}

Conditioning to an event $$A$$, with $$\mathbb P(A)>0$$, does not alter the main PMF and expectation properties. Note that conditioning could also include another discrete RV, e.g. $$A=\{Y=y\}$${% if jekyll.environment == "development" %} (see [PS4 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab4)){% endif %}.

|Property|Conditional on event $$A$$|Conditional on RV $$Y$$|
|-|:-:|:-:|
|PMF|$$\displaystyle p_{X\lvert A}(x)=\frac{\mathbb P(X=x \cap A)}{\mathbb P(A)}$$<br>$$\displaystyle p_{X\lvert X\in A}(x)=\begin{cases}\frac{p_X(x)}{\mathbb P(A)}&\text{if $x\in A$}\\0&\text{otherwise}\end{cases}$$|$$\displaystyle p_{X\lvert Y}(x\lvert y)=\frac{p_{X,Y}(x,y)}{p_Y(y)}$${% if jekyll.environment == "development" %}<br>(see [L7 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab3)){% endif %}|
|Normalization|$$\displaystyle\sum_x p_{X\lvert A}(x)=1$$|$$\displaystyle\sum_x p_{X\lvert Y}(x\lvert y)=1$$|
|Expectation|$$\displaystyle\mathbb E[X\lvert A]=\sum_x xp_{X\lvert A}(x)$$|$$\displaystyle\mathbb E[X\lvert Y=y]=\sum_x xp_{X\lvert Y}(x\lvert y)$$|
|LOTUS|$$\displaystyle\mathbb E[g(X)\lvert A]=\sum_x g(x)p_{X\lvert A}(x)$$|$$\displaystyle\mathbb E[g(X)\lvert Y=y]=\sum_x g(x)p_{X\lvert Y}(x\lvert y)$$|
|[Total probability](2022-01-05-conditioning-and-independence.markdown#main_three_tools)|$$\displaystyle p_X(x)=\sum_{i=1}^n\mathbb P(A_i)\mathbb P(X\lvert A_i)$$|$$\displaystyle p_X(x)=\sum_y p_Y(y)p_{X\lvert Y}(x\lvert y)$$|
|Total expectation|$$\displaystyle\mathbb  E[X]=\sum_{i=1}^n\mathbb P(A_i)\mathbb E[X\lvert A_i]$${% if jekyll.environment == "development" %}<br>(see [L6 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab11)){% endif %}|$$\displaystyle\mathbb E[X]=\sum_y p_Y(y)\mathbb E[X\lvert Y=y]$${% if jekyll.environment == "development" %}<br>(see [L6 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab15)){% endif %}|

Notice that $$\mathbb E[g(X,Y)\lvert Y=y']=\sum_x g(x,y')p_{X\lvert Y}(x\lvert y')=\sum_x\sum_y g(x,y)p_{X,Y\lvert Y}(x,y\lvert y')$$ because $$p_{X,Y\lvert Y}(x,y\lvert y')=0$$ for any $$y\neq y'$${% if jekyll.environment == "development" %} (see [L7 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab5)){% endif %}.

## Independence {#independence}

According to [independence](/2022/01/05/conditioning-and-independence.html#independence) of two events, $$X$$ is independent from $$A$$ if $$p_{X\lvert A}(x)=p_X(x)\mathbb P(A), \forall x$${% if jekyll.environment == "development" %} (see [PS4 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab1)){% endif %}. Similarly, $$X$$ is independent from $$Y$$ if $$p_{X,Y}(x,y)=p_X(x)p_Y(y), \forall x,y$${% if jekyll.environment == "development" %} (see [L7 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab8)){% endif %}. In such case, below properties hold.

|Property|Formula|
|-|:-:|
|Expectations|$$\mathbb E[XY]=\mathbb E[X]\mathbb E[Y]$${% if jekyll.environment == "development" %} (see [L7 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab15)){% endif %}|
|Independence of functions|$$\mathbb E[g(X)h(Y)]=\mathbb E[g(X)]\mathbb E[h(Y)]$${% if jekyll.environment == "development" %} (see [L7 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab11)){% endif %}|
|Sum of independent RV|$$\text{var}(aX+bY)=a^2\text{var}(X)+b^2\text{var}(Y)$${% if jekyll.environment == "development" %}<br>(see [L6 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab3), [L6 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab6) and [L7 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab13)){% endif %}|

Sometimes, independence may involve more than two variables, in such case we should always bear in mind that if certain variables are inter-dependent (say $$X$$ and $$Y$$) but independent from others (say $$Z$$), then $$p_{X,Y,Z}(x,y,z)=p_{X,Y}(x,y)p_Z(z)\neq p_X(x)p_Y(y)p_Z(z)$${% if jekyll.environment == "development" %} (see [L7 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab7)){% endif %}.

## Memorylessness {#memorylessness}

Geometric distribution has a remarkable property. Assuming it models coin tosses until it results in a head, every time we toss the coin $$\mathbb P(H)=p$$ is constant and independent from previous steps. In other words, given that initial $$k$$ tosses of a coin were all tails, the probability of having a head in subsequent $$x-k$$ tosses is as if the first $$k$$ tosses never occurred, or $$\mathbb P(X\lvert X>k)=\mathbb P(X-k)$$. Replacing $$k=1$$ we obtain the following relationships:

$$\begin{align}
\mathbb E[X\lvert X>1]&=\mathbb E[1+X]\\
\mathbb E[X^2\lvert X>1]&=\mathbb E[(1+X)^2]
\end{align}$$

Alternative way to derive the above is by thinking that $$\mathbb P(X> k)=(1-p)^{k}$$, and since each toss is independent the conditioned probability will be derived by dividing the probability by $$(1-p)^{k}$${% if jekyll.environment == "development" %} (see [L5 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab13)){% endif %}. 

## Joint PMFs {#joint_pmfs}

Taking two discrete RV, each having its own *marginal* distribution, say $$p_X(x)=\mathbb P(X=x)$$ and $$p_Y(y)=\mathbb P(Y=y)$$, their *joint* distribution is defined as $$p_{X,Y}(x,y)=\mathbb P(X=x\cap Y=y)$$. *Marginal* distributions can be derived again from the *joint* distribution as $$p_X(x)=\sum_y p_{X,Y}(x,y)$$ and $$p_Y(y)=\sum_x p_{X,Y}(x,y)$${% if jekyll.environment == "development" %} (see [L6 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab14)){% endif %}.

|Property|Formula|
|-|:-:|
|Non negativity|$$p_{X,Y}(x,y)\ge0$$|
|Normalization|$$\sum_x\sum_y p_{X,Y}(x,y)=1$${% if jekyll.environment == "development" %} (see [L6 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab14)){% endif %}|
|Probability of event $$A$$|$$\displaystyle\mathbb P((x,y)\in A)=\sum_{(x,y)\in A}p_{X,Y}(x,y)$$|

Given $$Z=g(X,Y)$$, we have $$p_Z(z)=\mathbb P(g(x,y)=z)=\sum_{(x,y):g(x,y)=z}p_{X,Y}(x,y)$${% if jekyll.environment == "development" %} (see [L5 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab5), [L5 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab17) and [PS4 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab2)){% endif %}. Accordingly, $$\mathbb E[Z]=\mathbb E[g(X,Y)]=\sum_x\sum_y g(x,y)p_{X,Y}(x,y)$${% if jekyll.environment == "development" %} (see [PS4 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab3)){% endif %}. Due to liearity, if $$g(X,Y)=aX+bY$$ then $$\mathbb E[g(X,Y)]=g(\mathbb E[X],\mathbb E[Y])=a\mathbb E[X]+b\mathbb E[Y]$$.

Quite often, we need to model joint probability of *independent and identically distributed* (iid) RV, such as $$X_i\overset{iid}{\sim}\mathcal P$$. In such case, the joint PMF $$p_{X_1,\dots X_n}(x_1,\dots,x_n)=\prod_{i=1}^n p_{X_i}(x_i)$$.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

In deriving the various relations, it may be useful bearing in mind the following relations.

|Formula|Equivalent form|
|:-:|:-:|
|$$\displaystyle s_n=\sum_{i=1}^n a_i$$|$$s_n=n\bar a$$, with $$\displaystyle\bar a=\frac{1}{n}\sum_{i=1}^n a_i$$ arithmetic mean|
|$$\displaystyle s_n=\prod_{i=1}^n a_i$$|$$s_n={\bar a}^n$$, with $$\displaystyle\bar a=\sqrt[n]{\prod_{i=1}^n a_i}$$ geometric mean|
|$$\displaystyle s_n=\sum_{i=1}^n\frac{1}{a_i}$$|$$s_n=\frac{n}{\bar a}$$, with $$\displaystyle\bar a=\frac{n}{\sum_{i=1}^n \frac{1}{a_i}}$$ harmonic mean|
|$$\displaystyle\sum_{k=1}^nk$$|$$\displaystyle\frac{k(k+1)}{2}$$|
|$$\displaystyle\sum_{k=1}^nk$$|$$\displaystyle\frac{k(k+1)(2k+1)}{6}$$|
|$$(X_1+\dots+X_n)^2$$|$$\displaystyle\underbrace{\sum_{i=1}^n X^2}_\text{$n$ terms}+\underbrace{\sum_{i\neq j}X_iX_j}_\text{$n^2-n$ terms}$$|