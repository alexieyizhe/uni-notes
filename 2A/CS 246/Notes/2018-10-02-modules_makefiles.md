**CS 246 |** Oct 2, 2018


# Separate Compilation
We want to split programs into __modules__, which provide:
 - __interface__: type definition, prototypes for functions
 - __implementation__: full definition for all provided functions

Note that an entity can be declared many times, but defined at most __once__.

```cpp
// interface (vec.h)
struct Vec {
  int x, y;
};

Vec operator+(const Vec &v1, const Vec &v2);
int globalNum; // is this the best place to put this?

// implementation (vec.cc)
...
```
However, in the above example, we defined `globalNum` in the _interface_, which will not allow it to be defined in the _implementation_.

Using an interface allows us to abstract, but will throw errors like `undefined reference to main` when we try to compile either the interface or the implementation.

To __compile separately__: use the `-c` flag when compiling
 - Produces an object file (`.o`)
 - Call `g++14` with multiple `.o` files to link them into an executable

# Dependencies
In the above example, if we change:
 - `vec.cc`, we need to recompile `vec.cc` and relink
 - `vec.h`, we need to recompile _both_ `vec.cc` and `main.cc`, and then relink

This does not scale well. To help us keep track of dependencies and perform minimal recompilation, we use a Linux tool called `make`.

A __Makefile is required__ to specify which files depend on which other files.

_Ex. A sample `Makefile`_
```Makefile
main: main.o vec.o
  g++ main.o vec.o -o main
main.o: main.cc vec.h
  g++ -std=c++14 -c main.cc
vec.o: vec.cc vec.h
  g++ -std=c++14 -c vec.cc

.PHONY: clean

clean:
  rm *.o main
```
The first words are the targets for building, and the `clean` cleans up the directory.

> Make 100% sure that the indents are __tabs, NOT spaces__.

`make` will intelligently recompile the files that have changed and their dependencies, and relink for you.

`make TARGET` will build the requested target (default is the first target)
 - `make clean` in the above example will run the clean command in the `Makefile`.

We can _generalize the Makefile_ using variables, and `Makefile` becomes:
```Makefile
CXX = g++ // compiler name
CXXFLAGS = -std=c++14 -Wall -g // compiler options
OBJECTS = main.o vec.o
EXEC = main

${EXEC}: ${OBJECTS}
  ${CXX} ${CXXFLAGS} ${OBJECTS} -o ${EXEC}

main.o: main.cc vec.h

vec.o: vec.cc vec.h

.PHONY: clean

clean: rm *.o ${EXEC}
```
Note that you can omit the recipes from each target; `make` is smart enough to infer this from the recipe for the first target.

However, the hardest part of writing the `Makefile` is still writing dependencies and keeping them up to date. `g++` can help with that: `g++ -MMD -c vec.cc` will create `vec.o` and `vec.d`, a dependency file of sorts.

The final optimized `Makefile`:
```Makefile
CXX = g++ // compiler name
CXXFLAGS = -std=c++14 -Wall -g -MMD // compiler options
OBJECTS = main.o vec.o
DEPENDS = ${OBJECTS:.o=.d}
EXEC = main

${EXEC}: ${OBJECTS}
  ${CXX} ${CXXFLAGS} ${OBJECTS} -o ${EXEC}

-include ${DEPENDS}
```

### Duplicate Dependencies
Including a dependency file more than once can and will cause problems if you include something that can only be defined once (_ex. structure definitions_).

Use an __include guard__:
```cpp
// vec.h
#ifndef VEC.H
#define VEC.H
...
everything you would include
...
#endif
```
This means vec.h is only defined if it has not been already.

> __ALWAYS__ put include guards in `.h` files
> __NEVER__ put `using namespace std` in `.h` files
> __NEVER__ compile `.h` files
> __NEVER__ include `.cc` files


# Classes
A __class__ is essentially a `struct` type that can contain functions:
```cpp
// student.h
struct Student {
  int assns, mt, final;
  float grade();
};

// student.cc
#include "student.h"

float Student::grade() {
          // ^^ scope resolution operator
  return assns * 0.4 + mt * 0.2 + final * 0.4;
}

// Client file
Student s { 60, 70, 80 };

cout << s.grade() << endl;
```
 - There is a `class` keyword in C++ (more on that later)
 - An __object__ is an instance of a class
 - The function `grade()` is called a __member function__ or __method__
    - The `Student::` syntax is a scope resolution operator that tells us that `grade()` belongs to the `Student` class
    - A member function/method can only be called with an object of that class
    - A member function/method has a hidden parameter `this` that is a _pointer_ to the object that the method is being invoked upon
