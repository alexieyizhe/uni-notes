__CS 241 |__ Feb 14, 2019 :heart:

#LR(1) Parsers: Parse Trees

The two different parsing methods have different ways of building out their parse trees:

- **Top down parsing** has the initial LHS of the rule (that was on the stack) as the parent node, and the children that are about to be pushed onto the stack to replace the LHS as the children.
- **Bottom-up parsing** has the characters before reducing (usually the RHS of a production rule) as the children, and the parent as the LHS that's being reduced to.

> **Ex. Building a bottom-up parse tree**
>
> ![image-20190318230739966](assets/image-20190318230739966.png)
>
> ![image-20190318230746150](assets/image-20190318230746150.png)
>
> 



# Context Sensitive Analysis

We have parts of a language that cannot be enforced by a context-free grammar. These are just some aspects:

- Type-checking
- Duplicate/missing declarations
- Scoping
- Well-typed expressions

These can be solved by **context-sensitive languages**, ones where the context matters.

### Multiple/Duplicate Declarations

We can catch these errors by constructing a symbol table.

1. Any rules where `TYPE ID` exists on the RHS, add the `TYPE ID` pair to the table. If it already exists, that's a duplicate declaration error.
2. Any rules with `ID` on the RHS, check the table. If it's not there, that's a missing declaration error.

Unlike MIPS, we only need one pass as variables _must_ be declared before they are used, so we will never find a variable being used before its declaration in a ==valid== program.

### Scoping

The previous solution to the declaration issue has to take into account scope as well. Two variables with the same name can be declared in different procedures with no problem, but one variable declared in a certain procedure cannot be used without declaration in a separate procedure.

To resolve this, we need to create a top level symbol table that also associates the procedure name with the `TYPE ID` pair that is tracked previously. It also helps to have a global variable that tracks the current procedure we're in.
