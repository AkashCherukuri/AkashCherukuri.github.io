---
title: Supervised and Unsupervised Learning
permalink: /notes/cs337/Lec1
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


<!-- Notes Begin from here -->

*Supervised Learning* is when a goal is achieved by learning from training data which contains true labels. Examples include linear regression and classification.

*Unsupervised Learning* is when objects similar to each other are grouped together. Examples include clustering and **dimensionality reduction**. The desired output is unobserved in the training data.

There are three canonical learning settings:
1. *Regression - Supervised*

  Estimate parameters, such as least square fit

2. *Classification - Supervised*

  Given parameters about an object, assign a label to it

3. *Unsupervised Learning*

  Clustering, and dimensionality reduction are prominent examples

&nbsp;

## Supervised Learning

Formally, let $\mathcal{X}$ be the input space and $\mathcal{Y}$ be the output space. We would like to obtain a function $f$ belonging to the function family $\mathcal{F}$ such that $y_i \approx f(x_i)$, where $(x_i, y_i) \in \mathcal{X} \times \mathcal{Y}$.

In linear regression, $\mathcal{F}$ is the *Linear Function Space*.

It is not guaranteed that the training data is error-prone. We would like the final estimator to be robust to errors, and one way to do this is **Data Cleansing** (pre-processing).

### Error Function

The error function $\mathcal{E}$ takes the curve and data as input and yields a real number as the output. This is used to quantitatively judge whether a function is a "good fit" for the given data.

Some examples of $\mathcal{E}$ are $\sum \vert f(x_i)-y_i\vert$ and $\sum (f(x_i)-y_i)^2$. We would ideally want the error to always be positive (so that positive and negative errors doesn't cancel out).

Using the error function $\sum (f(x_i)-y_i)^2$ is known as the  **Method of Least Squares**, or **Ordinary Least Squares** (OLS).