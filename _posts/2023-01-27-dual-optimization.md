---
layout: post
title: Dual optimization
author: Clément
---

We consider the following $L_ 2$ regularized binary *SVM training problem*:
$$\min\limits_{a} \sum\limits_ {i=1} ^n \operatorname{max}(0, 1 − y_ i (a^\top x_ i +b) + \frac{1}{2} ||a||_ 2^2 $$
where $C$ is the regularization parameter that controls the trade-off between maximizing the margin and avoiding overfitting, $a$ and $b$ are the coefficients of the hyperplane, $x_i$ and $y_i$ are the features and labels of the $i$th sample, and $\xi_i$ is the slack variable that allows for misclassified samples.

We showed that optimizing this problem via subgradient descent can be problematic: the sub-gradient is not necessarily a descent direction. The sub-gradient allows use to move closer to the optimal solution in term of euclidean distance, but it is difficult to check if an iteration improves this distance as the optimal point is obviously unknown. In this section, we will show an alternative way to train a SVM in its dual formulation. This formulation will have two advantages:
- it highlights what support vectors in SVM means,
- it allows us to use a hyper-parameter free optimization algorithm i.e. no stepsize

### Lagrangian duality

Let $U \subseteq \mathbb{R}^n$ be a convex set and $f: U \rightarrow \mathbb{R}$ be a function. We consider the following primal mathematical program:

$$\begin{equation}
\text{(P)} \quad \min_{u \in U} f(u) \quad \text{s.t.} \quad Au \le b
\end{equation}$$

where $A \in \mathbb{R}^{m \times n}$ and $b \in \mathbb{R}^m$ defines a set of $m$ linear inequalities. The Lagrangian of $(P)$ is the function $L: U \times \mathbb{R}^m_+ \rightarrow \mathbb{R}$ defined as follows:

$$\begin{equation}
L(u, \lambda) = f(u) + \lambda^T(Au - b)
\end{equation}$$

where $u \in U$ are the *primal variables* and $\lambda \in \mathbb{R}_ +^m$ are the *Lagrangian multipliers*, also called the *dual variables*. We build the following relaxation of the primal problem:

$$\begin{equation}
L(\lambda) = \min_{x \in X} L(x, \lambda)
\end{equation}$$

where $L$ is a function $L: \mathbb{R}^m_+ \rightarrow \mathbb{R}$. We use the same name for two different functions, hoping it will not confuse the reader. We call this problem relaxed because the constraints on the primal variables are replaced by penalties in the objective. This problem can be simpler to solve than the primal problem.

### Relaxation of the primal problem with weak Lagrangian duality

The relaxed problem $L : \mathbb{R}^m_+ \rightarrow \mathbb{R}$ is defined as:

$$\begin{equation}
L(\lambda) = \min_{u \in U} L(u, \lambda)
\end{equation}$$

Weak Lagrangian duality states that, given $\hat{u}$ as the optimal solution of the primal problem $(P)$, then for all $\lambda \in \mathbb{R}^m_+$:

$$\begin{equation}
f(\hat{u}) \geq L(\lambda)
\end{equation}$$

Proof:

Since $\hat{u}$ satisfies the constraints, we have $f(\hat{u}) \geq f(\hat{u}) + \lambda^T (A \hat{u} - b)$. Also, $f(\hat{u}) + \lambda^T (A \hat{u} - b) \geq \min_{u \in U} f(u) + \lambda^T(Au - b) = L(\lambda)$.

The Lagrangian dual problem is defined as follows:

$L(\lambda)$ is a lower bound to the primal problem for all $\lambda \in \mathbb{R}^m_+$, such that $f(\hat{u}) \geq L(\lambda)$.

### Lagragian dual problem

The dual problem $(D)$ is defined as the search for the best lower bound:

$$\begin{equation}
(D) \quad \max_{\lambda \in \mathbb{R}^m_+} L(\lambda)
\end{equation}$$

It is important to note that the dual problem is always concave, regardless of whether the function $f$ is convex or not.

Strong Lagrangian duality states that, given a dual feasible solution $\lambda \in \mathbb{R}^m_+$ and $\bar{u} = \arg\max_{u \in U} L(u, \lambda)$, if $\bar{u}$ satisfies the primal feasibility condition $A\bar{u} \leq b$ and the complementary slackness condition $\lambda^T (A\bar{u} - b) = 0$, then $\bar{u} = \hat{u}$ is the optimal solution of the primal problem $(P)$.

#### Dual concavity proof

Let $L(\lambda)$ be a function, then $L(\lambda)$ is concave if and only if the following two conditions are satisfied:

1. The domain of $L(\lambda)$ is convex (trivial). 
2. $\forall \lambda(1), \lambda(2) \in \lambda \in \mathbb{R}^m, \epsilon \in [0, 1]: L(\epsilon \lambda(1) + (1 - \epsilon) \lambda(2)) \ge \epsilon L(\lambda(1)) + (1 - \epsilon) L(\lambda(2))$

Let $\lambda = \epsilon \lambda(1) + (1 - \epsilon) \lambda(2)$ and $\bar{u} = \arg \min_{u \in X} L(u, \lambda)$:

$L(\bar{u}, \lambda(1)) \ge L(\lambda(1))$

$L(\bar{u}, \lambda(2)) \ge L(\lambda(2))$

$\implies \epsilon L(\bar{u}, \lambda(1)) + (1 - \epsilon) L(\bar{u}, \lambda(2)) \ge \epsilon L(\lambda(1)) + (1 - \epsilon) L(\lambda(2))$

To understand the left-hand side, recall that:

$L(\lambda) = \min_{u \in X} L(u, \lambda)$

Therefore:

- The right-hand side has the expected form
- The left-hand side is different, we need to fix this to finish the proof.

To simplify notations, we write $c(u) = Au - b$.

The left-hand side of the inequality can be rewritten as:

$\epsilon L(\bar{u}, \lambda(1)) + (1 - \epsilon) L(\bar{u}, \lambda(2)) = \epsilon (f(\bar{u}) + \lambda(1)^T c(\bar{u})) + (1 - \epsilon)(f(\bar{u}) + \lambda(2)^T c(\bar{u})) = \epsilon f(\bar{u}) + \epsilon \lambda(1)^T c(\bar{u}) + (1 - \epsilon) f(\bar{u}) + (1 - \epsilon) \lambda(2)^T c(\bar{u}) = f(\bar{u}) + (\epsilon \lambda(1) + (1 - \epsilon) \lambda(2))^T c(\bar{u}) = f(\bar{u}) + \lambda^T c(\bar{u}) = L(\bar{u}, \lambda) = L(\lambda) = L(\epsilon \lambda(1) + (1 - \epsilon) \lambda(2))$

Hence, we obtain the inequality:

$L(\epsilon \lambda(1) + (1 - \epsilon) \lambda(2)) \ge \epsilon L(\lambda(1)) + (1 - \epsilon) L(\lambda(2))$

which proves that the Lagrangian dual objective is concave.

#### Solve strong Lagragian duality

Let $\hat{u}$ be a primal optimal solution.
By weak Lagrangian duality, we know that:

$f(\hat{u}) \ge L(\lambda) = L(\bar{u}, \lambda) = f(\bar{u}) + \lambda^\intercal (A \bar{u} - b)$

From the prerequisites (complementary slackness), the second term is null:

$f(\hat{u}) \ge f(\bar{u})$

Moreover: $f(\hat{u}) \le f(\hat{u})$ because $\hat{u}$ is primal feasible,

Therefore $f(\bar{u}) = f(\hat{u})$.

### Relaxing equality constraints

$$\begin{align*}
\min_{u} &f(u) \\
\text{s.t. } &Au = b \\
\text{or } &Au \le b \\ - &Au \le -b
\end{align*}$$

The Lagrangian can be expressed as:

$$\begin{align*}
L(u, \lambda \ge 0, \lambda' \ge 0) &= f(u) + \lambda^\top (Au - b) + \lambda'^\top (-Au + b) \
&= f(u) + \lambda^\top (Au - b) - \lambda'^\top (Au - b) \
&= f(u) + (\lambda - \lambda')^\top (Au - b)
\end{align*}$$

Let $\lambda'' = \lambda - \lambda'$:

$$\begin{align*}
L(u, \lambda'') &= f(u) + \lambda''^\top (Au - b)
\end{align*}$$

In this formulation, the dual variables $\lambda'' \in \mathbb{R}^m$ are unconstrained. Relaxing the equalities has the benefits of an unconstrained optimization problem and a simpler strong duality condition.

### Karush–Kuhn–Tucker conditions

Assume we have a maximization problem defined as follows:

$$\begin{align}
\nabla f(\mathbf{x}) + \sum_ {i=1}^m \lambda_ i \nabla g_ i(\mathbf{x}) &= \mathbf{0} \\
g_ i(\mathbf{x}) &\le 0, \quad i = 1, 2, \ldots, m \\
\lambda_ i &\ge 0, \quad i = 1, 2, \ldots, m \\
\lambda_ i g_ i(\mathbf{x}) &= 0, \quad i = 1, 2, \ldots, m
\end{align}$$

where $\mathbf{x}$ is the vector of optimization variables, $f(\mathbf{x})$ is the objective function, $g_i(\mathbf{x})$ are the inequality constraints, $\lambda_i$ are the Lagrange multipliers, and $m$ is the number of constraints.

$$\begin{align}
&\text{max} \quad f(x) \\
&\text{s.t.} \quad g_i(x) \ge 0 \quad (1 \le i \le m) \\
&\quad\quad\quad h_i(x) = 0 \quad (1 \le i \le n) \\
&\text{where} \quad x \in \mathbb{R}^k \\
\end{align}$$

An optimal solution $x^* \in \mathbb{R}^k$ of the mathematical program satisfies the following constraints:

$$\begin{align}
&\text{(stationarity)} \quad \forall i : \frac{\partial f(x^*)}{\partial x_i} + \sum_{j=1}^{m} \mu_j \frac{\partial g_j(x^*)}{\partial x_i} - \sum_{j=1}^{n} \lambda_j \frac{\partial h_j(x^*)}{\partial x_i} = 0 \\
&\text{(primal feasibility)} \quad \forall i : g_i(x) \ge 0 \\
&\quad\quad\quad\quad\quad\quad\quad \forall i : h_i(x) = 0 \\
&\text{(dual feasibility)} \quad \forall i : \mu_i \ge 0 \\
&\text{(complementary slackness)} \quad \sum_{i=1}^{m} \mu_i g_i(x^*) \ge 0 \\
\end{align}$$

where $\mu \in \mathbb{R}^m$ and $\lambda \in \mathbb{R}^n$ are dual variables associated with primal inequalities and equalities, respectively.

These set of equations, in the general case, are necessary constraints: there may exists points $x$ that satisfies these constraints that are not optimal solutions. However, if:

$f$ is a concave function,
all $g_i$ are concave functions,
and all $h_i$ are affine functions,

then the KKT conditions are sufficient conditions too. In particular, we will see that in some special cases we can solve this set of equations to find the optimal $x^*$, i.e. the optimization problem has a closed form solution.
