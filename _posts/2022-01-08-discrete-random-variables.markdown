---
layout: post
title: "Discrete Random Variables"
---

$$\newcommand{\ind}{\perp\kern-5pt\perp}$$

## Definition {#definition}

A random variable (r.v.) $$X$$ is a function that associates a value with every possible outcome $$\omega\in\Omega$$. A random variable $$X(\omega)=x$$ can map into discrete (e.g. $$x\in\mathbb Z$$) or continuous (e.g. $$x\in\mathbb R$$) values. There could be multiple r.v. associated with the same sample space; and a function of one or more r.v. is in turn a r.v.{% if jekyll.environment == "development" %} (see [Prob L5 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab3) and [Prob L5 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab6)){% endif %}.

Probability mass function (PMF) $$p_X(x)$$, on the other hand, is a function that associates a real number to every possible outcome $$\omega\in\Omega$$. Or, more formally, $$p_X(x)=\mathbb P(\omega\in\Omega: X(\omega)=x)$$. Usual [axioms](/2022/01/03/probability-models-and-axioms.html#axioms) apply:

- $$p_X(x)\ge0$$, non negativity
- $$\sum_x p_X(x)=1$$, normalization

## Expectation {#expectation}

Expected value of $$X$$ is defined as $$\mu_X=\mathbb E[X]=\sum_x xp_X(x)$${% if jekyll.environment == "development" %} (see [Prob L5 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab15) and [PS4 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab6)){% endif %} and it can be interpreted as the [arithmetic mean](https://en.wikipedia.org/wiki/Arithmetic_mean) (referred by some as "*statistical hammer*") of a large number of [independent](/2022/01/05/conditioning-and-independence.html#independence) realizations. For infinite sums, expectation needs to be [well defined](https://en.wikipedia.org/wiki/Well-defined_expression) (read unambiguous, especially if $$X$$ can also take negative numbers), hence we assume that $$\sum_x \lvert x\rvert p_X(x)<\infty$$.

|Property|Formula|
|-|:-:|
|Bounds|$$a\le X\le b\implies a\le\mathbb E[X]\le b$$|
|Non negativity|$$X\ge0\implies\mathbb E[X]\ge0$$|
|Non negativity, with $$X\in\{0,1,\dots,\infty\}$$|$$\displaystyle\mathbb E[X]=\sum_{k=0}^\infty\mathbb P(X>k)$$|
|[Law Of The Unconscious Statistician](https://en.wikipedia.org/wiki/Law_of_the_unconscious_statistician) (LOTUS)|$$\displaystyle\mathbb E[g(X)]=\sum_x g(x)p_X(x)$${% if jekyll.environment == "development" %}<br>(see [Prob L5 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab19)){% endif %}|
|Indicator, $$\mathbb 1_A=\begin{cases}1&\text{event $A$ occurs}\\0&\text{otherwise}\end{cases}$$|$$\mathbb E[\mathbb 1_A]=\mathbb P(A)$$|
|Linearity|$$E[aX+b]=a\mathbb E[X]+b$${% if jekyll.environment == "development" %}<br>(see [Prob L5 Q21](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab21), [Prob L6 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab17) and [Prob L6 Q18](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab18)){% endif %}|

Observe that where $$\mathbb 1_{A\cap B}=\mathbb 1_A\cdot\mathbb 1_B\in\{0,1\}$$ is still an indicator r.v., $$\mathbb 1_A+\mathbb 1_B\in\{0,1,2\}$$ is not{% if jekyll.environment == "development" %} (see [Prob L5 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab8)){% endif %}. In this case, $$\mathbb 1_{A\cup B}=\mathbb 1_A+\mathbb 1_B-\mathbb 1_A\mathbb 1_B$$, given by the [inclusion-exclusion](/2022/01/03/probability-models-and-axioms.html#axioms) formula.

## Variance {#variance}

Defined as $$\sigma_X^2=\text{var}(X)=\mathbb E[(X-\mathbb E[X])^2]$$, variance measures the spread of a PMF and is invariant to location{% if jekyll.environment == "development" %} (see [Prob L6 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab12)){% endif %}. $$\sigma_X=\sqrt{\sigma_X^2}$$ is referred to as standard deviation.

|Property|Formula|
|-|:-:|
|Non negativity (*zero* only for constants)|$$\text{var}(X)\ge0$$|
|Equivalency|$$\text{var}(X)=\mathbb E[X^2]-(\mathbb E[X])^2$${% if jekyll.environment == "development" %}<br>(see [Prob L6 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab8), [Prob PS4 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab5) and [Prob MT1 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch7-s1-tab6)){% endif %}|
|Bounded|$$\displaystyle\text{var}(X)\le\frac{1}{4}(b-a)^2$$, if $$a\le X\le b$$|
|Scaled by the square|$$\text{var}(aX)=a^2\text{var}(X)$$|
|Invariant with respect to location|$$\text{var}(X+b)=\text{var}(X)$$|

From the above, we see that $$(\mathbb E[X])^2\le\mathbb E[X^2]$${% if jekyll.environment == "development" %} (see [Prob L6 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab4)){% endif %}. A more general concept is known as [Jensens's inequality](/2022/02/21/introduction-to-statistics.html#basic). As for the upper bound, intuitively the *maximum* dispersion is when $$X$$ has the same chances of being $$a$$ or $$b$$, or equivalently $$X=a+(b-a)Y$$, where $$Y\sim\text{Ber}(\frac 1 2)$$.

## Basic discrete r.v. distributions {#basic}

|r.v.|PMF<br>$$p_X(x)$$|Expectation<br>$$\mu_X=\mathbb E[X]$$|Variance<br>$$\sigma_X^2=\text{var}(X)$$|
|-|:-:|:-:|:-:|:-:|
|Bernoulli<br>$$\text{Ber}(p)$$|$$\begin{cases}p^x(1-p)^{1-x}&x\in\{0,1\}\\0&\text{otherwise}\end{cases}$$|$$p$$|$$p(1-p)$$|
|Rademacher<br>$$\text{Rad}$$|$$\begin{cases}\frac12&x=1\\\frac12&x=-1\\0&\text{otherwise}\end{cases}$$|$$0$$|$$1$$|
|Binomial<br>$$\text{Bin}(k,p)$$|$$\begin{cases}\displaystyle{k\choose x}p^x(1-p)^{k-x}&x\in\{0,1,\dots,k\}\\0&\text{otherwise}\end{cases}$${% if jekyll.environment == "development" %}<br>(see [Prob L5 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab11)){% endif %}|$$kp$$|$$kp(1-p)$$|
|Geometric<br>$$\text{Geom}(p)$$|$$\begin{cases}(1-p)^{x-1}p&\mathbb Z_{\ge1}\\0&\text{otherwise}\end{cases}$$|$$\displaystyle\frac{1}{p}$${% if jekyll.environment == "development" %}<br>(see [Prob MT1 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Exam_1/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch7-s1-tab4)){% endif %}|$$\displaystyle\frac{1-p}{p^2}$$|
|Pascal<br>$$\text{NBin}(k,p)$$|$$\begin{cases}\displaystyle{x-1\choose k-1}p^k(1-p)^{x-k}&\mathbb Z_{\ge k}\\0&\text{otherwise}\end{cases}$$|$$\displaystyle k\frac{1}{p}$$|$$\displaystyle k\frac{(1-p)}{p^2}$$|
|Poisson<br>$$\displaystyle\text{Pois}(\lambda)$$|$$\begin{cases}e^{-\lambda}\displaystyle\frac{\lambda^x}{x!}&\mathbb Z_{\ge0}\\0&\text{otherwise}\end{cases}$$|$$\lambda$$|$$\lambda$$|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\begin{cases}\displaystyle\frac{1}{n}&x\in\{a,a+1,\dots,b-1,b\}\\0&\text{otherwise}\end{cases}$$<br>where $$n=b-a+1$$|$$\displaystyle\frac{a+b}{2}$$|$$\displaystyle\frac{1}{12}(n^2-1)$$|
|Constant<br>$$\text{Unif}(c,c)$$|$$\begin{cases}1&\text{if $x=c$}\\0&\text{otherwise}\end{cases}$$|$$c$$|$$0$$|

Note that $$\mathbb E[X^2]\text{var}(X)+(\mathbb E[X])^2=\sigma_X^2+\mu_X^2$$. Also, observe that for $$X\sim\text{Ber}(p)$$, $$\mathbb E[X^k]=p$$, $$\forall k\ge1$$, while for $$X\sim\text{Rad}$$ we have that $$\mathbb E[X^k]$$ is equal to $$0$$ if $$k$$ is odd, and $$1$$ if $$k$$ is even.

Computing expectation and variance for Pascal r.v. (a.k.a. Negative Binomial) is easier if we [assume](/2022/02/08/bernoulli-and-poisson-processes.html#kth_arrival) $$X=\sum_{i=1}^k X_i$$, with $$X_i\sim\text{Geom}(p)$$, in which case $$\mathbb E[X]=k\mathbb E[X_i]$$ and $$\text{var}(X)=k\text{var}(X_i)$$.

Refer to [back-up](/2022/01/08/discrete-random-variables.html#cdf) for CDF of the above basic distributions and if you are curious about distributions and want to experiment with various parameters, check out this [great resource](https://share.streamlit.io/kaykozaronek/distributed/main/app.py) built by a fellow edX learner!

## Conditioning {#conditioning}

Conditioning to an event $$A$$, with $$\mathbb P(A)>0$$, does not alter the main PMF and expectation properties. Note that conditioning could also include another discrete r.v., e.g. $$A=\{Y=y\}$${% if jekyll.environment == "development" %} (see [Prob PS4 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab4)){% endif %}.

|Property|Conditional on event $$A$$|Conditional on r.v. $$Y$$|
|-|:-:|:-:|
|PMF|$$\displaystyle p_{X\lvert A}(x)=\frac{\mathbb P(X=x \cap A)}{\mathbb P(A)}$$<br>$$\displaystyle p_{X\lvert X\in A}(x)=\begin{cases}\frac{p_X(x)}{\mathbb P(A)}&\text{if $x\in A$}\\0&\text{otherwise}\end{cases}$$|$$\displaystyle p_{X\lvert Y}(x\lvert y)=\frac{p_{X,Y}(x,y)}{p_Y(y)}$${% if jekyll.environment == "development" %}<br>(see [Prob L7 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab3)){% endif %}|
|Normalization|$$\displaystyle\sum_x p_{X\lvert A}(x)=1$$|$$\displaystyle\sum_x p_{X\lvert Y}(x\lvert y)=1$$|
|Expectation|$$\displaystyle\mathbb E[X\lvert A]=\sum_x xp_{X\lvert A}(x)$$|$$\displaystyle\mathbb E[X\lvert Y=y]=\sum_x xp_{X\lvert Y}(x\lvert y)$$|
|LOTUS|$$\displaystyle\mathbb E[g(X)\lvert A]=\sum_x g(x)p_{X\lvert A}(x)$$|$$\displaystyle\mathbb E[g(X)\lvert Y=y]=\sum_x g(x)p_{X\lvert Y}(x\lvert y)$$|
|[Total probability](2022-01-05-conditioning-and-independence.markdown#main_three_tools)|$$\displaystyle p_X(x)=\sum_{i=1}^n\mathbb P(A_i)\mathbb P(X\lvert A_i)$$|$$\displaystyle p_X(x)=\sum_y p_Y(y)p_{X\lvert Y}(x\lvert y)$$|
|Total expectation|$$\displaystyle\mathbb  E[X]=\sum_{i=1}^n\mathbb P(A_i)\mathbb E[X\lvert A_i]$${% if jekyll.environment == "development" %}<br>(see [Prob L6 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab11)){% endif %}|$$\displaystyle\mathbb E[X]=\sum_y p_Y(y)\mathbb E[X\lvert Y=y]$${% if jekyll.environment == "development" %}<br>(see [Prob L6 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab15)){% endif %}|

Notice that $$\mathbb E[g(X,Y)\lvert Y=y']=\sum_x g(x,y')p_{X\lvert Y}(x\lvert y')=\sum_x\sum_y g(x,y)p_{X,Y\lvert Y}(x,y\lvert y')$$ because $$p_{X,Y\lvert Y}(x,y\lvert y')=0$$ for any $$y\neq y'$${% if jekyll.environment == "development" %} (see [Prob L7 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab5)){% endif %}.

## Independence {#independence}

According to [independence](/2022/01/05/conditioning-and-independence.html#independence) of two events, $$X\ind A$$ if $$p_{X\lvert A}(x)=p_X(x)\mathbb P(A), \forall x$${% if jekyll.environment == "development" %} (see [Prob PS4 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab1)){% endif %}. Similarly, $$X\ind Y$$ if $$p_{X,Y}(x,y)=p_X(x)p_Y(y), \forall x,y$${% if jekyll.environment == "development" %} (see [Prob L7 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab8)){% endif %}. Therefore, if $$X\ind Y$$ then we have as follows.

|Property|Formula|
|-|:-:|
|Expectations|$$\mathbb E[XY]=\mathbb E[X]\mathbb E[Y]$${% if jekyll.environment == "development" %} (see [Prob L7 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab15)){% endif %}|
|Independence of functions|$$\mathbb E[g(X)h(Y)]=\mathbb E[g(X)]\mathbb E[h(Y)]$${% if jekyll.environment == "development" %} (see [Prob L7 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab11)){% endif %}|
|Sum of independent r.v.|$$\text{var}(aX+bY)=a^2\text{var}(X)+b^2\text{var}(Y)$${% if jekyll.environment == "development" %}<br>(see [Prob L6 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab3), [Prob L6 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab6) and [Prob L7 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab13)){% endif %}|

Sometimes, independence may involve more than two variables, in such case we should always bear in mind that if certain variables are inter-dependent (say $$X$$ and $$Y$$) but independent from others (say $$Z$$), then $$p_{X,Y,Z}(x,y,z)=p_{X,Y}(x,y)p_Z(z)\neq p_X(x)p_Y(y)p_Z(z)$${% if jekyll.environment == "development" %} (see [Prob L7 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__7_Conditioning_on_a_random_variable__Independence_of_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s4-tab7)){% endif %}.

## Memorylessness {#memorylessness}

Geometric distribution has a remarkable property. Assuming it models coin tosses until it results in a head, every time we toss the coin $$\mathbb P(H)=p$$ is constant and independent from previous steps. In other words, given that initial $$k$$ tosses of a coin were all tails, the probability of having a head in subsequent $$x-k$$ tosses is as if the first $$k$$ tosses never occurred, or $$\mathbb P(X\lvert X>k)=\mathbb P(X-k)$$. Replacing $$k=1$$ we obtain the following relationships:

$$\begin{align}
\mathbb E[X\lvert X>1]&=\mathbb E[1+X]\\
\mathbb E[X^2\lvert X>1]&=\mathbb E[(1+X)^2]
\end{align}$$

Alternative way to derive the above is by thinking that $$\mathbb P(X> k)=(1-p)^{k}$$, and since each toss is independent the conditioned probability will be derived by dividing the probability by $$(1-p)^{k}$${% if jekyll.environment == "development" %} (see [Prob L5 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab13)){% endif %}. 

## Joint PMF {#joint_pmf}

Taking two discrete r.v., each having its own *marginal* distribution, say $$p_X(x)=\mathbb P(X=x)$$ and $$p_Y(y)=\mathbb P(Y=y)$$, their *joint* distribution is defined as $$p_{X,Y}(x,y)=\mathbb P(X=x\cap Y=y)$$. *Marginal* distributions can be derived again from the *joint* distribution as $$p_X(x)=\sum_y p_{X,Y}(x,y)$$ and $$p_Y(y)=\sum_x p_{X,Y}(x,y)$${% if jekyll.environment == "development" %} (see [Prob L6 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab14)){% endif %}.

|Property|Formula|
|-|:-:|
|Non negativity|$$p_{X,Y}(x,y)\ge0$$|
|Normalization|$$\sum_x\sum_y p_{X,Y}(x,y)=1$${% if jekyll.environment == "development" %} (see [Prob L6 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__6_Variance__Conditioning_on_an_event__Multiple_r_v_s/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s3-tab14)){% endif %}|
|Probability of event $$A$$|$$\displaystyle\mathbb P((x,y)\in A)=\sum_{(x,y)\in A}p_{X,Y}(x,y)$$|

Given $$Z=g(X,Y)$$, we have $$p_Z(z)=\mathbb P(g(x,y)=z)=\sum_{(x,y):g(x,y)=z}p_{X,Y}(x,y)$${% if jekyll.environment == "development" %} (see [Prob L5 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab5), [Prob L5 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__5_Probability_mass_functions_and_expectations/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s2-tab17) and [Prob PS4 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab2)){% endif %}. Accordingly, $$\mathbb E[Z]=\mathbb E[g(X,Y)]=\sum_x\sum_y g(x,y)p_{X,Y}(x,y)$${% if jekyll.environment == "development" %} (see [Prob PS4 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_4/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch6-s7-tab3)){% endif %}. Due to liearity, if $$g(X,Y)=aX+bY$$ then $$\mathbb E[g(X,Y)]=g(\mathbb E[X],\mathbb E[Y])=a\mathbb E[X]+b\mathbb E[Y]$$.

Quite often, we need to model joint probability of *independent and identically distributed* (i.i.d.) r.v., such as $$X_i\overset{i.i.d.}{\sim}\mathcal P$$. In such case, the joint PMF $$p_{X_1,\dots X_n}(x_1,\dots,x_n)=\prod_{i=1}^n p_{X_i}(x_i)$$.

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
|$$\displaystyle\sum_{k=1}^nk^2$$|$$\displaystyle\frac{k(k+1)(2k+1)}{6}$$|
|$$\displaystyle\sum_{k=0}^\infty\frac{\lambda^k}{k!}$$|$$e^\lambda$${% if jekyll.environment == "development" %}<br>(see [Stats HW0 Q2](https://learning.edx.org/course/course-v1:MITx+18.6501x+2T2021/block-v1:MITx+18.6501x+2T2021+type@sequential+block@prob_linalg_diag/block-v1:MITx+18.6501x+2T2021+type@vertical+block@prob_linalg_diag-tab2)){% endif %}|
|$$(X_1+\dots+X_n)^2$$|$$\displaystyle\underbrace{\sum_{i=1}^n X^2}_\text{$n$ terms}+\underbrace{\sum_{i\neq j}X_iX_j}_\text{$n^2-n$ terms}$$|

### CDF of basic discrete r.v. distributions {#cdf}

|r.v.|CDF<br>$$F_X(x)$$|
|-|:-:|
|Bernoulli<br>$$\text{Ber}(p)$$|$$\begin{cases}0&x\lt 0\\1-p&0\le x\lt1\\1& x\ge 1\end{cases}$$|
|Binomial<br>$$\text{Bin}(k,p)$$|$$\begin{cases}0&x\lt 0\\\displaystyle\sum_{k=0}^{\lfloor x\rfloor}{k\choose x}p^x(1-p)^{k-x}&0\le x\lt k\\1& x\ge k\end{cases}$$|
|Uniform<br>$$\text{Unif}(a,b)$$|$$\begin{cases}0&x\lt a\\\displaystyle\frac{\lfloor x\rfloor-a+1}{n}&a\le x\lt b\\1& x\ge b\end{cases}$$<br>where $$n=b-a+1$$|
|Constant<br>$$\text{Unif}(c,c)$$|$$\begin{cases}0&x\lt c\\1& x\ge c\end{cases}$$|
|Geometric<br>$$\text{Geom}(p)$$|$$\begin{cases}0&x\lt 1\\\displaystyle 1-(1-p)^{\lfloor x\rfloor}&x\ge1\end{cases}$$|
|Pascal<br>$$\text{NBin}(k,p)$$|$$\begin{cases}0&x\lt 0\\\displaystyle\sum_{n=k}^{\lfloor x\rfloor}{n-1\choose k-1}p^k(1-p)^{n-k}&x\ge0\end{cases}$$|
|Poisson<br>$$\displaystyle\text{Pois}(\lambda)$$|$$\begin{cases}0&x\lt 0\\\displaystyle e^{-\lambda}\sum_{k=0}^{\lfloor x\rfloor}\frac{\lambda^k}{k!}&x\ge0\end{cases}$$|