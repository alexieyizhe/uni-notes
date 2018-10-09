**CS 245 |** Sept 20, 2018

# Structural Induction

__Structural induction__ is pretty much regular induction, but operating on more than just the set of natural numbers ($\N$).

Tips for writing a proof by structural induction:
 - Identify which cases are base cases and which are inductive cases
 - Give a name for the property you want to prove
 - Prove!

# Truth Valuations
A __truth valuation__ is a function that maps propositional variables to the set $\{T, F\}$.
 - denoted $\alpha^t$ or $t(\alpha)$
 - the truth valuation for the __empty set__ is always true ($\emptyset^t = T$ always)

> Prop. variables have __no meaning__ until assigned a value by the truth valuation.

### Tautologies, Satisfactions, & Contradictions

A formula $\alpha$ is a:
 - __tautology__ _iff_ for every truth valuation $t$, $\alpha^t = T$
 - __contradiction__ _iff_ for every truth valuation $t$, $\alpha^t = F$
 - __satisfiable__ _iff_ for every truth valuation $t$, $\alpha^t = T$

### Equivalence
The formulas $\alpha$ and $\beta$ are __equivalent__ if they have the same truth value under any valuation.
 - _i.e._ $\alpha^t = \beta^t$ for all valuations $t$

### Semantic Entailment
Let $\Sigma$ be a set of formulas, and let $\alpha$ be a formula.
$\Sigma$ __entails__ $\alpha$ (denoted $\Sigma \models \alpha$) _iff_ for any truth valuation $t$, if $\Sigma^t = T$ then also $\alpha^t = T$.
 - If $\emptyset \models \alpha$, then $\alpha$ is a tautology.

_Lemma_: $\alpha \equiv \beta$ _iff_ $\{\alpha\} \models \beta \wedge \{\beta\} \models \alpha$.
> This lemma is an alternative way to express equivalence.
