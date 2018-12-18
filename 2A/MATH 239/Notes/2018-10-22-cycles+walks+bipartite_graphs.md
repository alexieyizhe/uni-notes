__MATH 239 |__ Oct 22, 2018

# Cycles

A __cycle__ can be thought of as either a graph or a walk $(v_0, v_1, ..., v_k)$ in which all vertices and edges are _distinct_ except we require $v_0 = v_k$. 

> For visualization, think of a circular graph where all vertices are connected by one singular circular path.

- $(v_0, v_1, v_0)$ is not a cycle, since all edges must be distinct 

==__Lemma^1^__: If every vertex in a graph $G$ has degree at least 2, then $G$ has a cycle.==

---

__Proof of Lemma^1^__
Let $v_0$ be any starting vertex. We iteratively build a walk by continuing towards a different vertex from one of the edges of the previous vertex. More formally:

if we have $v_0, v_1, ..., v_i$ distinct, we let $v_i v_{i+1}$ be an edge different from $v_{i - 1} v_i$ and now get $v_0, v_1, ..., v_i, v_{i+1}$. 

If  $v_{i + 1}$ is not one of $v_0, ..., v_i$, we continue.
If $v_{i + 1} = v_j, 0 \leq j \leq i$, that is, that $v_{i + 1}$ is one of the vertices already in the path, then we stop and note that $(v_0, v_1, ..., v_i, v_{i + 1})$ is a cycle.

---

The above also proves the following: ==If $G$ has at most one vertex with degree 1 and all others have degree $\geq 2$, then $G$ has a cycle.== 

> We can start with $v_0$ being the vertex of degree 1 to show the above.

A **Hamilton cycle** is a cycle that spans every vertex of the graph.


# Cycles & Walks in Bipartite Graphs

==Every cycle in a bipartite graph has **even** length.==

If $G$ is a bipartite graph with bipartition $(X, Y)$ and $W$ is a walk with origin in $X$, then:

1. $W$ has odd length _iff_ its terminus is in $Y$
2. $W$ has even length _iff_ its terminus is in $X$

A path is bipartite.

The empty graph is bipartite.




# Connectedness

A graph $G$ is **connected** if, for every pair of vertices $u, v$ in the graph, there is a path between $u$ and $v$.

==__Theorem:__ If for any vertex $v$ in a graph $G$, there is a path from any other vertex to $v$, then $G$ is a connected graph.==

### Components

A __component__ of a graph $G$ is a _connected_ subgraph $H$ of $G$ such that if  $H \not\subseteq K \subseteq G$, then $K$ is not connected.

> This means that every subgraph that properly contains $H$ is not connected.

If $H$ is a subgraph of a bipartite graph, then $H$ is bipartite. 

==If every component of $G$ is bipartite, then $G$ is bipartite.== 



Given a set of vertices $X$ in a graph $G$, the __cut__ induced by $X$ is the set of edges in $G$ that have exactly one end in $X$.

==__Theorem:__ A graph $G$ is not connected _iff_ there exists a proper non-empty subset $X$ of $V(G)$ such that the cut induced by $X$ is empty.==

![image-20181217151156828](/Users/alexieyizhe/Google Drive/University/2A/MATH 239/Notes/2018-10-22-cycles+walks+bipartite_graphs.assets/image-20181217151156828-5077516.png)

