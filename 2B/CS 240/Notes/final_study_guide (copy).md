__CS 240 | __Final Study Guide

### Dictionaries

- Can store dictionaries via **direct addressing** where each value has its own unique key and any dictionary key $k$ is bound by $0 \leq k \lt M$

  - dictionary keys are indices and values are stored as elements in an array
  - drawbacks:
    - space is wasted if number of stored elements is less than $M$
    - keys must be integers to be able to index into array

- **Hashing**: mapping (converting) keys to a smaller integer range $m$ and then use direct indexing into an array $T$ of size $m$, known as a **hash table**

  - Use a **hash function** $h$ to map keys to the range

    - $h(k)$ is the **hash value** of a key $k$
    - must be fast $O(1)$ to compute and use all array slots equally likely

  - item with key $k$ is stored at $T[h(k)]$

  - multiple keys may match to the same hash value, this is known as a **collision**

    - 2 strategies to deal with collision:
      1. **separate chaining**: multiple items allowed at each array location in hash table
      2. **open addressing**: each item can go in multiple locations
         1. probe sequence: many alternative locations
         2. cuckoo hashing: _one_ alternative location

  - **Separate Chaining**

    - each array entry in hash table is a bucket with 0 or more KVPs
      - bucket can be implemented many different ways:
        - simplest: unsorted linked list
        - another hash table or dictionary
    - ==Operations:==
      - _search(k)_: look for $k$ in the bucket at $T[h(k)]$
        - MTF heuristic might help here
      - _insert(k, v)_: add (k, v) to bucket at $T[h(k)]$
        - MTF also says to insert at front
      - _delete(k)_: search and delete from bucket at $T[h(k)]$
      - in `worst` case, all $n$ items have keys that hash to the same index
        - search $\Theta(n)$ 
        - insert $O(1)​$
        - delete $\Theta(n)$ 
      - in _average_ case, if we assume uniform hashing ($P(h(k) = i) = \frac 1 M​$):
        - the **load factor** $\alpha​$ is $\frac n M​$, where $M​$ is size of array in dictionary implementation
        - search is $\Theta(1 + \alpha)$ 
        - insert is $O(1)​$
        - delete is $\Theta(1 + \alpha)$
        - space complexity is $\Theta(M + n) = \Theta(\frac n \alpha + n)$
      - Since complexities depend on $\alpha$, we can get avg time complexity of $\Theta(1)$ and space of $\Theta(n)$ if we maintain $\alpha \in \Theta(1)$
        - we can do so through _rehashing_ whenever $n \lt c_1 M$ or $n \gt c_2 M$, with constants $0 \lt c_1 \lt c_2 $ 
          - rearranged, it's also $\frac n M \lt c_1$, or $\alpha \lt c_1$, and vice versa
        - to maintain appropriately sized hash:
          1. start with a smaller $M$ capacity
          2. during insert/delete, update $n$
          3. if load factor becomes too large and $\gt c_2$, rehash
             1. choose new $M'$ that's larger
             2. find new hash function $h'$ that will map to $\{0, 1, …, M' - 1\}$
             3. create new hash table $T'$ of size $M'$ and reinsert all elements that were in $T$
          4. if load factor becomes too small, do the same thing but with a smaller $M'$ instead of larger
        - rehashing costs $\Theta(M + n)$ but amortized over all operations, can be ignored

  - **Open Addressing**:

    - chaining wastes space on links when we have empty space in hash table

    - Search and insert in a sequence of possible locations for a key $k$ until empty spot is found

    - **linear probing** is simplest - if $h(k)$ is occupied, place item in next open index in hash table array

      - $h(k, i) = (h(k) + i) \mod M$

      - if we delete and leave an empty spot, the next search/delete may not go far enough (search stops when empty spot is reached and not found is returned)

        - use _lazy deletion_ to mark spot as deleted, different from empty
          - _delete_ will ignore empty spots and continue, but insert will insert in empty spot

      - ==Operations==

        - _insert(k, v)_: loop through array looking for empty spots at hash values, stop at $M$ iterations

          ```pseudocode
          insert(T, (k, v)):
            for(j = 0; j < M; j++)
              if T[h(k, j)] is empty or deleted
                T[h(k, j)] = (k, v) // insert the value
                return success
              return fail_to_insert
          ```

          - if can't insert after $M$ tries, fail
            - provided load factor $\alpha \lt 1$, linear probing should always find a spot
          - if insert fails, then call rehash

        - _search(k, v)_

          ```pseudocode
          search(T, (k, v)):
          	for(j = 0; j < M; j++) 
          		if T[h(k, j)] is empty
          			return fail_not_found
          		if T[h(k, j)] has key k
          			return T[h(k, j)]
          		// if $T[h(k, j)] = deleted, ignore and keep searching
          	return fail_to_insert			
          ```

      - drawbacks to linear probing: snowball effect, entries cluster in contiguous regions, results in unnecessary probes when searching/deleting/inserting

        - to avoid, we can use _double hashing_ for open addressing with a probe sequence that determines the hash value based on two _independent_ hash functions

    - **cuckoo hashing** is alternative to linear probing

      - two separate hash tables, one hash function for each table
      - an item with key $k$ can only be at one of $T_0[h_0(k)]$ or $T_1[h_1(k)]$
        - now, _search_ and _delete_ cost $O(1)$ time
      - for _insert_ of item with key $k$: 
        1. try inserting at $T_0[h_0(k)]$
        2. if already occupied, kick out old item and place new item there
        3. place old item (with key $k_o$) at $T_1[h_1(k_o)]$ in other hash table
        4. if already occupied, kick out that item and repeat, alternating hash tables
        5. if fail to place item (tables possibly full), rehash
      - insert is slow, but constant time if load factor is small and delete/search are fast

    - ![image-20190415155437888](assets/image-20190415155437888.png)

  - **Hash Function Strategies**

    - choosing a good hash function
      - each hash index value is equally likely (very hard, if not impossible, since you have to know input distribution)
      - choose one that is unrelated to patterns in data, and depends on all parts of the key
      - we saw _modulo_ and _multiplicative_ methods
        - modulo requires $M$ be prime
    - method: **universal hashing**
      - use randomization to help avoid bad hashing
      - choose prime number $p \gt M$ and random $a, b \in \{0, …, p - 1\}, a \not= 1$
      - use as hash function: $h(k) = ((ak + b) \mod p) \mod M$
      - probability of collision using this $h$ is at most $\frac 1 M$

  - For **multi-dimensional data** that may not be integers, we may need a way to convert those to integer keys

    - ex. for a word string $w$, use a function $f(w) \in N$ where $h(w) = f(w) \mod M$

  - **Hashing** vs **Balanced Search Trees**

    ![image-20190415160918654](assets/image-20190415160918654.png)

### Multi-Dimensional Data

- store data with multiple **aspects** of interest

  - each aspect represents a dimension (one $d$-dimensional item has $d$ aspects)
  - mostly, we consider $d = 2$ (Euclidean plane)

- dictionaries for multi-dimensional data have 4 operations: insert, delete, search, and:

  - **range-search query**: specify a range for some (or all) aspects, and find items in dictionary whose aspects fall in the specified range

- **Quadtrees**: a tree where nodes represent regions

  - nodes in higher levels cover larger regions, moving further down to smaller and smaller regions until the leaves

    - each node in a level represents the same size region

  - leaves of tree represent regions small enough to store one point

  - points on split lines belong to region on top or right

  - to build:

    1. start with $n$ points $\{(x_0, y_0), …, (x_{n-1}, y_{n - 1})\}$
    2. all points lie within a square $R$ (size can be found by getting difference between max and min of x/y values)
       - root node $r$ corresponds to the range $R$
    3. if $R$ contains 0 (or 1) point, then root $r$ is empty (or has a leaf that contains 1 point)
    4. else partition $R$ into four subsquares and create a subtree for each subsquare region
    5. repeat recursively

  - ==Operations==

    - 3 possibilities for _search/insert_, we find:

      1. leaf storing the single point we were looking for (found)
      2. leaf storing a single point different from the one we were looking for (not found)
         - for _insert,_ we expand this leaf into the next level and add our leaf to the same level, so the old leaf becomes an internal node
      3. empty subtree (not found)
         - for _insert,_ replace the empty subtree with a leaf storing the inserted point

    - _delete:_ search for leaf containing the point and replace that leaf with an empty subtree

      - if the parent now has only one child, and the child is a leaf, delete the parent and make the only leaf child to be a child of its grandparent (or the root if no grandparent)

    - _range-search query_: searching for all points that fall in a query rectangle $A$

      ```pseudocode
      quadtree_rangeSearch(v = root, A):
      	let R be the square associated with v
      	
      	if R completely inside A:
      		return all points in v
      	if R intersection A is empty:
      		return 
      	if v stores a single point p:
      		if p is in A: return p
      		else return
        
        for each child w of v:
        	quadtree_rangeSearch(w, A)
      ```

      - complexity is $\Theta(\text{number of visited nodes} + \text{output size})$
        - in worst case, we visit every node, so $\Theta(nh)$ is worst case for number of visited nodes
          - worst case can still happen even if range search result is empty

  - quadtrees can have very large height if distribution of points is bad

  - use **spread factor** to measure this for set of points $S$: $\beta(S) = \frac {\text{side length of } R} {d_{min}}$

    - $d_{min}$ is smallest distance between any two points in $S$
    - height $h$ of quadtree $\in \Theta(\log \beta(S))$
    - does not depend on number of points ($n$)
    - for good performance, $\log \beta(S)$ should be much smaller than $n$

  - complexity to build tree is $\Theta(nh)$ worst case

  - other dimensions:

    - 1 dimensional: range is linear on the number scale, splitting by 2 stops once you get to a single key in the range 

      ![image-20190416145732606](assets/image-20190416145732606.png)

    - easily generalize to higher dimensions (octrees, etc) but rarely used past 3 dimensions

  - potentially uses lots of space, but good if points are distributed well

  - possible variation is to stop splitting earlier and allow some constant $k$ amount of points in one leaf (instead of just 1 point)

- **kd-trees:** split area spanned by points into regions that have an equal number of points each

  - to construct:
    - split into two regions alternating vertically/horizontally
    - sort by the axis you're splitting on, and split on the median (upper median if even # of points)
    - recurse on the two new subregions
    - continue recursing until every region has a single point
  - can construct in $\Theta(height \times n)$ time
    - when splitting, split puts $\lfloor \frac n 2 \rfloor $ points on one side, $\lceil \frac n 2 \rceil$ points on other
    - so, height of tree is $O(\log n)$  and kd-tree **can be built in $\Theta(n \log n)$ time**
    - this is if points are in **general position** (cannot share coordinates, no two points have same x-coordinate or y-coordinate)
  - space efficiency is $O(n)$ since total nodes is summed over each level (1 + 2 + 4 + … + $\frac n 2 $ + n)
  - ==Operations==
    - _search:_ like binary search tree using desired coordinate
    - _insert_: first search, then insert as new leaf
    - _delete_: first search, then remove leaf and any parent with one child left
    - for _search_, _delete_, kd-tree can be left unbalanced and split will not be in median
      - we allow for a certain amount of imbalance, and rebuild the entire tree when it becomes too unbalanced
    - _range_search_: similar to quadtrees, since every node is associated with a region
      - nodes are associated with a region through inequality ($x \lt p_4x$ is the region in the graph of all x values less than the x-coord of $p_4$)
      - **time complexity** is $O(s + \sqrt n)$ where $s$ is the number of keys found in the range (the output)

- **range trees**:

  - 2d range tree search:

    1. Perform range_search on primary tree to get _boundary_ and _allocation_ nodes (but we do not go through nodes in subtrees of allocation nodes)
       - $O(\log n)$ time since we avoid going through subtrees of allocation nodes
    2. Check boundary nodes to see if their x-coord _and_ y-coord are in range, report if so
    3. For every allocation node $v$, search in the auxiliary tree for the desired y-coord range and report those following original range_search (go through subtrees of allocation nodes)

    - time complexity: $O(s + \log^2n)$

  - ==Operations==

    - _search_: BST search in the primary tree, but check y-coord through auxiliary tree before returning point
    - _insert_: 
      1. insert by x-coord into primary tree
      2. go back through path to root and insert point by y-coord in all auxiliary trees on path
    - _delete_: same process as _insert_, but delete instead
    - problem is insert/delete very slow if using AVL-trees, since rotation at a node changes the auxiliary tree of the node and requires rebuild
      - solution: allow imbalance and rebuild when too unbalanced

  - higher dimensions:

    - following a sequence (ex. $x, y, z$), each node in a subtree of one item in the sequence will have an auxiliary tree of the next type of coordinate in the sequence
      - ex. primary tree sorted by x-coords will have nodes with auxiliary trees sorted by y-coords, and all nodes in the y-coord auxiliary tree will have auxiliary trees sorted by z-coords, etc
    - _space_ complexity of $O(n\log ^{d-1}n)$
    - _construction time_ of $O(n \log^{d - 1}n)$
    - _range query time_ of $O(s + \log ^dn)$

    

![image-20190416232618470](assets/image-20190416232618470.png)



### String Matching

- **Karp-Rabin**: move through and check if hashes match

  - hash function takes mod of number made up of digits in possible match (mod base is a large prime number)
  - recompute hash in $O(1)$ time by shifting 1 to the right so you subtract the first digit that's been shifted out and add the last digit that's been shifted in
  - expected running time of fast rehash solution is $O(m + n)$

- **Boyer-Moore**: 

  ![image-20190417000633926](assets/image-20190417000633926.png)

- **Knuth-Morris-Pratt**: 

  - computing failure array fast computation:

    - failure arc from state $j$ leads to $F[j - 1]$
    - using information from previous $F[j]$, get the failure arc and add to DFA
    - if after parsing $P[1…j]$, if we reach state $l$, then $F[j] = l$

    ```python
    def failTable(pattern):
        # Create the resulting table, which for length zero is None.
        result = [None]
    
        # Iterate across the rest of the characters, filling in the values for the
        # rest of the table.
        for i in range(0, len(pattern)):
            # Keep track of the size of the subproblem we're dealing with, which
            # starts off using the first i characters of the string.
            j = i
    
            while True:
                # If j hits zero, the recursion says that the resulting value is
                # zero since we're looking for the LPB of a single-character
                # string.
                if j == 0:
                    result.append(0)
                    break
    
                # Otherwise, if the character one step after the LPB matches the
                # next character in the sequence, then we can extend the LPB by one
                # character to get an LPB for the whole sequence.
                if pattern[result[j]] == pattern[i]:
                    result.append(result[j] + 1)
                    break
    
                # Finally, if neither of these hold, then we need to reduce the
                # subproblem to the LPB of the LPB.
                j = result[j]
        
        return result
    ```

  ![image-20190417140218566](assets/image-20190417140218566.png)



### Compression

- Types of compression:

  - _Logical_: uses meaning of data, methods will only work on data of same domain (ex. Images, sound recordings)
  - _Physical_: uses physical bits only

- Variants of compression:

  - _Lossy_: better compression ratios, but decoding is approximate and exact source cannot be found from encoding
  - _Lossless_: always decodes source $S$ exactly

- ![image-20190417145227840](assets/image-20190417145227840.png)

- **prefix-free**: no encoded value is the prefix of any other encoded value for all values in the encoded alphabet $\Sigma_S$

  - this allows encoded text to be uniquely decodable
  - represented by _tries_ with each leaf being a character in the encoded alphabet

- **encoding**: for each letter $l$ in source text, search for $l$ in the dictionary (key = source text alphabet, value = encoded alphabet) and append to encoded text

- **encoding from trie:** use prefix-free trie

  1. place all leaves into an array indexed by the character it represents (char in $\Sigma_S $ )
  2. for each letter in decoded text, get the leaf corresponding to it in array and work up to the root, prepending each 0 or 1 in the edges of the path to the root to a string
  3. return that string that now represents the encoding of that letter
  4. repeat

- **decoding from trie:**

  1. starting at root, traverse the tree based on encountered characters in encoded text until you reach a leaf
  2. add the value at that leaf to your final result
  3. repeat, starting from where in the encoded text you found a leaf, until you reach the end of the encoded text
  4. return the decoded final result

- **Huffman Algorithm**

  ![image-20190417143803016](assets/image-20190417143803016.png)

  - tries are stored during the algorithm in a min-heap (key, value) = (trie weight, link to trie)

  - step 4 = 2 `delete_min`, step 5 = `insert`

  - final trie is _not_ unique, so trie must be transmitted along with encoded text

    - since a combined trie of two smaller tries may equal the weight of a larger weight trie, and any of those can be chosen to be combined with another trie (multiple possibilities)

  - have to make 2 passes through original source text: 1 to compute frequencie, 1 to encode

    ![image-20190417144315701](assets/image-20190417144315701.png)

  - optimal in the sense that the number of nodes visited by decoding is least amongst all encodings

- **Run-Length Encoding**: used when source and encoded alphabet is both binary, runs of repeated characters are long

  - method: 

    1. give first bit of source text (either 0 or 1)
    2. give sequence of integers indicating run lengths
       - bit (0 or 1) in these runs is implied since they're alternating and you're given the starting first bit

  - to encode integers in run length sequence, use **Elias Gamma code**

    - integer $k$ = $\lfloor \log k \rfloor $ copies of 0, followed by binary representation of $k$ (always starts with 1, so separated from copies of 0)

      ![image-20190417144943061](assets/image-20190417144943061.png)

    - easy to decode

      - $m$ = 1 + number of zeroes in encoding = number of digits in binary representation of $k$
      - after zeroes, read $m$ digits to get binary representation of $k$, then convert to decimal to decode

  - no compression until run-length $k \geq 6$, opposite effect (expansion) when run-length $k = 2$ or 4

- **LZW:**

- ![image-20190417150910583](assets/image-20190417150910583.png)

- **BWT**: 

  - encoding: source text includes terminator char `$`
    1. write out all cyclic shifts of the source text (forms array of shifts)
    2. sort array lexicographically 
    3. take the last column (last character in each index) of the sorted cyclic shift array as the encoding
  - decoding: given an encoded text representing last column of sorted shifts array
    1. place in a column and label with row numbers
    2. sort with a stable sort method 
       - $O(n)$ with count sort, since number of characters is constant based on encoded text's alphabet
    3. place sorted column as first column of shifts array
    4. to find first row $r_0$ in unsorted (original) shifts array, look for row with terminator char at end
    5. add first char in $r_0$ to decoded original text
    6. match first char and row number in $r_0$ with some other last char (in last column) in a row $r_i$ in shifts array
    7. add first char in $r_i$ to decoded original text
    8. repeat steps 6 and 7 until you get full original decoded text
  - ![image-20190417152310709](assets/image-20190417152310709.png)



### External Memory

- **memory locality**: whether elements that are frequently accessed together are located together in memory

- because only some parts of data are stored on cache or registers, we want to minimize the number of blocks an algorithm has to access at any one time

  - heapsort is optimial time and space when we just had only RAM, but now accesses many blocks since it reads spread out indices of array its sorting
  - merge sort is better when accessing array stored in external memory, always accesses consecutive indices in the same block and uses entire block (sorts entire block)

- can extend `mergesort` to sort $d$ "sections" of already sorted runs

  - original `mergesort` is $d = 2$, it merges 2 sections of already sorted parts of array together

    - cost $\Theta(n)$ time for each round of merge sort

  - to extend to $d$ ways, we need a min-heap to get the smallest of all $d$ sections

    ![image-20190417160213859](assets/image-20190417160213859.png)

    - 