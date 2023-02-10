---
layout: post
title: Quantum Dynamic Programming inspired from Poooya Ronagh
---

### Introduction: Nothing is magic ?

Quantum dynamic programming is an area of study that seeks to understand the potential benefits and limitations of using quantum algorithms to solve dynamic programming problems. Dynamic programming is a method of solving optimization problems by breaking them down into smaller subproblems and solving each subproblem only once. This approach can be applied to a wide range of problems, including the travelling salesperson problem, the minimum set-cover problem, and the edit distance problem, among others.

Quantum algorithms have the potential to solve these problems much faster than classical algorithms, but the difficulty lies in finding algorithms that can achieve a significant speedup. The study of quantum dynamic programming seeks to understand the conditions under which quantum algorithms can achieve a speedup and the limitations that prevent such a speedup. This area of study is of practical significance because it has the potential to improve the performance of algorithms in various fields, such as computer science, operations research, and artificial intelligence.

#### Approach

This paper is concerned with the problem of dynamic programming on a quantum computer. The authors focus on finite-horizon dynamic programming problems, which are of great interest in many areas of discrete and combinatorial algorithms, including the traveling salesperson problem (TSP) and the minimum set-cover problem (MSC). The authors study the query complexity of dynamic programming problems, that is, they aim to solve the problems with the fewest queries to an oracle that simulates the effects of performing an action.

In this paper, the authors introduce a general framework for studying finite-horizon dynamic programming problems on a quantum computer and provide a query model for bounded-error quantum algorithms that make coherent queries to an oracle representative of the dynamic programming problem. They also state several open problems related to the potential existence of quadratic quantum speedups in solving dynamic programming problems.

The authors provide several example constructions of the dynamic programming oracle for TSP, MSC, and the edit distance problem, and prove lower bounds for the query complexity of quantum and classical randomized algorithms for solving these problems. They show that a greater-than-quadratic speedup cannot be achieved using quantum algorithms. They also provide a quantum query complexity lower bound of Ω(√|S||A|) for solving dynamic programming problems using the generalized relational adversary method.

In conclusion, the authors provide a comprehensive study of dynamic programming on a quantum computer and the associated query complexity. Their results suggest that achieving a quadratic speedup in the number of state-action pairs may not be possible using quantum algorithms, but further research is needed to confirm this result.

#### Looking at the big picture

Dynamic Programming (DP) is a mathematical framework for solving decision making problems over a finite set of time epochs (T). The DP framework consists of two sets, S and A, which are finite sets of states and actions, respectively. The problem also involves a transition kernel or law of motion and a reward structure, which is a function of states, actions, and time epochs. The goal of DP is to find the optimal policy, which is a sequence of actions, that maximizes the reward. Bellman's optimality criteria are used to determine the optimal policy. The value iteration operator is defined as F(t) and the algorithm solves the DP problem by iteratively applying F(t) to the value function. The DP problem can be solved with quantum or classical algorithms that make queries to the transition kernel and reward structure.

#### Notations

"A DP problem is defined by a finite set of *states* $S$ or $A$, a finite set of possible actions
(decisions) A at each state, and a set of time epochs $\mathbb{T} = \{ 0, \ldots , T − 1 \}$. Performing an action at a given state
results in a *reward* (or cost) and a transition to a new state. The goal is to find an *optimal policy*
for an *agent* at every state. Here, the measure of optimality is the future reward the agent collects
should it pursue the actions prescribed by a policy. The cumulative future reward is often called
the *value function*."

(a) Consider two finite sets $S$ and $A$, and a transition kernel $P_{t}(s,a)$ or law of motion defined as:

$$P_{t}: S \rightarrow S \quad \forall t \in T, \forall a \in A$$

This means that at any time $t \in T$, the law of motion or transition kernel maps a state $s$ in $S$ to a new state $s'$ in $S$, given an action $a \in A$. The function $P_{t}(s,a)$ provides the probability of transitioning from state $s$ to state $s'$, when action $a$ is taken at time $t$

(b) A reward structure which is a bounded, deterministic, possibly time-dependent function of states, actions, and time epochs, and takes values in the set of non-negative integers $rt = rt(s, a) : S \times A \rightarrow \mathbb{Z}_{\geq 0}$ for all $t \in T$. We define a positive integer $⌈r⌉ \in \mathbb{N}$ as an upper bound on reward values, and assume a lower bound of 0 for the reward structure without loss of generality.

A policy consists of the choice of a single action at every state and every point in time, $\pi_t : S \rightarrow A$ for all $t \in T$. To a policy $\pi = (\pi_t){t \in T}$, we associate a possibly time-dependent value function $V{\pi}^t : S \rightarrow \mathbb{Z}{\geq 0}$ defined as $\sum{i \geq t} r_i(s_i, a_i)$, where $s_0 = s$ is an initial state and all subsequent actions are chosen according to $\pi$. The goal of DP is to find an optimal policy at $s_0$ at time $t = 0$, that is, to find $\pi^* = \arg\max_{\pi} V_{\pi}^0(s_0)$.

Bellman's optimality criteria state that an optimal policy $\pi^* = (\pi^_t)$ is associated with the unique optimal value function $V^t(s) := V{\pi^}^t(s)$ satisfying $V^t(s) = \max{a \in A} {rt(s, a) + V^_{t+1}(at(s))}$ for all $t \in T$ and the boundary condition $V^_T(s) = 0$ for all $s \in S$.

We consider quantum and classical algorithms that make queries to the transition kernel and reward structure to solve a DP problem. The quantum algorithms make coherent queries to $UDP : |s\rangle |a\rangle |t\rangle |x\rangle |y\rangle \rightarrow |s\rangle |a\rangle |t\rangle |x \oplus at(s)\rangle |y \oplus rt(s, a)\rangle$, while the classical algorithms make classical queries to $ODP : (s, a, t) \rightarrow (at(s), rt(s, a))$.

Based on Bellman's recursion, we consider two algorithms for solving the DP problem. We define the value iteration operator $F(t) : \mathbb{Z}_{\geq 0}^{|S|} \rightarrow
