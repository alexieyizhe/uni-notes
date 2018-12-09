__MATH 239 |__ Nov 28, 2018

# Bipartite Matching Algorithm

Let $G$ be a bipartite graph, with bipartition $(A, B)$ of $V(G)$. Let $M$ be a matching in $G$. Our algorithm outputs either a matching $N$ such that $|N| > |M|$ or a cover $C$ such that $|C| = |M|$.

The algorithm is as follows:

1. __Initialize__
   Let $X_o$ be the set of $M$-unsaturated vertices in $A$. Let $X = X_o, Y = \emptyset$.
2. __Iteration__
   1. Add any neighbour $v$ of a vertex in $X$ not currently in $Y$; add $v$ to $X$.
   2. Add a vertex $x$ adjacent by a edge of $M$ to a vertex in $Y$; add $x$ to $X$.

3. **Termination**
   Since the number of vertices in this cannot exceed $|V(G)|$, this algorithm eventually terminates. At termination, there are two possibilities:
   1. There is a leaf of the forest in $Y$. _This implies there is an $M$-augmenting path, which we proved last lecture leads to a bigger matching_
   2. Every leaf is in $X$. _By ==taking the vertices in $Y \cup A \setminus X $== , this will give us the cover required._

![Untitled](/Users/alexieyizhe/Google Drive/University/2A/MATH 239/Notes/2018-11-28.assets/Untitled.png)

==If at termination, every leaf of the forest is in $X$ (case 2), then $Y \cup A \setminus X$ is a cover such that $|M| = |Y \cup (A \setminus X)|$.==

---

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

---

==__Hall's Theorem:__ Let $G$ be a bipartite graph with bipartition $(A, B)$. $G$ has a matching that saturates _all_ of $A$ _iff_ for every $x \subset A$, $|N(x)| \geq |X|$ where $N(x) = \{y \in B \ | \ \text{there is an } x\in X, xy \in E(G)\}$==

==__Corollary:__ A bipartite graph $G$ with bipartition $(A, B)$ has a perfect matching _iff_ $|A| = |B|$ and, for every $Y \subset B, |N(Y)| \geq |Y|$==

==__Corollary:__ A bipartite graph $G$ with bipartition $(A, B)$ has a perfect matching _iff_ for every $X \subset A, |N(x)| \geq |X|$, and for every $Y \subset B, |N(Y)| \geq |Y|$.==

==__Theorem:__ Let $k$ be a positive integer and $G$ be a $k$-regular bipartite graph. Then, $G$ has a perfect matching.==

m