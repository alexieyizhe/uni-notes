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

