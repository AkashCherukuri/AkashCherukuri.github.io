---
title: Iterative Soft Thresholding Algorithm
permalink: /notes/cs337/Lec6
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

This algorithm is used for fitting the model using lasso regression.

While the relative drop in Lasso error across $t=k$ and $t=k+1$ is significant, the following two steps are done.

1. *LS Iterate*

    $w^{k+1}\_{LS} = w^{k+1}\_{Lasso} - \eta\nabla E\_{LS}(w^{k}\_{Lasso})$

2. *Proximal Step*

    If absolute value of $\left[w^{k+1}\_{LS}\right]\_i$ is less than $\lambda\eta$, then the $i^{th}$ element of $w^{k+1}\_{lasso}$ is 0.

    Else, just reduce its magnitude by $\lambda\eta$ while keeping the sign intact.

&nbsp;

# Evaluating Performance

### Method 1: Training Error

This idea is not good enough. Error obtained via ridge regression will always be larger than the least squared error. Also, going by training error alone lets overfitting slip by.

### Method 2: Test Error

Use a different dataset, seperate from the training data to evaluate loss of the model. This is good for finding if overfitting is taking place.

There tend to be three main sources of error:
1. Bias - Difference between true and fitted data function
2. Variance - Deviation of fits as sample data changes
3. Noise

## Bias Variance Analysis

Before starting the analysis, we assume the following three points:

1. *Noise is Additive:* $y = g(x) + \epsilon$
2. Noise has mean 0 and variance $\sigma^2$, need not be gaussian
3. We are performing Linear fit via OLS (Ordinary Least Squares)

Let $g$ be the true function, and $f$ be the model. If $\<\hat{x},\hat{y}\>$ is data, then the expected value of Least Square error is:

<div class="notice--info" style="text-align: center;">
  $$\begin{eqnarray}
  \mathcal{E}[(f-y)^2] &= \mathcal{E}[(f-\bar{f})^2] + (\bar{f} - g)^2 + \mathcal{E}[(y-g)^2] \\
  &= \text{Variance}(g) + \text{Bias}(g)^2 + \sigma^2 
  \end{eqnarray}$$
</div>

Here $f$ is $f(\hat{x})$, $g$ is $g(\hat{x})$ and $\bar{f}$ is $\mathcal{E}\[f(\hat{x})\]$. Also, remember that $\sigma$ is the variance of noise.

We divide the dataset into three categories:
1. *Train:* to train the model
2. *Validation:* to tune the model's hyperparameters
3. *Test:* for final testing