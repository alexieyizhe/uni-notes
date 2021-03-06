__MATH 239 |__ Oct 19, 2018

# Subgraphs

A **subgraph** of a graph $G$ is a graph $H$ such that $V(H) \subseteq V(G)$ and $E(H) \subseteq E(G)$.

> Essentially, pick some edges and vertices of $G$ that can form a _valid_ graph to get $H$.

A __path__ is defined as $(\{a_0, a_1, ..., a_n\}, \{\{a_0, a_1\}, \{a_1, a_2\}, ..., \{a_{n-1}, a_n\},\})$.

- The __length of a path__ is the number of edges in the path
- A conventional shorthand for a path is $(a, b, c, d, e)$, where $a, b, c, d, e$ are the vertices 

A graph $G$ is __connected__ if for any two vertices $u, v$ in $G$, there is a path in $G$ having $u,v$ as ends (shorthand as a $uv$-path).

A __walk__ in a graph $G$ is a sequence of vertices $(a_0, a_1, ..., a_k)$ such that, for each $i = 1, ..., k, \{a_{i - 1}, a_i\} \in E(G)$. 

A path is then, in this context, a walk where all the vertices are *distinct*. 

==**Theorem**: If a graph $G$ has a $uv$-walk, then $G$ has a $uv$-path.== 

---

**Proof of Theorem.**
By induction on the number of repetitions (a repetition is a vertex occurring more than once in the sequence):

If there are no repetitions, then the walk is a path, and we are done.

Otherwise, there is a repeated vertex $w$. Find the first and last occurrence of $w$ and removing the first occurrence of $w$ up until but not including the second occurrence of $w$ results in a walk with no repetition of $w$. If we inductively apply this to every repetition, we end up with a walk with no repetitions, resulting in a $uv$-path.  

---

