---
title: MAP and Bayes Estimates
permalink: /notes/cs337/Lec5
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

The posterior distribution's mean and variance have been calculated in the previous lecture. Because the posterior is a gaussian, we can clearly understand that

<div style="text-align: center;">
  $$ \hat{w}_{MAP} = \hat{w}_{Bayes} = \mu_m $$
</div>

MAP is the $w$ where a global maxima is attained, and Bayes is the expected value of $w$. 

## Pure Bayesian 

*Didn't understand anything, kek*

## Regularized Ridge Regression

The Bayes and MAP estimates obtained for linear regression coincide with *regularized ridge regression* as well.

<div style="text-align: center;">
  $$w_{ridge} = \text{arg }\min_w \vert\vert \Phi W - y \vert\vert^2_2 + \lambda\sigma^2\vert\vert W\vert\vert^2_2$$
</div>

In case of polynomial regression, increasing $\lambda$ tends to decrease the curvature, as 2-norm is being limited.

Replacing 2-norm with 1-norm is called as *Lasso Regression*, and with 0-norm is called as *Support Based Penalty*. 

The additional term is usually represented as $\Omega(w)$, and this formulation is known as *Penalized Formulation*. The original problem of wanting to limit 2-norm of $w$ to be less than or equal to $\theta$ is called *Constrained Formulation*.
{: .notice}

<div class="notice--info">
  <div style="font-weight: bold;">
  Claim.
  </div>

  For any Penalized Formulation with a particular $\lambda$, there exists a corresponding Constrained formulation with a corresponding $\theta$.

</div>

Lasso Regression tends to yield solutions that are *sparser*. That is, it is more likely for elements of $w$ to be 0 using this method. (many corners)

This follows a Laplacian distribution, and has no closed form solution. Therefore, iterating with gradient descent is the only way for Lasso regression. The algorithm for lasso regression will be explained in the next lecture.