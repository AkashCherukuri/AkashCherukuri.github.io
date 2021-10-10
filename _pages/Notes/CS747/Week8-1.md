---
title: Prediction Problem
permalink: /notes/cs747/week8_1
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

This problem is usually the first step in solving the Control problem. Let the learning algorithm be $L$. At each step $t$, let the estimated value of the states by the agent be $\hat{V}^t$. Given a policy $\pi$ that the agent follows, with value function $V^\pi$, we would like $L$ such that:

$$\lim_{t\to\infty} \hat{V}^t = V^\pi $$


A few assumptions have to be taken before we can begin to tackle this problem.

### Irreducibility

Given an MDP $M$ and policy $\pi$; if there is a directed path between every $s$ and $s'$ with non-zero policy, then **The MDP is said to be irreducible under the policy**.

If $M$ is irreducible for all $\pi\in\Pi$, then $M$ is irreducible.
{: .notice--info}

Intuition: We do not want the learning algorithm's policy to be stuck in some subset of states


### Aperiodicity

*whaaatt*

&nbsp;

### Ergodicity

An MDP which is both Irreducible and Aperiodic is said to be **Ergodic** in nature. An Ergodic MDP induces a steady state distribution $\mu^\pi: S\to(0,1)$ for every policy $\pi$.

That is, let the probability of current state being $s$ after $t$ timesteps be $p(s,t)$. This value must also depend on the initial state. However, ergocidity states that as $t\to\infty$, the distribution tends to $\mu^\pi$, which is **independent** od the initial state.
{: .notice--info}

&nbsp;

## Model-Based Approach

A *model* is an estimate of the MDP by the agent. Let the estimated MDP be $(S, A, \tilde{T}, \tilde{R}, \gamma)$, we wish that this converges to the true MDP.

As like with bandits, we would like to visit every state-action pair infinitely many times.

The algorithm we shall propose is the following:
- Take uniform random actions until every state-action pair has been taken atleast once, the model is said to be *valid* now
- If model is *valid*, take a random action with probability $\epsilon$ and calculated optimal with probability $1-\epsilon$
- Update the values of (S, A, T, R) to be their empirical means after every iteration

We shall state without a proof that **for convergence to optimal behaviour, the algorithm only requires irreducibility**.
{: .notice--info}

An algorithm is said to be "model-based" if if uses $\theta(n^2k)$ memory. Similarly, we call a model to be model-free if it is using only $\theta(nk)$ memory.


## Monte-Carlo's Method

Given an episodic task, we observe the agent taking uniform random actions for $e$ episodes. This method is used to estimate the value of each state given the history for each episode.

We define the following:

- $G(s,i,j)$ : Discounted reward of $s$ from its $j$'th visit in episode $i$
- $1(s,i,j)$ : 1 if $s$ has occured atleast $j$ times in episode $i$

### First Visit Monte-Carlo

$$ \hat{V}(s) = \frac{\sum G(s,i,1)}{\sum 1(s,i,1)} $$

### Every Visit Monte Carlo

$$ \hat{V}(s) = \frac{\sum_i\sum_j G(s,i,j)}{\sum_i\sum_j 1(s,i,j)} $$

### Second Visit Monte-Carlo

$$ \hat{V}(s) = \frac{\sum G(s,i,2)}{\sum 1(s,i,2)} $$

### Last Visit Monte-Carlo

$$ \hat{V}(s) = \frac{\sum G(s,i,times(s,i))}{\sum 1(s,i,times(s,i))} $$

&nbsp;

$\hat{V}(s)$ for the first three given above converges to the ideal value, **BUT THE LAST ONE DOESN'T!**
{: .notice--warning}