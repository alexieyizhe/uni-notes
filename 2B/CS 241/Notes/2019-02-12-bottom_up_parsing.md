__CS 241 |__ Feb 12, 2019

# Bottom Up Parsing

Instead of going from a start state $S$ to a word $w$, we can try to go from $w$ to $S$. In our stack, we'll store partially reduced input that we've already read so far.

The invariant this time is `stack + unread input = `$\alpha_i$ (an intermediate step in the derivation).

As we process a word $w$, we can take one of two options at each step:

1. **Shift**: Take one character from the input. Push it onto the stack.
2. **Reduce**: The top $n$ characters on the stack are the RHS of some grammar rule. Pop the $n$ characters off the stack, and push the LHS of the same rule onto the stack.

When we finish processing a word $w$, we can only accept _iff_ the stack contains $S'$ and the unread input is $\epsilon$ (nothing left).

### LR Scanning

We don't always know when we should shift vs reduce. We can use the next character of input as a lookahead to help decide, but it doesn't solve the issue. There's a theorem, however:

==__Theorem: (Knuth)__==: The set $\{wa : \ \exists x \ s.t. \ S \Rightarrow ^* wax \}$ , where $w$ is the stack and $a$ is the next character, is a regular language.

This allows us to use a DFA to decide when to shift or reduce, a technique known as **LR parsing,** which stands for **left to right scanning** and **rightmost derivations**.

==**Definition**==: An **item** is a production with a dot $\cdot$ somewhere on the RHS of a rule. It's basically a _partially completed rule._

### Building LR(0)

The start state is a state labelled with the rule $S' \rightarrow \bullet \vdash S \dashv$.

For each rule in a state:

- Move the dot forward over one character $c$. This character $c$ defines the transition function (if $c$ is a symbol $x$, then the arrow leading away from the state in the DFA would be on $x$).
- The new state will contain the following transition rules:
  - the rule in the previous state, but with the dot moved over as above.
  - for every rule that has $\bullet A$ for some non-terminal $A$, add the rules with $A$ in the LHS to the state.
    - Note that this is also recursive (_ex._if this adds another rule that has $\bullet B$ for some non-terminal $B$, we have to add every rule that hs $B$ on the LHS to the state as well)
- Repeat for each rule in the new state. Combine duplicate states into one.



### Using LR(0) DFA

A state where the dot ($\bullet$) is at the end of a rule is a `reduce` state. For $LR(0)$, these states must contain only one rule, otherwise we run into a conflict. All other states are `shift` states.

1. Start in the start state with only the start state on the stack. 

2. In a state, read in the next character and follow the transition function corresponding to the character. 

   - If the transition exists, push the character and then the new state onto the stack. Repeat this step.

   - If there is no such transition, try reducing.

3. If you need to reduce, the current state should only have one rule, the rule with the dot $\bullet$ at the end of a rule.

   - Pop the characters on the RHS of the rule off the stack, and push the LHS of the rule onto the stack. Follow the transition corresponding to the LHS of the rule to a new state.

4. If $S'$ is on the stack and the input is empty, ==accept.== Reject otherwise.



### Issues

If a state has $A \rightarrow x \bullet$ and another rule like mentioned before, it will have a conflict. There are two types:

1. **Shift-reduce conflicts:** when a state has $A \rightarrow x \bullet$ and some rule $A \rightarrow \bullet y$.
2. **Reduce-reduce conflict**: when a state hsa $A\rightarrow x \bullet$ and some rule $A \rightarrow y \bullet$.

Either way, we don't know which rule to follow. The way we solve this is by simply defining that ==__a grammar is $LR(0$ _iff_ after creating the DFA, no state has one of the two conflicts above. __==

$LR(0)$ grammars conflict with right recursive languages.



### SLR(1) Parsers

To fix the conflicts mentioned above, we can lookahead by 1 character to see which rule we should follow.

For each rule $A \rightarrow x \bullet$, we attach $Follow(A)$ to it. This means that looking at the next character $c$, apply a rule $A \rightarrow x \bullet$ if $c \in Follow(A)$.

These are **Simple LR with 1 character lookahead parsers**, or SLR(1) parsers.









