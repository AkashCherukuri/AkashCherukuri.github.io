---
title: Numerical Differentiation and Integration
permalink: /notes/ma214/diff_int
classes: wide
author_profile: false
sidebar:
    nav: "notes_ma214"


---

One of the simplest and easiest ways to approximate the value of $f’(x_0)$ would be to use the definition of derivative.


$$
f'(x_0) = \lim_{h\to 0}\frac{f(x_0+h)-f(x_0)}{h}
$$
 

Using a small enough $h$ should be sufficient to get a good approximation of the function’s derivative. But how small is “good enough”? To answer this question, we perform error analysis by assuming the line between the points at $x_0$ and $x_0+h$ to be a Lagrangian approximation. The error turns out to be:

$$
\left\vert f'(x_0) - \frac{f(x_0+h)-f(x_0)}{h} \right\vert= \frac{1}{2}\vert h f''(\xi(x))\vert
$$


### (n+1) Point Formula

Instead of using the naïve algorithm, the Lagrange polynomial can be differentiated to get an approximation of the derivative. Let the data be $\{ x_0,\ldots x_n \}$ and we would like to compute the derivative at $x_j$. It would be given by:


$$
f'(x_j) = \sum_i f(x_i)L_i'(x_j) + \frac{f^{(n+1)}(\xi(x_j))}{(n+1)!}\prod_{i\neq j}(x_j-x_i)
$$


![image-20220225225923591](E:\Github\AkashCherukuri.github.io\assets\images\typora\image-20220225225923591.png)

![image-20220225230317356](E:\Github\AkashCherukuri.github.io\assets\images\typora\image-20220225230317356.png)



It isn’t possible to reduce $h$ to an absurdly low value because round off errors become predominant in that case. The net error in the case of three point midpoint formula is given by $h^2M/6 + \epsilon/h$.

Therefore, we conclude that the $(n+1)$ point formula is **unstable** in nature.



&nbsp;



# Numerical Integration

The most basic method to approximate an integral is called **Numerical Aperture**. It involves using a summation.


$$
\int_a^bf(x)dx \approx \sum_{i=1}^n a_if(x_i)
$$


The Lagrange interpolating polynomial can be used to great effect here. For data $\{x_0,x_1\ldots x_n\}$ the polynomial and the corresponding numerical aperture approximation would be given by:


$$

$$
