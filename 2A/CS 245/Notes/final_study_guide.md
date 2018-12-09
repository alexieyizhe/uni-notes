__CS 245 |__ Final Study Guide

- ==Translating English to Well Formed Formulas==

- __Truth Valuation:__ A function with the set of all propsition symbols as domain and $\{F, T\}$ as the range.

- __Unique Readability Theorem:__ Every propositional WFF has a unique derivation as a well-formed formula.

  - Basically, you cannot write a formula two different ways, and each formula starts and ends with $(, $ $),$ or a prop variable 

- __3 ways to prove equivalence:__

  - Truth tables (final rows are same)
  - Valuation trees (leaves are same)
  - Logical equivalence simplication (becomes the same formula)

- Definition of __Semantic Entailment__

  - $\Sigma \models \alpha$, or $\Sigma$ entails $\alpha$, _iff_ for any truth valuation $t$, if $\Sigma^t = T$ then $\alpha^t = T$.
  - ==Show semantic entailment== by defining truth values for each variable so that all of it is true 

- __Lemma__: $\{\wedge, \vee, \neg\}$ is an adequate set of connectives

- __Literals__ (propositional variable or the negation of one), __clauses__ (disjunction $\vee$ of literals), and __Conjunctive Normal Form__

  - For a formula to be in CNF:
    - The only connectives used are one of $\{ \neg, \vee, \wedge \}$
    - $\neg$ applies only to variables
    - $\vee$ applies only to sub-formulas where $\wedge$ doesn't occur
    - There is no need for duplicates
  - ==Converting to CNF==
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

- Definition of __soundness__: a proof system $S$ is sound if every proof in $S$ is also entailed

  - If $\Sigma \vdash_S \phi$, then $\Sigma \models \phi$

  - > If you can write a proof for $\phi$ with $\Sigma$ as premises, then $\Sigma$ entails $\phi$.

- Definition of __completeness__: a proof system $S$ is complete if every entailment has a proof in $S$.

  - If $\Sigma \models \phi$, then $\Sigma \vdash_S \phi$

  - > If you can show that $\phi$ is entailed by $\Sigma$, then there is a proof for it in the system somehow.

- ==Proving a formula in __Resolution__==

  1. Negate $\gamma$ and move it to the set of premises.
     - this is the _only way_ you can use Resolution
  2. Convert all formulas in premises to CNF
  3. Split CNF formulas into clauses
  4. Apply the _resolution inference rule_ until either
     - $\perp$ (the empty clause) results, showing that $\Sigma \vdash \gamma$ is a theorem
     - Exhaust all possibilities without finding a new rule or $\perp$ 

  - The only inference rule in Resolution is:
    $$\frac{(\alpha \vee p) \ \ \ ((\neg p) \vee \beta)}{(\alpha \vee \beta)}$$
    with 2 special cases:

    __Contradiction__: $\frac{p \ \ \ (\neg p)}{\perp}$

    __Unit Resolution__: $\frac{\alpha \vee p \ \ \ (\neg p)}{\alpha}$

  - ==Understand proofs for soundness/completeness for Resolution==

  - ==Practice using Resolution==

- __Natural Deduction__ (propositional logic)

  - ==Understand proofs for soundness/completeness for ND==
  - ==Practice Natural Deduction==

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

  - __Bound/free__ variables

  - __Substitutions__

  - Expressions (**terms** and **formulas**)

    - Terms are:
      - constant symbols
      - variables
      - function symbols
    - Formulas are:
      - predicate symbols
      - if $\alpha$ is a formula, so is $(\neg  \alpha)$
      - if $\alpha, \beta$  are formulas, so is $(\alpha * \beta)$
      - if $\alpha$ is a formula, $x$ is a variable, then $\forall, \exists $ of those are formulas

  - An __interpretation__ $I$ for the set $L$ consists of:

    - A non-empty set $dom(I)$, aka $D^I$, aka $D$, called the __domain__ (or __universe__) of $I$
    - For each constant symbol $c$, some symbol $c^I$ that $\in D^I$
    - For each function symbol $f^{(i)}$, an $i$-ary function $f^I$
    - For each predicate symbol $P^{i}$, an $i$-ary predicate (relation) $P^I$
    - ==Practice finding interpretations==

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

    - **Valid** means every interpretation and environment satisfies the formula, **satisfiable** means some makes it true, **unsatisfiable** means nothing does
    - An interpretation $I$ and environment $E$ satisfy a formula $\alpha$, denoted $I \models_E \alpha$, if $\alpha^{(I, E)} = T$.

  - ==Definition of entailment for predicate logic==

    - use interpretations and environments paired together

  - ==Make __parse trees__ for Predicate Logic==

  - ==Practice using Natural Deduction for Predicate Logic==

- **Parse trees**

  - binary connectives: two subtrees
  - $\neg, \forall x, \exists y$: one subtree
  - variables: own node 
  - function $f$: node labelled $f$, subtree for each term in function
  - predicate $P$: node labelled $P$, subtree for each term in predicate

- ==Proving total correctness==

  - Use inference rules or implied to go from precondition to postcondition to prove **partial correctness** 
  - Prove **termination** using a variant: a template is..
    - Choose the variant $X$ (usually a variable or something similar).
      At the start of the loop, $\text{some condition involving } X$.
      Each time through the loop, $X$ does something to get closer to base case.
      So, the value of $X$ will eventually reach _some base case._
      When $X$ reaches base case, the guard will catch it and exit the loop.
      Thus, the program terminates.

- Program verification: Arrays

  - $A\{i \leftarrow e\}[j] = e$ if $j = i$, $A[j]$ if $j \not= i$

- A **decision problem** is a problem which has a yes or no answer on a given input. A decision problem is **decidable** _iff_ there exists an algorithm that decides it. Otherwise, that problem is **undecidable**.

- The Halting Problem

  - Given a program $P$ and an input $I$, determine if $P$ halts on input I
  - This is **undecidable**

- Reduction of problems: to prove that a problem $P$ is undecidable

  - Assume towards a contradiction that there is an algorithm $B$ that decides a new problem $P_0$ 
  - Show that we can create a new algorithm $A$ such that it decides the Halting Problem.
  - Conclude that $B$ should not have existed since the Halting Problem is undecidable and hence $P_0$ is undecidable. 

- Diagonalization: create a bijection between $\N$ and the set of all programs

  - Create a table with all inputs as columns and all programs as rows:
  - ![image-20181206175335454](/Users/alexieyizhe/Google Drive/University/2A/CS 245/Notes/final_study_guide.assets/image-20181206175335454-4136815.png)
  - By negating every entry on the diagonal and making it into a row, you can create a new row, since the diagonal is different from every row (it's different from every other program). The row is the program that loops if the input program halts, and halts if the other program does not halt (it loops).
    If you run this program with itself, it will either halt or loop forever. If it halts, then the input program (itself) must loop, so its a contradiction, but if it halts, then the input program (itself) must halt, which is also a contradiction! So this program cannot exist, and the problem it solves (the Halting Problem) is unsolvable.