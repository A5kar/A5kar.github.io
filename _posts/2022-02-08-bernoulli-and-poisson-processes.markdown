---
layout: post
title: "Bernoulli and Poisson Processes"
---

$$\newcommand{\ind}{\perp\kern-5pt\perp}$$

## Stochastic Processes {#stochastic_processes}

Occasionally referred as a **random process**, stochastic process is a collection of r.v. indexed by some set, usually a subset of a real line. In particular, the process is called either *discrete* or *continuous* if the index set is either integer or continuous.

Discrete processes are easier to study, and their simplest form is a **Bernoulli process**, denoted as $$\{X_i:i=1,\dots,n\}$$, where $$X_i\overset{i.i.d.}{\sim}\text{Ber}(p)$$. To picture the process, imagine a sequence of $$i$$ steps, where at each step we collect an observation from $$\text{Ber}(p)$$. It turns out that the number of stepts to observe the first success is [Geometrically distributed](/2022/02/08/bernoulli-and-poisson-processes.html#arrivals), and that the total occurrence of successes in $$n$$ steps follows a [Binomial distribution](/2022/02/08/bernoulli-and-poisson-processes.html#kth_arrival).

**Poisson process** as an example of continuous process. Note that $$\text{Pois}(\lambda\tau)$$ is a *discrete* r.v. and it describes the distribution of the number of successes within a *continuous* interval $$\tau$$, in the same way as $$\text{Bin}(n,p)$$ describes the number of successes within $$n$$ discrete steps. It turns out that Poisson r.v. is equivalent to a Binomial r.v., if we split a single step into $$n\rightarrow\infty$$ intervals, and provided that the *rate* of success $$\lambda=np$$ remains constant. This means that within every *infinitesimal* interval $$\delta=\frac1n$$ the probability of success is $$p=\frac\lambda n=\lambda\delta$$. Starting from $$X\sim\text{Bin}(n,p)$$, PMF of $$X\sim\text{Pois}(\lambda)$$ can be therefore derived by replacing $$p=\frac\lambda n$$ and observing the limit of $$p_X(k)$$ as $$n\rightarrow\infty$$:

$$\begin{align}
p_X(k)
&=\lim_{n\rightarrow\infty}{n\choose k}p^k(1-p)^{n-k}\\
&=\lim_{n\rightarrow\infty}{n\choose k}\left(\frac\lambda n\right)^k\left(1-\frac\lambda n\right)^{n-k}\\
&=\lim_{n\rightarrow\infty}\frac{n(n-1)\dots(n-k+1)(n-k)!}{k!(n-k)!}\frac{\lambda^k}{n^k}\left(1-\frac\lambda n\right)^n\left(1-\frac\lambda n\right)^{-k}\\
&=\frac{\lambda^k}{k!}\lim_{n\rightarrow\infty}\left(1-\frac\lambda n\right)^n\cancelto{=1}{\lim_{n\rightarrow\infty}\frac{n}n\frac{n-1}n\dots\frac{(n-k+1)}n\left(1-\frac\lambda n\right)^{-k}}\\
&=\frac{\lambda^k}{k!}e^{-\lambda}
\end{align}$$

Bearing in mind the expectation and variance of a [Binomial r.v.](/2022/01/08/discrete-random-variables.html#basic), derivation of $$\mathbb E[X]=np=\lambda$$ and $$\text{var}(X)=np(1-p)=\lambda-\frac{\lambda^2}{n}\rightarrow\lambda$$ is immediate.

An important observation is that Poisson remains a discrete distribution. It still indicates the chances of $$k$$ successes within an interval, and the difference is that where Binomial considered the $$n$$ steps, Poisson considers any continuous interval of the real line. For instance, assume an interval $$t$$ is split into $$n=\frac t\delta$$ slots, and probability of success within each slot is $$p=\mu\delta$$. Accordingly, the number of successes within interval $$t$$ will be distribued according to $$\text{Bin}\left(\frac t\delta,\mu\delta\right)\xrightarrow[\delta\rightarrow0]{}\text{Pois}(\mu t)$$.

## Definition

Considering the many analogies between Bernoulli and Poisson processes, the two will be treated in parallel during this segment.

||Bernoulli|Poisson|
|-|:-:|:-:|
|**Definition**|Sequence of $$X_i\overset{i.i.d.}{\sim}\text{Ber}(p)$${% if jekyll.environment == "development" %}<br>(see [Prob L21 Q3](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab3)){% endif %}|Series of discrete events during a continuous interval|
|**Unit time**|slot $$i$$|infinitesimal interval $$\delta$$|
|**Arrival during unit time**|$$p_X(x_i)=\begin{cases}1-p&\text{$x_i=0$}\\p,&\text{$x_i=1$}\end{cases}$$|$$p_X(x,\delta)=\begin{cases}1-\lambda\delta+O(\delta^2)&\text{$x=0$}\\\lambda\delta+O(\delta^2)&\text{$x=1$}\\O(\delta^2)&\text{$x\gt1$}\end{cases}$$|
|**Independence**|$$X_j\ind X_i$$, $$\forall i<j$$|Arrivals occurred in disjoint intervals are independent{% if jekyll.environment == "development" %}<br>(see [Prob L23 Q10](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab10), [Prob PS9 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Problem_Set_9/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s7-tab5) and [Prob F Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@sequential_Final_Exam/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch16-s1-tab7)){% endif %}|
|**Time homogeneity**|$$p$$ constant at each slot|$$\lambda$$ constant during any interval{% if jekyll.environment == "development" %}<br>(see [Prob L22 Q5](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__22_The_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s3-tab5)){% endif %}|

## Number of arrivals {#arrivals}

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
|**Definition**|$$\min\{T_1:X_{T_1}=1\}$${% if jekyll.environment == "development" %}<br>(see [Prob L21 Q6](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__21_The_Bernoulli_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s2-tab6)){% endif %}|no arrivals during $$[0,T_1]$${% if jekyll.environment == "development" %}<br>(see [Prob L23 Q4](https://learning.edx.org/course/course-v1:MITx+6.431x+1T2020/block-v1:MITx+6.431x+1T2020+type@sequential+block@Lec__23_More_on_the_Poisson_process/block-v1:MITx+6.431x+1T2020+type@vertical+block@ch13-s4-tab4)){% endif %}|
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

- **Poisson**, if $$\lambda=np$$ is small; and
- **Normal**, if $$\lambda=np$$ is large (e.g. above 30), bearing in mind that Poisson approximation is also acceptable if a small $$p$$ is fully compensated by a very large $$n$$.

Go back to the [syllabi breakdown](/2022/01/02/prob-and-stats-syllabi.html).

***

## Back-up

### Standard random walk {#srw}

An important form of [stochastic processes](/2022/02/08/bernoulli-and-poisson-processes.html#stochastic_processes) is a **random walk**, which is usually defined as a path consisting of a succession of i.i.d. random steps.

An elementary form of random walk is a sequence of $$\{X_i\}$$, with $$X_i=2Y_i-1$$ and $$Y_i\overset{i.i.d.}{\sim}\text{Ber}(p)$$. This means that starting from a position $$0$$, at each step we would move $$+1$$ or $$-1$$, with probabilities $$p$$ and $$1-p$$, respectively.

If $$\{X_i\}$$ is a sequence of [Rademacher r.v.](/2022/01/08/discrete-random-variables.html#basic), then the associated process is a form of *symmetric* or *standard* random walk (SRW). After $$n$$ steps, SRW will stop at $$S_n=\sum_{i=1}^n X_i$$, which will have the same distribution as $$2\sum_{i=1}^nY_i-n$$ with $$\sum_{i=1}^nY_i\sim\text{Bin}\left(n,\frac12\right)$$. Therefore, that $$\mathbb E[S_n]=0$$ and $$\text{var}(S_n)=n$$. [CLT](/2022/02/21/introduction-to-statistics.html#clt) tells us that $$\text{Bin}\left(n,\frac12\right)\xrightarrow{(d)}\mathcal N\left(\frac n2,\frac n4\right)$$, hence it follows that $$S_n\xrightarrow{(d)}\mathcal N(0,n)$$. In particular, with proper scaling we obtain $$\frac{S_n}{\sqrt{n}}\xrightarrow{(d)}\mathcal N(0,1)$$.

In the above example, we started splitting a single step. If we start from a continuous interval of length $$t$$ (as we did with the derivation of the [Poisson process](/2022/02/08/bernoulli-and-poisson-processes.html#stochastic_processes)), the derivation would be the same, but we will need to pay attention to the scaling factor because if a *unit* length is made up of $$n$$ intervals $$\delta$$, then an interval of length $$t$$ is made up of $$tn$$ intervals $$\delta$$ and, therefore, the number of $$+1$$ and $$-1$$ that can occur during the random walk are different.

In particular, by defining $$S_{\lfloor nt\rfloor}=\sum_{i=1}^{\lfloor nt\rfloor}X_i$$ one can observe that $$\frac{S_{\lfloor nt\rfloor}}{\sqrt n}$$ is distributed according to a Normal with variance $$t$$.

$$\frac{S_{\lfloor nt\rfloor}}{\sqrt n}=\sqrt t\frac{S_{\lfloor nt\rfloor}}{\sqrt{nt}}\xrightarrow{(d)}\sqrt t\mathcal N(0,1)=\mathcal N(0,t)$$

### Wiener process and Donsker's theorem {#donsker}

Wiener process (often referred to as the Brownian motion) is an important example of a continuous stochastic process. Wiener process has the following properties:

- $$B(0)=0$$;
- $$B(t+u)-B(t)\sim\mathcal N(0,u),\forall u\ge0$$;
- $$B(t+u)-B(t)\ind B(s),\forall s\lt t$$;
- $$B(t)$$ is continuous (but not differentiable) in $$t$$.

Visualizing a Wiener process may be complicated and the good news is that Donsker proved that we can approximate it with a properly rescaled SRW, such as $$W_n(t)=\frac{S_{\lfloor nt\rfloor}}{\sqrt n}$$, as $$W_n(t)\xrightarrow{(d)}B(t)$$.

Without strictly proving the **Donsker's theorem**, a rough idea is provided by proving the convergence of finite-dimension distributions $$\begin{bmatrix}W_n(t_1)\dots W_n(t_m)\end{bmatrix}^T\xrightarrow{(d)}\begin{bmatrix}B(t_1)\dots B(t_m)\end{bmatrix}^T$$, for any possible $$m$$ intermediary points, s.t. $$0\lt t_1\lt\dots\lt t_m$$. Before that observe as follows:

- $$W_n(0)=0$$, which is equivalent to the starting point of any SRW;
- $$W_n(t+u)-W_n(t)\xrightarrow{(d)}\mathcal N(0,u),\forall u\ge0$$, due to the following:

$$\begin{align}
W_n(t+u)-W_n(t)
&=\frac1{\sqrt n}\left(\sum_{i=1}^{\lfloor nt+nu\rfloor}X_i-\sum_{i=1}^{\lfloor nt\rfloor}X_i\right)\\
&=\frac1{\sqrt n}\sum_{i=\lfloor nt\rfloor+1}^{\lfloor nt+nu\rfloor}X_i=\frac{\sqrt u}{\sqrt{nu}}\sum_{i=\lfloor nt\rfloor+1}^{\lfloor nt+nu\rfloor}X_i\\
&\xrightarrow{(d)}\sqrt u\mathcal N(0,1)=\mathcal N(0,u)
\end{align}$$

- $$W_n(t+u)-W_n(t)\ind W_n(s),\forall s\lt t$$ because $$X_i\overset{i.i.d.}\sim\text{Rad}$$. In particular, $$X_i\ind X_j$$ for any $$1\le i\le\lfloor nt\rfloor$$ and $$\lfloor nt\rfloor +1\le j\le\lfloor nt+nu\rfloor$$.

Now, consider a vector of $$k$$ increments $$\{W_n(t_k)-W_n(t_{k-1})\}_{j=1}^{m}$$ and a linear mapping as follows.

$$\begin{bmatrix}
1&0&\dots&0\\
1&1&&0\\
\vdots&&\ddots&0\\
1&1&&1
\end{bmatrix}\begin{bmatrix}
W_n(t_1)-W_n(0)\\
W_n(t_2)-W_n(t_1)\\
\vdots\\
W_n(t_m)-W_n(t_{m-1})\end{bmatrix}=\begin{bmatrix}
W_n(t_1)\\
W_n(t_2)\\
\vdots\\
W_n(t_m)\end{bmatrix}$$

Since $$W_n(t_k)-W_n(t_{k-1})\xrightarrow{(d)}B(t_k)-B(t_{k-1})\sim\mathcal N(0,t_k-t_{k-1})$$, by applying the [CMT](/2022/02/21/introduction-to-statistics.html#properties), is clear that $$\mathbf W_n(t)=\begin{bmatrix}W_n(t_1)\dots W_n(t_m)\end{bmatrix}^T$$ converges to $$\mathbf B(t)=\begin{bmatrix}B(t_1)\dots B(t_m)\end{bmatrix}^T$$ in distribution, or that piecewise constant $$W_n(t)$$ converges in finite-dimension distributions to the continuous $$B(t)$$.

To establish further link between the two, one could introduce a continuous function that is still very close to $$W_n(t)$$, such as $$B_n(t)=W_n(t)+\frac{(nt-\lfloor nt\rfloor)}{\sqrt n}X_{\lfloor nt\rfloor+1}$$. Indeed, $$W_n(t)$$ can be seen as a limiting function, since $$\lim_{n\rightarrow\infty}B_n(t)=W_n(t)$$ and $$\lim_{t\rightarrow\frac{k+1}n}B_n(t)=B_n\left(\frac{k+1}n\right)=W_n\left(\frac{k+1}n\right)$$, because $$nt-\lfloor nt\rfloor\in[0,1)$$. Furthermore, $$\mathbf B_n(t)=\begin{bmatrix}B_n(t_1)\dots B_n(t_m)\end{bmatrix}^T\xrightarrow{(d)}\mathbf W_n(t)$$, because $$\boldsymbol{\Delta}_n(t)=\mathbf B_n(t)-\mathbf W_n(t)\xrightarrow{\mathbb P}\mathbf 0$$, as $$\lim_{n\rightarrow\infty}\mathbb P(\lVert\boldsymbol{\Delta}_n(t)\rVert_2^2\ge\varepsilon^2)=0$$. This is evident by noting that if $$\boldsymbol{\Delta}_n(t)=\frac1{\sqrt n}\begin{bmatrix}(nt_1-\lfloor nt_1\rfloor)X_{\lfloor nt_1\rfloor+1}\dots (nt_m-\lfloor nt_m\rfloor)X_{\lfloor nt_m\rfloor+1}\end{bmatrix}^T$$, then the following holds.

$$\begin{align}
\mathbb P\left(\lVert\boldsymbol{\Delta}_n(t)\rVert_2^2\ge\varepsilon^2\right)
&=\mathbb P\left(\frac1n\sum_{i=1}^m(nt_i-\lfloor nt_i\rfloor)^2X_{\lfloor nt_i\rfloor+1}^2\ge\varepsilon^2\right)&\href{/2022/01/05/conditioning-and-independence.html#sum}{\text{(probability of a sum)}}\\
&\le\sum_{i=1}^m\mathbb P\left((nt_i-\lfloor nt_i\rfloor)^2X_{\lfloor nt_i\rfloor+1}^2\ge n\varepsilon^2\right)\\
&=m\max_{i=1,\dots,m}\mathbb P\left(X_{\lfloor nt_i\rfloor+1}^2\ge\frac{n\varepsilon^2}{(nt_i-\lfloor nt_i\rfloor)^2}\right)&\href{/2022/02/21/introduction-to-statistics.html#basic}{\text{(Markov's inequality)}}\\
&\le m\frac{(nt_i-\lfloor nt_i\rfloor)^2}{n\varepsilon^2}{\mathbb E[X_{\lfloor nt_i\rfloor+1}^2]}\le\frac m{n\varepsilon^2}\rightarrow0&\text{($X_i\overset{i.i.d.}{\sim}\text{Rad}$)}
\end{align}$$

Accordingly, $$\mathbf B_n(t)=\mathbf W_n(t)+\boldsymbol{\Delta}_n(t)\xrightarrow{(d)}\mathbf B(t)+\mathbf 0$$. Put differently, this means that $$B_n(t)$$ converges in finite-dimension distributions to $$B(t)$$, which brings us to the main claim of the Donsker's thorem, according to which $$B_n(t)\xrightarrow{(d)}B(t)$$, which proof is omitted.

The main result of this theorem is that from simulation of $$B_n(t)$$ we can obtain the distribution of $$B(t)$$ by increasing $$n$$. A rough idea of such simulation is provided below, where you can manipulate the number of sub-intervals $$n$$ in which we split a time interval, and the number of processes to run in generate simultaneously $$m$$.

<iframe width='100%' height='950' src='https://rdrr.io/snippets/embed/?code=n%3C-1e2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20steps%20per%20experiment%0Am%3C-1e2%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20number%20of%20experiments%0At%3C-0%3An%2Fn%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20time%20intervals%0AR%3C-matrix((rbinom(n*m%2C1%2C.5)*2-1)%2Cnrow%3Dm)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20Rademacher%20steps%0AS_n%3C-cbind(rep(0%2Cm)%2Ct(apply(R%2C1%2Ccumsum)))%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20random%20walks%0AW_n%3C-S_n%2Fsqrt(n)%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20standardization%0Amatplot(t%2Ct(W_n)%2Ctype%20%3D%20%22l%22%2Cxlab%3D%22t%22%2C%0A%20%20%20%20%20%20%20%20ylab%3D%22standard%20random%20walk%22)' frameborder='0'></iframe>