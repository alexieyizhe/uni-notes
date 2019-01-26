__CS 241__ | January 24, 2019

# Formal Languages

There are many different types of languages, ranging from more low level (assembly) to more high level languages with helpful features (loops, objects, etc):

|              Assembly Language              |                     High-Level Languages                     |
| :-----------------------------------------: | :----------------------------------------------------------: |
|              Simple structure               |                         More complex                         |
| Recognition and translation into ML is easy | Harder to translate (1 keyword, like `for`, could be many ML instructions) |

We want a _formal theory of string recognition_ to handle complexities in a programming language, so that hardware or compilers will be able to parse source code as an entire giant string.

### Definitions

==**Alphabet:**== A finite set of symbols that appear in a language, denoted by $\Sigma$ (_ex. $\{a, b, c\}$_).

- Symbols can be anything (_ex. dots and dashes, English words, etc_).

==**String**== (also known as a **word**): A finite sequence of symbols from from an alphabet (_ex. $aaa, abc, ca, aca​$ _). 

- The **length** of a string $w$ is the number of symbols in $w$ and is denoted $|w|$.
- The **empty string** is an empty sequence of symbols, denoted by $\epsilon​$ (epsilon is NOT a symbol in any alphabet) where $|\epsilon| = 0​$. 

==**Language:**== A set of strings that are understood to be correctly interpreted (_ex. $\{a^{2n}b, n \geq 0\}$,_ but $\geq 0 \ n$ is not part of the math language).

- An **empty set** is denoted $\empty$ or $\{\}$. It is NOT the empty string. It's possible to have a language which is $\{\epsilon \}$, a language of 1 string.



The difficulty of recognizing "automatically" if a given string belongs to a given language _depends on how complex the language_ is. Generally, the more cases or different possibilities in the language, the _harder_ it is to do this. For example, **math syntax** or **MIPS** is relatively ==easy==, whereas modern languages like `C` or `Java` are `harder`. Some languages, like the halting problem, are impossible to recognize automatically.

##Language Classes

We classify languages according to _how hard the recognition process is._

####Finite Languages

Languages in this class have only a _finite_ number of strings.

**Verifying if a given string is valid** can be done through:

1. **Brute Force:** Store each valid string in memory. Compare given string with each stored string. `INEFFICIENT`
2. **Scanner:** Store valid words in a heap/tree where each node is a character and its children are following symbols in valid words. Traverse the tree going through nodes representing each symbol in the given string, until you reach a leaf or find the given string. ==BETTER==
   - This does not track the words we've seen, and we never go back through the input. 
   - Use this to **tokenize** an input. 



####Regular Languages

Languages in this class are built from:

-  **finite languages** 
- **unions**: ($L_1 \cup L_2 = \{x \ | \ x \in L_1 \text{ or } x \in L_2 \}$)
- **concatenations**: ($L_1 \cdot L_2 = \{xy \ | \ x \in L_1 \text{ and } y \in L_2 \}$)
- **repetitions**: Kleene $*$ ($L^*$ is the repetition of a language $L$)

> **Ex. Building a Regular Language**
>
> Let $L_1 = \{\text{dog, cat}\}, L_2 = \{\text{fish}, \epsilon\}$.
> $L_1 \cdot L_2 = \{ \text{dogfish, catfish, dog, cat}\}$
> $L_1^* = \{ \epsilon, \text{dog, cat, dogcat, catdog, dogdog, catcat, dogdogdog, catdogcat, etc...}\}​$

> **Ex. 2: Show that $S =\{a^{2n}b \ | \ n \geq 0\}$ is regular. **
>
> $S$ can be represented by $(a \cdot a)^* \cdot b$, so it falls into the class of regular languages. 
> It can also be represented by $\{\{a\} \cdot \{a\}\}^* \cdot \{b\}$ in set notation.

There are alternative formats of writing the elements in the set of a formal language, like **regular expressions**:

|     Regular Expression      |         Set Notation         |
| :-------------------------: | :--------------------------: |
|          $\empty$           |            $\{\}$            |
|         $ \epsilon$         |       $\{ \epsilon \}$       |
| $E_1 | E_2$ or $E_1 + E_2$  |        $L_1 \cup L_2$        |
| $E_1 \cdot E_2$ or $E_1E_2​$ | $L_1 \cdot L_2$ or $L_1 L_2$ |
|            $E^*$            |            $L_*$             |

To eliminate ambiguity but save us time when writing these expressions, we define **precedences:**

1. **$*$ before $\cdot$**       _ex. $aa^* \equiv a(a)^*$_
2. **$\cdot$ before $|$**        _ex. $aa |b \equiv (aa) | b$_

> **Ex. Is `C` regular?**
>
> A `C` program is a sequence of tokens, each of which comes from a regular language.
> There are a finite number of tokens. 
>
> So, $C \subseteq \{\text{valid C tokens} \}^*$, but is `C` regular? Maybe???



#### Other Languages

There are other classes that are increasingly hard to recognize automatically, including:

- Context-free
- Context-sensitive
- Recursive
- Recursively enumerable
- etc... (leading to impossibly `hard` to recognize)



#Deterministic Finite Automata (DFA)

Formally, a dFA is a 5-tuple $M = (\Sigma, Q, q_0, A, \delta)$:

- $\Sigma$ is a finite non-empty set representing the **alphabet.**
- $Q$ is a finite non-empty set representing the **states.**
- $q_0 \in Q$ is a **starting state**. 
- $A \subseteq Q$ is a set of **accepting states.**
- $\delta : (Q \times \Sigma) \rightarrow Q$ is the **[total] transition function** that tells us: given a state and a symbol of our alphabet, what state should we go do? 

<svg width="400" height="250" version="1.1" xmlns="http://www.w3.org/2000/svg">
	<ellipse stroke="black" stroke-width="1" fill="none" cx="153.5" cy="109.5" rx="30" ry="30"/>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="309.5" cy="74.5" rx="30" ry="30"/>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="282.5" cy="181.5" rx="30" ry="30"/>
	<ellipse stroke="black" stroke-width="1" fill="none" cx="282.5" cy="181.5" rx="24" ry="24"/>
	<path stroke="black" stroke-width="1" fill="none" d="M 179.352,94.327 A 215.761,215.761 0 0 1 279.644,71.826"/>
	<polygon fill="black" stroke-width="1" points="279.644,71.826 271.744,66.669 271.546,76.667"/>
	<text x="217.5" y="67.5" font-family="Times New Roman" font-size="20">a</text>
	<polygon stroke="black" stroke-width="1" points="179.696,124.121 256.304,166.879"/>
	<polygon fill="black" stroke-width="1" points="256.304,166.879 251.755,158.614 246.882,167.346"/>
	<text x="203.5" y="166.5" font-family="Times New Roman" font-size="20">b</text>
	<path stroke="black" stroke-width="1" fill="none" d="M 283.108,88.723 A 242.911,242.911 0 0 1 183.439,111.085"/>
	<polygon fill="black" stroke-width="1" points="183.439,111.085 191.483,116.014 191.394,106.014"/>
	<text x="236.5" y="126.5" font-family="Times New Roman" font-size="20">a</text>
	<polygon stroke="black" stroke-width="1" points="93.5,109.5 123.5,109.5"/>
	<polygon fill="black" stroke-width="1" points="123.5,109.5 115.5,104.5 115.5,114.5"/>
</svg>
_Created with http://madebyevan.com/fsm/_

The above is a DFA for $a^{2n}b, n \geq 0$, where there are an even positive number of occurrences of $a$ followed by a single occurrence of $b$.

