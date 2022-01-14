---
title: Image Priors
permalink: /notes/cs736/Lec2
classes: wide
author_profile: false
sidebar:
    nav: "notes_cs736"

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

*skipping over the proof for the equivalence of MRF and GRF*

 We have discussed earlier that images tend to be piecewise smooth. There are two general cases when the differences between the neighboring pixels is large:

1. Discontinuity - Likely edges in images
2. Outlier - a datum far from rest of neighborhood, eg "spotty" texture 

We want the MRF/GRF prior which allows such properties, and which doesn't assign a very low probability density to such configurations. Assigning a low probability will cause blurring during image denoising.

Lets start out with a simpler problem, lets model the prior on a **single pixel** given the neighborhood intensities of that pixel.

Let the pixel's intensity be $x$, the neighborhood be $N$ and the intensities of neighbors be $y_i$. We shall model the intensities as:

$$
y_i = x + \eta_i(i) \qquad \text{where }\eta_i(x)\text{ is deviation}
$$

Let the penalty function be $g(.)$, meaning that the penalty given the deviation would be $g(\eta_i(x))$. The "energy" function for this distribution would be:

$$
E(x) = \sum_i g(\eta_i(x))
$$

**Assumption** - **Even penalty function**

We would want $g$ to be even, so that no sign of deviation is favored over the other. We can therefore re-write the energy equation in terms of a new function $H(x)$ where $g(\vert x\vert) = H(\vert x\vert^2)$.

The derivative using chain rule would be:

$$
\frac{\partial g(x)}{\partial x} = \frac{\partial H(\vert x\vert^2)}{\partial x} = 2xH'(\vert x\vert^2) = 2x\cdot h(x)
$$

$h(x)$ is a newly defined function, and it is equal to $H'(\vert x\vert^2)$.

Computing the point where the derivative of $E(x)=0$, we get

$$
x = \frac{\sum_i h(\eta_i)y_i}{\sum_i h(\eta_i)}
$$

And therefore, the gradient descent update on $x$ with a step-size factor $\tau$ would be

$$
x^{n+1} = x^n + \tau \sum_i2\eta_ih(\eta_i)
$$

In both the cases, $h(\eta_i)$ acts like a weighting function. This property is used for finding how good of a choice the original penalty function $g(x)$ was. 

$h(x)$ acts as the weights in the first case, and $2xh(x)$ acts like a "force" in the second case.
{: .notice--info}

&nbsp;

### Analyzing penalty functions

We want the penalty functions to have the following properties, in addition to being continuous(1) , real-valued(2) and non-negative(3):

**Non-increasing**, with the following conditions:

- (4a) $\lim_{u\to\infty} h(u) = 0$
- (4b) $\lim_{u\to\infty}g'(u)\leq C$ where $C$ is a fixed positive constant



1. **Quadratic Penalty** - $g(x) = \vert x\vert^2$

   The value of $h(x) = 1$ for this choice. 

   As deviation $(\eta_i)\to \infty$, $h(\eta_i)$ remains a constant. This is would mean that the large deviation would significantly increase the energy of the distribution, meaning that this penalty function would smooth out all the edges present making the image blurry.



2. **Custom Function** - $g(x) = \gamma\exp(-\vert x\vert^2/\gamma)$

$$
\text{Huber's Function - } g(x) = 
\begin{cases}
\frac{\vert x\vert^2}{2} & x\leq\gamma \\
\gamma\vert x\vert - \frac{\gamma^2}{2} & x>\gamma 
\end{cases}
$$
