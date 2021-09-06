---
title: MDP Planning ALgorithms
permalink: /notes/cs747/week5
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

We would like to solve the MDP Solving problem efficiently. Before stating the algorithm, we shall first go over a bunch of theoretical results.

&nbsp;

## Banach Space

A *complete, normed vector space* is called as a Banach Space. That is, both the vector space and norm are well defined. Additionally, every Cauchy sequence must have a limit in that vector space.
{: .notice--info}

A *Cauchy sequence* is a convergent sequence. Example, rationals are not Banach because an irrational number can be written as a sequence of rational numbers ($\sqrt{2}$) 

### Contraction Mapping

A mapping $T:X\to X$ is called a contraction mapping with *contraction factor* $L$ if $\forall u,v\in X$,

$$\vert\vert Tv-Tu\vert\vert \leq L\vert\vert v-u\vert\vert$$

$x^\*$ is a **fixed point** of $T$ if $Tx^\*=x^\*$.

### Banachs Fixed-Point Theorem

This theorem states that for a given contraction mapping and a contraction factor $L\in\[0,1)$:

1. There exists a *unique* fixed point
2. For $x\in X, m\geq 0; \vert\vert T^mx-x^\*\vert\vert \leq L^m\vert\vert x-x^\*\vert\vert$

&nbsp;

## Bellman Optimality Operator

$B^\* : \mathcal{R}^n\to\mathcal{R}^n$ for an MDP $(S,A,T,R,\gamma)$ is given as follows;

<div style="text-align: center;">
$$ (B^*(F))(s) = \max_{a}\sum_{s'}T(s,a,s')\left[ R(s,a,s') + \gamma F(s') \right] $$
</div>

That is, we have used notation to redefine the domain of value function to be $\mathcal{R}^n$, and $B^\*$ maps value functions.

**Theorem.** $(\mathcal{R}^n, \vert\vert\cdot\vert\vert_{\infty})$ is  a Banach space, and $B^\*$ is a contraction mapping in this space with contraction factor $\gamma$.
{: .notice--warning}

<div style="text-align: center;">
  $$ \vert\vert F\vert\vert_{\infty} = \max (\vert f_1\vert, \ldots \vert f_n\vert) $$
</div>

## Bellmans Optimality Equations

The fixed point can be obtained by solving the equation:

<div style="text-align: center;">
$$ V^*(s) = \max_{a}\sum_{s'}T(s,a,s')\left[ R(s,a,s') + \gamma V^*(s') \right] $$
</div>

There are $n$ variables and $n$ unknowns, but the equations are non-linear in nature. These equations are called as the Bellman's Optimality Equations for the given MDP. Algorithms for solving these equations will be discussed below.

We shall also prove later that $V^\*$ is an optimal value function for a given MDP.

&nbsp;

# Value Iteration

This is a very simple algorithm. We apply the optimality operator iteratively until the difference is negligible. We know this works from the Banach's Fixed point operator.

Also, notice that $V^\*, Q^\*, \pi^\*$ have a cyclic relationship.

1. $V^\*\to Q^\*$: definition of $Q^\*$
2. $Q^\*\to \pi^\*$: $\text{arg}\max_aQ^\*(s,a)$
3. $\pi^\*\to V^\*$: Solve bellman equations for $\pi^\*$

&nbsp;

# Linear Programming

This is a technique where a *Linear objective function* of variables under *given linear constraints* is maximized. We can frame the Bellman's optimality equations as a linear programming problem.

From the Bellman optimality equations, we can say the following. Notice that there are $nk$ linear constraints and $V^\*$ staisfies all these constraints.

<div style="text-align: center;">
$$ V(s) \geq \max_{a}\sum_{s'}T(s,a,s')\left[ R(s,a,s') + \gamma V^*(s') \right] $$
</div>

<div class="notice--success">
  $B^*$ preserves $\succeq$
</div>

From this, we can say that $V \succeq V^\*$, and can thus linearise the result to be $\sum_s V(s)\geq \sum_s V^\*(s)$.

Therefore, the *objective function* to be maximized is given by 

<div style="text-align: center;">
$$ -\left( \sum_s V(s) \right) $$
</div>

This LP problem has $n$ variables and $nk$ constraints. Do note that a dual is possible which solves for $\pi^\*$ with $nk$ variables and $n$ constraints.