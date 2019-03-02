__CS 241__ | February 5, 2019

# Scanning

### Maximal Munch Algorithm

Run DFA (without $\epsilon$-moves) until no non-error move (transition) is available.

1. If in an accepting state, output the found token.

2. Otherwise, if not in an acceptable state (since the next move is an error):

   -  Revert back to the most recent accepting state and output token at that state. This requires the use of a variable to keep track of that state/token.

   - Resume from there.

3. $\epsilon$- move back to the start state.

**Caveats:** However, this can cause a lot of confusion if there is ambiguous input. For example, `a+++b` could be:

1. `a++ + b`
2. `a + ++b`

yet this will always choose option 1. So, if a programmer is unaware of the choices that the tokenizer makes and intends for the code to work like option 2, it can be _extremely hard to spot errors in code._

Maybe it's better to just error if there's ambiguity. So, we look at a more simplified version.

### Simplified Maximal Munch

This is the same as MM above, but if not in an accepting state when no transitions are available, produce an `ERROR`. This algorithm does not keep track of the last accepting state since it does not need it.

In practice, this algorithm is good enough, and most languages implement scanning through this method. 

> **Ex.** Prior versions of `C++` would not accept `vector<pair<string, int>>` since it would interpret `>>` as the right bitshift operator instead of closing brackets (you would need `> >` for it to be valid).



# Context Free Grammar

Consider the alphabet of parentheses and a language where all strings are balanced parentheses. Our DFA would be an increasing amount of states, where increasing by 1 state would let us recognize one more level of nested parentheses. This is not a DFA, as we would need an infinite number of states since any number of levels of nested parentheses is possible.

So, we move to **Context-Free Languages.** These are languages that _can be described by a Context-Free grammar._

For the problem above:
$$
S \rightarrow \epsilon \\
S \rightarrow ( \ S \ ) \\
S \rightarrow SS
$$

### Formal Definition

==A **context-free grammar (CFG)** is a 4 tuple  $ (N, \Sigma, P, S)$:==

- $N$ is a finite non-empty set of **non-terminal** symbols
- $\Sigma$ is a finite non-empty set of **terminal symbols** representing the **alphabet.**
- $P$ is a finite set of productions, each of the form $A \rightarrow \beta$ where $A \in N$ and $\beta \in (N \cup \Sigma)^*$
  - $A$ is a non-terminal symbol, $B$ is either another non-teminal or a terminal symbol
  - terminal symbols are terminal, they cannot be transformed into another symbol
  - The **vocabulary** of a CFG is $V = N \cup \Sigma$, the set of all symbols (terminal _and_ non-terminal) in the language.
- $S \in N$ is a starting symbol

The **language** of a grammar $G$ is $L(G) = \{w \in \Sigma^* : S \Rightarrow ^* w\}$.

==A language is context free _iff_ there exists a CFG such that $L = L(G)$.==

You can choose to start expanding (deriving) from the left or the right, known as **left derivations** and **right derivations**, respectively.

You can also draw **parse trees** for CFGs, which are multi-way trees where each edge represents a part of a derivation and the leaf nodes are the final word made up of only terminal symbols.

![image-20190305121649087](assets/image-20190305121649087.png)

Sometimes, a language can be **ambiguous** if there is more than one distinct derivation (leftmost or rightmost) or parse tree for a word. You can force a language to be unambiguous by either defining something like wrapping everything in brackets, or by forcing left/right associative rules:

|                       Left Associative                       |                      Right Associative                       |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![image-20190305122501628](assets/image-20190305122501628.png) | ![image-20190305122455175](assets/image-20190305122455175.png) |



### Undecidability

There are a few things that are undecidable about CFGs:

- Writing a program to determine if a grammar is ambiguous or not
- Whether or not given two different CFGs $G_1, G_2$, that $L(G_1) = L(G_2)$
- Whether $L(G_1) \cap L(G_2) = \empty$ 