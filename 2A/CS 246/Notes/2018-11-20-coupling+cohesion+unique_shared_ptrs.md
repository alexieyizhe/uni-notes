__CS 246 |__ Nov 15, 2018

# Measures of Design Quality

There are two principles of design quality that we should follow: __coupling__ and __cohesion__.

###Coupling

Coupling is a measure of how much distinct program modules depend on each other. There are many degrees:

==Low==		Modules communicate via function calls with basic parameters & results
​			Modules pass arrays/structs back and forth
​			Modules affect each other's control flow
`High`		   Modules have access to each other's implementation (they are `friend`s)

### Cohesion

Cohesion is a measure of how closely elements of a module are related to each other. There are also many degrees:

==Low==		   Module is an arbitrary grouping of unrelated elements (ex. `<utility>`)
​			Module has elements that share a common theme but are otherwise unrelated
​			Module has elements that manipulate state over the lifetime of an object
​			Module has elements that pass data to each other
`High`		 Module has elements that cooperate to perform exactly __one__ task

Ultimately, our goal is to aim for ==low== coupling and `high` cohesion.



## Decoupling the Interface

Your primary program classes should not print anything:

```cpp
class ChessBoard {
    ...
    cout << "Your Move" << endl;
};
```

This is bad design and inhibits code reuse (_e.g. consider the case if you want to reuse `ChessBoard` but not have it communicate via `std::cout`_).

One solution is to give the class `stream` objects for I/O:

```cpp
class ChessBoard {
    istream &in;
    ostream &out;
public:
    ChessBoard(istream &in, ostream &out): in{in}, out{out}, ...
        
    out << "Your Move" << endl;
};
```

However, it's even better if we don't have any output in this class at all.

### Single Responsibility Principle

The__Single Responsibility Principle__ states that _a class should only have one reason to change._

In `Chessboard`, there are two: gameplay & communication. We should be commjunicating with the chessboard via params/results/exceptions, and confine user communication to be outside of the game class.

> Do __not__ communicate in `main`. It is hard, if not impossible, to reuse code in `main`.

To do so, we create a class solely for interaction that is separate from the classes responsible for gameplay. This leads to a certain architecture of design.

## Model View Controller (MVC) Architecture

In MVC, we separate the dinstinct notions of a program into three aspects:

- __Model__: the data being represented
  - Can have multiple views (_e.g. having both text and graphical output_)
  - Doesn't need to know about implementation details
  - Can implement the classic Observer ==Design Pattern==
- __View__: the presentation of the data
- __Controller__: the manipulation of the data
  - Mediates control flow between model and view
  - May communicate with the user for input (or the View could do that)



# Exception Safety

Consider the following:

```cpp
void f() {
    MyClass mc;
    MyClass *p = new MyClass;
    g();
    delete p;
}
```

This code snippet will not leak memory unless `g()` throws an error. If that happens, _all stack memory is reclaimed by running destructors_ during __stack unwinding__, but _heap allocated memory is not destroyed._ If `g()` throws, `p` is leaked but `mc` is not.

A solution might be:

```cpp
void f() {
    MyClass mc;
    MyClass *p = new MyClass;
    try { g(); }
    catch { delete p; throw; }
    delete p;
}
```

However, this is ugly and creates code duplication. The only thing you can count on in C++ is that destructors for stack allocated data will run. So, __use stack allocated destructors as much as possible.__

### Resource Acquisition Is Initialization (RAII) ==Idiom==

Every resource should be wrapped in a stack-allocated object, whose destructor deletes the object. For example, take `ifstream f{"file"};`: acquiring the resource (`"file"`) = initializing the object (`f`).

This can be done with dynamic memory using a __unique pointer.__

### Unique Pointers

The `std::unique_ptr<T>` class is found in the `<memory>` module. It takes a `T *` in the constructor, can be used/dereferenced like a normal pointer, and deletes the pointer in the destructor.

```cpp
void f() {
    MyClass mc;
    std::unique_ptr<MyClass> p{new MyClass};         // Both of these are
    auto p = std::make_unique<MyClass>( /*args*/ );  // valid options.
} // This will never leak. Guaranteed.


// However...
class C {...};

unique_ptr<C> p{new C{...}};
unique_ptr<C> q = p; // this does NOT WORK - they are UNIQUE_ptrs
```

Since the destructor always runs for a `unique_ptr`, copying it would mean always running the destructor twice which means calling `delete` twice, which will error. So, copying is disabled for `unique_ptr`s, but _moving is still allowed._

A sample implementation of `unique_ptr` would be something like this:

```cpp
template<typename T> class unique_ptr {
    T *ptr;
public:
    explicit unique_ptr(T *p): ptr{p} {}
    ~unique_ptr() { delete ptr; }
    unique_ptr(const unique_ptr<T> &other) = delete;
    unique_ptr<T> &operator=(const unique_ptr<T> &other) = delete;
    unique_ptr(unique_ptr<T> &&other): ptr{other.ptr} {
        other.ptr = nullptr;
    }
    unique_ptr<T> &operator=(unique_ptr<T> &&other) {
        std::swap(ptr, other.ptr);
        return *this;
    }
    T &operator*() { return *ptr; }
};
```

If you _need_ to be able to copy pointers, first answer the question of __ownership__: which party will have responsibility for freeing the object?

The party responsible for doing so should be a `unique_ptr`, and all other pointers should be regular pointers (you can create these from the `unique_ptr` by fetching the underlying pointer using `unique_ptr::get()`).

### Shared Pointers

If there is __shared ownership__, which is rare, then `std::shared_ptr` should be used.

```cpp
auto p1 = std::make_shared<MyClass>();

if(...) {
    auto p2 = p1;
} // p2 goes out of scope and is popped, but ptr is NOT deleted

// when p1 goes out of scope and is popped, the ptr is deleted
```

This occurs because `shared_ptr`s maintain a _reference count_ - a count of all `shared_ptr`s pointing at that specific object. When the net count reaches 0, the memory is freed.

A situation where an object is owned by two things is rare, but consider the following Racket code:

```scheme
(define l1 (cons 1 (cons 2 (cons 3 empty))))
(define l2 (cons 4 (rest l1)))
```

In memory, this code looks like this:

`l1`: `1`  — a —> `2`  — b —> `3`

`l2`: `1` — c ———^

In Racket, this is easy to do. In C, maintaining a relationship like this is a nightmare. However, in C++, this is possible if we make $a$ and $b$ in the example above `shared_ptr`s.

Use the type of pointer that accurately reflects the pointers ownership role. This dramatically reduces the opportunity of a memory leak.