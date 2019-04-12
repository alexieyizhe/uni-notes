__CS 241 |__ Feb 28, 2019

# Code Generation

After running our program through parsing, type checking, etc, we are able to assume that the code has no compiler errors, and so is a valid program in our language.

Now, our final job is to take the code and convert it into a valid equivalent program in MIPS.

> We already wrote code for converting MIPS to binary, so combined, we have a full compiler down to binary.

There are *infinitely* many equivalent MIPS programs to a single WLP4 program. We want to take into account some points:

- Correctness is our primary goal.
- A simpler program is also good - we want to avoid overcomplicating anything if possible.
- Efficiency to compile - we don't want our equivalent program to be exponentially larger.
- Efficiency to run - we want our compiled code to be fast when running.

### Symbol Tables & Parse Tree Complications

When we convert the following two programs to MIPS:

```c++
// 1
int wain(int a, int b) {
  return a;
}

// 2
int wain(int a, int b) {
  return b;
}
```

The parse tree is exactly the same!

![image-20190324160100983](assets/image-20190324160100983.png)

We need to be able to distinguish between these two excerpts. 

This is what the **symbol table** is for: it stores the type and location of each symbol. However, we run into two problems (and their flawed solutions):

1. There are not enough registers to store symbols for a large program. To solve this, we can try storing them on the stack and keeping track of their offset from the stack pointer (`$30`).
2. If we store on the stack and keep track of the offset from `$30`, our problem is that the stack pointer (`$30`) changes as we push and pop stuff. We need to know what the exact correct offset is when we see the variable.

So, we store a pointer to the very bottom of the stack in `$29`, and store the offset in the symbol table as the offset from this address. Now, the location of each symbol in the stack will never chance if the stack pointer moves!

### Computing Values

If we want to compute `a + b`, we need to load both `a` and `b` before computing the final value.

We can use `$3` for scratch work and overwrite it with the final product, but we also need to use the convention that `$5` also stores intermediate work.

Again, with more than two variables (like `a + (b - c)`), we need an increasing amount of registers. So, we store intermediate values on the stack again as well.

We can define some **shorthands** for the above:

- Define `push($3)` to mean we push the value at `$3` onto the stack, and the code is:

  ```
  sw $3, -4($30)
  sub $30, $30, $4
  ```

- Define `pop($5)` to mean we pop the last value on the stack into `$5`, and the code is:

  ```
  add $30, $30, $4
  lw $5, -4($30)
  ```

  