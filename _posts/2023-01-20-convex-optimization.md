---
layout: post
title: Convex Optimization
---

#### Convex set

A set $U leg R^n$ is convex iff forall u, u^' in U, exists epsilon in 0, 1 s.t. epsilon u

#### Convex Hull

conv U = simplex 

#### Convex function 

*Convex sets* : A set $X⊆R^n$ is convex if and only if:
∀x,x′ ∈X,ε∈[0,1]:εx+(1−ε)x′ ∈X,
or, in other words, any point which is a convex combination of points in X must also be in X.

*Convex and concave functions*
LetX⊆Rn beaconvexset.Afunctionf:X→Risconvexifandonlyif:
∀x,x′ ∈X,ε∈[0,1]:f(εx+(1−ε)x′)≤εf(x)+(1−ε)f(x′)
Note that the domain of the function is required to be convex so that the left-hand side is well defined. A function f is concave if and only if −f is convex.

Hessian, Positive semi-definitive matrix and its equivalence with convex function
proper function, Closed function iff its epigraph is closed equivlent to semi lower continuity

Extended real value extension => transform a constrained optimization problem into an unconstrained problem

Only at this subsection, we adopt the following rule:
0·∞ = ∞·0 = 0·(−∞) = (−∞)·0 = 0.
μ2 2 +L − μ∥x − y∥2,
and the result follows after some simplifications.

*Extended Real-Valued Functions* : A function that can take values −∞ or +∞ is called an extended real-valued function. That is f : Rn → [−∞, +∞]. We can also denote [−∞, +∞] by R ∪ {±∞}. The domain of this function is defined by the set dom(f) = {x ∈ Rn | f(x) < +∞}.

For an arbitrary set S ⊂ Rn, the indicator function of S is defined by the following
extended real-valued function:

A function f : Rn → [−∞, +∞] is called *proper *if it does not attain the value −∞ and dom(f) ̸= ∅. This function is called closed if its epigraph is a closed set.
A function f : Rn → [−∞, +∞] is called lower *semicontinuous *at x ∈ R if f(x) ≤ lim inf f(xn)
n→∞
for any sequence {xn}∞n=1 for which xn → x. Therefore, a function f: Rn → [−∞,+∞] is called
lower semicontinous if it is lower semicontinuous at each point of Rn.
Theorem 5.28 Let f : Rn → [−∞, +∞]. Then the following conditions are equivalent:
1. f is lower semicontinuous.
2. f is closed.
3. For any λ ∈ R, the λ-level sets Lλ of f (see Theorem 5.3) are closed.

Definition 5.29 An extended real-valued function f: Rn → [−∞,+∞] is called convex if its epi-
graph is a convex set.
Therefore, we can show that the a proper extended real-valued function is a convex function if and only if it satisfies the condition for usual functions (Definition 5.1) using the rule (10).

### Operations preserving convexity of functions

Weighted sum of functions Beck 2.7 2.16
Maximum sum of functions
linear transformation (convex)

Scalar inout 
derivative:
Linear approximation : 
Chain rule

 Vector input:
partial derivative:
gradient:
chain rule for vector (sum):

### Subgradients

Definition 3.6: Subgradient
Given a function f : X ⊆ Rn → R, a subgradient of f at x ∈ X is a vector g ∈ Rn such that: ∀x′∈X: f(x′)≥f(x)+g⊤(x′−x)
The set of subgradients at point x is called the subdifferential and is denoted ∂f(x).

Properties:
f is convex 
- if f is differentiable at u then partial f(u) = {nab,a f(x)
- sub estimator h u' 
- super gradient is a similar definition for. oncave fucnrion



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
