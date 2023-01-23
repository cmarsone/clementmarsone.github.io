---
layout: post
title: Convex Optimization
---

#### Convex set: $U \subseteq R^n$

$\forall u, u^{\prime} \in U, \exists \epsilon \in [0,1] $ such that $\underbrace{\epsilon u +(1 -\epsilon)u^{\prime}}_ {\text{convex comb.}} \in U$

#### Convex hull: $\operatorname{conv} U$ the smallest convex set that contains $U$

$\operatorname{conv} U = \lbrace \epsilon u +(1 -\epsilon)u^\prime \mid u, u^\prime \in U, \epsilon \in [0, 1] \rbrace $
For instance, simplex $\operatorname{conv} E(k) = \Delta(k)$

#### Convex function $f:U \to \mathbb{R}$

1. $U$ is a convex set
2. $\forall u, u^\prime \in U, ε \in [0, 1], f( \underbrace{\epsilon u +(1 -\epsilon)u^\prime}_ {\text{dom. needs to be conv.}}) \leq \epsilon f(u) +(1 -\epsilon)f(u^\prime)$ or $\forall u \in U, \nabla^2f(u)$ (Hessian) is a positive semi-definite matrix ($\langle u,\nabla^2f(u) \rangle$ 

In other words, any point which is a convex combination of points in $U$ must also be in $U$. Note that the domain of the function is required to be convex so that the left-hand side is well defined. A function $f$ is concave if and only if $−f$ is convex.

#### (Epigraph) Domain of a function $\operatorname{dom}(f) = \lbrace x \in \mathbb{R}^n \mid f(x) < +\infty \rbrace$

#### Proper function $f:U \to \mathbb{R} \cup \lbrace - \infty, + \infty \rbrace$ 

If it does not attain the value $-\infty$ and $\operatorname{dom}(f) \neq \emptyset$ i.e.
1. $\forall u \in U, f (u) \neq -\infty$
2. $\exists u \in U, f (u) \neq +\infty$

#### Closed epigraph $\iff$ lower semi-continuous $\iff$ closed $\alpha$-level sets

A function is *closed* $\iff$ its *epigraph is closed*

$\iff$ A function $f : \mathbb{R}^n \to [−\infty, +\infty]$ is called *lower semi-continuous* at $x \in \mathbb{R}$ if $\liminf_ {x \to \bar x} f (x) = f (\bar x)$ for any sequence $\lbrace x_ n \rbrace_ {n \geq 1} \subseteq \mathbb{E}$ for which $x_ n \to x$ as $n \to \infty$ or at each point of $\mathbb{R}^n$ in other terms.

$\iff$ The $α$-*lower level set* of $f$ is the set: $\operatorname{lev}_ { \leq \alpha} f := \lbrace x \in S: f (x) \leq \alpha \rbrace$

#### Transform a constrained optimization into an unconstrained problem

A function that can take values $−∞$ or $+∞$ is called an *extended real-valued function*. That is $f : \mathbb{R}^n → [−∞, +∞]$. We can also denote $[−∞, +∞]$ by $\mathbb{R}\cup \{ ±∞ \}$. The domain of this function is defined by the set dom $(f) = \{x \in \mathbb{R}^n \mid f(x) < +∞ \}$

$$f(x) = 
\begin{cases} f(x) & \text{if } x \in \text{dom } \\
f = \infty & \text{otherwise} \end{cases}$$

For an arbitrary set $S \subset \mathbb{R}^n$, the *indicator function* of $S$ is defined by the following
extended real-valued function:

$$ \delta_ S (s) =
\begin{cases}
0 & \text{if }s \in S, \\
+∞ & \text{otherwise.}
\end{cases}$$

### Operations preserving convexity of functions

Weighted sum, Maximum & Linear transformation preserve all the convexity of functions

### Gradient

*Scalar input* $\to$ take the derivative $\to$ compute the linear approximation : 
We can use the chain rule to derive composed functions.

*Vector input* $\to$ take the partial derivative $\to$ compute the gradient : 
We can use the chain rule for vectors by a sum of derivatives.

### Subgradients

Given a function $f : \mathbb{R}^n → \mathbb{R}^n \cup \lbrace ∞ \rbrace$, a subgradient at $u ∈ U$ is a vector $g ∈ \mathbb{R}^n$ such that:
$∀u^\prime ∈ \mathbb{R}^n : f (u^\prime) ≥ f (u) + \langle g, u^\prime − u \rangle$
The set of *subgradients* at point $u$ is called the *subdifferential* and is denoted $∂f (u)$.

Properties:
If $f$ is convex:
- if $f$ is differentiable at $u$, then $\partial f(u) = \lbrace \nabla f(x) \rbrace$ i.e. the gradient is the single subgradient
- the function $h(u^{\prime})=f(u) + \langle g, u^{\prime}-u \rangle$ is a linear *sub-estimator* of $f$ 
- the *super-gradient* is a similar definition for a concave function.

*Non-emptiness and boundedness of the subdifferential set at interior points of the domain*. Let $f : \mathbb{R}^k → \mathbb{R} \cup \{ \infty \}$ be a proper convex function, and assume that $u \in \operatorname{int}(\operatorname{dom}(f)), \forall u$. Then $∂f(u)$ is non-empty and bounded i.e. existence of subgradient.

 #### Computing Subgradients

*Strong subgradients*: the subdifferential set at a given point is known i.e. full characterization of the subdifferential set
*Weak subgradients*: one or several subgradients at a given point are known but not all i.e. partially

*Multiplication by a positive scalar*: Let $f : \mathbb{R}^k → \mathbb{R} ∪ \lbrace \infty \rbrace$ be a proper function$, h(u) = αf (u)$ with $α > 0$. Then:
$$∀u ∈ \operatorname{dom} f , g ∈ \mathbb{R}^k : α . u ∈ ∂h(u) \iff g ∈ ∂f (u)$$

*Summation* Let $f_ 1, f_ 2 : \mathbb{R}^k → \mathbb{R}∪ \{ \infty \}$ be proper convex functions and $h(u) = f_ 1(u) + f_ 2(u)$. Then, $∀u ∈ \operatorname{dom} h, g ∈ \mathbb{R}^k$, we have $g ∈ ∂h(u) \iff g = g^{(1)} + g^{(2)}\text{ such that }g^{(1)} ∈ ∂f_ 1 (u)\text{ and }g^{(2)} ∈ ∂f_ 2 (u)$

*Maximization of subdifferential*: The following result shows how to compute the subdifferential set of a maximum of a finite collection of convex functions.

Let $f_ 1, \ldots, f_ n : \mathbb{R}^k → \mathbb{R} \cup \{ \infty \}$ be proper convex functions, and define $f(x) = \operatorname{max}(f_ 1 (x), \ldots,f_ n (x))$. Let $x ∈ \cap_i ^n \operatorname{int}(\operatorname{dom}(f_ i))$. Then, $g \in ∂f_ i (x) = \operatorname{conv} \cup_ {i∈I(x)} ∂f_ i (x)$, where $I(x) = \{ i \in \{ 1, \ldots, m\} : f_ i (x) = f(x) \}$

### Optimality conditions

#### Unconstrained optimization problem (Fermat)

Let $f : \mathbb{R}^k → \mathbb{R} ∪ \{ ∞ \}$ be a proper convex function and $\hat u ∈ \operatorname{dom} f$. If $0 \in \partial f (\hat u)$, then $f (\hat u)$ is the global minimum of $f$.

*Proof*

By the subgradient definition:

$∀u ∈ \mathbb{R}^k , g ∈ ∂f (\hat u) : f (u) ≥ f (\hat u) + \langle g, u − \hat u \rangle$. In particular, we know that $0 ∈ ∂f (\hat u)$, therefore $f (u) ≥ f (\hat u)$

#### Fenchel conjugates

Let $f : n → \mathbb{R} ∪ \{ ∞ \}$ be a function.
The *Fenchel conjugate* of $f$ is the function $f^ ∗ : \mathbb{R}^n → \mathbb{R} ∪ \{∞ \}$ defined as follows:
$$f^ ∗ (t) = \operatorname{sup}_ {u∈\operatorname{dom} f} \langle t, u \rangle − f (u)$$
The biconjugate of $f$ is the function $f^{∗∗} : \mathbb{R}^n → \mathbb{R} ∪ \{ ∞\}$ defined as follows:
$$f^{∗∗}(u) = \operatorname{sup}_ {t∈\operatorname{dom}} f^∗ \langle u, t\rangle − f^∗ (t)$$
If $f$ is proper, closed and convex, then $f^{ ∗∗} = f$

*Fenchel-Young inequality*. Let $f : \mathbb{R}^n → \mathbb{R}$ be a function, $u ∈ \operatorname{dom} f$ and $t ∈ dom \operatorname{f^* }$:
$$f (u) + f^ ∗(t) ≥ \langle u, t\rangle$$
Proof. Let $f : \mathbb{R}^n → \mathbb{R}$ be a function, $u ∈ \operatorname{dom} f$ and $t ∈ \operatorname{dom} f^ ∗$:
$$ \langle u, t \rangle − f (u) ≤ \operatorname{sup}_  {u^{\prime} ∈ \operatorname{dom} f} u^{\prime^{⊤}}y − f (u^{\prime}) = f^∗ (t)$$
By re-arranging terms, we get the expected inequality.

*Differentiable functions*: The conjugate of a differentiable function $f$ is also called the *Legendre transform* of $f$. Suppose $f$ is convex and differentiable, with $\operatorname{dom}f = \mathbb{R}^n$. Any maximizer $x^∗$ of $y^T x−f(x)$ satisfies $y = ∇f(x^∗)$, and conversely, if $x^∗$ satisfies $y = ∇f(x^∗)$, then $x^∗$ maximizes $y^T x − f(x)$. Therefore, if $y = ∇f(x^∗)$, we have $f∗(y) = x^{∗^{T}} ∇f(x^∗) − f(x^∗)$. This allows us to determine $f^∗(y)$ for any $y$ for which we can solve the gradient. Then, we have $f^∗ (y) = z^T ∇f(z) − f(z)$

*Subdifferential of a Fenchel conjuguate*. Let $f : \mathbb{R}^k → \mathbb{R} ∪ \{ \infty \}$ be a function. Let $t ∈ \operatorname{dom} f^∗$ and $$\hat u = \operatorname{arg} \operatorname{max}_ {u∈\operatorname{dom} f} ⟨u, t⟩ − f (u)$$
Then, $\hat u$ is a subgradient of $f^∗$ at $t$, i.e. $\hat u ∈ ∂f^∗ (t)$.

Proof. Although this can be proved via Danskin’s theorem, here is a simpler proof. We have $f^∗ (t) = \operatorname{max} u∈\operatorname{dom} f \langle u, t\rangle − f (u) =\langle u, t\rangle − f (\hat u)$.
For all $t^\prime ∈ \operatorname{dom} f^∗$ we have:

$$f^∗ (t) + \langle \hat u, t^\prime − t\rangle = \langle \hat u, t\rangle − f (\hat u) + \langle \hat u, t^\prime \rangle − \langle \hat u, t\rangle = \langle \hat u, t^\prime \rangle − f (\hat u) ≤ \operatorname{max}_ {u∈\operatorname{dom} f} u^⊤ t^\prime − f (u) = f^∗ (t^\prime)$$

Hence $\hat u$ is a subgradient of $f^∗$ at $t$.

#### Jensen's inequality

Let $w = \sum_i mu_ i w_i$ and $g \in \partial f(w)$, we need $w \in \operatorname{dom} f$ by previous theorem. By the definition of subgradient:
$$\forall i, f(w_ i) \geq f(w) + \langle g, w_ i -w \rangle$$

Therefore $\sum _ i mu_ i f_i(w) \geq \sum_ i mu_ i f(w) + \sum_ i mu_ i \langle g, w_ i -w \rangle$ which is $0$.

For instance,  $\log \sum_ i \exp w_ i $ (log-partition) convex ? We can prove by Jensen's or Holder's inequalities.
