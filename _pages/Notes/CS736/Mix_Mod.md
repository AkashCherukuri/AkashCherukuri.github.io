# Mixture Models

A statistical model to represent a general multimodal PDF. Assumes that the data is drawn from multiple subgroups (mixture). That is, we model distributions as convex combination of standard distributions (Gaussian, for example).


$$
\begin{align*}
p(x) &= \sum_{k=1}^K w_kp_k(x) \\
\sum_{k=1}^K w_k &= 1
\end{align*}
$$


The weights are positive, and sum up to one to ensure that the net integral of the summation is one as well.

- **Finite Mixture Model** - $K$ is finite
- **Gaussian Mixture Model** - Each PDF is a gaussian distribution. A GMM can model uni modal, multi modal, and curved distributions



### Fitting GMM to data - Maximum Likelihood

Given the data $y=\{y_n\}$, we try to fit a GMM of $k$ components to this data.


$$
P(x) := \sum_{k=1}^K w_k G(x;\mu_k, C_k)
$$


The parameters involved here are $\theta = \{w_k, \mu_k, C_k\}_{k=1}^K$. The likelihood, and the corresponding log-likelihood function would be given by the following equation. Notice that we cannot get a closed form solution because of the summation. Gradient descent converges quite slowly, so we introduce a new strategy for dealing with this.


$$
\begin{align*}
	LL(\theta\vert y) = \sum_{n=1}^N\log\left( \sum_{k=1}^K w_k G(x;\mu_k, C_k) \right)
\end{align*}
$$


#### Expectation Maximization (EM) Optimization

This is an iterative algorithm where a closed form solution is obtained in each iteration. It introduces the notion of a “hidden” random variable $X_n$ which we assume was missed when obtaining the data. Therefore, the complete data would be given by $\{(x_n, y_n)\}$.

We then marginalize over this introduced hidden variable.


$$
\max_{\theta}P(y\vert\theta) = \max_\theta\int_xP(y,x\vert\theta)dx
$$


Let the parameters at iteration $i$ be $\theta_i$.

##### E Step

Design a new function of parameters $F(\theta ; \theta_i)$ such that

1. $F$ is a lower bound for the Log-Likelihood function
2. $F$ touches the log likelihood function at current estimate $\theta_i$

##### M Step

Choose the new parameter estimates $\theta_{i+1}$ to be where the previously defined function $F$ has a maximum. (Or at least, greater than the value in the previous iteration)

*using entropy and KL in EM*



The algorithm is terminated when the change in $\theta$ falls below a user-defined threshold. (Computing the entropy part is computationally intensive)



### GMM Using EM

Let the hidden data be modeled by the random variable $Z=\{z_n\}$.

*Q(theta,theta_i) entropy and KL stuff*