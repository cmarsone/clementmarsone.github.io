---
layout: post
title: Quantum Dynamic Programming
author: inspired from Poooya Ronagh (2021)
---

Based on the paper of Ronagh, we focus on the application of dynamic programming (DP) to quantum computing. It introduces a method for comparing quantum and classical algorithms in solving DP problems through the use of a query model. The paper gives examples of oracle constructions for various DP problems and raises questions about the possibility of a quadratic speedup in quantum algorithms. The paper also provides lower bounds for the query complexity of both quantum and classical algorithms in solving DP problems and concludes that no more than a quadratic speedup can be achieved.

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

Linear programming with high precision can be written as a linear program (LP) equivalent to the functional equation. The value function depends on the time epochs $t \in \lbrace 0, ..., T \rbrace $ and states $s \in S$. For each value of the value function $V_ t^* (s)$, we assign a real variable $v_ {s,t}$ and write the constants $r_ {t} (s, a)$ as $r_ {s,a,t}$ for consistency. The LP formulation is:

\begin{align}
\min\ v_{s_0,0} & \\
\text{s.t.} \quad v_ {s,t} &\geq r_ {s,a,t} + v_ {a(s),t+1} \quad \forall a \in A, s \in S, t \in \mathbb{T} \cup \lbrace T \rbrace \\
v_ {s,t} &\geq 0 \quad \forall s \in S, t \in \mathbb{T} \cup \lbrace T \rbrace
\end{align}

The above LP is feasible and attains a unique solution, where $v_ {s,T} = 0$ for all $s \in S$. The LP can be thought of as a network flow problem, where the inward flow of each node $(s, t)$ must match the largest outward flow toward the states $(a(s), t + 1)$ for all $a \in A$, with an added flow bias of $r_{s,a,t}$. The goal is to find the smallest required inward flow from the initial node $(s_ 0, 0)$.

The author tried to solve the LP using the multiplicative weight update method (MWUM) in a previous preprint. This technique was used in previous studies to solve semidefinite and linear programming problems. However, the scaling of the precision parameter of the solution prohibits the method from providing a quadratic quantum advantage. The MWUM requires $O(1/\epsilon^2)$ queries to return an $\epsilon$-feasible solution, which is the main drawback of the method.

The number of variables $n$ and constraints $m$ in the LP are both $\tilde{O} ( \mid S \mid)$. In the context of MWUM, the primal width $\ell$ and dual width $L$ are both $O(T\lceil r \rceil)$, where $\lceil r \rceil$ is an upper bound on the reward structure. For a generic LP solver to provide a quadratic speedup, a scaling of $O(\sqrt{\max(n,m)} \text{polylog}(\eta))$ is required, where $\eta = \ell L \epsilon$. However, it has been shown that any generic quantum LP solver with sublinear dependence on $n$ or $m$ has to depend at least polynomially on $\eta$.

Another attempt to solve DP problems using quantum computation is reported in previous studies, where the goal was to demonstrate a quadratic quantum speedup for DP problems with convex value functions. The authors aim to find a unitary transformation that evolves a register prepared in the superposition of the values of the function to the superposition of the values of the convex conjugate of the function, using polylog($\mid D \mid$, $\mid K\mid$) quantum gates. However, the existence of such a unitary is still an open problem.

### The quantum TSP

The Traveling Salesman Problem (TSP) involves finding the shortest route that visits all vertices of a fully connected graph with vertices $V = \lbrace 1, \dots, n \rbrace$. The starting vertex is fixed at $1$, and the cost of traveling from vertex $i$ to vertex $j$ is denoted by $c_ {ij}$. The best known classical algorithm for this problem is due to Bellman and Held and Karp and has a runtime of $O(n^2 2^n) = O( \mid S \mid \mid A \mid)$.

The authors describe the problem as a Dynamic Programming (DP) problem, with a state defined as a pair $(H, i)$, where $i \in H$ and $H \subseteq V$. The action at a state $(H, i)$ corresponds to choosing a vertex $j \in H \setminus \lbrace i\rbrace$, with the instantaneous cost being $c_{ji}$. The cost function $C(H, i)$ represents the minimum total cost of a Hamiltonian path starting at $1$, entering $H$, traversing $H$, and ending at $i$. The optimization problem can be written as:

$C(H, i) = \min\limits_ {j \in H \setminus \lbrace i \rbrace} \big[ C(H \setminus \lbrace i \rbrace, j \big] + c_{ji}$

The authors also note that the problem can be transformed into a reward-maximizing problem by defining $r_ {ij} = \lceil c \rceil + 1 - c_{ij}$, where $\lceil c \rceil$ is an upper bound on the edge weights $c_{ij}$. The definition of states and actions can then be extended to allow $i \notin H$ and $j \notin H \setminus \lbrace i\rbrace$.

The DP problem has $O(n2^n)$ states, $O(n)$ actions, and a time horizon of $O(n)$, resulting in a time complexity of $O(n^{2} 2^n)$. The authors present an oracle construction for this problem, using $O(n^{2} \text{polylog}(n, \lceil c \rceil))$ qubits and a similar number of elementary quantum gates. The oracle queries an adjacency matrix oracle and outputs the updated state and reward.

The paper concludes by stating that an algorithm with this time complexity would likely have applications in other optimization problems and could lead to breakthroughs in quantum computing.

In the context of an edge-weighted graph $G$, an oracle construction is performed to solve the TSP (Travelling Salesman Problem). A quantum oracle $UG$ is assumed for the adjacency matrix of $G$, with $2\log(n) + \log(\lceil c \rceil)$ qubits required in the registers of $UG$. The oracle $UG$ is implemented using $O(n^2\text{polylog}(n,\lceil c \rceil))$ qubits. Another oracle $UTSP$ is then constructed from $UG$, with the states $\mid H,i\rangle$ encoded using binary strings of size $n$ and $\log(n)$ qubits respectively. The registers in $UTSP$ are made up of $O(n\text{polylog}(n,\lceil c \rceil))$ qubits. The circuit $UTSP$ queries $UG$ and uses a total of $O(n^2 \text{polylog} (n, \lceil c \rceil))$ qubits. The oracle $UTSP$ can be constructed using $O(n^2 \text{polylog} (n, \lceil c \rceil))$ qubits and a similar order of quantum gates. The question of whether there exists a quantum algorithm for TSP that makes $O^* (\sqrt{2n})$ queries to the oracle $UTSP$ remains open. However, a bounded-error quantum algorithm has been proposed that solves TSP in $O^* (1.728^n)$ but requires QRAM access to a classical algorithm.

*Remark*: $O^∗$ notation ignores polynomial factors in $n$.

### The quantum MSC

The minimum set-cover problem (MSC) is a problem of finding the minimum number of subsets of a given family F of m subsets Vi of a universe U with n elements, such that the union of these subsets covers the entire universe. The goal is to find the minimum cardinality F of F such that $\bar{F} = \bigcup_{V \in F} V = U$.

A dynamic programming (DP) problem can be defined to solve the MSC problem. The states of the DP problem are the subsets $S$ of the universe $U$. There are two actions, $u$ and $v$, where the transition from $S$ via $u$ at time $t$ is the inclusion of the subset $V_ {t+1}$, and the transition via $v$ skips this inclusion. The transition via $v$ has a reward of $1$, whereas the transition via $u$ has a reward of $0$, since it adds a new set to the candidate set cover. The value function at the initial state $(s_ 0 = ∅)$ at time $t = 0$ is maximized by a policy that constructs a *minimum set cover*. The DP problem has a time horizon $T = O(m)$, $\mid A\mid = 2 = O(1)$ actions, and $\mid S\mid = O(2^n)$ states. The best known classical algorithm for MSC has a runtime of $O(n m 2^n)$, consisting of $O(m 2^n)$ queries to the classical oracle and an additional $O(n)$ factor for set operations.

The family $F$ can be prepared using $O(mn)$ qubits by encoding each set $V_ i \subseteq U$ using a binary string of size $n$. Unions and set comparisons can be done using $O(n)$ elementary quantum gates, which suffices for constructing an oracle UMSC. The oracle UMSC can be constructed using $O(mn)$ qubits and the same order of elementary gate operations.

### Quantum complexity lower bound

The notation "M1 ⊔ M2" means the union of sets M1 and M2. We now investigate the quantum query complexity of solving DP problems using the adversary method of \cite{aaronson2007quantum}. Our construction follows ideas from \cite{aaronson2009limits}. Consider two families of DP problem instances $M_1$ and $M_2$, depicted in Fig. 1. The two families share the same state space $S = S^{\top} \cup S_1 \cup S_2 \cup S^{\perp}$, the same action space $A$, and the same time horizon $T \in \mathbb{N}$. We let $S_1 = S_2 = \[ n \] = \lbrace 1, \dots, n \rbrace$ and assume that $\mid A \mid > 2$. The set $S^{\perp}$ is a singleton $ \mid S^{\perp} \mid = 1$. For all instances in $M_1$ and $M_2$, every action maps $s \in S^{\perp}$ to itself with a reward of $2$ and every $s \in S_2$ to itself with a reward of $0$.

The structure of $S^{\top}$ is also common between DP problem instances in $M_1$ and $M_2$. It contains the initial state $s_0 \in S^{\top}$. Let $a_L, a_R \in A$ be two fixed actions. The states in $S^{\top}$ form a binary tree with $s_0$ as the root. The role of $S^{\top}$ is to make every state in $S_1$ accessible from $s_0$ in $\lceil \log n \rceil$ steps. The actions $a_L$ and $a_R$ map every parent state to its left and right children (which might coincide) with a reward of $0$, and every action $a \in A \setminus \lbrace a_L, a_R \rbrace$ maps every state in $S^{\top}$ to itself with a reward of $1$. It is easy to see that $\mid S^{\top} \mid \leq 2^n$ and thus $\mid S \mid = \mathcal{O}(n)$.

For any $M_1 \in M_1$, every $a \in A$ maps every $s \in S_1$ to some $a(s) \in S_2$ with a reward of $0$. Therefore, the optimal value function for $M_1$ at $s_0$ is $v^*_{M_1}(s_0) = T$ and any action $a \neq a_L, a_R$ is optimal. The instances $M_2 \in M_2$ differ from those in $M_1$ only in a special state-action pair $(\bar{s}, \bar{a}) \in S_1 \times A$ for which $\bar{a}(\bar{s})$ is the single element of $S^{\perp}$ with a reward of $\bar{r} = 2$. So long as $T > 2\lceil \log(n) \rceil$, the optimal action at $s_0$ is one of $a_L$ and $a_R$, depending on the choice of $\bar{s}$. We note that in the argument that follows we could instead assume $T > \lceil \log(n) \rceil$ but use instead and set ̄$\bar{r} = T$, but this would impose a scaling constraint of $\lceil r \rceil = Ω(\log(n))$ on the reward structure.

Now, consider a function $f: {0,1}^* \rightarrow \lbrace 0,1 \rbrace$ that receives a binary string describing the transition kernel of a problem instance in $M_1 \cup M_2$ and returns $0$ if and only if the optimal action at $s_0$ is in ${a_L, a_R}$. Using the adversary method of Ambainis et al. [6], we prove a lower bound of $\Omega(n^{1/3})$ on the quantum query complexity of computing $f$.

To prove the lower bound, we consider a set $T$ of $2^{\lfloor n/3 \rfloor}$ problem instances $M_i \in M_1 \cup M_2$. Each instance is described by a binary string $x_i$ of length $O(n)$, and we can assume that $x_i$ and $x_j$ differ in at least $\lfloor n/3 \rfloor$ positions for $i \neq j$. For each instance $M_i \in T$, we choose a special state-action pair $(\bar{s}_i, \bar{a}_i)$ as described above.

We assume towards a contradiction that there exists a quantum algorithm $Q$ that computes $f$ with query complexity $q < n^{1/3}$. We use $Q$ to construct a quantum algorithm $Q'$ that solves the set disjointness problem on ${x_i}$ using at most $q$ queries. We show that such a $Q'$ cannot exist, which contradicts the assumption that $Q$ exists.

To construct $Q'$, we define a unitary operator $U$ that maps the state $\mid i\rangle \mid s\rangle \mid t\rangle \mid 0\rangle$ to $\mid i\rangle \mid s\rangle \mid t\rangle \mid f(x_i)\rangle$, where $\mid i\rangle$ is the binary encoding of $i$, $\mid s\rangle$ is a state in $S$, $\mid t\rangle$ is a time step in $\lbrace 0,1,\dots,T-1 \rbrace$, and $\mid 0\rangle$ is a classical register initialized to $0$. The operator $U$ acts on the input register $\mid i\rangle$ by applying the Hadamard transform, and then applies the query operator for $f(x_i)$ and a controlled-$Z$ gate depending on the value of $f(x_i)$.

We also define a unitary operator $V$ that maps the state $\mid i\rangle \mid j\rangle \mid s\rangle \mid t\rangle \mid 0\rangle$ to $\mid i\rangle \mid j\rangle \mid s\rangle \mid t\rangle \mid d_{ij}\rangle$, where $d_{ij} = 1$ if $x_i$ and $x_j$ differ in at most $n/3$ positions and 0 otherwise. The operator $V$ applies the Hadamard transform to the input registers $\mid i\rangle$ and $\mid j\rangle$, and then queries the input registers $\mid i\rangle$ and $\mid j\rangle$ using the quantum algorithm $Q$ for $f$. Finally, $V$ applies the $\mid d_{ij}\rangle$ state to the output register.

Using $U$ and $V$, we define a quantum algorithm $Q'$ for the set disjointness problem on $\lbrace x_i \rbrace$ as follows. We initialize $\mid0\rangle$ in the output register, and then apply $V$ to all pairs of indices $i,j$ with $i < j$.
After applying the adversary method of Ambainis [6] to the function $f$, we obtain the following quantum query complexity lower bound for solving DP problems:

$$Q(f) = \Omega\left(\sqrt{\frac{\mid M_1\mid+\mid M_2\mid}{\log(\mid M_1\mid+\mid M_2\mid)}}\right),$$

where $\mid M_1\mid$ and $\mid M_2\mid$ denote the number of instances in $M_1$ and $M_2$, respectively.


The quantum query complexity of the function $f$ is the minimum number of queries to the transition kernel of an input instance that a quantum algorithm must make to correctly determine whether $f$ outputs $0$ or $1$ with high probability.

We show that any quantum algorithm that solves this problem with bounded error must make $\Omega(\sqrt{n})$ queries to the transition kernel, where $n$ is the size of the instance. Our proof follows a standard adversary argument, which involves constructing two distributions of instances, one that leads to a positive outcome for $f$ and one that leads to a negative outcome, and showing that the algorithm cannot distinguish between the two with high probability using only a small number of queries.

The construction of the two distributions is based on the difference between the instances in $M_1$ and $M_2$. For an instance in $M_1$, the optimal action at $s_0$ is either $a_L$ or $a_R$, whereas for an instance in $M_2$, it depends on the special state-action pair $(\bar{s},\bar{a})$. We construct the two distributions by setting $(\bar{s},\bar{a})$ to be either $a_L$ or $a_R$, respectively, with equal probability.

We then use a standard argument to show that the two distributions are indistinguishable using only a small number of queries to the transition kernel. In particular, we show that for any fixed number $q$ of queries, the difference in the distributions is bounded by a term that depends on the maximum probability of reaching $\bar{s}$ from $s0$ using $q$ queries. Using the fact that $\mid S\mid\leq O(n)$ and the structure of the instance, we obtain a lower bound of $\Omega(\sqrt{n})$ for this maximum probability, and hence for the query complexity of any quantum algorithm that solves the problem with bounded error.


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

### Classical complexity lower bound

We are now investigating the computational complexity of solving DP problems in the classical setting with an oracle. Using techniques from adversary methods, we apply them to bounded-error classical randomized algorithms, as previously described in a section.

Let M1 and M2 be families of DP instances with identical state and action spaces, and let $M = M1 \cup M2$ represent the set of all instances. An algorithm that finds an optimal action at s0 can differentiate between instances in M1 and M2. We use $Q$ to represent the number of queries a deterministic algorithm makes to the oracle. $\Pi_Q$ is defined as the set of all deterministic algorithms that make at most $Q$ queries to the oracle before returning an optimal action at $s_ 0$. A randomized algorithm running for at most $Q$ steps is represented by a distribution $\mu$ on $\Pi_Q$.

If there exists a randomized algorithm $\mu \in \mathcal{P}(\Pi_Q)$ that, with high probability, returns the optimal action for every $M \in M$, then, according to Yao’s minimax principle, there exists a deterministic algorithm $\mu \in \Pi_Q$ that returns the optimal action for a large fraction of instances in M1 and M2.

Let $D_1$ and $D_2$ be the uniform distributions on M1 and M2, respectively, and let $D$ be the uniform mixture of the two. $C_i$ represents the set of instances for which a deterministic algorithm $\mu$ succeeds, where it is clear that $\mid C_ i\mid \geq (1-2\xi)\mid M_ i\mid =  (1-2\xi)mn^m$ for $i = 1, 2$. A "twin" is defined as two DP instances with identical transition kernels except for one reward difference, and the number of twins that a deterministic algorithm $\mu$ succeeds on is lower bounded by $(1-4\xi)mn^m$.

The *function distinction* problem is defined as the task of distinguishing between two integer-valued functions $f$ and $g$ defined on a discrete domain $X$ with $X = \lbrace 1, \ldots, m \rbrace$. Any deterministic algorithm $\mu$ that performs vector differentiation requires at least $\Omega(m)$ queries to distinguish at least $\frac{1}{2}mn^m$ twins of functions. This result directly translates to the setting of DP problems, implying that a deterministic algorithm requires at least $\Omega(m)$ queries to distinguish at least $\frac{1}{2}mn^m$ twins of DP instances

### Conclusion: Is quantum magic ?

Quantum computing is not magic, but it can seem like it because it operates on principles that are different from classical computing and can lead to exponential speedup in certain tasks.
However, quantum computing is still in its early stages of development, and there are many technical challenges that must be overcome before it can be widely used. Moreover, quantum computing is not always faster than classical computing and its advantage depends on the specific problem being solved.
In conclusion, the authors provide a comprehensive study of dynamic programming on a quantum computer and the associated query complexity. Their results suggest that achieving a quadratic speedup in the number of state-action pairs may not be possible using quantum algorithms, but further research is needed to confirm this result.
