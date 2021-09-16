---
title: Logistic Regression
permalink: /notes/cs337/Lec9
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

We've been taking the label of an input to be predicted by $\text{sign}(W^\text{T} \phi)$ in the binary classification problem. In logistic regression, we shall take it to be given by $\sigma (W^\text{T} \phi)$.

$$ \sigma(x) = \frac{1}{1+e^{-x}} $$

In general, $f_w(x) = \Omega (W^\text{T} \phi(x))$ where $\Omega$ is called the *Activation function*.

In the case of binary classification using logistic regression, we shall take the value of $\sigma$ to be the *probability* of the label being 1. We can thus take the value of $w^\*$ to be the MLE estimate via this assumption.

$$\begin{align}
  w^* &= \text{arg}\max_W \prod_i \sigma(W^\text{T} \phi(x_i))^{y_i}(1-\sigma(W^\text{T} \phi(x_i)))^{1-y_i}\\
      &= \mathcal{L}(Data, W)\\
\end{align}$$

We define *Cross Entropy Loss Function* $E$ to be equal to $(-1/m)\log(\mathcal{L}(Data, W))$. Notice that maximising Log-likelihood or minimising this loss function are essentially the same thing. Upon simplification, the loss function turns out to be:

$$
E(w) = -\frac{1}{m}\left[ \sum_i \left(y_iW^\text{T}\phi_i - \log(1+\exp(W^\text{T}\phi_i))\right) \right]
$$

No closed form solution exists for the cross entropy loss function. We thus have to resort to gradient descent. The update rules for Gradient descent and Stochastic gradient descent respectively are given below.

$$\begin{align}
  W^{k+1} &= W^k + \eta \left[\frac{1}{m} \sum_i (y_i - \sigma_{w^k}(x_i))\phi_i \right] \\
  W^{k+1} &= W^k + \eta\text{ } (y_i - \sigma_{w^k}(x_i))\phi_i \\
\end{align}$$
 

## Regularised Logistic Regression

Similar to what has been done in Linear regression, we just add an additional term to the regularised loss function. The loss function now would be:

$$
E(w) = -\frac{1}{m}\left[ \sum_i \left(y_iW^\text{T}\phi_i - \log(1+\exp(W^\text{T}\phi_i))\right) \right] + \frac{\lambda}{2m}\vert\vert w\vert\vert^2_2
$$

The above loss is obtained by assuming a gaussian prior on the weight vector, $W\sim\mathcal{N}(0,1/\lambda)$

It can be easily calculated that each of the update rules now have an additional term corresponding to the derivative of the penalisation term. The update rules for normal and stochastic are:

$$\begin{align}
  W^{k+1} &= W^k + \eta \left[\frac{1}{m} \sum_i (y_i - \sigma_{w^k}(x_i))\phi_i - \lambda W^k \right] \\
  W^{k+1} &= W^k + \eta\text{ } (y_i - \sigma_{w^k}(x_i))\phi_i - \eta\lambda W^k \\
\end{align}$$

## Extension to Multiclass

We've been discussing the case of binary classification, where the number of classes are 2. Now, let there be $K$ classes. We would need $K-1$ weight vectors in this case, as the $K^{th}$ class is just the negation of all the others. Let the $K-1$ weight vectors be given by $w_1,\ldots w_{k-1}$.

$$\begin{align}
  \mathcal{P}(y=c\vert \phi) &= \frac{e^{-w_c^\text{T}\phi}}{1+\displaystyle\sum_{j=1}^{K-1}e^{-w_j^\text{T}\phi}} \\
  \mathcal{P}(y=K\vert \phi) &= \frac{1}{1+\displaystyle\sum_{j=1}^{K-1}e^{-w_j^\text{T}\phi}} \\
\end{align}$$

We can have $K$ weight vectors with a little modification to the above formula, but it usually is not necessary. The probability equation in this case is given by:

$$
  \mathcal{P}(y=c\vert \phi) = \frac{e^{-w_c^\text{T}\phi}}{\displaystyle\sum_{j=1}^{K}e^{-w_j^\text{T}\phi}}
$$
