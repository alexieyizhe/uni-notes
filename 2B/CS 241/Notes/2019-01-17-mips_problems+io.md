__CS 241 |__ January 17, 2019

# MIPS Procedures

Functions, or methods, are known as **procedures** in MIPS. However, there are a number of difficulties with implementing these in MIPS, like:

- Transferring **control** to and from a procedure
- **Calling other** procedures
- Working with **parameters**
- Working with **recursive** procedures
- **Returning** values
- **Limited** number of registers
- **Existing** data

We will address these problems and their solutions in this lecture.

### Solutions to Problems  and a New Instruction: `jalr`

Most of the time, you reserve some registers for use by your procedure. However, because there are only a limited number of registers available to store data in, procedures may need to _reuse_ a register that already has existing data in it.

:warning: **You CANNOT just overwrite registers if you do not 100% know that the data is not needed, as the program might return control to procedures that need to make use of it after.** 

So, we need to _save the existing data_ somewhere else first. We can make use of the large amount of memory in RAM, but we need to make sure that we don't overwrite anything there as well.

Our **stack pointer**, accessible in Register `$30`, _keeps track of the free RAM_: it points to the **address of the last item** stored in RAM, which is utilized in the data structure of a **stack**, like so:

<img src="assets/image-20190127140348273.png" style="height:400px" />

> In the diagram above, procedure `f` has called procedure `g` and pushed registers onto the RAM stack, which has done the same with procedure `h`, all saving data/registers in RAM.

#### Template for Storing Data

If a procedure `f` has to modify registers `$1` and `$2`, the code would look something like this:

```bash
main:
	lis $8
	.word f
	jr $8  ; call procedure f
	jr $31 ; program is complete
	
	
f:
	sw $1, -4($30) ; save registers we will modify by
    sw $2, -8($30) ; pushing them onto RAM stack
    lis $2         
    .word 8        ; decrement stack pointer to enforce invariant
    sub $30, $30, $2
    ; CODE FOR PROCEDURE F
    lis $2
    .word 8
    add $30, $30, $2
    lw $2, -8($30)
    lw 41, -4($30)
    ; HOW DO WE RETURN TO MAIN???
```

In order to return to the previous procedure,  we needed to keep track of the address that called the current procedure. 

This is done with the **Jump and Link Register ** `jalr` **instruction**. `jalr $s` sets `$31` to the PC and sets the PC to `$s`. To avoid overwriting the previous value in register `$31`, we need to save that value before as well.

Here's an updated template:

```bash
main:
	sw $31, -4($30)
	lis $31              ; we just saved $31, so we can use it
	.word 4
	sub $30, $30, $31    ; decrement stack pointer to enforce invariant
	lis $8
	.word f
	jalr $8              ; call procedure f and set $31 to be this addr
	lis $31 
	.word 4
	add $30, $30, $31
	lw $31, -4($30)      ; pop stored value of $31 from stack
	jr $31               ; program is complete
	
	
f:
	sw $1, -4($30) ; save registers we will modify by
    sw $2, -8($30) ; pushing them onto RAM stack
    lis $2         
    .word 8        ; decrement stack pointer to enforce invariant
    sub $30, $30, $2
    ; CODE FOR PROCEDURE F
    lis $2
    .word 8
    add $30, $30, $2
    lw $2, -8($30)
    lw 41, -4($30)
    jr $31         ; jalr $8 saved $31 for us to return to
```



#### Passing Parameters & Recursion

To pass parameters to a procedure, usually we'll just use registers to store the parameters and have the called procedure access them through those registers. _Make sure you save the previous values of the registers!_

When we store these values and parameters properly, **recursion** will function correctly just like in any other language.



# MIPS I/O

To produce output as well as read input, we use specific special addresses. One limitation is that we can only do this _one byte at a time._

#### Output

To produce output, use `sw ` to store words in address location `0xffff000c`. The least significant byte of the stored value will be printed.

#### Input

To read from input, use `lw` to load values that are stored in address location `0xffff0004`. The least significant byte at that address will be the next character from `stdin`.



