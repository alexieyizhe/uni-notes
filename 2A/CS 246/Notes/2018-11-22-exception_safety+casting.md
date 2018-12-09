__CS 246 |__ Nov 22, 2018

# Exception Safety (cont.)

There are 3 levels of exception safety:

1. __Basic guarantee:__ If an exception occurs, the program will be in some valid state.
   - Nothing is leaked, class invariants must remain true,  no corrupted data structures
2. __Strong guarantee:__ If an exception is raised while executing `f()`, the state of the program will be as if `f()` had not been called.
   - Either we get all the effects of `f()` (if it runs successfully) or we get none of the effects.
3. __No-throw guarantee:__ `f()` will never throw an exception and will always achieve its purpose.
   - This means you can't just never throw and supress any exceptions, because it'll defeat the purpose.

```cpp
class A {...};

class B {...};

class C {
    A a;
    b b;
public:
    void f() {
        a.g(); // both of these may throw,
        b.h(); // but have strong guarantees
    }
}

// is C::f() exception safe?
```

`C::f()` is _probably_ __not__ exception safe:

1. If `a.g()` throws, nothing has happened yet so it's ok.
2. If `a.g()` runs successfully but `b.h()` throws, the effects of `a.g()` would have to be undone to offer the strong guarantee - which is very hard or impossible if `g()` has non-local side effects.

If `g()` and `h()` do not have non-local side-effects, we can utilize copy + swap:

```cpp
class C {
    ...
	void f() {
        A atemp = a;
        B btemp = b;
        atemp.g(); // these might still throw,
        btemp.h(); // but the original a, b are still intact
        
        a = atemp; // but wait - what if the copy
        b = btemp; // assignment operator throws?
    }
}

// the solution is the PIMPL idiom

class C {
    unique_ptr<CImpl> pImpl;
    ...
    void f() {
        auto tmp = make_unique<CImpl>(*pImpl);
        tmp->a.g();
        tmp->b.h();
        std::swap(pImpl, tmp); // this NEVER throws
    } // this is a strong guarantee for f()
}
```

### Exception Safety & the STL: `Vector`

Vectors encapsulate a heap-allocated array and follows the __RAII__ idiom - when a stack-allocated vector goes out of scope, the internal heap-allocated array is freed.

```cpp
void f() {
    vector<MyClass> v;
    ...
} 
// when v goes out of scope, the internal array is freed
// and MyClass destructor runs on all objects in the vector

void g() {
    vector<MyClass *> v;
    ...
}
// when v goes out of scope, array is freed, but
// ptrs dont have destructors so objs being pointed to
// are NOT deleted

void h() {
    vector<unique_ptr(MyClass)> v;
    ...
}
// when v goes out of scope, the internal array is freed
// and unique_ptr + MyClass destructor runs 
// AND no explicit deallocation
```

The `vector::emplace_back()` method offers the strong guarantee. If the internal array is full, three things happen:

1. **New array is allocated**: if this fails, it's the first thing we did so it's fine!
2. **Objects are copied over (copy constructor)**: if this fails, we have to _destroy the new array_ (but the old array is still intact so we're fine)
3. **Delete old array**: this never fails

However, copying is expensive. What if we replace Step $2.$  by __moving the objects over (move constructor)__ instead? If the move constructor is used and it throws, we **cannot** offer the strong guarantee since the _original is no longer intact._

If the move constructor offers the no-throw guarantee, `emplace_back()` will use the move constructor; otherwise, it uses the copy constructor (which may be slower).

> Every example in this course of a move operator has been non-throwing - you should always strive for a no-throw guarantee on all your move operators. 

If your move constructors provide the no-throw guarantee, indicate this to the compiler by using the `noexcept` keyword on your methods:

```cpp
MyClass(MyClass &&other) noexcept { ... }
MyClass &operator=(MyClass &&other) noexcept { ... }
```

If you know that a function will never throw or propogate an exception, declare it `noexcept` - this facilitates optimization. At minimum, moves + swaps should be `noexcept`s.

# Casting

In C, casting is done like so:

```cpp
Node n;
int *ip = (int *) &n; // forces C++ to treat a Node* as an int*
```

**C-style casting should be avoided in C++.** 

If you must cast, use a C++-style cast - there are 4 kinds:

1. `static_cast`
2. `reinterpret_cast`
3. `const_cast`
4. `dynamic_cast`

### Static Casting

`static_cast` is sensible casting with well-defined meanings.

- _ex. converting a `double` to an `int`_

  ```cpp
  double d;
  void f(int x);
  void f(double x);
  f(static_cast<int>(d)) // will call first f()
  ```

- _ex. converting_ `superclass_ptr` -> `subclass_ptr`

  ```cpp
  Book *b = new Text { .. };
  Text *t = static_cast<Text *>(b);
  ```

### Reinterpret Casting

`reinterpret_cast`: **unsafe**, implementation-specific, 'weird conversions'

```cpp
Student s;
Turtle *t = reinterpret_cast<Turtle *>(&s);

class C {
    int a;
public:
    int getA() { return a; }
};

class RogueC {
public:
    int a;
}

int main() {
    C val = C {10};
    RogueC val2 = reinterpret_cast<RogueC *>(&vol);
	val2->a = 20;
    cout << val2->getA() << endl; // will print 20 :0
}
```

