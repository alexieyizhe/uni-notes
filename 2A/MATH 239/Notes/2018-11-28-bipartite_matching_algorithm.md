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

---

__Proof of above fact__
If $y \in Y$, then $y$ is not a leaf of the forest. Thus, $y$ is is incident with a matching edge. The other end of this edge is in $X$

Therefore, every vertex in $X$ is either $M$-unsaturated (in $X_o $)or is $M$-adjacent to a vertex in $Y$. 

If $a \in A\setminus X$, $a$ is $M$-saturated ($a$ not in $X_o $). By the previous paragraph, $a$ is $M$-adjacent to a vertex in $B \setminus Y$. 

To show that $Y \cup (A \setminus X)$ is a cover, we need to show that there is no edge from a vertex in $X$ to a vertex in $B \setminus Y$.
If $x \in X$, then any edge $xy \in M$ has $y \in Y$ by rule 2 in the algorithm.
If $x \in X$, and $xy \not\in M$,  then Rule 2a guarantees $y \in Y$.
Since all edges with one end in $X$ has the other end in $Y$ and none in $B \setminus Y$, we have shown that there is no edge from a vertex in $X$ to a vertex in $B \setminus Y$. Thus, $Y \cup (A \setminus X)$ is a cover.

Therefore, $|M| = |Y \cup (A \setminus X)|​$, and having the same sizes further means that $Y \cup (A \setminus X)​$ is a minimum cover, and $M​$ is a maximum matching. by theorems proven in previous lectures.

This also proves __König's Theorem__ from the previous lecture.

---

### Hall's Theorem

There is a theorem that applies König's Theorem to check if a graph $G$ with a bipartition $A, B$ can have a perfect matching, by essentially seeing if every subset of $A$ has enough unique vertices connected to its vertices for a perfect matching (since edges in a matching cannot connect to the same vertex).

==__Hall's Theorem:__ Let $G$ be a bipartite graph with bipartition $(A, B)$. $G$ has a matching that saturates _all_ of $A$ _iff_ for every subset $X \subset A$, $|N(X)| \geq |X|$ where $N(X) = \{y \in B \ | \ \text{there is an } x\in X, xy \in E(G)\}$ (the set of edges with one end in $X$ and one in $Y​$).== 

==__Corollary:__ A bipartite graph $G$ with bipartition $(A, B)$ has a perfect matching _iff_ $|A| = |B|$ and, for every $Y \subset B, |N(Y)| \geq |Y|$==

==__Corollary:__ A bipartite graph $G$ with bipartition $(A, B)$ has a perfect matching _iff_ for every $X \subset A, |N(x)| \geq |X|$, and for every $Y \subset B, |N(Y)| \geq |Y|$ .==

> This is saying that we can have a perfect matching only if the bipartition separates the vertices equally _and_ for every subset of $A$, there are enough vertices connected to them in the other bipartitioned set (all these vertices form the neighbour set) to have a unique edge between each vertex in the subset and one in the other bipartitioned set.

==__Theorem:__ Let $k$ be a positive integer and $G$ be a $k$-regular bipartite graph. Then, $G$ has a perfect matching.==

