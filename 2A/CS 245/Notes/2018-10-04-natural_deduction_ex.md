**CS 245 |** Sept 18, 2018

# Hella Examples of Natural Deduction
> These examples are unfinished for now bc my $LaTeX$ skills are substandard for keeping up in class :sadface:


`Ex.` Show that $\{(p \rightarrow q)\} \vdash_{ND} ((r \vee p) \rightarrow (r \vee q))$.
  1. $(p \rightarrow q)$   _(from premise)_
  2. $p$ _(from $\wedge e \ 1$)_
  3. $q$ _(from $\wedge e \ 1$)_
  4. $(q \wedge p)$ _(from $\wedge i \ 2, 3$)_

__Reflexivity__:
`Ex.` Show that $\{p, q\} \vdash_{ND} p$.
  1. ?
  2. ?


__Conjunction__:
`Ex.` Show that $\{(p \wedge q)\} \vdash_{ND} (q \wedge p)$.
  1. $(p \wedge q)$   _(from premise)_
  2. $q$ _(from $\wedge e \ 1$)_
  3. $p$ _(from $\wedge e \ 1$)_
  4. $(q \wedge p)$ _(from $\wedge i \ 2, 3$)_

`Ex.` Show that $\{(p \wedge q), r\} \vdash_{ND} (q \wedge r)$.
  1. $(p \wedge q)$   _(from premise)_
  2. $r$   _(by premise)_
  3. $q$ _(from $\wedge e \ 1$)_
  4. $(q \wedge r)$ _(from $\wedge i \ 2, 3$)_


__Disjunction__:
`Ex.` Show that  $\{(p \vee q), (q \rightarrow r)\} \vdash_{ND} ((p \rightarrow q) \vee (q \rightarrow p))$.
  1. ??
  2. ?


__Implication__:
`Ex.` Show that  $\{(p \rightarrow q), (q \rightarrow r)\} \vdash_{ND} (p \rightarrow r)$.

`Ex.` Show that  $\empty \vdash_{ND} (p \rightarrow q)$.
  1. $p$ _(assumption)_
  2. $p$ _(reflexivity)_
  3. $(p \rightarrow p)$ _(by $\rightarrow i$ 1-2)_


__Contradiction__:
`Ex.` Show that  $\{\alpha, (\alpha \rightarrow (\neg \alpha))\} \vdash_{ND} \beta$.
  1. $\alpha$ _(premise)_
  2. $(\alpha \rightarrow (\neg \alpha))$ _(premise)_
  3. $(\neg \alpha)$ _(by $\rightarrow e$ 1,2)_
  4. $\perp$ _(by $\perp i$ 1,3)_
  5. $\beta$ _(by $\perp e$ 4)_


__Negation__:
`Ex.` Show that  $\{((\neg \alpha) \rightarrow (\neg (\neg \alpha)))\} \vdash_{ND} \alpha$.
  1. $((\neg \alpha) \rightarrow (\neg (\neg \alpha)))$ _(premise)_
  2. $(\neg \alpha)$ _(premise)_
  3. $(\neg (\neg \alpha))$ _($\rightarrow e$ 1, 2)_
  4. $(\alpha)$ _(by $\rightarrow e$ 1,2)_
  5. $\perp$ _(by $\perp i$ 1,3)_
  6. $(\neg (\neg \alpha))$ _(by $\neg i$ 2-5)_
  7. $\alpha$ _(by $\neg \neg e$ 6)_
