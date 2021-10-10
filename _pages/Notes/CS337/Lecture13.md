---
title: Clustering
permalink: /notes/cs337/Lec13
classes: wide
author_profile: false
sidebar:
    nav: "notes_cs337"
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

The  important parameters associated with clustering are given below.

1. Similarity Measure: $\rho(d_1, d_2)$
2. Distance Measure: $\delta(d_1, d_2)$
3. Number of clusters: $k$

In the same cluster, we would like $\delta$ to be small and $\rho$ to be large. This is called "Inter-Cluster". Similarly, we would like large $\delta$ and small $\rho$ between two different clusters. ("Intra-Cluster")

There are various methods of clustering the data. Some of these have been discussed below.

### Bottom-Up Clustering

Simply put, the pair of points with the smallest distance between them are "merged" into a cluster at every iteration. A visual representation of this is called as a **Dendogram**.

### Top-Down Clustering

We initialise $k$ arbitrary centroids, and iterate through the data and modify these centroids appropriately. We have a semblence of cluster representative in top-down, wheras bottom-up is just peer-to-peer in nature.

An idea is to perform bottom-up clustering until $k$ clusters are obtained, and using the means as the initial centroids for performing top-down clustering.

&nbsp;

## K-Means Algorithm

We will be dealing with the "hard" version of the K-Means algorithm. There are two main steps for this algorithm.

1. Keeping datapoints' assignments the same, update the position of cluster center to the empirical mean.
2. Fix the cluster centers and assign datapoints to cluster with least euclidean distance.

