---
title: Classification using Perceptrons
permalink: /notes/cs337/Lec7
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

We would like a classifier which maps a data point to one of the given classes. Linear regression is not viable here as the classes are NOT REAL!

A (bad) solution is to assign numbers to classes, but this **imposes ordering to the classes**, which is not ideal. We use *perceptrons* for this case, and the classes are modeled as one-hot encoded vector.

To start off, we shall tackle a **Binary Classification Problem** where the classes are represented by $+1$ and $-1$.

For input attributes $\phi$ and learnt weights $w$, the hyperplane which seperates the two clasess would be given by $w^\text{T}\phi = 0$. We look at the perceptron algorithm for learning the weights.

That is, $y_{pred}=1$ if $w^\text{T}\phi>0$ and $y_{pred}=-1$ if $w^\text{T}\phi<0$. Do note that $w^\text{T}\phi$ is the perpendicular signed distance from the hyperplane.

## Perceptron Algorithm

We iterate over all the available data. For a given data point $\< x_i, y_i \>$;

- If classified correctly, do nothing
- Marginally correct weights if incorrectly classified.

$$ w^{t+1} = w^t + \eta y \phi $$

Note that $y \phi$ is *unsigned distance* as it is always positive. $\eta$ is the learning rate here.

The perceptron algorithm finds *any* hyperplane which correctly classifies the given data, **not the best** hyperplane. SVM is used to find the best hyperplane, this is one of the drawbacks of this method.
{: .notice--info}