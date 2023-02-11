---
layout: post
title: Quantum Dynamic Programming inspired from Poooya Ronagh
---

### Introduction

*Dynamic programming* is a method of solving optimization problems by breaking them down into smaller subproblems and solving each subproblem only once. We will see that this approach can be applied to a wide range of problems, including the travelling salesperson problem, the minimum set-cover problem, and the edit distance problem, among others.

*Quantum dynamic programming* is an area of study that seeks to understand the potential benefits and limitations of using quantum algorithms to solve dynamic programming problems. 

Quantum algorithms have the potential to solve these problems much faster than classical algorithms, but the difficulty lies in finding algorithms that can achieve a significant speedup. The study of quantum dynamic programming seeks to understand the conditions under which quantum algorithms can achieve a speedup and the limitations that prevent such a speedup. This area of study is of practical significance because it has the potential to improve the performance of algorithms in various fields, such as computer science, operations research, and artificial intelligence.

#### Approach: the problem of finite-horizon dynamic programming (DP) on a quantum computer

This paper is concerned with the problem of dynamic programming on a quantum computer. The authors focus on finite-horizon dynamic programming problems, which are of great interest in many areas of discrete and combinatorial algorithms, including the traveling salesperson problem (TSP) and the minimum set-cover problem (MSC). The authors study the query complexity of dynamic programming problems, that is, they aim to solve the problems with the fewest queries to an oracle that simulates the effects of performing an action.

In this paper, the authors introduce a general framework for studying finite-horizon dynamic programming problems on a quantum computer and provide a query model for bounded-error quantum algorithms that make coherent queries to an oracle representative of the dynamic programming problem. They also state several open problems related to the potential existence of quadratic quantum speedups in solving dynamic programming problems.

The authors provide several example constructions of the dynamic programming oracle for TSP, MSC, and the edit distance problem, and prove lower bounds for the query complexity of quantum and classical randomized algorithms for solving these problems. They show that a greater-than-quadratic speedup cannot be achieved using quantum algorithms. They also provide a quantum query complexity lower bound of $Ω(\sqrt{|S||A|})$ for solving dynamic programming problems using the generalized relational adversary method.

In conclusion, the authors provide a comprehensive study of dynamic programming on a quantum computer and the associated query complexity. Their results suggest that achieving a quadratic speedup in the number of state-action pairs may not be possible using quantum algorithms, but further research is needed to confirm this result.

#### Looking at the big picture

"A DP problem is defined by a finite set of *states* $S$ or $A$, a finite set of possible actions
(decisions) A at each state, and a set of time epochs $\mathbb{T} = \{ 0, \ldots , T − 1 \}$. Performing an action at a given state
results in a *reward* (or cost) and a transition to a new state. The goal is to find an *optimal policy*
for an *agent* at every state. Here, the measure of optimality is the future reward the agent collects
should it pursue the actions prescribed by a policy. The cumulative future reward is often called
the *value function*."

(a) Consider two finite sets $S$ and $A$, and a transition kernel $P_{t}(s,a)$ or law of motion defined as:

$$P_{t}: S \rightarrow S \quad \forall t \in \mathbb{T}, \forall a \in A$$

This means that at any time $t \in \mathbb{T}$, the *law of motion* or *transition kernel* maps a state $s$ in $S$ to a new state $s'$ in $S$, given an action $a \in A$. The function $P_{t}(s,a)$ provides the probability of transitioning from state $s$ to state $s'$, when action $a$ is taken at time $t$

(b) A reward structure which is a bounded, deterministic, possibly time-dependent function of states, actions, and time epochs, and takes values in the set of non-negative integers $r_ t = r_ t(s, a) : S \times A \rightarrow \mathbb{Z}_ {\geq 0}$ for all $t \in \mathbb{T}$. We define a positive integer $⌈r⌉ \in \mathbb{N}$ as an upper bound on reward values, and assume a lower bound of 0 for the reward structure without loss of generality.

(c) A policy consists of the choice of a single action at every state and every point in time, $\pi_ t : S \rightarrow A$ for all $t \in \mathbb{T}$. To a policy $\pi = (\pi_ t)_ { \{ t \in \mathbb{T}\} }$, we associate a possibly time-dependent value function $V_ t^{\pi} : S \rightarrow \mathbb{Z}_ {\geq 0}$ defined as $V_ t^\pi (s) = \sum\limits_ {i \geq t} r_i(s_i, a_i)
$, where $s_0 = s$ is an initial state and all subsequent actions are chosen according to $\pi$. That is $at = \pi_t(s_t)$ and $s_{t+1} = a_t(s_t)$. The goal of DP is to find an optimal policy at $s_0$ at time $t = 0$, that is, to find $\pi^* = \arg\max_{\pi} V_ 0^{\pi}(s_ 0)$.

#### Bellman's optimality criteria 

It states that an optimal policy $\pi^* = (\pi_ t^* )$ is associated with the unique optimal value function $V_ t^* (s) := V_ y^{\pi^* } (s)$ satisfying $V_ t^* (s) = \max\limits_ {a \in A} \{r_ t(s, a) + V_ {t+1}^* (a_ t(s))}$ for all $t \in \mathbb{T}$ and the boundary condition $V_ T^* (s) = 0$ for all $s \in S$.

#### Query model

The *DP* problem is solved by quantum and classical algorithms that make queries to the transition kernel and reward structure. The *quantum algorithms use a coherent query process* called $U_ {DP}$, represented by:

$$ U_ {DP} \ : \ |s\rangle |a\rangle |t\rangle |x\rangle |y\rangle \rightarrow |s\rangle |a\rangle |t\rangle |x \oplus at(s)\rangle |y \oplus rt(s, a)\rangle $$

whereas the *classical algorithms* use a similar oracle called $O_ {DP}$, represented by:

$$ O_ {DP} \ : \ (s, a, t) \rightarrow (at(s), rt(s, a)) $$

In cases where one of the transition kernel, reward structure, or policies is independent of time, they are referred to as being *time homogeneous*. The algorithms for solving the DP problem are based on Bellman's recursion. The *value iteration operator* is defined as:

$$ F^{(t)} \ : \ v_s \rightarrow \max_{a \in A} {r_t(s, a) + v_{at(s)}} $$

The recursive applications of this operator are represented by:

$$ v^{(T-t-1)} = \mathcal{F}^{(T-t-1)}(v^{(T-t)}) t \in T $$

where $v(T) = 0$ for all $s \in S$, and $T$ represents the set of all time points. It can be seen that after applying the value iteration operator recursively, $v(T-k)$ will attain the optimal value function at time $T-k$. This is represented by:

$$ V^*_{T-k}(s) = F(T-k) \circ \dots \circ F(T-1)(0) $$

Thus, to find the optimal action at $s_0$ at time $t=0$, it suffices to find $v(1)$ and then find the action that maximizes:

$$ \text{argmax}_{a \in A} \left[r_0(s_0, a) + v(1) a_0(s_0)\right] $$

Based on Bellman's recursion, we consider two algorithms for solving the DP problem. We define the value iteration operator $F(t) : \mathbb{Z}_{\geq 0}^{|S|} \rightarrow$

Linear programming with high precision can be written as a linear program (LP) equivalent to the functional equation. The value function depends on the time epochs $t \in {0, ..., T}$ and states $s \in S$. For each value of the value function $V^*t(s)$, we assign a real variable $v{s,t}$ and write the constants $r_{t}(s, a)$ as $r_{s,a,t}$ for consistency. The LP formulation is:

\begin{align}
\min\ v_{s_0,0} \
\text{s.t.} \quad v_{s,t} &\geq r_{s,a,t} + v_{a(s),t+1} \quad \forall a \in A, s \in S, t \in T \
v_{s,t} &\geq 0 \quad \forall s \in S, t \in T \cup {T}
\end{align}

The above LP is feasible and attains a unique solution, where $v_{s,T} = 0$ for all $s \in S$. The LP can be thought of as a network flow problem, where the inward flow of each node $(s, t)$ must match the largest outward flow toward the states $(a(s), t + 1)$ for all $a \in A$, with an added flow bias of $r_{s,a,t}$. The goal is to find the smallest required inward flow from the initial node $(s_0, 0)$.

The author tried to solve the LP using the multiplicative weight update method (MWUM) in a previous preprint. This technique was used in previous studies to solve semidefinite and linear programming problems. However, the scaling of the precision parameter of the solution prohibits the method from providing a quadratic quantum advantage. The MWUM requires $O(1/\epsilon^2)$ queries to return an $\epsilon$-feasible solution, which is the main drawback of the method.

The number of variables $n$ and constraints $m$ in the LP are both $\tilde{O}(|S|)$. In the context of MWUM, the primal width $\ell$ and dual width $L$ are both $O(T\lceil r \rceil)$, where $\lceil r \rceil$ is an upper bound on the reward structure. For a generic LP solver to provide a quadratic speedup, a scaling of $O(\sqrt{\max(n,m)} \text{polylog}(\eta))$ is required, where $\eta = \ell L \epsilon$. However, it has been shown that any generic quantum LP solver with sublinear dependence on $n$ or $m$ has to depend at least polynomially on $\eta$.

Another attempt to solve DP problems using quantum computation is reported in previous studies, where the goal was to demonstrate a quadratic quantum speedup for DP problems with convex value functions. The authors aim to find a unitary transformation that evolves a register prepared in the superposition of the values of the function to the superposition of the values of the convex conjugate of the function, using polylog($|D|$, $|K|$) quantum gates. However, the existence of such a unitary is still an open problem.

### Is quantum magic ?

Quantum computing is not magic, but it can seem like it because it operates on principles that are different from classical computing and can lead to exponential speedup in certain tasks.
However, quantum computing is still in its early stages of development, and there are many technical challenges that must be overcome before it can be widely used. Moreover, quantum computing is not always faster than classical computing and its advantage depends on the specific problem being solved.
