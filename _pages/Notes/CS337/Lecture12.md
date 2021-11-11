---
title: Unsupervised Learning
permalink: /notes/cs337/Lec12
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

The methods discussed so far, regression and classification were supervised in nature. This is because the $y_i$ is provided for every datapoint.

We shall now look at a few unsupervised learning methods, where only $x_i$ are provided to the model.

&nbsp;

## Dimensionality Reduction

> "All other things being equal, pick the simplest solution" - Occam's Razor

That is, we would like to find the "true dimensionality" of the given model. We like having fewer dimensions because:

- Easier to learn
- Solves overfitting

That is, we would like to convert $x\in\mathcal{R}^d$ to $z\in\mathcal{R}^k$ where $k\text{ }<<\text{ }d$.

$$ z = U^T x $$

$U$ is a $d\times k$ *Projection Matrix*. We also want $U^TU = I_k$. Note that $UU^T$ need not be identity at all.

This implies that reconstructing a point from $z$ dimension is lossy, because the correlation is only approximate. That is, if $z = U^Tx$ and $\tilde{x} = Uz$, then $\tilde{x}$ need not be equal to $x$.
{: .notice--info}

&nbsp;

### Principal Component Analysis

PCA-1 aims to minimize the squared loss error between the actual data and the reconstructed data. $U^TU = I_k$ must be satisfied.

$$ U = \underset{U}{\operatorname{argmin}} \sum_x \vert\vert x - UU^Tx \vert\vert ^2 $$

Here is another way of approaching the same problem, dubbed PCA-2.

We assume that the datapoints are centered, with $\mathcal{E}\[x\] = 0$. (Just shift the origin)

PCA-2 aims to maximize the variance of the data in the new hyperplane. Do note that $U^TU=I_k$ must hold here as well.

$$ U = \underset{U}{\operatorname{argmax}} \mathcal{E}[\vert\vert U^Tx \vert\vert^2] $$

This is related to the eigen value decomposition.The dimension $k$ is determined by the 

It can be proven that both PCA-1 and PCA-2 are equivalent. Let $C =\Phi\Phi^T $ be the covariance matrix of the given data $\Phi$. Note that $C$ is $n\times n$, where $n$ is the number of datapoints given.  

The vectors corresponding to the dimensional projection are the first $k$ **Eigen Vectors** of $C$ when arranged in descending order of their corresponding Eigen Value. The data needs to be then projected along these eigen vectors.
{: .notice--info}

&nbsp;

### PCA with Kernels

Let the data matrix be given by $X$ ($\Phi$). Assuming that $X$ is psd, the Singular value decomposition of $X$ can be given by $ X = ADB^T $. From this, we can say that:

$$\begin{align}
  nC &= XX^T &= AD^2A^T \\
  \mathcal{K} &= X^TX &= BD^2B^T \\
\end{align}$$ 

Where $\mathcal{K}$ is the kernel matrix. Therefore, we can see that the eigen vectors obtained after eigen value decomposition of the kernel matrix lead to the **projection of the data on the principal components**. (That is, we previously obtained the components and then projected the data along these components. In this method however, we get the projected data directly and we do not obtain the components themselves.)