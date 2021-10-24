---
title: Convolutional Neural Networks
permalink: /notes/cs337/Lec18
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

The "depth" is typically increased as the size of the image is shrunk by pooling and filters to prevent loss of data. This increment is caused by using multiple filters, which are learnt by training.

Ultimately, we perform softmax in the final layer to get probability of each class.

## Pooling layer

Usually, $\max$ is used for dimensionality reduction via down-sampling of the input. This reduces overfitting and translational invariance only sends important information to the next layer.

Padding is usually not done because it doesn't change the value. The output size is given by:

$$\left(\frac{M-P}{S}+1\right)\times\left(\frac{N-Q}{S}+1\right)$$

