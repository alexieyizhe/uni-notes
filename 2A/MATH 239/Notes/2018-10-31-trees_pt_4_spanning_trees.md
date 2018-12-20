__MATH 239 |__ Oct 31, 2018 :ghost:

# Trees (pt. 4)

A __spanning tree__ $T$ of a graph $G$ is a subgraph of $G$ that is a tree where $V(T) = V(G)$. It's a subgraph that has the same vertices but possibly less edges.

==__Lemma:__ An odd cycle is not bipartite.==

> We show this by defining a vertex set, picking the 'middle' vertex, and going 'outwards' by 1 each time to find two vertices that must be in the same partition.. Once you reach the very 'outside', you find two vertices in the same partition which are adjacent, which contradicts the fact that it is bipartite.

==__Theorem^1^:__ A graph is bipartite _iff_ it has no odd cycles.==

> Proof of this done through using the lemma above and contradiction.

---

__Proof of Theorem^1^__
Let $T$ be a spanning tree of $G$, and let $(X, Y)$ be a bipartition of $T$. 

Either:

1. For every edge $e$ in $E(G) \setminus E(T)$, $e$ has one end in $X$ and one in $Y$. This means $(X, Y)$ is a bipartition of $G$ and $G$ is bipartite.
2. There is an edge $e$ in $E(G) \setminus E(T)$ where both ends of $e$ are in the same one of $X, Y$. This means the path $P$ in $T$ joining the ends of $e$ has even length. Therefore, the cycle $P + e$ has odd length. If $G$ has only even cycles, this cannot occur, so $G$ must be bipartite by elimination.

---

> In homework, we showed: if $G$ is a bipartite graph with $n$ vertices, then $|E(G)| \leq (\frac{n}{2})^2$.
> A harder version: if $G$ is a graph with no cycle of length 3, then $|E(G)| \leq (\frac{n}{2})^2$ (leads to Turan's Theorem).

### Minimum Weight Spanning Trees

Consider a graph with numbers corresponding to edges. Find a spanning tree that minimizes the sum of the numbers on its edges. These are called __minimum weight spanning trees.__, or __minimum spanning trees__.

There are two main algorithms for _finding these minimum trees:_

| Prim's Algorithm                                             | Kruskal's Algorithm                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Builds up with trees always                                  | Builds up without ever introducing a cycle                   |
| Starting at a vertex, pick one of the cheapest edges having one end in the tree and one end not in the tree | Given the components of what we have, pick a cheapest edge in the graph that has ends in different componenets of our current graph |

### Algorithm Steps

__Prim's__

1. Let $v$ be any vertex in $G$. Let $T$ be the tree consisting of just $v$. 
2. Pick an edge having one vertex in $T$ and another not in $T$ that has the smallest weight. Add it to $T$. 
3. Repeat with the tree $T$ growing each time, until you reach a point where there are no more edges not in $T$ , and $T$ is now a minimum spanning tree of $G$.

__Kruskal's__

1. Sort the edges of $G$ into a list from least weight to most weight.
2. Going up the sorted list, pick the edge with the least weight and add it to $T$, as long as the edge does not form a cycle.
3. Repeat with the tree $T$ growing each time, until you have no more edges that are not in $T$ or will form a cycle if added to $T$, and now $T$ is a minimum spanning tree of $G$. 

