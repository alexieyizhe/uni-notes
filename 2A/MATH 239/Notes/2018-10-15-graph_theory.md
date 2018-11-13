__MATH 239 |__ Oct 15, 2018

# Intro to Graph Theory

A __graph__ is an ordered pair $(V, E)$ of finite sets $V$ and $E$ such that $E$ (an __edge__) is a set of subsets of $V$ (a __vertex__) of size 2.

------

__Ex.__ $(\{1, 2, 3, 4, 5, 6\}, \{\{1, 2\}, \{1, 3\}, \{2, 3\}, \{2, 4\}, \{3, 4\}, \{4, 5\}, \{4, 6\}, \{5, 6\}, \{5, 1\}, \{6, 1\}, \{6, 2\}\})$ is a graph.

------

- The __degree__ of a vertex $v$ is the number of edges containing $v$; it is denoted $deg(v)$

- If $\{u, v\}$ is an edge, then $u$ and $v$ are __incident__ with $\{u, v\}$ and $u$ and $v$ are __adjacent__/__neighbours__.

> Essentially, an edge is an ordered pair of two vertices that are in $V$. We can _visualize_ this by representing a vertex with a dot and an edge with a line connecting two dots (vertices). There can be multiple visualizations of the same graph.



### When are two graphs the same?

The graphs $(V, E)$ and $(W, F)$ are __isomorphic__ if there is a bijection $\Phi:V \rightarrow W$ such that for every distinct $u ,v \in V, \{u, v\} \in E \Longleftrightarrow \{\Phi (u), \Phi (v)\} \in F$.  

> Every pair in $F$ must correspond to a pair with the same vertices in $E$.



### Common Graphs

- The __empty graph__ is denoted $(V, \emptyset)$
  - It has as many vertices as you wish, but _no edges_
- The __complete graph__ is a graph in which the set of edges $E$ is _all_ the 2-element subsets of $V$
  - For a complete graph with $n$ vertices, it has ${n \choose 2}$ edges
- A __path__ $P_n$ is a linear graph with the following form:
  - $P_n = (\{0, 1, ..., n\}, \{\{i - 1, i\} \ |\ i = 1 , ... , n\})$
- A __cycle__ $C_n$ is a cyclic graph with the following form:
  - $C_n = (\{0, 1, ..., n - 1\}, \{\{i - 1, i\} \ |\ i = 1 , ... , n - 1\})$ (modulo $n$) 
-  An __n-th dimensional cube__ $Q_n$ has as vertices all binary strings of length $n$ and two vertices are adjacent precisely when their strings differ in exactly one coordinate. 
  - $Q_0$:  $\bullet$
  - $Q_1$:  $\bullet -\bullet$
  - $Q_2$:  square lol
  - $Q_3$:  just imagine a cube lmao
  - In $Q_n$, every vertex has $deg(n)$
    - This is a result of being able to find a new adjacent vertex by switching exactly one value of the binary string from $0$ to $1$ or vice versa 

