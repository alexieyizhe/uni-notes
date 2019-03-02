CS 240 |__ Midterm Study Guide

#Outline

- Everything from modules 1 - 5 
- Tries, Compressed Tries and Multiway Tries from module 6
- Lower bound may not be covered specifically but decision trees are fair game (covered earlier)

#Asymptotic Analysis

- experimental studies are bad, too many factors can affect runtime (performance of hardware, OS, etc)
- **order notation** ignores constants and lower order terms, mostly consider runtime for large inputs
- ==**Big O**==; $f(n) \in O(g(n))$ if there exists a constant $c \gt 0$ such that $|f(n)| \leq c | g(n)|$ for all $n \geq n_0$.
- ==**Big Omega ($\Omega$) **==: $f(n) \in \Omega(g(n))$ if there exists a constant $c \gt 0$ such that $|f(n)| \geq c |g(n)|$ for all $n \geq n_0$ (lower bound)
- ==**Big Theta ($\Theta$)**==: $f(n) \in \Theta(g(n))$ if there exists constants $c_1, c_2$ such that $c_1|g(n)| \leq |f(n)| \leq c_2|g(n)|$ for all $n \geq n_0$ (tight bounds on both sides)
- ==**Small o ($o$)**==: $f(n) \in o(g(n))$ if for ALL constants $c \gt 0$, there exists a constant $n_0 \gt 0$ such that $|f(n)| \lt c |g(n)|$ for all $n \geq n_0$.
- ==**Small omega ($\omega$)**==: $f(n) \in \omega(g(n))$ if for ALL constants $c \gt 0$, there exists a constant $n_0 \gt 0$ such that $|g(n)| \lt c |(fn)|$ for all $n \geq n_0$ (opposite, so $f(n) \in \omega(g(n))$ if $g(n) \in o(f(n))$).

![image-20190227213655423](assets/image-20190227213655423.png)

### Rules

- **Maximum rules**:
  - $O(f(n) + g(n)) = O(max\{f(n), g(n)\})​$
  - $\Omega(f(n) + g(n)) = \Omega(max\{f(n), g(n)\})​$
- **Transitivity rules:**
  - $f(n) \in X(g(n)), g(n) \in X(h(n)) $ means $ f(n) \in X(h(n))$.
- **Limit rule:**
  - if $L = \lim\limits_{n \rightarrow \infty} \frac {f(n)} { g(n)}$:
    - $f(n) \in o(g(n))$ if $L = 0$
    - $f(n) \in \Theta(g(n))$ if $0 \lt L \lt \infty$
    - $f(n) \in \omega(g(n))$ if $L = \infty$
  - ==L'Hopital's rule is is useful when calculating limit==

### Tips

- Use nested summations `PRACTICE THIS`

- To find $\Theta()$, either:

  1. Use $\Theta$ bounds throughout the entire analysis to get the bounds
  2. Prove $O$-bound and $\Omega$-bound separately (might be easier to sum them separately)

  ![image-20190227213806605](assets/image-20190227213806605.png)

`Know MERGESORT`

# Abstract Data Types

### Priority Queue

- items in collection have a priority, there's a deleteMax method to delete highest priority
- can use **unsorted** arrays ($O(1) $ insert, but $O(n)$ deleteMax) or **sorted** ($O(n)$ insert, but $O(1)$ deleteMax)



### Binary Heaps

- binary heap is a binary tree with two properties:

  - **structural:** all levels are filled except possibly last one, which is filled from left to right
  - **heap-order**: key of the parent of a node is larger than the key of the node in max-heap (reverse is true for min-heaps)

- height of heap with $n$ nodes is $\Theta(\log n)$

- **Binary heaps with arrays**: 

  - root at $A[0]$
  - left child of $i$ at $A[2i]$, right child at $2i + 1$

- **Insertion:** 

  1. Place new node at first free leaf spot
  2. Perform **fix-up** if heap-order violated (continue swapping with parent nodes until key is greater than and heap-order is restored)

  - $O(height \ of \ heap) = O(\log n) $ time 

- **deleteMax:** 

  1. replace last leaf node with root node (root node is max, the node we want to delete)
  2. delete the last leaf node (which was previously root node)
  3. move the last leaf node (now at root position) down to correct position with **fix-down** (find larger child of current node being fixed down, swap with that child until correct and heap-order is restored)

  - $ O(height \ of \ heap) = O(\log n)$ time

- can create priority queues using heaps and keeping track of size of heap (= size of priority queue)

- **Sorting with heaps**

  - We can sort an array by inserting it into a heap and "emptying out" the heap after back into the array by calling deleteMax
  - this takes $O(n \times insert + n \times deleteMax) = O(n \log n + n \log n) = O(n \log n)$ time
  - we can use the same original array as the array representation of the heap we're using to sort, thus reducing space to $O(1)$
    - this is what **Heapsort** does
      - ![image-20190227222443666](assets/image-20190227222443666.png)
      - calls heapify to build a heap out of the array
      - calls deleteMax, which places the largest element at end of array
        - decreases n and repeats so the 2nd largest element is placed 2nd last, 3rd largest at 3rd last, etc
    - `Know HEAPSORT`

- To **heapify ** build a heap from an array: use fix-downs from the parent of the last leaf node

  1. Starting with the parent, bubble up the largest child node of the two children so the parent of this parent can access it
  2. Keep doing the same as you go up the list, this guarantees the children of the current node being worked on are the largest of their subtree 
  3. so you always bubble up the largest child until you get to the top

# Sorting

### Selection

- find $k$th largest element in the sorted version of an array $A$:
- **quick-select** (and also **quick-sort**) rely on:
  - **choose-pivot**: just choose a set value for now
  - **partition**: partition $A$ into two sections and return an index $i$ where all elements with index $\leq i$ are $\leq A[i]$ and all with index greater or equal are greater or equal in value to $A[i]$.
    - partition is easy, iterate through array, place elements in two defined arrays, then put back into $A$
    - partitioning in place is harder:
      -  keep swapping outermost wrongly-positioned pairs (keep track of two pointers that start at opposite ends of $A$):
      - keep moving up/down if element is in the right "side " (left/right) of pivot, stop when encountered wrongly-positioned element
      - if youv'e overlapped, then you're done
      - otherwise, swap it with the element at other side (which has also moved up/down until it found a wrongly-positioned element)
      - repeat

![image-20190227223527887](assets/image-20190227223527887.png)

![image-20190227223819619](assets/image-20190227223819619.png)

   - **quick-select**: Basically partition, then keep running quick-select until your pivot is the desired $k$th index position
        - best case $\Theta(n)$, worst case $\Theta(n^2)$

### Randomized Algorithms

- well designed randomized algorithms will have the _same_ expected running time in worst case and average case.
- **randomized expected runtime analysis** `KNOW HOW TO DO THIS`
  - if you choose a random index as pivot equally likely, it's a $\frac 1 n$ chance of having pivot at index $i$
  - **average** runtime is sum of costs for all permutations, divided by number of permutations
  - **expected** runtime is only for randomized
    - **expected** is $T^{(exp)}(I) = E[T(I, R)] = \sum\limits_R T(I, R) \times Prob(R)$ where $R$ is a sequence of random nums
-  choosing a random pivot instead of always the same index is the fastest **quick-select**
- **quick-sort**:
  - very similar to **quick-select**, but instead of checking if you are at the desired index and returning if so, you _always_ continue sorting the two subsections in the partitioned array
  - can use randomized algorithm to get expected $\Theta (n \log n)$
  - best case $\Theta(n \log n)​$, worst case $\Theta(n^2)​$





- can be expressed as a decision tree:

- ![image-20190228101927063](../../../../../Google%20Drive/University/2B/CS%20240/Notes/assets/image-20190228101927063.png)

- Comparison based sorting lower bound is $\Omega(n \log n)$ 
  - When expressed as a decision tree, the number of leaves must be at least $n!$ since any permutation of the original array of $n$ elements could be the possible sorted array
  - then the height of the tree (runtime of the program) must be at least $\log n!$ aka $O(\log n!)$
  - also, $n! = n(n - 1) ... \geq \frac n 2 \times \frac n 2 (\frac n 2 times)$, so $O(\log n!) \geq \log(\frac n 2 ^{\frac n 2}) = \frac n 2 \log n - \frac n 2 = \Theta(n \log n)$ 
  - so, $\log (n!) \in \Omega(n \log n)$ for all comparison based sorting algorithms



### Non-comparison based sorting

- if elements are in base $R$, there is a radix of $R$ (decimal $R = 10$, etc)

- if all elements have same number of digits (pad less digits with leading 0), we can use **bucket-sort**

  - place them in $R$ different buckets based on a predetermined single digit of the element
  - then copy buckets back
  - this is **stable**, meaning elements stay in original order if they are "equal" (placed in the same bucket)

- we don't want to waste space when it comes to **bucket-sort**, so we use arbitrary buckets in **count-sort**

  - first, count how many elements of a certain kind there are (how many will go in a single bucket)
  - then, find the starting index of the kind in the original array by adding starting index of previous kind to number of previous kind and store in $idx$ array
  - create single new array to hold sorted order, then go through original array and find index in $idx$, and place in new array
  - increment same index in $idx$ by 1 (since that's now the new starting index for any more placed elements of that kind)

- **MSD-radix-sort** and **LSD-radix-sort** both use above sorting, but once on each digit of every element if there are multiple digits

  - **MSD** uses lots of recursions, since it calls itself on each "bucket" after partitioning (partitioning basically means sorting on one of the digits)

    - isnt stable unless it partitions (sorts) using a stable algorithm

  - **LSD** just sorts in place starting from least significant digit down

    - LSD is always **stable** since it needs to keep previously sorted digits in the right place, so it uses countsort

    - can use other algorithms, but might not be correctly sorted:

      > Imagine you had a list of {24, 23}.
      >
      > You sort by LSD.  Our first sort gives us {23, 24}.  But on our second sort, if it *wasn't* stable, it could potentially sort to {24, 23}.  This is evidently wrong.



### Binary tree

- **BST-delete**: if node has two children, find the smallest element larger than it (in right subtree), and swap with that one, then delete that one
  - that node will never have more than a right subtree, so it is ez to delete always
- **AVL tree** of $n$ nodes has $\Theta(\log n)$ height at most
  - if $N(h)$ is min number of nodes in height $h$ tree, then $N(h) = 1 + N(h - 1) + N(h - 2)$
    - root node + larger subtree + smaller subtree (subtrees cannot differ in height by more than 1)
    - use recurrence relation $N(h) > 2 N(h-  2) = 4(N(h - 4)) = ...$
  - **AVL tree deletion:** perform same as BST delete, then fix all nodes above that are violating structural property of AVL trees
  - if **AVL tree** is unbalanced after insertion/deletion, perform rotations
  - all operations are $\Theta(\log n)$



### Skip Lists

- to randomize expected runtime, define a probability $p$ where there is a $p$ chance of increasing height of tower of node being inserted
  - height of tower is number of nodes on top of base (so three nodes total in tower means height 2)
- all skip list operations are $O(\log n)$ expected runtime



### Static/Dynamic Ordering of Lists

- **Static ordering:** if you know frequency of access $f$ of each element, probability of access is $\frac f F$ where $F$ is total of all probabilities of access
  - sorting by highest to lowest probability of access gives optimal expected access cost
- **Dynamic ordering:** if you do _not_ know frequency of access $f$ of each element, use temporal locality (elements accessed is more likely to be accessed soon again)
  - **Move-to-front (MTF)**: move element to front of list when accessed
  - **Transpose:** swap element with preceding element when accessed



### Tries

- **normal trie:** represent every bit as an edge to a node, represent `$` as  edge to a leaf node that holds value of string
- **compressed trie:** compress nodes with one child as much as possible, store bits as edges still, **but** store indices as nodes to indicate which index to test next 
- **multiway trie**: instead of having binary edges leading to child nodes, have multiple children (more than 2)





| Algorithm      | Best                             | Avg                              | Worst                            | Space       |
| -------------- | -------------------------------- | -------------------------------- | -------------------------------- | ----------- |
| Quicksort      | $\Theta(n \log n)$               | $\Theta(n \log n)$               | $\Theta(n^2)$                    |             |
| Mergesort      | $\Theta(n \log n)$               | $\Theta(n \log n)$               | $\Theta(n \log n)$               |             |
| Heapsort       | $\Theta(n \log n)$               | $\Theta(n \log n)$               | $\Theta(n \log n)$               |             |
| Insertion Sort | $\Theta(n)$                      | $\Theta(n^2)$                    | $\Theta(n^2)$                    |             |
| Selection Sort | $\Theta(n^2)$                    | $\Theta(n^2)$                    | $\Theta(n^2)$                    |             |
| Bucket Sort    | $\Theta(n + R)$ for single digit | $\Theta(n + R)$ for single digit | $\Theta(n + R)$ for single digit | $\Theta(n)$ |
| CountSort      | $\Theta(n + R)$ for single digit | $\Theta(n + R)$ for single digit | $\Theta(n + R)$ for single digit | $\Theta(R)$ |
| MSD Radix Sort |                                  |                                  |                                  |             |
| LSD Radix Sort |                                  | $\Theta(m(n + R))$ m is # digits |                                  |             |
| AVL ops        |                                  | $\Theta(\log n)$                 |                                  |             |
| Skip List ops  |                                  | $\Theta(\log n)$                 |                                  |             |