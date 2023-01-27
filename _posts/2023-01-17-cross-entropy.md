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


Dual optimization
We consider the following L2 regularized binary SVM training problem:
Xn 1
min max(0, 1 − a⊤x(i)y(i)) + ∥x∥2 a2
i=1
We showed that optimizing this optimization problem via subgradient descent can be problematic: the sub- gradient is not necessarily a descent direction. The sub-gradient allows use to move closer to the optimal solution in term of euclidean distance, but it is difficult to check if an iteration improves this distance as the optimal point is obviously unknown. In this section, we will show an alternative way to train a SVM in its dual formulation. This formulation will have two advantages:
• it highlights what support vectors in SVM means,
• it allows us to use a hyper-parameter free optimization algorithm (no stepsize!) We first need to bring in some theory
4.1 Lagrangian duality
Let X ⊆ Rn be a convex set and f : X → R be a function. We consider the following primal mathematical program:
(P) min f(x) x∈X
s.t. Ax ≤ b
where A ∈ Rm×n and b ∈ Rm defines a set of m linear inequalities. The Lagrangian of (P) is the function
L:X×Rm+ →Rdefinedasfollows:
where x are the primal variables and λ the Lagrangian multipliers also called the dual variables. We build the
L(x, λ) = f (x) + λ⊤ (Ax − b) following relaxation of the primal problem:
L(λ) = min L(x, λ) x∈X
where L is a function L : Rm+ → R. We use the same name for two different functions, we hope it won’t confuse the reader. We call this problem relaxed because the constraints on the primal variables are replaced by penalties in the objective. It can be the case that this problem is simpler to solve than the primal problem.


Weak Lagrangian duality Let xˆ be the optimal solution of the primal problem (P). Then: ∀λ∈Rm+ : f(xˆ)≥L(λ)
In other word, for any set of dual variables λ, the relaxed problem gives use a lower bound to the optimal solution. To prove this, first note that xˆ satisfies the primal constraints by definition, therefore λ⊤(Axˆ − b) ≤ 0:
f(xˆ) ≥ f(xˆ) + λ⊤(Axˆ − b)
If this inequality is true for xˆ, it will also be true if we try to find the x that minimizes the right-hand side:
which ends the proof.
≥ min f(x) + λ⊤(Ax − b) x∈X
= L(λ)
Lagrangian dual problem By weak Lagrangian duality, we know that for any λ the relaxed problem is a lower bound to the primal problem. Therefore, we may want to search for the best lower bound possible, that is maximizing the lower bound. This problem is called the Lagrangian dual problem and is defined as follows:
(D) max L(λ) λ∈Rm+
Note that λ must be in the non-negative orthant. The difference between the primal optimal value and dual optimal value is called the duality gap. One important problem to know whether the primal and dual optimal value match or not, i.e is the duality gap null or not? We won’t study this problem here, we can just note that if X is a convex set, f is convex function, the constraints are linear (i.e. of the form Ax ≤ b as described here) and the problem is well defined (there exists at least one optimal solution), then there is no duality gap. The conditions that ensures that there is no duality gap are described in [Borwein and Lewis, 2010, Section 4.3] An important property of the duality gap is that it lets us estimate the quality of a primal feasible solution. However, this may not come for free as it requires to build a dual feasible solution. Finally, we show below how we can test if the duality gap is null.
Concavity One important property of the Lagrangian dual problem is that its objective function is concave. Moreover, this property does not depends on the the convexity of the primal objective function. Remember that a function is concave if its opposite is convex. Therefore, the following properties must be satisfied:
1. the domain of L(λ) must be convex
2. ∀λ(1),λ(2) ∈λ∈Rm+ andε∈[0,1]:L(ελ(1)+(1−ε)λ(2))≥εL(λ(1))+(1−ε)L(λ(2))
The first property is trivially satisfied for the domain Rm+ .
For the second property, lets write λ = ελ(1) + (1 − ε)λ(2) and x∗ = arg minx∈X L(x, λ). The following
inequality are satisfied by definition:
L(x∗, λ(1)) ≥ L(λ(1)) L(x∗, λ(2)) ≥ L(λ(2))
as the right-hand sides are minimizations over the primal variables. We multiply and sum both inequalities to obtain:
εL(x∗, λ(1)) + (1 − ε)L(x∗, λ(2)) ≥ εL(λ(1)) + (1 − ε)L(λ(2))
To simplify notations, we write c(x) = Ax − b. The left-hand side of the inequality can be rewritten as:
εL(x∗ , λ(1) ) + (1 − ε)L(x∗ , λ(2) ) = ε f (x∗ ) + λ(1)⊤ c(x∗ ) + (1 − ε) f (x∗ ) + λ(2)⊤ c(x∗ )
= εf(x∗) + ελ(1)⊤c(x∗) + (1 − ε)f(x∗) + (1 − ε)λ(2)⊤c(x∗)
∗  (1)
=f(x )+ ελ +(1−ε)λ
= f(x∗) + λ⊤c(x∗)
= L(x∗,λ)
= L(λ)
= L(ελ(1) + (1 − ε)λ(2))

Hence, we obtain the inequality:
L(ελ(1) + (1 − ε)λ(2)) ≥ εL(λ(1)) + (1 − ε)L(λ(2)) which proves that the Lagrangian dual objective is concave.

### Strong Lagrangian duality

Let λ ∈ Rm+ be a dual feasible solution and x∗ = arg minx∈X L(x, λ). If: • Ax∗ ≤ b (primal feasibility condition)
• and λ⊤(Ax∗ − b) = 0 (complementary slackness condition)
then x∗ is a primal optimal solution. To prove this, let xˆ be a primal optimal solution. By weak Lagrangian duality, we know that:
f(xˆ) ≥ L(λ)
= L(x∗,λ)
= f(x∗) + λ⊤(Ax∗ − b) From the prerequisites the second term in null, therefore we have:
f(xˆ) ≥ f(x∗)
Moreover, we know that f(xˆ) ≤ f(x∗) because x∗ is primal feasible, and therefore f(xˆ) = f(x∗), which ends
the proof.
Equality constraints As of now we only considered linear inequality constraints. If we want to introduce
equality constraints Ax = b instead, note that the problem can be formulated as follows: (P) min f(x)
x∈X
s.t. Ax ≤ b
− Ax ≤ −b
Then, the Lagrangian is a function L(x,λ,λ′) with two vectors of dual variables λ ∈ Rm+ and λ′ ∈ Rm+ defined
as follows:
L(x, λ, λ′ ) = f (x) + λ⊤ (Ax − b) + λ′⊤ (−Ax + b) = f(x) + λ⊤(Ax − b) − λ′⊤(Ax − b)
= f(x) + (λ − λ′)⊤(Ax − b)
By defining λ′′ = λ − λ′ we could instead formulate the Lagrangian with a single vector of dual variable:
L(x, λ′′ ) = f (x) + λ′′⊤ (Ax − b)
In this formulation, the dual variables λ′′ ∈ Rm is unconstrained. Equality constraints with this formulation simplifies the problem in two ways:

First, the maximization in the Lagrangian dual problem is simpler as there is no constraint on the dual variables,
Second, the strong duality condition simplifies as primal feasibility implies complementary slackness.


### Karush–Kuhn–Tucker conditions
Assume we have a maximization problem defined as follows:
max f (x) x
s.t. g(i)(x)≥0 h(i)(x) = 0
∀1≤i≤m ∀1 ≤ i ≤ n
where x ∈ Rk, g(i) ≥ 0 is a set of m inequality and h(i)(x) = 0 is a set of n equality. An optimal solution x∗ ∈ Rk of the mathematical program satisfies the following constraints:
(stationarity) (primal feasibility)
(dual feasibility) (complementary slackness)
∀i:
∀i : ∀i: ∀i :
∂ f(x∗)+Xμ ∂ g(j)(x∗)−Xλ ∂ h(j)(x∗)=0 ∂x j ∂x j ∂x
ijiji
g(i)(x) ≥ 0 h(i) (x) = 0 μi≥0
X μig(i)(x∗) ≥ 0 i
where μ ∈ Rm and λ ∈ Rn are dual variables associated with primal inequalities and equalities, respectively. These set of equation, in the general case, are necessary constraints: there may exists points x that satisfies these constraints that are not optimal solution. However, if:
• f is a concave function,
• all g(i) are concave functions,
• annd all h(i) are affine functions,
then the KKT are sufficient conditions too. In particular, we will see that in some special cases we can solve this set of equations to find the optimal x∗, i.e. the optimization problem as a closed form solution.

