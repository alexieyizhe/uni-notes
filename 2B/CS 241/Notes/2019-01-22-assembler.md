__CS 241 | __January 22, 2019

# The Assembler

Our goal is to convert assembly code (our MIPS language instructions) into machine code (binary ones and zeroes). The translation process between these two involves phases:

1. **Analysis:** Understand what is meant by the input source.
2. **Synthesis:** Output the equivalent target code in the new format.

###Assembly File

An **assembly file** is written in machine code and can be thought of as _a string of characters._ We need to break it down into meaningful **tokens:** phrases like labels, numbers, `.word`, and other MIPS instructions, etc (this is done for us in `asm.rkt` and `asm.cc`).

For our two steps, we need to perform:

1.  **Analysis:** Group tokens into valid instructions, if possible.
2. **Synthesis:** Output the equivalent machine code that corresponds to the given code. 
3. Output `ERROR` to `stderr` if not valid.

> **Tip for Assignment**: Focus on finding correct tokens, as there are many more incorrect ones than correct ones.

### A Big Problem

The problem arises when we encounter a label that references a line further into the code:

```bash
beq $0, $1, someLabel
; other instructions
someLabel: 
	add $1, $1, $0
```

In the example above, when we see `someLabel` on line 1, we don't know what the corresponding address is to convert this into machine code. 

So, we need to make two passes:

1. Group tokens into instructions. Record address of all labelled instructions, most likely in a dictionary, also known as a symbol table.
2. Translate each instruction into machine code. If the instruction refers to a label, look up the associated address in the table created in Pass 1 and calculate the correct value.

### Your Assembler

When writing your assembler, you will do two things:

1. Output the machine code from the assembled MIPS code to `stdout`.
2. Output the symbol table created in Pass 1 to `stderr`.



#Writing Binary Code in `C++`

### Bitwise Operations in `C++`

There are numerous operations that manipulate the bit (binary) representation of values:

| Operation                              | Example                                                    |
| -------------------------------------- | ---------------------------------------------------------- |
| `&`: Bitwise AND ==Binary==            | `1010 & 0011` is `0010`                                    |
| `|`: Bitwise OR ==Binary==             | `0101 | 1010` is `1111`                                    |
| `^`: Bitwise XOR ==Binary==            | `0110 ^ 1101` is `0010`                                    |
| `~`: Bitwise NOT ==Unary==             | `~11101` is `00010`                                        |
| `<<` or `>>`: Bitwise Shift ==Binary== | `00110 >> 2` is `11000`<br />`0110100 << 3` is `110100000` |

### An Example

To illustrate these steps for assembling code, we will do a comprehensive example of translating the following ==MIPS== instruction to ==binary==:

`bne $2, $0, -37` $\Rightarrow$ `0001 0100 0100 0000 1111 1111 1111 1101`

The instruction in MIPS can be broken down as follows:

![image-20190127145133072](../../../../../Google%20Drive/University/2B/CS%20241/Notes/assets/image-20190127145133072.png)

- `bne`'s opcode is $000101$, which is 5 in binary
- `$s` is `$2`, so the binary is $00010$.
- `$t` is `$0`, so the binary is $00000$.
- The offset is `-3`, so the binary is $1111111111111101​$.

![image-20190127150336898](assets/image-20190127150336898.png)

But, we can't just print out `instr` by doing `cout << instr`. This would output the 9 bytes that correspond to the ASCII code for each image, and we want just the 4 bytes that correspond to this number. 

![image-20190127150510229](assets/image-20190127150510229.png)

and we're done!