__CS 245 |__ Midterm Study Guide

- ==Translating English to Well Formed Formulas==

- __Unique Readability Theorem:__ Every propositional WFF has a unique derivation as a well-formed formula.

  - Basically, you cannot write a formula two different ways, and each formula starts and ends with () or a prop variable

- __3 ways to prove equivalence:__

  - Truth tables
  - Valuation trees
  - Logical equivalence simplication

- **Parse trees**

- Definition of __Semantic Entailment__

- __Lemma__: $\{\wedge, \vee, \neg\}$ is an adequate set of connectives

- __Literals__ (propositional variable or the negation of one), __clauses__ (disjunction $\vee$ of literals), and __Conjunctive Normal Form__

  - For a formula to be in CNF:

    - The only connectives used are one of $\{ \neg, \vee, \wedge \}$
    - $\neg$ applies only to variables
    - $\vee$ applies only to sub-formulas where $\wedge$ doesn't occur
    - There is no need for duplicates

  - ### Converting to CNF

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

  - ==Converting formulas to CNF==

- Definition of __soundness__ and __completeness__

- __Resolution__

  - ### To prove a formula $\gamma$ from $\Sigma$:

    1. Negate $\gamma$ and move it to the set of premises.
       - this is the _only way_ you can use Resolution
    2. Convert all formulas to CNF
    3. Split CNF formulas into clauses
    4. Apply the _resolution inference rule_ until either
       - $\perp$ (the empty clause) results, showing that $\Sigma \vdash \gamma$ is a theorem
       - Exhaust all possibilities without finding a new rule or $\perp$ 

  - The only inference rule in Resolution is:
    $$\frac{(\alpha \vee p) \ \ \ ((\neg p) \vee \beta)}{(\alpha \vee \beta)}$$
    with 2 special cases:

    __Contradiction__: $\frac{p \ \ \ (\neg p)}{\perp}$

    __Unit Resolution__: $\frac{\alpha \vee p \ \ \ (\neg p)}{\alpha}$

  - Resolution is sound: every proof in Resolution is entailed.

  - Resolution is complete: every entailment has a proof in Resolution.

  - ==Understand proofs for soundness/completeness for Resolution==

  - ==Practice using Resolution==

- __Natural Deduction__ (propositional logic)

  - ==Understand proofs for soundness/completeness for ND==

- __Predicate Logic__

  - There are 7 types of symbols in Predicate Logic:

    | Symbol            | Example                                            |
    | ----------------- | -------------------------------------------------- |
    | Constant symbols  | $c, d, c_1, c_2$, etc                              |
    | Variables         | $x, y, z, x_1, y_2$                                |
    | Function symbols  | $f, g, h, f_1, g_2$                                |
    | Predicate symbols | $P, Q, P_1, Q_3$                                   |
    | Connectives       | $\neg, \wedge, \vee, \rightarrow, \leftrightarrow$ |
    | Quantifiers       | $\forall, \exists$                                 |
    | Punctuation       | $( $ or $   )$ or $,$                              |

  - __Domain__, __constants__, __variables__, __functions__, __predicates__, __relations__, __quantifiers__

    - __Bound/free__ variables
    - __Substitutions__

  - Expressions (**terms** and **formulas**)

  - An __interpretation__ $I$ for the set $L$ consists of:

    - A non-empty set $dom(I)$, aka $D^I$, aka $D$, called the __domain__ (or __universe__) of $I$
    - For each constant symbol $c$, some symbol $c^I$ that $\in D^I$
    - For each function symbol $f^{(i)}$, an $i$-ary function $f^I$
    - For each predicate symbol $P^{i}$, an $i$-ary predicate (relation) $P^I$

  - #### Meanings for Expressions

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
         - $T$ if $\alpha^{(I, E[x \mapsto d])} = T \ \forall d \in D^I$
         - $F$ otherwise
       - $(\exists x \ \alpha)^{(I, E)}$ is:
         - $T$ if $\alpha^{(I, E[x \mapsto d])} = T$ for some $ d \in D^I$
         - $F$ otherwise

  - Difference between **valid** and **satisfiable** and **unsatisfiable** formulas

    - **Valid** means every interpretation and environment satisfies the formula, **satisfiable** means some makes it true, unsatisfiable means nothing does

  - ==Make __parse trees__ for Predicate Logic==

  - ==Practice using Natural Deduction for Predicate Logic==
