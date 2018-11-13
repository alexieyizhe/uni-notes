__MATH 239 |__  Nov 5/7, 2018

# Coloring Graphs

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
The vertex $v$ has $\leq \triangle(G)$ neightbours in $H$, so those neighbours are coloured with at $\leq \triangle(G)$ colours.  Thus, at least 1 colour out of the $\triangle(G) + 1$ colours is available to colour $v$ a colour that is different from its neighbours. QED.

------

Eventually, we'll prove that every _planar graph_ can be properly coloured with $5$ colours.



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

---

__Proof of Euler's Formula for Connected Graphs__
We let $T$ be a spanning tree in $G$ (a connected graph embedded in the plane). Then the embedding of $G$ yields an embedding of $T$: erase the edges of $G$ in $T$.

_Base case:_ Since $T$ has one face, and $|V(G)| - |E(T)| = 1$, we have $|V(T)| - |E(T)| + |Faces(G)| = 1 + 1 = 2$, yielding the formula as required.

For the inductive step, let $e$ be an edge of $G$ not in $T$. Since $T$ is a spanning tree of $G$ and $e$ is not in $T$, then $G - e$ is connected since $T$ is still completely in $G - e$. By the induction, $|V(G - e)| - |E(G - e)| + |Faces(G - e)| = 2$.

We know $|V(G - e)| = |V(G)|$, and $|E(G - e)| = |E(G)| - 1$. How do we show that $|Faces(G - e)| = |Faces(G)| - 1$?

We use another theorem (no proof needed in scope of this class): the ==__Jordan Curve Theorem__ states that every embedding of a cycle $c$ in the plane partitions the plane into the inside face, the outside face, and the cycle itself.==

So, since $e$ is not in the spanning tree $T$ there is a path $P$ in $T$ that connects each end of $e$. Combined with $e$, $P + e$ forms a cycle. This edge and cycle (by the Jordan Curve Theorem) separates two faces, $F_1, F_2$ from each other. Since $F_1 \not= F_2$ for $G$, but they merge into one face for $G - e$, then $|Faces(G - e)| = |Faces(G)| - 1$.

Therefore, $2 = |V(G - e)| - |E(G - e)| + |Faces(G - e)| = |V(G)| - (|E(G) - 1) + (|Faces(G)| - 1) = |V(G)| - |E(G)| + |F(G)|$

_QED_

---

==__Platonic Solids Theorem:__ Let $G$ be a connected $d$-regular graph embedded in the plane so that every face has degree $d^*$. If $d \geq 3, d^* \geq 3$, then $(d, d^*)$ is one of $(3, 3), (3, 4), (3, 5), (4, 3), (5, 3)$.==

![Image result for regular planar graphs](https://faculty.etsu.edu/gardnerr/5025/platonic/platonic1.bmp)

_examples of planar embeddings of regular graphs_

---

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

---



