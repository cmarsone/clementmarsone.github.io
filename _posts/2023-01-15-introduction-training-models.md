---
layout: post
title: Training machine learning models
---

### Notations

* $X, Y, \ldots$ random variables
* $x, y, \ldots$ values
* * Given a vector $x \in \mathbb{R}^d$ with $d$ is the number of feature/input values, we want to predict an output $y \rightarrow f(Y|X=x) \in \mathbb{R}$ for regression & binary classification or $ \in \mathbb{R}^k$ for multiclass classification or strutured prediction.
* $\mathbb{P}(X, Y)$ : data distribution
* * $\mathbb{P}_{\theta}(Y|X)$ : model distribution over outputs
* $\sum_i \exp(\omega_i)$ : partition
* $\log\sum_i \exp(\omega_i)$ : log-partition

## General framework : Proof of convergence rates of different optimization techniques

* Training machine learning models is an optimization problem. The aim is to find the minimum of a function. Be careful to distinguish between *min* (a single value), *argmin* (a set of values), *inf* (the lower bound/limit) & conversely for a *max*.

### Types of problem
