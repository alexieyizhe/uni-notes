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

---

__Proof of the 6 Colour Theorem__
From the theorem we covered on 11/12, we know that every planar graph has a vertex with degree $\leq 5$.

If $G$ has $n$ vertices, then we set $v_n$ to be any vertex of $G$ that has degree $\leq 5$ in $G$. Now move to $G - v_n$. This is a planar graph, so it has a vertex $v_{n - 1}$ of degree $\leq 5$ (and so degree $\leq 6$ in $G$). In general, $G - \{v_n, v_{n - 1}, ..., v_{i + 1}\}$ is a planar graph, so it has a vertex $v_i$ of degree $\leq 5$ in $G - \{v_n, v_{n - 1}, ..., v_{i + 1}\}$ and so degree $\leq 5 + (n - i)$ in $G$.

In this way, we have ordered the vertices as $v_1, v_2, ..., v_{n - 1}, v_n$. Colour in this order, using 6 colours: when we colour $v_i$, the degree of $v_i$ in $G - \{v_{i+1}, ..., v_n\}$ is $\leq 5$, so $v_i$ has $\leq 5$ neighbours among the coloured vertices $v_1, v_2, ..., v_i$. Therefore, there is at least one colour of the 6 available that is used to colour any neighbour of $v_{i + 1}$ in $v_1, ..., v_i$ This colour can be used to colour $v_{i + 1}$.    ==$QED.$==

__Revised Version__
We proceed by induction on $|V(G)|$ (the number of vertices on our planar graph).

If $|V(G)| \leq6 $, then $G$ has a 6-colouring.

Suppose the result holds for all planar graph with $k​$ vertices. Let $G​$ be a planar graph with $k + 1​$ vertices. Then, $G​$ has a vertex $v​$ with degree $\leq 5​$ in $G​$. Let $G' = G - v​$. Then $G'​$ is a planar graph on $k​$ vertices and so has a 6-colouring $f:V(G - v) \rightarrow C​$, |C| = 6. Since $deg(v) \leq 5​$, the number of colours appearing in the colouring $f​$ on the neighbours of $v​$ is $\leq 5​$. Thus, there is a colour in $C​$ different from these colours on $v​$'s neighbours that we use on $v​$ to extend $f​$ to a 6-colouring of $ G​$.            ==$QED.​$==

---

__Proof of the 5 Colour Theorem__
If $G$ has a vertex $v$ with degree $\leq 4$, proceed exactly as in the proof of the 6 Colour Theorem, turning any occurrence of $6$ into $5$. 

Otherwise, $G$ has a vertex $x$ with degree 5, and the vertices connected to that vertex must not all be adjacent to each other, since that would create a subdivision of $K_5$ and would make $G$ not planar (a contradiction).

An ==__edge contraction__== $G /e$ of an edge $e$ in a graph $G$ is the graph obtained by reducing the length of $e$ to 0 and allowing the two vertices connected by $e$ to become one vertex, and any vertex that was adjacent to either one or both of the vertices connected to $e$ are connected with the new single vertex.

So, there are two vertices $u,v​$ not adjacent to each other. We edge contract both of these vertices' edges with the vertex with degree 5, so that we have one less vertex. By the inductive hypothesis, we have a graph that is 5-colourable. However, instead of colouring both $u, v​$ different colours, colour them the same colour. 

Now, 2 of the 5 vertices connected to $x$ have the same colour, and so there are 4 colours in the vertices connected to $x$. Colour $x$ the remaining colour out of the 5 we're using to colour the graph, and now we have a 5-colouring of $G$. 