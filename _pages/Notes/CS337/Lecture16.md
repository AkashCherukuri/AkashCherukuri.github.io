---
title: Neural Networks
permalink: /notes/cs337/Lec16
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

Adding hidden layers to the neural network causes the objective function to become non-convex. Further more, since the activations of the hidden layers are unobserved, we do not know what the function itself is! 

## Backpropogation Algorithm

This algorithms uses the *chain rule* and *memoization* for differentiating output layers wrt the internal layers.

Consider a network with one hidden layer, whose activation functions are represented by $g_1$ and $g_2$, and the output layer's activation is $f$. For inputs $x,y,z,w$ the output could be:

$$ output = f(w^2_1g_1(w^1_1x+w^1_2y)+w^2_2g_2(w^1_3z+w^1_4w)) $$

The derivative wrt $w^1_1$ can now be written as follows using the chain rule.

$$ \frac{\partial o}{\partial w^1_1} = \frac{\partial f}{\partial w^1_1} = \frac{\partial f}{\partial g_1}\frac{\partial g_1}{\partial w^1_1} $$

This is where memoization kicks in, we could store the values of these partial derivatives for use later speeding up the computations.

We memoize partial derivatives, products and sums of products.
{: .notice--info}

### Notation

The output layer is denoted as the $L$'th layer, and the hidden layers behind it are $l$'th, $l-1$'th and so on. (right to left)

$\sigma^l_i$ is the $i$'th activation layer (neuron) in the $l$'th layer. 

$w^l_{ij}$ is the weight connecting the $(i-1)$'th neuron in the $(l-1)$'th layer and $j$'th neuron in the $l$'th layer.

$\text{sum}^l_i$ is the input argument to $\sigma^l_i$, given by $\sum_t w^l_{ti} \sigma_t^{l-1}$.

Therefore, the L2 regularized objective function to be minimized is:

$$\begin{align}
E(w) &= -\frac{1}{m}\left[ \sum_i \sum_k y_k^{(i)}\log\sigma^L_k(x^{(i)}) + (1-y_k^{(i)})\log(1-\sigma^L_k(x^{(i)})) \\
&+ \frac{\lambda}{2m}\sum_l\sum_i\sum_j (w^l_{ij})^2 \\
\end{align}$$

That is, the objective function only looks at the output layer, but the regularization parameter penalizes ALL weights!
{: .notice--warning}

&nbsp;

### Equations for backpropogation

$$ \frac{\partial E}{\partial w^l_{ij}} = \frac{\partial E}{\partial \sigma_j^l}\frac{\partial \sigma_j^l}{\partial \text{sum}^l_j}\frac{\partial \text{sum}^l_j}{\partial w^l_{ij}} $$

The values of each individual partial derivative have been given below.

$$\begin{align}
\frac{\partial E}{\partial \sigma_j^l} &= \sum_p \frac{\partial E}{\partial \sigma_p^{l+1}}\frac{\partial \sigma_p^{l+1}}{\partial sum_p^{l+1}}\frac{\partial sum_p^{l+1}}{\partial w^l_{ij}} \\
\frac{\partial \sigma_j^l}{\partial \text{sum}^l_j} &= \text{(just differentiate the activation function)} \\
\frac{\partial \text{sum}^l_j}{\partial w^l_{ij}} &= \sigma_i^{l-1} \\
\end{align}$$

Note that the rhs of the first equation would have already been stored in the previous iteration of the algorithm.