**CS 245 |** Sept 18, 2018



#  Proof Systems (cont.)
A formula in a proof can be an assumption, but anything you work with and conclusions you draw are limited to the scope of only that assumption.


# Natural Deduction
__Natural deduction__ is a proof system that allows us to:
  - _Make assumptions_ to start subproofs
    - Each assumption starts a subproof
    - Subproofs must all be closed by the end
    - Subproofs have their own scope
  - Use inference rules that resemble how we _reason naturally_
  - Prove a formula _directly_ instead of refuting the negation (_resolution_)
Like other proof systems, ND has soundness and completeness.

### Reflexivity
If a formula is in the proof already, it can be re-written - as long as it is in the same proof scope (not in a diff. subproof).


### Derived Rules
If we have the proof $\Tau \vdash \alpha$, then we can consider it as a derived rule ($\frac{\Tau}{\alpha}$).

Some __commonly known derived rules__:
  - Principle of _modus tollens_: $\{(p \rightarrow q, (\neg q))\} \vdash (\neg p)$
  - Proof by contradiction: $\Sigma, (\neg \alpha) \vdash \perp \ \ \Rightarrow \ \Sigma \vdash \alpha$
   - Law of Excluded Middle: $\emptyset \vdash (\alpha \vee (\neg \alpha))$
  - Double-Negation Introduction: $\Sigma \vdash \alpha \ \Rightarrow  \ \Sigma \vdash (\neg (\neg \alpha))$

### Alex's Amazing Collection of ND Rules
| Name | $\vdash notation$ | Inference Notation |
| - | - | - |
| Reflexivity  | $$\Sigma, \alpha \vdash \alpha$$ | $$\frac{\alpha}{\alpha}$$ |
| $\wedge$-introduction ($\wedge i$) | if $\Sigma \vdash \alpha$ and $\Sigma \vdash \beta$, then $\Sigma \vdash \alpha \wedge \beta$  | $$\frac{\alpha \ \ \ \ \beta}{\alpha \wedge \beta}$$ |
| $\wedge$-elimination ($\wedge e$)  | if $\Sigma \vdash \alpha \wedge \beta$, then $\Sigma \vdash \alpha$ and $\Sigma \vdash \beta$ | $$\frac{\alpha \ \wedge  \ \beta}{\alpha \ \ or \  \ \beta}$$ |
| $\vee$-introduction ($\vee i$) | if $\Sigma \vdash \alpha$, then $\Sigma \vdash \alpha \vee \beta$ and $\Sigma \vdash \beta \vee \alpha$ | $\frac{\alpha}{\alpha \vee \beta}$ or $\frac{\alpha}{\beta \vee \alpha}$ |
| $\vee$-elimination ($\vee e$)  | if $\Sigma, \alpha_1 \vdash \beta$ and $\Sigma, \alpha_2 \vdash \beta$, then $\Sigma, \alpha_1 \vee \alpha_2 \vdash \beta$ | $$\frac{\alpha_1 \vee \alpha_2 \ \ \ [\alpha_1 ... \beta] \ \ \ [\alpha_2 ... \beta]}{\beta}$$ |
| $\rightarrow$-introduction ($\rightarrow i$)  | if $\Sigma, \alpha \vdash \beta$, then $\Sigma \vdash \alpha \rightarrow \beta$ | $$\frac{[\alpha ... \beta]}{\alpha \rightarrow \beta}$$ |
| $\rightarrow$-elimination ($\rightarrow e$)  | if $\Sigma \vdash \alpha \rightarrow \beta$ and $\Sigma \vdash \alpha$, then $\Sigma \vdash \beta$  | $$\frac{\alpha \rightarrow \beta \ \ \ \alpha}{\beta}$$ |
| $\perp$-introduction ($\perp i$) | $\Sigma$, $\alpha$, $\neg \alpha \vdash \perp$  | $$\frac{\alpha \ \ \ \neg \alpha}{\perp}$$  |
| $\perp$-elimination ($\perp e$)  | if $\Sigma \vdash \perp$, then $\Sigma \vdash \alpha$  | $$\frac{\perp}{\alpha}$$ |
| $\neg$-introduction ($\neg i$)  | if $\Sigma, \alpha \vdash \perp$, then $\Sigma \perp \neg \alpha$  | $$\frac{[\alpha ... \perp]}{\neg \alpha}$$  |
| $\neg \neg$-elimination ($\neg \neg e$)  | if $\Sigma \perp \neg \neg \alpha$, then $\Sigma \perp \alpha$  | $$\frac{\neg \neg \alpha}{\alpha}$$  |
_where $[...]$ indicates a completed subproof._


### Tips 'n Tricks
  1. Start with premises at the top and conclusion at the bottom.
  2. If you can apply an elimination rule to premises, do so.
  3. Work backwards from the end.
  4. Treat a subproof as a full proof.
