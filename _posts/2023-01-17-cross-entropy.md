---
layout: post
title: Cross-entropy
---

### General overview

Cross-entropy is a measure of the difference between two probability distributions, typically used in machine learning to evaluate the performance of a model. It is defined mathematically as:

$$H(p, q) = -\sum_{x} p(x) \log q(x)$$

where:

    $H(p, q)$ is the cross-entropy between the true distribution $p$ and the predicted distribution $q$
    $x$ is a discrete variable representing the possible outcomes of the distribution
    $p(x)$ is the true probability of outcome $x$
    $q(x)$ is the predicted probability of outcome $x$
    $\log$ is the natural logarithm
    $\sum$ is the summation over all possible outcomes $x$

The cross-entropy loss is calculated between two probability distributions, the target probability distribution and the predicted probability distribution. The target probability distribution is typically one-hot encoded, and the predicted probability distribution is calculated by the model. Cross-entropy loss is used to update the model's parameters so that the predicted probability distribution is closer to the target probability distribution.
