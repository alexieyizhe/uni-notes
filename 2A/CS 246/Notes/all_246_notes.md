**CS 246 |** Sept 13, 2018

# Intro to the Shell

The **shell** is the **interface to the OS** and your method of allowing the OS to perform tasks like running programs, managing files, etc. You can interact with a shell through:

- A **graphical** interface (click, touch)
  - Having a UI is easier to reason with
- A **command line** interface (typing commands at a prompt)
  - More versatile, powerful, but a bit more clunky

This course uses **bash** (**B**ourne **A**gain **SH**ell).

### The Basics

- A **directory is just a special type of file**, so when we refer to ‘files’ in this course, we include directories in that definition as well.
- Every line of a valid text file must end with a newline char (`\n`), INCLUDING THE LAST LINE (Marmoset will check for this so include it so you don’t fail all your tests lol).

### Shell Commands

- `cat file.txt` passes the name of the file as an argument, and cat opens the file and displays it, but `cat < file.txt` has the file being opened by the shell, which passes the contents to cat as input
- <kbd>CTRL</kbd>+<kbd>D</kbd> sends an EOF signal to the program to indicate that there is no more input, <kbd>CTRL</kbd>+<kbd>C</kbd> kills the program immediately.
- A globbing pattern (*e.g.* `*`) is a shell capability that matches text based on patterns like the wildcard operator. These aren’t regex, just a functionality implemented by the shell.
- Using piping hands output to another __program__ or __utility__; output redirection passes output to another __file__ or __stream__.
- Use `$(CMD_NAME)` to embed commands inside others
- `"double quotes"` group stuff together, `'single quotes'` completely supresses any commands inside

### Process Streams

Every running process is attached to 3 streams which are (by default): `stdin`, `stdout`, `stderr`.

`stderr` is a separate output stream for error messages:

- Allows for intended output to be separated from unintended error messages
- Displays messages in stream instantly, is not buffered compared to other streams
- Use 2> to redirect error output just like regular output redirection





**CS 246 |** Sept 18, 2018

# Shell Scripting

A shell script is a series of shell commands (`bash` or otherwise) contained in a file that can be run all at once.

- write `#!/bin/bash` at the top to denote a bash script (the shell will look in all the `PATH`s it knows to find a bash executable to run the script)

### Syntax

__Arguments:__

- Access specific arguments passed in on the cmd line through `$1`, `$2`, etc.
- `$#` denotes number of arguments
- `$*` gives all arguments

__If Statements:__

```bash
if [ $1 -neq "pass" ]; then
  echo "you fail"
elif [ $1 -eq "probation" ]; then
  echo "oh it gets worse"
else
  echo "ok another chance"
fi
```

- Note that the spaces in the statement ` [ ... ] ` are mandatory as the brackets are aliases for the `test` command, so they are commands themselves.

__Loops:__

```bash
for i in {START_VAL..END_VAL..STEP_VAL}; do
    echo "$i is inclusive"
done

for var in ~/Documents/*.txt; do
  echo $var
done

for output in $(COMMAND); do
  echo $output
done
```

__Functions:__

```bash
some_fn () {
  echo "this function is called a subroutine in bash"
  exit 0
}

some_fn # call the function
```

__Misc:__

| Syntax      | Usage                |
| ----------- | -------------------- |
| `exit`      | quits program        |
| `-a`        | && for statements    |
| `-o`        | \|\| for statements  |
| `-e FILE`   | T if file exists     |
| `-z STRING` | T if string len is 0 |
| `=`         | == for strings       |
| `-eq`       | ==  for ints         |
| `-ne`       | !=  for ints         |
| `-lt`       | <   for ints         |
| `-le`       | <=  for ints         |
| `-gt`       | >=  for ints         |
| `-ge`       | >=  for ints         |





**CS 246 |** Sept 20, 2018

# Testing

Testing all the code you write is a good way of checking for faulty or logically incorrect sections. It doesn't magically fix your code, but can catch more semantic errors than compiler syntax errors, for example.

__Tips 4 Testing__:

- Write smaller unit tests (only evaluate a single logical section of your code)
- Check __edge cases__, __corner cases__ (when multiple cases are at extremes), __random values__, etc

> Personal tip: read through a question multiple times, writing down all possible edge cases or things that might help to test.

# C++

### Brief Intro

C++ introduced many new ideas to the familiar C, most famous of all being OOP concepts (hence the ++ in the name). It has many different standards and versions, with CS246 using C++14. this is also why you can use C libraries, run C code/programs in C++ without a problem.

### Diving Deeper

- Uses the `.cc` file extension
- Must be __compiled__ before being executable
  - CS246 uses the `g++` compiler (*e.g.* `g++14 file_to_compile.cc -o compiled_prog` to compile)

## I/O

### Working With I/O

I/O is done through `#include <iostream>`, which allows us to use:

- __std:cin__ (`>>`): reads input from `stdin`; like `scanf` in C

  - `cin` is implicitly converted into a __boolean__ and set to 0 if bad input or EOF is encountered

  - Reads all chars until whitespace is encountered and ignores multiple whitespace

    - Use `getline(cin, s)` if whitespace needs to be preserved

  - Use `cin.eof()` to see if EOF has been reached

  - Use `cin.fail()` to see if a read has failed

  - __IMPORTANT:__ reads will keep failing until you `cin.clear()` the fail flag and remove the char that caused the read fail by using `cin.ignore` because it doesn't skip the problematic character!

  - `>>` is also C’s right bitshift operator, except when the LHS is cin

  - `cin >> i` reads a value into `i` and __returns `cin`__

    - This means you can chain `cin` calls `cin >> x >> y >> z;` (like Promises in JavaScript)

  - All the properties of `cin` allow you to simplify code like:

    ```cpp
    int main() {
      int i;
      while (true) {
        cin >> i;
        if(cin.fail()) break;
    
    	 cout << i << endl;
      }
    }
    ```

    into

    ```cpp
    int main() {
      int i;
      while (cin >> i) {
         cout << i << endl;
      }
    }
    ```

- __std::cout__ (`<<`) writes to `stdout`; prints to bash in most cases

- __std::cerr__ (`<<`) similar to `cout` but writes to `stderr`

### Manipulation

I/O manipulators __change the formatting of output__ for the entire program after it is used.
`cout << hex << 95 << endl;` will cause 95 and all subsequent integers to be printed in hex.
`cout << dec;` will return the output to printing in decimal values.
`endl` itself is a manipulator - in addition to printing a `\n` character, it will also flush the buffer.
For more manipulators, look into `#include <iomanip>`

## Strings

A comparison between C and C++:

| C Strings                                         | C++ Strings                                      |
| ------------------------------------------------- | ------------------------------------------------ |
| stored in char arrays                             | stored as a `string` type                        |
| forces writer to manage memory                    | dynamically change their size                    |
| requires a null terminator to properly signal EOS | no null terminator required, safer to manipulate |

- Use by including `#include <string>`
- Define with `string s = "hello";`
- Note that this string is __still a C-style string__ (_i.e._ a char array), but a C++ string is created from the C string on initialization

### String Operations

| Operation                  | Syntax                              |
| -------------------------- | ----------------------------------- |
| Equality/Inequality        | `s1 == s2`/`s1 != s2`               |
| Comparison (lexicographic) | `s1 <= s2`/`s1 >= s2`               |
| Length                     | `s1.length() // O(1) efficiency !!` |
| Extracting Chars           | `s[0]`, `s[20]`, _etc_              |
| Concatenation              | `s3 = s1 + s2`, `s4 += s3`          |

_and more!_

### Details

To attach a stream to a string and use it for R/W with the string, use `#include <sstream>`, which will give you:

- the __std::istringstream__ type to read from a string
- the __std::ostringstream__ type to write to a string

`Ex.` converting between strings and ints:

```cpp
string intToString(int n) {
	ostringstream sock;
	sock << n;
	return sock.str();
}

int stringToInt(string s) {
    int n;
	istringstream sock{s};
	sock >> n;
	return n;
}
```





**CS 246 |** Sept 25, 2018

# C++ (cont.)

## Files

To work with files, use `#include <fstream>` to gain access to:

- the __std::ifstream__ type to read from a file
- the __std::ofstream__ type to write to a file

_E.g._ file I/O

```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
	ifstream f {"file.txt"}; // opens file when initialized with filename
	string s;
      while (f >> s) {
	     cout << s << endl;
      } // file is automatically closed when the ifstream (f) goes out of scope
}
```

<br/>

> Anything that you can do with cin/cout, you can do with an `ifstream`/`ofstream`.

## C++ Details

### Default Function Parameters

C++ allows parameters to be optional and a default parameter to be used for when you leave out a param.

```cpp
void printFile(string name="file.txt") {
	ifstream f{name};
	string s;
	while (f >> s) cout << s << endl;
}
```

Optional parameters must be the last `n` parameters!

### Overloading

C++ allows functions with different parameter lists to have the same name. For example, two functions that negate an integer and a boolean respectively can both have the function name. This is __based on the number and the types of arguments in the function call__, so two functions that overload must __differ__ in at least one of the two.

_E.g._ the + operator accepts various types of arguments.

### Structs

While defining and initializing structs, you no longer have to write syntax like `struct Node * next;` instead, you can just write `Node * next;`

### Constants

`const int maxGrade = 100;`

- Must be initialized
- Declare as many variables as const as permitted (helps with catching errors)

### Parameter Passing

Passing a variable by value into a function will hand over a copy of the variable and __leave the original unfazed__ by any changes to it in the function. If you did want to mutate the original variable, you must pass the memory address instead of the value itself.

But why `cin >> x` and not `cin >> &x` ? Because C++ has another ptr-like type - __references__.

### References

References are like __constant ptrs with automatic dereferencing__. Consider the example:

```cpp
int y = 10;
int &z = y;
```

An lvalue is a value that has already been initialized previously (being on the LHS of a line). In this case, `z` is an __lvalue__ reference to y.  If we try to get the address of `z` or set the value of `z`, it sets the value of `y` instead. In all cases, `z` behaves exactly like `y` - essentially, it is an alias for `y`.

You __cannot__ do the following with references:

- Leave them uninitialized
- Initialize them to a value that does not have an address (ex. `int &x = 3`; or `int &x = y + z;`)
- Create a pointer to a reference
  - a reference to a pointer is fine though
- Create a reference to a reference
  - __WARNING:__ this will compile, but is syntax for something different - be careful!
- Create an array of references

You __can__ do the following with references:

- Pass them as function parameters
  - useful for keeping the speed of pass-by-value while not needing to dereference every time you use it in the f'n
- Set a reference to const
  - useful in same case as above but with the added requirement of the f'n not modifying the value  
  - also allows you to pass in values that are not normally lvalues - so:
    - for `if int g(const int &n) {...}`, `g(5)` is valid even though `5` is not an lvalue





**CS 246 |** Sept 27, 2018

# Dynamic Memory Allocation

This is how we allocated memory in C:

```c
int *p = malloc( SOME_TYPE * sizeof(int))

...

free(p);
```

Do not use this in C++. Instead, use `new` and `delete`:

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



**CS 246 |** Oct 3, 2018

# Debugging

This courses uses __Valgrind__ as a test suite (_Marmoset_). Valgrind checks for memory leaks.

### Valgrind

- Invoke using `valgrind VALGRIND_ARG ... PROG_NAME PROG_ARG ...`
- Valgrind will report memory as __definitely lost__, __possibly lost__, __indirectly lost__, and __still reachable__
  - _indirectly lost_ means first pointer is lost
  - _still reachable_ means valid pointer found right before program terminates



**CS 246 |** Oct 4, 2018

# Classes (cont.)

`assns`, `mt`, `final` inside of `Student::grade` are fields of the _current_ object - the object upon which `grade` was called.

`Ex.`

```cpp
Student billy { ... }
billy.grade();  // uses billy's assns, mt, final
```

Methods take in an _extra hidden parameter_ called `this`, which is a pointer to the object on which the method was called.

We can write methods on the class itself:

```cpp
struct Student {
  ...
  float grade() {
    return (this->assns * 0.4) + (this->mt * 0.2) + (this->final * 0.4);
  }
  // impls should be put in .cc files
};
```

### Initializing Objects

C struct initialization like `Student billy{70, 80, 90};` is ok, but limited.
A _better way to initialize objects_ is to write a constructor method that does it:

```cpp
struct Student {
  int assns, mt, final;
  float grade();
  Student(int assns, int mt, int final);
};

Student::Student(int assns, int mt, int final) {
  this->assns = assns;
  this->mt = mt;
  this->final = final;
}

// you can then call it like so:
Student billy{70, 80, 90};
```

This replicates the functionality of the built-in initialization, but allows us to do everything a method allows us to do, like _default params, overloading, sanity checks, etc_.

Every class already comes with a default (0-arg) constructor (_ex._ `Vec v;`), but it stops working if you define your own constructor.

Every class has the following __defaults__:

- __default constructor__: lost if you write any constructor yourself
- __copy constructor__: just copies all fields
- __copy assignment operator__
- __destructor__
- __move constructor__
- __move assignment operator__

### Dealing With Consts & Refs

`Structs` can be defined with constants or refs, but where do we assign these values?

```cpp
int z;

Struct MyStruct {
  const int myConst = 5;
  int &myRef = z;
};
```

The above works, but means every single `MyStruct` object will have the same value, which is not useful most of the time (_ex. student IDs don't change but need to be different for every student_).

##### Object Creation Process

1. Space is allocated.
2. Fields are constructed in declaration order.
3. Constructor body runs.

We need to initialize `const` and references in Step 2, and we do this through the __Member Initialization List (MIL)__.

```cpp
Student::Student(int id, int assns, int mt, int final):
  id{id}, assns{assns}, mt{mt}, final{final} {}
//  ^---------------Step 2----------------^  ^^ Step 3
```

- Initialize _any_ field in this way, not just `const` or refs
- Even if the MIL orders them differently, fields always initialize in declarative order
- MIL is _more efficient_ sometimes
- MIL takes precedence over inline initialization/definitions
- Variables _inside_ braces follow normal rules for scope, variables _outside_ are fields

> Lushman says: Embrace the MIL! (use it anywhere you possibly can)





__CS 246 | __Oct 11, 2018

# C++ Copying

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

> Sidenote: postfix operators always take precedence over prefix operators in C++.

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
    Node tmp = o; // calls the copy constructor
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
    for (Node* p = &n; p; p = n-> next) {
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







**CS 246 |** Oct 18, 2018

# More Operators

```cpp
struct Vec {
    int x, y;
    ...
    Vec operator+(const Vec &ither) {
        return { x + other.x, y + other.y }; 
    }
    Vec operator*(const int k) {
        return { x * k, y * k }; // this implements v * k
    }
};
```

`k * v`  must be non-member operator:

```cpp
Vec operator*(const int k, const Vec &v) { return v * k; }
```

__I/O Operators:__

```cpp
struct Vec {
    ...
    OStream &operator<<(ostream &out) {
        return out << x << ' ' << y;
    }
};
```

However, this makes `Vec` the virst operand, not the second. You would have to use it like so: `v << cout`, which is confusing. So, we define operator `<<`, `>>` as _non-members_.

> Certain operators must be members:
>
> - operator=
> - operator[]
> - operator->
> - operator()
> - operator `T` where `T` is a type



# Arrays of Objects

```cpp
struct Vec {
    int x, y;
    Vec(int x, int y): x{x}, y{y}{}
};

// this is WRONG, since the default constructor will be called but no default
// constructor exists (thus the items cannot be initialized)
Vec *vp = new Vec[10];
Vec moreVecs[10];
```

Our options to fix the above are:

1. Provide a default constructor: 
   _only do so if a default constructor makes sense (e.g. if you have a `Student` object, you don't want each initialized `Student` object to have the same name when initialized, so a default constructor __doesn't__ make sense here._

2. Provide values for initialization
   For _stack_ arrays:
   `Vec MoreVecs[3] = { {0, 0}, {1, 1}, {2, 4} }; `
   For _heap_ arrays of __known__ size:
   `Vec *vp = new Vec[3] { {0, 0}, {1, 1}, {2, 4} };`

3. For _heap_ arrays of __dynamic__ size, create an array of pointers:

   ```cpp
   Vec **vp = new Vec *[5];
   vp[0] = new Vec{0, 0};
   vp[1] = new Vec{1, 1};
   ... // do whatchu gotta do
   // make sure to DELETE ONCE YOU'RE DONE WITH THE ARRAY
   for(int i = 0; i < 5; i++) delete vp[i];
   delete []vp;
   
   ```



# Const Objects

A const object is an object which has fields that cannot be modified. Const objects come up a lot, often as a result of parameters defining the object as `const`.

You _can_ call methods on const objects, but only methods that do not modify fields.

```cpp
struct Student {
    int assns, mt, final;
    float grade() const; // promises not to modify fields
};
```

The compiler verifies that const methods don't modify fields, and only const methods can be called on const objs.

### Use Case: Collecting Usage Stats on `Student` Objects

```cpp
struct Student {
    ...
    int numCalls = 0;
};
```

We want to be able to mutate `numCalls`, even on `const Student` objects. This field is not part of the "logic" of students (like `assns`, `mt`, or `final`). We can do so by declaring the field `mutable`.

```cpp
struct Student {
    ...
    mutable int numCalls = 0; // can be changed, even if object is a constant
    float grade() const {
        numCalls++;
        ...
        return ...;
    }
};
```



### Static Fields & Methods

For the above example, if we want to track `numCalls` on all `Student` objects instead of each individual one, we can use __static members__. These are associated with the _class itself_, not a particular instance of the `Student` object.

```cpp
struct Student {
    ...
    static int numStudents;
    Student(...): ... {
        numStudents++;
    }
};

int Student::numStudents = 0; // in .cc file
// static fields MUST be defined external to the class, since it should only be defined once and not for every creation of a Student object
```

A __static member function__ doesn't depend on an instance as well (so it has no `this` param). This means you can only access _static fields_ and other _static member functions_.

```cpp
struct Student {
    ...
    static int numStudents;
    ...
    static void howMany() {
        cout << numStudents;
    }
};

// in .cc
Student billy{ 60, 70, 80 }, jane{ 70, 80, 90 };
Student::howMany(); // prints 2
```



# Invariants & Encapsulation

Consider:

```cpp
struct Node {
    int data;
    Node *next;
    ~Node() { delete next; }
};


Node n1{1, new Node{2, nullptr}};
Node n2{3, nullptr};
Node n3{4, &n2};
```

This will cause _undefined behaviour_ when we try to delete `n3`, since the destructor tries to delete `&n2`, but `n2` is on the stack - we can only delete stuff that's on the heap!

`Node` relies on an assumption for its proper operation - that `next` is either `nullptr`, or was allocated by `new`. This is an __invariant__ - a statement that must hold trie - that `Node` relies on.

However, we can't guarantee this invarient; we can't trust the user to use `Node` properly. To _enforce invarients_, we use __encapsulation__. 

- Treat objects as _black boxes_ - capsules, in a sense
  - Seal away the implementation
  - Only allow interaction through provided methods
  - Both the above are examples of __abstraction__

```cpp
struct Vec {
    Vec(int x, int y); // by default, visibility is public
private: // can't be accessed outside of the Vec struct
    int x, y;
public:
    Vec operator+(const Vec &other);
};
```

> Always try to define fields as `private` - only methods should really be `public`



### Classes

It's always better to have default visibility be `private`. So, we switch from `struct` to `class`:

```cpp
class Vec {
    int x, y;
public:
    Vec(int x, int y);
    Vec operator+(const Vec &other);
}
```

The __default visibility__ of `class` is __`private`__, compared to __`public`__ for `struct`.

> This is literally the only difference apart from one word being shorter than the other lol

```cpp
// list.h
class List {
    struct Node; // private nested class is only accessible inside class List
    Node *theList = nullptr;
public:
    ...
}
```







__CS 246 | __Oct 23, 2018

# Working with the `LinkedList` class

```cpp
// list.h
class List {
    struct Node; //private nested class - only accessible within the List class
    Node *theList = nullptr;
    
public:
    void addToFront(int n);
    int &ith(int i); // reference allows us to mutate items in list directly
    ~List();
}


// list.cc
#include "list.h"

struct List::Node {
    int data;
    Node *next;
    Node(...): ... {...} // constructor
    ~Node() { delete next; }
}

void List::addToFront(int n) {
    theList = new Node{n, theList};
}

int &List::ith(int i) {
    Node *cur = theList;
    for(int n = 0; n < i; n++, cur=cur->next);
    return cur->data;
}
```

Now, only `List` can create/manipulate `Node` objects, so we can guarantee the invariant that `next` is always either `nullptr` or allocated by `new`.

However, now we can't traverse the list from `Node` to `Node` as we would a normal `LinkedList` without calling `ith()`, which is already $O(n)$ time itself.



# Design Patterns

Certain programming problems arise often and we use __design patterns__ to keep track of solutions to these problems for reuse and mass adoption.

### Iterator ==Pattern==

**Problem:** we can't trust the user to access `Nodes`.
**Solution:** create a class that manages access to nodes

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

The above code declares `x` to be the same type as its initializer (`y` in this case).

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

In the `List` example, the client cannot create iterators _except for one_:

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

> Classes should be introverts: give them as few friends as possible since it weakens encapsulation.

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

| Ver                                    | _Name_               |
| -------------------------------------- | -------------------- |
| `-x: Integer`<br />`-y: Integer`       | _Fields (optional)_  |
| `+getX: Integer`<br />`+getY: Integer` | _Methods (optional)_ |

The `-` and `+` represent private and public visibility, respectively.





__CS 246 |__ Oct 25, 2018

# Relationships

## Composition

Suppose we have two Class declarations as follows:

```cpp
class Vec {
	int x, y;
public:
    Vec(int x, int y): x{x}, y{y} {}
};

class Basis {
    Vec v1, v2;
    ...
};
```

We cannot initialize `Basis`, as the constructor for `Basis` requires the default constructor for `Vec` to create `v1` and `v2`, and it doesn't exist!

So, we amend the `Basis` class:

```cpp
class Basis {
    Vec v1, v2;
public:
    Basis(): v1{1, 0}, v2{0, 1} {}
}
```

Embedding one object inside another (`Vec` inside `Basis`, in this case) is called __composition__. The relationship between the two classes is: `Basis` "__owns a__" `Vec`. 

If $A$ _owns a_ $B$, then _typically:_

1. $B$ has no identity outside of $A$ (no independent existence)
2. If $A$ is destroyed, $B$ is destroyed.
3. If $A$ is copied, $B$ is copied as well (through a _deep copy_).

------

__Ex. Ownership and Compositions__
A car owns four wheels - a wheel is part of a car. 

1. Destroying the car $\Longrightarrow$ destroying the wheels. 
2. Duplicating the car $\Longrightarrow$ duplicating (copying) the wheels.

------

#### Modelling a Relationship: Compositions of Classes

We model this through containing each class as a box, and drawing an arrow from the owner to the owned class. The other end of the arrow (the end on the owner) has a _solid filled-in_ diamond on it.

## Aggregation

Suppose now instead of having wheels in a car ("__owns a__"), you now have wheels in a catalogue. The catalogue contains the parts, but the parts have an independent existence. This is also known as an aggregation, or a "__has a__" relationship.

If $A$ _owns a_ $B$, then _typically:_

1. $B$ exists apart from its association with $A$.
2. If $A$ is destroyed, $B$ is __not__ destroyed - it lives on.
3. If $A$ is copied, $B$ is not (shallow copy).
   - This means copies of $A$ share the same $B$ as the original.

------

__Ex. Aggregation__: Ducks in a pond

```cpp
class Pond {
    Duck *duck[maxDucks]; // notice this is an array: we don't want ducks to be deleted if the pond is
    ...
}
```

------

#### Modelling a Relationship: Aggregation

> Todo: find diagram



## Inheritance

> This is a fundamental principle of OOP!

Suppose you want to track your collection of Books.

```cpp
class Book {
    string title, author;
    int length;
public:
    Book(...);
    ...
};
```

Different types of books sometimes have different additional information we want to store. For example, a _textbook_ requires a `topic` field, or a _comic book_ requires a `hero` field. 

We _could_ create separate classes for each of these, but this _doesn't capture the relationship_ between comic books, textbooks, and regular old boring books. 

Even more importantly, what happens when we want to _store all three types in the same array_ (very common scenario)? _You can't._

Our options are to:

1. __Use a union.__

   ```cpp
   union BookType { Book *b, Textbook *t, Comicbook *c } // each of these is a field (access a book using b, textbook using t, comicbook c)
   BookTypes myBooks[20];
   ```

   __Drawbacks:__ This is not type-safe. There are no safety checks to ensure you don't store or retrieve books, textbooks, or comic books as a different type.

2. __Use an array of `void *`.__

   __Drawbacks:__ This is _definitely_ NOT type-safe. At least with option 1, you know it's a type of book. With `void *` you have not a clue what is being stored in the pointer array.

For a better solution, we note that textbooks and comic books are _kinds of books_ - they are `Book`s with extra "features." We are going to want to use the __inheritance__ model in this scenario.

```cpp
class Book {
    string title, author;
    int length;
public:
    Book(...);
    ...
};

class Text: public Book {
    string topic;
public:
    Text(...);
    ...
};

class Comic: public Book {
    string hero;
public:
    Comic(...);
    ...
};
```

`Book` is an example of a __base class__, or __superclass.__ `Text` and `Comic` are examples of a __derived class__, or __subclass.__

These are known as an "__is a__" relationship.

#### Modelling a Relationship: Aggregation

> TODO: find a diagram

### Superclasses and Subclasses

1. Subclasses _inherit_ fields and methods from the superclass.

   > This is why we didn't have to rewrite `string title, author;` or `int length;` in the subclasses - they are inherited from `Book`.

2. Methods that can be called on the superclass can always be called on any subclass of that superclass.

   > Any method that can be called on `Book` can be called on `Text` and `Comic`.

3. Subclasses _cannot_ access private fields defined on the superclass.

   > `Text` and `Comic` cannot access `length`, `title`, or `author` (or any other private field declared in the `Book` class).

The 3^rd^ rule poses a problem for creating instances of subclasses, since those private fields exist in the subclass and thus need to be initialized when constructing the object.

It's important to note that even though _fields are inherited from the superclass, they are __not__ fields of the subclass._ This means you cannot access them in the MIL, or access them even if they are `public` in the superclass.

Here's the __updated object creation process__:

1. Space is allocated.
2. The superclass portion of the class is constructed. _\*NEW\*_
3. Fields are constructed.
4. Constructor body runs.

In our example, step (2) doesn't work, since `Book` has no default constructor. To fix this, we invoke `Book`'s constructor ourselves in the MIL of `Text`'s constructor.

```cpp
class Text: public Book {
    string topic;
public:
    Text(string title, string author, int length, string topic):
    	Book{title, author, length}, topic{topic} {}
    ...
}
```

If you want to give subclass access to certain members, we cause `protected` visibility, like so:

```cpp
class Book {
    ...
protected:
    string title, author;
    int length;
public:
    ...
};

class Text: public Book {
    ...
public:
    ...
    void addAuthor(string a) { author += a; } // this works if author is protected and not private
    ...
};
```

> `protected` visibility makes stuff accessible _only_ to the class itself and any of its subclasses.

However, there are good reasons to keep superclass fields inaccessible to subclasses. Since anyone can write a subclass of your class, it is __hard to enforce invariants__ on fields with `protected` visibility since subclasses can do anything they want to those fields without the careful checks and validation you've put in place in your class to enforce your invariantes.

A better idea is to __keep fields private__ and __provide protected accessors/mutators__:

```cpp
class Book {
    string title, author;
    int length;
protected: // subclasses can call all of these!
    string getTitle() const;
    void setAuthor(string newAuthor);
public:
    Book(...);
    bool isHeavy() const;
    ...
};
```





__CS 246 |__ Oct 30 2018

# Inheritance (cont.)

From the previous lecture, we wanted to write a method `isHeavy()` for our `Book` class and all of its subclasses. However, there are different defintions of "heavy" for different types of books:

- Regular old books are heavy if they contain > 200 pages
- `Text`books are heavy if they contain > 500 pages
- `Comic`books are heavy if they contain > 30 pages

So, we write the following code:

```cpp
class Book {
    ...
public:
    bool isHeavy() const { return length > 200; }
    ...
};

class Text:public Book {
    ...
public: 
    bool isHeavy() const { return length > 500; }
    ...
};
// and something similar for the Comic subclass

// create instances of the classes
Book b{...,..., 50};
Comic c{...,...,40, ...};
cout << b.isHeavy(); // FALSE
cout << b.isHeavy(); // TRUE
```

Since we're in a "__is a__" relationship, we should be able to do the following:

```cpp
Book b = Comic{...,..., 40,...}; // this works!
```

Interestingly, `b.isHeavy()` will return `false` since it will invoke the `Book::isHeavy` method. Why?

A `Comic` object takes up more space in memory than a `Book` object, so when assigning a `Comic` object to a `Book` lvalue, the `Comic` object is __sliced__ (it has its `hero` field removed) and it is __coerced__ into a `Book` type. So, `Book b = Comic{...};` creates a `Book` and that's why the `Book::isHeavy` method is invoked.

When accessing objects through pointers or references, slicing is unnecessary and does not happen.

```cpp
Comic c = {...,..., 40,...};
Book *pb = &c;
Comic *pc = &c;
pc->isHeavy(); // TRUE
pc->isHeavy(); // FALSE - why?
```

The `Book::isHeavy` method is still invoked for the `pb` pointer. The compiler uses the type of the pointer/reference to decide which `isHeavy()` method to run - it _doesn't consider the actual type of the object_. The same object behaves differently depending on what is being used to access it.

We can make a `Comic` object act like a `Comic`, even when pointed to by the `Book` pointer, by using the `virtual` and `override` keywords:

```cpp
class Book {
    ...
protected:
    int length;
public:
    virtual bool isHeavy() const { return length > 200; }
    ...
};

class Comic:public Book {
    ...
public:
    bool isHeavy() const override { return length > 30; }
    ...
};
```

These `virtual` methods choose which class' method to invoke based on the actual type of the object at _runtime_ and not based on the accessor type.

Now, we can finish the solution for the question we set out to solve way way back - creating a collection of different books.

```cpp
Book *myBooks[20];
...
for (int i = 0; i < 20; i++) {
	cout << myBooks[i]->isHeavy() << endl;
}
// this will use the correct isHeavy method 
// Book::isHeavy for Book, Text::isHeavy for Text, etc
```

Accommodating multiple types under one abstraction is known as __polymorphism__.

> Fun fact: polymorphism is fancy Greek for "many types."

Being able to do this is _dangerous!_ Consider:

```cpp
class A {
    int x, y;
    ...
};

class B:public A {
    int z;
    ...
}

void f(A *a) {
    a[0] = A{6, 7};
    a[1] = A{8, 9};
}

B myArray[2] = {{1, 2, 3}, {4, 5, 6}};
f(myArray); // this will run, but what happens?
```

The above example will stick `A{8, 9}` halfway into `B[0]` and cause the data to become _misaligned_. Since they are different sizes and `a[1]` will increment the pointer arithmetic based on the size of `A`, not taking into account the extra field on `B`.

So, __never use arrays of objects polymorphically.__ Instead, use __arrays of pointers.__



### Inheritance & The Big 5

Consider the following example:

```cpp
class X {
    int *a;
	X(int n): a{ new int [n] } {}
    ~X() { delete [a]; }
};

class Y:public X {
    int *b;
public:
    Y(int n, int m): X(n), b{ new int[m] } {}
    ~Y() { delete [] b; }
};

X *myX = new Y{10, 20};
delete myX; // this will leak memory, since we call the destructor for X for an object of class Y
```

To ensure that deletion through superclass pointer will call the subclass destructor, _make the destructor virtual:_

```cpp
class X {
    ...
public:
    virtual ~X() { delete [] a; } 
    ...
};
```

> We do not need to use the `override` keyword for subclasses, since a destructor has only one signature (no possible mismatch in subclass methods).

__Always__ make the destructor virtual in classes that are meant to have subclasses - even if the destructor doesn't do anything (since subclasses might have destructors that do stuff that need to be called instead).



If a class is _not_ meant to have subclasses, declare it so using the `final` keyword:

```cpp
class Y final:public X {
    ...
}; // Y cannot have subclasses
```







__CS 246 |__ Nov 1, 2018

# Pure Virtual Methods & Abstract Classes

A `Student ` can be one of 2 kinds: _Regular_ or _Co-op_.

```cpp
class Student {
    ...
public:
    virtual int fees() const;    
};

class Regular:public Student {
public:
    int fees() const override; // computes fees for a regular student
};

class CoOp:public Student {
public:
    int fees() const override; // same but for co-op
};
```

We know how to calculate fees for regular and for co-op students, but since we're not sure who could be a `Student` but not a `Regular` or `CoOp` student, we don't know how to implement the `fees()` method for the `Student` superclass. 

We can explicitly give `Student::fees` __NO__ implementation. 

```cpp
class Student {
    ...
public
    virtual int fees() const = 0; // lol this syntax is weird but roll w it
};
```

This is called a __pure virtual method.__ Instead of allowing a subclass' method to override this one when a subclass method is implemented, this makes it _mandatory_ for a subclass to implement the method.

> Why even have the method on the superclass? You might want to invoke the method through a pointer to the superclass, in which case that would only work if you defined it on the superclass.

A class with a pure virtual method cannot be instantiated: `Student s;` is now _illegal._ This is known as an __abstract class.__ It serves the purpose of organizing subclasses and allowing them to be stored in a common place, such as arrays. Subclasses of an abstract class are also abstract, _unless_ they implement all pure virtual methods in the superclass. Non-abstract classes (like `Regular` and `CoOp` in our example) are called __concrete classes.__

> Subclasses of a partially-concrete subclass can be concrete if they implement the rest of the methods since they inherit the already implemented methods from their superclass.

### UML

Virtual and pure virtual methods are denoted with _italics_. 
Abstract classes have their class name denoted with _italics._

> If we can't write in italics or cursive by hand, make it clear what we're doing instead.



# Inheritance with Copy/Move

```cpp
class Book {
    // Big 5 is implemented
};

class Text: public Book {
    // copy/move operations is NOT implemented
};

Text t{...,...,...,...};
Text t2 = t; // no copy constructor in Text - what happens?
```

If a subclass does not implement a copy/move operation, the compiler first invokes the superclass' equivalent, before reverting to default behaviour (copying field-by-field) for any additional fields in the subclass. 

To write your own operations:

```cpp
Text::Text(const Text &other): Book{other}, topic{other.topic} {}

Text & Text::operator=(const Text &other) {
    Book::operator=(other);
    topic=other.topic;
    
    return *this;
}

Text::Text(Text &&other): Book{std::move(other)}, topic{other.topic} {}

Text & Text::operator=(const Text &other) {
    Book::operator=(std::move(other));
    topic = std::move(other.topic);
    
    return *this;
}
```

Be careful: `other` is an rvalue _reference._ It points at an rvalue, but it itself is an lvalue. If we just called `Book{other}`, it would be passing in an lvalue, which invokes `Book`'s copy constructor and not its move constructor. `std::move(x)` forces an lvalue `x` to be treated as an rvalue, so that move operations are run instead of copy operations.

The operations we wrote above are equivalent to the default. Modify and add to it as needed for pointers, `Nodes`, etc.

Now, consider:

```cpp
Text t1{...}, t2{...};
Book *p1 = &t1, *p2=&t2; // assign a Book pointer to each Text
*p1=*p2; // Book's operator= will run here, and only copy the Book parts!!
```

The type of the pointer was `Book`, so `Book`'s `operator=` method ran and only the `Book`'s fields are copied between the `Text` objects, causing a __partial assignment.__ 

If we try using the `virtual`/`override` keywords:

```cpp
virtual Book &operator=(const Book &other);

Text &operator=(const Text &other) override;
```

 the _parameter types are different_ so it's not an override and it won't compile. We can't replace `const Text &other` with `const Book &other` either, or else you would be able to assign objects that aren't `Text` to a `Text` lvalue, which is horrible.

To __sum up__:

1. If `operator=` is non-virtual, we run into _partial assignment through superclass pointers._
2. If `operator=` is virtual, we run into _mixed assignment_.

Because of this, it's __strongly recommended__ to ==make all superclasses abstract==.

But wait! We have books that are not comics or textbooks, so does this work? In reality, our `Book` design heirarchy is wrong and needs a redesign:

- `AbstractBook` _(new superclass)_
  - `NormalBook` _(where we would define `Books` previously)_
  - `Text`
  - `Comic`

and allows us to write the following definition:

```cpp
class AbstractBook {
    string title, author;
    int length;
protected:
    AbstractBook &operator=(const AbstractBook &other);
public:
    AbstractBook();
    ...
    virtual ~AbstractBook() = 0; // pure virtual method
}
```

If we use the destructor as a pure virtual method, it __must__ be implemented still, since the destructor on the subclass __will call it.__

> We need at least one pure virtual method to make this class an abstract class. If none of the methods are appropriate, then use the destructor.

This makes `*pb1 = *pb2;` invalid code and it won't compile, forcing the client to be more precise about what they want to assign to what, while still allowing subclasses to access it for copy/move.

An updated implementation for the subclasses of `AbstractBook`:

```cpp
class NormalBook:public AbstractBook {
public:
    NormalBook(...);
    ~NormalBook();
    NormalBook &operator=(const NormalBook &other) {
        AbstractBook::operator=(other);
        return *this;
    }
}

// other subclasses implemented in a similar fashion
```





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





__CS 246 |__ Nov 8, 2018

# Exceptions (cont.)

A handler can act as a catch-all.

```cpp
try { 
	// do stuff here
} catch(...) { // the ellipses are literal
    // do other stuff here    
}
```

You can throw any type you want, not just exceptions. 

```cpp
class BadInput{};
...
throw BadInput{};
```

However, exceptions are not optimized since they are intended for exceptional circumstances, like their name implies. You shouldn't be using them for more general use cases like returning values, etc.

#### Exceptions & The Big 5

When `new` fails, it throws a `std::bad_alloc` exception. 

You should __never let a destructor throw an exception.__  It will cause the program to abort immediately. If you want to let a destructor throw, you can tag it with `noexcept(false)`, but if a destructor is running during stack unwinding while dealing with another exception and _that_ destructor throws as well, you now have 2 active (unhandled) exceptions. This will _also_ cause the program to abort immediately. 

_exceptions will be covered more later on_



# More Design Patterns

## Observer ==Pattern==

This pattern is used when you have classes that need to react to another class's data. It follows the publish/subscribe model. 

- One class is the __publisher/subject__: it generates data. 
- One or more classes are __subscriber/observer__ classes: they receive data and react to it.

> You can obviously have multiple classes subscribed to a single subject: think about people listening to a radio station (a single subject).
>
> You can also have a subscriber class subscribed to more than one subject: think about a graph in Excel - it's subscribed to all the cells it's pulling data from and will update automatically if any of them change.

#### UML Diagram

![Image result for observer pattern uml](https://www.cs.mcgill.ca/~hv/classes/CS400/01.hchen/doc/observer/observer.gif)

The following sequence occurs when something changes in the publisher/subject:

1. Subject's state is updated.
2. `Subject::notify()` is invoked -it calls each observer's `update()` 
   - This is going to be the `ConcreteObserver`'s `update()` since `Observer` is an abstract class and `update()` is virtual.
3. Each observer calls `ConcreteSubject::getState()` to query the state and reacts to this updated state accordingly.

#### Implementation

One implementation of the pattern is as follows:

```cpp
class Subject {
    vector <Observer *> observers;
    
public:
    void attach(Observer *ob) { observers.emplace_back(ob); }
    void detach(Observer *ob) { ... } // just look for this observer in observers list and remove it
    void notifyObservers() { for(auto &ob:observers) ob->notify(); }
    virtual ~Subject() = 0; // so that the Subject class is abstract
};
    
Subject::~Subject() {}


class Observer {
    
public:
    virtual void notify() = 0;
    virtual ~Observer();
} 
```

To give a concrete example, imagine running a horse race. You will need a subject to publish winners of the race, and the observers will be the individual bettors. That implementation will be as follows:

```cpp
class HorseRace::public Subject {
    ifstream in; // source of horse race results
    string lastWinner;
    
public:
    HorseRace(string source): in{source} {}
    bool runRace() { // we return a bool to indicate if a race has been run (if we haven't reached EOF)
        in >> lastWinner;
        return in;
    }
    string getState() { return lastWinner; }
};


class Bettor:public Observer {
    HorseRace *subject;
    string name, myHorse;
    
public:
    Bettor(...): ,,, {
        subject->attach(this);
    }
    ~Bettor() { subject->detach(this); } // we do not delete subject
    void notify() {
        string winner = subject->getState();
        if(winner == myHorse) cout << "I won!" << endl;
        else cout << ":(" << endl;
    }
}


// main.cc
HorseRace hr;
Bettor Larry(&hr, "Larry", "RunsLikeACow"); // amazing name (both the horse and the bettor)
... // probably other bettors

while(hr.runRace()) {
    hr.notifyObservers();
}
```

## Decorator ==Pattern==

This pattern is used when we want to add/remove functionality from an object at runtime.

#### UML Diagram

The following classes exist:

- A `Component` is an interface with operations that your objects will provide.
- A `ConcreteComponent` implements the interface: it is a basic object.
- Many subclasses will all inherit from `Decorator`, which inherits from `Component`
  - This means every Decorator _is a_ `Component` and _has a_ `Component`.

![Image result for decorator pattern uml](https://mertarauh.com/wp-content/uploads/2016/05/Decorator.gif)

> As an example, take a windowing system in an operating system. 
>
> A `Window w/ scrollbar` _is a_ `Window`, and _has a_ pointer to the underlying plain `Window`.
> A `Window w/ scrollbar+menu` _is a_ `Window`, and _has a_ pointer to a `Window w/ scrollbar`, which _has a_ pointer to a plain `Window`.
>
> All of these will inherit from `AbstractWindow`, so `Window` methods can be used polymorphically on all of the above.

#### Implementation

We take the example of a pizza. _yum_

```cpp
class Pizza {
public:
	virtual float price() const = 0;
    virtual string desc() const = 0;
    virtual ~Pizza() {}
    
};


class CrustAndSauce: public Pizza {
public:
    float price() const override { return 5.99; }
    string desc() const override { return "Pizza"; }
    
};


class Decorator:public Pizza {
protected:
    Pizza *component;
    
public:
    Decorator(Pizza *p): component{p} {}
    virtual ~Decorator() { delete component; }
    
};


class StuffedCrust:public Decorator {
public:
    float price() { return component->price() + 2.69; }
    string desc() { return component->desc() + " with Stuffed Crust"; }
    
};

// similarly for other subclasses like toppings, dipping sauce, etc
```



> There isn't an abstract general implementation of the pattern itself, since a `Decorator` is always a subclass that inherits from some implemented class (so we had to start with the pizza example).







__CS 246 |__ Nov 13, 2018

# Maps & Design Patterns (cont.)

## Factory Method ==Pattern== 

This pattern is used when a creator class relies on different subclasses to do different things.



#### UML Diagram

![Image result for factory method design pattern uml](https://upload.wikimedia.org/wikipedia/commons/e/ed/Factory_Method_UML_class_diagram.png)



#### Implementation

We take the example of a video game with two kinds of enemies: turtles and bullets. The system randomly sends turtles or bullets, but bullets are more frequently seen in harder levels. Our problem is that we never know exactly which enemy comes next, so we can't call the turtle and bullet constructors directly.

```cpp
class Level { 
public:
    virtual Enemy* createEnemy() = 0; // this is known as a *factory method*
};


class Easy:public Level {
public:
    Enemy *createEnemy() override {
        // this method will create mostly turtles
    }
};

class Hard:public Level {
public:
    Enemy *createEnemy() override {
        // this will create more bullets
    }
};


// In the client:
Level *l = ...;
Enemy *e = l->createEnemy(); // factory method decides what we get
```



## Template Method ==Pattern==

This pattern is used when we want subclasses to override superclass behaviour but some aspects must stay the same.

#### UML Diagram

![Image result for template method design pattern uml](https://sourcemaking.com/files/v2/content/patterns/Template_method_example.png)



#### Implementation

Consider the video game example in the Factory Method design pattern above. We now extend it to say that there are two types of turtle enemies: red turtles and green turtles. They are mostly drawn the same, but differ slightly in their shell colour.

```cpp
class Turtle {
public:
    void draw() {
        drawHead();
        drawShell();
        drawFeet();
    }
private:
    void drawHead() { ... };
    virtual void drawshell() = 0;
    void drawFeet() { ... };
}


class RedTurtle:public Turtle {
    void drawShell() override { ... } // draw red shell
};

class GreenTurtle:public Turtle {
    void drawShell() override { ... } // draw green shell
};
```

- Subclasses cannot change the way a turtle is drawn, but can change the way the shell is drawn
- Reduces code repetition as well

> This has nothing to do with C++ templates.



### The Non-Virtual Interface (NVI) idiom

Notice that a public virtual method is really two things:

1. An interface to the client: *it indicates provided behaviour with pre/post conditions.*
2. An interface to subclasses: *it provides a "hook" to insert specialized behaviour.*

This is a bit conflicting: it's hard to separate these ideas if they are tied to the same one function. If you want to be able to split a virtual method into two, maybe with some constant code in between, you risk changing the client's interface. 

To make sure that overriding functions conform to the pre/post conditions, the __NVI__ says that:

- All `public` methods should be non-`virtual`.
- All `virtual` methods should be `private` (or at least `protected`).
  - With the one exception of the destructor

------

__Ex. Digital Media__

```cpp
// initial implementation
class DigitalMedia {
public:
    virtual voide play() = 0;
};

// NVI-approved implementation
class DigitalMedia {
public:
    void play() {
        // could add code before ( ex. checkCopyright() )
        doPlay();
        // could add code after ( ex. updatePlayCount() )
        // guarantees pre/post code will be called
    }
    
private:
    virtual voide doPlay() = 0; // subclasses override this method
};
```

------

This generalizes the Template Method design pattern by essentially __putting every virtual function inside a template method.__



## Maps

Maps are a part of the STL. They are used for creating dictionaries: "arrays" that map a __key__ to a __value__. You can use it by placing `#include <map>`in the file.

| Syntax                       | Purpose                                                      |
| ---------------------------- | ------------------------------------------------------------ |
| `std::map<string, int> m;`   | Initialize a map                                             |
| `m["abc"] = 1;`              | Add key-value pair to map                                    |
| `m.erase("abc");`            | Removing pair from map                                       |
| `cout << m["ghi"];`          | Accessing pair in map (if `key` is not present, it is inserted with the value default constructed) |
| `if(m.count("abc")) { ... }` | Checking for existence of key in map (returns `0` if not found, `1` if found) |



> Lushman says: use `map` if you want to implement a balanced BST.





## Visitor ==Pattern==

This pattern is used for implementing __double dispatch__: choosing virtual methods based on the type of _two_ objects at runtime (as opposed to one).

#### Implementation

Consider the case of the video game example above again. Suppose we want to implement attacking, which determines what happens based on which `Weapon` is used _and_ on which `Enemy` is being attacked.

If `attack()` is a method of `Enemy`|`Weapon` (choose 1), we determine based on the type of `Enemy`|`Weapon` but not on `Weapon`|`Enemy`.

```cpp
class Enemy {
public:
    virtual void beStruckBy(Weapon &w) = 0;
};

class Turtle:public Enemy {
public:
    void beStruckBy(Weapon &w) override { w.strike(*this); } // *this is a Turtle
};

class Bullet:public Enemy {
public:
    void beStruckBy(Weapon &w) override { w.strike(*this); } // *this is a Bullet    
};



class Weapon {
public: 
    virtual void strike(Turtle &t) = 0; // these are
    virtual void strike(Bullet &b) = 0; // overloads
};

class Stick:public Weapon {
public:
    void strike(Turtle &t) override {
        // strike Turtle t with this Stick
    }
    void strike(Bullet &b) override {
        // strike Bullet with this Stick
    }
};
// something similar for a Rock Weapon



// In client:
Enemy *e = new Bullet { ... };
Weapon *w = new Rock { ... };

c->beStruckBy(*w);
```

On line 41:

1. `Bullet:beStruckBy` runs (virtual method)
2. `Weapon::strike` is called (`*this` is Bullet, so Bullet version is chosen at compile time)
3. Virtual method call resolves to `Rock::strike(Bullet &)`



#### Adding Functionality to Existing Classes

The Visitor pattern can also be used to add functionality to existing classes, without changing or recompiling the classes themselves.

```cpp
class Book {
public:
    ...
    virtual void accept(BookVisitor &v) { v.visit(*this); }
};

class Text:public Book {
public:
    ...
    void accept(BookVisitor &v) { v.visit(*this); }
};
// this is the Visitor pattern in a different form
```







__CS 246 |__ Nov 15, 2018

# Dependencies

```cpp
class Book {
public:
    virtual void accept(BookVisitor &v) { v.visit(*this); }
};

class Text:public Book {
public:
    void accept(BookVisitor &v) { v.visit(*this); }
};


class BookVisitor {
public:
    virtual void visit(Book &b) = 0;
    virtual void visit(Text &t) = 0;
    virtual void visit(Comic &c) = 0;
};
```

Suppose we want to develop an application that tracks how many of a certain type of `Book` there are. We want to track:

- `Book`s by __Author__
- `Text`s by __Topic__
- `Comic`s by __Hero__

We can add `virtual void updateCatalogue(...)` to each class, but we could just write a visitor:

```cpp
struct Catalogue:public BookVisitor {
    map<string, int> theCatalogue;
    
    void visit(Book &b) override { theCatalogue[b.getAuthor()]++; }
    void visit(Text &t) override { theCatalogue[t.getTopic()]++; }
    void visit(Comic &c) override { theCatalogue[c.getHero()]++; }
}
```

However, this code will not compile. Since `book.h` and `BookVisitor.h` include each other, this is a __circular include dependency__ and `book.h` will not be included a second time because of the _include guard_  in `book.h`. As a result, `Text` does not have the definition of a `Book` and doesn't know what it is.

### Compilation Dependencies

There are two options when requiring a dependency - you can either:

1. `#include` the dependency (what we normally do)
2. Forward declare the dependency (declare a skeleton version of the class with `class XXX;` just to show that there is such a class)

Consider the following classes defined in separate header `.h` files:

```cpp
class A { ... }; // A.h

class B: public A { ... }; // B.h


class C { // C.h
    A;
};

class D { // D.h
    A *a_ptr;
};

class E { // E.h
    A f(A x); 
};

class F { // F.h
    A f(A x) { ... x.someMethod(); ... }
};
```

When does a compilation dependency need to exist (_i.e. when do we need to `#include` the dependency_? For each class:

| Class | Requires `#include`? | Reasoning                                                    |
| ----- | -------------------- | ------------------------------------------------------------ |
| `B`   | ==Yes==              | Much like `C`, `B` being a subclass of  `A` is a lot like having an object field; it has all the fields that `A` does, so the compiler will require knowledge of the contents and size of `A`. |
| `C`   | ==Yes==              | Since `C` has an object field of type `A`, constructing an instance of `C` will require space allotment for `A`, which requires the compiler to know exactly how big and what is in `A`. |
| `D`   | No                   | Since there is just a pointer to `A` and all pointers are the same size, a forward declaration is sufficient to compile `D`. |
| `E`   | No                   | Since the function is just declared and not defined in the `E.h` file, a forward declaration is sufficient to compile `E`. In an `E.cc` file, we will have to `#include` the dependency of `A`. |
| `F`   | ==Yes==              | Since the function is defined and implemented, and an object of type `A` is used and a method of the object is called, the compiler needs to know everything about the object and thus everything about `A`. |

If the code doesn't need an `#include`, ==don't create a needless compilation dependency== by using `#include`unnecessarily. 

In the __implementation__ (`.cc`) of `D` and `C`, we _will_ need to know about class `A` since we are most likely manipulating objects of type `A` and whatnot. Then we can `#include "A.h"` and not worry about circular dependencies since a `.h` file will _never_ include a `.cc` file.

> This has the added benefit of reducing recompilation: in the example above, only `A, B, C, F` will need recompiling when `A` changes.



Now, consider the `XWindow` class.

```cpp
class XWindow {
    Display *d;                  // do we know what
    Window w;                   // all these 
    int s;                     // fields
    GC gc;                    // do?
    unsigned long colours[10];
public:
    ...
}
```

This class has a lot of clients (everyone in  $CS \ 246$). If you add or change one of these `private` members, _all clients must recompile._ The solution to this is the __pointer to implementation (PIMPL) idiom__.

### PIMPL ==Idiom==

We create a second `XWindowImpl` class that holds the "meat" of the class: all those fields that we had no idea what they did in the previous code block.

```cpp
// XWindowImpl.h
#include <X11/Xlib.h>
struct XWindowImpl {
    Display *d;
    Window w;
    int s;
    GC gc;
    unsigned long colours[10];
};

// Window.h
class XWindowImpl; // forward declaration

class XWindow {
    XWindowImpl *pImpl;
public:
    ... // no change from previous XWindow class
};

// Window.cc
#include "Window.h"
#include "XWindowImpl.h"

XWindow::XWindow(...): pImpl{ new XWindowImpl } {...}
// other methods stay the same except you replace fields:
// d becomes pImpl->d
// s becomes pImpl->s
```

Now, there's no need to include `Xlib.h`, and there is no compilation dependency on `XWindowImpl.h`. This means that clients also don't depend on `XWindowImpl.h`. If you keep all private fields in this `XWindowImpl.h`, then only `Window.cc` needs to be recompiled if you change `XWindow`'s implementation.

Furthermore, if you have several possible window implementations (_e.g. `XWindow`s and also `YWindow`s_), you can make the `Impl` struct a superclass:

> Insert UML diagram here

The __pImpl__ idiom with a class heirarchy of implementations is called the __Bridge__ ==Design Pattern==.           





__CS 246 |__ Nov 15, 2018

# Measures of Design Quality

There are two principles of design quality that we should follow: __coupling__ and __cohesion__.

### Coupling

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







__CS 246 |__ Nov 27, 2018

# Casting (cont.)

### Const Casting

`const_cast` is for converting between `const` and non-`const` values. It is the only method you can employ to remove `const`.

```cpp
void g(int *p);
const int *q = ...;
g(q);		// won't compile - can't pass const object to a method that might try mutating it
g(const_cast<int *>(q)); // will compile with no errors
```

Using `const_cast` is considered __bad practice__, but it is a surefire way to get rid of all const errors. This is dangerous  as `q` might be pointing to READ_ONLY memory, in which case your program _will_ crash.

> A useful situation for `const_cast` is if you have no control over methods you're using but you know they are `const` (_i.e. someone who doesn't use `const` parameters in their code_).

### Dynamic Casting

`dynamic_cast` is useful for working with superclasses and subclasses. Consider the following:

```cpp
Book *pb = ...;
static_cast<Text *>(pb)->getTopic(); // is this safe?
```

The above code will work depending on what `pb` is actually pointing to. In this case, before attempting to manipulate or use the new object after casting, it's best to do a "tentative" cast and check to see if it succeeds first.

```cpp
Book *pb = ...;
Text *pt = dynamic_cast<Text *>(pb);
if(pt) { cout << pt->getTopic(); }
else { cout << "pt is not a book" << endl; }
```

If the cast works (meaning that `*pb` is actually a `Text` or a subclass of `Text`), `pt` will point at a `Text` object created from `pb`. If the cast _fails_, `pt` will be a `nullptr`.

We can use this and `static_pointer_cast` and `dynamic_pointer_cast` to work with pointers to __make decisions based on the Runtime Type Information (RTTI)__. 

```cpp
void whatIsIt(shared_ptr<Book> b) {
    if(dynamic_pointer_cast<Comic>(b)) cout << "It's a comic!";
    else if(dynamic_pointer_cast<Text>(b)) cout << "Text";
    else cout << "Book";
}
```

However, code like this is tightly coupled ot the `Book` class and may indicate **bad design**. A better solution is virtual methods, or a Visitor ==Design Pattern==.

_Dynamic casting_ also works with references, like so:

```cpp
Text t{...};
Book &b = t;
Text &t2 = dynamic_cast<Text &>(b); 
```

If `b` points to a `Text`, `t2` is a reference to the same `Text`. Otherwise, it raises an exception (since there's no such thing as a null exception to mimic the behaviour of `dynamic_cast` with `nullptr`).

> Dynamic casting works with only classes with at least one virtual method.

With dynamic reference casting, we can solve the __polymorphic assignment problem.__

```cpp
Text &Text::operator=(const Book &other) {
    const Text &textOther = dynamic_cast<const Text &>(other);
    if(this == &textOther) return *this;
    Book::operator=(other);
    this->topic = textOther.topic;
    
    return *this;
}
```

# Virtual Methods

If we have a virtual method, the class also contains a pointer that's known as a `vptr`. The location of the base class obect is stored in a **Vtable**. 





__CS 246 |__ Nov 29, 2018 (last​ lecture :cry:)

# Multiple Inheritance

A class can inherit f rom more than 1 class:

```cpp
class A{ int a; };
class B{ int b; };

class C: public A, public B {...} // class C will have fields a and b
```

However, you may have fields that are named the same on two superclasses that a subclass is inheriting from:

```cpp
class A{ int a; };
class B{ int a; };

class C: public A, public B {...} // class C will have two fields named a

C c;
cout << c.a << endl; // this is ambiguous

cout << c.A::a << endl; // this is how you need to say it
cout << c.B::a << endl;
```



Would there be two `a` fields if we have both class `A` and `B` being subclasses of the same superclass `X`, which has an `a` field that the two subclasses inherit from?

We make `X` a **virtual base class**:

```cpp
class X { int a; };

class A: virtual public X{...};
class B: virtual public X{...};

class C: public A, public B{...};
```



# Template Functions

```:cry:
template<typename T> T min(T x, T y) {
    return x < y ? x : y;
}

int x = 1, y = 2;
int z = min(x, y); // T = int - compiler figures this out based on the type of x, y
int a = min<int>(x, y); // this also works, but is more typing
auto f = min(1.0, 3.0); // T = double
```

`min` will work for any type `T` that has operators.

### C++ STL Library `<algorithm>`

The `<algorithm>` library contains a suite of template functions, many of which work for iterators.

There's the `find` method, which returns an iterator to a value the client wants to find, or an iterator to `last()` if not found:

```cpp
template<typename Iter, typename T>
Iter find(Iter first, Iter last, const T &val) {
    while(first != last) {
        if(*first == val) return first;
        ++first;
    }
    
    return last;
}
```

There's `count`, which is like `find`, but returns the number of occurrences of `val`.

There's also `copy`, which copies one container range from `first` to `last` to another, starting at `result`:

```cpp
template<typename InIter, typename OutIter>
OutIter copy(InIter first, InIter last, OutIter result) {
	// does the copying 
}

// client code
vector<int> v{1, 2, 3, 4, 5, 6, 7};
vector<int> w(4); // 0, 0, 0, 0
copy(v.begin() + 1, v.begin() + 5, w.begin()); // w = 2, 3, 4, 5
```

Note that __`copy` does not allocate new memory__ - it is the client's responsibility to do this and make sure there's enough space for the copying. 

> The above nuisance is because `copy` has no idea what `w` is; it can't, since it just has an iterator to `w` and thus `w` could be a `map`, `vector`, or anything else that has an iterator.

There's another called `transform`, which behaves similarly to `copy`, but accepts a function that will "transform" the values while copying them over:

```cpp
template<typename InIter, typename OutIter, typename Func>
OutIter copy(InIter first, InIter last, OutIter result, Func f) {
    while(first != last) {
		*result = f(*first);
		++first; 
		++result;
    }
    
    return result;
}


int add1(int n) { return n + 1; }
...
vector v{2, 3, 5, 7, 11};
vector w(v.size()); // all 0s
transform(v.begin, v.end(), w.begin(), add1); // 3, 4, 6, 8, 12
```

However, functions are not the only things that can be called as a function:

```cpp
vector v{2, 3, 5, 7, 11};
vector w(v.size()); // all 0s

// objects also have operator()
class Plus1 {
public:
    int operator()(int n) { return n + 1; }
};

transform(v.begin, v.end(), w.begin(), Plus1{}); // 3, 4, 6, 8, 12 (adds 1)


// might as well generalize while we're at it
class Plus {
    int increment;
public:
    Plus(int i): increment{i} {}
    int operator()(int n) { return n + increment; }
};

transform(v.begin, v.end(), w.begin(), Plus{2}); // 4, 5, 7, 9, 13 (adds 2)
```

Classes that are used like this are known as __function objects__. Apart from being able to generalize like above, another advantage to function objects are their ability to __maintain state:__

```cpp
class IncreasingPlus {
    int incrementBy = 0;
public:
    int operator() { return n + (incrementBy++); }
    void reset() { incrementBy = 0; }
};

vector<int> v(5, 0);   // both of these are
vector<int> w = v;     // 0, 0, 0, 0
transform(v.begin(), v.end(), w.begin(), IncreasingPlus{}); // w = 0, 1, 2, 3, 4
```

Other methods include `count_if` (returns the number of objects that match the function bool given).

### Anonymous Functions 

When using template functions, it's sometimes annoying and seems like a waste to have to write "one-liner" functions for single use cases:

1. You have to explicitly create the function, adding one more thing you have to do to get your code working.
2. Functions cannot be defined inside other functions, so often your definition of a "one-liner" function will _not_ be right before the template function call (_i.e. if the template function call happens inside a bunch of nested functions_).

You can use__ anonymous lambda functions__ much like we did lambda functions in Racket. Consider the situation where you want to count how many `int`s in a `vector` are even:

```cpp
vector<int> v...;
bool even(int n) { return n % 2 == 0; }
int x = count_if(v.begin(), v.end(), even);

int x = count_if(v.begin(), v.end(), [](int n) { return n % 2 == 0; });
```

### Other Use Cases for Iterators

You can also apply the notion of iteration to other sources of data.

For example, you can create an iterator to an `ostream`:

```cpp
#include <iterator>

vector<int> v{1, 2, 3, 4, 5};
ostream::iterator<int> out { cout, ", "};
copy(v.begin, v.end(), out); // will print "1, 2, 3, 4, 5, "
```

As noted above, `copy` does not allocate new memory since it just has an iterator to the return value. So, the only way to have an automatically copying method is to use **an iterator whose assignment operator inserts a new item**.

```cpp
vector<int> v{1, 2, 3, 4, 5};
vector<int> w;
copy(v.begin(), v.end(), w.begin()); // undefined behaviour - segfaults
copy(v.begin(), v.end(), back_inserter(w)); // copies v to the end of w, adding new entries
```

This `back_inserter` iterator is available for any container with a `push_back` method.





> __Lushman says :speech_balloon: (last one):__ I hope C++ is your favourite programming language...for now.







