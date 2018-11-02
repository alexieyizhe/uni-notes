**CS 245 |** Sept 25, 2018


# Connectives
Connectives represent a function that __maps truth value(s) to a truth value__.
 - __Nullary connectives__ ignore their inputs and always evaluates to the same value
 - __Unary connectives__ depend on a single input
 - Generally, ___n_-ary connectives__ represent a function with _n_ inputs

Let $C$ be a set of connectives.
A connective is said to be __definable__ in terms of the connectives in $C$ if it can be expressed using _only_ the connectives in $C$.

> Essentially, we can make an equivalent formula using the connectives in $C$.

### Adequate Set of Connectives
Let $C$ be a set of connectives.
$C$ is defined to be __adequate__ _iff_ any _n_-ary connective can be defined in terms of the connectives in $C$.
> Essentially, a set is adequate if any formula can be re-written into an equivalent formula using only connectives in that set.

==__Lemma__: $\{\wedge, \vee, \neg\}$ is an adequate set of connectives.==

==__Theorem__: The set $\{\wedge, \vee \}$ is not adequate.==

 - Given an adequate set of connectives $C$ and asked to prove another set $C'$ is adequate, we need to show all connectives in $C$ can be represented using only connectives from $C'$
 - Given a set of connectives $C'$ and asked to show it is _not_ adequate, we need to find a connective that cannot be constructed from the connectives in $C'$

A set $C$ is __minimally adequate__ _iff_ both $C$ is adequate and every proper subset of $C$ is _not_ adequate.


# Conjunctive Normal Form (CNF)
A __literal__ is a propositional variable or the negation of it.
A __clause__ is a disjunction ($\vee$) of literals.
A formula is in __conjunctive normal form__ if it s a conjunction ($\wedge$) of clauses.

For a formula to be in CNF:
 - The only connectives used are one of $\{ \neg, \vee, \wedge \}$
 - $\neg$ applies only to variables
 - $\vee$ applies only to sub-formulas where $\wedge$ doesn't occur
 - There is no need for duplicates

> Essentially, a clause is a set of literals, and a CNF formula is a set of clauses.

### Converting to CNF
1. Replace occurrences of $\leftrightarrow$ and $\rightarrow$
   - $\alpha \rightarrow \beta$ becomes $\neg \alpha \vee \beta$
   - $\alpha \leftrightarrow \beta$ becomes $(\neg \alpha \vee \beta) \wedge (\alpha \vee \neg \beta)$
   - Should only have $\wedge$, $\vee$, and $\neg$ connectives left
2. Apply _De Morgan's Laws_ and _Double Negation_ until not possible
   - $\neg \alpha \vee \beta$ becomes $\neg \alpha \wedge \neg \beta$
   - $\neg \alpha \wedge \beta$ becomes $\neg \alpha \vee \neg \beta$
   - $\neg \neg \alpha$ becomes $\alpha$
   - Negations should now only be applied to variables
3. Use _distributivity_, _associativity_, _communitivity_ to turn into a conjunction of clauses
   - $\alpha \vee (\beta \wedge \gamma)$ becomes $(\alpha \vee \beta) \wedge (\alpha \vee \gamma)$
4. If asked, simplify as necessary using rest of identities
