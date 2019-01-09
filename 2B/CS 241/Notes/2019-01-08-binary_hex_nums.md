__CS 241 |__ January 8, 2019



RANDOM????????: Using the __Random Access Machine (RAM) model__, we create a simulated __MIPS__ machine.

# Binary and Hexadecimal

The **binary** system consists of $0$'s and $1$'s, known as **bits.** It's the only unit that a computer understands. It's convenient to group these bits together into sequences of 8 bits, also known as a **byte**, or 4 bits, also known as a **nibble.**

- There are $2^8$ different patterns, or bytes.
- A **word** is the machine-specific grouping of bits: most computers these days use 32-bit or 64-bit words.
  - As our machines get more complex and our memory capacity grows, we require larger words to properly track each portion of memory.
  - In this course, we use a 32-bit computing machine.

> Binary is hard for us to understand, so we develop higher-level programming languages like `C` and `JavaScript` to allow us to more easily issue commands.





### Numbers: Binary Representation

A byte can have multiple different meanings depending on where and what it's used for - we need to know the context.

> **Ex. In the context of a number, what decimal number is $11001001$?**
> $11001001 = (2^7 * 1) + (2^6 * 1) + (2^5 * 0) + (2^4 * 0) + (2^3 * 1) + (2^2 * 0)+ (2^1 * 0) + (2^0 * 1) = 201$
>
> **Ex. How do we convert $201$ into a binary number?**
> $201 - 2^7 = 73 - 2^6 = 9 - 2^3 - 2^0 = 0$, so set the 7^th^, 6^th^, 3^rd^, and 0^th^ bit to $1$ and the others to $0$.

In the context of binary numbers, we need a way to represent positive or negative numbers. We do this by making the first bit symbolize positive or negative, known as the **sign magnitude.** However, this is wasteful, since we now have -$0$ and $0$.

#### 2s-complement

Instead, computers use a system called **$2$s-complement**:

1. Interpret the $n$-bit number as an unsigned integer $a$.

2. Examine the first (leftmost) bit.

   - If the first bit is $0$, we are done and the number is $a$.

   - Otherwise, subtract $2^n$ from $a$ to get the number.

> **Ex. 2s-complement representation of $n = 3$.**
>
> | 000  | 001  | 010  | 011  | 100          | 101          | 110          | 111          |
> | ---- | ---- | ---- | ---- | ------------ | ------------ | ------------ | ------------ |
> | 0    | 1    | 2    | 3    | $4 - 8 = -4$ | $5 - 8 = -3$ | $6 - 8 = -2$ | $7 - 8 = -1$ |



#### An Alternate Method

==+==: Interpret the 2s-complement number as normal magnitude
`-`: Take the magnitude of the  2s-complement number. Flip the bits. Add 1 to get the decimal number.

To convert back from a negative decimal number, you can do the same processs forwards (flip bits, add 1) since it's cyclic.

> **Ex. -73 using alternate method.**
> Forwards: $01001001 \rightarrow 10110110 \rightarrow 10110111$ 
> Backwards: $10110111 \rightarrow 01001000 \rightarrow 01001001$



### Numbers: Hexadecimal Representation

We represent 4 bits of binary with 1 digit in base 16. Since we only have 10 digits from 0-9, we represent the other 6 with $a, b, c, d, e, f$.

> **Ex. Decimal/Hexadecimal/Binary Conversion**
> $ 00110111 \rightarrow 0011 \ 0111$ (grouped) $\rightarrow 3 7 $ (hexadecimal) $=  (16^1 * 3) + (16^0 * 7) = 55$ (decimal) 



### Interpreting Bits & Bytes

The computer's only way of telling what a group of bits should be interpreted as is through **types**.



### Characters: ASCII

Real ASCII is 7 bits, but we force it into 8 bits since its nicer, but this causes compatability issues.

Unicode also used for global characters.