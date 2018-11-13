**CS 245 |** Oct 11, 2018

# Predicate Logic

Propositional logic is not expressive enough. We want to be able to talk about __objects__ in a set instead of everything, and possibly about _some_ object, not _all_ objects.

---

__Ex.__ Think about the statements below:

Not all birds can fly. (_generalizing patterns_) 
Every bear likes honey. (_generalizing patterns_)
Alice is married to Jay and Alice is not married to Leon. (_relationships among individuals_)

These are difficult to express using propositional logic.

---

A __domain__ is a non-empty set of objects. It's the world that our statement lives in, since _the same statement can have different truth values in different domains_. 

## Syntax

There are 7 types of symbols in Predicate Logic:

| Symbol            | Example                                            |
| ----------------- | -------------------------------------------------- |
| Constant symbols  | $c, d, c_1, c_2$, etc                              |
| Variables         | $x, y, z, x_1, y_2$                                |
| Function symbols  | $f, g, h, f_1, g_2$                                |
| Predicate symbols | $P, Q, P_1, Q_3$                                   |
| Connectives       | $\neg, \wedge, \vee, \rightarrow, \leftrightarrow$ |
| Quantifiers       | $\forall, \exists$                                 |
| Punctuation       | $( $ or $   )$ or $,$                              |

A __constant__ is a concrete (specific) object in the domain.

A __variable__ is a placeholder for constants. It lets us refer to the idea of an object without specifying a particular specific object.

A __function__ is just a symbol $f$ for now. A function that has arity $n$ (requires $n$ arguments) is denoted $f^{(n)}$. 

> Later, we'll attach meaning so a function behaves like mathematical functions, mapping $n$ copies of the domain into the domain:
> $$f : D^n \rightarrow D$$

A __predicate__ represents a property that an individual, or collection of individuals, may or may not have. In symbolic logic, we write $M(x)$ to represent $x$ has a specific property. Mathematically, we represent a predicate by the set of all things that have the property (if $S$ is the set of all students, then $x \in S$ means $x$ is a student). A predicate must be a _subset of the domain_.

A __relation__ is a $k$-ary predicate, or a set of $k$-tuples of domain elements. It _relates_ one domain element to another (or many others, if $k \gt 2$).

A __quantifier__ is used to express how many objects in the domain the statement is true for. 

- $\forall$ is the __universal quantifier__: the statement is true for _every_ object in the domain.
- $\exists$ is the __existential quantifier__: the statement is true for some _(one or more)_ object in the domain.

#### Parse Trees

For the newly introduced elements, their rule in a parse tree is as follows:

- Quantifiers ($\forall x, \exists x$) are grouped in one node, like negation (only 1 sub-tree)
- A predicate symbol $P(t_1, ..., t_i)$ or a function symbol $f(t_1, ..., t_i)$ has a node labelled $P$ or $f$ respectively, and a sub-tree for each of the terms $t_1, ..., t_i$ 



### Expressions 

In Predicate Logic, we need to consider _two types of expressions:_

1. __Terms__: those that refer to an object of the domain.
   _Defined recursively as follows:_
   1. Each _constant_ symbol is a term and each _variable_ is a term. These are called __atomic terms__.
   2. If $t_1, ..., t_n$ are terms and $f$ is a _function_ of arity $n$, then $f(t_1, ..., t_n)$ is a term.
   3. _Nothing_ else is a term.
2. __Formulas__: those that can have a truth value - also known as well-formed formulas (WFFs).
   _Defined recursively as follows:_
   1. An expression of the form $P(t_1, ..., t_n)$ where $P$ is an $n$-ary predicate symbol and each $t_i$ is a term, is a WFF. These are called __atomic formulas__.
   2. If $\alpha$ is a WFF, then $(\neg \alpha)$ is a WFF.
   3. If $\alpha, \beta$ are WFFs and $*$ is a binary connective symbol, then $(\alpha * \beta)$ is a WFF.
   4. If $\alpha$ is a WFF and $x$ is a variable, then $(\forall x \ \alpha)$ and $(\exists x \ \alpha)$ are both WFFs.
   5. _Nothing_ else is a WFF.



### Variables

For a WFF $(\exists x \ \alpha)$, $\alpha$ is the __scope__ of the quantifier. Inside $\alpha$, the variable $x$ is __bound__ by the quantifier since _it lies in the scope of the quantifier._ Otherwise, the occurrence of the variable is __free__.

- If there are multiple occurrences of a variable, each occurrence needs to be considered separately
- The variable immediately after $\exists$ (like in $\exists x$) is _neither free nor bound_

> This quantifier will keep this scope even if it's part of a larger formula.

A formula with _no free variables_ is called a __closed formula__, or a __sentence__.

The formal definition of a _free_ variable in a formula $\alpha$ is _iff_ it is a member of the set $FV(\alpha)$ defined as:

1.  If $\alpha$ is $P(t_1, ..., t_k)$, then $FV(\alpha) = \{x | x$ appears in some $t_i\}$
2. If $\alpha$ is $(\neg \beta)$, then $FV(\alpha) = FV(\beta)$
3. If $\alpha$ is $(\beta * \gamma)$, then $FV(\alpha) = FV(\beta) \ \cup \ FV(\gamma)$
4. If $\alpha$ is $(?x \ \beta)$ for $? \in \{\forall, \exists\}$, then $FV(\alpha) = FV(\beta) - \{x\}$

> Basically, any quantifier describing $x$ means $x$ inside the formula of that quantifier is bound, and if there's no outer quantifier describing $x$, then $x$ is free!

#### Substitution

We use __substitution__ to replace a variable in a formula with a specific term. 

For a variable $x$, a term $t$, and a formula $\alpha$, $\alpha[t/x]$ denotes the resulting formula by replacing each _free_ occurrence of $x$ in $\alpha$ with $t$.

> IMPORTANT: Note that _substitution does not replace any bound occurrences of the variable - it cannot affect the bounding of the formula._

The formal definition of a substitution where $x$ is a variable and $t$ is a term is as follows:

1. If $\alpha$ is $P(t_1, ..., t_k)$, then $\alpha[t/x]$ is $P(t_1[t/x], ..., t_k[t/x])$
2. If $\alpha$ is $(\neg \beta)$, then $\alpha[t/x]$ is $(\neg \beta[t/x])$
3. If $\alpha$ is $(\beta * \gamma)$, then $\alpha[t/x]$ is $(\beta[t/x] * \gamma[t/x])$
4. If $\alpha$ is $(?x \ \beta)$ for $? \in \{\forall, \exists\}$, then $\alpha[t/x]$ is $\alpha$  _(every occurrence of $x$ is bound, so no substitution occurs)_
5. If $\alpha$ is $(?y \ \beta)$ for $? \in \{\forall, \exists\}$ and some other variable $y$, then:
   1. If $y$ does not occur in $t$, then $\alpha[t/x]$ is $(?y \ \beta[t/x])$
   2. If $y$ does occur in $t$, then select a variable $z$ that does not occur in $\alpha$ and $t$, and then $\alpha[t/x]$ is $(?z (\beta[z/y])[t/x])$ _(this prevents the new variable introduced as part of the substitution from being captured by an existing unrelated quantifier of that variable, if both have the same variable name)_



However, keep in mind _syntax_ is just a bunch of symbols that don't have meaning - to obtain meaning, we need to look at the Semantics of Predicate Logic.



