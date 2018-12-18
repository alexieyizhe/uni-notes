__MATH 239 |__  Nov 2, 2018

# Trees (pt. 5)

==__Theorem^2^:__ Kruskal's (or Prim's) Algorithm always outputs a minimum weight spanning tree.==

>We start with a forest whose components are all the vertices of a graph $G$ as isolated vertices. 
>
>For each iteration: among all edges of $G$ having ends in different components of the current forest, add one that has least weight.

---

__Proof of Kruskal's__
Let $T$ be a tree output by Kruskal's Algorithm. Let $e_1, e_2,...,e_{n-1}$ be the edges of $T$ in the order they are selected.

We claim that for each $i = 0, 1, ..., n-1$, there is a minimum weight spanning tree $S_i$ containing all of $e_1, e_2, ..., e_i$. ($S_0$ is any minimum weight spanning tree).

_Induction Step:_ Assume there is a minimum weight spanning tree $S_i$ containing all of $e_1, ..., e_i$ (every min. weight spanning tree has $n-1$ edges, we just don't know what the other $n - 1 - i$ edges are in this case). 

We prove there is a minimum weight spanning tree containing all of $e_1, ..., e_i$, AND $e_{i+1}$ _(note that_ $T = S_{n-1}$, _so $T$ is a min. weight spanning tree)._If $e_{i+1} \in E(S_i)$, then we're done in this iteration and we set $S_{i +1} = S_i$.

If $e_{i+1}$ is not in $S_i$, then we notice that $T - e_{i+1}$ has two components, say $T_1, T_2$. The ends of $e_{i+1}$ are, say, $u_1, u_2$, with $u_1 \in V(T_1)$ and $u_2 \in V(T_2)$.  Since they are vertices of $T$, of $G$ and of $S_i$, there is a $u_1u_2$-path $P$ in $S_i$. Then $P$ is a path in $G$ starting at a vertex $u_1$ in $V(T_1)$ and ending at a vertex $u_2$ in $V(T_2)$.

There is an edge $vw$ of $P$ having one end $v \in V(T)1$ and $w \in V(T_2)$. Since $e_{i+1}$ is the only edge of $T$ with one end in $T_1$ and the other end in $T_2$, and $e_{i+1} \not\in E(S)$ and $vw \in E(S)$, then we know $e_{i+1} \not= vw$. At the moment we chose $e_{i+1}$, $u_1$ and $u_2$ were in different components of the forest at that time (using edges $e_1, ..., e_i$). Every component of that forest is contained in either $T_1$ or $T_2$, therefore __$vw$ was available in the selection to be added to that forest__, so $weight(vw) \geq weight(e_{i+1})$. 

Look at $S_i + e_{i+1}$: it has the cycle $P + e_{i + 1}$. Deleting any edge $f$ in $P$ produces a new spanning tree of $G$ with weight $weight(S_i) - weight(f) + weight(e_{i+1}) \geq weight(S_i)$, no matter what edge $f$ we delete, since $S_i$ was a minimum weight spanning tree. So, $weight(e_{i+1}) \geq weight(f)$, and if we pick $vw = f$, then $weight(e_{i+1}) \geq weight(f)$ and  $weight(f = vw) \geq weight(e_{i+1})$, so $weight(e_{i+1}) = weight(vw = f)$. So, $S_{i+1} = (S_i - vw) + e_{i+1}$ is a minimum weight spanning tree, since we're replacing $vw$ with $e_{i+1}$ while keeping the same weight and $S_{i+1}$ includes all edges $e_1, ..., e_i, e_{i+1}$. 

By induction, we can show $T = S_{n - 1}$ is a minimum weight spanning tree. 

---

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

---

