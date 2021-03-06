__CS 245 |__ Nov 1, 2018

# More Properties of Natural Deduction w/ Predicate Logic

### Definability

Let formula $\phi$ have variables $x_1, ...,x_k$. Given an interpretation $I$, a formula $\phi$ __defines__ the $k$-ary relation of tuples that make $\phi$ true. Mathematically, the relation

$$R_\phi = \{(a_1, ..., a_k) \in dom(I)^k \ | \ \phi^{(I, E[x_1 \mapsto a_1]...[x_k \mapsto a_k])} = T \}$$

A relation $R$ is __definable (in $I$)__ _iff_ $R = R_\phi$ for some formula $\phi$.

---

__Ex. Definability in Peano Arithmetic__
The relation $\leq$ is defined by the formula $(\exists z \ ((x_1 + z) = x_2))$.

---

### Soundness & Completeness

Natural Deduction is sound for Predicate Logic: if $\Sigma \vdash \alpha$, then $\Sigma \models \alpha$. 

Natural Deduction is complete for Predicate Logic: if $\Sigma \models \alpha$, then $\Sigma \vdash \alpha$.

_see proof in Carmen's slides_

---



