---
layout: post
title: (Quantum) Dynamic programming
---

#### Aim: found an optimal solution for some combinatorial problem

### Motivations

*Shortest path*: Dynamic Programming offers a different approach for solving combinatorial optimization problems (COPs)
- Let $ D = (V , A)$ a directed graph with arc distances $c_ e$, $e \in A and a root node $s \in V$ 
- > finding the shortest from a node $s$ to ecery other node $v \in V$

![image](https://user-images.githubusercontent.com/109908559/217756375-185fc715-ecb3-499f-8b89-4bbd048ddd50.png)

*Complexity* $=O(n^2)$

#### Induction
By increasing *k* from $1$ to $n − 1$ and computing each time
$D_ k (j)$, $∀j ∈ V$ by recurrence, we get an algorithmin  $O(mn)$ et
$d(j) = D_ {n−1} (j)$.
This technique where the optimal solution is calculated by reccurence from the solution
of different slightly problems is called *Dynamic Programming*.

The following terminology will be used:
1. Optimality : property of some parts of optimal solutions that are themselves optimal
2. States : Nodes that need different operations.
3. Steps : steps which define the order we have to follow.

*Knapsack* : Assuming that the RHS $λ$ taking values $0, \ldots , b$ represent the states and the subset of variables $x_ 1, \ldots , x_ r$ ,
represented by $r$ steps, we get the following formula $P_ r (λ)$ :

$$\begin{align*}
f(\lambda) = \max_{\mathbf{x} \in \mathbb{B}} &\sum_{j=1}^{r} c_j x_j \
\text{s.t.} &\sum_{j=1}^{r} a_j x_j \leq \lambda
\end{align*}$$

where $f_ r (λ)$ is the optimal value of $P_ r (λ)$.
Thus, $z = f_ n (b)$ gives the optimal value for the knapsack problem.

Let $\mathcal{P}_ {r}(\lambda)$ be the optimal value of the knapsack problem with capacity $\lambda$, and let $f_ {r}(\lambda)$ be the corresponding value of the relaxed problem. The value of the knapsack problem is given by $z=f_ {n}(b)$.

We need to define a recurrence to calculate $f_{r}(\lambda)$ in terms of values $f_{s}(\mu)$ for $s \leq r$ and $\mu \leq \lambda$.

- Optimial solution

To obtain the optimal solution of the knapsack problem, we start from the optimal value of $f_{n}(b)$. There are two cases:
If $x_{r}^{*}=0$, then $f_{r}(\lambda)=f_{r-1}(\lambda)$.
If $x_{r}^{*}=1$, then $f_{r}(\lambda)=c_{r}+f_{r-1}(\lambda-a_{r})$.
By repeating this process $n$ times, we obtain the optimal solution.

- Initialization

$f_{r}(\lambda)=-\infty$, for $r \geq 0$ and $\lambda < 0$.

$f_{r}(0)=0$, for $r \geq 0$.

$f_{0}(\lambda)=0$, for $\lambda \geq 0$.

The complexity of the dynamic programming algorithm is $O(nb)$.

The recurrence for the $0-1$ knapsack problem can be derived in a similar manner. If $x^{}$ is the optimal solution for the problem $\mathcal{P}{r}(\lambda)$ for a value of $g{r}(\lambda)$, then we retain the value of $x^{}_{r}$.

If $x^{*}_ {r}=t$, then $g_ {r}(\lambda)=c_{r}t+g_{r-1}(\lambda-t a_{r})$ for $t=0, \dots , b \lambda/a_{r}$ according to the principle of optimality.
Therefore, the following recurrence formula:
$g_{r}(\lambda)=\max_{t=0, \dots , b \lambda/a_{r}} {c_{r}t+g_{r-1}(\lambda-t a_{r}) }$

The worst case complexity of this algorithm is $O(nb^{2})$. Can this algorithm be improved? Is it possible to reduce the calculation of $g_{r}(\lambda)$ to a comparison of two cases?
