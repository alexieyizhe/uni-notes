__MATH 239 |__ Midterm

# Study Guide

- Counting

  - There are $n \choose k$ $k$-element subsets of an $n$-element set
  - $2^n$ total subsets of an $n-element set

- Bijections

  - To show a bijection between two sets, you have the following options:	
    1. Determine a function $f$ and its inverse $f^{-1}$ such that for any set of values $(a_1, ...,a_n)$ in the first set, $f((a_1, ..., a_n)) = (b_1, ..., b_m)$ where $(b_1, ..., b_m) \in$ the second set, and $f^{-1}((b_1, ..., b_m)) = (a_1, ..., a_n)$.
  - To determine if $LS = RS$, find two sets that describe each side respectively, and show that there's a bijection between the two sets!

- Combinatorial Proofs

  - Find bijections lol
  - $(1+x)^n = \sum\limits_{k = 0}^n {n \choose k} x^k$
  - 

- Series

  - Sum of an infinite geometric series:
    - $\sum\limits_{n = 0}^{\infty}ar^n = \frac{a}{1-r}$
  - A generating series is a way to represent, given a specific weight function $w$ and a set of configurations $S$, the number of elements in $S$ with weight $k$ is $a_k$, where $\Phi_S(x) = \sum\limits_{a \in S}x^{w(a)} = \sum\limits_{k = 0}^{\infty}a_kx^k$.

- Formal Power Series

  - $\sum\limits_{n = 0}^{\infty}a_nx^n$ is a formal power series
  - A formal power series has an __inverse__ _iff_ it has a non-zero constant term. If the constant term is non-zero, the inverse is unique.
  - If $A(x)$ and $B(x)$ are formal power series with the constant term of $B(x)$ equal to zero, then $A(B(x)) $ is a formal power series.
  - To find an inverse of $f(x)$: 
    - Inverse of $1-x$ is $1+x+x^2+...$
    - Let $P(x) = 1-x$, write the original $f(x)$ in terms of $P(a)$, then $f^{-1} = P(a)^{-1} $.
    - ![image-20181105224931292](/Users/alexieyizhe/Documents/Projects/uni-notes/2A/M239/image-20181105224931292.png)

- Sum/Product Lemmas

  - ==___Sum Lemma:_ Let $A, B$ be a partition of a set $S$ ($A$ and $B$ are disjoints sets whose union is $S$). Then:__==
    $$\Phi_S(x) = \Phi_A(x) + \Phi_B(x)$$
    - This can be generalized to $n$ sets by applying the inclusion-exclusion principle for sets
      - _ie._ $\Phi_{A \cup B}(x) = \Phi_A(x) + \Phi_B(x) - \Phi_{A \cap B}(x)$
  - ==___Product Lemma:_ Let $A, B$ be sets of configurations with weight functions $\alpha$ and $\beta$ respectively. If $w(\gamma) = \alpha (a) + \beta (b)$ for each $\gamma = (a, b) \in A \times B$, then:__==
    $$\Phi_{A \times B}(x) = \Phi_A(x) \Phi_B(x)$$
  - The Product Lemma fails when:
    1. There is ambiguity in the sets/decompositions.
    2. The weight functions don't match. 
       _ex._ Let $A=\{2, 3, 4\}, \alpha(a) = a$ and $B = \{1, 5\}, \beta(b) = b$. Then, $\Phi_A(x) = x^2 + x^3 + x^5, \Phi_B(x) = x+ x^5$. Then, let $A \times B = \{(2, 1), (3, 1), (4, 1), ...\}$ and $w((a,b)) = 3a + 2b$, but in order for the Product Lemma  to apply, it would produce a $w((a,b)) = a + b$ instead.

- Integer Compositions (compositions of parts that make up $n$)

  - There are ${n - 1} \choose {k- 1}$ compositions of $n$ with $k$ parts
  - In general, to solve problems along the lines of `how many compositions of n are there with ... (some property)`:
    1. Find a set $S$ that represents all possible compositions of a certain type with the property we're looking for (without considering a specific $n$)
    2. Find $\Phi_S(x)$ where $w(a_1,...,a_k) = a_1 + ... + a_k$ (find the generating series for S where the weight is the sum of the parts)
    3. The abswer to the number of compositions of $n$ is $[x^n]\Phi_S(x)$
    4. Try to find an explicit formula for $[x^n]\Phi_S(x)$ or try to simplify if possible with series, etc
  - Look at Chapter 2.2!!!

- Binary Strings

- Binary Decompositions

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

- Finding Coefficients (==look at chapter 3.1==)

- Homogeneous Recurrences (Recurrence Relations)

  - To find a recurrence relation:
    1. Multiply denom of fraction over to LS. 
    2. "Expand" generating series (power series with $\sum\limits_{n \geq 0}$) to find terms of $x^0, x^1, x^2, ...$
    3. Compare coefficients to get initial conditions and use later terms in the power series to find a recurrence relation.
  - To find closed form formula for $[x^n]\Phi_S(x)$:
    1. Use reurrence relation to get characteristic polynomial (example $a_n - a_{n-1} - 2a_{n-2}$ gives CP of $x^2 - x - 2$)
    2. $[x^n]\Phi_S(x) = (r_1^n)*A + (r_2^n) * B$ where $r_n$ is one of $n$ roots, and $A, B$ are either $A, B, An+B, An^2+Bn+C$, depending on the multiplicity of the root (how many times the root appears, $(x-2)$ has multiplicity 1, $(x - 2)^3$ has multiplicity 3)
    3. Compare initial conditions with subbing in $n$ for any $n \geq 1$ to part 2 (ex. $a_1 = 0$ means sub in $n = 1$ and set equal to 0)
    4. Solve for $A, B, C, etc$ to get closed form formula
    5. Make sure to have separate case for $a_0, (n = 0)​$ (which you can get from initial condition)
  - ==PRACTICE THIS==

- Partial Fractions

- Graph Theory

  - A __graph__ is an ordered pair $(V, E)$ of finite sets $V$ and $E$ such that $E$ (an __edge__) is a set of subsets of $V$ (a __vertex__) of size 2.

  - ==__Handshake Lemma__: Let $(V, E)$ be a graph. Then, $\sum\limits_{v \in V} deg(v) = 2|E|$==

    - __Corollary:__ Every graph has an even number of vertices with odd degree.

  - Isomorphism

    - Find 1:1 correspondence (bijection!!) between vertices of two graphs to prove isomorphism

  - Bipartite Graphs: a graph that can be partitioned evenly into two sets such that every edge has one side in one set and the other in the other set.

  - Paths/Cycles

    - A __walk__ is any linear series of vertices all connected (doesn't have to be unique)
    - A __path__ is a walk with all vertices in it being unique
    - ==__Lemma^1^__: If every vertex in a graph $G$ has degree at least 2, then $G$ has a cycle.==
    - Every cycle in a bipartite graph has **even** length.

  - Connections: a graph is connected if for any two vertices $x, y$, there is a path from $x$ to $y$.

    - A component of $G$ is a subgraph $C$ of $G$ such that 

      1. $C$ is connected

      2. No subgraph of $G$ that properly contains $C$ is connected

         _basically a component is a subgraph of $G$ that is maximally connected_

  - Bridges: an edge $e$ of a graph $G$ is a __bridge__ if $G - e$ has more components than $G$.

    - _basically an edge is a bridge if removing it splits the graph_
    - An edge is a bridge of a graph _iff_ it is not contained in any cycle of that graph.
    - If there are two distinct paths from a vertex $u$ to a vertex $v$ in $G$,  then $G$ contains a cycle.

  - TIPS:

    - consider vertices at the end of a longest path in a graph

_70% Non-Graph Theory, 30% Graph Theory_

### Midterm Review Session

1. Let $S_n$ be the set of compositions of $n$ where each part is greater than 1.

   1. Prove that $|S_n| = [x^n]\frac{1-x}{1-x-x^2}$.

      Let $S$ be the set of all compositions where each part $\geq 2$. Then, $S = \cup_{i \geq 0}S_i = \cup_{i \geq 0} \N^i_{\geq2}, \N_{\geq 2} = \{2, 3, 4,...\}$ Then, $\Phi_S(x) = \sum\limits_{i \geq 0}(\Phi_{\N_{\geq 2}}(x))^i = \sum\limits_{i \geq 0}(x^2+x^3+...)^i = \sum\limits_{i \geq 0}(\frac{x^2}{1-x})^i = \frac{1}{1 - \frac{x^2}{1-x}} = \frac{1 - x}{1 - x - x^2}$.

   2. Derive a recurrence relation satisfied by $a_n$, where $a_n = |S_n|$.

      $\Phi_S(x) = $



























---

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