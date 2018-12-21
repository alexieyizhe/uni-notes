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
  - A complete graph with $n$ vertices is denoted $K_n$
- A __path__ $P_n$ is a linear graph with the following form:
  - $P_n = (\{0, 1, ..., n\}, \{\{i - 1, i\} \ |\ i = 1 , ... , n\})$
- A __cycle__ $C_n$ is a cyclic graph with the following form:
  - $C_n = (\{0, 1, ..., n - 1\}, \{\{i - 1, i\} \ |\ i = 1 , ... , n - 1\})$ (modulo $n$) 
- An __n-th dimensional cube__ $Q_n$ has as vertices all binary strings of length $n$ and two vertices are adjacent precisely when their strings differ in exactly one coordinate. 
  - $Q_0$:  $\bullet$
  - $Q_1$:  $\bullet -\bullet$
  - $Q_2$:  square lol
  - $Q_3$:  just imagine a cube lmao
  - In $Q_n$, every vertex has $deg(n)$
    - This is a result of being able to find a new adjacent vertex by switching exactly one value of the binary string from $0$ to $1$ or vice versa 



__MATH 239 |__ Oct 17, 2018

# Degrees

### Handshake Lemma

==Let $(V, E)$ be a graph. Then, $\sum\limits_{v \in V} deg(v) = 2|E|$==

> The edge that connects two vertices contributes +1 to the degree of one of its vertices, and +1 to the other, so each edge contributes +2 to the overall degrees of all vertices in the graph.

------

__Proof of the Handshake Lemma__

Let $X$ be the set $\{ (v, e) \ | \ v \in V, e \in E, v \in e \}X$. Then, $|X| = \sum\limits_{v \in V} deg(v)$, since each vertex $v \in V$ has  $deg(v)$ number of edges and thus contributes $deg(v)$ elements into the set $X$.  

Similarly, we can count it by considering the fact that each edge has two vertices that belong to that edge, so $|X| = \sum\limits_{e \in E} 2 = 2|E|$.

By counting the set $X$ in two different ways, we've shown that $\sum\limits_{v \in V} deg(v) = 2|E|$.

------

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

------

**Proof of Theorem.**
By induction on the number of repetitions (a repetition is a vertex occurring more than once in the sequence):

If there are no repetitions, then the walk is a path, and we are done.

Otherwise, there is a repeated vertex $w$. Find the first and last occurrence of $w$ and removing the first occurrence of $w$ up until but not including the second occurrence of $w$ results in a walk with no repetition of $w$. If we inductively apply this to every repetition, we end up with a walk with no repetitions, resulting in a $uv$-path.  

------



__MATH 239 |__ Oct 22, 2018

# Cycles

A __cycle__ can be thought of as either a graph or a walk $(v_0, v_1, ..., v_k)$ in which all vertices and edges are _distinct_ except we require $v_0 = v_k$. 

> For visualization, think of a circular graph where all vertices are connected by one singular circular path.

- $(v_0, v_1, v_0)$ is not a cycle, since all edges must be distinct 

==__Lemma^1^__: If every vertex in a graph $G$ has degree at least 2, then $G$ has a cycle.==

------

__Proof of Lemma^1^__
Let $v_0$ be any starting vertex. We iteratively build a walk by continuing towards a different vertex from one of the edges of the previous vertex. More formally:

if we have $v_0, v_1, ..., v_i$ distinct, we let $v_i v_{i+1}$ be an edge different from $v_{i - 1} v_i$ and now get $v_0, v_1, ..., v_i, v_{i+1}$. 

If  $v_{i + 1}$ is not one of $v_0, ..., v_i$, we continue.
If $v_{i + 1} = v_j, 0 \leq j \leq i$, that is, that $v_{i + 1}$ is one of the vertices already in the path, then we stop and note that $(v_0, v_1, ..., v_i, v_{i + 1})$ is a cycle.

------

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

![image-20181217151156828](/Users/alexieyizhe/Google%20Drive/University/2A/MATH%20239/Notes/2018-10-22-cycles+walks+bipartite_graphs.assets/image-20181217151156828-5077516.png)



__MATH 239 |__ Oct 24, 2018

# Trees

A connected graph with no cycles is a __tree.__

> Paths are trees, since they contain no cycles. They are also bipartite.

If we delete an edge from a tree, we end up with a graph with two __tree components.__

------

__Side Lemma!__
==Let $G$ be a connected graph and let $e$ be an edge of $G$. Then the graph $G-e$ obtained by deleting $e$ has _at most two components._==

If you remove an edge that connects two nodes with another path between them, then the number of components stay at 1. If you remove an edge that connects two nodes _without_ another path between them, you've just split the graph up into two components.

Formally, let $u, v$ be two vertices of $G$ incident with $e$. For every vertex $w$ of $G$, let $P_w$ be a $wu$-path in $G$. Let $U = \{w \ | \ \forall \ P_w, v \not\in P_w \}$ (vertices where all their paths to $u$ do not contain $v$) and $V = \{w \ | \ \exists \ P_w, v \not\in P_w \}$ (vertices where there exists a path between said vertex to $u$ without going through $v$). Since $G$ is connected, $V(G) = U \cup V$.

Any two vertices of $U$ are in the same component of $G - e$ with $u$, and any two vertices of $V$ are in the same component of $G - e$ with $v$.

This shows that $G - e$ has at most two components. There are two components _iff_ $U$ and $V$ are in different components of $G - e$.

------

### Bridges

If $G$ is a connected graph, a __bridge__ of $G$ is an edge $e$ of $G$ such that $G - e$ is not connected.

==__Theorem^1^:__ An edge $e$ of a connected graph $G$ is not a bridge of $G$ _iff_ there is a cycle in $G$ containing $e$.==

------

__Proof of Theorem^1^__
_Backwards:_ Let $u, v$ be the ends of $e$. Let $C$ be a cycle in $G$ containing $e$. Then $C - e$ is a $uv$-path in $G - e$, showing $u, v$ are in the same component of $G - e$. Our earlier fonsiderations show us that $G - e$ is connected.

_Forwards:_ If $e$ is not a bridge of $G$, then $G - e$ is connected. In particular, there exists a $uv$-path $P$ in $G - e$ $P + e$ is a cycle. 

_QED._

------

==__Corollary^1^__: Every edge of a tree is a bridge. The only tree with no bridge is $\bullet$, a tree of 1 element.==

==__Theorem^2^__: Let $T$ be a tree with $n \geq 1$ vertices. Then, $|E(T)| = n - 1$.==

------

__Proof of Theorem^2^ by Induction__
_Base Case: $n = 1$_
In this case, $|E(T)| =  0$.

For the induction step, $n \geq 2$, and $T$ has at least 1 edge $e$. Because $e$ is a bridge, $T - e$ has two components $T_1, T_2$ are both trees (they are connected anf have no cycles).

We know:
$|V(T_1)| + |V(T_2)| = |V(T)|$, so $ |V(T_1)| < |V(T)|$ and $|V(T_2)| < |V(T)|$, and $|E(T_1)| + |E(T_2)| = |E(T)| - 1$.

The induction implies $|E(T_1)| = |V(T_1)| - 1$ and $|E(T_2)| = |V(T_2)| - 1$.
$|E(T)| - 1 = |E(T_1)| + |E(T_2)| = (|V(T_1)| - 1) + (|V(T_2)| - 1)$
$\ \ \ \ \  \ \ \ \ \ \ \  \ \ \ \ \ \ = |V(T)| - 2$, so
$|E(T)| = |V(T)| - 1$, as required.

------

==__Corollary:__ IF $u$ and $v$ are vertices in a tree $T$, then there is a unique $uv$-path in $T$.==



__MATH 239 |__ Oct 26, 2018

# Trees: the sequel

==__Lemma^2^__: Let $u, v$ be vertices in a graph $G$ such that there are two different $u, v$ paths in $G$. Then, $G$ has a cycle.==

------

__Proof of Lemma^2^__
Let $(u, v_1, v_2, ... , v_{k-1}, v)$ and $(u ,w_1, w_2, ..., w_{l - 1}, v)$ be two different $uv$-paths in $G$. Let $i$ be the least index such that $v_i \neq w_i$. Let $e$ be the edge $w_{i - 1} \rightarrow w_i$.

We will prove that in $G - e$, there is a path between $w_{i - 1} \rightarrow w_i$. Observe that $e$ is not an edge of $(u, v_1, v_2, ... , v_{k-1}, v)$. We also know that $v_{i -1}$ is not one of the vertices $v_i, v_{i + 1}, ..., v_{k - 1}, v$. Therefore, none of the edges $v_{i - 1} \rightarrow v_i, v_i \rightarrow v_{i + 1}, ..., v_{k - 1} \rightarrow v$ is e. 

For the proof, we concatenate the paths $(w_i, w_{i + 1}, ..., w_{l - 1}, v)$ and $(v, v_{k - 1}, ..., v_i, v_{i - 1})$. This is a $w_i w_{i-1}$-walk in $G - e$!

------

A graph with no cycles is a __forest__. Each component of a forest is a tree.

For a tree T, $\sum\limits_{v \in V(T)} deg(V) = 2(|V(T)| - 1) = 2|V(T)| - 2$.

==__Fact:__ Every tree has a vertex $v$ with $deg(v) \lt 2$.==

> The graph $\bullet$ is the only tree with vertex of $deg \ 0$.

==If $|V(T)| \geq 2$, then $T$ has at least two vertices with $deg = 1$.== These vertices with $deg = 1$ are called __leaves.__

> Useful: Suppose $T$ is a tree with at least two vertices. The ends of a longest path in $T$ have degree 1 in $T$.
>
> Useful: Suppose $G$ is a graph in which every vertex has degree $\geq 2$. Then $G$ has a cycle.



__MATH 239 |__ Oct 29, 2018

# Trees (cont. cont.)

Last Time:

- Every tree with $\geq 2$ vertices has at least two vertices of degree 1
- Every edge of a tree is a bridge.

------

Let $T$ be a tree and $u$ a vertex of $T$ with degree 1.
Let $e$ be the edge of $T$ incident with $u$.
What is $T - e$?

Since the edge $e$ is a bridge between the rest of $T$ and $u$, the tree is split into 2 components: a smaller tree and the isolated vertex $u$. We can think of the smaller tree as $T - u$, a tree with one fewer vertex and one fewer edge than $T$.

------

> A vertex with degree 1 in a tree is often called a __leaf__.

==__Theorem^1^:__ Every tree is bipartite.==

------

__Proof of Theorem^1^ (by Induction)__
_Base Case:_ Let $k$ be the number of vertices. If $k = 1$, the tree is the graph $\bullet$, which is bipartite since it has no edges.

_Inductive Hypothesis:_ Suppose this statement is true for trees with $k$ vertices.

_Inductive Conclusion:_ We prove this statement is true for trees with $k + 1$ vertices.

Let $T$ be a tree with $k + 1$ vertices, and let $u$ be a vertex of $T$ with degree 1 (we know such a vertex exists for all trees with $\geq 2$ vertices, from Oct 26). 
Since $T - u$ has $k$ vertices, by the $IH$, we know that $T - u$ has a partition of its vertex set into $X$ and $Y$ such that every edge of $T - u$ has one end in $X$ and one end in $Y$. 
Let $v$ be the other end of the edge of $T$ that is incident with $u$ (the vertex that $u$ connects to in $T - u$). Then, $v \in X$ or $v \in Y$, and adding $u$ to the set that does not contain $v$ yields a bipartition of $T$. 

This proves that a tree $T$ with $k + 1$ vertices is bipartite, as required.

------

==__Theorem^2^:__ Let $G$ be a graph. If any 2 of the following 3 statements hold, then $G$ is a tree:==

1. ==$G$ is connected.==
2. ==$|E(G)| = |V(G)| - 1$==
3. ==$G$ has no cycles.==

------

__Proof of Theorem^2^__

- _1. and 3._ make up the definition of a tree.

- _2. and 3._
  Suppose $G$ has components $C_1, ..., C_r$. Each $C_i$ is a connected graph with no cycles, and so is a tree. Therefore, $|E(C_i)| = |V(C_i)| - 1$, and $|E(G)| = \sum\limits_{i = 1}^r |E(C_i) = \sum\limits^r_{i = 1} (|V(G)| - 1) = \sum\limits^r_{i = 1} |V(C_i)| - r = |V(G) |- r$. Since $2.$ says $|E(G)| = |V(G)| - 1$, then $r = 1$. Thus, $G$ is connected and we have proven $1.$, and since $1.$ and $3.$ is true, then by the definition of a tree, $G$ is a tree.

- _1. and 2._
  Our claim is that $G$ is connected $\rightarrow$ $G$ contains a subgraph of $T$ that is a tree and $|V(T)| = |V(G)|$.
  We induct on the number $n$ of cycles in $G$. 

  If $n = 0$, then $G$ is a tree. 

  If $n > 0$, then let $C$ be a cycle in $G$ and let $e \in E(C)$. Then $G - e$ is connected since $e$ is not a bridge of $G$, but has fewer cycles than $G$ has. By continuing to remove edges that are in a cycle of $G$ but keeping $G$ connected, this induction yields a subgraph $T$ of $G - e$ that is a tree with $V(T) = V(G - e)$. Then $T$ is a subgraph of $G$ that is a tree with $V(T) = V(G)$.

  By this claim, $G$ has a subgraph of $T$ that is a tree and $V(T) = V(G)$.
  Thus, $|E(T)| = |V(T)| - 1 = |V(G)| - 1 = |E(G)|$, thus $|E(T)|= |E(G)|$ and $G = T$, so $G$ is a tree!

------



__MATH 239 |__ Oct 31, 2018 :ghost:

# Trees (pt. 4)

A __spanning tree__ $T$ of a graph $G$ is a subgraph of $G$ that is a tree where $V(T) = V(G)$. It's a subgraph that has the same vertices but possibly less edges.

==__Lemma:__ An odd cycle is not bipartite.==

> We show this by defining a vertex set, picking the 'middle' vertex, and going 'outwards' by 1 each time to find two vertices that must be in the same partition.. Once you reach the very 'outside', you find two vertices in the same partition which are adjacent, which contradicts the fact that it is bipartite.

==__Theorem^1^:__ A graph is bipartite _iff_ it has no odd cycles.==

> Proof of this done through using the lemma above and contradiction.

------

__Proof of Theorem^1^__
Let $T$ be a spanning tree of $G$, and let $(X, Y)$ be a bipartition of $T$. 

Either:

1. For every edge $e$ in $E(G) \setminus E(T)$, $e$ has one end in $X$ and one in $Y$. This means $(X, Y)$ is a bipartition of $G$ and $G$ is bipartite.
2. There is an edge $e$ in $E(G) \setminus E(T)$ where both ends of $e$ are in the same one of $X, Y$. This means the path $P$ in $T$ joining the ends of $e$ has even length. Therefore, the cycle $P + e$ has odd length. If $G$ has only even cycles, this cannot occur, so $G$ must be bipartite by elimination.

------

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



__MATH 239 |__  Nov 2, 2018

# Trees (pt. 5)

==__Theorem^2^:__ Kruskal's (or Prim's) Algorithm always outputs a minimum weight spanning tree.==

> We start with a forest whose components are all the vertices of a graph $G$ as isolated vertices. 
>
> For each iteration: among all edges of $G$ having ends in different components of the current forest, add one that has least weight.

------

__Proof of Kruskal's__
Let $T$ be a tree output by Kruskal's Algorithm. Let $e_1, e_2,...,e_{n-1}$ be the edges of $T$ in the order they are selected.

We claim that for each $i = 0, 1, ..., n-1$, there is a minimum weight spanning tree $S_i$ containing all of $e_1, e_2, ..., e_i$. ($S_0$ is any minimum weight spanning tree).

_Induction Step:_ Assume there is a minimum weight spanning tree $S_i$ containing all of $e_1, ..., e_i$ (every min. weight spanning tree has $n-1$ edges, we just don't know what the other $n - 1 - i$ edges are in this case). 

We prove there is a minimum weight spanning tree containing all of $e_1, ..., e_i$, AND $e_{i+1}$ _(note that_ $T = S_{n-1}$, _so $T$ is a min. weight spanning tree)._If $e_{i+1} \in E(S_i)$, then we're done in this iteration and we set $S_{i +1} = S_i$.

If $e_{i+1}$ is not in $S_i$, then we notice that $T - e_{i+1}$ has two components, say $T_1, T_2$. The ends of $e_{i+1}$ are, say, $u_1, u_2$, with $u_1 \in V(T_1)$ and $u_2 \in V(T_2)$.  Since they are vertices of $T$, of $G$ and of $S_i$, there is a $u_1u_2$-path $P$ in $S_i$. Then $P$ is a path in $G$ starting at a vertex $u_1$ in $V(T_1)$ and ending at a vertex $u_2$ in $V(T_2)$.

There is an edge $vw$ of $P$ having one end $v \in V(T)1$ and $w \in V(T_2)$. Since $e_{i+1}$ is the only edge of $T$ with one end in $T_1$ and the other end in $T_2$, and $e_{i+1} \not\in E(S)$ and $vw \in E(S)$, then we know $e_{i+1} \not= vw$. At the moment we chose $e_{i+1}$, $u_1$ and $u_2$ were in different components of the forest at that time (using edges $e_1, ..., e_i$). Every component of that forest is contained in either $T_1$ or $T_2$, therefore __$vw$ was available in the selection to be added to that forest__, so $weight(vw) \geq weight(e_{i+1})$. 

Look at $S_i + e_{i+1}$: it has the cycle $P + e_{i + 1}$. Deleting any edge $f$ in $P$ produces a new spanning tree of $G$ with weight $weight(S_i) - weight(f) + weight(e_{i+1}) \geq weight(S_i)$, no matter what edge $f$ we delete, since $S_i$ was a minimum weight spanning tree. So, $weight(e_{i+1}) \geq weight(f)$, and if we pick $vw = f$, then $weight(e_{i+1}) \geq weight(f)$ and  $weight(f = vw) \geq weight(e_{i+1})$, so $weight(e_{i+1}) = weight(vw = f)$. So, $S_{i+1} = (S_i - vw) + e_{i+1}$ is a minimum weight spanning tree, since we're replacing $vw$ with $e_{i+1}$ while keeping the same weight and $S_{i+1}$ includes all edges $e_1, ..., e_i, e_{i+1}$. 

By induction, we can show $T = S_{n - 1}$ is a minimum weight spanning tree. 

------

__Proof of Prim's__
Let $T_1, ..., T_n$ be trees where $T_{k + 1}$ is the tree created by adding the edge $e_k$ to $T_k$.

We will prove by induction that there exists a MST containing $T_i$ as a subgraph, which means that $T_i$ must be the MST, otherwise that MST is not a MST.

_Base case:_ For $i = 1$, $T_1$ is a subgraph of every MST, so this is true.

_Inductive hypothesis:_ Assume that there exists a MST containing $T_i$ as a subgraph.

 _Inductive step:_ Prove that there is a MST containing $T_{i + 1}$ as a subgraph.
Let $T^*$ be a MST that contains $T_i$ as a subgraph, which is assumed by the inductive hypothesis. 

If $T^*$ also contains $e_i$, then it contains $T_{i + 1}$ and we are done.

If $T^*$ does not contain $e_i$, then $T^* + e_i$ contains a single cycle $C$, since $T^*$ is a spanning tree. $C - e_i$ is a path between vertices $u, v$, where $u \in T_i$ and $v \not\in T_i$, since $e_i$ is not in $T_i$. So, there is an edge $e'$ in $C - e_i$ that has one end in $V(T_i)$ and the other not (that is, that $e'$ is not in $T_i$). By a previous theorem, $T' =T^* + e_i -e' $ is also a spanning tree. 

If the weight of $e_i$, the edge added to $T_i$ to get $T_{i + 1}$, is larger than the weight of $e'$, then $w(T') \lt w(T^*)$, which contradicts the fact that $T^*$ is a MST. As well, the weight of $e_i$ cannot be larger than the weight of $e'$ because in that case we would've picked $e'$ instead of $e_i$ when using Prim's Algorithm. So, the weight of $e_i$ is the same as the weight of $e'$, which means that $w(T') = w(T^*)$, which means $T'$ is a MST that contains all the edges in $T_{i + 1}$, which menas that $T_{i + 1}$ is a subgraph of a MST $T'$. 

So, by induction, for each $n$, there is a MST that contains $T_n$, which means $T_n$ must be that MST, and so the algorithm always produces a MST.      ==$QED.$==

------



__MATH 239 |__  Nov 5/7, 2018

# Planar Graphs

A __planar graph__ is a graph that can be represented in a single plane without two edges of the graph ever intersecting.

- An $n$-cycle is planar: we can represent it by a regular $n$-gon (pentagon, hexagon, etc)
- Every tree is planar: we can prove this using induction

### Faces

__Faces__ are enclosed regions defined by the edges and vertices of a planar graph. Each enclosed area is considered a single face, and an additional face is defined to be the __outer face__, the region outside the graph.

![Image result for faces in graphs](https://caagt.ugent.be/CaGe/Images/graph-faces.gif)

> You can distinguish different faces based on if you cross an edge or not (if you do, its a different face).

- A tree has 1 face (no region is enclosed since there are no cycles)

==__Euler's Formula For Connected Graphs:__ If $G$ is a _connected graph embedded in the plane_, then $|V(G)| - |E(G)| + |Faces(G)| = 2$==

==__Euler's Formula (General Version):__ For all graphs embedded in the plane, then $|V(G)| - |E(G)| + |Faces(G)| = 1 + components(G)$==

------

__Proof of Euler's Formula for Connected Graphs__
We let $T$ be a spanning tree in $G$ (a connected graph embedded in the plane). Then the embedding of $G$ yields an embedding of $T$: erase the edges of $G$ in $T$.

_Base case:_ Since $T$ has one face, and $|V(T)| - |E(T)| = 1$, we have $|V(T)| - |E(T)| + |Faces(G)| = 1 + 1 = 2$, yielding the formula as required.

For the inductive step, let $e$ be an edge of $G$ not in $T$. Since $T$ is a spanning tree of $G$ and $e$ is not in $T$, then $G - e$ is connected since $T$ is still completely in $G - e$. By the induction, we need to prove that $|V(G - e)| - |E(G - e)| + |Faces(G - e)| = 2$.

We know $|V(G - e)| = |V(G)|$, and $|E(G - e)| = |E(G)| - 1$. How do we show that $|Faces(G - e)| = |Faces(G)| - 1$?

We use another theorem (no proof needed in scope of this class): the ==__Jordan Curve Theorem__ states that every embedding of a cycle $c$ in the plane partitions the plane into the inside face, the outside face, and the cycle itself.==

So, since $e$ is not in the spanning tree $T$ there is a path $P$ in $T$ that connects each end of $e$. Combined with $e$, $P + e$ forms a cycle. This edge and cycle (by the Jordan Curve Theorem) separates two faces, $F_1, F_2$ from each other. Since $F_1 \not= F_2$ for $G$, but they merge into one face for $G - e$, then $|Faces(G - e)| = |Faces(G)| - 1$.

Therefore, $2 = |V(G - e)| - |E(G - e)| + |Faces(G - e)| = |V(G)| - (|E(G) - 1) + (|Faces(G)| - 1) = |V(G)| - |E(G)| + |F(G)|$

We apply this inductively for every edge $e$ in $G$ not in $T$, to get the result for $G$ of Euler's Theorem.

==$QED.$== 

------

### Platonic Solids

A **platonic solid** is just a shape where there exists a planar embedding where all vertices have the same degree $d \geq 3$ and all faces have the same degree $d^* \geq 3$.

==__Platonic Solids Theorem:__ Let $G$ be a connected $d$-regular graph embedded in the plane so that every face has degree $d^*$. If $d \geq 3, d^* \geq 3$, then $(d, d^*)$ is one of $(3, 3), (3, 4), (3, 5), (4, 3), (5, 3)$.==

There are exactly 5 platonic graphs.

![image-20181217173732528](/Users/alexieyizhe/Google%20Drive/University/2A/MATH%20239/Notes/2018-11-05-7-planar_graphs.assets/image-20181217173732528-5086252.png)

------

__Proof of Platonic Solids Theorem__

We utilize three theorems:

1. __Handshake Lemma:__ $d|V(G)| = 2|E(G)|$
2. __Faceshake Lemma:__ $d^*|Faces(G)| = 2|E(G)|$
3. __Euler's Formula:__ $|V(G)| - |E(G)| + |F(G)| = 2$

Substituting __HL__ and __FL__ into __EF__ gives us $\frac{2|E(G)|}{d} - |E(G)| + \frac{2|E(G)|}{d^*} = 2$
Multiplying by $-1 * \frac{dd^*}{|E(G)|}$ gives us: $-2d^* + dd^* - 2d = -\frac{2dd^*}{|E(G)|}$
Adding $4$ and factoring the $LHS$  gives us: $(d - 2)(d^*-2) = 4 - \frac{2dd^*}{|E(G)|}$

Since $d, d^* \geq 3$, then the $LHS \geq 0$. $\frac{2dd^*}{|E(G)} \gt 0, $ so $RHS \lt 4$.

So, $(d - 2, d^* - 2)$ is one of $(1, 1), (1, 2), (1, 3), (2, 1), (3, 1)$ since those are the only positive pairs that multiply to give an integer $\lt 4$.

$QED$

------



__MATH 239 |__ Nov 9, 2018

# Faces (cont.)

The __degree__ of a face is the length of its boundary walk. 

![Image result for faces in graphs](https://caagt.ugent.be/CaGe/Images/graph-faces.gif)

> You might have to traverse an edge twice if it's a leaf edge that extends into the face - this will indeed add 2 to the degree of the face.

==__The Faceshake Lemma:__ Let $F$ be the set of faces of a planar embedding of a graph $G$. For each face $f \in F$, denote the degree of $f$ as $d^*(f)$. Then, $\sum\limits_{f \in F} d^*(f) = 2 |E(G)|$.==

> This is because every edge has two sides, and each side will be traversed exactly once. Sometimes this will be in the traversal of a single face, sometimes two faces, sometimes more, but each side is always part of exactly one traversal.

==__Lemma:__ If $G$ contains a cycle, then in a planar embedding of $G$, the boundary of every face contains a cycle.==



__MATH 239 |__ Nov 12, 2018

# Faces (cont.)

==__Today's Theorem:__==

1. Every planar graph has a vertex with degree at most 5.

2. If $G$ is a planar graph with at least 3 vertices, then $|E(G)|  \leq 3|V(G)| - 6$.

   _this is not an iff!_

3. $K_5$ is not planar.

==__Lemma^1^:__ Let $G$ be a connected graph embedded in the plane. If $|V(G)| \geq 3$, then every face has degree at least 3.==

------

__Proof of Theorem^1^__
If $|V(G)| \leq 2$, then every vertex $v$ has $deg(v) \leq$ 2.

Thus, we may assume $|V(G)| \geq 3$. Then Theorem^2^ implies $|E(G)| \leq 3|V(G)| - 6$. The smallest degree is $\leq$ the average degree = $\frac{\sum\limits{v \in V(G)}deg(v)}{|V(G)|}$ = $\frac{2|E(G)|}{|V(G)|} \leq \frac{6|V(G)| - 12}{|V(G)|} = 6 - \frac{12}{|V(G)|} \leq 5$, so the smallest degree $\leq 5$.        $QED$

------

__Proof of Theorem^2^__
Suppose first $G$ is connected. By Lemma^1^, every face has degree $\geq 3$ and the Faceshake Lemma says that $2|E(G)| = \sum\limits_{all faces F} deg(F)$. Putting these last two sentences together, $2|E(G)| = \sum\limits_{all faces F} deg(F) \geq 3|F(G)|$. 

Euler's formula says $|V(G)| - |E(G)| + |F(G)| = 2$. Since rearranging the inequality above gives us $|F(G)| \leq \frac{2}{3}|E(G)|$, we see that $2 = |V(G)| - |E(G)| + |F(G)| \leq |V(G)| - |E(G)| + \frac{2}{3}|E(G)|$.

So, $2 \leq |V(G)| - \frac{1}{3} |E(G)|$, and we rearrange to get $|E(G)| \leq 3|V(G)| - 6$.

To complete the proof, suppose $G$ is not connected. Then $G$ has $\alpha$ components that are $\bullet$ (single vertices), $\beta$ components that are $\bullet -\bullet$, and $\gamma$ components with $\geq 3$ vertices. 

$|E(G)| = \sum\limits_{all \ components \ C} |E(C)|$ = $E(\alpha) + E(\beta) + \sum\limits_{all \ components \geq 3 \ vertices} |E(C)|$ = $0 + \beta + \sum\limits_{all \ components \geq 3 \ vertices} |E(C)|$.

$|V(G)| = \sum\limits_{all \ components \ C} |V(C)|$ = $\alpha + 2\beta + \sum\limits_{all \ components \geq 3 \ vertices} |V(C)|$.

_proof incomplete for non-connected graphs, but is not as important to know compare to connectedness_

------

__Proof of Theorem^3^__
We proceed by proof by contradiction. If $K_5$ were planar, then Theorem^2^ tells us that $|E(K_5)| \leq 3 |V(K_5)| - 6$. Substituting in known values, $10 = {5 \choose 2} \leq 3 * 5 - 6 = 9$, and since $10 \not\leq 9$, this is a contradiction and thus $K_5$ is not planar. 

------

__Proof of Lemma^1^__
Let $F$ be the face and let $uv$ be an edge in the boundary walk of $F$. Because $G$ is connected and has at least 3 vertices, at least one of $u, v$ has degree at least 2 in $G$; say $u$ has degree $\geq 2$.

This implies that, starting the boundary walk of $F$ at $v$ and proceeding first to $u$, we must traverse a new edge $ux$ next (since $u$ has degree $\geq 2$). Since $x \not= v$, we still have to return to $v$, so there is at least one more step in the boundary walk of $F$. This means that $deg(F) \geq 3$.          ==$QED$==

------



__MATH 239 |__ Nov 14, 2018

__Recall Yesterday's Theorem^1^ & Lemma^1^:__

1. Every planar graph has a vertex with degree at most 5.

2. If $G$ is a planar graph with at least 3 vertices, then $|E(G) \leq 3|V(G)| - 6$.

   _this is not an iff!_

3. $K_5$ is not planar. 

__Lemma^1^:__ Let $G$ be a connected graph embedded in the plane. If $|V(G)| \geq 3$, then every face has degree at least 3.



Today, we extend this to _bipartite_ graphs.

### Bipartite Graphs

In a bipartite graph, every closed walk has _even_ length. Thus, in a bipartite connected graph, every face will have even degree. If the bipartite connected planar graph has at least 3 vertices, every face degree is an even number at least 3.

Since it's an even number, we amend the Theorem^1^ above to fit:

==__Corollary:__ If $G$ is a bipartite planar graph with $\geq 3$ vertices, then $|E(G)| \leq 2|V(G)| - 4$.==

==__Corollary:__ $K_{3,3}$ is not planar.==



# Non-Planar Graphs

#### Kuratowski's Theorem (1930)

==A graph $G$ is __not__ planar _iff_ it contains a __subdivision__ of either $K_5$ or $K_{3,3}$.==

> __Observations__
>
> 1. If $H$ is a subgraph of a planar graph $G$, then $H$ is planar. 
> 2. _Contrapositive of 1:_ If $H$ is a non-planar subgraph of a graph $G$, then $G$ is non-planar.

Let $G$ be a graph and let $e$ be an edge of $G$. Then, the __subdivision of $G$ in $e$__ is the graph obtained from $G - e$ by adding a new vertex with degree 2 joined to the ends of $e$ in $G$. Conversely, a graph $H$ __is a subdivision__ of a graph $G$ if there is a sequence $G = G_0, G_1, ..., G_k = H$ such that, for $i = 1, ...,k$, $G_i$ is the subdivision of $G_{i - 1}$ in some edge of $G_{i - 1}$.

> Subdivisions should preserve (non-)planarity.



__MATH 239 |__ Nov 16, 2018

# Graph Colouring

We colour the vertices such that adjacent vertices get different colours.

__Some Facts:__ 

1. A graph can be coloured with 2 colours _iff_ it is bipartite.
2. A graph can be coloured with 1 colour _iff_ it has no edges.
3. An odd cycle needs 3 colours.
4. A complete graph with $n$ vertices ($K_n$) needs $n$ colours.

==__Theorem^2^:__ Let $G$ be a graph and let $\triangle(G)$ denote the largest degree of any vertex in $G$. Then $G$ can be coloured with $\triangle(G) + 1$ colours.==

------

__Proof of Theorem^2^__
We proceed by induction on $|V(G)|$.

_Base Case:_ $|V(G)| = 1$
In this case, $\triangle(G) = 0$ and $G$ can indeed be coloured with 1 colour.

If $|V(G)| > 1$, let $v$ be any vertex of $G$ and let $H = G - v$. Then $\triangle(H) \leq \triangle(G)$ and by induction, $H$ can be coloured with $\triangle(H) + 1$ colours.
The vertex $v$ has $\leq \triangle(G)$ neighbours in $H$, so those neighbours are coloured with at $\leq \triangle(G)$ colours.  Thus, at least 1 colour out of the $\triangle(G) + 1$ colours is available to colour $v$ a colour that is different from its neighbours. QED.

------

Eventually, we'll prove that every _planar graph_ can be properly coloured with 6 colours, and then 5..

### Four Colour Theorem

==Every planar graph has a 4-colouring.== 

First, we'll prove the __six colour theorem:__ every planar graph has a 6-colouring.

A __colouring__ of a graph with colour set $C$ is a function $f: V(G) \rightarrow C$ such that, if $uv \in E(G), f(u) \not= f(v)$.

The __chromatic number__ of a graph $G$ is denoted $\chi(G)$ and is the size of the _smallest_ set $C$ such that there is a colouring of $G$ with colour set $C$. It has the properties:

- $1 \leq \chi(G) \leq |V(G)|$
- $\chi(G) \leq 1 + \text{largest degree of a vertex in }G$
- $\chi(K_n) = |V(K_n)|$ (an $n$-regular graph requires $n$ colours to colour it)
- A graph $G$ **has a $k$-colouring** (or is __$k$-colourable__) if $k \geq \chi(G)$

------

__Proof of the 6 Colour Theorem__
From the theorem we covered on 11/12, we know that every planar graph has a vertex with degree $\leq 5$.

If $G$ has $n$ vertices, then we set $v_n$ to be any vertex of $G$ that has degree $\leq 5$ in $G$. Now move to $G - v_n$. This is a planar graph, so it has a vertex $v_{n - 1}$ of degree $\leq 5$ (and so degree $\leq 6$ in $G$). In general, $G - \{v_n, v_{n - 1}, ..., v_{i + 1}\}$ is a planar graph, so it has a vertex $v_i$ of degree $\leq 5$ in $G - \{v_n, v_{n - 1}, ..., v_{i + 1}\}$ and so degree $\leq 5 + (n - i)$ in $G$.

In this way, we have ordered the vertices as $v_1, v_2, ..., v_{n - 1}, v_n$. Colour in this order, using 6 colours: when we colour $v_i$, the degree of $v_i$ in $G - \{v_{i+1}, ..., v_n\}$ is $\leq 5$, so $v_i$ has $\leq 5$ neighbours among the coloured vertices $v_1, v_2, ..., v_i$. Therefore, there is at least one colour of the 6 available that is used to colour any neighbour of $v_{i + 1}$ in $v_1, ..., v_i$ This colour can be used to colour $v_{i + 1}$.    ==$QED.$==

__Revised Version__
We proceed by induction on $|V(G)|$ (the number of vertices on our planar graph).

If $|V(G)| \leq6 $, then $G$ has a 6-colouring.

Suppose the result holds for all planar graph with $k$ vertices. Let $G$ be a planar graph with $k + 1$ vertices. Then, $G$ has a vertex $v$ with degree $\leq 5$ in $G$. Let $G' = G - v$. Then $G'$ is a planar graph on $k$ vertices and so has a 6-colouring $f:V(G - v) \rightarrow C$, |C| = 6. Since $deg(v) \leq 5$, the number of colours appearing in the colouring $f$ on the neighbours of $v$ is $\leq 5$. Thus, there is a colour in $C$ different from these colours on $v$'s neighbours that we use on $v$ to extend $f$ to a 6-colouring of $ G$.            ==$QED.$==

------

__Proof of the 5 Colour Theorem__
If $G$ has a vertex $v$ with degree $\leq 4$, proceed exactly as in the proof of the 6 Colour Theorem, turning any occurrence of $6$ into $5$. 

Otherwise, $G$ has a vertex $x$ with degree 5, and the vertices connected to that vertex must not all be adjacent to each other, since that would create a subdivision of $K_5$ and would make $G$ not planar (a contradiction).

An ==__edge contraction__== $G /e$ of an edge $e$ in a graph $G$ is the graph obtained by reducing the length of $e$ to 0 and allowing the two vertices connected by $e$ to become one vertex, and any vertex that was adjacent to either one or both of the vertices connected to $e$ are connected with the new single vertex.

So, there are two vertices $u,v$ not adjacent to each other. We edge contract both of these vertices' edges with the vertex with degree 5, so that we have one less vertex. By the inductive hypothesis, we have a graph that is 5-colourable. However, instead of colouring both $u, v$ different colours, colour them the same colour. 

Now, 2 of the 5 vertices connected to $x$ have the same colour, and so there are 4 colours in the vertices connected to $x$. Colour $x$ the remaining colour out of the 5 we're using to colour the graph, and now we have a 5-colouring of $G$. 



__MATH 239 |__ Nov 19, 2018

# Planar Duals

![Image result for planar duals](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Noniso_dual_graphs.svg/290px-Noniso_dual_graphs.svg.png)

We give each **face** of a graph $G$ a **vertex** to form a graph $G'$. This allows you to go from colouring vertices to colouring faces, allowing us to use the 4-colouring theorem for colouring faces (like regions on a map, etc).

We also draw **edges** connecting the vertices in $G'$ such that $G'$ has an **edge** whenever two faces of $G$ are separated from each other by an edge in $G$, and a **loop** whenever the same face appears on both sides of an edge.

This is a planar graph. It is the planar __dual__ of $G$, meaning that $G' $ is a dual of $G$ and $G$ is a dual of $G'$ (symmetric).

==__Theorem^1^:__ Let $G$ be a connected graph embedded in the plane and let $T$ be a spanning tree of $G$. Let $G^*$ be the dual of $G$. Then $(V(G^*), \ E(G^*) \setminus E^*(T) )$ is a spanning tree of $G^*$.==

------

__Proof of Theorem^1^__
We showed that the number of edges is the right number for a spanning tree of $G^*$. We will show that these edges do not include the edges of a cycle in $G^*$.

So, let $C^*$ be a cycle of $G^*$ using the edges not in $T$. Let $e^*$ be any edge of $C^*$ and let $e$ be the edge of $G$ dual to $e^*$. Let $u,v$ be the vertices of $G$ incident with $e$. Notice that $u,v$ are on different sides of $C^*$.

There is a $uv$-path $P \text{ in } T$. There is, starting from $u$, a first vertex $w$ of $P$ on the side of $C^*$ containing $v$. The predecessor $x$ of $w$ in $p$ is on the same side of $C^*$ as $u$, so $xw$ crosses $C^*$. But then either $xw$ is not in $T$ or the edge of $C^*$ crosses in $T$. These are both contradictions, so $C^*$ does not exist.    ==$QED.$==



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

------



### König's Theorem

==If $G$ is a bipartite graph, then the size of a maximum matching and the size of a minimum cover are equal.==

_proof in next lecture_



__MATH 239 |__ Nov 28, 2018

# Bipartite Matching Algorithm

### $XY$-Construction

We can use alternating paths to define sets $X, Y$ and show that they have certain properties.

Let $A, B$ be a bipartition of $G$, and let $M$ be a matching of $G$. Let $X_0$ be the set of $M$-unsaturated vertices in $A$, and $Z$ be the set of vertices joined to a vertex in $X_0$ by an alternating path. We define sets $X, Y$ to be:

- $X$ is the set of vertices in $A$ connected to any vertex in $X_0$ by an alternating path.
- $Y$ is the set of vertices in $B$ connected to any vertex in $X_0$ by an alternating path.

Note that $X \cup Y = Z$. Also, any alternating path $P(v)$ from a vertex $v$ to any vertex in $X_0$ has:

- **Even** length if $v \in A$ (if it's connecting $X_0$ to $X$).
- __Odd__ length if $v \in B$ (if it's connecting $X_0$ to $Y$).

That observation of length tells us that since the first edge of the alternating path beginning in $X_0$ does not belong to the matching $M$ (since all vertices in $X_0$ are $M$-unsaturated):

- If $v \in X$, it is connected by a path of even length and the edge connecting to $v$ will be a part of $M$.
- If $v \in Y$, it is connected by a path of odd length and the edge connecting to $v$ will not be in $M$.

This is known as **$XY$-construction** and will be useful in the algorithm for a maximum matching.

### Algorithm Steps

Let $G$ be a bipartite graph, with bipartition $(A, B)$ of $V(G)$. Let $M$ be a matching in $G$. Our algorithm outputs either a matching $N$ such that $|N| > |M|$ or a cover $C$ such that $|C| = |M|$.

1. Let $\hat X$ be the set of all $M$-unsaturated vertices in $A$. Let $\hat Y$ be $\emptyset$. Let $pr(v)$ be the parent vertex to a vertex $v$ and set it to undefined for all $v \in V(G)$.
2. For every vertex $v \in B \setminus \hat Y$ that connects to a vertex $u$ in $\hat X$, add $v$ to $\hat Y$ and set $pr(v) = u$.
   - If no vertex satisfies the conditions in Step 2, ==$C = \hat Y \cup (A \setminus \hat X)$ is a **minimum cover**== with $|C| = |M|$, which also makes ==$M$ a **maximum matching**== by König's Theorem. __Algorithm terminates.__
   - If a vertex $v$ that is $M$-unsaturated is added to $\hat Y$, use $pr()$ values to trace an augmenting path from $v$ to an $M$-unsautrated element of $\hat X$. Use this path to create ==a larger **matching** $M'$==. __Algorithm repeats with $M'$ as the initial matching.__
3. For every vertex $v \in A \setminus \hat X$ that connects to a vertex $u \in \hat Y$ **through an edge in $M$**, add $v$ to $\hat X$ and set $pr(v) = u$.  __Repeat from Step 2.__

![image-20181218111316166](/Users/alexieyizhe/Google%20Drive/University/2A/MATH%20239/Notes/2018-11-28-bipartite_matching_algorithm.assets/image-20181218111316166-5149596.png)

![image-20181218111450358](/Users/alexieyizhe/Google%20Drive/University/2A/MATH%20239/Notes/2018-11-28-bipartite_matching_algorithm.assets/image-20181218111450358-5149690.png)

------

__Proof of above fact__
If $y \in Y$, then $y$ is not a leaf of the forest. Thus, $y$ is is incident with a matching edge. The other end of this edge is in $X$

Therefore, every vertex in $X$ is either $M$-unsaturated (in $X_o $)or is $M$-adjacent to a vertex in $Y$. 

If $a \in A\setminus X$, $a$ is $M$-saturated ($a$ not in $X_o $). By the previous paragraph, $a$ is $M$-adjacent to a vertex in $B \setminus Y$. 

To show that $Y \cup (A \setminus X)$ is a cover, we need to show that there is no edge from a vertex in $X$ to a vertex in $B \setminus Y$.
If $x \in X$, then any edge $xy \in M$ has $y \in Y$ by rule 2 in the algorithm.
If $x \in X$, and $xy \not\in M$,  then Rule 2a guarantees $y \in Y$.
Since all edges with one end in $X$ has the other end in $Y$ and none in $B \setminus Y$, we have shown that there is no edge from a vertex in $X$ to a vertex in $B \setminus Y$. Thus, $Y \cup (A \setminus X)$ is a cover.

Therefore, $|M| = |Y \cup (A \setminus X)|$, and having the same sizes further means that $Y \cup (A \setminus X)$ is a minimum cover, and $M$ is a maximum matching. by theorems proven in previous lectures.

This also proves __König's Theorem__ from the previous lecture.

------

### Hall's Theorem

There is a theorem that applies König's Theorem to check if a graph $G$ with a bipartition $A, B$ can have a perfect matching, by essentially seeing if every subset of $A$ has enough unique vertices connected to its vertices for a perfect matching (since edges in a matching cannot connect to the same vertex).

==__Hall's Theorem:__ Let $G$ be a bipartite graph with bipartition $(A, B)$. $G$ has a matching that saturates _all_ of $A$ _iff_ for every subset $X \subset A$, $|N(X)| \geq |X|$ where $N(X) = \{y \in B \ | \ \text{there is an } x\in X, xy \in E(G)\}$ (the set of edges with one end in $X$ and one in $Y$).== 

==__Corollary:__ A bipartite graph $G$ with bipartition $(A, B)$ has a perfect matching _iff_ $|A| = |B|$ and, for every $Y \subset B, |N(Y)| \geq |Y|$==

==__Corollary:__ A bipartite graph $G$ with bipartition $(A, B)$ has a perfect matching _iff_ for every $X \subset A, |N(x)| \geq |X|$, and for every $Y \subset B, |N(Y)| \geq |Y|$ .==

> This is saying that we can have a perfect matching only if the bipartition separates the vertices equally _and_ for every subset of $A$, there are enough vertices connected to them in the other bipartitioned set (all these vertices form the neighbour set) to have a unique edge between each vertex in the subset and one in the other bipartitioned set.

==__Theorem:__ Let $k$ be a positive integer and $G$ be a $k$-regular bipartite graph. Then, $G$ has a perfect matching.==

