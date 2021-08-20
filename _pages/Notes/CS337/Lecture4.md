---
title: Bayesian Linear Regression
permalink: /notes/cs337/Lec4
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

<!-- Notes begin from here -->

As discussed earlier, we would like the norm of $W_i$ to be small. For the sake of simplicity, we limit ourselves to a univariate case.

Here, we just want the value of $W$ to be small. We can thus assume that the prior for $W$ is a gaussian distribution of 0-mean and variance $1/\lambda$.

Recall that the product of two gaussians, $\mathcal{N}(\mu_1, \sigma_1^2)$ and $\mathcal{N}(\mu_2, \sigma_2^2)$ is also a gaussian distribution with the following parameters:

<div style="text-align: center;">
  $$\begin{eqnarray}
    \frac{1}{\sigma^2} &= \frac{1}{\sigma_1^2} + \frac{1}{\sigma_2^2} \\
    \frac{\mu}{\sigma^2} &= \frac{\mu_1}{\sigma_1^2} + \frac{\mu_2}{\sigma_2^2} \\ 
  \end{eqnarray}$$
</div>

Consider the univariate case where a random variable $X$ is a gaussian $\mathcal{N}(\mu, \sigma^2)$, and $\sigma$ is known. We have prior distribution of $\mu$ as well, $\mathcal{N}(\mu_o, \sigma_o^2)$. Given $m$ datapoints of x, it can be quite easily seen that the posterior distribution of $\mu$ would be $\mathcal{N}(\mu_m, \sigma_m)$, where:

<div style="text-align: center;">
  $$\begin{eqnarray}
    \frac{1}{\sigma_m^2} &= \frac{1}{\sigma_o^2} + \frac{1}{\sigma_2^2} \\
    \frac{\mu_m}{\sigma_m^2} &= \frac{\mu_o}{\sigma_o^2} + \frac{\mu}{\sigma^2} \\ 
  \end{eqnarray}$$
</div>


### Extend to Multivariate Case

The above result can be extended to a multi-variate linear regression case as well. In the equation, $Y = W^T\Phi + \epsilon$, let the $\epsilon$ distribution's prior be given by $(\mu_o, \Sigma_o^{-1})$ where $\Sigma_o$ is analogous to $\sigma^2$. (It is the covariance matrix) 

Similarly, data would be given by $(\mu_{mle}, \Sigma^{-1})$ (assuming that $\Sigma$ is fixed like in univariate), and $m$ data points are available to us. The posterior distribution can be calculated to be $(\mu_m, \Sigma_m)$ where

<div style="text-align: center;">
  $$\begin{eqnarray}
    \Sigma_m^{-1} &=  \Sigma_o^{-1} + m\Sigma^{-1} \\
    \mu_m\Sigma_m^{-1} &= \mu_o\Sigma_o^{-1} + m\mu_{mle}\Sigma^{-1} \\
  \end{eqnarray}$$
</div>


However, the value of $\Sigma$ was arbitrarily introduced by us. We have been taking $\epsilon\sim\mathcal{N}(0,\sigma^2)$. We can use this and the closed form solution to the equation, $W = (\Phi^T\Phi)^{-1}\Phi^TY$ to replace its value, to obtain the final solution given below.

<div class = "notice--warning" style="text-align: center;">
  $$\begin{eqnarray}
    \Sigma_m^{-1} &= \Sigma_o^{-1} + (\Phi^T\Phi)/\sigma^2 \\
    \mu_m\Sigma_m^{-1} &= \mu_o\Sigma_o^{-1} + (\Phi^TY)/\sigma^2 \\
  \end{eqnarray}$$
</div>
