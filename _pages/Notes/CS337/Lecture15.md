---
title: Neural Networks
permalink: /notes/cs337/Lec15
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

We'll be tackling non-linear classification now. We've already discussed the usage of kernels for such classification. However, domain knowledge is required for selecting a proper kernel for the given situation, which limits the applications.

Neural networks, on the other hand, act as *universal function approximators* which do not require as much domain knowledge.

In general, a series of mappings are used to obtain the desired results.

$$x\xrightarrow{f}y\xrightarrow{g}z\xrightarrow{h}\{c_1, \ldots c_k\}$$

&nbsp;

## Activation Functions

$$f(x) = g(w^Tx)$$

Here, $g$ is called the *Activation function*. Some examples of activation functions are:

- Sigmoid
- Tanh
- Linear
- ReLU: $\max(0,s)$
- Softplus: $\log(1+e^s)$, is the "differentiable version" of ReLU

The problem with sigmoid and tanh is that, their values are limited. ReLU and Softplus do not have this problem.

&nbsp;

## VC Dimensions

The cardinality of the largest set of points that $f(w)$ can **shatter** is its VC Dimension. A function is said to shatter a given set of points if, for all assignments of labels to those points there exists a $w$ such that $f_w$ perfectly evaluates the set.

The VC Dimensions of a linear separator in $\mathcal{R}^2$ is 3.

The VC dimensions of a threshold classifier in $\mathcal{R}$ is 1.
{: .notice--warning}

&nbsp;

## Designing Neural Networks

Neural networks have great expressive power owing to:

1. Non linearity of the activation functions
2. Cascaded non-linear activation functions

There are four main design choices that are to be considered while coding up a neural network. These are:

- Input Layer
- Number of Hidden layers and number of nodes per hidden layer
- Output layer
- Loss function

Do note that the activations at the hidden layers are not visible, even during training.