__CS 241 | __April 02, 2019

# Heap Management

We were given a library to deal with allocation of memory that wasn't in the stack frame through `new` and `delete`. This was managed through the command `init` initializing a heap for use.

Heaps are messier than stacks, since used memory on the heap can be scattered all about.

The hierarchy is as follows:

![image-20190422131645884](assets/image-20190422131645884.png)

Our stack will contain a pointer to where the heap is.

We'll go through a number of iterations of how to manage and implement the heap.

### Iteration 1: No Reclamation of Memory + Fixed Size Blocks

- After `init`, you get two pointers: one to the start of memory on the heap, and one to the end
  - Initialization is $O(1)​$
- Block sizes are fixed
  - Allocation moves the pointer to the start, and is $O(1)$
- Never deallocate memory (no `delete`)
- Runs out of memory very quickly

### Iteration 2: Explicit Reclamation + Linked List of Fixed Size Blocks

- Keep track of which blocks are free using a linked list
  - Allocate from this list if memory is being requested, deallocate to add to this list
- Allows for reclamation of memory, reusable

### Iteration 3: Variable Sized Blocks

- Use a linked list, but each node stores:
  1. Number of bytes in the block
  2. Where the block can be found (its address)
  3. Pointer to the next node in linked list
- Start with the entire heap being free
  - Allocation will reduce the number of bytes in the block, and move forward where the block is found
    - Allocation of $n$ bytes takes up $n + 4$ bytes in the heap - first 4 bytes store an integer indicating size of the allocated block
    - Allocation returns a pointer to the start of the $n$ bytes (NOT the start of $n + 4$ bytes!)
  - Deallocation of a block will add a node to the linked list in the correct place (based on address) with the correct information stored in the node
  - If two nodes in the linked list are consecutive (address + # of bytes = next address), collapse them into a single node and combine their sizes
    - This can happen multiple times until you have a min of one block left
- This causes **fragmentation**: free memory is split after many uses
  ![image-20190422132918210](assets/image-20190422132918210.png)
- Many ways to deal with fragmentation:
  - First fit: place memory in first available slot
  - Best fit: place block in closest free match to its size
  - Binary buddy system

### Binary Buddy System

- Start off with ex. 512 bytes of free heap memory
- If allocation of 20 bytes is needed, find smallest block of size $2^s$ (in this case, $2^5 = 32$) and split free memory in half until you have a block of that size. Reserve the entire block for this allocation.
  - The first free block larger than the desired block size is split.
- If a block is freed and its buddy (the other half of the split memory with the same size) is also free, then combine the two blocks (can be repeated)
-  Avoids fragmentation, but can waste memory (20 bytes takes up 32 bytes in heap)

### Automatic Memory Management

Some languages will manage memory automatically for the user, which means that once an object in allocated memory is no longer accessible (out of scope, removed) then the memory is reclaimed.

There are many techniques for doing this:

##### Reference Counting

- For each heap block, keep track of the number of pointers that point to that block
- Must watch every pointer, update the reference count each time a pointer is reassigned
- If a reference count of a block reaches 0, reclaim it
- Issue: if two blocks point to each other and no other pointers exist to either block, their reference counts are not 0 but both should be reclaimed since they're unreachable

##### Mark & Sweep

- Scan the entire stack and global variables to search for pointers
- Mark the blocks at these pointers
  - if these blocks have pointers, continue and mark those as well
- Scan the heap and reclaim any blocks that are not marked
- This is a graph traversal problem

##### Copying the Collector

- Splilt heap into two halves $H_1, H_2$
- Allocate memory in $H_1$ until full or cannot allocate further, then copy $H_1$ into $H_2$
  - coying can be done through mark & sweep method
- $H_2$ will have all the memory stored in $H_1$, but stored contiguously since each allocated block size is known
- Start allocating to $H_2$
- Repeat, alternating the roles of $H_1$ and $H_2$ as necessary
- No fragmentation in memory, `new` & `delete` very fast, _but_ we can only use half the size of memory!
- Variants are possible (split equally into more than 2 regions and use only 1 region for copy, etc)





