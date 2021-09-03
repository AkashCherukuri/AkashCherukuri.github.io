---
title: Classification using Perceptrons
permalink: /notes/cs337/Lec6
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

