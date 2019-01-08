---
layout: post
title: Hierarchical graphs
---

<!--
What about other types of graph. Hyper, ...!?
 -->

We say things like "the sun is hot because of the energy released by the fusion of hydrogen atoms". We could construct a graph of concepts and relations, linking `the sun` to `hot` via some `is` relation, and ...

But `the sun`, `hydrogen atoms`, `energy`, ... are not basis concepts (and neither are `because`, `released`, `fusion`, ... basis relations), they are extremely complicated ideas built up by experience and reasoning.

`the sun` could be represented as a graph of 'more basic' concepts, "the bright thing that moves across the sky". And again, these concepts and relations could be decomposed.

INSERT pretty pic

***

We will need a graph equiped with an enbedding fn and a function for composition.

$$
\begin{align}
V &\subseteq \mathbb X^m \\
E &\subseteq \mathbb X^n \\
G &:= \mathcal P(V)\times \mathcal P(E) \\
\\
f: G &\rightarrow V \tag{embed graph in node}\\
\circ: G \times G &\rightarrow G \tag{compose two graphs} \\
\end{align}
$$
the ability to take $\mathcal G \rightarrow v$


What about $e,v \in \mathbb C^d$. Where edges and nodes share the same space!? But are composed via $e^T \cdot v$!?
https://arxiv.org/abs/1702.06879

## Isomorphism and a metric

We can define a metric on the space $G$.

$$
d: G \times G \rightarrow \mathbb R^+ \\
d(g_i, g_j) = \parallel f(g_i) - f(g_i)\parallel \\
symmetry, reflexivity, transitivity...
$$

Thus graph isomorphism can be computed approximately Convolutional
$$
\begin{align}
bool &= g_i \equiv g_j \tag{graph isomorphism}\\
&\approx d(g_i, g_j) \le \epsilon \tag{approximation} \\
\end{align}
$$

## Construction

Any $G$ must be constructed using only the basis nodes $v \in V: ?$. What about the edges!?

And feasible graphs must be constructible via bases. (this is the part we seem to have missed)

## Graph embedding

So how 'should' it be done? Message passing through the edges?
Maybe this needs to be softened?
To a graph compression!?

## Graph composition

Does this need to be a learned function?

If a node already exists (but nodes are in $\mathbb X^m$ so we need a metric... if X is the reals then!??).

- What if we have the same node in a graph twice?! Is that allowable?


# Uses

## Indexing a dictionary of graphs

Given these ops you could imagine a dictionary of graphs.

$$
\{v_i: g_i \mid\;\text{where}\; v_i = f(g_i) \} \\
$$

This dictionary can be indexed by a graph.

##
