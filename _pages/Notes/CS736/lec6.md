# Image Segmentation 2 - Electric Boogaloo

Images acquired by an MRI scanner have an inherent “inhomogeneity field” (or a bias field) causing them to be corrupted. For example, consider the following MRI scan. The intensity of the true image is scaled by the value of the bias field at every pixel.

![image-20220213133307854](E:\Github\AkashCherukuri.github.io\assets\images\typora\image-20220213133307854.png)

It can be concluded using both experience and physics that the bias field for an MRI scan is smooth, and continuously differentiable.

This occurs in cameras taking pictures as well, called “Vignetting”. Vignetting causes the images to have reduced brightness and saturation at the lens edges compared to the center. This is often used to draw attention to the subject of the image.

Bias field introduces new problems to be tackled with respect to image segmentation, as it causes the same segment to have different intensity values at different places in the image. For example, consider the grey matter intensities in the image at different places in the image. Our goal is to extend Fuzzy-C-means to be able to segment images with the bias field modeling/correction incorporated into it.

&nbsp;

## Modified FCM

At voxel $i$, let the intensity be $x_i$ and the bias field be $b_i$. Let the noise model used be an additive zero mean gaussian. Therefore, the observed intensity $y_i$ would be:


$$
y_i = x_ib_i + \eta_i \qquad \text{where }\eta_i\sim\mathcal{N}(0,1)
$$


We make the following two assumptions:

1. Number of image classes, $K$ is known
2. Each class has a constant uncorrupted MRI intensity $c_k$

Therefore, consider a voxel $i$ whose neighboring voxel $j$ belongs to the class $k$;


$$
x_jb_j \approx c_kb_i
$$


### Strategy

The Euclidean distance between the observed intensity $y_i$ and the predicted intensity $x_ib_i$ is used as the basis of the objective function. Two weighting parameters are involved too;

1. We do not know the class which voxel $j$ belongs to, so we weight the distance with membership parameter $u_{jk}^q$.
2. The approximation $x_jb_j \approx c_kb_i$ is less accurate the further apart the two voxels are, so we add a new weight $w_{ij}$ based upon this.

The objective function thus turns out to be;


$$
\begin{align*}
J :&= \sum_{i=1}^N J_i \\
J_i :&= \sum_{j=1}^Nw_{ij}\sum_{k=1}^K\left( u_{jk}^q(y_j - c_kb_i)^2 \right) \\
\implies J &= \sum_{j=1}^N\sum_{k=1}^K u_{jk}^q \left( \sum_{i=1}^N w_{ij} (y_j - c_kb_i)^2 \right)
\end{align*}
$$


Note that the rewritten objective function is quite similar to the objective function of the FCM objective function. Let $d_{kj}$ be the distance between the $j$’th datapoint and the $k$’th cluster. It only depends on $k,j$.

Therefore the optimization problem thus becomes the following equation. **Lagrange’s Multipliers** can be used to solve this, just like what we’ve done for FCM!


$$
L := \min_{\{u_{jk}\}, \{c_k\}, \{b_i\}} \sum_{j=1}^N\sum_{k=1}^Ku_{jk}^q d_{kj}
$$


### Optimization

*LM method I have no idea lol*



&nbsp;



## Limitations of K-means and FCM

These methods cannot model clusters with unequal spreads. They also cannot model ellipsoidal cluster distributions, because they require a Multivariate Gaussian model with a covariance matrix for each cluster.

It doesn’t enforce spatial smoothness on segmentation. 