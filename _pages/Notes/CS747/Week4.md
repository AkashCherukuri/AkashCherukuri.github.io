---
title: Markov Decision Problem
permalink: /notes/cs747/week4
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

A Markov Decision problem $M$ is given by the tuple $(S, A, T, R, \gamma)$. Each of these elements are defined below.

- $S$ is the set of states. $\vert S\vert = n$
- $A$ is the set of actions. $\vert A\vert = k$

- $T$ is the Transition function. $T(s, a, s')$ gives the probability of reaching $s'$ from $s$ by taking the action $a$. Note that $T(s,a,\cdot)$ is a probability distribution over $S$.

- $R$ is the Reward function. $R(s,a,s')$ gives the reward for reaching $s'$ from $s$ via action $a$. We assume $R(s,a,s')\in \[ -R_{max}, R_{max} \]$.

- $\gamma$ is the Discount factor.

Let $s^t$ denote the state at the $t^{th}$ time-step. Similarly, $a^t$ is the action taken at this time-step and $r^t$ is the reward for this action.

*Trajectory* is the history of the agent.

A *policy* $\pi$ is a function which the agent follows to give an action at any state. For simplicity, let the agent look *only* at the current state for its policy. That is, $\pi: S\to A$. This policy is:
- *Markovian* - Looks only at the current state and not at history
- *Deterministic* - A single action is given, not probability distribution
- *Stationary* - The output doesn't change with time

$\Pi$ is the set of all policies. In this case, $\vert \Pi\vert = k^n$. We would like a policy which maximizes the overall reward obtained.

### Value of a State

The value of a state under a policy $\pi$, $V^{\pi}(s)$ tries to tell us how "good" the state is for accumulating a large reward. 

<div style="text-align: center;">
  $$ V^{\pi}(s) = \mathcal{E}_{\pi}\left[ r^0 + \gamma r^1 + \gamma^2r^2 + \ldots \vert s^0 = s \right] $$
</div>

Large $\gamma$ means a large "lookahead". The agent looks further ahead into the future to decide upon the value of the state. Do note that $\gamma\in \[0,1)$

&nbsp;

## MDP Planning Problem

It can be mathematically proven that every such MDP has an optimal Markovian, deterministic, stationary policy $\pi^\*$ such that

<div style="text-align: center;">
  $$ \forall\pi\in\Pi, \forall s\in S: V^{\pi*}(s)\geq  V^{\pi}(s)$$
</div>

That is, the value of every state is larger in the optimal policy. This policy is *NOT* unique! The MDP Planning Problem is centered around finding this optimal policy $\pi^\*$.

