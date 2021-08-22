---
title: Linear Regression
permalink: /notes/cs337/Lec2
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

Regression is about learning to predict a set of output (*dependent*) variables as a function of input (*independent*) variables.

Consider the inputs to be of form $\<x_i, y_i\>$. *Attributes* of $x$ are (non-linear) functions $\phi$ which operate on $x$. An equation which linear regression tries to optimize is:

<div style="text-align: center;">
  $$ Y = \sum_{i=1}^n w_i\phi_i(x) + b = W^T\Phi(x) + b $$
</div>

Where $\Phi$ is a vector of all attributes, and $W$ of all weights.

Do note that $b$ can be dropped by defining $\widetilde{w}, \widetilde{\Phi}$ with one additional element being $b$ and $1$ respectively.

Linear regression is linear in terms of weights and attributes, and (generally) non-linear in terms of $x$ owing to $\Phi$.
{: notice--warning}

For example, $\phi_1(x)$ could be the date of investment, $\phi_2$ could be value of investment and so on.

There are general classes of basis functions, such as:
- Radial Basis function
- Wavelet function
- Fourier Basis

### Formal Notation

Dataset $\mathcal{D} = \<x_1, y_1\> \ldots \<x_m, y_m\>$.

Attribute/basis functions $\phi_i$, and the general class of basis $\Phi$ is given as shown below. Do note that we have redefined the value of $\Phi$ now, and we shall be using this definition from here on.

<div style="text-align: center;">
  $$\Phi = 
  \begin{bmatrix}
    \phi_1(x_1) & \phi_2(x_1) & \ldots & \phi_p(x_1) \\
    \vdots      &             &        &             \\
    \phi_1(x_m) & \phi_2(x_m) & \ldots & \phi_p(x_m) \\
  \end{bmatrix}$$
</div>

The equation with the above redefinition becomes finding an optimal $W$ such that $Y = \Phi W$.

**General regression** is the following problem;

<div style="text-align: center;">
  $$\hat{f} = \min_{f\in\mathcal{F}} E(f, D)$$
</div>

**Parameterized Regreesion** is a bit more complex, it involves the optimization of weights in the above definition for a given $f(\phi(x), w, b)$ for minimizing error.

<div style="text-align: center;">
  $$ w* = \min_{w,b} \left[ E(f(\phi(x), w, b), D) \right] $$
</div>

The error function determines the type of regression. Some examples are given below. These will be discussed later in the course.

- Least Squares Regression
- Ridge Regression
- Logistic Regression


## Least Square Solution

Formally, the solution is given by:

<div style="text-align: center;">
  $$ w* = \min_{w,b} \sum_{j=1}^m \left( \left( \sum_{i=1}^p w_i\phi_i(x_j) + b - y_j \right)^2 \right) $$
</div>

If the "true" relation between $X$ and $Y$ was linear in nature, then 0 error is attainable. That is, $y = \Phi W$ exists, or **Y belongs to the column space of Phi**. We can just solve linear equations to get the optimal value of $W$.

If $Y$ is not in the column space of $\Phi$, the closed form solution for optimal weights $W\*$ is given by:

<div style="text-align: center;">
  $$W* = \left(\Phi^T\Phi\right)^{-1}\Phi^TY$$
</div>

Do note that $\Phi^T\Phi$ is invertible iff it has full column rank. That is:
- All columns are linearly independent of each other
- The columns are not data driven

It can be proven that Gradient Descent converges to the same solution as well.