---
title: Probabilistic Linear Regression
permalink: /notes/cs337/Lec3
classes: wide
author_profile: false
sidebar:
    nav: "notes_cs337"
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


<!-- Notes begin from here --->

We can model $Y$ to be a linear function as before, with an additional noise parameter $\epsilon \sim \mathcal{N}(0,\sigma^2)$. That is, the relation is

<div style = "text-align: center;">
  $$ Y = W^T\Phi(x) + \epsilon $$
</div>

Normal distribution has the maximum entropy amongst all distributions with a given variance. The $3-\sigma$ rule also plays a vital role for picking this. (68, 95, 99.7)

The maximum likelihood estimate of $W$ is calculated in this case. (Remember that calculation is simplified by taking $\log$ to get the *Log-Likelihood*)

&nbsp;

# Overfitting and Regularization

Increasing the degrees of freedom causes this issue. The model essentially brute-forces all data points in training data, which isn't very helpful. Overfitting is caused by $\vert\vert W_i\vert\vert$ being large, and regularization tries to suppress this.

## Bayesian Linear Regression

The problem of overfitting is addressed by a *prior*. That is, the prior models $W$ by bounding the norm to be smaller than some $\Theta$.

To understand this better, we shall first tackle a simpler coin-tossing example.

I have a newly minted coin which I *believe* to be fair. I now flip it four times and get 4 heads. The MLE would be 1, but this isn't taking the prior belief into account. The posterior would be given by the baye's rule.

The *Prior* is given by $P(H)$, and the *Posterior* is given by $P(H\vert D)$. Therefore, the relation is given by:

<div style="text-align: center;">
  $$P(H|D) = \frac{P(D|H)\times P(H)}{P(D)} \propto P(D|H)\times P(H)$$
</div>

We ignore the denominator as it is just a normalizing factor, and is constant as the data is known.

If $P(D\vert H)$ follows distribution $d_1$ the *posterior* and *prior* follow the same distribution $d_2$, then $d_2$ is said to be the **conjugate prior** of $d_1$.
{: .notice--warning}

Examples include:
- Gaussian - Gaussian
- Bernoulli & Binomial - Beta
- Categorical & Multinomial - Dirchlet

### Beta Distribution

Wikipedia page link: [Beta distribution](https://en.wikipedia.org/wiki/Beta_distribution)

In short, the beta distribution has two parameters $\alpha, \beta$. The value of the distribution always lies between 0 and 1. The pdf is given by:

<div style="text-align: center;">
 $$\begin{eqnarray}
 \text{Beta}(\alpha, \beta) &= \frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha, \beta)}\\
 B(\alpha, \beta) &= \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}\\
 \end{eqnarray}$$

 <img src="/assets/images/CS337/beta_dist.png">
</div>

The advantage of conjugate distributions is that the posterior is always of the same family as the prior, with just the parameters changed. This makes calculations very easy.

In the above coin tossing example, we know that Bernoulli and Beta are conjuagtes. Therefore, we can model the prior of $p$ as a *BETA* distribution $\text{Beta}(\alpha, \beta)$ for simplicity.

If there are $h$ heads occurring in $n$ tosses, then the posterior distribution turns out to be $\text{Beta}(\alpha+h, \beta+n-h)$.
{: .notice--info}

If we have no prior information regarding $p$, we can model it as a beta with both parameters equal to 1. (The beta is uniform in 0 to 1 when both parameters are 1, just what we intend to have)