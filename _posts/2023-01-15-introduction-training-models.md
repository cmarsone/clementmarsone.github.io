---
layout: post
title: Training machine learning models
---

### Notations

* $X, Y, \ldots$ random variables
* $x, y, \ldots$ values
* Given a vector $x \in \mathbb{R}^d$ with $d$ is the number of feature/input values, we want to predict an output $y \to f(Y \mid X=x) \in \mathbb{R}$ for regression & binary classification or $ \in \mathbb{R}^k$ for multiclass classification or strutured prediction.
* $\mathbb{P}(X, Y)$ : data distribution
* $\mathbb{P}_ {\theta}(Y \mid X)$ : model distribution over outputs
* $\sum_i \exp(\omega_i)$ : partition
* $\log\sum_i \exp(\omega_i)$ : log-partition
* $\text{conv}(Y)$ : the Convex Hull i. e. the smallest convex set that contains $Y$ 

## General framework : Proof of convergence rates of different optimization techniques

* (input space) $\to$ scoring function $\omega=\sigma_\theta(x)$ $\to$ (score/logit/weight space) $\to$ prediction function $\mu=\hat{y}(\omega)$ $\to$ (output space)
* Training machine learning models is an 'optimization problem'. The aim is to find the 'minimum of a function'. Be careful to distinguish between *min* (a single value), *argmin* (a set of values), *inf* (the lower bound/limit) & conversely for a *max*.
* Actually, we have to define a loss function $\ell:Y\times\mathbb{R}^k \to \mathbb{R}_ {+}$ & try to minimize it over a distribution by finding $\theta=\text{argmin}_ \theta \mathbb{E}_ {\mathbb{P}(X,Y)}(\ell(y, \sigma_ {\theta(x)})$
* 'Monte-Carlo estimation' : $D$ training data, set of i.i.d samples from $\mathbb{P}(X,Y)$ such that $\mathbb{E}_ {\mathbb{P}(X,Y)}(\ell(y, \sigma_\theta(x)) \sim \frac{1}{D} \sum_{(x,y) \in D} \ell(y, \sigma_\theta(x)$
* Then we add in the loss function a regularization term to avoid overfitting $\to$ regularization weights : $L_1$ (LASSO), $L_2$ (Ridge), Elastic-net, $\ldots$. ⚠ Genrally, do not regularize the intercept ($\neq$ `fit_intercept`)

### Types of problem

#### Regression 

$Y \in \mathbb{R}$, $\text{conv}(Y)=\mathbb{R}$, $\sigma_\theta(x)=a^T x + b = \langle a, x \rangle + b$, $\theta(a, b)$, $a \in \mathbb{R}^d$, $b \in \mathbb{R} \to \hat{y}(\omega) = \omega$
#### Binary classification

$Y = \{ 0, 1 \}$, $\text{conv}(Y)=\[ 0, 1 \]$, $\sigma_\theta(x)=a^T x + b = \langle a, x \rangle + b$, $\theta(a, b)$, $a \in \mathbb{R}^d$, $b \in \mathbb{R} \to \hat{y}(\omega) = \omega$

$$\hat{y}(\omega) = \begin{cases}
1 & \text{if } \omega \ge 0 \\
0 & \text{otherwise}
\end{cases}$$ 

or $\hat{y}(\omega) = \frac{\exp(\omega)}{1 + \exp{\omega}} = \sigma(\omega) \in \] 0, 1 \[$ (sigmoid)

$\mu = \hat{y}(\omega)$, $\mu$ should be interpreted as the parameter of a Bernoulli distribution

$$\begin{cases}
\mathbb{P}_ \theta (Y = 1 \mid X = x) = \mu \\
\mathbb{P}_ \theta (Y = 0 \mid X = x) = 1 - \mu
\end{cases}$$

The following prediction function is an *optimal prediction rule*. It is kown as the *Bayes classifier* :

$$f^* (x) = \mathbb{1} \{ \mu \ge 1/2 \} \in \operatorname{argmax}_{y \in \{ 0, 1\}} P(Y = y \mid X = x)$$ and $\epsilon^* = \mathbb{E} \left[ \min \left( \eta (X), 1 - \eta (X) \right) \right] $

#### Multiclass classification

$Y$ is the set of one-hot vectors of dimension $k$, $\text{conv}(Y)=\Delta(k)$ simplex of dim $k = \{ \mu \in \mathbb{R}^k \mid \sum_ i \mu_ i = 1 \text{ and } \mu_ i \ge 0, \forall i \} $

$\sigma_\theta(x)=a^T x + b = \langle a, x \rangle + b$, $\theta(a, b)$, $a \in \mathbb{R}^{k \times d}$, $b \in \mathbb{R}^k \to \hat{y}(\omega) = \text{argmax}_ {y \in Y} \langle y, \omega \rangle$ or $\hat{y}(\omega) = \text{softmax}(\omega) \iff \mu_ i = \frac{\exp(\omega_ i)}{\sum_ j (\omega_ j)}$

#### Multilabel : structured prediction

Multilabel classification is a machine learning problem where a model is trained to predict multiple output variables for a given input.
