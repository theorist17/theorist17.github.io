---
layout: post
title: "Word Embedding"
date: 2021-05-06
---

# Word Embedding


Think about language input, e.g. a movie review about Interstellar.

The text first should be converted into numeric vectors.

Or image inputs, e.g. handwritten images of numbers.

The classification may be about whether the data sample is positve/negative or, out of 0-10, which number the image is reprensenting.

The text may be more challenging, as they have these so-called word dependencies between words. The longer the text, the more complicated the dependencies within them get.

So, we need a good conversion from text to vectors, and build a good neural networks (the mapping into the given classification layer).

## One-hot Vector/Encoding

![one-hot-vector](/assets/2021-05-06-00-one-hot-vector.png)

Given a corpus of text, we can get the vocabulary from it (consisting of unique terms), then we set the target vector dimenstion to represnet them. If you use the one-hot encoding, the dimension is equal to the size of the vocabulary. So if your vocab are 10, then the dimension is 10. e.g. "apple" becomes 0000000001 and "banana" becomes 0000000010. Only one index is assigned with value "one", so one-hot!

## Drawbacks of One-hot Representation

### Curse of Dimenstionality

Many ML problems become exceedingly difficult when the number of dimensions in the data is high.

Each data sample is sparsely represented.

Information quality gets worse, memory use gets bigger, and computation time gets higher as your dimension gets bigger. 

\* usually 300 is popular dimension, e.g. Word2Vec.

### Orthogonality

If you multiply two one-hot embeddings, you get always get zero.
That may means all the two words is euqlly distances in terms of their similarity. e.g. the distance between "dog" and "puppy" is the same as "dog" and "computer".

This can be called that all word embeddings are orthogonal to each other. We don't want this for the downstream NLP tasks. We want numeric operations over them, assuming they are embedded in a semantically meaningful way.


### Dimensionality Reduction

Due to the curse of dimension, we need to reduce the dimension.

The process of converting a set of high dimenstional data into a lower dimenstional representation that conves similar information.

E.g. Pricipal Component Analysis (PCA), Linear Discrimina Analysis (LDA)


PCA finds a linear subspace that maximized the variance of the data once it is projected into a lower-dimensitonal space. It also minimizes the distance off the projection in a least-squares sense.

![PCA](/assets/2021-05-06-01-PCA.png)



It mease that while the data points gets maixmal variance (so that they are well distinguished from each other), we want to keep the pattern intact (the line in the right image well represent the dots!). SO we use the line (or a hyperplane) to replace the dots, reducing a dimension.


### Manifold Hypothesis

PCA may be good. But problems get harder and harder as data forms non-linear patterns.

Manifolds hypothesis address the non-linear patterns.

Natural data in high dimensional spaces contentrates close to lower dimensional manifolds. Moving away from the supporting manifold (reducing dimension), probability density decreases (model becomes incorrect).

![manifold-hypo](/assets/2021-05-06-02-manifold-hypo.png)

Reducing dimension in the middle image, the distance between two points A and B, gets very bigger. This may cause problems.

So dont' just linearize the pattern in manifold patterns (instead of uniform patterns, or etc).


Regarding the words, are they form the manifold pattern? or maybe uniform patterns?


### Autoencoder

