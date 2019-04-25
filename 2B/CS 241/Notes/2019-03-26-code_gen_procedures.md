__CS 241 |__ March 26, 2019

# Code Generation: Procedures

We had to do a number of things in the prologue/epilogue for `wain`, but how does this change for any other generic procedure?

- Don't need any imports
- Must update `$29` to create a new stack frame
- Must save registers that we're using
- Must restore registers and stack (at end)
- Must `jr $31` (at end)

### Caller vs. Callee

There are responsibilities that the **caller** (a function that calls another function) has to cover and there are some that the **callee** (the function that's called by the other function) must perform.

- Caller must save `$31`, otherwise return address is lost once we `jalr` to the callee

- Callee must save registers that it's using (makes sense, since only the callee knows which registers it's going to use)

- No one has to save `$30`, since it's always up to date

- Someone must save `$29`

  - If **Callee** saves `$29`:

    - It needs to create the stack frame by `sub $29, $30, $4` before it saves the registers it's going to use
      - If it saves registers first, you will have to keep track of how many registers have been saved since `$29` has to point to the start of the stack frame and saving registers modifies `$30`
    - Also needs to save the previous value of `$29` before creating the new stack frame
      - Otherwise, when returning to the caller after execution, the caller will not be able to use `$29`
    - So, `push($29)`and then `add $29, $30, $0`
      - `$29` now points to 1 word above bottom of stack frame, which is the first free word (first word in stack frame is `$29`)

  - If **Caller** saves `$29`:

    - Must `push($29)` before `jalr` to callee function
    - Then, `pop($29)` after callee is finished
    - ==EASIER==, so this is what we use

  - Final code in caller:

    ```php
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

  - Final code in callee:

    ```php
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

    - we need to do `code(dcls)` before we save the registers that the function is going to use because we need the local variables to be able to be referenced starting at `0($29)` like our convention
      - if we did `code(dcls)` after, then they would have weird values since `0($29)` would be the value of some saved register, etc
    - parameters have positive offsets (from `$29`), local variables have non-positive (0 or greater) offsets

  