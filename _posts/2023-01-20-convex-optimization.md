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

If it does not attain the value $-\infty$ and $\operatorname{dom}(f) \neq \0$ i.e.
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
$∀u\prime ∈ \mathbb{R}^n : f (u\prime) ≥ f (u) + \langle g, u\prime − u \rangle$
The set of *subgradients* at point $u$ is called the *subdifferential* and is denoted $∂f (u)$.

Properties:
IF $f$ is convex:
- if $f$ is differentiable at $u$, then $\partial f(u) = \lbrace \nabla f(x) \rbrace i.e. the gradient is the single subgradient
- the function $h(u^{\prime})=f(u) + \langleg, u^{\prime}-u \rangle$ is a linear *sub-estimator* of $f$ 
- the *super-gradient* is a similar definition for a concave fucnrion



beck 3.14Theorem 3.14 (nonemptiness and boundedness of the subdifferential set at interior points of the domain). Let f : E → (−∞,∞] be a proper convex function, and assume that x ̃ ∈ int(dom(f)). Then ∂f(x ̃) is nonempty and bounded.


 #### compute subgradients 3.4

strong and weak subgradients

multiplication by a positive scalar 3,35
Theorem 3.35. Let f : E → (−∞, ∞] be a proper function and let α > 0. Then for any x ∈ dom(f)
∂(αf)(x) = α∂f(x).
 
summation 3.36
Theorem 3.36. Let f1,f2 : E → (−∞,∞] be proper convex functions, and let x ∈ dom(f1) ∩ dom(f2).
(a) The following inclusion holds:
∂f1(x) + ∂f2(x) ⊆ ∂(f1 + f2)(x).
(b) If x ∈ int(dom(f1)) ∩ int(dom(f2)), then
∂(f1 + f2)(x) = ∂f1(x) + ∂f2(x).

maimization 3.50
The following result shows how to compute the subdifferential set of a maximum of a finite collection of convex functions.
Theorem 3.50 (max rule of subdifferential calculus). Let f1, f2, . . . , fm : E → (−∞, ∞] be proper convex functions, and define
f(x) = max{f1(x),f2(x),...,fm(x)}. Let x ∈ mi=1 int(dom(fi)). Then

∂f(x) = conv ∪i∈I(x)∂fi(x) , where I(x) = {i ∈ {1,2,...,m} : fi(x) = f(x)}.

un constrained optimization pronlem fermat s theorem

#### Fenchel conjugates

Fenchel’s inequality
From the definition of conjugate function, we immediately obtain the inequality f(x) + f∗(y) ≥ xT y
for all x, y. This is called Fenchel’s inequality (or Young’s inequality when f is differentiable).
For example with f(x) = (1/2)xT Qx, where Q ∈ Sn++, we obtain the inequality xT y ≤ (1/2)xT Qx + (1/2)yT Q−1y.
Conjugate of the conjugate
The examples above, and the name ‘conjugate’, suggest that the conjugate of the conjugate of a convex function is the original function. This is the case provided a technical condition holds: if f is convex, and f is closed (i.e., epi f is a closed set; see §A.3.3), then f∗∗ = f. For example, if domf = Rn, then we have f∗∗ = f, i.e., the conjugate of the conjugate of f is f again 

Differentiable functions
The conjugate of a differentiable function f is also called the Legendre transform of f. (To distinguish the general definition from the differentiable case, the term Fenchel conjugate is sometimes used instead of conjugate.)
Suppose f is convex and differentiable, with domf = Rn. Any maximizer x∗ of yT x−f(x) satisfies y = ∇f(x∗), and conversely, if x∗ satisfies y = ∇f(x∗), then x∗ maximizes yT x − f(x). Therefore, if y = ∇f(x∗), we have
f∗(y) = x∗T ∇f(x∗) − f(x∗).
This allows us to determine f∗(y) for any y for which we can solve the gradient
Then we have f∗(y) = zT ∇f(z) − f(z).




Jensen's inequality
let w =sum_i mu_ i w_i and g in partial f(w), we need w in dom f by previous theorem
by def of subgradient:
forall i f(w_ i) >= f(w) + <g, w_ i -w >
therefore sum _ i mu_ i f_i(w) >= sum mu_ i f(w) + sum mu i <g, w i-w> which is 0

example: is log-partition = log sum exp w_ i convex ? proof by jensen or holder s inequalities
