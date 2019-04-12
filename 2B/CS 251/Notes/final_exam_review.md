__CS 251 | __Final Exam

## Review

#### Checklist

- [ ] Single cycle datapath
- [ ] Pipelining
- [ ] Caches
- [ ] Virtual Memory

### Questions

- [ ] What parts of a datapath does an instruction use, and why

  - [ ] R-format
  - [ ] lw
  - [ ] sw
  - [ ] branch
  - [ ] jump

- [ ] which bits correspond to `$rs`, `$rt`, `offset`, in instructions

  - [ ] R-format

  - [ ] I-format:
    addi \$rt, ​$rs, offset

    beq \$rs, ​$rt, offset

    sw \$rt, offset(​$rs)

    lw \$rt, offset(​$rs)

  - [ ] Jump

- [ ] ALUOp codes and `00` for add, `01` for subtract

- [ ] What is the value at a specific point in the datapath (single cycle, pipelined)

- [ ] What is the timing for a specific format or instruction

  - remember that some parts of the datapath can happen in parallel, but some rely on the other executions finishing first

- [ ] Implement instructions in single cycle into pipelined datapath and vice versa

- [ ] 

### Single cycle datapath

- **program counter**, **instruction memory**, **registers**, **ALU**, and **data memory** make up the processor
- ==fetch-execute cycle==: every clock cycle, we:
  1. Fetch instruction & update PC
     - First, current PC 32-bit address is used to read an instruction from instruction memory
     - Adder that adds current PC 32-bit address to a hard-coded 32-bit value for 4
  2. Execute instruction by: fetching register operands, computing result, then using or storing result
- if we execute one instruction per cycle, we have to slow clock down to slowest instruction speed
  - also require separate instruction/data memories
- only a single instruction has use of the datapath at one time
- on the falling edge of clock cycle (at the very end) the registers are written to and PC is updated
- the main control unit sends a 2 bit ALUop line to ALU control unit:
  - if instruction was R-format (`add`, `sub`, `and`, `or`, `slt`), use the lower 6 FUNCT bits to determine what to do
  - if instruction was I-format (`lw`, `sw`, `beq`, `addi`) then use ALUop bits:
    - `00` opcode for ALU means add
    - `01` opcode for ALu means subtract 
  - if instruction was R-format, ALUop are `10` (but not used) and use 5 funct bits from instruction
  - Implementation of control unit:![image-20190407170751394](assets/image-20190407170751394.png)
- We want to add parallelism through **Pipelining**
- *why is the PC's top 4 bits being concatenated with the jump offset?* we want to keep the offset relative to the PC, so we append the top 4 bits to the offset so it's relative to the PC!
- ==how to modify datapath to add a new instruction==
  - determine what parts of datapath we need for new instruction (ALU, data mem, instr mem, etc) or if we need new parts
    - if we need new ones, wire them into existing datapath
  - add new control signals to control units
  - adjust old control signals to account for new instr



### Multi-cycle datapath

- split up one long clock cycle into multiple shorter ones

- store data between stages (after each clock cycle) in a state element

- control bits are routed to each intermediate register state to be turned on if it's the active state

- Stages:

  1. **Instruction Fetch (IF)**: 

     - ==instruction is fetched from instr memory==
     - PC updated to PC + 4
     - at end of cc: write data to IF/ID intermediate register

  2. **Instruction Decode (ID)**:

     - ==read from intermediate register==
     - ==opcode sent to control unit==

     - at end of cc: write data to ID/EX intermediate register

  3. **Execute (EX)**:

     - ==ALU performs computation==
     - if `beq`: branch target address is calculated

     - at end of cc: store data in EX/MEM intermediate register

  4. **Memory (MEM)**:

     - if branch: update PC
     - ==write or read from data memory==
     - at end of cc: store in MEM/WB imtermediate register

  5. **Write Back (WB)**:

     - ==if necessary: write back to a register==
     - end of datapath

### Pipelining

- if we overlap execution of multiple instructions in a multi-cycle datapath, we can speed up execution time
- if information isn't needed until a later stage, it gets passed through intermediate registers to the correct stage
- instructions cannot look back, must bring information with them
- **Hazards:**
  - **Structural hazard**:
    -  if there's only a single memory for both data/instr, instr fetch cannot happen at the same time as load/store of data
      - possible solution: split up instruction & data memory
    - if > 1 stage of the datapath are attempting to use data mem to read/write
      - possible solution: write in the first half of cc before reading in the second half
  - **Data hazard**: result of one instruction is needed by the next one
    - for 2 instructions that read/write at the same time, do the write first half of clock cycle and the read second half, since the read will rely on having updated data
    - for instructions that need the result before it's been written, implement a ==stall== 
      - NOPs: an instruction that has no outcome, inserted to force a gap between instructions that cause data hazards (`sll, $0, $0, 0` or `add $0, $0, $0`)
    - better: implement ==data forwarding== to send data to instruction immediately following
      - forward the data in the intermediate register to a stage before the current stage for following instructions
      - MUXs handle choosing which intermediate register's data to use: 
        1. ID/EX (normal)
        2. EX/MEM (after ALU)
        3. MEM/WB (after getting from memory)
           1. this is why `lw` **has one stall that's inevitable when an instruction uses the same register right after** - it cannot be forwarded to the instruction after it in time, since by the time `lw` has the correct data, the instruction after it will be past the EX stage
      - new `ForwardA`, `ForwardB` bits that tell MUX which to pick
      - if both instructions before the one in EX are writing to the register the one in EX is using, then the closer one (the one in EX/MEM) will take precedence
    - ==code rearrangement== can solve the issue with `lw`'s mandatory **stall**: move an instruction that needs to be executed anyways and does not use the `lw` between the `lw` and the use.
      - rearranged code should not affect the behaviour of the code (dont swap into/out of loops, data dependencies, etc)
    - **branch-data hazard**: this is another case requiring a stall - when you decide a branch in ID stage based on register data from prior instruction
      - when branch in MEM, the hazard can be avoided because data is forwarded in time, but not in ID
      - when we branch in ID, the ALU computed value of the instruction prior cannot be forwarded in time to the branch instruction. so, there is a mandator 1cc stall with `beq` (a branch data hazard)
    - Implementing stalls in the hardware:
      - hazard detection unit is responsible for creating a stall if it detects a hazard
        1. prevent instructions behind stall from moving forward
        2. zero out all signals in control units
  - **Control hazard**: conditional branch hazard may or may not change sequence of instructions executed
    - if we branch in MEM stage, then the 3 instr after have to be flushed
    - Solution: ==branch in ID stage==
      - move the equality test to its own special unit in ID
      - compute new target address for PC in ID stage as well
      - if branch is taken, instruction(s) (either 1 or 3 depending on where you branch) after it should not be executed - can be dealt by in 2 ways:
        1. flush the instructions that should not be executed by zeroing control bits (slower :disappointed: )
        2. use code rearrangement to add NOPs or move instructions that should be executed to after the branch
- Summary:
  - **load-use hazard:** instruction after `lw` uses register being loaded into
    - 1cc stall OR code rearrangement
  - **branch-control hazard:** instructions after branch start executing but may be unneeded if branch is taken
    - 1cc flush or NOP insertion if branch in ID
    - 3cc flush or NOP insertion if branch in MEM
    - can be avoided with code rearrangement
  - **branch-data hazard**: instruction before branch deal with data used in determining branch or not
    - with no data forwarding, 1cc stall or code rearrangement or NOP is needed
    - with data forwarding and branch in MEM, this is nonexistent
    - with data forwarding and branch in ID, 1cc stall OR code rearrangement or NOP is needed

### Cache

- relationship between CPU storage (cache) and RAM

- store more recently used and likely to be used information in faster memory

- **temporal** and **spacial** locality: information that has been recently used has higher chance to be referenced again, and other information near currently used stuff has more chance to be used again

- caches are on CPU, faster to access, if cache miss, you go to RAM in memory

- types of caches

  1. **one way set associative (direct mapped) cache:** only one place a specific block of memory can go, if something is there it has to be removed
     - valid bit indicates if the data at the location is valid 
     - byte offset is the number of bits needed to represent a block of size $x$
       - ex. block size 4 = 2 bits byte offset
       - block size 8 = 3 bits byte offset
     - ==index== is lower $n$ bits of address where $2^n = $ size of cache
     - rest of the address are the _tag_ bits that identify if you have a hit or miss
  2. **two way set associative cache:** two spots for each index, so two blocks with same index can be in cache at the same time
     - each spot has its own tag bits that are used to differentiate different blocks stored in cache
  3. $n$**-way set associative**: $n$ spots for each index
  4. **fully associative cache**: all spots in cache are open to all blocks
     - no index bits
     - all bits in address are tag bits

- remember that each increase in associativity decreases number of index, so total # of spots stays the same

- increasing associativity does _not_ increase search time, but rather increases hardware since searching cache is done in parallel 

- when cache is full, use **Least Recently Used (LRU)** replacement scheme: replace the location that was used least recently

  - go back in mem access history starting at most recent access
  - eliminate spots until you have one spot left - replace that one

- average memory access time (AMAT):` Time for a hit` + `Miss rate` x `Penalty for a miss`

- we can bring in more than one word at a time if we increase block size and bring in entire blocks

  - introduce the **block bits**: lower than index, higher than byte offset

  - block bits represent where in the block the word is (`00` means first word in block, `10` means 3rd, etc)

  - all words in a block will have _same_ index and tag bits, only block bits are different - store them all in the same index slot in cache

    ![image-20190410201448758](assets/image-20190410201448758.png)

- every cache miss means RAM access time (`Penalty for a miss`)

  - larger block size = increase in access time (still less than fetching one by one separately: 104cc for fetching block size of 4, and 100 x 4 cc for fetching one by one)

- we use the ==write-back== technique to reduce cost of writing: **dirty bit** represents if the item in cache was modified

  - when we write to a word in data memory (`sw`), we modify that word in cache ONLY and indicate it's been modified by setting dirty bit to 1
    - since we always read from cache first, accessing that word will give the correct modified value always
  - when the word is bumped from cache, then we update the RAM value of any blocks with dirty bit 1
    - entire block shares one dirty bit, so all words in block are updated even if they're not changed

- **instruction cache misses** are when you reach an instruction not in cache and have to bring it in

  - when calculating cost of this in clock cycles, make sure to ==pay attention to block alignment== (code snippet might start at a word that is not first in the block, so calculations might be off)
  - blocks also mean subsequent instructions of a block are already brought into cache, so do not add RAM access time when analyzing those instructions

- **data cache misses** are caculated based on above memory access times, write-back times

  - also need to check:
    - block alignment to determine what block exists or is being brought into cache
    - subsequent data being brought into cache in the same block
  - ==for block size of 1, a cache miss when modifying data (`sw`) does not result in RAM access - it just writes to where that data would be in cache and sets dirty bit to 1==
    - no read before write, reduces time

- total clock cycles =` # of runtime cycles` (hazards, stalls, etc) + `instruction cache misses` + `data cache misses`

### Virtual Memory

- relationship between RAM (physical memory) and disk (virtual memory)

  - going to disk is very expensive (millions of cc)

- programs are larger than RAM size, so they're stored on disk (secondary storage) split into **pages**

- pages of different programs are loaded into RAM, but the CPU has to differentiate between them (and they both have instructions with addresses that can be the same)

- RAM (physical memory) is also split into pages

  - smaller/larger page sizes have tradeoffs: in this class, we usually use 4kb pages 

- each program has a **page table** also stored in RAM that maps virtual pages (spots in RAM) to physical pages (corresponding page of program in disk)

  - tells the system which program has which pages in which spots in RAM
  - as programs are loaded into RAM, their respective page tables are created and added to RAM as well
  - a virtual address (somewhere like in the PC) is mapped to a physical address through the page table for the program that's running rn
    - the **page table register** keeps track of which progarm is running by pointing to the location of the current page table

  - given a virtual address and thus a virtual page number (VPN), the page table will tell us the physical page number (PPN) on RAM that the virtual page is loaded into
    - if the virtual page (page of the program on disk) is not loaded into RAM, it will also tell us that and result in a page fault
  - virtual address bits broken up into: **virtual page number** (which page of the program) and **page offset** (how far into that page the address is)
    - page offset stays the _same_ for the address with VPN and when translated into PPN
    - number of bits for page offset depends on page size
      - ex. 4kb page = 4000 bytes = $2^{12}$ bytes so 12 bits of address must be offset
  - the page table has a row for each virtual page number, and a _valid bit_ associated with the vpn
    - if valid bit is true: page is in RAM and has a physical page number associated with that VPN
    - if valid bit is false: page is not in RAM _(page fault)_ and must be fetched from disk
  - uses **reference bit** to determine which pages that are currently in RAM can be replaced if necessary

- every instruction has a virtual **instruction address**, and instructions like `sw`, `lw` that reference data, also have a virtual **data address** (both must be translated into physical first to access in RAM)

- _dirty bit_ and _write-back_ also used for RAM to disk, like cache to RAM

  - entire page is written back if dirty bit is true
  - reference bit helps us find the Least Recently Used page when replacing

- **TLB: Translation Look-aside Buffer**

  - finding the PPN from VPN requires one RAM access since page table is in RAM, additional cost
  - store some entries of page table in **TLB** in a small cache that contains only address translations
  - check TLB first and only check Page Table if TLB does not contain virtual address or VPN
  - NOTE: the valid bit in a row of the TLB only tells us if we can use the information in said row: it doesn't say anything about whether the page is in RAM or Disk
    - Page Table valid bit will tell us 1 if the page is in RAM and 0 if it is not in RAM (it's in disk)
    - If an entry is valid in TLB, it means it must be in RAM
  - TLB is updated whenever a new page is brought into RAM from disk
    1. If page is swapped/replaced in RAM: 
       - references to page TLB (and cache) are removed
       - Info about new page is placed into Page Table, and copied to TLB
  - since TLB stores only the VPN -> PPN translation, it doesn't require as much space as the cache itself
  - TLB is _independent_ of cache
  - TLB hit _iff_ Page is in RAM (page fault not possible)
    ![image-20190411153333115](assets/image-20190411153333115.png)
    Last row is Possible, 0 Disk Reads, 2 RAM Accesses (data in RAM, but not in cache)





### Summary

- **Path of System**
  1. **CPU** obtains virtual address it needs to act on (can be from PC, from `lw`, `sw`, etc).
  2. **CPU** checks **TLB** for VPN -> PPN.
     - if TLB==HIT==: Get PPN and convert to physical address.
     - if TLB`MISS`: Go to RAM and check for PPN in Page Table
       - If Page Table ==HIT== (valid bit is on): 
         - get PPN from VPN.
       - If Page Table `MISS` (valid bit off, page fault):
         -  fetch page from disk and place in RAM - might have to replace a page if RAM is full, use reference bits to determine which to remove
         - Update TLB
  3. At this point, you have a physical address with PPN and page offset.
     Check **cache** in datapath to find data or instruction.
     1. If cache ==HIT==: Get data/instruction from cache. 
     2. If cache `MISS` (does not contain address): 
        - fetch the block containing address from RAM and load into cache using techniques described previously.
  4. Do whatever with the data/instruction. Repeat from Step 1.
- 