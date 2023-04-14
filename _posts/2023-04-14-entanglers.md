---
layout: post
title: Entanglers in 2-player-N-strategies quantum games
author: Clément
---

## Abstract 

We discuss the construction of entanglers in 2-player-N-strategies quantum games. In these games, each player has a normalized vector in an $N$-dimensional Hilbert space upon which they apply their strategy. A normalized vector in an $N$-dimensional Hilbert space $\mathcal{H}_ \mathcal{N}$ can be represented as: $\vec{x} \in \mathcal{H}_ \mathcal{N}$, $\mid\vec{x}\mid = 1$, where $\mid\cdot\mid$ denotes the norm. The players draw their payoffs from a state $\vert \Psi \rangle = J^{\dagger}U_1 \otimes U_2 J \vert \Psi_0 \rangle \in \mathcal{H}_ N \otimes \mathcal{H}_ N$. Here, $|Ψ_0〉$ and $J$ (both determined by the game’s referee) are respectively an unentangled $2$-qubit (pure) state and a unitary operator such that $|Ψ_1〉 \equiv J|Ψ_0〉 ∈ \mathcal{H}_ N \otimes \mathcal{H}_ N$ is partially entangled. The degree of entanglement of the state is related to the existence of pure strategy Nash equilibrium in the quantum game. The paper suggests an algorithm to construct a special quantum gate that should be useful not only in quantum games but also as a special gate in manipulating quantum information protocols. The gate generates partially entangled states whose degree of entanglement is controlled by a single real parameter, and this property is referred to as single parameter completeness. The paper discusses the relevance of the problem to quantum information and suggests an extension of the algorithm to $N>2$.

## Introduction

The theory of quantum games is a growing area of research that explores the application of quantum mechanics to fields outside of physics, such as economics, finance, and gambling. This is done by "quantizing" classical games, which involves formulating rules and allowing players to use quantum information tools, such as qubits and quantum gates, to make decisions. One example of a quantum game is the 2-2 game, which is based on a classical game that involves two players and two strategies

## The Role of Entanglement in Quantum Games

There is significant research on the quantized version of classical strategic 2-2 games, with most of it based on a protocol specified in [5]. The protocol requires the application of an entanglement (unitary) operator Jβ, where β is a real parameter, on a non-entangled 2-qubit (pure) state. The resulting state is entangled, and its degree of entanglement is measured by its von-Neumann entropy 2Sβ. A desired property of Jβ is that 2Sβ is a continuous function of β that varies between 0 and log2 (maximal entanglement). The degree of entanglement is crucial for the existence of pure strategy Nash equilibrium in the 2-2 quantum game. The problem of controlling the entropy by a single parameter that varies between 0 and log2 is known as single parameter completeness. The design of an entanglement gate Jβ that generates entangled states with a degree of entanglement controlled by a single parameter should be useful in quantum information.
