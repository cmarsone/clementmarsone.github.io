---
layout: post
title: Training machine learning models
---

### Notations

* $X, Y, \ldots$ random variables
* $x, y, \ldots$ values
* Given a vector $x \in \mathbb{R}^d$ with $d$ is the number of feature/input values, we want to predict an output $y \to f(Y \mid X=x) \in \mathbb{R}$ for regression & binary classification or $ \in \mathbb{R}^k$ for multiclass classification or strutured prediction.
* $\mathbb{P}(X, Y)$ : data distribution
* $\mathbb{P}_{\theta}(Y \mid X)$ : model distribution over outputs
* $\sum_i \exp(\omega_i)$ : partition
* $\log\sum_i \exp(\omega_i)$ : log-partition
* $\text{conv}(Y)$ : the Convex Hull i. e. the smallest convex set that contains $Y$ 

## General framework : Proof of convergence rates of different optimization techniques

* Training machine learning models is an 'optimization problem'. The aim is to find the 'minimum of a function'. Be careful to distinguish between *min* (a single value), *argmin* (a set of values), *inf* (the lower bound/limit) & conversely for a *max*.
* Actually, we have to define a loss function $\ell:Y\times\mathbb{R}^k \to \mathbb{R}_+$ \& try to minimize it over a distribution by finding $\theta=\text{argmin}_\theta \mathbb{E}_{\mathbb{P}(X,Y)}(\ell(y, \sigma_\theta(x))$
* (input space) $\to$ scoring function $\omega=\sigma_\theta(x)$ $\to$ (score/logit/weight space) $\to$ prediction function $\mu=\hat{y}(\omega)$ $\to$ (output space)

### Types of problem
* *Regression* : $Y \in \mathbb{R}$
* *Binary classification* : $Y = \{0, 1\}$
* *Multiclass classification* :  $Y$ is the set of one-hot vectors of dimension $k$
* *Multilabel* : structured prediction
