---
title: Regret Optimization
permalink: /notes/cs747/week2
classes: wide
author_profile: false
sidebar:
    nav: "notes_cs747"
---
<script type="text/javascript" src="https://code.jquery.com/jquery-1.7.1.min.js"></script>

<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML" async></script>

<!-- Notes begin from here -->

Let's analyze the performance of $\epsilon$G1 and $\epsilon$G2. The regret calculations are shown below:

<div style="text-align: center;">
  $$\begin{eqnarray}
  R_T &=& Tp_M - \sum^{T-1}_{t=0}\mathbb{E}(r^t) \\
  &=& Tp_M - \sum^{\epsilon T-1}_{t=0}\mathbb{E}(r^t) - \sum^{T-1}_{t=\epsilon T}\mathbb{E}(r^t) \\
  &\geq& Tp_M - (\epsilon T)p_{avg} - T(1-\epsilon)p_M \\
  &\geq& \epsilon T(p_M - p_{avg}) \\
  &\in& \Omega (T) \\
  \end{eqnarray}$$
</div>

That is, the regret is not sublinear, even in the best case scenario where the algorithm performs perfectly after exploration.


Now let's do the same regret analysis of $\epsilon$G3.

<div style="text-align: center;">
  $$\begin{eqnarray}
  R_T &=& Tp_M - \sum^{T-1}_{t=0}\mathbb{E}(r^t) \\
  &\geq& Tp_M - \sum^{T-1}_{t=0}(\epsilon p_{avg} + (1-\epsilon)p_M)\\
  &\geq& \epsilon T(p_M - p_{avg}) \\
  &\in& \Omega(T) \\
  \end{eqnarray}$$
</div>

That is, all three epsilon greedy algorithms discussed earlier are not sub-linear in nature.
{: .notice--warning}


## Acheiving Sublinear Regret

There are two general heuristics which should be met for a sub-linear algorithms.

1. Every arm in the multi-armed bandit must be pulled *infinite* number of times as $T\rightarrow \infty$.

2. Let $exploit(T)$ be the number of pulls that are exploitative in nature. Then, for sublinear regret we need the following;

  <div style="text-align: center;">
    $$\lim_{T\to\infty}\frac{\mathbb{E}(exploit(T))}{T} = 1$$
  </div>

  That is, *nearly all* of the pulls must be of exploitative behaviour.

Now, let $\bar{\mathcal{I}}$ be a set of all bandit instances with reward means **strictly** less than 1. Then;

An algorithm *L* acheives sub-linear regret on all instances of $I \in \bar{\mathcal{I}}$ **iff** the algorithm satisfies both the above mentioned conditions.
{: .notice--success}

These conditions are called as **GLIE** in short, which stands for "Greedy Limit Infinite Exploitation".

### Modifying epsilon greedy strategies

$\epsilon$G1/2 can be modified slightly to make it "GLIE compliant", instead of exploring for $\epsilon T$ pulls, we explore for $\sqrt{T}$ pulls.

- C1 satisfied since each arm pulled $\sqrt{T}/n$ times on average
- C2 satisfied as $exploit(T)$ would be $T-\sqrt{T}$

Similarly, $\epsilon$G3 can be fixed by making epsilon a function of $t$, as $1/(t+1)$. It can be seen pretty easily that the conditions are satisfied, using the below equation.

<div style="text-align: center;">
  $$\sum^{T-1}_{t=0}\frac{1}{n(t+1)} = \Theta(\frac{\log T}{n})$$
</div>


# Lai and Robbins Lower Bound

This result establishes that the lower bound on the regret  attainable for a **sub-polynomial** algorithm is *logarithmic* in $T$.
{: .notice--success}

It has been stated more formally below; note the little-o notation.

If $L$ be an algorithm such that for every bandit $I\in\bar{\mathcal{I}}$ and for every $\alpha>0$, as $T\rightarrow\infty$

<div style="text-align: center;">
  $$R_T(L,I) = o(T^\alpha)$$
</div>

Then, for every bandit instance $I\in\bar{\mathcal{I}}$ as $T\rightarrow\infty$

<div style="text-align: center;">
  $$ \frac{R_T(L,I)}{ln(T)} = \sum_{a:p_a(I)\neq p_M(I)}\frac{p_M(I) - p_a(I)}{KL(p_a(I), p_M(I))} $$
</div>

Where, $KL(x,y) = xln(x/y)+(1-x)ln((1-x)/(1-y))$

(Notice that the RHS of second equation is constant for a given bandit)

## Sublinear Algorithms

### UCB 
  
  At every time $t$ and arm $a$, define $\text{ucb}^t_a$ as follows:

  <div style="text-align: center;">
    $$\text{ucb}^t_a = \hat{p}^t_a + \sqrt{\frac{2ln(t)}{u^t_a}}$$
  </div>

  Where $\hat{p}^t_a$ is the empirical mean of that arm, and $u^t_a$ is the number of times that arm has been pulled. (Pull all the arms once before calculating)

  The algorithm samples the arm with the **highest ucb**. This acheives a regret of $O(\log(T))$, the optimal dependance on $T$.

### KL UCB 

  Although UCB is optimal order-wise, the constant is still different. KL-UCB fixes this by changing the definition of UCB slightly.

  <div style="text-align: center;">
    $$\text{kl-ucb}^t_a = \max\{ q\in[\hat{p}^t_a,1]\text{ where } KL(\hat{p}^t_a,q)\leq ln(t)+cln(ln(t)) \}$$
  </div>
  <div style="text-align: right;">
    $$\text{where } c\geq 3$$
  </div>

  Notice that $ u^t_aKL(\hat{p}^t_a,q)$ monotonically increases with $q$, easy to find value by binary search! This algorithm asymptotically matches the Lai and Robbins' Lower Bound as well.


### Thompson Sampling

  This algorithm uses *Beta Distribution*, and it's parameters are given below. Note that this distribution is always going to give values between 0 and 1.

  $$Beta(\alpha, \beta) \rightarrow \mu = \frac{\alpha}{\alpha+\beta}, \sigma^2 = \frac{\alpha\beta}{(\alpha+\beta)^2(\alpha+\beta+1)}$${: .notice--warning}

  <!-- Here's the [Wikipedia Page](https://en.wikipedia.org/wiki/Beta_distribution) {: .btn .btn--success} for Beta Distribution. -->

  At time $t$, let arm $a$ have $s^t_a$ successes and $f_a^t$ failures. Then, $Beta(s^t_a+1, f_a^t+1)$ represents a *belief* about the true mean of that arm.

  For every arm $a$, draw a sample $x^t_a \sim Beta(s^t_a+1, f_a^t+1)$ and chose the arm which gave the maximal $x^t_a$ (and update the distribution).

  This acheives optimal regret, and is excellent in practice. Usually, it performs slightly better than KL-UCB as well.


All these algorithms are examples of *optimism in face of uncertainity* principle.
{: .notice--info}