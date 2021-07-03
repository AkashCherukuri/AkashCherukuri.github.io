---
title: "Deep Learning"
permalink: /notes/dl/dl
classes: wide
author_profile: false
sidebar:
    nav: "notes_soc"
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

---
[This book](http://neuralnetworksanddeeplearning.com/index.html) on deep learning has been followed, this section will contain nomenclature and a few key definitions I thought were important enough.

- `perceptrons`: older way of representing neural networks. Can give an output of either 0 or 1, corresponding to if the value of $w\cdot x+b$ is lesser than or greater than 0.
- `sigmoid neurons`: we usually change the values slightly in perceptrons to slowly approach the required classification function. However, because perceptrons are binary in nature, small changes can cause drastic (and unintended) changes to the output. Sigmoid neurons try to minimize this issue.

The standard sigmoid function is given as follows:

<div style="text-align: center">
	$$ \sigma (w\cdot x+b) = \frac{1}{1+exp(-w\cdot x-b)} $$
</div>	

That is, is is a smoothened out version of the step function. We can also see that the output changes linearly with changes in inputs (using partial derivatives). $(w\cdot x+b)$ is called as the "Weighted input" for that particular neuron, and is represented by $z$.


&nbsp; 


## MLP - Multi Layer Perceptrons 

These have **sigmoid neurons** as layers in them. The neurons taking input are called *input neurons* and comprise the *input layer*. Similarly, we have the output neurons and the output layer. Neurons (and layers) which are neither input nor output are called as **Hidden Layers**. We will be using a **feed-forward** neural network, meaning that the output of a layer always leads to an input of another layer in a linear fashion without loops. If layers have loops, they are called **Recurrent Neural networks** or RNNs.

For example, a neural network responsible for detecting the number in a MNIST dataset can have just three layers; Input (28×28 neurons), hidden (variable $n$) and output (10 neurons). The network is trained using a training set, and the mean squared loss function is minimized by using gradient descent.

&nbsp; 

### Gradient Descent

Given a function $f(x_1, x_2)$, the minima of the function can be computed empirically by taking its partial derivative and “walking” such that the function value is reduced.

<div style="text-align: center">
$$\begin{eqnarray}
\Delta f &=& \frac{\partial f}{\partial x}(\Delta x) + \frac{\partial f}{\partial y}(\Delta y) \nonumber \\
&=& (\triangledown f)\cdot(\Delta X) \nonumber \\
&=& -\eta \parallel \triangledown f \parallel ^2 \nonumber \\
\end{eqnarray}$$
</div>

We have substituted $\Delta X = -\eta \triangledown f$ to get the above equation, which is always negative. 

$\eta$ is called as the *Learning Rate*, and is directly proportional to how “large” the “steps” are.

In our case, we would be applying gradient descent and changing the values of all the biases ($b_i$) and weights ($w_i$) to minimize the cost function. A drawback of this method is that calculating the cost function requires the summation of the mean squared error over all values of training data, which would be ranging in the order of $10^5$. This causes the training to be very slow.

&nbsp; 

### Stochastic Gradient Descent

Instead of taking all the $n$ values in the training data set, we create a subset called the “mini set” where each element is a random subset of size $m\<n$. We compute the cost function over every subset in the mini set, with the assumption that the “true” cost function and the empirically calculated cost function are nearly equal. This dramatically reduces the time required for training the network.

When the mini set is exhausted, an **epoch** of training is said to be completed after which the process is repeated again. This is to mark the progress of training.

*** Vectorizing sigmoid function ***

&nbsp; 

## Back-Propagation

Assumption1: The cost function for a set of inputs is equal to the average of the cost function for each individual input. This assumption holds for the Least-Mean-Squared cost function.

Assumption2: The cost function should be a function of the outputs of the neural network.

Given the cost function C, and the weighted input z for a neuron, we define error for this neuron δ as follows;

<div style="text-align: center">
$$\delta = \frac{\partial C}{\partial z}$$
</div>

That is, if $\delta$ is a large value, then a change in $z$ can bring about a change in $C$. If it is zero, then it means that $C$ is optimal wrt $z$.

There are four fundamental equations to back propogation, and they have been given below. $\delta L$ is the $\delta$-vector for the final layer.
- δL = (∂C/∂a) ⊙ σ'(z)
- δⁿ = (wⁿ⁺¹)ᵀ(δⁿ⁺¹) ⊙ σ'(z)
- (∂C/∂b) = δ  ⇒  Delta of a neuron is equal to the derivative of the cost function wrt to its bias
- (∂C/∂wⁿⱼₖ) = aₖⁿ⁻¹ * δⱼⁿ   (Do remember that in wⱼₖ, neuron `k` is in the n-1'th layer and neuron `j` is in the n'th layer)

This is how a single iteration of training a neural network is done:
1. Input a set of training examples.
2. Feedforward the values to get the output.
3. Calculate the error at the outer-most layer.
4. Backpropogate the error till the input layer.
5. Perform gradient descent, as partial derivatives wrt all biases and weights is known.


&nbsp; 

## Learning Slowdown and the cross entropy cost function

We've been using the quadratic cost function so far. It does have a few issues, notably its derivative is very small when the value of $\sigma(z)$ is close to 0 or 1. In gradient descent, the change in biases and weights is directly proportional to the derivative of the cost function, meaning it is possible for this function to learn very slowly when it is giving wrong results. We turn to the cross entropy cost function as a solution.

<div style="text-align: center">
$$C = -\frac{1}{n}\sum_x[y\log(\sigma(z)) + (1-y)\log(1-\sigma(z))]$$
</div>

It can be checked mathematically that the derivative of this cost function wrt $b$ and $x$ is independant of $\sigma '(z)$, meaning no learning slowdown occurs. Moreover, the derivative is proportional to error meaning that learning occurs faster when the model is more wrong, as we would like it.

The cross entropy cost function can be defined for an entire layer as well;-

<div style="text-align: center">
$$C = -\frac{1}{n}\sum_x\sum_y[y\log(\sigma(z_j^L)) + (1-y)\log(1-\sigma(z_j^L))]$$
</div>

Here zⱼᴸ is the j'th neuron in the final layer 'L'.


Do note that a sigmoid function coupled with the cross entropy cost function is quite similar in terms of learning slowdown to the softmax function coupled with the log-likelihood cost function. (the derivatives wrt `b` and `x` have the same behaviour)


&nbsp; 

## Avoiding overfitting

1. Increase the size of training data

2. Regularization 
	- In L2 regularization, a new term is added to the cost function as shown below. The second summation is over all the weights in the network. $\lambda$ is called the *regularization parameter*.

	<div style="text-align: center">
		$$C = -\frac{1}{n}\sum_x\sum_y[y\log(\sigma(z_j^L)) + (1-y)\log(1-\sigma(z_j^L))] + \frac{\lambda}{2n}\sum_w w^2$$
	</div>

	- Similarly, L1 regularization is given below:

	<div style="text-align: center">
		$$C = -\frac{1}{n}\sum_x\sum_y[y\log(\sigma(z_j^L)) + (1-y)\log(1-\sigma(z_j^L))] + \frac{\lambda}{2n}\sum_w |w|$$
	</div>

	- Dropout regularization is a technique wherina random half of the hidden neurons are ommited from the network for a single training iteration. The idea here is that "different networks can have different overfitting heuristics, and training them seperately can cause the averaging out of their errors."

3. Artificially inflate the size of training data
	In the case of MNIST, just rotate/blur the images by a small degree to get new training data!

&nbsp; 

## Initializing the weights and biases

We have so far been initializing all weights and biases from a gaussian distribution of mean 0 and standard deviation 1. This isn't optimal, as the standard deviation of $z=\sum_i(w_ix_w)+b$ would be very large, proportional to the square of the umber of inputs the neuron has. This can cause the output of the sigmoid function to be nearly 0 or 1, causing stagnation as discussed earlier.

To solve this problem, we initialize $b$ as earlier but $w$ is initialized with mean 0 and standard deviation of $1/\sqrt{n}$ where n is the number of inputs.


&nbsp; 

## Universality of Neural Networks

This is a very important mathematical analysis (which I shall not write here for the sake of brevity) that neural networks (even simple ones with a single hidden layer) can compute any function with relative precision given enough time to train.

The approximation is better when there are more neurons used in the hidden layer. Also, we get an approximated continuous function as a result of estimating a discontinuous function by this method.