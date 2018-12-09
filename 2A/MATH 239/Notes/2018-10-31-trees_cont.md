__MATH 239 |__ Oct 31, 2018 :ghost:

# Trees (cont.)

A __spanning tree__ $T$ of a graph $G$ is a subgraph of $G$ that is a tree where $V(T) = V(G)$. It's a subgraph that has the same vertices but possibly less edges.

==__Theorem^1^:__ If $G$ is a connected graph such that every cycle in $G$ has even length, then $G$ is bipartite.==

> The way we approach proving this is by showing if a cycle in $G$ has odd length, it's connecting two vertices in the same set in a bipartition (_i.e. if you jump back and forth between the two sets (moving between vertices), jumping an even number of times gives you two vertices in the same partition, so they are the same colour and thus the graph cannot be bipartite)._)

---

__Proof of Theorem^1^__
Let $T$ be a spanning tree of $G$, and let $(X, Y)$ be a bipartition of $T$. 

Either:

1. For every edge $e$ in $E(G) \setminus E(T)$, $e$ has one end in $X$ and one in $Y$. This means $(X, Y)$ is a bipartition of $G$ and $G$ is bipartite.
2. There is an edge $e$ in $E(G) \setminus E(T)$ where both ends of $e$ are in the same one of $X, Y$. This means the path $P$ in $T$ joining the ends of $e$ has even length. Therefore, the cycle $P + e$ has odd length. If $G$ has only even cycles, this cannot occur, so $G$ must be bipartite by elimination.

---

> In homework, we showed: if $G$ is a bipartite graph with $n$ vertices, then $|E(G)| \leq (\frac{n}{2})^2$.
> A harder version: if $G$ is a graph with no cycle of length 3, then $|E(G)| \leq (\frac{n}{2})^2$ (leads to Turan's Theorem).



Consider a graph with numbers corresponding to edges. Find a spanning tree that minimizes the sum of the numbers on its edges. These are called __minimum weight spanning trees.__ 

There are two main algorithms for _finding these minimum trees:_

| Prim's Algorithm                                             | Kruskal's Algorithm                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Builds up with trees always                                  | Builds up without ever introducing a cycle                   |
| Starting at a vertex, pick one of the cheapest edges having one end in the tree and one end not in the tree | Given the components of what we have, pick a cheapest edge in the graph that has ends in different componenets of our current graph |

---

__Proof of Kruskal's Algorithm__
Let $T$ be a tree constructed by Kruskal's Algorithm, having picked the edges $e_1, e_2, ...,e_k$ in this order. Let $S$ be a least weight spanning tree.

We _claim_ that there is a minimum weight spanning tree $S_1$ containing $e_1$. 

---





