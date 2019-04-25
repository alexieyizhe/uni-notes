

__CS 241 | __ Final Study Guide

### MIPS Conventions

- `$30` points to the word at the top of the stack

  - points to the word lower than the first free word
  - decrement by 4 to get the first free word in stack
    - at the start, use `sw $x, -4($30)` to store in the first free word, then `-8($30)`, etc
  - decremented as you use it towards start of memory, where your program is stored

- `$29` stores `$30 - 4` at the start

  - `0($29)` is the address on the stack of the first free word when the program starts
  - does not change throughout program execution, provides a set constant way to reference a specific variable in the program

- structure for code:

  - **prologue**

    - load 4 into `$4` and 1 into `$11`

    - `.import print` and store `print` into `$10`

    - `.import init` and call 

      ```
      .import init
      sw $31, -4($30)
      sub $30, $30, $4
      lis $5
      .word init
      jalr $5
      add $30, $30, $4
      lw $31, -4($30)
      ```

    - `.import new`, `.import delete`

    - store the return address on the stack

    - initialize frame pointer in `$29` to create a stack frame

    - store registers `$1` and `$2`

  - **body**

    - code 
    - remember to store local variables in stack frame

  - **epilogue**

    - pop the stack frame by incrementing `$30` by 4
    - restore previous variables like return adress, etc

> **Example**
>
> ```php
> // Translate the following code into MIPS shorthand:
> // 1)
> int wain(int a, int b) {
>   int c = 0;
>   return a + (b - c);
> }
> 
> code(a)
> push(3)
> code(b)
> push(3)
> code(c) // $3 contains c
> pop(5) // $5 contains b
> sub $3, $5, $3 // $3 contains b - c
> pop(5) // $5 contains a
> add $3, $5, $3 // $3 contains a + (b - c)
>   
> // 2)
> int wain(int a, int b) {
> 	int c = 0;
>   c = (a - b * a) + (b + a);
>   return c;
> }
> 
> code(a)
> push(3)
> code(b)
> push(3)
> code(a)
> pop(5) // $5 contains b
> mult $5, $3 
> mflo $3 // $3 contains b * a
> pop(5) // $5 contains a
> sub $3, $5, $3 // $3 = (a - b * a)
> push(3) 
> code(b)
> push(3)
> code(a)
> pop(5) // $5 contains b
> add $3, $5, $3 // $3 = b + a
> pop(5) // $5 contains (a - b * a)
> add $3, $5, $3 // $3 = (a - b * a) + (b + a)
> ```



### Questions 

- [ ] ==Converting from 2's complement to decimal, decimal to 2's complement==

  - [ ] decimal to 2's complement of number $n$:
    - encode as if it were $|n|$
    - **if $n$ negative:** flip the bits
    - **if $n$ negative:** add 1
  - 2's complement to decimal of number $n$
    - **if $n$ negative:** flip the bits
    - **if $n$ negative:** add 1
    - convert to decimal

- [ ] ==Writing MIPS programs==

  - simple commands

  - using procedures and `jalr`

  - recursive procedures

  - MIPS I/O

  - `$30` points to the word at the top of the stack

    - points to the word lower than the first free word
    - decrement by 4 to get the first free word in stack
      - at the start, use `sw $x, -4($30)` to store in the first free word, then `-8($30)`, etc
    - decremented as you use it towards start of memory, where your program is stored

  - `$29` stores `$30 - 4` at the start

    - `0($29)` is the address on the stack of the first free word when the program starts
    - does not change throughout program execution, provides a set constant way to reference a specific variable in the program

  - structure for code:

    - **prologue**

      - load 4 into `$4` and 1 into `$11`

      - `.import print` and store `print` into `$10`

      - `.import init` and call 

        ```
        .import init
        sw $31, -4($30)
        sub $30, $30, $4
        lis $5
        .word init
        jalr $5
        add $30, $30, $4
        lw $31, -4($30)
        ```

      - `.import new`, `.import delete`

      - store the return address on the stack

      - initialize frame pointer in `$29` to create a stack frame

      - store registers `$1` and `$2`

    - **body**

      - code 
      - remember to store local variables in stack frame

    - **epilogue**

      - pop the stack frame by incrementing `$30` by 4
      - restore previous variables like return adress, etc

  - calling functions:

    - **caller** always saves `$31`

    - if **caller save:**

      - ```
        // CALLER
        push($29)
        push($31)
          
        code(expr1) ; parameter 1
        push($3)
        code(expr2)
        push($3)
        ...
        code(exprN)
        push($3)     ; finished storing parameters
          
        lis $5
        .word FUNC_NAME
        jalr $5
          
        pop($5)
        ...
        pop($5)      ; pop N times
          
        pop($31)     ; restore other stuff
        pop($29)
        ```

        ```
        // CALLEE
        sub $29, $30, $4 ; create new stack frame, $29 points to first free word
        
        code(dcls) ; local declarations of variables
        
        push($x) ; here, we save the values in the registers 
        ...      ; that the callee is going to use so that 
        push($x) ; we can restore them after
        
        ;; BODY OF CODE
        code(stmts) ; function logic
        code(expr)  ; return value
        
        pop($x)  ; restore all the values in registers
        ...      ; that we used that were
        pop($x)  ; saved from the push($x)
        
        add $30, $29, $4 ; pop the stack frame
        jr $31 ; return to caller
        ```

    - if **callee save**:

      1. **caller** saves `$31`
      2. **caller** pushes arguments 

      3. **callee** saves `$29`
         - must be done before saving registers, since otherwise `0($29)` would point to some saved register
      4. **callee** pushes local arguments (declarations)
      5. **callee** save the registers it's going to use

- [ ] Bitwise operators

- [ ] Regular expressions

- [ ] Formal languages

  - Terms & definitions
  - different language classes & hierarchy (based on difficulty to parse)

- [ ] DFAs & NFAs

  - Formal definitions
  - ==**converting NFA to DFA**==
  - every DFA is an NFA
  - every NFA can be converted into a DFA
  - $\epsilon​$-NFAs
    - combining two NFAs
    - recognizing regular languages with $\epsilon$-NFAs
    - ==**converting into DFA**==
    - scanning a program into an  $\epsilon$-NFA

- [ ] Methods of scanning

  - Maximal munch, simplified MM

- [ ] Context Free Grammars (CFG)

  - formal definition
  - undecidability
  - how to augment to add an operator based on precedence
  - top down parsing
    - algorithm to parse top down
    - ==parse trees==
    - predictor tables
    - definition of LL(1)
      ![image-20190423113935577](assets/image-20190423113935577.png)
    - Converting a non-LL(1) to LL(1)
  - bottom up parsing
    - ==parse bottom up and build parse trees (lec 15)==
  - [ ] **LL(1) Parsing**
    - Nullable 
    - First & Follow sets
    - LL(1) predictor tables
    - Conflicts
    - Check if a grammar LL(1)
      ![image-20190423114510153](assets/image-20190423114510153.png)
    - ==Creating Nullable, First, Follow, Predict tables==
  - [ ] **LR(0) Parsing**
    - ==Constructing and Using LR(0) automaton==
    - Conflicts
    - ==Constructing SLR(1) parser==
    - ==Constructing LR(1) parser==
  - [ ] **Type Checking**
    - [ ] semantic vs syntax (parsing), scanning (lexical), runtime errors
      - everything in context-sensitive is semantic errors
        - type checking
        - declaration errors (multiple/missing declarations)
        - scoping
        - well-typed expressions
    - [ ] how to typecheck
      - symbol tables
      - signature tables
      - traversing parse trees

### DO

- [ ] Converting from NFA -> DFA

- [ ] Converting from $\epsilon$-NFA -> NFA -> DFA

- [ ] Building a DFA/NFA

- [ ] Make Leftmost/Rightmost derivation of a string given a CFG

- [ ] Finding ambiguity in a CFG

- [ ] LL(1) Parsing

  - [ ] Creating Nullable, First, Follow, Predict tables
  - [ ] **Parsing a string**

- [ ] LR(0) Parsing

  - [ ] **Constructing DFA**
  - [ ] **Parsing a string**

- [ ] Adding WLP4 features

- [ ] Error Analysis

  - [ ] Finding Errors (Syntax, Semantic, Scanning, Runtime)

- [ ] Loading & Linking 

  - link before you load

  - **ESR:** `.import WORD`
    - tells linker to replace any `WORD` with a placeholder and to put the correct address once it finds it
  - **ESD:** `.export WORD`
  - linking replaces external definitions with their proper addresses in other files
  - loading moves the references to addresses to the correct place
    - program assumes it starts at 0x0, but when you move it, it needs to be updated as well

- [ ] Optimizations

- [ ] Memory Allocation Methods 

  - [ ] First Fit
  - [ ] Best Fit
  - [ ] Binary Buddy
  - [ ] ==Final Review Q6.3==



### Review Session

1. **True or False**

   **a.** `False`, you can have multiple labels (multiple entries in symbol table) on a single line
   **b.** `False`, you can express up to $2^{k - 1} - 1$ 
   **c.** ==True==, NFA corresponds 1-1 to regular languages and regular languages are a subset of CF languages
   **d.** `False`, see above
   **e.** ==True==, if a language is regular it can be written as a DFA, to get the complement of the language just reverse the accepting states of the DFA (all accepting is now non-accepting, vice versa)

2. **CFGs**
   **a.** $A = \{0^n1^n : n \in \N\}$ (cannot be represented by a DFA)
   **b.** A grammar is ambiguous if there exists two distinct derivations for the same string (two parse trees with differing structures)
   **c.** Remember to use $\Rightarrow$ and NOT $\rightarrow$ between derivations

3. **Top Down Parsing**
   **a.** Left-to-right Left canonical derivation w/ 1 token lookahead.
   A grammar is not LL(1) if the Predict Table has 1+ cells with more than one entry

   **b.** `Predict(A, a)` = $\{A \rightarrow \beta : a \in First(\beta) \vee (Nullable(\beta) \wedge a \in Follow(A)) \}$

   Need to:

   1. Compute `First` for RHS of every rule

   2. Compute `Nullable` for RHS of every rule

   3. Compute `Follow` for LHS of evey non-terminal

      |      | BOF  | EOF  | a    | b    | c    | d    | e    |
      | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
      | $S'$ | 0    | -    | -    | -    | -    | -    | -    |
      | $S$  | -    | -    | 1    | -    | -    | 2    | -    |
      | $Y$  | -    | -    | -    | 4    | 3    | -    | -    |
      | $X$  | -    | -    | -    | -    | -    | 5    | -    |

4. **Bottom Up Parsing**

   Start with the $S'$ rule and the dot $\cdot $ at the start of the RHS

   - move dot over one and use the symbol you just moved over as the transition to a new state with the dot moved over one
   - if symbol $s$ after dot is non-terminal, you can be at the start of any rule (dot at start of RHS) where LHS is $s$
     - this can be applied recursively, so any of those rules that have the dot in front of it can also add more rules to this state
   - if the dot is at the end of the RHS of a rule, then we can reduce
   - **Shift-reduce conflict**: if the dot $\cdot$ is at the end of one rule and the middle or start of another in the same state
   - **Reduce-reduce**: if the dot $\cdot$ is at the end of two or more rules 

5. **Error Checking**

   - lexical/scanning means the scanner won't be able to accept it as a token (num out of bounds, no such token exists in language)
   - semantic error: meaning of the code is ambiguous, if its valid syntactically but we don't know what it would do
   - runtime: crash after compiling, infinite loop, depends on values or what happens after you run the program
   - syntax: scanner will accept it as valid tokens, but doesn't make sense for something to be in that position

   **a.** 

   **b.** lexical, since 12345678910 is out of range of a num token

   **c.** semantic, WLP4 says any duplicate IDs refer to local vars and not any procedures, so `foo` refers to the int

   **d.** runtime, dereferencing NULL, is valid and able to be scanned, but will crash at runtime

   **e.** semantic, the inner return will be caught since we parse bottom up

6. **Error Checking**
   - `.export wain` not defined [semantic]
   - `print:` follows a `.word` [syntax]
   - `jr $ 31` [scanning/lexical]
   - branch will cause `.word -1` to execute, but that will crash (`0xffffff` is not a valid instruction) [runtime]



1. **Compile** high level language to assembly code

   1. **Scan** code to get tokens
   2. **Parse** tokens to get a parse tree
   3. Analyze **semantics** to verify it's valid code
   4. **Generate** assembly code and output

2. **Assemble** the assembly code

   1. **Scan** into assembly tokens
   2. Check **syntax**

   3. Output machine code

3. **Link** the machine code

4. **Loading** the machine code to get a complete program

5. **Execute** the program