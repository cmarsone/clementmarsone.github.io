---
layout: post
title: Markov decision processs
author: Clément
---

## Discounted rewards

He "discounted sum of future rexards" using discount factrro gamma
reaward +gamm reward at 1step....

Define:
$V_A$: expected discounted futur rewards starting in state $A$
$V_B=\cdots$

### Markov system with rewards

Set of states $\{ S_ 1, \cdots, S_ N \}$

A transition probability matrix

$$\[
\begin{pmatrix}
P_{11} & P_{12} & \cdots & P_{1n} \\
P_{21} & P_{22} & \cdots & P_{2n} \\
\vdots & \vdots & \ddots & \vdots \\
P_{n1} & P_{n2} & \cdots & P_{nn}
\end{pmatrix}
\]$$

$P_{ij} = \text{Prob } ( \text{next } (S_i) | \text{ this }) = S_j$

Each state has reward $\{ r_1, r_2, r_N \}$

Discount factor $0 < \gamma < 1$
$V^* (S_ i)=$ expected discounted sum of future rewards starting in $S_ i$
$= r_ i + \gamma$ ( expected future rewards starting from you next state)
$= r_ i + \gamma (P_{i1} V^* (S_1) + P_ {iN} V^* (S_N))$
$=R + \gamma P V^* (S) $

#### Value iteration

$$V^1 (S_i) = r_i$$
$$V^2 (S_i) = r_i +\gamma\sum\limits_{j=1}^ N p_{ij}= V^1 (s_j)$$
...
$$V^{k+1} (S_i) = r_i +\gamma\sum\limits_{j=1}^ N p_{ij}= V^k (s_j)$$
