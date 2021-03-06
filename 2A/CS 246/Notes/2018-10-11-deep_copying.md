__CS 246 | __Oct 11, 2018

# C++ Copy Constructor

Consider the following copying method:

```cpp
Node *n = new Node {1, new Node {2, new Node {3, nullptr }}}
Node m = *n;
Node *p = new Node { *n };
```

If we want a _deep copy_ that copes the entire list, we have to write our own copy constructor.

```cpp
struct Node {
    ...
    Node(const Node &other): data{other.data},
    	next { other.next ? new Node {*other.next} : nullptr } {}
};
```

This process is _recursive_, since `new Node { *other.next }` is another call to the copy constructor (a form of recursion) - this allows us to copy every `Node` in the list.

The **copy constructor** is called:

1. When an object is initialized by another object of the same type
2. When an object is passed by value
3. When an object is returned by value from a function

>  Sidenote: postfix operators always take precedence over prefix operators in C++.

Be careful with constructors that can take _one_ parameter like so:

```cpp
struct Node {
    ...
    Node (int data): data {data}, next {nullptr} {}
};

Node n{4}; // this is fine
Node n = 4; // this is also fine - is this intended behaviour?
```

This can create _implicit conversions_ from one type to another. In the above, `4` is implicitly converted from `int ` to `Node`.  This is __dangerous__ because it is silently converted and the compiler will not error:

```cpp
int f(Node n);
f(4); // this will work and compile, which is often not intended
```

To _disable the implicit conversion_, we want to make the constructor explicit:

```cpp
struct Node {
    ...
    explicit Node (int data): data {data}, next {nullptr} {}
};

Node n{4}; // this is still fine
Node n = 4; // this will error
f(4); // this will error
f(Node {4}); // this is also fine
```

This is much safer, since we have to explicitly define a `Node`.



# Destructors

When an object is destroyed (for _stack-allocated_: when it goes out of scope, for _heap-allocated_: when it's deleted):

1. Destructor body runs 
   - classes always come with a destructor that just calls destructors on all fields that are objects
2. Fields' destructors invoked in reverse declaration order (for fields that are objects)
3. Space in memory is deallocated

#### When do we need to write a destructor? 

```cpp
Node *np = new Node { 1, new Node { 2, new Node { 3, nullptr }}};
```

If `np` goes out of scope, `np` is reclaimed (since its stack-allocated) but all 3 `Node`s are leaked (they are heap-allocated).
If we call `delete np`, it calls `*np`'s destructor, which does nothing.

We write a destructor ourselves to ensure the entire list is freed:

```cpp
struct Node {
    ...
    ~Node() { delete next; }
};

delete np; // will now free the whole list
```

This is also done _recursively._

# Copy Assignment Operator

```cpp
Student billy {70, 80, 90};
Student jane = billy;
Student joey; // default constructor
joey = billy; // copy but not a construction, it's the built-in copy assignment operator
```

We want to write our own:

```cpp
struct Node {
    ...
    Node &operator=(const Node &other) { // no MIL bc this is not a constructor
        data = other.data;
        delete next; // since this is assignment, we assume it has existing ptrs
        next = other.next ? new Node{ *other.next } : nullptr;
        
        return *this;
    }
}
```

but once again, this is also __DANGEROUS__:

```cpp
Node *np = new Node { 1, new Node { 2, new Node { 3, nullptr }}};

// uh oh
n = n; // yikes
```

This will delete `n` and then try to copy `n` to `n` (which is __undefined behaviour__). 



So we amend the above:

```cpp
struct Node {
    ...
    Node &operator=(const Node &other) {
        if (this = other) return *this;
        ... // same as above
    }
}
```







