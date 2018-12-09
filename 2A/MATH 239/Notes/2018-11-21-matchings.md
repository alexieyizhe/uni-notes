__MATH 239 |__ Nov 21, 2018

# Matchings in Graphs

A __matching__ in a graph $G$ is a set $M$ of edges of $G$ such that every vertex of $G$ is incident with _at most_ one edge in $M$.

> You can have vertices not being incident with any edges in the set $M$, but you cannot have vertices incident with more than one edge in the set $M$.

A matching $M$ is __perfect__ if every vertex is incident with exactly one edge of $M$.

==If $M$ is a matching in a graph $G$, then $|M| \leq \frac{1}{2}|V(G)|$.==

### Saturated & Alternating

Let $M$ be a matching in a graph $G$. 

A vertex $v$ of $g$ is __$M$-saturated__ if $v$ is incident with any edge of $M$. It is __$M$-unsaturated__ if it is not incident with any.
A path $P$ in $G$ is __$M$-alternating__ if the edges in $P$ alternate being in $M$ and not in $M$.
A path $P$ in $G$ is __$M$-augmenting__ if $P$ is $M$-alternating and the end vertices of $P$ are $M$-unsaturated (it is a path starting and ending with edges not in $M$, and alternating in the middle).

==__Theorem:__ If $M$ is a matching in a graph $G$ and $P$ is an $M$-augmenting path in $G$, then $M \ (+) \ P = (M \setminus E(P)) \cup (E(P) \setminus M)$ is a matching with one more edge than $M$ has.==



