---
layout: post
title: Entanglers in 2-player-N-strategies quantum games
author: Clément
---

## Abstract 

We discuss the construction of entanglers in 2-player-N-strategies quantum games. In these games, each player has a normalized vector in an $N$-dimensional Hilbert space upon which they apply their strategy. A normalized vector in an $N$-dimensional Hilbert space $\mathcal{H}_ \mathcal{N}$ can be represented as: $\vec{x} \in \mathcal{H}_ \mathcal{N}$, $\mid\vec{x}\mid = 1$, where $\mid\cdot\mid$ denotes the norm. The players draw their payoffs from a state $\vert \Psi \rangle = J^{\dagger}U_1 \otimes U_2 J \vert \Psi_0 \rangle \in \mathcal{H}_ N \otimes \mathcal{H}_ N$. Here, $\vert \Psi_0 \rangle$ and $J$ (both determined by the game’s referee) are respectively an unentangled $2$-qubit (pure) state and a unitary operator such that $\vert \Psi_1 \rangle \equiv J\vert \Psi_0 \rangle \in \mathcal{H}_ N \otimes \mathcal{H}_ N$ is partially entangled. The degree of entanglement of the state is related to the existence of pure strategy Nash equilibrium in the quantum game. The paper suggests an algorithm to construct a special quantum gate that should be useful not only in quantum games but also as a special gate in manipulating quantum information protocols. The gate generates partially entangled states whose degree of entanglement is controlled by a single real parameter, and this property is referred to as single parameter completeness. The paper discusses the relevance of the problem to quantum information and suggests an extension of the algorithm to $N>2$.

## Introduction

The theory of quantum games is a growing area of research that explores the application of quantum mechanics to fields outside of physics, such as economics, finance, and gambling. This is done by "quantizing" classical games, which involves formulating rules and allowing players to use quantum information tools, such as qubits and quantum gates, to make decisions. One example of a quantum game is the 2-2 game, which is based on a classical game that involves two players and two strategies

## The Role of Entanglement in Quantum Games

There is significant research on the quantized version of classical strategic 2-2 games, with most of it based on a protocol specified in [Quantum Games and Quantum Strategies](https://journals.aps.org/prl/abstract/10.1103/PhysRevLett.83.3077). The protocol requires the application of an entanglement (unitary) operator $J(β)$, where $β$ is a real parameter, on a non-entangled 2-qubit (pure) state. The resulting state is entangled, and its degree of entanglement is measured by its von-Neumann entropy $S_2(β)$. A desired property of $J(β)$ is that $S_2(β)$ is a continuous function of $β$ that varies between $0$ and $\log2$ (maximal entanglement). The degree of entanglement is crucial for the existence of pure strategy Nash equilibrium in the 2-2 quantum game. The problem of controlling the entropy by a single parameter that varies between $0$ and $\log2$ is known as single parameter completeness. The design of an entanglement gate $J(β)$ that generates entangled states with a degree of entanglement controlled by a single parameter should be useful in quantum information.

## Classical Commensurability

The passage describes the construction and properties of a parameterized entangler $J(\beta)$ for a 2-2 quantum game. The entangler can be constructed easily from classical strategies, and its action on an unentangled 2-qubit state yields a Schmidt-decomposed form, enabling the computation of the corresponding entanglement entropy. The entangler satisfies single parameter completeness and is periodic and symmetric. The entangler also has a property called *classical commensurability*, which means that players in a 2-2 quantum game can use their classical strategies as a special case and collect the corresponding classical payoffs. However, *classical commensurability* does not hold for $N > 2$. The specific details of the entangler and its properties are as follows.

In a 2-2 game, the classical strategy of a player is denoted by $i\sigma_y \in SU(2)$, and $J(\beta) = e^{-i\beta/2}\sigma_y \otimes \sigma_y$ is an appropriate construction for the entangler. The action of $J(\beta)$ on an unentangled 2-qubit state, such as $\mid 00\rangle$, yields $J(\beta)\mid 00\rangle = \cos(\beta/2)\mid 00\rangle - i\sin(\beta/2)\mid 11\rangle$. The Schmidt-decomposed form of $\mid \Psi_1\rangle = J(\beta)\mid 00\rangle$ enables the computation of the corresponding entanglement entropy $S_2(\beta)$, which is a continuous function of $\beta$ and gets all values in $\[ 0, \log 2\]$. $S_2(\beta)$ is periodic with period $\pi$, symmetric about the midpoint $\pi/2$, with $S_2(0) = 0$ and $S_2(\pi/2) = \log 2$. $J(\beta)$ satisfies single parameter completeness. $J(\beta)$ has a property referred to as classical commensurability, $\[ J(\beta),\sigma_y\otimes\sigma_y \]=0$, which means that players in a 2-2 quantum game can use their classical strategies as a special case and collect the corresponding classical payoffs. Classical commensurability does not hold for $N > 2$.

## The present work

The article examines now the construction of the entangler $J(\beta)$ for a 2-N quantum game based on a 2-players-N-strategies classical game. For $N=3,4$, the corresponding von-Neumann entropy $S_N(\beta)$ satisfies single parameter completeness. However, for $N>4$, $S_N(\beta) < \log N$, and another method is suggested to design $J(\beta)$ that satisfies single parameter completeness for any $N$. The article introduces the classical 2-3 game and formulates its quantum version before addressing the construction of $J(\beta)$.

## Two-Players-Three-Strategies Classical Games: Trits

Consider a two-player classical game with three strategies for each player. The game can be represented using a trit with three values: $C=\mid 1 \rangle$, $S=\mid 2 \rangle$, and $D=\mid 3 \rangle$, corresponding to Confess, Stay quiet, and Don't confess respectively. The game is played in nine two-trit states $\mid ij \rangle$, where $i,j = 1,2,3$, representing the entries of the game table. The classical game protocol involves the players deciding whether to leave their respective trit state as it is or to change it to either $\mid 2 \rangle$ or $\mid 3 \rangle$. The classical strategies of the players can be represented using the permutation group $S_3$, with $13$, $S_{12}$, and $S_{13}$ as the generators. Quantum strategies are represented using $SU(3)$ matrices, and the classical strategies are a special case of the quantum strategies. The payoff for each player is determined based on the selected strategies and the corresponding entry in the game table.

## The Analogous Quantum Game: 1 and 2 Quirt States

The structure of the corresponding quantum game involves qutrits, quantum strategies, and entanglement operations. A qutrit is a vector $\mid\psi\rangle=v_1\mid1\rangle+v_2\mid2\rangle+v_3\mid3\rangle\in H_3$ of unit norm, where $H_3$ is the three-dimensional Hilbert space with orthonormal basis vectors $\mid1\rangle$, $\mid2\rangle$ and $\mid3\rangle$. A general 2-qutrit state is a normalized vector in $H_3\otimes H_3$. A maximally entangled two-qutrit state is written in a Schmidt decomposed form, and its entanglement degree is measured by the von Neumann entropy $S_3=-\frac{1}{3}\sum_{i=1}^3\mid u_i\mid ^2\log(\mid u_i\mid^2/3)=\log 3$.

## Quantum Game Strategies

In a 2-3 quantum game, a player's strategy is represented by an $SU(3)$ matrix that acts on their qutrit as a quantum gate. This strategy, denoted as $U(\gamma) \in SU(3)$, depends on eight Euler angles $\gamma = {\alpha_1, \alpha_2, \dots, \alpha_8}$. The explicit expression of $U(\gamma)$ can be written in terms of Gellman matrices ${\lambda_m}$, where $m = 1, 2, \dots, 8$. This expression is well-known.

## 2-3 Quantum Game Procedure

The referee suggests an initial non-entangled two-qutrit
state $\mid \Psi_0 \rangle$ (e.g the analog of the classical two trit state
$\mid \Psi_0 \rangle = \mid 11 \rangle$). Before letting the players apply their quantum strategies, the referee operates on $\mid \Psi_0 \rangle$ with a unitary operator $J(\beta)$ such that $\mid \Psi_1 \rangle = J(\beta) \mid \Psi_0 \rangle$ is entangled (otherwise the game remains classical). Construction of the operator $J(\beta)$ (our central goal) is detailed below. At this stage of the game, the players apply their respective strategies $U_1 \otimes U_2$. Finally, the referee applies the operator $J^{\dagger}(\beta)$ leading to the final state
$\mid \Psi \rangle = J^{\dagger}(\beta) (U_1 \otimes U_2) J(\beta) \mid 11 \rangle = \sum_{i,j=1,3} v_{ij} \mid ij \rangle$,
where $\gamma_k$ is the octet of 8 Euler angles defining the $SU(3)$ matrix $U(\gamma_k)$ (that is the strategy of player $k=1,2$).
The payoff $P_k$ of player $k=1,2$ is given by,
$P_k(\gamma_1, \gamma_2) = \sum_{i,j=1,3} u_k(i,j) \mid v_{ij}(\gamma_1, \gamma_2) \mid^2$,
where $u_k(i,j)$ are the payoffs at entry $(i,j)$ of the classical game table. Like in the classical game, each player chooses a strategy with the goal of maximizing their payoff.

## Pure Strategy Nash Equilibrium (NE)

Because the set of $8$ Euler angles $\gamma$ uniquely determines the player's strategy $U(\gamma) \in SU(3)$, a pure strategy NE in the 2-3 quantum game is a pair of strategies $(\gamma_1^, \gamma_2^)$ (each represents 8 angles), such that
\begin{align}
P_1(\gamma_1, \gamma_2^) &\leq P_1(\gamma_1^, \gamma_2^) \quad \forall \gamma_1, \
P_2(\gamma_1^, \gamma_2) &\leq P_2(\gamma_1^, \gamma_2^) \quad \forall \gamma_2. \label{eq:pure_ne_2_3}
\end{align}
The question of whether a pure strategy NE exists in the 2-2 quantum game, and its relation to the degree of entanglement (controlled by $\beta$), has been discussed in numerous works [9-15]. In brief, if there is NE in the classical game that is not Pareto efficient [16], then there is a critical value $\beta_c$ above which there is no pure strategy NE in the quantum game. As $\beta$ approaches $\beta_c$ from below, the respective payoffs in the quantum game at NE approach the Pareto point of cooperation [11, 15]. This is the main reason why, right from the onset, we stressed the relevance of partially entangled 2-qutrit states where $S_N(\beta) < \log N$.

## Absence of Classical Commensurability

We will now explain why there is no classical commensurability in a 2-3 quantum game, as stated in reference [10]. In classical commensurability, the players get their classical payoffs when they use classical strategies. If we take a classical strategy $\gamma$, it belongs to $S_3$, where $U_\gamma$ is a unitary permutation matrix. From Equation (6), it follows that $J$ should commute with all outer products of classical strategies. If the initial state is $\mid\Psi\rangle = \mid11\rangle$, then the 9 outer products of classical strategies are $1\otimes 2^s \otimes s$, where $s \in {1,2,3}$ and ${1,2,3}^{\otimes 2}={12,13,21,23,31,32}$ (see Equation (3)). Classical commensurability requires that $[J, \otimes_{S\in{1,2,3}^{\otimes 2}} U_S^{\otimes s}] = 0$, which leads to Equation (9): $[J,\otimes_{S\in{1,2,3}}U_S^{\otimes 2}] = 0$. This is only possible if $J$ is a function of $A\otimes A$, where $A$ is a $3\times 3$ matrix satisfying $A\otimes A = 0$ and $A$ is not just a multiple of the identity matrix $I$. However, this is impossible because $S_{12}$ and $S_{13}$ generate an irreducible representation of the permutation group $S_3$, and therefore, by Schur's lemma, $A$ is just a multiple of $I$. These arguments hold for any $N>2$.

## Designing the Entangler $J(\beta)$

The passage discusses the construction of an entanglement operator $J(\beta)$ for $N > 2$. The operator is constructed for $N = 3$ and then extended to any $N$. The entanglement operator $J(\beta)$ is obtained by exponentiating a combination of classical strategies in the $2 \times 2$ game framework specified in Eq.~(1). The operator $J(\beta)$ is defined as $J(\beta) = e^{i\beta/2} Z$ where $Z \equiv S_{12} \otimes S_{12} + S_{13} \otimes S_{13}$. The exponent of $J(\beta)$ is calculated to obtain the entangled $2$-qutrit state. The maximal entanglement is obtained when the absolute values of all three coefficients are equal. The entanglement operator $J(\beta)$ satisfies single parameter completeness. The extension to arbitrary $N$ is done by defining the $N \times N$ matrix representing the permutation $i \leftrightarrow j$ and an unentangled $2$-quNit state $\mid ij \rangle$, where $i, j = 1, 2, \ldots, N$. The entangled state is obtained from $\mid 11 \rangle$ by defining $J(\beta) \mid 11 \rangle = e^{i\beta/2} \sum_{j=2}^N S_{1j} \otimes S_{1j} \mid 11 \rangle = e^{-i\beta/2}\sqrt{N}( e^{iN\beta/2(N-1)} \mid 11 \rangle + \sqrt{\frac{N-1}{N}} \sum_{j=2}^N \mid jj \rangle )$. The maximal entanglement entropy $S_N(\beta)$ is obtained by solving the equality $\mid e^{iN\beta_0/2(N-1)} + \sqrt{\frac{N-1}{N}} e^{-iN\beta_0/2} \mid ^2/N^2 = 1/N$. For $N = 3$ and $4$, maximal entanglement is achieved. For $N > 4$, maximal entanglement is not achieved, and single parameter completeness is not satisfied.

## Extension to Arbitrary $N$

The main result of the study concerns the construction of an entanglement operator $J_\beta$ for 2-qutrit states. The operator is constructed for $\mid 3\rangle$-qutrit states and extended to any $N$. The goal is to obtain an entangled 2-qutrit state with $\beta$ specifying the degree of entanglement that can range from $0$ to $\log 3$. The operator $J_\beta$ is constructed by exponentiating a combination of classical strategies. To obtain the diagonal 2-qutrit states $\mid 2\rangle\mid 2\rangle$ and $\mid 3\rangle\mid 3\rangle$ from $\mid 1\rangle\mid 1\rangle$, $J_\beta$ operates on $\mid 1\rangle\mid 1\rangle$ with $Z\otimes S\otimes S\otimes Z\otimes S\otimes S$, where $Z$ and $S$ are defined as quantum gates. The exponent of $J_\beta$ is calculated to obtain the entangled state. The maximal entanglement is obtained when the absolute values of all three coefficients are equal, which happens at $\beta = 2e^2-1$. The entanglement operator satisfies single-parameter completeness. The von Neumann entropy of the entangled state is displayed as a function of $\beta$ in Figure 1(a), showing that it is a periodic function of $\beta$ with a period of $4\pi/3$ and is symmetric about the midpoint $2\pi/3$. It has two maxima for $\beta=2e^2\pm1$, where it equals $3\log 3$. The entanglement in quantum games is obtained in terms of permutation exponentials that are $SU(3)$ matrices.

## Illustration for $N=5$

A convenient way to build an appropriate unitary $N \times N$ matrix $R$ is to start from a
simple non-singular matrix $A$ and then orthogonalize it
within the Grahm-Schmidt procedure. For example,
$A =
\begin{pmatrix}
1 & 1 & 1 & 1 & 1 \
1 & 1 & 0 & 0 & 0 \
1 & 0 & 1 & 0 & 0 \
1 & 0 & 0 & 1 & 0 \
1 & 0 & 0 & 0 & 1 \
\end{pmatrix}$, $R =
\begin{pmatrix}
1/\sqrt{5} & \sqrt{3}/10 & \sqrt{3}/14 & 3/(2\sqrt{14}) & 1/\sqrt{5} - \sqrt{2}/15 \
\sqrt{3}/10 & 1 & -\sqrt{3}/14 - 3/(2\sqrt{14}) & 2\sqrt{2} & \sqrt{3}/10 - \sqrt{2}/21 \
\sqrt{3}/14 & -\sqrt{3}/14 - 3/(2\sqrt{14}) & 1 & 2\sqrt{2} & \sqrt{3}/14 - 1/\sqrt{14} \
3/(2\sqrt{14}) & 2\sqrt{2} & 2\sqrt{2} & 1 & 2\sqrt{2} - 1/\sqrt{2} \
1/\sqrt{5} - \sqrt{2}/15 & \sqrt{3}/10 - \sqrt{2}/21 & \sqrt{3}/14 - 1/\sqrt{14} & 2\sqrt{2} - 1/\sqrt{2} & 1/\sqrt{5} \
\end{pmatrix}$.
Proceeding with the list of steps prescribed above,
we can easily construct $J(\beta)$ and compute the von
Neumann entropy of the state $\mid \Psi_1 \rangle = J(\beta) \mid 11 \rangle$ upon
which the players apply their strategies according to the
game protocol specified in Eq. (6). The result is given in
Fig. 2. As explained in the figure’s caption, the degree
of entanglement is controlled by a single parameter
and $S_N(\beta)$ is a continuous function of $\beta$ reaching any
value in the interval $\[0, \log N\]$. Thus we have achieved
our goal of constructing an entangler $J(\beta)$ that turns a
non-entangled 2-quNit state into an entangled one given
in a Schmidt decomposed form with single parameter
completeness satisfied.
## Wrap-Up

To summarize, we propose two ways to create an entanglement operator J(β) that transforms a non-entangled 2-quNit state into a partially entangled state with its von Neumann entropy controlled by a single parameter. The first method is straightforward and involves using classical strategies in an exponential equation, as shown in Equation (10) and Figure 1. However, this method only works for N ≤ 4 since the resulting entropy does not reach the maximum value of log N. Thus, we propose a second method that works for any N but is more complex. The resulting entropy as a function of β is depicted in Figure 2.
