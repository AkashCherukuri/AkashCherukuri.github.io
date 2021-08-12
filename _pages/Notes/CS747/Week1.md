---
title: Multi-Armed Bandits
permalink: /notes/cs747/week1
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


<!-- Notes Begin from here -->

## Explore Exploit Dilemma

This dilemma can be stated as the question:

> Do I use the experience gained so far to pick the most optimal move, or do I keep exploring and obtain more data?

Do note that it is not guaranteed for the move made by the agent (using limited data) to be optimal globally. Such a dilemma is observable in clinical trials, online advertising and packet routing in communication networks.

## Formal Definitions and Notations

### Stochastic Multi-armed bandit

Has $n$ *arms*, each of which is a Bernoulli Distribution. The $i^{th}$ arm has mean reward $p_i$, and the largest mean is $p_M$.

It is *Stochastic* because the distribution of each *arm* is known.

### Algorithm

Operates on the multi-armed bandit, by deciding which *arm* is to be pulled; to get a reward for that action.

That is, at any time $t$, given the **history** ($h^t$) it chooses an arm to **sample** ($a^t$) to obtain a reward $r^t$.

<div style="text-align: center;">
	$$ h^t = (a^0, r^0, a^1, \ldots, a^{t-1}, r^{t-1}) $$
</div>

The maximum number of pulls allowed is called as the total sampling budget or **horizon** ($T$).

A *deterministic algorithm* maps the set of all histories to the set of all arms. Similarly, a *randomized algorithm* maps the set of all histories to the set of all **probability distributions** over the arms.

<div style="text-align: center;">
	$$ \mathbb{P}(h^t) = \prod^{T-1}_{t=0} \mathbb{P}(a^t|h^t)\cdot \mathbb{P}(r^t|a^t) $$
</div>


Using the above relation, we can see that $(2n)^T$ possible histories are possible for a deterministic algorithm acting on a stochastic multi-armed bandit, with horizon $T$.
{: .notice--primary}

## Epsilon Greedy Algorithms

$\epsilon$ is a parameter $\in [0,1]$ which controls the amount of exploration. It is used in different ways, some explained below.

1. $\epsilon$G1
	- For $t \leq \epsilon T$, sample an arm uniformly at random
	- At $t = \lfloor \epsilon T \rfloor$ determine the action with the highest empirical mean, and choose this action everytime

2. $\epsilon$G2
	- For $t \leq \epsilon T$, sample an arm uniformly at random
	- For $t > \epsilon T$, sample the arm with the highest empirical mean
	- That is, the value of the mean  is updated in this case after $\epsilon T$ steps, wheras it wasn't done previously

3. $\epsilon$G3
	- With probability $\epsilon$ sample an arm uniformly at random, and with $1-\epsilon$ sample the arm with highest empirical mean

## Evaluating Algorithms

This is visualized by plotting a graph between the expected reward and the time stamp of the algorithm. To gauge the performance, three horizontal lines are plotted; $p_M$, $p_{min}$, $p_{avg}$. We expect the algorithm to start out near the average and reach the max with increasing time steps.

The expected cumulative **regret** of the algorithm is defined as follows:

<div style="text-align: center;">
	$$ R_T = Tp_M - \sum_{t=0}^{T-1}\mathbb{E}(r^t) $$
</div>

That is, the difference between the maximum possible reward and what you end up getting. Ideally, we would like the value of $(R_T/T)$ to tend to $0$ as $T$ tends to $\infty$.

That is, we would like the algorithm's regret to be sublinear.
{: .notice--warning}