__CS 246 |__ Nov 6, 2018

# Templates

> This is a huge topic - we'll cover just the highlights.

Recall the `List` class:

```cpp
class List {
    struct Node {
        int data;
        Node *next;
    };
    
    Node *theList;
    ...
}
```

We want to be able to store more types than just `int`s in a `List` (_ex. storing a List of Lists, or a List of strings_). This is where we use a __template__ - a class parameterized by a type.

```cpp
template <typename T> class Stack {
    int size, cap;
    T *contents;
public:
    Stack(){...}; // regular ol constructor
    void push(T x) {...}
    T &top() {...}
    void pop() { ... }
    
    ...
};

// OR a List class

template <typename T> class List {
    struct Node {
        T data;
        Node *next;
    };
    
    Node *theList;
public:
    
    class Iterator {
        ...
    public:
        T &operator*() {...}
    };
    
    T &ith(int i) {...}
    void addToFront(T n);
    
	...
};

// and to use in the client...
List<int> l1;
List<List<int> l2;
l1.addToFront(3);
l2.addToFront(l1);

for(List<int>::Iterator it = l1.begin(); it != l1.end(); it++) {
    cout << *it << endl;
}

for(auto n:l1) cout << n << endl;
```

The compiler "specializes" templates at the source code level, before compilation. The compiler writes a brand new class, substituting the new type for `T` at every occurrence.

When writing template classes, you _must_ ==write the implementation and the declaration in the same `.h` file== - this is the only way that the compiler can write classes for you since it needs to know everything about the class to do so!

# The Standard Template Library (STL)

The STL contains a large number of useful templates.

For example, _dynamic-length arrays_ can be found in the STL as __vectors__.

### Vectors

```cpp
#include <vector>
std::vector<int> v{4, 5} // 4, 5
v.emplace_back(6); // 4, 5, 6
v.emplace_back(7); // 4, 5, 6, 7
```

> _Lushman says:_ If you're using heap-allocated arrays now, you're doing stuff wrong. From now on, use `vector`!

> Funky behaviour: `vector<int> v(4, 5);` will initialize `v` to be $5, 5, 5, 5$ (4 occurrences of $5$)

#### Looping over vectors

```cpp
for(int i = 0; i < v.size(); i++) {
    cout << v[i] << endl;
}
       
                 // lowercase i instead of uppercase!
for(vector<int>::iterator it = v.begin(); it != v.end(); it++) cout << *it << endl;

for(auto n:v)  cout << n << endl;

// iterate in reverse (cannot use auto, it will always call the forward iterator)
for(vector<int>::reverse_iterator it = v.rbegin(); it != v.rend(); it++) ...
    
// remove last element, does not return it
v.pop_back(); 
    
// remove first element
auto it = v.erase(v.begin()); // returns iterator pointing at first item after the point of erasure

// remove element n
it = v.erase(v.begin() + 3); // erases the 4th element
it = v.erase(it); // erases the 5th element in this case

it = v.erase(v.end() - 1); // erases the last item

// safely access the ith element
v.at(i);
```



# Exceptions

In C, handling errors is done through one of two ways:

1. Return a status code: _this doesn't work well with functions that need to actually return something_
2. Set a global variable `errno`

Both these solutions suffer from the same problem: errors are easy to ignore. Good coding practice would require lots of error checking through if statements and awkward programming, which means this encourages programmers to not practice error checking.

In C++, when an error condition arises, the function __raises an exception.__ An exception can be thought of as a class.

By default, _execution stops_ if this happens. However, you can also deal with the error by writing __handlers__ to __catch exceptions__.

```cpp
#include <stdexcept>

...
    
try {
	cout << v.at(10000);
    ... // only continue if previous line succeeds
} catch (out_of_range r) {
    cerr << "Range error: " << r.what() << endl;
}



void f() {
    throw out_of_range{ "I AM ERROR" };
}

void g() { f(); }
void h() { g(); }

int main() {
    try {
        h();
    } catch(out_of_range) { ... }  // if we don't use the error, we don't have to name it (like out_of_range r)
}
```

Control goes back through the call chain (__unwinds__ the stack) until a handler is found. If no matching handler is found, then the program terminates. A handler can do part of the recovery job by executing any corrective code it needs and throwing another error.

```cpp
try { ... }
catch(SomeErrorType s) {
    ... // recovery code
    throw; // option 1: actual type of s is retained
    throw s; // option 2: throws a new exception of type SomeErrorType (may slice s if s is a subclass of SomeErrorType)
    throw SomeOtherError { ... } // option 3: throw a different error completely
}
```



