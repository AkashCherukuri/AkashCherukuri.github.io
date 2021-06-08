---
title: "Notes for Chemical Catalysis"
permalink: /notes/chemcat/
---

# Table of Contents
1. [Random Forest Algorithm](#random-forest-algorithm)
	- [Working](#working)
	- [Hyperparameters](#important-hyperparameters)

# Random Forest Algorithm
This is a very versatile algorithm, as it can act as both a classifier and an regressor. It is used in various fields, such as the stock market and banking for starters.

### Working

This algorithm consists of building multiple decision trees to act as an ensemble. Each of the decision trees have access to a random set of features. Let the number of trees in the ensemble be `N`. Each individual tree produces a result when data is provided for classification, and the majority is given as the result of the entire classifier.

This is considered to be efficient as it is very likely that one tree might have trouble with a certain type of data, but the majority of the trees can classify the data just fine. However, for this to happen, it is necessary that all trees have next to no correlation with each other.

This is acheived in the following ways:

- **Bagging:**

	Let one of the data set during training be \[1,2,3,4\]. This data is modified a little randomly so that all trees in the classifier get different variations of the same data. For example, one tree might get \[1,1,2,4\] and another can get \[1,2,2,3\] and so on.

- **Random Features:**

	Discussed already, each tree has access to a random subset of features. This further decreases the chances of two trees having similarities.

### Important Hyperparameters

1. `n_estimators`: Number of trees in the ensemble. Large values imply better learning but slower training and classification times.
2. `max_features`: Maximum number of features that a node can consider before splitting. Large features would improve each individual tree but correlation is increased as well.
3. `max_depth`: Maximum depth of a tree in the ensemble. Large values can cause overfitting.
4. `min_samples_split`: The minimum samples that must be present in a node before split.
5. `min_samples_leaf`: The minimum samples that a leaf can have. 