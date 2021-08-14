---
title: "Gryffin: Bayesian Optimization of Categorical Variables"
permalink: /notes/surp/gryff
classes: wide
author_profile: false
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

<!-- Notes Begin here -->

We formulate a chemical reaction as an optimization algorithm. The parameters associated can be either *continuous* or *categorical*. There exist methods such as **PHOENICS** for the optimization of continuous variables, but its pretty tough for applying the same for categorical variables. 

This is where **GRYFFIN** steps in, it tries to extrapolate the methods used for continuous variables to categorical variables.

Thus, to understand GRYFFIN we would have to first understand PHOENICS better.

## PHOENICS - Continuous Variable Optimization

Let the true function be represented by $f$, and our estimate of the function (*surrogate function*) so far be $\hat{f}$. A three layered bayesian neural network is used for this purpose.

This is done by sampling values, and the *acquisition function* $\alpha (z)$ tells us which value to sample at.

This is an iterative procedure, the following steps are done:
- $\alpha (z)$ proposes the optimal value at which to sample, $x'$
- Sample at $x'$, and rebuild $\hat{f}$ using the bayesian network
- We stop after a set number of iterations are done, or when convergence is reached



<!-- Fill in the gaps for the first part's lecture here! -->


## Extending to Categorical

For example, let there be three types of Ligands, *A* *B* and *C*. We can represent each of these ligands as a one-hot encoded vector, such as $(1,0,0)$ for Ligand *A*. 

We now assume the following:

The Ligands *A* *B* and *C* are sufficiently independant and descriptive enough of the "Ligand Space".
{. :notice--success}

We then try to represent the rest of the ligands as a vector. That is, another ligand *D* might be represented by the vector $(0.2, 0.3, 0.7)$, using the **Gumbel-SoftMax Distribution**.

> This is called as *Soft One Hot Encoding*

This method is not fool-proof though, it is plausible that our original assumption is not valid. That is, if *A* and *B* are similar in nature, there is a redundancy in the Ligand Space!

The issue of similarity is addressed by introducing a *descriptor space*.


### Descriptor Space

Incorporate domain knowledge to measure similarity! That is, we can plot the ligands on a 2d plot where the axes correspond to the HOMO-LUMO densities, and use the "distance" of a ligand *D* from each of these ligands to get the soft-one hot vector.

We would like the set of descriptors to have:

1. High correlation with the objective function
2. Number of descriptors should be small
3. Low pair-wise correlation amongst each other

It is quite difficult to manually select a large number of descriptors which folow the above pair of rules.

What the paper did was just send the descriptor vector into a neural network with a single hidden layer and softsign activation to get a descriptor output vector, of smaller size.


