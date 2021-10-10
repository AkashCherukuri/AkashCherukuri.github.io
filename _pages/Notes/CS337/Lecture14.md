---
title: SVM
permalink: /notes/cs337/Lec14
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

We've discussed the perceptron algorithm already. However, there are a few drawbacks for this method:

- Does not find the best seperating hyperplane
  *Soln*: Large margin classification

- Sigmoidal perceptron can seperate only address linearly seperable data

We shall tackle the first drawback now. The second drawback will be discussed in the next lecture.

## Support Vector Machines

Provide breathing space to perceptron algorithm to have better seperating planes.

$$\begin{align}
w^T\phi(x)+b \geq +1 & \text{ for } y(x) = +1 \\
w^T\phi(x)+b \leq -1 & \text{ for } y(x) = -1
\end{align}$$

For such a case, the *margin* is given by $2/\vert\vert w\vert\vert$. The margin is the distance between both the displaced planes.

However, points need not be linearly seperable, meaning the above equations are not guaranteed to hold. We thus add a new term called *slackness* represented by $\xi$.

$$\begin{align}
w^T\phi(x_i)+b \geq +1-\xi_i & \text{ for } y(x_i) = +1 \\
w^T\phi(x_i)+b \leq -1+\xi_i & \text{ for } y(x_i) = -1 \\
& \xi_i \geq 0 \\
\end{align}$$

SVM tries to maximise the margin, and minimize $\sum\xi_i$.