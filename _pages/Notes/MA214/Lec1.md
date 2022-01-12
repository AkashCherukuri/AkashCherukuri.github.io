---
title: Numerical Analysis
permalink: /notes/ma214/lec1
classes: wide
author_profile: false
# sidebar:
#     nav: "notes_cs337"

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
$$
e = \lim_{n\to\infty}(1+1/n)^n
$$
The value of $e$ is approximated using the infinitely differentiable exponential function $\exp(x)$ and the **Taylor's Theorem**. This series can be used to obtain the value to a required degree of precision. Note that $c\in (x,a)$.
$$
f(x) = f(a)+f'(a)(x-a) +\cdots+\frac{f^k(a)}{k!}(x-a)^k + \frac{f^{k+1}(c)}{(k+1)!}(x-a)^{k+1}
$$
The final term when approximating the value of $e$ would be:
$$
\frac{e^c}{(n+1)!}
$$
We know that $e^c<3$ when $c\in (0,1)$. We can thus obtain the value of $e$ to a required degree of error by choosing an appropriate value of $n$. We can similarly compute the value of $e^a$ to any required degree of accuracy.





