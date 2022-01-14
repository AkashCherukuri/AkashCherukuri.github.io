---
title: Texture Modeling
permalink: /notes/cs736/Lec3
classes: wide
author_profile: false
sidebar:
    nav: "notes_cs736"


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

We try to learn a bank of textures using which one would be able to model any texture as a linear combination of these stored textures. This idea is analogous to the wavelet basis methodology. Unlike wavelet models whose basis were mathematically defined, the texture bank is learnt from data. This method is called as Dictionary Learning.

Consider the simple case of linear regression

$$
Ax = b
$$

<div style="text-align: right;">
$b$ - observed data, $A$ - known system matrix
</div>

There are two problems here:

1. Which solution to pick if multiple solutions exist? (under constrained)

2. Overfitting (noisy data / over constrained)

**Priors, regularization** are the tools used to solve the above problems. *Ridge regression* is an example of a popular regularization technique where the 2-norm is minimized. The objective function in ridge regression is quadratic, meaning that finding the optimal value is easy.

$$
\text{Ridge} = \min \{\vert\vert Ax-b\vert\vert^2 + \vert\vert \Gamma x\vert\vert^2 \} \\
\hat{x} = (A^TA + \Gamma^T\Gamma)^{-1}A^Tb
$$

The Bayesian interpretation would be a gaussian prior with mean 0 and covariance $(\Gamma^T\Gamma)^{-1}$.

*Lasso Regularization* instead proposes using L1-norm instead of the L2-norm. Note that this objective function has no closed form solution, meaning that gradient descent must be used. The equivalent prior is the Laplacian distribution.

&nbsp;

# Dictionary Learning

One of the techniques earlier discussed was Dictionary Learning. This problem can now be formally defined as follows.

- Data Sample - $X = [x_1, \ldots x_K]$ where $X\in \mathcal{R}^d$
- Dictionary      - $D\in\mathcal{R}^{d\times n}:D=[d_1,\ldots d_n]$ (each column is an "atom")
- Coefficient Vectors - $R = [r_1,\ldots r_K]$ where $R\in\mathcal{R}^n$

$$
\text{arg}\min_{D\in C, r_i\in\mathcal{R}^n} \left[ \sum_{i=1}^k\vert\vert x_i-Dr_i\vert\vert^2_2 + \lambda\vert\vert r_i\vert\vert_0\right] \\
C = \{ \mathcal{D}\in\mathcal{R}^{d\times n} : \vert\vert d_i \vert\vert_2\leq 1 \forall i \}
$$

The condition $\mathcal{C}$ is required to avoid trivial solutions where $r_i\to0$ and $D\to\infty$ which is not what we want. The regularization parameter can be changed on a case-by-case basis.