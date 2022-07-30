---
layout: post
title: "Bernoulli and Poisson Processes"
---

$$\newcommand{\ind}{\perp\!\!\!\perp}$$

## Definition

Considering the many analogies between Bernoulli and Poisson processes, the two will be treated in parallel during this segment.

||Bernoulli|Poisson|
|-|:-:|:-:|
|**Definition**|Sequence of $$X_i\overset{i.i.d.}{\sim}\text{Ber}(p)$${% if jekyll.environment == "development" %}<br>(see [Prob L21 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab3)){% endif %}|Series of discrete events during a continuous interval|
|**Unit time**|slot $$i$$|infinitesimal interval $$\delta$$|
|**Arrival during unit time**|$$p_X(x_i)=\begin{cases}1-p&\text{$x_i=0$}\\p,&\text{$x_i=1$}\end{cases}$$|$$p_X(x,\delta)=\begin{cases}1-\lambda\delta+O(\delta^2)&\text{$x=0$}\\\lambda\delta+O(\delta^2)&\text{$x=1$}\\O(\delta^2)&\text{$x\gt1$}\end{cases}$$|
|**Independence**|$$X_j\ind X_i$$, $$\forall i<j$$|Arrivals occurred in disjoint intervals are independent{% if jekyll.environment == "development" %}<br>(see [Prob L23 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab10), [Prob PS9 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab5) and [Prob F Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab7)){% endif %}|
|**Time homogeneity**|$$p$$ constant at each slot|$$\lambda$$ constant during any interval{% if jekyll.environment == "development" %}<br>(see [Prob L22 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab5)){% endif %}|

## Number of arrivals

|# of arrivals|Bernoulli|Poisson|
|-|:-:|:-:|
|**Definition**|$$\displaystyle X=\sum_{i=1}^n X_i$$, $$X_i\overset{i.i.d.}{\sim}\text{Ber}(p)$$|$$\displaystyle X=\lim_{n\rightarrow\infty}\sum_{i=1}^{\tau/\delta} X_i$$, $$X_i\overset{i.i.d.}{\sim}\text{Ber}(\lambda\delta)$$|
|**Probability law**|$$k$$ arrivals in $$n$$ slots $$\sim\text{Bin}(n,p)$$|$$k$$ arrivals during interval $$\tau$$ $$\sim\text{Pois}(\lambda\tau)$$|

For expectation and variance of the above, refer to the [summary](/2022/01/08/discrete-random-variables.html#basic) of basic discrete r.v., bearing in mind that Poisson PMF can be derived assuming $$np\simeq\lambda\tau$$, obtained from $$p=\lambda\delta+O(\delta^2)$$ and $$n=\frac \tau \delta$$.

As opposed to *slots* in the Bernoulli case, continuous time intervals can be stretched or compressed. We can interpret such cases as a change in the rate $$\lambda$$ or infinitesimal interval $$\delta$$, indifferently{% if jekyll.environment == "development" %} (see [Prob L22 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab3)){% endif %}.

## $$k$$-th arrival {#kth_arrival}

Assuming the same distributions as above for each of Bernoulli and Poisson processes, the distribution of the first arrival $$T_1$$ is as follows.

|First arrival|Bernoulli|Poisson|
|-|:-:|:-:|
|**Definition**|$$\min\{i:X_i=1\}$${% if jekyll.environment == "development" %}<br>(see [Prob L21 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab6)){% endif %}|no arrivals during $$[0,t]$${% if jekyll.environment == "development" %}<br>(see [Prob L23 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab4)){% endif %}|
|**Probability law**|$$T_1\sim\text{Geom}(p)$$|$$T_1\sim\text{Exp}(\lambda)$$|

Earlier summary tables provide for expectations and variances of [Geometric](/2022/01/08/discrete-random-variables.html#basic) and [Exponential](/2022/01/13/continuous-random-variables.html#basic) r.v. Note that $$T_1$$ and any other inter-arrival time $$T_i$$ (i.e. the time elapsed between arrivals $$i-1$$ and $$i$$) have the same distribution. Accordingly, time until $$k$$-th arrival, is a sum of i.i.d. r.v.

|$$k$$-th arrival|Bernoulli|Poisson|
|-|:-:|:-:|
|**Definition**|$$\displaystyle Y_k=\sum_{i=1}^k T_i$$, $$T_i\overset{i.i.d.}{\sim}\text{Geom}(p)$$|$$\displaystyle Y_k=\sum_{i=1}^k T_i$$, $$T_i\overset{i.i.d.}{\sim}\text{Exp}(\lambda)$${% if jekyll.environment == "development" %}<br>(see [Prob L23 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab11)){% endif %}|
|**Probability law**|$$Y_k\sim\text{NBin}(k,p)$${% if jekyll.environment == "development" %}<br>(see [Prob PS9 Q1](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab1) and [Prob PS9 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab4)){% endif %}|$$Y_k\sim\text{Erlang}(k,\lambda)$$|

Refer to the summary tables for basic [discrete](/2022/01/08/discrete-random-variables.html#basic) and [continuous](/2022/01/13/continuous-random-variables.html#basic) r.v. for further detail. Note that Pascal distribution (referred above as $$\text{NBin}(k,p)$$ or Negative Binomial) is ready for use to describe the PMF of failures before $$k$$-th arrival. Think of the $$n$$-th slot when $$k$$-th arrival occurs. Considering that out of those $$n$$ slots, $$k$$ slots are arrivals, it follows that total failures occurred meantime are $$n-k$${% if jekyll.environment == "development" %} (see [Prob PS9 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab3)){% endif %}.

As for Poisson processes, observe that events can be described either in terms of arrivals in a given time interval, or in terms of $$k$$-th arrival time. Assuming $$X(t)$$ indicates the number of arrivals during an interval $$[0,t]$$, the following formulations are equivalent $$\mathbb P(X(t)\ge k)=\mathbb P(Y_k\le t)$${% if jekyll.environment == "development" %} (see [Prob L22 Q12](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab12)){% endif %} or $$\mathbb P(X(t)\lt k)=\mathbb P(Y_k\gt t)$${% if jekyll.environment == "development" %} (see [Prob PS9 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab8)){% endif %}.

Assuming two Pascal r.v., of order $$n$$ and $$m$$ respectively, we notice that their sum is another Pascal r.v. of order $$n+m$$, that is $$Y_n+Y_m=\sum_{i=1}^n T_i+\sum_{i=1}^m T_i=\sum_{i=1}^{n+m} T_i$${% if jekyll.environment == "development" %} (see [Prob L22 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab13)){% endif %}. The fact that Pascal is a sum of i.i.d. Bernoulli r.v. explains why it tends towards a Normal distribution, as its order $$\rightarrow\infty$$. Same considerations apply *mutatis mutandis* to Erlang r.v. (see [CLT](/2022/02/21/introduction-to-statistics.html#clt)){% if jekyll.environment == "development" %} (see [Prob L22 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab14)){% endif %}.

## Memorylessness

Due to their nature, and in particular their reliance on the properties of [Geometric](/2022/01/08/discrete-random-variables.html#memorylessness){% if jekyll.environment == "development" %} (see [Prob L21 Q11](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab11)){% endif %} and [Exponential](/2022/01/13/continuous-random-variables.html#memorylessness) distributions, Bernoulli and Poisson processes benefit from memorylessness{% if jekyll.environment == "development" %} (see [Prob L22 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab17)){% endif %}.

In particular, if we consider a conditional probability of whatever happens after a given moment (either slot $$n$$, or time $$t$$), the process will continue independently of past events and will remain a Bernoulli or Poisson, as the case may be{% if jekyll.environment == "development" %} (see [Prob L21 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab9)){% endif %}. And the probability associated with combination of events occurred in disjoint intervals is a joint probability of independent events{% if jekyll.environment == "development" %} (see [Prob L21 Q9](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab9)){% endif %}.

The main condition is that the moment at which we decide to *fresh-start* is determined *causally*{% if jekyll.environment == "development" %} (see [Prob L21 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab8)){% endif %}, that is based on the events that occurred in the past; otherwise, the independence between preceding and succeeding intervals would not be satisfied, and we will lose the ability to fresh-start a new process.

## Sum, merge and split of processes

For ease of notation, $$\text{merge}(X,Y)$$ indicates a process with arrivals coming from *either* $$X$$ or $$Y$$, and $$\text{split}(Z,q)$$ indicates two processes, with arrivals from $$Z$$, with probabilities $$q$$ and $$1-q$$, respectively.

||Bernoulli|Poisson|
|-|-|-|
|**Sum**|$$X+Y\sim\text{Bin}(n+m,p)$$, where $$X\sim\text{Bin}(n,p)$$ and $$Y\sim\text{Bin}(m,p)$$ are **independent**|$$X+Y\sim\text{Pois}(\lambda(t+s))$${% if jekyll.environment == "development" %} (see [Prob L23 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab3)){% endif %}, where $$X\sim\text{Pois}(\lambda t)$$ and $$Y\sim\text{Pois}(\lambda s)$$ are **independent**|
|**Merge**|If $$X\sim\text{Bin}(n,p)$$ and $$Y\sim\text{Bin}(n,q)$$ are **independent**, a process obtained from the merge of respective arrivals will be distributed according to $$\text{Bin}(n, p+q-pq)$$ (see [union of two events](/2022/01/03/probability-models-and-axioms.html#axioms)){% if jekyll.environment == "development" %} (see [Prob L21 Q14](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab14)){% endif %}, with $$\left(\frac{p}{p+q-pq}\right)$$ being the probability that the arrival in the merged process came from $$X$$|If $$X\sim\text{Pois}(\lambda t)$$ and $$Y\sim\text{Pois}(\mu t)$$ are **independent**, a process obtained from the merge of respective arrivals will be distributed according to $$\text{Pois}((\lambda+\mu)t)$${% if jekyll.environment == "development" %} (see [Prob L23 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab6)){% endif %}, with $$\left(\frac{\lambda}{\lambda+\mu}\right)$$ being the probability that the arrival in the merged process came from $$X$${% if jekyll.environment == "development" %} (see [Prob L23 Q8](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab8)){% endif %}|

CDF of the first arrival of the merged process can also be derived as $$1-\mathbb P(\min\{X,Y\}\ge t)$$. This approach is also useful to determine the distribution of the last arrival as $$\mathbb P(\max\{X,Y\}\le t)$${% if jekyll.environment == "development" %} (see [Prob PS9 Q2](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab2)){% endif %}.

As for the split of events, we consider an input process $$N$$ and two outputs, obtained from the splitting the arrivals in one or the other stream, depending on the variable $$X$$.

|Input<br>$$N$$|Split<br>$$X$$|Output<br>$$M$$|
|:-:|:-:|:-:|
|$$\text{Bin}(n,p)$$|$$\text{Ber}(q)$$|$$\begin{cases}\text{Bin}(n,pq)&X=1\\\text{Bin}(n,p(1-q))&X=0\end{cases}$$<br>streams are **dependent**, as success in one determines failure in the other{% if jekyll.environment == "development" %} (see [Prob L21 Q16](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab16)){% endif %}|
|$$\text{Pois}(\lambda t)$$|$$\text{Ber}(q)$$|$$\begin{cases}\text{Pois}(\lambda t q)&X=1\\\text{Pois}(\lambda t(1-q))&X=0\end{cases}$$<br>streams are **independent**, as success in one does not affect the other, due to interval continuity{% if jekyll.environment == "development" %} (see [Prob L23 Q13](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab13)){% endif %}|

## Random incidence

Random incidence refers to a "*paradox*" of observing a higher than average inter-arrival times, when starting observation *randomly*. Although it can be easier introduced with Poisson processes, it is not specific to Poisson. In particular, it introduces the importance of sampling and the issues that one can encounter when sampling does not reflect the objective of the experiment.

Assume a Poisson process, with $$k$$-th arrival occurring at time $$t_k$$, and inter-arrival times distributed Exponentially. When an observer joins this process at a random time $$t$$, it will observe that intervals $$[t_{k-1},t]$$ and $$[t,t_k]$$ are both distributed Exponentially, due to memorylessness. Accordingly, the inter-arrival time recorded by the observer will be distributed according to $$\text{Erlang}(2,\lambda)$$ (that is, a sum of two i.i.d. Exponential r.v.){% if jekyll.environment == "development" %} (see [Prob L23 Q15](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab15)){% endif %}. Analogously, if the inter-arrival time is distributed according to $$\text{Erlang}(k,\lambda)$$, then the inter-arrival time recorded by the observer will be distributed according to $$\text{Erlang}(k+1,\lambda)$$, where one of the Exponential r.v. has been replaced with two.

In general, assume you have $$n$$ possible intervals, each of duration $$T_n$$ and probability $$p_n$$. The chances that a random observer will see $$n$$-th interval is $$p_N(n)=\frac{T_n p_n}{\sum_n T_n p_n}$$. Accordingly, the expected duration of the intervals seen by a random observer is $$\mathbb E[S]=\sum_n T_n p_N(n)=\frac{\mathbb E[T^2]}{\mathbb E[T]}=\mathbb E[T]+\frac{\text{var}(T)}{E[T]}$${% if jekyll.environment == "development" %} (see [Prob L23 Q17](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab17), [Prob L23 Q19](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab19) and [Prob PS9 Q7](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab7)){% endif %}, which is consistent with $$\mathbb E[S]=\frac{k+1}{\lambda}$$ when $$S\sim\text{Erlang}(k+1,\lambda)$$, derived from an initial $$T\sim\text{Erlang}(k,\lambda)$${% if jekyll.environment == "development" %} (see [Prob PS9 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab6)){% endif %}.

## Poisson vs CLT approximations

We have [seen](/2022/01/08/discrete-random-variables.html#basic) that PMF of $$X=\sum_{i=1}^n X_i$$, where $$X_i\sim\text{Ber}(p)$$ and $$\lambda=np$$, is approximated with $$\text{Pois}(\lambda)$$ as $$n\rightarrow\infty$$. At the same time, [CLT](/2022/02/21/introduction-to-statistics.html#clt_binomial) tells us that a sum of infinite i.i.d. r.v. is approximated by a Normal distribution, which is different from Poisson and one may wonder: "*is there a contradiction?*"

The answer is that in the first case, we maintained the term $$\lambda=np$$ constant, and therefore $$p\rightarrow0$$ as $$n\rightarrow\infty$$. Accordingly, our distribution $$\text{Ber}(p)$$ changed with every increase of $$n$$, which invalidated the assumption that we kept *adding* i.i.d. variables. Depending on the scenario, $$X\sim\text{Bin}(n,p)$$ can be approximated as follows:

- Poisson, if $$\lambda=np$$ is small;
- Normal, if $$\lambda=np$$ is large (e.g. above 30); and
- Poisson or Normal, if $$\lambda=np$$ is large, despite a small $$p$$ which is fully compensated by $$n$$.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).
