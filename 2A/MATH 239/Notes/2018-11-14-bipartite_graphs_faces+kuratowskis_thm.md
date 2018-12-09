__MATH 239 |__ Nov 14, 2018

__Recall Yesterday's Theorem^1^ & Lemma^1^:__

1. Every planar graph has a vertex with degree at most 5.

2. If $G$ is a planar graph with at least 3 vertices, then $|E(G) \leq 3|V(G)| - 6$.

   _this is not an iff!_

3. $K_5$ is not planar. 

__Lemma^1^:__ Let $G​$ be a connected graph embedded in the plane. If $|V(G)| \geq 3​$, then every face has degree at least 3.



Today, we extend this to _bipartite_ graphs.

### Bipartite Graphs

In a bipartite graph, every closed walk has _even_ length. Thus, in a bipartite connected graph, every face will have even degree. If the bipartite connected planar graph has at least 3 vertices, every face degree is an even number at least 3.

Since it's an even number, we amend the Theorem^1^ above to fit:

==__Corollary:__ If $G$ is a bipartite planar graph with $\geq 3$ vertices, then $|E(G)| \leq 2|V(G)| - 4$.==

==__Corollary:__ $K_{3,3}$ is not planar.==



#### Kuratowski's Theorem (1930)

==A graph $G$ is __not__ planar _iff_ it contains a __subdivision__ of either $K_5$ or $K_{3,3}$.==

> __Observations__
>
> 1. If $H$ is a subgraph of a planar graph $G$, then $H$ is planar. 
> 2. _Contrapositive of 1:_ If $H$ is a non-planar subgraph of a graph $G$, then $G$ is non-planar.

Let $G$ be a graph and let $e$ be an edge of $G$. Then, the __subdivision of $G$ in $e$__ is the graph obtained from $G - e$ by adding a new vertex with degree 2 joined to the ends of $e$ in $G$. Conversely, a graph $H$ __is a subdivision__ of a graph $G$ if there is a sequence $G = G_0, G_1, ..., G_k = H$ such that, for $i = 1, ...,k$, $G_i$ is the subdivision of $G_{i - 1}$ in some edge of $G_{i - 1}$.

> Subdivisions should preserve (non-)planarity.