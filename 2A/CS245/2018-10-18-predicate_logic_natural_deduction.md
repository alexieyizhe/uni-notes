__CS 245 |__ Oct 18, 2018

# Natural Deduction for Predicate Logic

A variable $x$ is __fresh__ in a subproof if $x$ does not occur anywhere outside the box of the subproof.

> Do not reuse variable names for fresh variables. Start with a new fresh variable for different subproofs!

A variable $y$ is __not free__ in a set of well-formed Predicate Logic formulas  $\Sigma$ _iff_ it is not free in any $\gamma \in \Sigma$.

----

__Ex.__ Not Free Variables
Let $L$ be a language consisting of variables $w, x, y, z$, and predicate symbols $P^{(2)}, Q^{(1)}$. Then, if
$$\Sigma = \{(\forall w \ \P(w, x)), (\exists y \ Q(y))\}$$
we see that each of $w, y, z$ are _not_ free in $\Sigma$ and only $x$ is free.

---

| Name                   | $\vdash$-notation                                            | Inference Notation                                           | Explanation                                                  |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| $\forall$-elimination  | If $\Sigma \vdash (\forall x \ \alpha)$, then $\Sigma \vdash \alpha[t/x]$ | $\frac{(\forall x \ \alpha)}{\alpha[t/x]}$                   | If a formula $\alpha$ holds for any $x$, it holds for a specific term $t$ |
| $\forall$-introduction | If $\Sigma \vdash \alpha[u/x]$ and $u$ is not free in $\Sigma$ or $\alpha$, then $\Sigma \vdash (\forall x \ \alpha)$ | $\frac{[u^f...\alpha [u/x]]}{(\forall x \ \alpha)}$          | $u^f$ denotes a __fresh__ variable.So, in order to prove $(\forall x \ \alpha(x))$, prove $\alpha(u)$ for an arbitrary $u$. By "$u$ not free in $\alpha$" we mean when $\alpha$ becomes $\forall x \ \alpha$, it cannot still contain $u$. |
| $\exists$-elimination  | If $\Sigma, \alpha[u/x] \vdash \beta$, with $u$ fresh, then $\Sigma, (\exists x \ \beta) \vdash \beta$ | $\frac{(\exists x \ \alpha) \ \ \ [\alpha[u/x], u^f...\beta]}{\beta}$ |                                                              |
| $\exists$-introduction | If $\Sigma \vdash \alpha[t/x]$, then $\Sigma \vdash (\exists x \ \alpha)$ | $$\frac{\alpha[t/x]}{(\exists x \ \alpha)}$$                 | If a formula $\alpha$ holds for a term $t$, then it holds for some $x$. |

### Examples

__$\forall$-i__
_to be finished unless lazy then look at Lecture 13 Stephanie's notes_

