__MATH 239 |__ Oct 17, 2018

#Degrees

### Handshake Lemma

==Let $(V, E)$ be a graph. Then, $\sum\limits_{v \in V} deg(v) = 2|E|$==

> The edge that connects two vertices contributes +1 to the degree of one of its vertices, and +1 to the other, so each edge contributes +2 to the overall degrees of all vertices in the graph.

---

__Proof of the Handshake Lemma__

Let $X$ be the set $\{ (v, e) \ | \ v \in V, e \in E, v \in e \}X$. Then, $|X| = \sum\limits_{v \in V} deg(v)$, since each vertex $v \in V$ has  $deg(v)$ number of edges and thus contributes $deg(v)$ elements into the set $X$.  

Similarly, we can count it by considering the fact that each edge has two vertices that belong to that edge, so $|X| = \sum\limits_{e \in E} 2 = 2|E|$.

By counting the set $X$ in two different ways, we've shown that $\sum\limits_{v \in V} deg(v) = 2|E|$.

---

==__Corollary:__ Every graph has an even number of vertices with odd degree.==

> The proof for the corollary is simply that $2|E|$ is even and for the sum of the degrees to add up to an even number, the amount of vertices with odd degrees must be even. 



Recall that $Q_n$ has vertices that are represented by binary strings of length $n$. Two strings are adjacent if they differ in exactly one place. Each vertex has degree $n$; there are $2^n$ vertices,  so $2|E| = \sum deg(v) = n 2^n$ and $|E| = n 2^{n - 1}$.

Recall that $K_n$ has $n$ vertices and $n \choose 2$ edges. Every vertex has degree $n-1$, so $n (n-1) = 2 {n \choose 2}$.



### Regular Graphs

A graph in which every vertex has degree $k$ is called a $k$-**regular** graph. 

A complete graph is an example of a regular graph, but not every regular graph is a complete graph.



# Bipartite Graphs

A graph $(V, E)$ is __bipartite__ if $V$ partitions into two sets $X$ and $Y$ such that every edge has one vertex in $X$ and one vertex in $Y$.  

> We say that $X$ and $Y$ are partitions of $V$ iff $V = X \cup Y$ and $X \cap Y = \emptyset$. 

### Complete Bipartite Graphs

For positive integers $p, q$ the complete bipartite graph $K_{p, q}$ has $|X| = p, |Y| = q$, and all possible edges with one end in $X$ and one end in $Y$.

- $|E(K_{x,y})| = xy$
  - This is because every edge has exactly one end in $X$ and one end in $Y$
- A __bipartition__ of a graph $(V, E)$ is a partition $X, Y$ of $V$ such that every edge has one end in $X$ and one end in $Y$

==__Lemma:__ If $(V, E)$ is a bipartite graph with bipartition $X, Y$, then $\sum\limits_{v \in X} deg(v) = |E| = \sum\limits_{v \in Y} deg (v)$.==

> The proof for this lemma follows from the first bullet point. Note that a __bipartition__ is a partition $X, Y$ that separates the vertices into two disjoint sets.

### Bipartite $Q_n$ Graphs 

$Q_n$ is _bipartite_ for every $n \geq 0$.

For $Q_n$, a bipartition is defined by $X$ being the set of strings with an even number of $1$s, and $Y$ being the strings with an odd number of $1$s. Since adjacent strings differ in exactly one bitm the nbumber of $1$s differ by onem so one in $X$, one in $Y$.  

 