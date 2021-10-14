---
title: Reinforecment Learning
permalink: /notes/cs747/week8_2
classes: wide
author_profile: false
sidebar:
    nav: "notes_cs747"
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

We shall focus on the first-visit Monte Carlo method for now. We've already defined the estimate of the value of the state to be given by:

$$\begin{align}
\hat{V}^t(s) &= \frac{1}{t}\sum_{i=1}^t G(s,i,1) \\
&= \frac{1}{t}\left( (t-1)\hat{V}^{t-1}(s) + G(s,t,1) \right) \\
&= (1-\alpha_t)\hat{V}^{t-1}(s) + \alpha_t G(s,t,1) \quad \alpha_t = 1/t \\
\end{align}$$

We know that $\hat{V}^t(s)$ converges when $\alpha_t = 1/t$. What about other values, does the value estimate converge then?

&nbsp;

### Stochastic Approximation

The value estimate converges ($\lim_{t\to\infty} \hat{V}^t\to\hat{V}^\pi$) iff $\sum_i\alpha_t = \infty$ and $\sum_i \alpha_t^2 < \infty$.
{: .notice--info}

This is called as the **On-Line** implementation of the monte-carlo algorithm.

&nbsp;

## TD-0 Algorithm

In MC methods, we wait for the episode to end before updating. However, we could update the state just after making an action. That is, consider the following history:

$$ s_1, 2, s_2, 1, s_3, 3, s_T $$

The updated estimate for $s_1$ would be given by:

$$ \hat{V}^{t+1}(s_1) = (1-\alpha_{t+1})\hat{V}^t(s_1) + \alpha_{t+1}\[ 2+\gamma+3\gamma^2 \] $$

However, we can instead update the estimate of $s_1$ right after making the first action by using the estimated value of $s_2$ as follows:

$$ \hat{V}^{t+1}(s_1) = (1-\alpha_{t+1})\hat{V}^t(s_1) + \alpha_{t+1}\[ 2+\gamma\hat{V}^t(s_2) \] $$

This estimate is called the **Bootstrapped Estimate**. Do note that $\hat{V}(s_T)$ is set to 0, and is not updated for episodic tasks.
{: .notice--warning}

This is the main philosophy of TD(0) algorithms, the estimated value of the state is updated everytime an action is taken.

Usually, the data which is provided to us is small, meaning that the value obtained after iterating through it would depend on the random initial policy used. To circumvent this, we iterate over the entire dataset *multiple times*, and the value function obtained like this is given by $\hat{V}^t_{batch\_TD}(s)$.

&nbsp;

## Convergence of MC and TD-0 Algorithms

It can be seen quite easily from the definitions of MC algorithms that the MC algorithms converge least square solution which minimizes a cost function.

$$\begin{align}
  \hat{V}^t(s) &= \frac{\sum_i G(s,i,1)}{\sum_i 1(s,i,1)} &= \underset{V}{\operatorname{argmin}} \sum_i 1(s,i,1)\[ V(s)-G(s,i,1) \]^2 \\
\end{align}$$

Similarly, it turns out that the value function the TD-0 algorithm converges to is the **MLE** estimate for the given data!
{: .data--info}

&nbsp;

## Control with TD Learning

Recall that in the control problem, we would like to reach the optimal policy and not just calculate the value functions. To tackle this, we maintain an *Action-Value* function instead of just a value function.

- *Q-Learning*: $r^t + \gamma\max_a \hat{Q}^t(s^{t+1},a)$
- *Sarsa*: $r^t + \gamma \hat{Q}^t(s^{t+1},a^{t+1})$
- *Expected Sarsa*: $r^t + \gamma\sum_a \pi^t(s^{t+1},a)\hat{Q}^t(s^{t+1},a^{t+1})$

Q-Learning is called *Off-policy* wheras Sarsa and Expected Sarsa are called *On-policy* learning algorithms.
{: .notice--info}

If the underlying policy is $\epsilon$-greedy, all three algorithms converge to the same Q function. However, if the policy is time-invariant, then Sarsa and Expected Sarsa converge to the policy but Q-Learning converges to its epsilon greedy equivalent!

Also note that these three algorithms are model-free!