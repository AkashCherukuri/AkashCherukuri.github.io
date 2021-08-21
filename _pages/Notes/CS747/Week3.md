---
title: Hoeffding's Inequality
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

Let $X$ be a random variable in $\[0,1\]$ with $E\[X\] = \mu$. Now, let's say that we draw $u$ samples from this distribution, each $x_i$, and the empirical mean is $\bar{x}$.

Then, for any fixed $\epsilon>0$ we have

<div class="notice" style="text-align: center;">
  $$\begin{eqnarray}
    \mathcal{P}\{ \bar{X} \geq \mu+\epsilon} \leq \exp{-2u\epsilon^2} \\
    \mathcal{P}\{ \bar{X} \leq \mu-\epsilon} \leq \exp{-2u\epsilon^2} \\
  \end{eqnarray}$$
</div>

Intuitively, as $u$ increases, the probablity that empirical mean deviates should decrease. Here, $\epsilon$ acts as **Confidence Interval** around the true mean (which is unknown).

*Doubt in Slide 4, point 2; It doesn't seem right*

Hoeffding's Inequality can be extended to a random variable bounded in $\[a,b\]$ by defining a new random variable $y = \frac{X-a}{b-a}$, and applying to this. We get;

<div class="notice" style="text-align: center;">
  $$\begin{eqnarray}
    \mathcal{P}\{ \bar{X} \geq \mu+\epsilon} \leq \exp{\frac{-2u\epsilon^2}{(b-a)^2}} \\
    \mathcal{P}\{ \bar{X} \leq \mu-\epsilon} \leq \exp{\frac{-2u\epsilon^2}{(b-a)^2}} \\
  \end{eqnarray}$$
</div>

## KL Inequality

This gives a tighter bound for empirical mean. **Note that** $\mu\pm\epsilon$ **must be positive** in RHS of both the inequalities.

<div class="notice" style="text-align: center;">
  $$\begin{eqnarray}
    \mathcal{P}\{ \bar{X} \geq \mu+\epsilon} \leq \exp{-uKL(\mu+\epsilon, \mu)} \\
    \mathcal{P}\{ \bar{X} \leq \mu-\epsilon} \leq \exp{-uKL(\mu+\epsilon, \mu)} \\
    \\
    KL(p,q) = pln(\frac{p}{q})+(1-p)ln(\frac{1-p}{1-q}) \\
  \end{eqnarray}$$
</div>

Note that both the inequalities are examples of *Chernoff bounds*.

&nbsp;

# Analysis of UCB

We shall use the above inequalities to prove that the UCB algorithm is logarithmic in nature.

### Notation

- $\Delta_a = p_M - p_a$ - The difference between this arm and optimal
- $Z^t_a$ - An *event* when arm $a$ is pulled at time $t$
- $z^t_a$ - Indicator for the above event (1 if event occurs, 0 otherwise)

<div style="text-align: center;">
  $$\mathcal{E}\[z^t_a\] = \mathcal{P}\[Z^t_a\]$$
</div>

- $u^t_a$ - Number of times arm $a$ has been pulled, till time $t$
<div style="text-align: center;">
  $$u^t_a = \sum_{i=0}^{t-1}z^i_a$$
</div>

- $\bar{u}^T_a$ - A constant used in the proof, sufficient number of pulls of arm $a$ for horizon $T$
<div style="text-align: center;">
  $$\bar{u}^T_a = \ceil{ \frac{8}{(\Delta_a)^2}ln(T) }$$
</div>

*This proof truly be a mind = blown moment :/*


&nbsp;

# Thompson Sampling