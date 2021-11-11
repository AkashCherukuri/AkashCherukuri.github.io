---
title: Kernelized Logistic Regression
permalink: /notes/cs337/Lec11
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

We know that Regularized logistic regression's loss function is the cross entropy loss function with a regularization parameter. When the sigmoid activation function is used, we have already seen that the loss function becomes:

$$
E(w) = -\frac{1}{m}\left[ \sum_i \left(y_iW^\text{T}\phi_i - \log(1+\exp(W^\text{T}\phi_i))\right) \right] + \frac{\lambda}{2m}\vert\vert w\vert\vert^2_2
$$

Similar to the sigmoid activation, we define the activation function in logistic regression to be the following:

$$
\sigma_w(x) = \frac{1}{1+exp\left[ -\sum_j \alpha_j K(x,x_j) \right]}
$$

Using this function, the loss function in kernelized logistic regression turns out to be:

$$
E_D(\alpha) = -\left[ \sum_i \left( \sum_j y^i K(x^i, x^j)\alpha_j - \frac{\lambda}{2}\alpha_i K(x^i, x^j)\alpha_j \right) - \log\left( 1+exp\left[ -\sum_j\alpha_jK(x^i, x^j) \right] \right) \right]
$$

