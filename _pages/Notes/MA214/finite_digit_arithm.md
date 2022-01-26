---
title: Introduction to Numerical Analysis
permalink: /notes/ma214/intro_to_num
classes: wide
author_profile: false
sidebar:
    nav: "notes_ma214"


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

We study the various methods of solving equations, approximating functions and study the errors corresponding to the aforesaid methods. For example, consider the approximation of $e$ using its definition and the Taylor’s Series.


$$
\begin{align*}
e &= \lim_{n\to\infty}(1+1/n)^n \\
f(x) &= f(a) + f'(a)(x-a) + \ldots+ \frac{f^{(k)}(a)}{k!}(x-a)^k + \frac{f^{(k+1)}(c)}{(k+1)!}(x-a)^{k+1}
\end{align*}
$$


Where $c$ is a real number between $x$ and $a$. We can also compute the number of terms that are required in the Taylor’s series to estimate its value with a given error using the final term.



### Finite Digit Arithmetic

A $64$ bit representation is generally used for a real number. The smallest magnitude possible by this representation is when $(s,c,f) = (0,1,0)$. Note that the tuples $(0,0,0)$ and $(1,0,0)$ represent $0$ and not $2^{-2013}\cdot 1$.

| Bits | Symbol | Name           | Use                                  |
| ---- | ------ | -------------- | ------------------------------------ |
| 1    | $s$    | Sign Indicator | Indicating whether the number is +/- |
| 11   | $c$    | Characteristic | Exponent of the number               |
| 52   | $f$    | Mantissa       | Fractional part of the number        |

$$
\text{Number} = (-1)^s\cdot 2^{c-1023}\cdot (1+f)
$$

![image-20220126175545918](..\..\..\assets\images\typora\image-20220126175545918.png)

![image-20220126175555508](..\..\..\assets\images\typora\image-20220126175555508.png)





### Floating Point Representation

We shall represent numbers in the form:


$$
\pm 0.d_1d_2\ldots d_k\times 10^n \qquad \text{where }1\leq d_1\leq9, 0\leq d_i\leq9
$$


If a number has greater than $k$ digits, we can bring it down by two methods:

1. **Chopping**: All digits from $d_{k+1}$ are dropped
2. **Rounding**: We add $5\times 10^{n-(k+1)}$ to the number and then drop the additional digits

There are two ways of finding the error of such approximations. Let $p$ denote the actual value and $p^*$ denote the approximated value.

1. **Absolute** - $\vert p-p^* \vert$
2. **Relative** - $\vert p-p^* \vert/p$

Relative error is usually the better measure as it takes the actual value of $p$ into account.



### Significant Digits

We say that the number $p^*$ approximates $p$ to $t$ significant digits when $t$ is the largest non-negative integer such that


$$
\frac{\vert p-p^* \vert}{p} < 5\times 10^{-t}
$$


That is, the number of significant digits **NEED NOT BE EQUAL** to the number of decimal places that a number has!

{: .notice–info}





## Errors Caused by Finite Digit Arithmetic

There are two main kinds of errors that are caused by the limitations of finite digit arithmetic, cancellation of nearly equal numbers and division by small numbers.

Consider the function $f(x) = 1-Cos(x)$ at $x = 1.2\times 10^{-5}$. The value of $Cos(x)$ would be $\text{0.999 999 999 9}$ with $10$ digits, however, the function value equates to $\text{0.000 000 000 1}$. We had started with $10$ significant digits but ended up with only $1$ by the end. The relative error that we get in this case would be very large.


$$
\frac{\vert1-Cos(1.2\times 10^{-5}) - \text{0.000 000 000 1}\vert}{1-Cos(1.2\times 10^{-5})} = 0.3889
$$


Errors also get magnified when divided with small numbers. For example, let $a^* = a+\epsilon$ be the approximation with error $\epsilon$. When divided by $b=10^{-n}$ we can see that the error has increased drastically. 


$$
fl\left(\frac{fl(a)}{fl(b)}\right) = (a+\epsilon)\times 10^n
$$


In the quadratic roots formula, we can rationalize it to avoid errors incurred when $b^2$ is very large compared to $4ac$. We use the first formula if $b>0$ and use the second formula if $b<0$.


$$
\frac{-2c}{b+\sqrt{b^2-4ac}} \qquad\qquad \frac{-2c}{b-\sqrt{b^2-4ac}}
$$


Instead of getting $0$ outright, we now get $-2c/b$ which is an improvement. This is highly case-specific however, and more ways of avoiding errors will be discussed subsequently.