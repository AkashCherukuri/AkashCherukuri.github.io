---
title: Kernel Perceptrons
permalink: /notes/cs337/Lec10
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

The update rule for a perceptron has been discussed earlier. It is given by:

$$\begin{align}
  w^{k+1} &= w^k + \eta y'\phi(x') \\
  \implies f^{k+1}(x) &= sign\left(f^k(x) + y'\phi^\text{T}(x')\phi(x)\right) \\
  \implies f^{k+1}(x) &= sign\left(f^0(x) + \sum_{x',y'} y'\phi^\text{T}(x')\phi(x) count(x')\right)\\
\end{align}$$

$count(x)$ is the number of times that $x'$ has been misclassified so far. Notice that $\phi^\text{T}(x')\phi(x)$ is a dot-product, which is akin to a measure of similarity between them both.

We can redefine this to obtain a non-linear update function, as given below!

$$f(x) = sign\left( b + \sum_i y_i \alpha_i K(x_i, x) \right)$$

$\alpha$ is a vector initialized to 0s, and corresponding element is incremented by 1 if it is misclassified. (It stores $count$)

$K(x_i, x)$ replaces $\phi^\text{T}(x')\phi(x)$, and it is the "relation" between the given two datapoints.

Some examples of kernels are:

1. **Linear:** $K(x,y) = x^\text{T}y$
2. **Polynomial:** $K(x,y) = \left(1+x^\text{T}y\right)^2$
3. **Radial Basis:** $K(x,y) = exp(\vert\vert x-y \vert\vert^2_2 / 2\sigma^2)$

This is used to find non-linear partitions between classes. Kernels operate on an implicit space, and are usually easier to compute than the linear separator in higher dimensional space.

&nbsp;

## Gram Matrices

For a given dataset $\{ x_1, \ldots x_m \}$, the Gram Kernel Matrix $\mathcal{K}$ is defined as follows:

$$\mathcal{K} = \begin{bmatrix}
  K(x_1, x_1) & K(x_1, x_2) & \ldots & K(x_1, x_m)\\
  K(x_2, x_1) & K(x_2, x_2) & \ldots & K(x_2, x_m)\\
  \vdots & \vdots & & \vdots\\
  K(x_m, x_1) & K(x_m, x_2) & \ldots & K(x_m, x_m)\\
\end{bmatrix}$$

Given a Gram matrix, the attribute vector can be obtained via Singular Value Decomposition. That is, we find a diagonal matrix $D$ and a matrix $U$ with $UU^T=I$ such that:

$$K = UDU^T = (UD^{1/2})(UD^{1/2})^T = \Phi\Phi^T$$

Therefore, for a Kernel matrix to be valid:
1. It needs to be symmetric
2. It needs to be Positive Semi Definite (for any $b\in\mathcal{R}^m$, $b^TKb\geq 0$)

### Mercer Kernel

A kernel which has the following property is said to be a Mercer Kernel. Do keep in mind that every mercer kernel is valid. (This follows from the mercer theorem, but the proof is not necessary for this course)

$$\int_x\int_y K(x,y)g(x)g(y) dx dy \geq 0 \text{ for all square-integrable functions } g(x)$$