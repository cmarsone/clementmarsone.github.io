---
layout: post
title: Quantum Dynamic Programming
author: inspired from Poooya Ronagh (2021)
---

### Introduction

*Dynamic programming* is a method of solving optimization problems by breaking them down into smaller subproblems and solving each subproblem only once. We will see that this approach can be applied to a wide range of problems, including the travelling salesperson problem, the minimum set-cover problem, and the edit distance problem, among others.

*Quantum dynamic programming* is an area of study that seeks to understand the potential benefits and limitations of using quantum algorithms to solve dynamic programming problems. 

Quantum algorithms have the potential to solve these problems much faster than classical algorithms, but the difficulty lies in finding algorithms that can achieve a significant speedup. This area of study is of practical significance because it has the potential to improve the performance of algorithms in various fields, such as computer science, operations research, and artificial intelligence.

#### Approach: the problem of finite-horizon dynamic programming (DP) on a quantum computer

"A DP problem is defined by a finite set of *states* $S$ or $A$, a finite set of possible actions
(decisions) A at each state, and a set of time epochs $\mathbb{T} = \lbrace 0, \ldots , T − 1 \rbrace$. Performing an action at a given state
results in a *reward* (or cost) and a transition to a new state. The goal is to find an *optimal policy*
for an *agent* at every state. Here, the measure of optimality is the future reward the agent collects
should it pursue the actions prescribed by a policy. The cumulative future reward is often called
the *value function*."

![image](https://user-images.githubusercontent.com/109908559/218268322-9618f4bf-6d28-4e57-b7a1-1a93704bae1a.png)


(a) Consider two finite sets $S$ and $A$, and a *transition kernel* $a_ {t}$ or *law of motion* defined as:

$$a_ {t}: S \rightarrow S \quad \forall t \in \mathbb{T}, \forall a \in A$$

This means that at any time $t \in \mathbb{T}$, the *law of motion* or *transition kernel* maps a state $s$ in $S$ to a new state $s'$ in $S$, given an action $a \in A$. The function $a_ {t}(s,a)$ provides the probability of transitioning from state $s$ to state $s'$, when action $a$ is taken at time $t$

(b) A *reward structure* which is a bounded, deterministic, possibly time-dependent function of states, actions, and time epochs, and takes values in the set of non-negative integers $r_ t = r_ t(s, a) : S \times A \rightarrow \mathbb{Z}_ {\geq 0}$ for all $t \in \mathbb{T}$. We define a positive integer $⌈r⌉ \in \mathbb{N}$ as an upper bound on reward values, and assume a lower bound of $0$ for the reward structure without loss of generality.

(c) **Value fonction** A *policy* consists of the choice of a single action at every state and every point in time, $\pi_ t : S \rightarrow A$ for all $t \in \mathbb{T}$. To a policy $\pi = (\pi_ t)_ { \lbrace t \in \mathbb{T}\rbrace }$, we associate a possibly time-dependent value function $V_ t^{\pi} : S \rightarrow \mathbb{Z}_ {\geq 0}$ defined as $V_ t^\pi (s) = \sum\limits_ {i \geq t} r_i(s_i, a_i)
$, where $s_0 = s$ is an initial state and all subsequent actions are chosen according to $\pi$. That is $a_ t = \pi_t(s_t)$ and $s_{t+1} = a_t(s_t)$. The goal of DP is to find an optimal policy at $s_0$ at time $t = 0$, that is, to find $\pi^* = \arg\max_{\pi} V_ 0^{\pi}(s_ 0)$.

#### Bellman's optimality criteria 

It states that an optimal policy $\pi^* = (\pi_ t^* )$ is associated with the unique optimal value function $V_ t^* (s) := V_ t^{\pi^* } (s)$ satisfying $V_ t^* (s) = \max\limits_ {a \in A} \{r_ t(s, a) + V_ {t+1}^* (a_ t(s))}$ for all $t \in \mathbb{T}$ and the boundary condition $V_ T^* (s) = 0$ for all $s \in S$.

![image](https://user-images.githubusercontent.com/109908559/218268126-85372814-1ab1-442e-ba98-5e45cbb035f3.png)


#### Query model

The *DP* problem is solved by quantum and classical algorithms that make queries to the transition kernel and reward structure. The *quantum algorithms use a coherent query process* called $U_ {DP}$, represented by:

$$ U_ {DP} \ : \ |s\rangle |a\rangle |t\rangle |x\rangle |y\rangle \rightarrow |s\rangle |a\rangle |t\rangle |x \oplus a_ t(s)\rangle |y \oplus r_ t(s, a)\rangle $$

whereas the *classical algorithms* use a similar oracle called $O_ {DP}$, represented by:

$$ O_ {DP} \ : \ (s, a, t) \rightarrow (a_ t(s), r_ t(s, a)) $$

In cases where one of the transition kernel, reward structure, or policies is independent of time, they are referred to as being *time homogeneous*. The algorithms for solving the DP problem are based on Bellman's recursion. The *value iteration operator* is defined as:

$$ \mathcal{F}^{(t)} \ : \ v_s \rightarrow \max_{a \in A} \{r_t(s, a) + v_{a_ t}(s)\} $$

The recursive applications of this operator are represented by:

$$ v^{(T-t-1)} = \mathcal{F}^{(T-t-1)}(v^{(T-t)}) \text{ , } t \in \mathbb{T} $$

where $v^{(T)} = 0$ for all $s \in S$, and $T$ represents the set of all time points. It can be seen that after applying the value iteration operator recursively, $v^{(T-k)}$ will attain the optimal value function at time $T-k$. This is represented by:

$$ V^*_{T-k}(s) = \mathcal{F}(T-k) \circ \dots \circ \mathcal{F}(T-1)(0) $$

Thus, to find the optimal action at $s_0$ at time $t=0$, it suffices to find $v(1)$ and then find the action that maximizes:

$$ \text{argmax}_{a \in A} \left[r_0(s_0, a) + v_ {a_ 0 (s_ 0)}^{(1)} \right] $$

### Quantum Linear Programming

Linear programming with high precision can be written as a linear program (LP) equivalent to the functional equation. The value function depends on the time epochs $t \in \lbrace 0, ..., T \rbrace $ and states $s \in S$. For each value of the value function $V_ t^*(s)$, we assign a real variable $v_ {s,t}$ and write the constants $r_ {t} (s, a)$ as $r_ {s,a,t}$ for consistency. The LP formulation is:

\begin{align}
\min\ v_{s_0,0} & \\
\text{s.t.} \quad v_ {s,t} &\geq r_ {s,a,t} + v_ {a(s),t+1} \quad \forall a \in A, s \in S, t \in \mathbb{T} \cup \lbrace T \rbrace \\
v_ {s,t} &\geq 0 \quad \forall s \in S, t \in \mathbb{T} \cup \lrbace T \rbrace
\end{align}

The above LP is feasible and attains a unique solution, where $v_ {s,T} = 0$ for all $s \in S$. The LP can be thought of as a network flow problem, where the inward flow of each node $(s, t)$ must match the largest outward flow toward the states $(a(s), t + 1)$ for all $a \in A$, with an added flow bias of $r_{s,a,t}$. The goal is to find the smallest required inward flow from the initial node $(s_ 0, 0)$.

The author tried to solve the LP using the multiplicative weight update method (MWUM) in a previous preprint. This technique was used in previous studies to solve semidefinite and linear programming problems. However, the scaling of the precision parameter of the solution prohibits the method from providing a quadratic quantum advantage. The MWUM requires $O(1/\epsilon^2)$ queries to return an $\epsilon$-feasible solution, which is the main drawback of the method.

The number of variables $n$ and constraints $m$ in the LP are both $\tilde{O} ( \mid S \mid)$. In the context of MWUM, the primal width $\ell$ and dual width $L$ are both $O(T\lceil r \rceil)$, where $\lceil r \rceil$ is an upper bound on the reward structure. For a generic LP solver to provide a quadratic speedup, a scaling of $O(\sqrt{\max(n,m)} \text{polylog}(\eta))$ is required, where $\eta = \ell L \epsilon$. However, it has been shown that any generic quantum LP solver with sublinear dependence on $n$ or $m$ has to depend at least polynomially on $\eta$.

Another attempt to solve DP problems using quantum computation is reported in previous studies, where the goal was to demonstrate a quadratic quantum speedup for DP problems with convex value functions. The authors aim to find a unitary transformation that evolves a register prepared in the superposition of the values of the function to the superposition of the values of the convex conjugate of the function, using polylog($\mid D \mid$, $\mid K\mid$) quantum gates. However, the existence of such a unitary is still an open problem.

### The quantum TSP

The Traveling Salesman Problem (TSP) involves finding the shortest route that visits all vertices of a fully connected graph with vertices $V = \lbrace 1, \dots, n \rbrace$. The starting vertex is fixed at $1$, and the cost of traveling from vertex $i$ to vertex $j$ is denoted by $c_ {ij}$. The best known classical algorithm for this problem is due to Bellman and Held and Karp and has a runtime of $O(n^{2}2^n) = O( \mid S \mid \mid A \mid)$.

The authors describe the problem as a Dynamic Programming (DP) problem, with a state defined as a pair $(H, i)$, where $i \in H$ and $H \subseteq V$. The action at a state $(H, i)$ corresponds to choosing a vertex $j \in H \setminus {i}$, with the instantaneous cost being $c_{ji}$. The cost function $C(H, i)$ represents the minimum total cost of a Hamiltonian path starting at 1, entering $H$, traversing $H$, and ending at $i$. The optimization problem can be written as:

$C(H, i) = \min\limits_{j \in H \setminus \lbrace i \rbrace} \bigl[ C(H \setminus \lbrace i \rbrace, j \bigr] + c_{ji}}$

The authors also note that the problem can be transformed into a reward-maximizing problem by defining $r_{ij} = \lceil c \rceil + 1 - c_{ij}$, where $\lceil c \rceil$ is an upper bound on the edge weights $c_{ij}$. The definition of states and actions can then be extended to allow $i \notin H$ and $j \notin H \setminus {i}$.

The DP problem has $O(n2^n)$ states, $O(n)$ actions, and a time horizon of $O(n)$, resulting in a time complexity of $O(n^{2}2^n})$. The authors present an oracle construction for this problem, using $O(n^{2} \text{polylog}(n, \lceil c \rceil))$ qubits and a similar number of elementary quantum gates. The oracle queries an adjacency matrix oracle and outputs the updated state and reward.

The authors also note that Problem (A) asks for a quantum algorithm for the TSP problem that makes $O^*(\sqrt{2n})$ queries to this oracle. The article concludes by stating that an algorithm with this time complexity would likely have applications in other optimization problems and could lead to breakthroughs in quantum computing.

In the context of an edge-weighted graph $G$, an oracle construction is performed to solve the TSP (Travelling Salesman Problem). A quantum oracle $UG$ is assumed for the adjacency matrix of $G$, with $2\log(n) + \log(\lceil c \rceil)$ qubits required in the registers of $UG$. The oracle $UG$ is implemented using $O(n^2\text{polylog}(n,\lceil c \rceil))$ qubits. Another oracle $UTSP$ is then constructed from $UG$, with the states $|H,i\rangle$ encoded using binary strings of size $n$ and $\log(n)$ qubits respectively. The registers in $UTSP$ are made up of $O(n\text{polylog}(n,\lceil c \rceil))$ qubits. The circuit $UTSP$ queries $UG$ and uses a total of $O(n^2\text{polylog}(n,\lceil c \rceil))$ qubits. The oracle $UTSP$ can be constructed using $O(n^2\text{polylog}(n,\lceil c \rceil))$ qubits and a similar order of quantum gates. The question of whether there exists a quantum algorithm for TSP that makes $O^(\sqrt{2n})$ queries to the oracle $UTSP$ remains open. However, a bounded-error quantum algorithm has been proposed that solves TSP in $O^(1.728n)$ but requires QRAM access to a classical algorithm.

### The quantum MSC

The minimum set-cover problem (MSC) is a problem of finding the minimum number of subsets of a given family F of m subsets Vi of a universe U with n elements, such that the union of these subsets covers the entire universe. The goal is to find the minimum cardinality F of F such that $\bar{F} = \bigcup_{V \in F} V = U$.

A dynamic programming (DP) problem can be defined to solve the MSC problem. The states of the DP problem are the subsets S of the universe U. There are two actions, u and v, where the transition from S via u at time t is the inclusion of the subset Vt+1, and the transition via v skips this inclusion. The transition via v has a reward of 1, whereas the transition via u has a reward of 0, since it adds a new set to the candidate set cover. The value function at the initial state (s0 = ∅) at time t = 0 is maximized by a policy that constructs a minimum set cover. The DP problem has a time horizon T = O(m), |A| = 2 = O(1) actions, and |S| = O(2^n) states. The best known classical algorithm for MSC has a runtime of O(m * 2^n), consisting of O(m * 2^n) queries to the classical oracle and an additional O(n) factor for set operations.

The family F can be prepared using O(mn) qubits by encoding each set Vi using a binary string of size n. Unions and set comparisons can be done using O(n) elementary quantum gates, which suffices for constructing an oracle UMSC. The oracle UMSC can be constructed using O(mn) qubits and the same order of elementary gate operations.

There are three different quantum algorithms that have been proposed for solving MSC: Problem A asks whether MSC can be solved in O*(√2n * poly(m)) queries to the oracle UMSC, while Problems C and D ask for query complexities O*(m√2n) and O*(√m * 2^n), respectively. [4] also shows a bounded-error quantum algorithm for solving MSC that uses recursive applications of Grover's search to solve the problem in O(1.728n * poly(m, n)) using quantum random access memory (QRAM).

### Quantum complexity lower bound

We now investigate the quantum query complexity of solving dynamic programming (DP) problems using the adversary method. The DP problems are split into two families, M1 and M2, which share the same state space, action space, and time horizon. The states in family M1 and M2 form a binary tree with a root state, with the optimal value function being T for M1 and dependent on the choice of a special state-action pair for M2. A function f is defined that receives a binary string describing the transition kernel of a problem instance in M1 or M2 and returns 0 if the optimal action at the root state is either aL or aR. The article concludes that any quantum algorithm computing the function f requires at least $\Omega(\sqrt{|S||A|})$ queries.

![image](https://user-images.githubusercontent.com/109908559/218268634-ec8e8a6c-9895-4ffb-8309-529113c8078a.png)

#### (Go further being more detailed)

*Theorem*. Any quantum algorithm that computes the function $f$ above uses $\Omega(\sqrt{\mid S \mid \mid A \mid})$ queries

This theorem states that any quantum algorithm that computes the function $f$ requires $\Omega(\sqrt{\mid S \mid \mid A \mid})$ queries. This is proven by considering a relation $R$ between instances $M1 \in M1$ and $M2 \in M2$ such that $(M1, M2) \in R$ if and only if their transition kernels differ in exactly one pair $(\bar{s}, \bar{a})$. By using a result, it is shown that the number of queries made by the quantum algorithm is lower bounded by $\Omega(\sqrt{\mid S \mid\mid A\mid})$.

*Corollary*. A bounded-error quantum algorithm solving finite-horizon DP problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(\mid S \mid))$ makes $\Omega(\sqrt{\mid S \mid \mid A\mid})$ queries to the oracle (3).

It states that a bounded-error quantum algorithm solving finite-horizon dynamic programming (DP) problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(\mid S \mid))$ requires $\Omega(\sqrt{\mid S\mid\mid A\mid})$ queries to the oracle.

*Corollary*. A bounded-error quantum algorithm solving Problem A is optimal in $\mid S\mid$ for DP problems with $\mid A\mid = O(\text{polylog}(\mid S \mid))$ and time horizon $T = \Theta(\text{polylog}(\mid S\mid))$.

It states that a bounded-error quantum algorithm solving Problem A is optimal in $\mid S \mid$ for DP problems with $\mid A \mid = O(\text{polylog}(\mid S \mid))$ and time horizon $T = \Theta(\text{polylog}(\mid S \mid))$.

*Proposition*. A bounded-error quantum algorithm solving time-ordered finite-horizon DP problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(\mid S \mid))$ makes $\Omega(\sqrt{\mid S\mid\mid A\mid})$ queries to the oracle (3).

It states that a bounded-error quantum algorithm solving time-ordered finite-horizon DP problems with states $S$, actions $A$, and time horizon $T = \Omega(\log(\mid S \mid))$ requires $\Omega(\sqrt{\mid S\mid \mid A \mid})$ queries to the oracle. This is proven by adding a logarithmic number of states to $S$ to make the DP problems time-ordered, and the argument of Theorem 5 remains valid.

*Corollary*. A bounded-error quantum algorithm solving Problem D for time-ordered finite-horizon DP problems with time horizon $T = \Theta(\text{polylog}(\mid S \mid))$ is optimal in $\mid S \mid$, and dependence on a $\text{poly}(\sqrt{\mid A\mid})$ factor is inevitable.

It states that a bounded-error quantum algorithm solving Problem D for time-ordered finite-horizon DP problems with time horizon $T = \Theta(\text{polylog}(\mid S \mid))$ is optimal in $\mid S\mid$, and dependence on a poly($\sqrt{\mid A\mid }$) factor is inevitable

![image](https://user-images.githubusercontent.com/109908559/218268331-5f3d80ef-9705-4da3-87c3-26921c2e8e0b.png)

### Classic complexity lower bound

We now examine the computational complexity of solving DP problems in a classical setting with an oracle. As in a previous section, we use techniques from adversary methods to apply them to bounded-error classical randomized algorithms.

Let M1 and M2 be families of DP instances with the same state and action spaces, and let M = M1 ⊔ M2 be the set of all instances. An algorithm that finds an optimal action at s0 can distinguish instances between M1 and M2. We use Q to represent the number of queries a deterministic algorithm makes to the oracle. We define ΠQ as the set of all deterministic algorithms that make at most Q queries to the oracle before returning an optimal action at s0. A randomized algorithm running at most Q steps is represented by a distribution μ on ΠQ.

Suppose that there exists a randomized algorithm μ ∈ P(ΠQ) that, with high probability, correctly returns an optimal action for every M ∈ M. Then, by Yao’s minimax principle, there exists a deterministic algorithm μ in ΠQ that succeeds in returning an optimal action for a large fraction of instances in M1 and M2.

Let D1 and D2 be uniform distributions on M1 and M2, respectively, and let D be the uniform mixture of the two. We define Ci as the set of instances for which a deterministic algorithm μ succeeds. It is clear that |Ci| ≥ (1 − 2ξ)|Mi| for i = 1, 2. A twin is defined as two DP instances with identical transition kernels except for one reward difference. The number of twins that a deterministic algorithm μ succeeds on is lower bounded by (1 − 4ξ)mnm.

We now define a new problem, function distinction, as the task of distinguishing between two integer-valued functions f and g defined on a discrete domain X with X = {1, ..., m}. Any deterministic algorithm μ that performs vector differentiation requires at least Ω(m) queries to distinguish at least 1/2mnm twins of functions. This result directly translates to the setting of DP problems and implies that a deterministic algorithm requires at least Ω(m) queries to distinguish at least 1/2mnm twins of DP instances.

### Conclusion: Is quantum magic ?

Quantum computing is not magic, but it can seem like it because it operates on principles that are different from classical computing and can lead to exponential speedup in certain tasks.
However, quantum computing is still in its early stages of development, and there are many technical challenges that must be overcome before it can be widely used. Moreover, quantum computing is not always faster than classical computing and its advantage depends on the specific problem being solved.
In conclusion, the authors provide a comprehensive study of dynamic programming on a quantum computer and the associated query complexity. Their results suggest that achieving a quadratic speedup in the number of state-action pairs may not be possible using quantum algorithms, but further research is needed to confirm this result.
