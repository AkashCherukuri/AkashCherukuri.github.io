---
title: "Generative Adversial Networks"
permalink: /notes/dl/gan
classes: wide
author_profile: false
sidebar:
    nav: "notes_soc"
---

---
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML" async></script>

GAN stands for Generative Adversial Networks, and they belong to the set of Generative models. These models are called "generative" because of their ability to generate new data, such as a picture of a human face.

The mathematical analysis and intuition behind these networks is given below.

&nbsp; 

## Inverse Transform Method and its implications

This method is used to simulate drawing values from a complicated probability distribution, using a uniform distribution. Let the CDF of the complicated distribution be `F`. Assume that it is invertible, and let its inverse be given by `F⁻¹`. Let a draw from the uniform distribution be `u`. It can quite easily be proven that `F⁻¹(u)` has the same distribution as `F` itself.

`F⁻¹` is called as the **Transform Function**, as it is used to transform the uniform distribution to the target distribution.

This has a very important implication in the generation of new data. Suppose that there is a probability distribution for a vector of size n² (an image of size nxn) called the "Human Distribution" `H`, which tells how likely it is that the image represents a human face. We can now *simply* generate a random vector from uniform distribution, pass it through `H⁻¹` to generate a human face!

There are very obvious problems here:
- The "human distribution" is a very complex distribution over a very large space
- It may or may not exist

&nbsp; 

## Generative Models

In reality, we cannot explicitly say what `H` is. Therefore, a generative model aims at estimating the value of the transform function (`H⁻¹` in this case). Training such a model has two ways, **direct** and **adversial**. Both these methods have been explained below.

&nbsp; 

### Direct training (Generative Matching Networks)

We have one neural network which aims to estimate the transform function by comparing the acheived distribution to the "true" distribution. However, we do not know the true distribution (otherwise we wouldn't need to do all this!) We thus take samples of human faces from available data and generate human faces via the neural network. Then, the **M**aximum **M**ean **D**iscrepency between the two estimated distributions is taken as the error for back-propogation. 

The neural net would strive to reduce MMD, meaning that it would learn the transform function upon training for sufficient time. This way of training for generation is used in Generative Matching Networks.

&nbsp; 

### Adversial training (GANs)

We have two neural networks here, the *generator* and the *discriminator*. The generator has the same role as the previous model, wherein it tries to estimate the transform function by generating images of a human face. The discriminator is handed images from both generator and the already available data. It is tasked with classifying the images into two groups, the ones from the generator and the ones from the true data set. The generator is hence tasked with fooling the discriminator to the best possible extent.

Both the networks are trained simultaneously, and it can be clearly seen that they both are competing with each other. The discriminator tries to increase the error between the generated and the true data set whereas the generator tries to decrease this value at the same time. This competition is why the architecture is referred to as an "Adversial" network. Both the nets improve in what they're trying to acheive by competing against each other.
