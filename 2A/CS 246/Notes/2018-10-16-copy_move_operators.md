__CS 246 |__ Oct 16, 2018

# Copy Assignment Operator

__How can we improve the copy assignment operator?__

```cpp
// Attempt 2
Node& operator=(const Node& o) {
    if (this == &o) return *this;
    delete next;
    next = o.next ? new Node{ *o.next }: nullptr;
    data = o.data;
    return *this;
}

// Attempt 3: It's better to create the copy first, then delete it
Node& operator=(const Node& o) {
    if (this == &o) return *this;
    Node *tmp = next;
    next = o.next ? new Node { *o.next }: nullptr;
    data = o.data;
    delete tmp; // destructor
    return *this; //if new fails, Node still holds the old data
}

// Attempt 4: Use this copy-and-swap idiom to achieve the advantages of this version more concisely
#include <utility>
struct Node {
    ...
    void swap(Node& o) {
        using std::swap;
        swap(data, o.data); // this is the std::swap function
        swap(next, o.next);
    }
}

Node& operator=(const Node& o) {
    Node tmp{o}; // calls the copy constructor
    swap(tmp);
    return *this;
    // tmp is deleted once it goes out of scope
}
```



# Rvalues and rvalue references

> Recall: 
>
> - An lvalue is a value with a previously assigned reference
> - An lvalue reference (`&`) is like a `const ptr` with automatic dereferencing; it is always initialized to an lvalue

```cpp
Node n {1, new Node { 2, nullptr } };
Node m = n; // copy constructor
Node m2;
m2 = n; // copy assignment operator

Node plusOne(Node n) {
    for (Node* p = &n; p; p = p->next) {
        p.data++;
    }
    return n;
}

Node m3 = plusOne(n); // copy constructor is called here
```

**In the above example, what is `other` in `m3`'s case?'**
`other` is an lvalue ref, but the address of the object it points at is not immediately clear. In reality, the compiler creates a temporary object to hold the result of `plusOne(n)` and `other` is a ref to this temp. object. Then, the copy constructor makes a deep copy of this temporary object and assigns it to `m3`.

However, it's wasteful to have to create a tmp obj and then copy from it - let's steal from it instead!

We need to know if the parameter is temporary or a separate 'standalone' object.

# Move Constructors/Assignment Operators

In C++, an __rvalue reference__ of type `Node&&` is a reference to a temporary object of type `Node`. We can write a constructor that takes a `Node&&`:

```cpp
struct Node {
    ...
    // this is a move constructor!
    Node (Node && o): data{ o.data }, 
        next{o.next} {
			o.next = nullptr; // o.next so that the data we stole is not deleted when o is deleted
        }
    }
}

// Similarly:
Node m;
m = plusOne(n); // assignment from a tmp

Node& operator=(Node&& o) {
    using std::swap;
    swap(this->data, o.data);
    swap(this->next, o.next);
    return *this; // o goes out of scope and deletes our data
}
```

If you don't define a move constructor/assignment operator, the copy versions are used.

If the move constructor/move assignment operator is defined, it will replace all calls to the copy constructor/copy assignment operator where the argument is a temp (rvalue). The compiler takes care of this.

