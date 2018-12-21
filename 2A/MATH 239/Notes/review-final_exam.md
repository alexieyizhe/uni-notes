__ MATH 239 |__ Final

# Study Guide

### Combinatorics

- **Counting**

  - There are $n \choose k$ $k$-element subsets of an $n$-element set
  - $2^n$ total subsets of an $n$-element set

- **Bijections**

  - To show a bijection between two sets, you have the following options:	
    1. Determine a function $f$ and its inverse $f^{-1}$ such that for any set of values $(a_1, ...,a_n)$ in the first set, $f((a_1, ..., a_n)) = (b_1, ..., b_m)$ where $(b_1, ..., b_m) \in$ the second set, and $f^{-1}((b_1, ..., b_m)) = (a_1, ..., a_n)$.
  - To determine if $LS = RS$, find two sets that describe each side respectively, and show that there's a bijection between the two sets!

- **Combinatorial Proofs**

  - Find bijections lol
  - ==__Binomial Theorem:__== $(1+x)^n = \sum\limits_{k = 0}^n {n \choose k} x^k$
  - ==__Negative Binomial Theorem:__== $\frac{1}{(1-x)^k} = \sum\limits_{n \geq 0} {{n + k - 1} \choose {k - 1}} x^n$  

- **Series**

  - Sum of an infinite geometric series:
    - $\sum\limits_{n = 0}^{\infty}ar^n = \frac{a}{1-r}$
  - A generating series is a way to represent, given a specific weight function $w$ and a set of configurations $S$, the number of elements in $S$ with weight $k$ is $a_k$, where $\Phi_S(x) = \sum\limits_{a \in S}x^{w(a)} = \sum\limits_{k = 0}^{\infty}a_kx^k$.
  - Generating Series from:
    - **Binary string**: weight of string is its length

- **Formal Power Series**

  - $\sum\limits_{n = 0}^{\infty}a_nx^n$ is a formal power series
  - A formal power series has an __inverse__ _iff_ it has a non-zero constant term. If the constant term is non-zero, the inverse is unique.
  - If $A(x)$ and $B(x)$ are formal power series with the constant term of $B(x)$ equal to zero, then $A(B(x)) $ is a formal power series
    - If $B(x)$ had a non-zero constant term, then $A(B(X))$ would have a sum of infinite constant terms which is not a well-defined formal power series 
  - To find an inverse of $f(x)$: 
    - Inverse of $1-x$ is $1+x+x^2+...$
    - Let $P(x) = 1-x$, write the original $f(x)$ in terms of $P(a)$, then $f^{-1} = P(a)^{-1} $.
    - **Inverse also needs to be a formal power series, otherwise inverse does not exist or is not correct**

- **Sum/Product Lemmas**

  - ==___Sum Lemma:_ Let $A, B$ be a partition of a set $S$ ($A$ and $B$ are disjoints sets whose union is $S$). Then:__==
    $$\Phi_S(x) = \Phi_A(x) + \Phi_B(x)$$
    - This can be generalized to $n$ sets by applying the inclusion-exclusion principle for sets
      - _ie._ $\Phi_{A \cup B}(x) = \Phi_A(x) + \Phi_B(x) - \Phi_{A \cap B}(x)$
  - ==___Product Lemma:_ Let $A, B$ be sets of configurations with weight functions $\alpha$ and $\beta$ respectively. If $w(\gamma) = \alpha (a) + \beta (b)$ for each $\gamma = (a, b) \in A \times B$, then:__==
    $$\Phi_{A \times B}(x) = \Phi_A(x) \Phi_B(x)$$
  - The Product Lemma fails when:
    1. There is ambiguity in the sets/decompositions.
    2. The weight functions don't match ($w(ab) \not= w(a) + w(b)$)
       _ex._ Let $A=\{2, 3, 4\}, \alpha(a) = a$ and $B = \{1, 5\}, \beta(b) = b$. Then, $\Phi_A(x) = x^2 + x^3 + x^5, \Phi_B(x) = x+ x^5$. Then, let $A \times B = \{(2, 1), (3, 1), (4, 1), ...\}$ and $w((a,b)) = 3a + 2b$, but in order for the Product Lemma  to apply, it would produce a $w((a,b)) = a + b$ instead.

- **Integer Compositions (compositions of parts that make up $n$)**

  - There are ${n - 1} \choose {k- 1}$ compositions of $n$ with $k$ parts
  - Parts in a composition are $\geq 1$
  - In general, to solve problems along the lines of `how many compositions of n are there with ... (some property)`:
    1. Define a set $S$ that represents all possible compositions of a certain type with the property we're looking for (without considering a specific $n$)
    2. Find the generating series $\Phi_p(x)$ for a single part of the composition using the property/restriction of a single part 
    3. Find $\Phi_S(x)$ where $w(a_1,...,a_k) = a_1 + ... + a_k$ (find the generating series for S where the weight is the sum of the parts). This generating series is:
       - $\sum\limits_{k = 0}^\infty(\Phi_p(x))^k$ if the number of parts can by any amount *by product and sum lemma*
       - $(\Phi_p(x))^k$ if they want a specific $k$ number of parts *by product lemma*
    4. The answer to the number of compositions of $n$ is $[x^n]\Phi_S(x)$
    5. Try to find an explicit formula for $[x^n]\Phi_S(x)$ or try to simplify if possible with series, etc
  - Look at Chapter 2.2!!!

- **Binary Strings**

- **Binary Decompositions**

  - 3 ways to decompose:

    1. __Decompose after either a 0 or a 1 (after each character)__: $\{0, 1\}^*$

    2. __Decompose after each occurrence of $0$ OR $1$__:

       $(\{1\}^*\{0\})^*\{1\}^*$ or : $(\{0\}^*\{1\})^*\{0\}^*$

    3. __Block decomposition__: $\{1\}^*(\{0\}\{0\}^*\{1\}\{1\}^*)^*\{0\}^*$ or $\{0\}^*(\{1\}\{1\}^*\{0\}\{0\}^*)^*\{1\}^*$

       1. The part that changes is inside the $()$!! Use that to form the specific property you're looking for

    4. Recursively define the string:

       1. The empty string is in $S$.

       2. Any other element of $S$ consists of either 0 or 1 followed by another element of $S$.

          _sometimes its helpful to find two different equations to describe it, then sub one into the other_

  - Sum and Product Rules:

    - If $A, B$ are binary strings:
      1. If the expression $AB$ is unambiguous, then $\Phi_{AB}(x) = \Phi_A(x) \Phi_B(x)$
      2. If the expression $A^*$ is unambiguous, then $\Phi_{A^*}(x) = (1 - \Phi_A(x))^{-1} $

  - ==look at chapter 2.7, 2.8!!==

  - How to find an unambiguous decomposition:	

    1. 

- **Finding Coefficients (==look at chapter 3.1==)**

- **Homogeneous Recurrences (Recurrence Relations)**

  - To find a recurrence relation:
    1. Multiply denom of fraction over to LS. 
    2. "Expand" generating series (power series with $\sum\limits_{n \geq 0}$) to find terms of $x^0, x^1, x^2, ...$
    3. Compare coefficients to get initial conditions and use later terms in the power series to find a recurrence relation.
  - To find closed form formula for $[x^n]\Phi_S(x)$:
    1. Use reurrence relation to get characteristic polynomial (example $a_n - a_{n-1} - 2a_{n-2}$ gives CP of $x^2 - x - 2$, use the coefficients as coefficients of CP, power of $x$ in CP is position relative to right side)
    2. $[x^n]\Phi_S(x) = (r_1^n)*A + (r_2^n) * B$ where $r_n$ is one of $n$ roots, and $A, B$ are either $A, B, An+B, An^2+Bn+C$, depending on the multiplicity of the root (how many times the root appears, $(x-2)$ has multiplicity 1 so will be $A$ or $B$, $(x - 2)^3$ has multiplicity 3 so will be $An^2 + Bn + C$
    3. Compare initial conditions with subbing in $n$ for any $n \geq 1$ to part 2 (ex. $a_1 = 0$ means sub in $n = 1$ and set equal to 0)
    4. Solve for $A, B, C, etc$ to get closed form formula
    5. If the recurrence relation is for $n \geq x$  where substituting $x$ into recurrence is greater than 0, make sure to have separate case for $a_0, (n = 0)$ (which you can get from initial condition)
  - ==PRACTICE THIS==

- **Partial Fractions**



### Graph Theory

- A **graph** $G$ is a finite nonempty set, $V(G)$, of vertices, together with a set $E(G)$ of unordered pairs of distinct vertices, called edges.

- ==__Handshake Lemma__: Let $(V, E)$ be a graph. Then, $\sum\limits_{v \in V(G)} deg(v) = 2|E(G)| $==

  - __Corollary:__ Every graph has an even number of vertices with odd degree.

- **Isomorphism**

  - Find 1:1 correspondence (bijection!!) between vertices of two graphs to prove isomorphism

- **Bipartite Graph**s: a graph that can be partitioned evenly into two sets such that every edge has one side in one set and the other in the other set.

  - ==A graph is bipartite _iff_ it has no odd cycle.==

- **Paths/Cycles**

  - A __walk__ is any linear series of vertices all connected (doesn't have to be unique)
  - A __path__ is a walk with all vertices in it being unique
  - ==__Lemma^1^__: If every vertex in a graph $G$ has degree at least 2, then $G$ has a cycle.==
  - Every cycle in a bipartite graph has **even** length.

- **Connections**: a graph is connected if for any two vertices $x, y$, there is a path from $x$ to $y$.

  - A **component** of $G$ is a subgraph $C$ of $G$ such that 

    1. $C$ is connected

    2. No subgraph of $G$ that properly contains $C$ is connected

       _basically a component is a subgraph of $G$ that is maximally connected_

  - If every component of a graph is bipartite, the graph is bipartite

  - Given a set of vertices $X$ in a graph $G$, the ==__cut__== induced by $X$ is the set of edges in $G$ that have exactly one end in $X$ (set of edges that dont connect vertices in the set to each other, and don't connect vertices outside the set)

- **Bridges**: an edge $e$ of a graph $G$ is a __bridge__ if $G - e$ has exactiy one more component than $G$.

  - _basically an edge is a bridge if removing it splits the graph_
  - An edge is a bridge of a graph _iff_ it is not contained in any cycle of that graph.
  - If there are two distinct paths from a vertex $u$ to a vertex $v$ in $G$,  then $G$ contains a cycle.

- **Trees**: a connected graph with no cycles

  - every edge of a tree is a _bridge_
  - ==__Theorem^2^__: Let $T$ be a tree with $n \geq 1$ vertices. Then, $|E(T)| = |V(T)| - 1 = n - 1$.== 
    - derived from Euler's formula
  - every tree has at least two vertices with $deg =1$, except the tree with one vertex (1 vertex with degree 1)
  - ==Every tree is bipartite.== (proof by induction)
  - ==__Theorem:__ A graph is connected _iff_ it has a spanning tree.==
  - ==__Theorem^2^:__ Let $G$ be a graph. If any 2 of the following 3 statements hold, then $G$ is a tree:==
    1. ==$G$ is connected.==
    2. ==$|E(G)| = |V(G)| - 1$==
    3. ==$G$ has no cycles.==
  - A __spanning tree__ of a graph $G$ is a tree with the same vertices as $G$.
  - ==__Theorem__: If $T$ is a spanning tree of a graph $G$ and $e$ is an edge in $G$ not in $T$, then $T + e$ has exactly one cycle. As well, if $e'$ is any edge in that cycle, then $T + e - e'$ is also a spanning tree of $G$.==
  - **Minimum Weight Spanning Trees**: two algorithms to find them:
    - **Prim's**: pick any vertex and add it to $T$, find the cheapest edge having one end in $T$ and the other not, add the other end to $T$, repeat
      - proof by induction, show a MST containing each tree at each step of the process _is_ the same as the tree at that step
    - **Kruskal's**: sort edges in a list from cheapest to least cheap, pick cheapest edge not in tree that does not form a cycle when added to the tree, add edge to tree and repeat until no options left

- **Planar graphs**: graphs that can be represented (drawn) in a single plane without two edges intersecting

  - A _tree_ is always planar: proof by induction - since a tree always has at least 1 vertex with degree 1, remove that to use the inductive hypothesis
  - ==__Euler's Formula__: For all planar graphs, $|V(G)| - |E(G)| + |Faces(G)| = 1 + components(G)$==
    - proof by induction: use a spanning tree of a graph $G$, add an edge to form a cycle, show that adding the edge increases faces by 1 and that Euler's formula still holds true
    - a **platonic solid** is a shape with a planar embedding where all vertices ahve same degree and all faces have same degree
      - there are 5: cube, icosahedron, tetrahedron, octahedron, dodecahedron
      - (vertex degrees, face degrees) of platonic solids: (3, 3), (3, 4), (3, 5), (4, 3), (5, 3)
  - ==__Faceshake Lemma__: Let $F$ be the set of faces of a planar graph $G$. Then, $\sum\limits_{f \in F} deg(f) = 2|E(G)| $== 
  - If $G$ contains a cycle, then in a planar embedding of $G$, the boundary of every face contains a cycle.
  - **Theorem:**
    1. ==Every planar graph has a vertex with degree $\leq 5$.==
    2. ==If $G$ is a planar graph with $\geq 3$ vertices, then $|E(G)|  \leq 3|V(G)| - 6$. (__not__ an _iff_)==
       1. ==If $G$ is also bipartite, then $|E(G)| \leq 2|V(G)| - 4$ (tighter bound)==
    3. ==If $G$ is a connected planar graph with $\geq 3$ vertices, then every face has degree $\geq 3$.==
  - ==**Kuratowski's Theorem**: A graph is NOT planar _iff_ it contains a subdivision of either $K_5$ or $K_{3, 3}$.==
    - Complete graph with 5 vertices, or complete _bipartite_ graph with 3 vertices in each partition
    - A ==**subdivision**== is a graph where you remove an edge and add a vertex of degree 2 connected to the two vertices that the edge you removed connected to previously

- **Graph Colouring**

  - A graph can be coloured with:
    - 1 colour if it has no edges
    - 2 colours if it is bipartite
    - 3 colours if it contains only odd cycles
    - $n$ colours if it is a complete graph with $n$ vertices ($K_n$)
    - $k + 1$ colours if it is a graph with the largest degree of any vertex being $k$
    - 4 colours if it is planar
      - prove 6-colour and 5-colour theorem by induction:
        - we know it has a vertex of degree $\leq 5$, remove that vertex, use inductive hypothesis, that vertex will connect to at most 5 other colours, use the 6^th^ (or 5^th^ if proving 5-colour thm) colour on that vertex
        - If vertex $v$ has degree = 5, there are two vertices not adjacent to each other in the vertices connected to $v$ otherwise it would not be planar since it has $K_5$. colour those two the same colour, now we have at most 4 colours used, colour vertex $v$ the 5^th^ colour
  - **Planar Duals**
    - Draw a vertex for $G^*$ on each face in $G$. Draw edges in $G^*$ connecting vertices wherever two faces are separated by an edge in $G$ and wherever same face appears on both sides of an edge in $G$.
    - can use Four Colour Theorem to colour faces just like colouring vertices, since graph is symmetric between duals via _duality_

- **Matchings & Covers**

  - A **matching** $M$ is a set of edges in a graph where every vertex is incident with at most one edge in $M$.

    - A __perfect matching__ is one where all vertices are incident with an edge in $M$

  - A **cover** $C$ is a set of vertices in a graph where every edge is incident with at least one vertex in $C$.

  - | Graph Type        | Largest Matching                                             | Smallest Cover                                               |
    | ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
    | $K_n$             | $\left \lfloor{\frac{n}{2}}\right \rfloor$  (any larger and you will have two edges in $M$ connecting to the same vertex) | $n - 1$ (any smaller and there will be two vertices not in $C$ with an edge connecting them) |
    | $K_{a, b}$        | $min(a, b)$                                                  | $min(a, b)$                                                  |
    | $Q_n$             | $2^{n - 1}$                                                  | $2^{n - 1}$                                                  |
    | Cycle with length | $\left \lfloor{\frac{n}{2}}\right \rfloor$                   | $\left \lceil{\frac{n}{2}}\right \rceil$                     |
    | Path with length  | $\left \lceil{\frac{n}{2}}\right \rceil$                     | $\left \lceil{\frac{n}{2}}\right \rceil$                     |

  - ==__König's Theorem: __If $G$ is a bipartite graph, then the size of a maximum matching and the size of a minimum cover are equal.== (see some examples above)

  - ==__Lemma:__ If $M$ and $C$ are a matching and a cover in a graph $G$, respectively, then $|M| \leq |C|$ .==

  - ==__Theorem^1^:__ If $M$ is a matching in a graph $G$ that is not a maximum matching, then there is an $M$-augmenting path in $G$.==

    - We know there is a matching $N$ larger than $M$, we take a subgraph with edges only from $N$ or $M$ and show that there has to be a component that's n alternating path with odd length and more $N$ edges than $M$ edges, which means it's an $M$-augmenting path

  - ==**Bipartite Matching Algorithm**==

    - Let $G$ be a bipartite graph, with bipartition $(A, B)$ of $V(G)$. Let $M$ be a matching in $G$. Our algorithm outputs either a matching $N$ such that $|N| > |M|$ or a cover $C$ such that $|C| = |M|$.
      1. Let $\hat X$ be the set of all $M$-unsaturated vertices in $A$. Let $\hat Y$ be $\emptyset$. Let $pr(v)$ be the parent vertex to a vertex $v$ and set it to undefined for all $v \in V(G)$.
      2. For every vertex $v \in B \setminus \hat Y$ that connects to a vertex $u$ in $\hat X$, add $v$ to $\hat Y$ and set $pr(v) = u$.
         - If no vertex satisfies the conditions in Step 2, ==$C = \hat Y \cup (A \setminus \hat X)$ is a **minimum cover**== with $|C| = |M|$, which also makes ==$M$ a **maximum matching**== by König's Theorem. __Algorithm terminates.__
         - If a vertex $v$ that is $M$-unsaturated is added to $\hat Y$, use $pr()$ values to trace an augmenting path from $v$ to an $M$-unsaturated element of $\hat X$. Use this path to create ==a larger **matching** $M'$==. __Algorithm repeats with $M'$ as the matching.__
      3. For every vertex $v \in A \setminus \hat X$ that connects to a vertex $u \in \hat Y$ through an edge in $M$, add $v$ to $\hat X$ and set $pr(v) = u$. __Repeat from Step 2.__

  - ==__Hall's Theorem:__ Let $G$ be a bipartite graph with bipartition $(A, B)$. $G$ has a matching that saturates _all_ of $A$ _iff_ for every subset $X \subset A$, $|N(X)| \geq |X|$ where $N(X) = \{y \in B \ | \ \text{there is an } x\in X, xy \in E(G)\}$ (the set of edges with one end in $X$ and one in $Y$).== 

    - Basically saying that we can have a perfect matching only if the bipartition separates the vertices equally _and_ for every subset of $A$, there are enough vertices connected to them in the other bipartitioned set (all these vertices form the neighbour set) to have a unique edge between each vertex in the subset and one in the other bipartitioned set.
      - which is why a $k$-regular bipartite graph always has a perfect matching!
    - ==Every $k$-regular bipartite graph has a perfect matching.==

- TIPS:

  - consider vertices at the end of a longest path in a graph
  - use induction when in doubt!





- [ ] counting how many binary strings satisfy a certain requirement

- [ ] combinatorial proofs

  - [ ] finding bijections

  - [ ] finding two ways to count things

    ![image-20181218214744618](/Users/alexieyizhe/Google Drive/University/2A/MATH 239/Notes/review-final_exam.assets/image-20181218214744618-5187664.png)

    ![image-20181218214759463](/Users/alexieyizhe/Google Drive/University/2A/MATH 239/Notes/review-final_exam.assets/image-20181218214759463-5187679.png)

- [ ] finding generating series from 

  - [ ] descriptions of sets

    $\Phi_S(x) = \sum\limits_{\sigma \in S}x^{w(\sigma)}$ where $w$ is the weight function

  - [ ] compositions

    - $w$ is the sum of all the parts ($w(c_1, c_2, ..., c_k) = w(c_1) + w(c_2) + ... + w(c_k)$)

  - [ ] binary strings

- [ ] formal power series

  - [ ] inverses

    ![image-20181218215551474](/Users/alexieyizhe/Google Drive/University/2A/MATH 239/Notes/review-final_exam.assets/image-20181218215551474-5188151.png)

  - [ ] finding coefficients of rational functions/generating series

- [ ] finding amounts of compositions

- [ ] definitions of important theorems

  - [ ] sum and product lemma

- [ ] binary strings

  - [ ] determine if they are ambiguous
  - [ ] finding unambiguous decompositions
    - [ ] block decomp
      - [ ] use $\{1\}^*(\{0\}\{0\}^*\{1\}\{1\}^*)^*\{0\}^*$ or $\{0\}^*(\{1\}\{1\}^*\{0\}\{0\}^*)^*\{1\}^*$ and substitute middle part for what you need
    - [ ] Recursively
      - [ ] Find $L$, the set of strings that do not contain $X$ (a substring)
        - Let $M$ be the set of strings that have one occurrence of $X$ exactly, at the end of string
          $\{\epsilon\} \cup L\{0, 1\} = L \cup M$
          $L\{X\} = M$
          is a recursive unambiguous decomp for $L$
        - can convert this to generating series and solve 2 equations 2 unknowns for $\Phi_M(x)$, then sub in to solve for $\Phi_L(x)$ 

- [ ] finding closed form formula for a coefficient of a generating series

  - [ ] finding recurrence relations
  - [ ] finding closed form formulas

- [ ] drawing graphs

  - [ ] finding isomorphisms: find vertices with distinct characteristics and use those
- [ ] finding minimum weight spanning tree using Prim's or Kruskal's
- [ ] prove a graph is planar or non-planar (draw planar embedding _or_ use Kuratowski's Theorem)
- [ ] finding maximum matching/minimum cover using bipartite matching algorithm
- [ ] drawing planar duals













------

1. __Give a combinatorial proof that, for non-negative integers $n \geq k \geq r$, __

   ${n \choose k} {k \choose r} = {n \choose r}{{n - r} \choose {k - r}}$.

2. Determine the following coefficient. Simplify as much as possible.

   $[x^n]\frac{(1+x)^n}{1-x}$

3. Let $A_n$ be the set of all compositions of $n$ where each part is either 1 or 3. Note that the number of parts is not restricted. For example, compositions in $A_4$ include (1, 3) and (1, 1, 1, 1) but not (2, 1, 1) nor (4).

   1. Prove that $|A_n| = [x^n]\frac{1}{1 - x - x^3}$
   2. Let $a_n = |A_n|$. Derive a recurrence relation that the sequence ${a_n}$ satisfies, along with sufficient initial conditions to uniquely specify the sequence.

4. 

   1. Let $S$ be the set of binary strings with the following decomposition: $S = (\{0\}^*\{11\}\{1\}^*)^*$. Explain why this is an ambiguous expression for $S$. 
   2. Suppose the weight of a string is its length. Let $\phi_S(x)$ be the generating series for $S$. Suppose we obtain $\phi_S^{'}(x)$ by applying the product and sum lemmas for strings using the ambiguous expression in part (a). Which of the following are true? Justify your answer.
      1. For all $n \geq 1$, $[x^n]\phi_S(x) \gt [x^n]\phi_S^{'}(s)$.
      2. For all $n \geq 1$, $[x^n]\phi_S(x) \lt [x^n]\phi_S^{'}(s)$.
      3. There exists an $n \geq 1$ such that $[x^n]\phi_S(x) \gt [x^n]\phi_S^{'}(x)$.
      4. There exists an $n \geq 1$ such that $[x^n]\phi_S(x) \lt [x^n]\phi_S^{'}(x)$.
   3. Write an unambiguous expression for the set of all binary strings that do not contain $1100$ as a substring.

5. For $n \in \N$, let $G_n$ be the graph whise vertices are all the compositions of $n$ and there is an edge between two compositions if we can add two consecutive terms in the longer composition to get the shorter composition. 

   For example, in $G_{11}, (1, 4, 3, 2, 1)$ is adjacent to $(1, 7, 2, 1)$ by combining the second and third part (4 and 3) to get 7. Furthermore, (1, 7, 2, 1) is adjacent to (8, 2, 1).