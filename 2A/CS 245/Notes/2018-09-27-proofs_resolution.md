**CS 245 |** Sept 27, 2018


# Proof Systems
A __proof__ is a formal demonstration that a statement is true.
 - Must be mechanically checkable
 - $\Sigma \vdash_s \gamma$ denotes "_there is a proof in the proof system $s$ with premises $\Sigma$ and conclusion $\gamma$_"

A proof contains, _in order_:
 - The premises, if any
 - Valid _inferences_ based on inference rules from preceding formulas
 - A conclusion as the final formula

There is a __set of inference rules__ which define a __proof system__.

An inference rule is written as:
$$ \frac{\alpha_1 \ \alpha_2 \ ... \  \alpha_i}{\beta}$$
which means that given formulas $\alpha_1, \alpha_2,...,\alpha_i$ (appeared previously in proof), you can infer $\beta$.

There are two desirable properties of proof systems: __soundness__ and __completeness__.

#### Soundness
A proof system $S$ is __sound__ if every proof in $S$ is also entailed.
If $\Sigma \vdash_S \gamma$, then $\Sigma \models \gamma$.
 - This allows us to show an argument does not have a proof in this system by showing that the conclusion is not entailed by the premises.

#### Completeness
A proof system $S$ is __complete__ if every entailment has a proof in $S$.
If $\Sigma \models \gamma$, then $\Sigma \vdash_S \gamma$.
- This allows us to show an argument has a proof in this system by showing that the conclusion is entailed by the premises.


# Resolution
__Resolution__ is a proof system that proves the negation of a formula is a contradiction.
 - It only applies to formulas in _CNF_
 - It only proves _contradictions_
 - It is _sound_ and _complete_ ([source](https://www.student.cs.uwaterloo.ca/~cs245/Instructor-Specific-Pages/SMcintyre/Lecture7.pdf))

To prove $\Sigma \vdash_{Res} \alpha$, use resolution with $\Sigma \ \cup \{\neg \alpha\} \vdash_{Res} \ \perp$.

The only inference rule in Resolution is:
$$\frac{(\alpha \vee p) \ \ \ ((\neg p) \vee \beta)}{(\alpha \vee \beta)}$$
with 2 special cases:

__Contradiction__: $\frac{p \ \ \ (\neg p)}{\perp}$

__Unit Resolution__: $\frac{\alpha \vee p \ \ \ (\neg p)}{\alpha}$

#### Steps To Using Resolution:
To prove a formula $\gamma$ from $\Sigma$:
 1. Negate $\gamma$ and move it to the set of premises.
    - this is the _only way_ you can use Resolution
 2. Convert all formulas to CNF
 3. Split CNF formulas into clauses
 4. Apply the _resolution inference rule_ until either
    - $\perp$ (the empty clause) results, showing that $\Sigma \vdash \gamma$ is a theorem
    - A new formula cannot be found using the rule, showing that it is not a theorem
