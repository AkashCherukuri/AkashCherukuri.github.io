---
title: "Basic Methods"
permalink: /notes/dl/basic
classes: wide
author_profile: false
sidebar:
    nav: "notes_soc"
---

---
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML" async></script>
## Linear Regression

The main aim is to estimate a linear equation representing the given set of data. There are two approaches to this.   

1. A closed form solution.  
   This can be directly obtained by solving the linear differential equation. Calculate the partial derivative of the error function wrt x, y and equate both of them to zero to get the values of the parameters which minimizes the error function.
2. An iterative approach.  
   This is similar to **Gradient Descent**. We try to obtain the minima (L1, L2 norm etc) by calculating the gradient at each point and moving in small steps along the gradient vector. 
   Refer to [this](https://youtu.be/8PJ24SrQqy8) video for more details. 

### Logistic Regression

Refer to the following [link](https://towardsdatascience.com/logistic-regression-detailed-overview-46c4da4303bc) to see an example of logistic regression. 