__MATH 239 |__ Nov 21, 2018

# Matchings in Graphs

A __matching__ in a graph $G$ is a set $M$ of edges of $G$ such that every vertex of $G$ is incident with _at most_ one edge in $M$. An alternative way of expressing a matching is a set of edges such that no two edges in the set have the same end vertex. 

> You can have vertices not being incident with any edges in the set $M$, but you cannot have vertices incident with more than one edge in the set $M$.

==__Lemma__: If $M$ is a matching in a graph $G$, then $|M| \leq \frac{1}{2}|V(G)|$.==

### Saturated Vertices, Alternating Paths, & Perfect Matchings

Let $M$ be a matching in a graph $G$. 

A vertex $v$ of a graph $G$ is __$M$-saturated__ if it's incident w/ any edge of $M$. It's __$M$-unsaturated__ if it isn't incident w/ any.
A path $P$ in $G$ is __$M$-alternating__ if the edges in $P$ alternate belonging to $M$ and not to $M$.
A path $P$ in $G$ is __$M$-augmenting__ if $P$ is $M$-alternating and the end vertices of $P$ are $M$-unsaturated (it is a path starting and ending with edges not in $M$, and alternating in the middle).

A matching $M$ is __perfect__ if _every_ vertex is $M$-saturated; that is, that every vertex in $G$ is incident with exactly one edge of $M$.

==__Theorem^1^:__ If $M$ has an augmenting path, then it is not a maximum matching.==

==__Theorem^2^:__ If $M$ is a matching in a graph $G$ and $P$ is an $M$-augmenting path in $G$, then $M \ (+) \ P = (M \setminus E(P)) \cup (E(P) \setminus M)$ is a matching with one more edge than $M$ has.==

> Basically, Theorem^1^ tells us that there are fewer edges of $P$ in $M$ than there are not in $M$. If we define $M'$ to be all the edges in $P$ not in $M$ and all the edges of $M$ that are not in $P$, then $M'$ is a larger matching since there is one more edge of $P$ not in $M$ than in $M$.



__MATH 239 |__ Nov 23, 2018

# Covers

*From last time:* A __matching__ is a set $M$ of edges in a graph $G$ such that every *vertex* of $G$ is incident with _at most_ one *edge* in $M$.

A __cover__ is a set $C$ of vertices in a graph $G$ such that every *edge* of $G$ is incident with _at least_ one *vertex* in $C$.

> These two terms are essentially the same, just describing relationships between vertices and edges.

### Common Graphs

| Graph Type            | Largest Matching                           | Smallest Cover                           |
| --------------------- | ------------------------------------------ | ---------------------------------------- |
| $K_n$                 | $\left \lfloor{\frac{n}{2}}\right \rfloor$ | $n - 1$                                  |
| $K_{a, b}$            | $min\{a, b\}$                              | $min\{a, b\}$                            |
| $Q_n$                 | $2^{n - 1}$                                | $2^{n - 1}$                              |
| Cycle with length $n$ | $\left \lfloor{\frac{n}{2}}\right \rfloor$ | $\left \lceil{\frac{n}{2}}\right \rceil$ |
| Path with length $n$  | $\left \lceil{\frac{n}{2}}\right \rceil$   | $\left \lceil{\frac{n}{2}}\right \rceil$ |

==__Lemma:__ If $M$ and $C$ are a matching and a cover in a graph $G$, respectively, then $|M| \leq |C|$ .==

> This is because for each edge connecting vertices $u, v$, at least one of $u, v$ is in $C$, so $|C| \geq \frac{1}{2}|V(G)|$. It follows from the first lemma that $|M| \leq \frac{1}{2}|V(G)| \leq |C|$.  

==__Side Lemma:__ If $M$ and $C$ are a matching and a cover in a graph $G$, respectively, and $|M| = |C|$, then $M$ is a maximum matching in $G$ and $C$ is a minimum cover in $G$.==

==__Theorem^1^:__ If $M$ is a matching in a graph $G$ that is not a maximum matching, then there is an $M$-augmenting path in $G$.==

------

__Proof of Theorem^1^__
Let $N$ be a matching such that $|N| \gt |M| $. Let $H$ be the subgraph of $G$ with edge set $M + N = (M \setminus N) \cup (N \setminus M)$ (_a subgraph consisting of edges that are in exactly one of $M$ or $N$_.

All vertices in $H$ have degree 1 or 2, since every edge connected to a vertex is either shared between $M$ and $N$ (1 edge) or different (2 edges). Every component of $H$ is either a path or a cycle (since connected & all vertices have degree 1 or 2). Since $|N| \gt |M|$, some component of $H$ has more edges in $N$. Since cycles must alternate between $M$-edges and $N$-edges (so no two from each set are adjacent to each other), they have even length and must have the same number of edges in $N$ as $M$. 

So, if the component has more edges in $N$, it can only be a _path_. It must alternate between edges in $M$ and edges in $N$, since otherwise that would contradict the definition of a matching. Since there are more edges in $N$ in this component than $M$, it must have odd length, and so the path must start and end with an edge in $N$ (thus not in $M$) and alternate in between, making the path an $M$-augmenting path in $G$.

==$QED.$==

---



### König's Theorem

==If $G$ is a bipartite graph, then the size of a maximum matching and the size of a minimum cover are equal.==

_proof in next lecture_

