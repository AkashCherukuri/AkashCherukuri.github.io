---
title: Reinforcement Learning
permalink: /notes/cs747/week7
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

Looking at the MDP from the agent's point of view, it is not guaranteed to know the transition probabilities and the rewards associated with an action. 

That is, the entire MDP (S, A, T, R, $\gamma$) is provided to the agent in the planning problem. In a learning setting, the agent knows only (S, A, $\gamma$) and sometimes R. It has to make inferences on T from experience.

Let a t-length history be defined as follows:

$$h^t = (s^0, a^0, r^0 \ldots s^t)$$

## Learning Algorithm

A *Learning Algorithm* L is a mapping from the set of all histories to set of all probability distributions over arms. We would like to construct L such that:

$$ \lim_{T\to\infty}\frac{1}{T}\left( \sum_{t=0}^{T-1} \mathcal{P} \[ a^t\sim L(h^t) is optimal for s^t \] \right) $$

The above problem is also known as the **Control Problem**.