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

![image](https://user-images.githubusercontent.com/109908559/218268322-9618f4bf-6d28-4e57-b7a1-1a93704bae1a.png)


(a) Consider two finite sets $S$ and $A$, and a transition kernel $P_{t}(s,a)$ or law of motion defined as:

$$P_{t}: S \rightarrow S \quad \forall t \in \mathbb{T}, \forall a \in A$$

This means that at any time $t \in \mathbb{T}$, the *law of motion* or *transition kernel* maps a state $s$ in $S$ to a new state $s'$ in $S$, given an action $a \in A$. The function $P_{t}(s,a)$ provides the probability of transitioning from state $s$ to state $s'$, when action $a$ is taken at time $t$

(b) A reward structure which is a bounded, deterministic, possibly time-dependent function of states, actions, and time epochs, and takes values in the set of non-negative integers $r_ t = r_ t(s, a) : S \times A \rightarrow \mathbb{Z}_ {\geq 0}$ for all $t \in \mathbb{T}$. We define a positive integer $⌈r⌉ \in \mathbb{N}$ as an upper bound on reward values, and assume a lower bound of 0 for the reward structure without loss of generality.

(c) A policy consists of the choice of a single action at every state and every point in time, $\pi_ t : S \rightarrow A$ for all $t \in \mathbb{T}$. To a policy $\pi = (\pi_ t)_ { \{ t \in \mathbb{T}\} }$, we associate a possibly time-dependent value function $V_ t^{\pi} : S \rightarrow \mathbb{Z}_ {\geq 0}$ defined as $V_ t^\pi (s) = \sum\limits_ {i \geq t} r_i(s_i, a_i)
$, where $s_0 = s$ is an initial state and all subsequent actions are chosen according to $\pi$. That is $at = \pi_t(s_t)$ and $s_{t+1} = a_t(s_t)$. The goal of DP is to find an optimal policy at $s_0$ at time $t = 0$, that is, to find $\pi^* = \arg\max_{\pi} V_ 0^{\pi}(s_ 0)$.

#### Bellman's optimality criteria 

It states that an optimal policy $\pi^* = (\pi_ t^* )$ is associated with the unique optimal value function $V_ t^* (s) := V_ y^{\pi^* } (s)$ satisfying $V_ t^* (s) = \max\limits_ {a \in A} \{r_ t(s, a) + V_ {t+1}^* (a_ t(s))}$ for all $t \in \mathbb{T}$ and the boundary condition $V_ T^* (s) = 0$ for all $s \in S$.

![image](https://user-images.githubusercontent.com/109908559/218268126-85372814-1ab1-442e-ba98-5e45cbb035f3.png)


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

### Quantum Linear Programming

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

### The quantum TSP

The Traveling Salesman Problem (TSP) involves finding the shortest route that visits all vertices of a fully connected graph with vertices $V = {1, . . . , n}$ starting and ending at vertex 1. The best known classical algorithm for TSP has a runtime of $O(n^22^n)$ and is based on dynamic programming (DP). The DP problem can be transformed into a reward-maximizing problem by assigning rewards to edges and rewriting the DP problem as a functional equation. A quantum oracle for the TSP problem can be constructed with $O(n^2 \text{polylog}(n, \lceil c \rceil))$ qubits, where $\lceil c \rceil$ is an upper bound on the edge weights. The quantum algorithm for TSP that makes the minimum number of queries to this oracle has $O^*(\sqrt{2n})$ queries

### The quantum MSC

### Quantum complexity lower bound

We now investigate the quantum query complexity of solving dynamic programming (DP) problems using the adversary method. The DP problems are split into two families, M1 and M2, which share the same state space, action space, and time horizon. The states in family M1 and M2 form a binary tree with a root state, with the optimal value function being T for M1 and dependent on the choice of a special state-action pair for M2. A function f is defined that receives a binary string describing the transition kernel of a problem instance in M1 or M2 and returns 0 if the optimal action at the root state is either aL or aR. The article concludes that any quantum algorithm computing the function f requires at least $\Omega(\sqrt{|S||A|})$ queries.

![image](https://user-images.githubusercontent.com/109908559/218268634-ec8e8a6c-9895-4ffb-8309-529113c8078a.png)

Theorem 5: Any quantum algorithm that computes the function $f$ above uses $\Omega(\sqrt{|S||A|})$ queries

Theorem 5 states that any quantum algorithm that computes the function $f$ requires $\Omega(\sqrt{|S||A|})$ queries. This is proven by considering a relation $R$ between instances $M1 \in M1$ and $M2 \in M2$ such that $(M1, M2) \in R$ if and only if their transition kernels differ in exactly one pair $(\bar{s}, \bar{a})$. By using a result from [6, Theorem 2], it is shown that the number of queries made by the quantum algorithm is lower bounded by $\Omega(\sqrt{|S||A|})$.

Corollary 6: A bounded-error quantum algorithm solving finite-horizon DP problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(|S|))$ makes $\Omega(\sqrt{|S||A|})$ queries to the oracle (3).

Corollary 6 states that a bounded-error quantum algorithm solving finite-horizon dynamic programming (DP) problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(|S|))$ requires $\Omega(\sqrt{|S||A|})$ queries to the oracle.

Corollary 7: A bounded-error quantum algorithm solving Problem A is optimal in $|S|$ for DP problems with $|A| = O(\text{polylog}(|S|))$ and time horizon $T = \Theta(\text{polylog}(|S|))$.

Corollary 7 states that a bounded-error quantum algorithm solving Problem A is optimal in $|S|$ for DP problems with $|A| = O(\text{polylog}(|S|))$ and time horizon $T = \Theta(\text{polylog}(|S|))$.

Proposition 8: A bounded-error quantum algorithm solving time-ordered finite-horizon DP problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(|S|))$ makes $\Omega(\sqrt{|S||A|})$ queries to the oracle (3).

It states that a bounded-error quantum algorithm solving time-ordered finite-horizon DP problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(|S|))$ requires $\Omega(\sqrt{|S||A|})$ queries to the oracle. This is proven by adding a logarithmic number of states to $S$ to make the DP problems time-ordered, and the argument of Theorem 5 remains valid.

Corollary 9. A bounded-error quantum algorithm solving Problem D for time-ordered finite-horizon DP problems with time horizon $T = \Theta(\text{polylog}(|S|))$ is optimal in $|S|$, and dependence on a $\text{poly}(\sqrt{|A|})$ factor is inevitable.

Corollary 9 states that a bounded-error quantum algorithm solving Problem D for time-ordered finite-horizon DP problems with time horizon $T = \Theta(\text{polylog}(|S|))$ is optimal in $|S|$, and dependence on a poly($\sqrt{|A|}$) factor is inevitable

![image](https://user-images.githubusercontent.com/109908559/218268331-5f3d80ef-9705-4da3-87c3-26921c2e8e0b.png)

### Classic complexity lower bound

We now examine the computational complexity of solving DP problems in a classical setting with an oracle. As in a previous section, we use techniques from adversary methods to apply them to bounded-error classical randomized algorithms.

Let M1 and M2 be families of DP instances with the same state and action spaces, and let M = M1 ⊔ M2 be the set of all instances. An algorithm that finds an optimal action at s0 can distinguish instances between M1 and M2. We use Q to represent the number of queries a deterministic algorithm makes to the oracle. We define ΠQ as the set of all deterministic algorithms that make at most Q queries to the oracle before returning an optimal action at s0. A randomized algorithm running at most Q steps is represented by a distribution μ on ΠQ.

Suppose that there exists a randomized algorithm μ ∈ P(ΠQ) that, with high probability, correctly returns an optimal action for every M ∈ M. Then, by Yao’s minimax principle, there exists a deterministic algorithm μ in ΠQ that succeeds in returning an optimal action for a large fraction of instances in M1 and M2.

Let D1 and D2 be uniform distributions on M1 and M2, respectively, and let D be the uniform mixture of the two. We define Ci as the set of instances for which a deterministic algorithm μ succeeds. It is clear that |Ci| ≥ (1 − 2ξ)|Mi| for i = 1, 2. A twin is defined as two DP instances with identical transition kernels except for one reward difference. The number of twins that a deterministic algorithm μ succeeds on is lower bounded by (1 − 4ξ)mnm.

We now define a new problem, function distinction, as the task of distinguishing between two integer-valued functions f and g defined on a discrete domain X with X = {1, ..., m}. Any deterministic algorithm μ that performs vector differentiation requires at least Ω(m) queries to distinguish at least 1/2mnm twins of functions. This result directly translates to the setting of DP problems and implies that a deterministic algorithm requires at least Ω(m) queries to distinguish at least 1/2mnm twins of DP instances.

### Is quantum magic ?

Quantum computing is not magic, but it can seem like it because it operates on principles that are different from classical computing and can lead to exponential speedup in certain tasks.
However, quantum computing is still in its early stages of development, and there are many technical challenges that must be overcome before it can be widely used. Moreover, quantum computing is not always faster than classical computing and its advantage depends on the specific problem being solved.
