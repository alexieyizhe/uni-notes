__CS 241 |__ March 28, 2019

# Code Optimization

Optimizing code is difficult. Usually, we want to minimize the runtime of the compiler and the code that it outputs, but in this course we focus on just _minimizing line numbers._

There are a number of strategies that we can employ:

### Constant Folding

If we consider the following code:

```c++
int wain(int a, int b) {
  return 2 + 3;
}
```

In our translation into MIPS, we might use the stack to store the constant $2$, but we could have just loaded the value into a different register.

Additionally, our compiler could have just done the computation and loaded the value $5$ into `$3`. This is known as **constant folding.**

### Constant Propogation

If a defined value never changes throughout its usage, you should be able to replace any occurrence of the value with a constant, and then possibly use _constant folding_ to simplify the translated code.

Consider the code:

```c++
int wain(int a, int b) {
  int x = 5;
  return x + x;
}
```

We could simply `lis $5` and `.word 10`.

### Common Subexpression Elimination

If we have multiple subexpressions that are used more than once, we do not need to compute this value twice - instead, we can just compute the value, and perform the operation with itself (since MiPS allows you to repeat a register number in an operation).

If we had the code in the example for _constant propagation,_ we could simply do `add $3, $3, $3` to get the desired value of $10$.

### Dead Code Elimination

Dead code will never be executed no matter the input, so translating it is useless. 

Examples include code that follow tests that always simplify to false, or computing values that are then never used.

If it can be detected and removed, then we can improve runtime.

### Register Allocation

Accessing variables on RAM (in the stack) is expensive, and we have multiple registers like those from `$14` to `$28` that we don't use at all. 

We can use those registers much like intermediate registers to store values that are most used, recently used, etc. We want to store variables in registers during their **live ranges**: sections of code between their first occurrence and their last usage.

An example of live ranges:

![image-20190422122349827](assets/image-20190422122349827.png)

### Strength Reduction

Multiplication is a lot more code than addition, and in the real word, is much faster as well. Avoiding multiplication is best, so you should do $n + n$ instead of $n * 2$.

### Inlining Procedures

If a procedure's body is shorter than the code to call the procedure, you should inline the procedure by replacing any call to the procedure with the procedure body itself.

> This has pitfalls to be aware of, like not working with recursive calls, and being harder to calculate than other methods of code optimization.

If you inline every call to a procedure `f`, then you don't need the code for `f` at all.

### Tail Recursion

Tail recursion is when the last operation done in a stack frame is returning a value of a recursive call. This allows us to reuse a stack frame, since we don't need to keep track of any other value (the return value is calculated in each call of the procedure, so it's fine to overwrite the same stack frame with the new iteration).

This is not possible in WLP4 - however, we can write simpler code that does fall within the constraints of the current language. This is known as **intermediate code** and, once put through the compiler, will resolve to MIPS output that follows tail recursion.

