__CS 245 |__ Oct 30, 2018

# Equality Axioms

The Equality Axioms are:

------

__EQ~symm~:__ $(\forall x \ (\forall y \ ((x = y) \rightarrow (y = x))))$

------

__EQ~trans(k)~:__ $\frac{(t_1 = t_2) \ \ (t_2 = t_3) \ \ ... \ \ (t_k = t_{k + 1})}{(t_1 = t_{k+1})}$

------

__EQ~subs(r)~:__ $\frac{(t_1 = t_2)}{(r[t_1/z]) = r[t_2/z]}$

------



# Peano Arithmetic

> **Recall:** 
> An axiom is a formula that is assumed as a premise in any proof. An axiom schema is a set of axioms, defined by a pattern or rule.

Define a domain as $\N$, the natural numbers. We interpret the constant symbol $0$ as 0 and the unary function symbol $s$ as the successor function.

This defines a term for each number in $\N$ ($0, s(0), s(s(0))$, _etc_)

---

__PA 1:__ No number is a predecessor of $0$.
_Mathematically:_ $(\forall x \ (\neg (s(x) = 0)))$

---

__PA 2:__ No number has two predecessors.
_Mathematically_: $(\forall x \ (\forall y \ ((s(x) = s(y)) \rightarrow (x = y))))$

---

__PA 3:__ Any number when added to $0$ is itself.
_Mathematically_: $(\forall x \ ((x + 0) = x))$

---

__PA 4:__ Any number when added to a successor yields the successor of the sum.
_Mathematically_: $(\forall x \ (\forall y \ ((x + s(y)) = s((x + y)))))$

---

__PA 5:__ Any number when multipled by 0 yields 0.
_Mathematically_: $(\forall x \ ((x * 0) = 0))$

---

__PA 6:__ Multiplication of a successor.
_Mathematically_: $(\forall x \ (\forall y \ ((x * s(y)) = ((x * y) + x))))$

---

__PA 7:__ Induction. For any formula $\phi$ and variable $r$,
$(\phi[0/v] \rightarrow ((\forall v (\phi \rightarrow \phi[s(v)/v])) \rightarrow (\forall v \ \phi))$

---

> Note: PA stands for Peano Axioms.



==__Theorem (Gödel's Incompleteness Theorem):__ If Peano Axioms are consistent (that is, that they not derive a contradiction), then the proof system is incomplete.==

---

__Ex. Proof that addition is associative.__
We want to prove that $\emptyset \vdash_{PA} (\forall x \ (\forall y \ (\forall z \ (((x + y) + z) = (x + (y + z))))))$.
Let $A(x, y, z)$ to be the condition of associativity, which is $(((x + y) + z) = (x + (y + z))))$.
Choosing $\phi$ to be $A(x, y, z)$ yields the instance $A(x, y, 0) \rightarrow (\forall z \ (A(x, y, z) \rightarrow A(x, y, s(z))) \rightarrow (\forall z \ A(x, y, z)))$, which is what we need to prove.

_Base Case:_ We claim that $\emptyset \vdash_{PA} (((x + y) + 0) = (x + (y + 0)))$.

1. $(((x + y) + 0) = (x + y))$      _(PA3 + $\forall e$)_
2. $((y + 0) = y)$      _(PA3 + $\forall e$)_
3. $(((x + (y+ 0) = (x + y))$      _(EQ~subs~: 2 where $r$ is $(x + z) $)_
4. $(((x + y) + 0) = (x + (y + 0)))$      _(EQ~trans~: 1, 3)_

Thus, we have proven the base case.

_Inductive Hypothesis:_ We claim that $\emptyset \vdash_{PA} (\forall z \ (A(x, y, z) \rightarrow A(x, y, s(z))))$. We don't want to do this using induction bc that's crazy lmao, so we use predicate logic.

- 1. $z'$ _fresh_

  - 2. $(((x + y) + z') = (x + (y + z'))$ _(Assumption)_
    3. $(s((x + y) + z') = s(x + (y + z'))$ _(EQ~subs~: 2 where $r = s(z)$)_
    4. $(((x + y) + s(z')) = s((x + y) + z'))$   _(PA4 + $\forall e^2$)_ 
    5. $((x + s(y + z')) = s(x + (y + z'))$   _(PA4 + $\forall e^2$)_ 
    6. $((y + s(z')) = s((y + z')))$   _(PA4 + $\forall e^2$)_
    7. $((x + (y + s(z'))) = (x + s(y + z')))$  _(EQ~subs~: 6 where $r = (x + z)$_
    8. $A(x, y, s(z'))$  _(EQ~trans~: 4, 3, 5, 7)_

- 2. $A(x, y, z) \rightarrow A(x, y, s(z'))$   _($\rightarrow$-i 2-8)_

- $(\forall z \ (A(x, y, z) \rightarrow A(x, y, s(z))))$ _($\forall$-i 1-9)_

_Next, put the two proofs together as subproofs in a full proof._

_Look at Carmen's slides for the full proof of associativity._

---

