**CS 246 |** Sept 27, 2018


# Dynamic Memory Allocation
This is how we allocated memory in C:
```c
int *p = malloc( SOME_TYPE * sizeof(int))

...

free(p);
```

Do not use this in C++. Instead, use `new` or `delete`:
```cpp
struct Node {
  int data;
  Node *next;
};

Node *np = new Node;

...

delete np;
```

 - all local vars reside on the **stack**, and deallocate when they go out of scope.
 - allocated memory resides on the **heap**, and remains allocated until delete is called
 - if you don't delete all allocated memory, a **memory leak** happens!


### Allocating Arrays on the Heap

Memory allocated with `new` must be deallocated with `delete`, and the same for `new[...]` and `delete []` - mixing these is **undefined behaviour**.

```cpp
Node *nodeArray = new Node[10];

...

delete [] nodeArray;
```

If you want a function that gives you a new node, you can either:
 - return by value (expensive, the node is copied to caller's stack frame on return)
 - return a pointer (**BAD**, gives ptr to stack-allocated data, which is dead after return)
 - return a pointer to heap data allocated by `new` (OK, but don't forget to `delete` it after)

Which one should you use? **Return by value**. It's not as expensive as it looks (more on this later).


# Operator Overloading
We can give meaning to C++ operators for types we create.
```cpp
struct Vec {
  int x, y;
};

Vec operator+(const Vec &v, const Vec &v2){
  Vec v { v1.x + v2.x, v1.y + v2.y };
  return v;
}

Vec operator*(const int k, const Vec &v){
  return { k * v.x, k* v.y };
  // works bc the compiler knows it's a Vec based on return type
}

// Reuse code to allow for commutativity
Vec operator*(const Vec &v, const int k){
  return k * v;
}
```


### Overloading I/O Operators
Sometimes we want to work with custom types (e.g. grades).
```cpp
struct Grade {
  int theGrade;
  // struct wrapper allows for overloading
};

ostream &operator<<(ostream &out, const Grade &g){
  out << g.theGrade << '%';
  return out;
}

istream &operator>>(istream &in, Grade &g){
  in >> g.theGrade;
  if(g.theGrade < 0) g.theGrade = 0;
  if(g.theGrade > 100) g.theGrade = 100;
  // allows for additional manipulation straight from IO

  return in;
}
```



# The Preprocessor
The preprocessor transform the code before passing it to the compiler. It sees **preprocessor directives** like:
 - `#include` allows for additional code to be placed before your file contents

   - in C++, you can **include old C headers** using different names (`<cstdio>` instead of `stdio.h`)
 - `#define VAR VALUE` sets a preprocessor variable `VAR` where all occurrences of it are replaced by `VALUE`
   - obsolete; used ages ago when computing power for looking up a constant was expensive
   - defined constants are **still useful** for conditional compilation:
      ```cpp
      #define SECURITY_LEVEL 1
      #if SECURITY_LEVEL == 1
        short int
      #elif SECURITY_LEVEL == 2
        long long int
      #endif
        publickey;
      ```
  - can also define symbols via compiler arguments
    ```cpp
    int main() { // in define.cc
      cout << x << endl;
      // x is undefined D:
    }
    ```
    - if we then run `g++14 -DX=15 define.cc -o define` and `./define`, we will get `15` as output.
    - you can define more variables on the command line to configure debug output, etc.
