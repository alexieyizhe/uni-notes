**MATH 239 |** Oct 1, 2018


# Binary Strings & Recursion
_ex._ Find an unambiguous decomposition for the set $S$ of binary strings that do not contain $010$ as a substring.

> _Recall_:
  __1-decomposition__: $(\{0\}^*\{1\})^*\{0\}^*$
  __block decomposition__: $\{1\}^*(\{0\}\{0\}^*\{1\}\{1\}^*)^*\{0\}^*$

Let $\sigma$ be a string without $010$:
 - if $\sigma$ does not end in $01$, then $\sigma 0$ and $\sigma 1$ also has no $010$.
 - if $\sigma$ ends in $01$, then $\sigma1$ has no $010$.

Let $T$ denote the strings in $S$ that do end in $01$. Then,
$S=\{\epsilon\} \cup (S \setminus T)\{0, 1\} \cup T\{1\}$ and
$T=(S\setminus T)\{01\}$
are unambiguous decompositions ( _i.e. the only way to get $\epsilon$ is from $\{\epsilon\}$, and every string of positive length belongs in either $(S \setminus T)\{0, 1\}$ or $T\{1\}$ but not both_).
So, these three sets are disjoint.

It also means that the concatenation of a string in $S \setminus T$ with $\{0,1\}$ is uniquely determined.

We know:

$\Phi_{\{0,1\}}(x) = 2x$
$\Phi_{\{1\}}(x) = x$
$\Phi_{\{01\}}(x) = x^2$

and thus

$
 \ \ \ \ \ \Phi_T(x) = (\Phi_S(x) - \Phi_T(x)) * \Phi_{\{01\}}(x) = x^2 \Phi_S(x)  - x^2\Phi_T(x) \\
 \Rightarrow (1 + x^2)\Phi_T(x) = x^2\Phi_S(x) \\
 \Rightarrow \Phi_T(x) = \frac{x^2}{(1+x^2)}\Phi_S(x)
$


To find the generating series for $S$:

$
\ \ \ \ \ \Phi_S(x) = 1 + (\Phi_S(x) - \Phi_T(x)) * \Phi_{\{0,1\}}(x) + \Phi_T(x) \Phi_{\{1\}}(x) \\
\Rightarrow (1-2x)\Phi_S(x) = 1-x*\Phi_T(x) \\
\Rightarrow (1-2x)\Phi_S(x) = 1 - x(\frac{x^2}{(1+x^2)}\Phi_S(x)) \\
\Rightarrow \Phi_S(x) = \frac{1}{1 - (2x + \frac{x^3}{1 + x^2})} = \frac{1 + x^2}{1 - 2x + x^2 - x^3}
$

### Tutorial
 1. __Let $A$ be a set of binary strings given by the decomposition $\{1\}^*(\{0\}\{00\}^*\{11\}^*)^*\{0\}^*$.
    Let $B$ be a set of binary strings given by the decomposition $\{00, 101, 11\}^*$.
    Prove that one of these decompositions is unambiguous and the other is ambiguous.__ <br /> <br />

    $A$ is ambiguous. Consider the cases of constructing the string $000$ from $A$. Here are two different ways:
        $\{\epsilon\}^*(\{0\}\{00\}^1\{\epsilon\}^*)^1\{\epsilon\}^*$
        $\{\epsilon\}^*(\{0\}\{\epsilon\}^*\{\epsilon\}^*)^1\{0\}^2$
    \
    We need to prove $B$ is unambiguous. To do so, we need to show $\{\epsilon\}, S, S^2, S^3$, _etc_ are disjoint, and then show S^i is unambiguous for all $i \geq 0$.
    \
    Suppose $\exists \ s \in S^i \cap S^j, i \lt j$.
    We can form $s$ from $i$ strings by using more $101$s than we do when we form $s$ using $j$ strings, so they cannot be the same string!

    But the number of instances of $101$ is uniquely determined by the number of length 1 blocks of $0$s.

    To show $S^i$ is unambiguous, we have to use induction by saying if there is a substring of $00$, find the first instance, delete it to get two strings which have $i - 1$ parts in all, same with $101$, and else the string is all $1$s.




 2.
   a) six Strings b) $\frac{1 - x - x^2}{1-x-2x^2}$
   b) $\frac{1+x-x^2}{1-x-2x^2+x^3-x^5}$
 3.
