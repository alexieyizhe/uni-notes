__CS 245 |__ Oct 16, 2018



# Predicate Logic (cont.)

## Semantics

A language for our formulas is a set $L$ of constant symbols, function symbols, variable symbols, and predicate symbols.

An __interpretation__ $I$ for the set $L$ consists of:

- A non-empty set $dom(I)$, aka $D^I$, aka $D$, called the __domain__ (or __universe__) of $I$
- For each constant symbol $c$, some symbol $c^I$ that $\in D^I$
- For each function symbol $f^{(i)}$, an $i$-ary function $f^I$
- For each predicate symbol $P^{i}$, an $i$-ary predicate (relation) $P^I$

------

__Ex.__ Creating an interpretation.
Consider $f$ an unary function and $0$ a constant. If we have an interpretation $I$ with domain $\N$ and $0^I$ being the usual 0 and $f^I$ being the usual successor function (increment by 1), then:

$f(0)^I = f^I(0^I) = 1$

> Note that $0$ was a constant symbol, and so we still had to specify that the interpretation of $0$ in $I$ is 0 - it's not a value, it's a constant symbol that has no meaning until we assign it one under an interpretation!
>
> If we specify $0^I$ to be 1 instead, then under the same interpretation, $f(0)^I = f^I(0^I) = 2$, which is different. 
>
> _don't do this it's weird and confusing and kinda dumb_
>
> This is misleading, and we can avoid this issue by not using symbols that could be misinterpreted (_i.e. using $0$ to represent anything other than 0_).

------

A __total function__ is a function that has arity $k$ and satisfies $f^I : D^k \rightarrow D$ where every $k$-tuple from the domain must map into the domain. 

A first-order __environment__ is a function that assigns a value in the domain to _every_ variable symbol in the language.
For any environment $E$ and domain element $d$, the environment "$E$ with $x$ __reassigned__ to $d$", denoted $E[x \mapsto b]$, is defined as:

1. $E[x \mapsto b](y) = d$, if $y$ is $x$
2. $E[x \mapsto b](y) = E(y)$, if $y$ is not $x$

> $E[x \mapsto b]$ is just another environment!

> Basically, this means a variable $x$ will become the domain element $d$ ($d$ doesn't have to be another variable, could be another type of symbol) in the environment $E[x \mapsto b]$, and nothing changes otherwise.

#### Meanings for Expressions

Pairing an interpretation $I$ together with an environment $E$ allows us to define a value for every expression:

1. For a _term_ $t$, it is defined recursively:
   - If $t$ is a constant $c$, the value $t^{(I, E)} = c^I$
   - If $t$ is a variable $x$, the value $t^{(I, E)} = x^E$
   - If $t$ is $f(t_1, ..., t_n)$, the value $t^{(I, E)} = f^I (t_1^{(I, E)}, ..., t_n^{(I, E)})$
2. For a _formula_ $\alpha$, it is defined recursively:
   - If $\alpha = P(t_1, ..., t_n)$, then $\alpha^I$ is:
     - $T$ if $t_1^I, ..., t_n^I \in P^I$
     - $F$ otherwise
   - If $\alpha = (\neg \beta)$ or $\alpha = (\beta * \gamma)$ for some binary connective $*$, then $\alpha^I $ is determined by $\beta^I, \gamma^I$ in the same way as propositional logic
   - $(\forall x \ \alpha)^{(I, E)}$ is:
     -  $T$ if $\alpha^{(I, E[x \mapsto d])} = T \ \forall d \in D^I$
     - $F$ otherwise
   - $(\exists x \ \alpha)^{(I, E)}$ is:
     -  $T$ if $\alpha^{(I, E[x \mapsto d])} = T$ for some $ d \in D^I$
     - $F$ otherwise

> Note that formulas only map to $\{T, F\}$, compared to terms that map to values in the domain of $I$.

------

__Examples of Meanings__

1. __Terms:__ Suppose a language has constant symbol $0$, a unary function $s$, and a binary function $+$. Define a term $s((s(0) + s(x))$, $D^I = \N$, $0^I$ = 0, $E(x) = 3$, $s^I$ to be the successor function, and $+^I$ to be the addition operation. Then:
   $$(s((s(0) + s(x))))^{(I, E)} = 6$$
2. __Functions:__ Let $D^I = \{a, b\}$, $P^I = \{(a, a), (a, b), (b, b)\}$, $E(x) = a$, and $E(y) = b$. Then:
   - $P(x, x)^{(I, E)} = T$, since $(E(x), E(x)) = (a, a) \in P^I$
   - $(\exists y \ P(y, x))^{(I, E)} = T$, since $P(y, x)^{(I, E[y \mapsto a])} = T$
   - $(\forall x \ P(y, x))^{(I, E)} = F $, since $P(y, x)^{(I, E[x \mapsto a])} = F $ (because of $(b, b)$) and $P(y, x)^{(I, E[x \mapsto b])} = T$ 

------

#### Validity and Satisfiability

An interpretation $I$ and environment $E$ __satisfy__ a formula $\alpha$ if $\alpha^{(I, E)} = T$. This is denoted $I \models_E \alpha$.
An interpretation $I$ satisfies a formula $\alpha$ if $I \models_E \alpha$ for every $E$. This is denoted $I \models \alpha$.

| $\alpha$ is...               | Condition such that $I \models_E \alpha$                     |
| ---------------------------- | ------------------------------------------------------------ |
| $P(t_1, ..., t_k)$           | $(t_1^{(I, E)}, ..., t_k^{(I, E)}) \in P^I$                  |
| $(\neg \beta)$               | $I \not\models_E \beta$                                      |
| $(\beta \wedge \gamma)$      | Both $I \models_E \beta$ and $I \models_E \gamma$            |
| $(\beta \vee \gamma)$        | Either $I \models_E \beta$ or $I \models_E \gamma$ or both   |
| $(\beta \rightarrow \gamma)$ | Either $I \not\models_E \beta$ or $I \models_E \gamma$ or both |
| $(\forall x \ \beta)$        | For every $a \in D^I$, $I \models_{E[x \mapsto a]} \beta$    |
| $(\exists x \ \beta)$        | For some $a \in D^I$, $I \models_{E[x \mapsto a]} \beta$     |

A formula $\alpha$ is:

1. __valid__ if every interpretation and environment satisfies $\alpha$ (_i.e._ $\forall I, E, \ \ I \models_E \alpha$ )
2. __satisfiable__ if some interpretation and environment satisfy $\alpha$ (_i.e._ $\exists I, E, \ \ I \models_E \alpha$ )
3. __unsatisfiable__ if no interperation and environment satisfy $\alpha$ (_i.e._ $\forall I, E, \ \ I \not\models_E \alpha$ )

==__Relevance Lemma:__ Let $\alpha$ be a first-order formula, $I$ be an interpretation, and $E_1, E_2$ be two environments such that $E_1(x) = E_2(x)$ for every $x$ that occurs free in $\alpha$.==

==Then, $I \models_{E_1} \alpha $ _iff_  $I \models_{E_2} \alpha$ _(prove by using induction on the structure of $\alpha$)_==

----

__Examples of Validity/Satisfiability__

1. 

---

#### Semantic Entailment

Let $\Sigma$ be a set of well-formed Predicate Logic formulas and $\alpha$ be a well-formed Predicate Logic formula.

For an interpretation $I$ and environment $E$, we write $I \models_E \Sigma$ _iff_ $\forall \phi \in \Sigma, I \models_E \phi$. 

We say that $\Sigma$ __semantically entails__ $\alpha$ (or that $\alpha$ is a __logical consequence__ of $\Sigma$), written as $\Sigma \models \alpha$, _iff_ for any interpretation $I$ and environment $E$, we have $I \models_E \Sigma \ \rightarrow \ I \models_E \alpha$. This is also denoted $\alpha^{(I, E)} = T$.

> $\emptyset \models \alpha$ means that $\alpha$ is valid.

---

__Examples of Semantic Entailment__

1. 