__CS 246 | __Oct 23, 2018

# Design Patterns

Certain programming problems arise often and we use __design patterns__ to keep track of solutions to these problems for reuse and mass adoption.

### Iterator ==Pattern==

**Problem:** Recall the `LinkedList` class from last lecture: we can't trust the user to create `Nodes`, but solving that means we can't access existing `Nodes` efficiently. 
**Solution:** Create a class that manages access to nodes efficiently but still prevents clients from accessing pointers directly.

> Essentially, we create an abstraction of a pointer and walk the list without exposing the actual pointers.

For the above `LinkedList`, we implement the following improvements:

```cpp
class List {
    struct Node;
    Node *theList = nullptr;
public:
    class Iterator {
        Node *p;
    public:
        explicit Iterator(Node *p): p{p} {}
        int &operator*() { return p->data; }
        Iterator &operator++() { p = p->next; return *this; }
        bool operator!=(const Iterator &other) { return p != other.p; }
    };
    
    Iterator begin() { return Iterator{theList}; }
    Iterator end() { return Iterator{nullptr}; }
    
    ...
}

// Client code utilizing Iterator
int main() {
    List l;
    l.addToFront(1);
    l.addToFront(2);
    l.addToFront(3);
    
    for(List::Iterator it=l.begin(); it != l.end(); ++it) {
        cout << *it << endl; // this loop is linear O(n) time!
    }
}
```

### Automatic Type Deduction

```cpp
auto x = y;
```

The above code declares `x` to be the same type as its initializer (will be same type as`y`, in this case).

For the `List` and `Iterator` example:

```cpp
// long version
for(auto it = l.begin(); it != l.end(); ++it) {
    cout << *it << endl;
}

// shortcut
for(auto n:l) {
    cout << n << endl;
}
```

This shortcut is available for any class with:

1. Methods `begin()` and `end()` that produce iterators
2. The iterator must support `!=`, prefix `++`, and unary `*`

Note that the shortcut produces a copy - to iterate with references instead:

```cpp
for(auto &n:l) { // just declare it as references!
    ++n
}
```

### Back to Encapsulation

In the `List` example, the client cannot create iterators since it cannot have `Node` pointers _except for one_:

```cpp
auto it = List::Iterator{nullptr};
```

which violates encapsulation (since it's the same as `end()`, if we change `end()` then this might break stuff). 

One option is to make `Iterator`'s constructor `private`, but now `List` cannot call it either. So, we give `List` privileged access to `Iterator` by making it a `friend`. 

```cpp
class List {
    ...
public:
    class Iterator {
        Node *p;
        explicit Iterator(Node *p);
    public:
        ...
        friend class List;
    }
}
```

Now, `List` can still create `Iterator`s, but the client can only create `Iterator`s by calling `begin()` or `end()`.

> Even knowing this, classes should be introverts: give them as few friends as possible since it *weakens* encapsulation.

For a better way to provide access to `private` fields, you want to write __accessor__ and __mutator__ methods.

```cpp
class Vec {
    int x, y;
public:
    ...
    int getX() const { return x; } // accessor
    void setY(int z) { y = z; } // mutator 
}
```

For `operator<<`, it can't be a member (would put ostream on right side, weird syntax) but still needs `x, y`. Just declare it as a `friend` function!

```cpp
class Vec {
    ...
    friend std::ostream &operator<<(std::ostream &out, const Vec &v);
}
```



# System Modelling

When working collaboratively, it's helpful to visualize the structure of the system - like abstractions and the relationships between them - to aid design and implementation.

### Unified Modelling Language (UML)

| Ver                                    | _Name_ |
| - | - |
|`-x: Integer`<br />`-y: Integer`| _Fields (optional)_ |
|`+getX: Integer`<br />`+getY: Integer`| _Methods (optional)_ |

The `-` and `+` represent private and public visibility, respectively.