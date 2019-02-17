__CS 251 |__ Midterm Review

- ==Logic gates:==

  - **NOT**, **AND**, **OR**, **NAND**, **NOR**, **XOR** are most common
  - multiple input **XOR** is true for odd number of input 1's

- ==Transistors==: an off/off switch controlling the flow of electricity

  - created by 3 ppl at Bell Labs, but copied previously Canadian physicist Julius Lilienfeld

  - V = IR, voltage & current consistent in parallel, total resistance is $\frac 1 {R_i} + ...$

  - **NMOS:** leaves floating electrons around

    - Input 1 = Output 0 (NMOS stands for Negate)

  - **PMOS:** leaves positive ions around

    - Input 1 = Output 1 (PMOS stands for Preserve)

    ![image-20190214102809445](assets/image-20190214102809445.png)

  - power at drain, ground at source, region of resistance in the middle

  - whenever resistance is low, surge of power to ground = bad, so we put a resistor between drain and output

    - results in transmitting weak signal when resistance is low

  - **CMOS** solves weak signals: PMOS on top, NMOS on bottom, **negates input**

  - float (" - ") means the output does not connect to either power or ground via low resistance path

  - short circuit (" * ") means circuit has low resistance path to both power and ground (surge of power to ground)

    - NAND: 4 transistors
    - Negate: 2 transistors (CMOS)
    - new input: 2 transistors

  - **transistors** form **logic gates**, which are building blocks of circuits

- ==Decoder==

  - $n$ inputs, $2^n$ outputs where only one output is true for a specific input
  - Decoders can specify a write register number via a **control bit** to perform write operations on a single register

- ==Multiplexors==

  - $2^n$ inputs, $n$ select line bits, $1$ input chosen as output based on select line bits
  - **difference between decoders and MUXs:** decoders _take into account all of the inputs and produce a new unique output,_ but MUXs _preserve one of the inputs as the output._

- ==Flip Flops==

  - $n$-bit registers are stored in $n$ flip-flops since they hold state and preserve the data stored in them

- SR latch: 

  - S = 1, R = 0: Q = 1, notQ = 0
  - S = 0, R = 1: Q = 0, notQ = 1
  - S = 0, R = 0: Q and notQ stay in their previous states

- 

- ==Binary num operations==

  

- ==Decoding fractions==

  - .1011 is $2^{-1} \times 1 + 2^{-2} \times 0 + 2^{-3} \times 1 + 2^{-4} \times 1$, etc

- ==Encoding fractions==

  1. Convert non-fraction part to binary (ex. 2.625, 2 --> 10)
  2. Convert fraction part to binary (mult by two, take leading digit, repeat)
  3. Combine both parts
  4. **Normalize** if necessary: shift floating point to left, mult by $2^1$ each time
  5. Convert to IEEE FP representation (1 bit sign, 8 bit bias, 23 bit significand)
     - bias is x where $x - 127 = \text{exponent of original binary fractional num}$

  - IEEE FP representation is ordered (sign, exponent, significand) to allow for easy sorting (go left to right, compare bit by bit)