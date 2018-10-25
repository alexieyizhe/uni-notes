__CS 246 |__ Midterm

# Study Guide



- Piping (`|`) hands output to another __program__ or __utility__; output redirection (`>`) passes output to another __file__ or __stream__.
- `stderr` is not buffered unlike other streans `stdin` `stdout`, displays output instantly
  - use `2>` to redirect `stderr` stream
- `#!/bin/bash` at the top for scripts

| Purpose                                        | Syntax                                                       | Notes                                                   |
| ---------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------- |
| embed commands inside quotes or other commands | `$(your_cmd_here)`                                           | Single quotes will suppress everything                  |
| get arguments from bash command line           | `$1 $2 $# $*`, `$0` is name of program                       | 1^st^/2^nd^ arg, # of args, all args                    |
| if statement                                   | `if [ $1 -neq "pass" ]; then` and `fi` to close              | `fi` to end if statement flow, __SPACES ARE MANDATORY__ |
| for loops                                      | `for i in {START_VAL..END_VAL..STEP_VAL}; do` and `done` to close | can also use `$(COMMAND)` or file                       |
| subroutines                                    | `foo() { do things }` and call with `foo`                    |                                                         |
| quit program                                   | `e`                                                          |                                                         |
| AND, OR for if statements                      | `-a` and `-o`                                                |                                                         |
| file existence                                 | `-e`                                                         |                                                         |
| string length > 0                              | `-n`                                                         |                                                         |
| string equality                                | `=`                                                          |                                                         |
| integer equality                               | `-eq`, `-ne`, `-lt`, `-le`, `-gt`, `-ge`                     |                                                         |

- redirect to `/dev/null` if you want silent output

---

### C++

| Library               | Usage                                                        |
| --------------------- | ------------------------------------------------------------ |
| `iostream`, `iomanip` | Gives `cin`, `cout`, and manipulators                        |
| `string`, `sstream`   | Gives `istringstream`, `ostringstream`                       |
| `fstream`             | Gives `ifstream`, `ofstream`; can do everything you do with `cin`, `cout` but with files, file is closed automatically when variable is destroyed |

- if `cin >> i` where `i` is an integer fails, then it read in a non-int input and must be cleared with `cin.clear()` and then `cin.ignore()` to skip the char
- optional-default parameters must all appear last in the parameter list
- __overloading__ is based on _number_ and _types of arguments_ of function
  - dont overload I/O operators as member functions since it reverses the order (`cout << x;` becomes `x << cout;` - weird) 
- __references__:
  - an __lvalue__ is an object that is initialized and has an address already
  - __rvalue__ is the opposite
  - can't leave them *uninitialized* or create a *pointer to a reference* or a _reference to a reference_
  - defining a **reference as `const`** allows you to pass `rvalues` in like so: for `if int g(const int &n) {...}`, `g(5)` is _valid_ even though `5` is _not_ an lvalue

#### Strings

- c++ strings are stored as `string` type, dynamic sizing, no null terminator required
- use `getline(cin, str, '/')` (_delimiter is a char, `\n` by default_)

```cpp
#include <sstream>
string intToString(int n) {
	std::ostringstream sock;
	sock << n;
	return sock.str();
}
int stringToInt(string s) {
    int n;
	std::istringstream sock{s};
	sock >> n;
	return n;
}
```

### Preprocessor

| Syntax                           | Usage                                                        |
| -------------------------------- | ------------------------------------------------------------ |
| `#if ...`, `#elif ...`, `#endif` | code inside these are only compiled if statements evaluates to `true` |
| `#ifdef VAR`, `#ifndef VAR`      | same as above, but only if `VAR` is defined;                 |

- use include guards by replacing `VAR` in `#ifdef VAR` with a _unique_ identifier (common to use `MODULENAME_H`) and adding `#define MODULENAME_H` after to show it's now been defined

__Makefile__

```cpp
CXX = g++ // compiler name
CXXFLAGS = -std=c++14 -Wall -g -MMD // compiler options
OBJECTS = main.o vec.o
DEPENDS = ${OBJECTS:.o=.d}
EXEC = main

${EXEC}: ${OBJECTS}
  ${CXX} ${CXXFLAGS} ${OBJECTS} -o ${EXEC}

-include ${DEPENDS}
```

---

### Classes

#### Methods for Classes

1. **constructor**: classes come with a default 0 parameter one but is lost if we write our own
2. **copy constructor**
   - called when: return by value, pass by value, initialize from another obj
3. **copy assignment operator**
4. **move constructor**
5. **move assignment operator**: takes in an _rvalue__
6. **destructor**

##### Object Creation Process

1. Space is allocated.
2. Fields are constructed in declaration order.
3. Constructor body runs.

#### Member Initialization List (MIL)

- Use for everything but especially
  - `const` member fields
  - members that are references (`&`)
  - members that are objects without a default constructor (default was overwritten by user)
- MIL takes precedence over inline declarations/initializations
- default values for objects is created by invoking the default constructor (other ones will be random values left behind previously)

#### General

- make constructors `explicit` when you have one parameter only
- make member functions constant by putting `const` before curly braces
  - this basically makes it invalid to modify `this` in the member function

---

### General Tips

- be aware of when you're using the stack and when you're using the heap
  - Heap is use when calling `new OBJ{}`
- don't use `using namespace std;` in `.h` files
- _separate compilation_ produces `.o` files called __object files__
- `static` fields and methods are associated with class, not specific instances

---

### `Makefile`s

- the `.d` files keep track of all the dependencies of certain files, essentially creating a list of _all_ files that need to be checked, even if the file itself doesn't change
  - _e.g. changing the `.h` file should recompile the `.cc` file, but the `.cc` file itself doesn't change_ 

#### Random

- `new X{}` returns an _rvalue_
- defining a destructor for a class preserves all other methods in the "big 5"
- if you write a class $A$ with no copy constructor (by making that copy constructor nonsensical) and you write another class $B$ with said class $A$ as a field, then you lose the copy constructor for $B$
-  