__CS 251 |__ March 19, 2019

# Memory Hierarchies

We load **pages** of our program into physical memory (RAM), as loading the entire program into memory is resource intensive.

From these pages, we then load **chunks** of data from physical memory into our instruction/data memory. These are known as the **L1 Cache** (L1 D contains data, L1 I contains instructions).

Because these are just chunks, the program counter may try to find instructions in the L1 I cache that are not loaded into the cache right now. This is know as a **cache miss**, and it incurs a **miss penalty** where it costs $n$ clock cycles to go to physical memory, fetch the instruction, and load it into the cache.

> Usually, the miss penalty is around 100 clock cycles. This process costs much more than executing an instruction because of the overhead of determining if you have a miss, how big of a chunk to fetch, where to place the chunk, etc.

There are **intermediate caches** (L2, L3) that have a smaller miss penalty than physical memory, and other parts of the program are usually loaded into this instead of stayingi n physical memory.

> For multi-core processors, each core is assigned to their own thread that can run instructions in parallel. There is also an additional controller unit that conducts the work of each core.

> **Ex. **

### Direct Mapped Caches

With all of the instructions being fetched and moved around, we need to know where an instruction is in the cache. This can be accomplished through a **direct mapped cache.**

