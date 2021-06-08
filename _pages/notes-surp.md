---
title: "Notes for Chemical Catalysis"
permalink: /notes/chemcat/
---

# Table of Contents
1. [Random Forest Algorithm](#random-forest-algorithm)
	- [Working](#working)
	- [Hyperparameters](#important-hyperparameters)
2. [SMILES](#smiles-notation)

-1. [References](#references)



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




# SMILES Notation

SMILES stands for **S**implified **M**olecular **I**nput **L**ine **E**ntry **S**ystem. This is somewhat akin to the IUPAC nomenclature, but is designed to be compact and use ASCII characters. Five basic syntax rules are to be followed, and they have been listed below.

1. **Atom and Bond Nomenclature**

	Atoms are represented using their atomic symbols, and hydrogen is usually exempted in the string. That is, `C` refers to methane and `CC` refers to Ethane.

	Capital letters denote normal atoms and small letters denote aromatic atoms. That is, `CCCCCC` is Cyclo-Hexane, wheras `cccccc` is Benzene. For atoms with multi character atomic symbols, it is usually better to represent them in \[\]. For example, Scandium is represented as `[Sc]` and not `Sc` as the latter refers to Sulphur being attached to an aromatic carbon.

	The symbols used for bonds are given below. Single bonds are usually not represented manually.

	| Symbol |  Character  |
	|:------:|:-----------:|
	|   =    | Double Bond |
	|   #	 | Triple Bond |
	|   *    | Aromatic Bond |
	|   .    | Disconnected Structures |


2. Chains

	As explained earlier, hydrogens need not be written down for the structure to be generated. That is, `CC#C` refers to propyne. However, if hydrogens are represented anywhere in the string, it is assumed that ALL hydrogens have been mentioned explicitly. For example, `HC(H)=C(H)(H)` is ethene.

3. Branches

	Branches in molecules are represented using parantheses. The bond by which the branch is attached to the "main" chain is given after the opening paranthesis. For example, `CC(=C)C` and `CC(C)=C` both represent 2-Methyl Prop-1-ene.

4. Rings

	Rings are represented using SMILES by marking the "start" and "end" carbons of a ring using a number. That is, Cyclohexane is represented as `C1CCCCC1`, and Benzene is `c1ccccc1`. If the start and end of a ring are connected via a double or triple bond, it is mentioned before the number of the "start" atom. That is, `C=1CCCCC1` is Cyclo-Hexene.

5. Charge on Atoms

	The charge on an atom is represented in braces as `+1` or `-1`. That is, Enolate ion of Prop-2-one is given by `CC(O{-1})=C`.

# References

1. [Hyperparameter tuning for Random Forest algorithm](https://towardsdatascience.com/hyperparameter-tuning-the-random-forest-in-python-using-scikit-learn-28d2aa77dd74)
2. [Understanding Random Forest Algorithm](https://towardsdatascience.com/understanding-random-forest-58381e0602d2)

3. [SMILES Tutorial by USEPA](https://archive.epa.gov/med/med_archive_03/web/html/smiles.html)