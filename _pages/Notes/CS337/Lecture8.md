---
title: Analysis of Perceptron Algorithm
permalink: /notes/cs337/Lec8
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

The following claim can be proven mathematically.

**Claim.** If $\exists w^\*$ such that the given data is linearly seperable, then the perceptron algorithm will converge to a value $\hat{w}$ which classifies the entire data correctly.
{: .notice--info}

*Proof todo here*

&nbsp;

## Stochastic Gradient Descent

In normal gradient descent, we compute the value of $\nabla \mathcal{E}(\Phi W, Y)$ and update the value of the weight vector accordingly. 

In Stochastic gradient descent, we iterate over the entire data and update the weight vector at the $i^{th}$ iteration according to $\nabla \mathcal{E}(W^\text{T}\phi, y_i)$. It can be seen that the perceptron update rule follows stochastic gradient descent with the **Hinge Loss Function**.

$$ \text{Hinge Loss}(f_w(x), y)= \max(0, -yf_w(x))$$


### Deciding final weight vector

Using the finally obtained weight vector is not always a good idea, because the process is iterative in nature. Usually, one of these two methods is employed:

1. **Voted Perceptron:**
2. **Averaged Perceptron:**