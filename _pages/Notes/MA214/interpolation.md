---
title: Interpolation
permalink: /notes/ma214/interp
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



We will be focusing on interpolation using polynomial functions.



$$
P(x) = a_nx^n+a_{n-1}x^{n-1}+\ldots+a_0
$$



Given any continuous function $f:[a,b]\rightarrow\mathcal{R}$, there exists a polynomial that is as “close” to the given function as desired. This is called as the **Weierstrass Approximation Theorem**.
{: .notice–info}



One natural choice would be to use the polynomial obtained from the Taylor’s theorem. However, note that these polynomials approximate the function **only at a given point**. It is not guaranteed that the Taylor’s polynomials at higher degree would offer higher a better approximation. (Works for $e^x$ but not for $1/x$)



## Lagrange Interpolating Polynomials

Let $x_0, x_1, \ldots x_n$ be distinct $(n+1)$ points and let $f$ be a function with $f(x_i)=y_i$. We would like to find a polynomial $P$ such that $P(x_i)=y_i$

Define $L_{n,i}(x_j) = \delta_{i,j}$ where $\delta_{i,j}$ is $1$ iff $i=j$ and $0$ otherwise. We can define $L_{n,i}(x)$ as follows:



$$
L_{n,i}(x) = \frac{(x-x_0)(x-x_1)\ldots(x-x_{i-1})(x-x_{i+1})\ldots(x-x_n)}{(x_i-x_0)(x_i-x_1)\ldots(x_i-x_{i-1})(x_i-x_{i+1})\ldots(x_i-x_n)}
$$



Now that this term has been defined, we can easily write the interpolation function as:



$$
P(x) = y_0L_{n,0}(x)+y_1L_{n,1}(x)+\ldots+y_nL_{n,n}(x)
$$



We can say that a unique interpolation polynomial of degree $\leq n$ exists for a given set of $n$ points.



### Error of interpolation

Let $f:[a,b]\rightarrow \mathcal{R}$ be $(n+1)$ differentiable, and $P(x)$ be the interpolating polynomial given $(n+1)$ distinct points $x_0, x_1\ldots x_n$ where $x_i\in[a,b]$.

For each $x\in[a,b]$ there exists a $\xi (x)\in(a,b)$ such that



$$
f(x) = P(x) + \frac{f^{(n+1)}(\xi(x))}{(n+1)!}(x-x_0)(x-x_1)\ldots(x-x_n)
$$



### Neville’s Formula - Cumulative Computation

We would like to have a method in which the lower degree polynomials help in computing the higher degree interpolating polynomial. Consider the nodes $\{x_0, \ldots x_n\}$ with $Q_i(x)$ being the interpolation of all points except $x_i$ and $Q_j(x)$ being the interpolation over all points except $x_j$. The interpolation over the entire set of nodes is given by:



$$
P(x) = \frac{(x-x_j)Q_j(x) - (x-x_i)Q_i(x)}{x_i-x_j}
$$



This lets us build the interpolating polynomial from the ground up, one degree at a time. Let $P_{i,j,k,\ldots}$ denote the interpolating polynomial obtained from the $i$‘th, $j$’th, $k$‘th and so on points, we can see that:

![image-20220126103921259](../../../assets/images/typora/image-20220126103921259.png)

If we only care about the value of the interpolated polynomial, we don’t even need to calculate the polynomial itself; we can just replace $x$ in Neville’s formula with the required value. The value of $x$ here is $2.1$.

![image-20220126104135836](../../../assets/images/typora/image-20220126104135836.png)



### Divided Differences

This is another method of constructing the interpolated polynomial. Given $(n+1)$ nodes $x_0, x_1, \ldots x_n$, we can define a new function $f[x_0, x_1, \ldots x_n]$ which is the coefficient of $x^n$ in the interpolating polynomial. Note that the function is independent of the order of nodes.

We shall now try to construct a recursive relation over $f$. Let $P_{n-1}$ be the polynomial over $\{x_0, x_1\ldots x_{n-1}\}$ and $Q_{n-1}$ be the polynomial over $\{x_1, x_2\ldots x_n\}$. From Neville’s formula we can get the following:


$$
\begin{align*}
	P_n(x) &= \frac{(x-x_n)P_{n-1} - (x-x_0)Q_{n-1}}{x_0-x_n} \\
	f[x_0,\ldots,x_n] &= \frac{f[x_0,\ldots,x_{n-1}] - f[x_1,\ldots,x_{n}]}{x_0 - x_n}
\end{align*}
$$


We know that for $x_i\in\{x_0,\ldots x_{n-1}\}, P_n(x_i)=P_{n-1}(x_i)$, by definition of the interpolating polynomial. Therefore, $P_n - P_{n-1}$ is equal to $0$ at the aforementioned $n$ points.


$$
\begin{align*}
P_n - P_{n-1} &= \alpha(x-x_0)(\ldots)(x-x_{n-1}) \\
&= f[x_0, \ldots, x_{n}](x-x_0)(\ldots)(x-x_{n-1}) \\
\implies P_n &= P_{n-1} + f[x_0, \ldots, x_{n}](x-x_0)(\ldots)(x-x_{n-1}) \\ 
\end{align*}
$$


We can pre-compute the divided differences using the modified Neville’s formula and then use the above recursive formula to get the interpolating polynomial function recursively.

![image-20220126110256934](../../../assets/images/typora/image-20220126110256934.png)


$$
\begin{align*}
P_n &= f(x_0) + f[x_0,x_1](x-x_0) + f[x_0,x_1,x_2](x-x_0)(x-x_1)+\ldots \\
&= f(x_0) + (x-x_0)\left[ f[x_0,x_1] + (x-x_1)[f[x_0,x_1,x_2] + (x-x_2)[\ldots]]  \right]\\
\end{align*}
$$


Writing the recurrence relation in the nested form allows for efficient computation.



### Newton’s Difference as a function

**Theorem**

If $f$ is $n$-times continuously differentiable on $[a,b]$ then


$$
f[x_0, \ldots, x_n] = \frac{f^{(n)}(\xi)}{n!}
$$


for some $\xi\in[a,b]$



We would like to extend newton’s difference to be a function. From the modified Neville’s formula, we get that


$$
f[x_0, x] = \frac{f(x_0) - f(x)}{x_0 - x} \quad \text{where }x\neq x_0
$$


From the above theorem (extended MVT) and applying $\lim_{x\to x_0}$ we get the following base case for the function:


$$
f[x_0, x] = 
\begin{cases}
\frac{f(x_0) - x}{x_0 - x} & x\neq x_0 \\
f'(x_0) & x = x_0
\end{cases}
\qquad \text{ base case}
$$


We can now extend this base case to get the general function as shown in the below equation. Note that we would have to take care when there is equality between the nodes. **Divided differences function is continuous by induction**.


$$
f[x_0, \ldots, x_{n-1}, x] = f[x_0,\ldots,x,x_{n-1} ] = \frac{f[x_0,\ldots,x] - f[x_1, \ldots, x, x_{n-1}]}{x_0 - x_{n-1}}
$$

