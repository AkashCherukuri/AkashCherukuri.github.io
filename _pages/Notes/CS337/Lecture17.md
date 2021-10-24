---
title: Overfitting in Neural Networks
permalink: /notes/cs337/Lec17
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

One can represent any **smooth** function to any desired accuracy using a single hidden layer of sufficient size.
{: .notice--info}

We can counter this using already learnt methods such as L1 and L2 regularization. However for neural networks, we can avoid overfitting using smart network design. More specifically, we shall look at usage of Convolutional Neural Networks for image related tasks.

&nbsp;

## Convolutional Neural Networks

*filters, stride, padding*

We would like the learn the weights for each of the filters. Convolution improves upon fully connected layers in the following ways:

- sparse interactions
- parameter sharing
- equivariant representations, with $f(g(x)) = g(f(x))$ where $f$ is convolution and $g$ is shift function

&nbsp;

### Number of parameters

Let the given input given by $M\times N\times D$, upon which convolution is performed using a patch of size $P\times Q$ with stride $S$ and number of channels $C$, and padding $D$. 

1. **Number of parameters**
  $$ (P\cdot Q\cdot D)\times C $$

2. **Number of Neurons**
$$ \left(\frac{M-P+2D}{S}\right)\left(\frac{N-Q+2D}{S}\right)(C) $$

