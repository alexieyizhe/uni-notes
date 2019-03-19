__CS 241__ | February 7, 2019

# Parsing

## Top Down Parsing

To parse top-down, we start with the starting state $S$ and keep matching derivations until we get to a word $w$.

We define some additional symbols $\vdash, \dashv$ to signify BOF and EOF, respectively. Accordingly, we also replace our start state with a new start state $S'$ with derivation $S' \rightarrow \vdash S \dashv$.

We follow the following algorithm to verify that a certain word $w$ is a valid word in the CFG:

1. Start with the start state $S'$ pushed onto a `stack`.
2. We pop the last element $\alpha$ of the `stack`. If the `stack` is empty, go to step 4.
   1. Find a production rule $\alpha \rightarrow \beta$ and push all symbols in $\beta$ in reverse order onto the `stack` (so the leftmost is at the top and is parsed next - if this was rightmost derivation, we would push in normal order)
   2. Otherwise, if there is no matching production rule, $\alpha  $ must be a terminal symbol for the word to be valid. So, we read in the next character we haven't read yet of the word $w$ in input, and check to see if it matches the symbol $\alpha$. 
      - If it _does not match,_ **reject** the word as it doesn't belong to the language.
      - Otherwise, continue parsing.
3. Repeat Step 2 with the new elements in the `stack` until the `stack` is empty.
4. Check if the next character we haven't read yet in the word $w$ in input is EOF $(\dashv)$.
   - If it is, then ==**accept**== the word.
   - If not, **reject** the word.

There's a problem!

In step $2.1$, we had to find a production rule that matched $\alpha$ as the $LHS$. However, there might be multiple production rules fitting that description, and if we want to avoid trying all combinations (brute force = bad), then we need to look ahead by one character and construct a **predictor table** to tell us which prod rule to use.

### Predictor Table & LL(1)

A **predictor table** is a lookup table that takes in a non-terminal symbol (the one on the `stack`) and a single character (the next character in input) - it outputs the rule that we should use.

> **Ex.** Assume that rows are elements of the set of non-terminal symbols and columns are the next character seen (elements of the set of terminal symbols $\Sigma'​$):
>
> ![image-20190305142452268](assets/image-20190305142452268.png)

Empty cells in the predictor table are always ERROR states. As well, each of the sets in a cell should have only one 'number' representing a certain rule for this to work. So, it's not guaranteed to remove all ambiguity from all CFGs.

> **Ex.** Consider a CFG with rules $\alpha \rightarrow abc$ and $\alpha \rightarrow adf$. It's not possible to know which rule to pick based on looking at a single character $a$.

We want to look only at those grammars for which this will work. These grammars are known as **LL(1)**.

==__A grammar is known as LL(1) _iff_ each cell of the predictor table contains at most one entry.__==

- First $L$ stands for scanning _left to right_
- Second $L$ stands for _leftmost_ derivations
- The $1$ means to look ahead _one_ symbol

Our end goal is to use this to create a `Predict(A, a)` function: a function that will give us the production rule(s) that apply when $A$ (a non-terminal symbol) is on top of the `stack`, and $a$ (a terminal symbol) is next in the input.

- We define a helper function `First(B)` that will give us a set of characters that can be the first letter of a derivation starting from $B$ (a symbol in the vocabulary).
  - To calculate `First(B)`, we look at each production rules where $B$ is the $LHS$, and keep processing until we get to a terminal or symbol that's not nullable, which is a symbol in `First(B)`. Then, do this for all other rules as well.
- Then, `Predict(A, a)` _should_ just give us the set of production rule(s) $A \rightarrow B$ where $a \in$ `First(B)` $(1)$

However, it's possible that $a$ did not come from a derivation of $A$, since it's possible that $A \Rightarrow^* \epsilon$ (a series of production rules turns $A$ into $\epsilon$) and $a$ is a part of a derivation of some other symbol after $A$. This is a problem, since the definition of `Predict` at $(1)$ will not match any rule that will help turn $A$ into $\epsilon$.

We need to define two more helper functions:

- `Nullable(A)` is true _iff_ $A \Rightarrow^* \epsilon $ where $A$ is a symbol in the vocabulary.
- `Follow(A)` is the set of characters that can come immediately after $A$ in a derivation. 
  - Formally: it is the set $ \{b \in \Sigma' : S' \Rightarrow^* \alpha Ab \beta, \ \ \alpha, \beta \in V^*\}$
  - To calculate, it's similar to `First`.

If `Nullable(A)` is false, then $A$ derives to be some symbol that's not $\epsilon$, so we care about that symbol and not the symbol in `Follow`. So, `Follow` only matters if `Nullable(A)` is true.

We can now create the correct definition of the predictor table:

==`Predict(A, a)` $= \{A \rightarrow \beta : a \in \text{First}(\beta)\} \cup \{A \rightarrow \beta : \beta \text{ is nullable and } a \in \text{Follow}(A)\}$.==

