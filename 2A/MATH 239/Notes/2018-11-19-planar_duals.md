__MATH 239 |__ Nov 19, 2018

# Planar Duals

![Image result for planar duals](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/Noniso_dual_graphs.svg/290px-Noniso_dual_graphs.svg.png)

We give each **face** of a graph $G$ a **vertex** to form a graph $G'$. This allows you to go from colouring vertices to colouring faces, allowing us to use the 4-colouring theorem for colouring faces (like regions on a map, etc).

We also draw **edges** connecting the vertices in $G'$ such that $G'$ has an **edge** whenever two faces of $G$ are separated from each other by an edge in $G$, and a **loop** whenever the same face appears on both sides of an edge.

This is a planar graph. It is the planar __dual__ of $G$, meaning that $G' $ is a dual of $G$ and $G$ is a dual of $G'$ (symmetric).

==__Theorem^1^:__ Let $G$ be a connected graph embedded in the plane and let $T$ be a spanning tree of $G$. Let $G^*$ be the dual of $G$. Then $(V(G^*), \ E(G^*) \setminus E^*(T) )$ is a spanning tree of $G^*$.==

---

__Proof of Theorem^1^__
We showed that the number of edges is the right number for a spanning tree of $G^*$. We will show that these edges do not include the edges of a cycle in $G^*$.

So, let $C^*$ be a cycle of $G^*$ using the edges not in $T$. Let $e^*$ be any edge of $C^*$ and let $e$ be the edge of $G$ dual to $e^*$. Let $u,v$ be the vertices of $G$ incident with $e$. Notice that $u,v$ are on different sides of $C^*$.

There is a $uv$-path $P \text{ in } T$. There is, starting from $u$, a first vertex $w$ of $P$ on the side of $C^*$ containing $v$. The predecessor $x$ of $w$ in $p$ is on the same side of $C^*$ as $u$, so $xw$ crosses $C^*$. But then either $xw$ is not in $T$ or the edge of $C^*$ crosses in $T$. These are both contradictions, so $C^*$ does not exist.    ==$QED.$==

