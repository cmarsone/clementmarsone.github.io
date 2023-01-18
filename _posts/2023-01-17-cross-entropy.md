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

#### Negative log-likehood

Let $\mu \in \Delta(k)$, $\lambda \in \Delta(k)$ simplex of $k$ (multiclass). $\mu$ is a one-hot vector

*Shannon entropy* : $H^s \[ \mu \] = -\sum_ i \mu_ i \log \mu_ i$ gives a mesaure of uncertainty of the distribution $\mu$

$\to \forall \mu \in \Delta(k)$, $H^s \[ \mu \] \ge 0$ such that $H^s \[ \mu \] = -\sum_ i \mu_ i \log \mu_ i \ge -\sum_ i \mu_ i ( \mu_ i - 1) = 1 - \sum_ i \mu_ i^2 \ge 0$

$$\begin{cases}
H^ s [ \mu ] = 0 & \iff \mu \text{ is a one-hot vector (min-entropy)} \\
H^ s [ \mu ] \text{ is maximized } & \iff \forall i \text{ , } \mu_ i = \frac{1}{k} \\
\end{cases}$$ 

*Kullback-Leibler divergence*, also known as relative entropy, is a measure of the difference between two probability distributions. We assume $\forall i$, $\mu_ i \ge 0 \iff \lambda_ i \ge 0$.

$\text{KL}\[ \mu, \lambda \] = \sum_ i \log \frac{\mu_ i}{\lambda_ i}$

Properties of positivity: 

$$\begin{cases}
\text{KL} [ \mu, \lambda ] & \ge 0 \\
\text{KL} [ \mu, \lambda ] & = 0 \iff \mu = \lambda
\end{cases}$$

⚠️ But it does not commute in general: $\text{KL}\[ \mu, \lambda \] \neq \text{KL}\[ \lambda, \mu \]$

$\text{KL}\[ y, \mu]$ is one-hot vector $\mu = \text{softmax}(\omega)$

$$\text{KL} [ y, \mu] = \sum_ i \log \frac{y_ i}{\mu_ i} = \underbrace{-y_ i \log \mu_ i}_ {cross-entropy} - \underbrace{H [y] }_ {= 0 \text{ as } y \in \mathbb{E} [ k ]} = \sum_ i y_ i \log \frac{\exp(\omega_ i)}{2\omega} \\
= \sum_ i \omega_ i y_ i +\sum_ i y_ i \log 2\omega = -\langle y, \omega \rangle + \log 2\omega = -\log \mathbb{P}_ \theta (Y = y \mid X = x)$$

*Fermi-Dirac entropy* : The Fermi-Dirac entropy is a statistical measure of the entropy of a system of non-interacting fermions, such as electrons in a metal.

$$S = k_ {B}ln(2)(1 + n_ {F})$$

Where $k_ {B}$ is the Boltzmann constant, ln is the natural logarithm, and $n_ {F}$ is the Fermi-Dirac occupation number.

Let $\mu \in \[ 0, 1 \]$ be the paramters of Bernoulli such that $H^{FD}\[ \mu \] = -\mu \log \mu - (1- \mu) \log(1- \mu)$
