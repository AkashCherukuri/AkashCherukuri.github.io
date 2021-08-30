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

&nbsp;

# Alternative Formulations

### Reward Function

The reward function can be defined differently in literature. For example, it could be *stochastic* instead of deterministic. It might be just dependant on $(s,a)$ instead of $(s,a,s')$. 

Some authors minimize *cost* instead of maximizing reward. The core idealogy remains the same, however.

A *multi-armed bandit* is an MDP with a single state and each of the actions being associated with a uniform distribution as a reward!
{: .notice--success}

### Episodic Tasks

Our discussion used *continuing tasks*, where trajectories are infinitely long. Episodic tasks have a *terminal/sink* state from which outgoing transitions are absent. 

There should be non-zero probability of reaching the sink state from every non-terminal state, meaning that trajectories would surely be finite.
{: .notice}

### Value function

The definition used by us is called as **Infinite Discounted Reward**. There are other choices as well:

1. Total Reward - Can only be used on episodic tasks (Obv)
2. Finite Horizon Reward - Set a horizon $T$ and sum up rewards till here. Optimal policies for this need not be stationary.
3. Average Reward - Exactly what the name suggests

&nbsp;

# Policy Evaluation

The process of calculating the value of each state given the MDP is called as policy evaluation. **Bellman's Equations** are used for this procedure.

These equations are used to find the values of every state for a given MDP. For every state $s\in S$;

$$V^{\pi}(s) = \sum_{s'\in S} T(s, \pi(s), s')\left{ R(s, \pi(s), s') + \gamma V^{\pi}(s') \right}$$
{: .notice--info}

There are $n$ such linear equations, and $n$ unknowns. 
- unique solution guaranteed if $\gamma < 1$
- for episodic, if $\gamma=1$, solution guaranteed if value of terminal state fixed as $0$.

&nbsp;

## Action Value Functions

The naive method of finding $\pi^\*$ for a given MDP would be to use Bellman's equations for each policy and get the minima. This would take $\text{poly}(n,k)\cdot k^n$ time.

We define the Action Value function $Q^{\pi}(s,a)$ as the first step for obtaining a more efficient solution.

$Q^{\pi}(s,a)$ is the expected long term reward for starting at state $s$, taking action $a$ at $t=0$ and then following $\pi$ for $t\>0$.

Its value is given by the equation:
<div class="notice--info" style="text-align: center;">
  $$ Q^{\pi}(s,a) = \sum T(s,a,s')\left[ R(s,a,s') + \gamma V^{\pi}(s') \right] $$
</div>

We know that all optimal policies have same optimal value function, and by extension, all optimal policies will have the same action value function as well.