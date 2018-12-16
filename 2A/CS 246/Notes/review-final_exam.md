__CS 246 |__ Study Guide

# Concept Checklist for Final

- [ ] C++ I/O: `cin`, `cout`, `cerr` in `iostream`

- [ ] Difference between C++ and C style strings

  - stored in char arrays *vs.* stored as `string `type
  - forces client to manage memory *vs.* manages memory for you
  - requires null terminator for EOS *vs.* no null terminator required

  - [ ] Using `sstream`s

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

- [ ] Using `fstream`s: open with `ifstream input{"FILENAME"};`, use same way as I/O

- [ ] Optional/default parameters: overloading looks at **number** and **types** of parameters in function

- [ ] `const` values must be initialized, can't be declared first

- [ ] references

  - can't create a pointer to a reference, can create a reference to pointer
  - declaring function parameter as `const TYPE &` means you can passs in rvalues too
    - for `if int g(const int &n) {...}`, `g(5)` is valid even though `5` is not an lvalue
    - this is because `const int &r = 5;` is valid
  - pass-by-reference does not create copy of the object

- [ ] lvalues can be implicitly transformed into rvalue, but not the other way

  ```cpp
  int i = 1;
  int j = i; // i is an lvalue that is implicitly transformed into rvalue
  
  i + 2 = j; // i + 2 is an rvalue, error
  ```

- [ ] don't mix `new`+ `delete` with `new[]` and `delete []`

- [ ] Classes

  - object initialization
    - C style initialization just takes fields and sets them equal to parameters in order
    - constructors allow us to do lots of checks or overloading
    - **default 0-arg constructor**: `C c;` for a class `C`
      - leaves all primitive types _uninitialized_, calls constructors of non-primitive types
      - is deleted if user constructor is defined
    - **empty copy constructor**: `C c();` or `C c{};` or `C c = {};` 
      - initializes all primitive types to zero values, calls constructors of non-primitive types
    - **user defined non-0-arg constructor**
  - Object Creation Process
    1. Space is allocated
    2. Superclass portion of the class is constructed (_if inheriting_)
    3. Fields are constructed in declaration order
       **MIL** runs here, can initialize `const` values or references here, order in MIL doesn't matter, only declarative order matters
    4. Constructor body runs
  - Object Destruction Process
    1. Destructor body runs 
       - classes always come with a destructor that just calls destructors on all fields that are objects (doesn't call it for pointers!)
    2. Fields' destructors invoked in reverse declaration order (for fields that are objects)
    3. Space in memory is deallocated
  - some operators must be members:
    - operator=
    - operator[]
    - operator->
    - operator()
    - operator `T` where `T` is a type
  - `mutable` keyword: allows the field to be mutated even on const objects, only use on fields not part of the "logic" of the class
  - `static` keyword: 
    - on fields, makes them shared class-wide instead of being on the instance - MUST initialize once in `.cc` file and not in constructor
    - on member functions, only allows them to access `static` fields and other `static` member functions

- [ ] Big 5: differences between them, what they're used for, implementation

  - Copy Constructor
    - called when: 
      1. When an object is initialized by another object of the same type
      2. When an object is passed by value
      3. When an object is returned by value from a function

  - Copy Assignment Operator
    - called when:
      1. you set an object of a class equal to another existing object of the same class
    - for the most efficient version of a CAO
      1. use the copy constructor to create a 'temp' copy of the object being copied
      2. swap everything with the temp
  - Move Constructor
    - set everything equal to the contents of the object being copied, set pointers in object being moved to  null to avoid being deleted when it goes out of scope
    - if not defined, copy constructor used
  - Move Assignment Operator
    - swap everything with the object being copied, rvalue being copied will delete the old data we had as it goes out of scope
    - if not defined, CAO used
    - same as CAO except you don't need to create a temp object, the temp object you're swapping with is the rvalue parameter object
  - Destructor
  - [ ] _How they work with inheritance_
  - use explicit in front of constructors that only take in one argument!

- [ ] Benefits of modularization: separating implementation from headers

  - [ ] reusability: low coupling means many places can use the same module
  - [ ] maintainability: able to test and debug separate things at once
  - [ ] abstraction: implementation details are hidden, client only knows public interface, allows for us to change stuff or make stuff more efficient easily

- [ ] Benefits of **encapsulation**: restricting direct access to some of the object/class's components, we want to treat objects as **black boxes**

  - hide implementation: be able to change implementation without client knowing
  - enforce invariants: instead of having clients mutate object directly, we can enforce rules about the class inside the class ourselves and force clients to go through our process
  - usually all fields should be `private`, use **getters** and **setters**
    - `operator<<` needs private fields to print out the object, but shouldn't be a member since it would put the `ostream` on the right, weird syntax, so you declare it as `friend`

- ==**Design patterns**: what they are, what problems they solve, implementation and example of one==

  - **Iterator**: mimic the behaviour of pointer but don't let client actually access pointer
    - created as a nested class inside the class you want to have an Iterator for
      - **must** declare outer class as a `friend` of the iterator in public section of Iterator class
    - need to implement (bare minimum):
      1. constructor
      2. `begin()`
      3. `end()`
      4. `operator*` (unary, not binary multiplication)
      5. `operator++`
      6. `operator!=`
      7. optional are `operator->`, `operator==`, `operator++(int)` (postfix increment)
    - first 6 things above **must** be implemented to use `auto it : lst` (for a copy) or `auto &it : lst` (for references no need for dereferencing) or similar in for loop
  - **Template Method**: subclasses want to override superclass behaviour but some aspects must stay the same
    - have the superclass have as much of the implementation that doesn't require overriding as possible, so that they are guaranteed to stay they same
    - delegate certain steps of the process to the subclasses without allowing them to completely change the structure of the overarching process
    - can enforce invariants through this
    - reduces code repetition
  - **Factory Method**: relies on different subclasses having different functionality for the sam goal
    - each subclass will have their own override of a single method or whatever they want to accomplish
    - Factory Method determines at runtime because of `virtual` functions the type of the object the method is invoked on, and calls the right method
  - **Visitor**: can implement double dispatch, where you choose virtual methods based on the runtime type of two objects, not just one
    - **structure**: two superclasses `A` and `B`, each with subclasses
      - `A` has a `virtual` method `f`
      - `B` has multiple pure `virtual` methods `g` for each subclass of `A` 
      - `A`'s subclasses override the method `f` that takes in a generic `B` and calls some method `g` on it with the subclass as a parameter
        - `f` is an overriding method in this case
      - `B`'s subclasses implement a method `g` for **each** subclass of `A` and defines behaviour based on the subclass
        - `g` is overriding an overloaded method
    - a call during runtime will resolve itself based on the correct `virtual` method of both classes
  - **Decorator**: want to be able to add functionality to an object at runtime
    - **structure:**
      - an abstract class `AbstractComponent` has children that are 'base' component objects, and it also has a `Decorator` child class that is also abstract
        - `Decorator` will have children that add functionality to the base components, and should have all the methods and fields that any component has
        - every `Decorator` **has a** `AbstractComponent` and **is a** `AbstractComponent`
        - it wraps another `AbstractComponent` that it interacts with through a field
  - **Observer**: classes that need to react to another class's data, follows pub/sub
    - **structure:** 
      - one class is the __publisher/subject__: it generates data
      - one or more classes are __subscriber/observer__ classes: they receive data and react to it
      - **subject** keeps track of all observers, can add or remove them
      - when something changes and it needs to notify each observer, it calls a `notify` method for each of the observers its keeping track of
      - **observers** keep track of their subject but don't do anything except add themselves to the subject's observer tracking list
      - until they get notified through their `notify` method, then they do what they have to do after getting the **subject**'s data
  - **MVC**
    - Single responsibility principle ==idiom==
    - __Model__: the data being represented
      - invariants, etc
    - __View__: the presentation of the data
      - Can have multiple views (_e.g. having both text and graphical output_)
      - Doesn't need to know about implementation details
      - Can implement the classic Observer ==Design Pattern== in which the view would be the observer
    - __Controller__: the manipulation of the data
      - Mediates control flow between model and view
      - May communicate with the user for input (or the View could do that)

- C++ templates: **a class parameterized by a type**

  - `template <typename T> class CLASSNAME { ... }` and use `T` anywhere you would use a type that influences the class
    - write the rest of the class the same
  - must write in the same `.h` file since the compiler writes a brand new class for each different type `T`

- **UML diagram rules**

  | Behaviour                           | Described by...                                 | Example                                                      |
  | ----------------------------------- | ----------------------------------------------- | ------------------------------------------------------------ |
  | Public visibility                   | `+`                                             | `+x: Integer`                                                |
  | Protected visibility                | `#`                                             | `#getYVec: Vector`                                           |
  | Private visibility                  | `-`                                             | `-x: List of Integers`                                       |
  | Composition)(*Owns-a* relationship) | arrow with solid filled-in diamond at other end | ![image-20181214125941152](/Users/alexieyizhe/Google Drive/University/2A/CS 246/Notes/review-final_exam.assets/image-20181214125941152-4810381.png) |
  | Aggregation (*Has-a* relationship)  | arrow with hollow bordered diamond at other end | ![image-20181214125932530](/Users/alexieyizhe/Google Drive/University/2A/CS 246/Notes/review-final_exam.assets/image-20181214125932530-4810372.png) |
  | _Is a_ relationship                 | arrow with nothing at the other end             |                                                              |
  | Virtual/pure virtual methods        | italicized                                      |                                                              |
  | Abstract class                      | class name italicized                           |                                                              |
  | Static fields and methods           | bolded                                          |                                                              |
  | function parameters                 | `(PARAMNAME : PARAMTYPE)`                       | `(mark : Integer)`                                           |

- **Inheritance**: super/subclasses, abstract classes and virtual methods, pure virtual methods

  - subclasses cannot access superclass private fields: this is so that you can **enforce invariants** in your class design

  - to solve the above^^, in subclass constructor, call superclass constructor in MIL if no default constructor exists

  - without pointers, assigning subclass to superclass will **slice** the subclass contents to **coerce** it into the size of the superclass

    - this is without pointers

  - with pointers without `virtual`, slicing doesnt happen but c++ uses type of pointer to check which method to run, not the type of the instance of the object

  - with pointers with `virtual`, methods choose which class method to invoke based on the _runtime_ type of the object, not the type of what's accessing it

    - `override` really is just a error-checking keyword that will cause code to not compile if your signatures don't match, you technically don't need it

  - do not use arrays of objects polymorphically, only arrays of pointers

  - inheritance with copy/move

    - always make the destructor virtual if a class has subclasses, even if the destructor doesn't do anything
    - if subclass doesn't have a big 5, it calls the superclass equivalent before reverting to default behaviour copying field by field
    - to write the big 5
      - call the superclass equivalent and then deal with the rest of the fields like you would a normal big 5 operator
      - make sure to `std::move()` when you pass into superclass equivalent

  - __partial assignment__ is when you copy/move a subclass through a superclass pointer and the superclass copy/move runs and only operates on the superclass fields, leaving the additional subclass fields the same

    - you can't override copy/move assignments since the signature is different, unless you wanna be able to assign every subclass to a single subclass
    - to solve, make sure all superclasses are **abstract**

  - __mixed assignment __is when you try to assign a subclass to a different subclass of the same parent class through the following operator:

    ```cpp
    Child1 & Child1::operator=(const Base &b) {
        ... // error will occur here when you assume that b is a Child1 type
    }
    ```

    - solve this by dynamic_casting the `b` object to a `Child1 &` type first and then working with the temporary object

- **Design Principles**:

  - Single responsibility idiom
    - a class should only have one reason to change, do not use a class for two different things like interaction and communicating results
  - Non-virtual interface idiom
    - all methods that clients can use (the interface) should **not** be `virtual`
    - all methods that can be implemented by subclasses or can be changed (`virtual` ones) should be `private` or `protected`
    - make sure all the code you want guaranteed to run is non-`virtual`
      - even if the function should be `virtual`, wrap it in a non-`virtual` method and make the guaranteed parts in the that method and only the specific parts should be in a `virtual` method
    - Generalizes the Template Method ==Design Pattern== by wrapping every virtual function with a Template Method
  - Resource Acquisition Is Initialization (RAII) idiom
    - every time you acquire resources (heap memory, new file), you must do it with initialization of an object
      - this allows for the resource to be released when the lifetime of the object ends
    - use smart pointers and vectors for this!
  - pImpl Idiom
    - hide all object fields in a different `XCLASS_impl.h` file so you can just forward declare it and clients don't have to depend on the implementation.
    - no other files except the `XCLASS.cc` file need to be recompiled if the implementation changes
    - leads to the Bridge ==Design Pattern== if you have a class heirarchy of implementations 
  - copy & swap idiom
    - make a temporary object just like the object you want to manipulate
    - do stuff to the temporary object (maybe even copy to the temp object)
    - swap it with the real object (could be yourself)
      - need to define your own **swap**!!!!
  - Coupling & Cohesion
    - want **low** coupling, modules communicate only through simple function calls with basic params/results
      - **NOT** high coupling: modules have access to everything of each other (they are `friends`, they affect each other's control flow)
    - want **high** cohesion: modules have elements that combine to perform exactly **one** task
      - **NOT** low cohesion: arbitrary group of random unrelated methods and stuff ex `<utility>` library (it's not enough to share a common theme)

- __Exceptions__:

  - stack unwinds until a handler is found or program terminates when reaches `main`
  - should never let a destructor throw because it will terminate immediately
    - even if you `noexcept(false)` and another destructor throws during stack unwinding, it will also terminate immediately if there are two exceptions at once
  - `delete` never throws
  - `emplace_back` never throws
  - `swap` never throws
  - pointer reassignment never throws
  - exception safety and strong guarantees
    - __Basic guarantee:__ If an exception occurs, the program will be in some valid state.
      - Nothing is leaked, class invariants must remain true,  no corrupted data structures
      - function `f` has two functions with strong guarantees, this function has basic guarantee because if it throws, you don't know if it's the first or second function that caused it, and if it's the second then the program's state will **not** be as if `f` was never called
    - __Strong guarantee:__ If an exception is raised while executing `f()`, the state of the program will be as if `f()` had not been called.
      - Either we get all the effects of `f()` (if it runs successfully) or we get none of the effects.
    - __No-throw guarantee:__ `f()` will never throw an exception and will always achieve its purpose.
      - This means you can't just never throw and suppress any exceptions, because it'll defeat the purpose.
    - use copy-and-swap idiom for strong guarantee:
      - copy to a temporary object: this can throw, but leaves original in intact state
      - do stuff to the temporary object: can throw, but also leaves original intact
      - swap original with temporary: never throws, so this will always work

- __Vectors and Maps__:

  - understand what `clear()` and `erase()` do
    - it makes the object go out of scope!
  - if key is not present while looking for a value with a key, inserts key with value default constructed
  - ==possible exam question: implement a balanced BST with `map`==

- __Compilation Dependencies__

  - Do you need to include a class `A`?
    - **Subclass of  `A`** ==YES==, similar to having object fields
    - **Has an object field of type `A`**: ==YES==, object fields require space allotment
    - **Has a pointer field of type `A`**: `NO`
    - **Declares method with type `A` as parameter:** `NO`
    - **Defines method with type `A` as parameter:** ==YES==

- **Casting**: differences between the different types, what each type does

  - `static_cast`: sensible, defined behaviour

    - **used for:** 
      - casting between primitive types like int and double
      - casting from a superclass pointer type to a subclass pointer type IF **the superclass pointer points to a subclass instance, otherwise undefined behaviour**
    - use if you don't need any checks and you know it will work, but will not compile if pointer cast is between incompatible types

  - `reinterpret_cast`: dangerous, weird behaviour, will convert any types, doesn't matter

  - `const_cast`: allows for 'casting away' a `const` of a value

    - **used for**: 

      - passing `const` values to non-const functions: modifying values that were initially const is undefined behaviour, don't do it! but values that were initially not const is fine

        ```cpp
        // undefined behaviour
        const int val = 10;
        const int *ptr = &val;
        f(const_cast<int *>(ptr)); // f is a function that mutates the value of the int *
        
        // the code below is fine
        int val = 10
        const int *ptr = &val;
        f(const_cast<int *>(ptr)); // f is a function that mutates the value of the int *
        ```

      - changing non-constant fields in a class inside a const member function

        ```cpp
        class Student {
            int i;
        public:
            f() {
                // initially, 'this' is a const Student* const type, meaning you cannot modify Student instance from 'this'
                (const_cast <student*>(this))->i = 5;
                // the above turns it into a Student * const, which is a constant pointer to a mutable student with a non-const field i
            }
        }
        ```

    - cannot be used to cast between different types, will error

  - `dynamic_cast`: convert from subclass to superclass (which can also be done without casting), or from superclass pointer to subclass pointer (as long as the superclass pointer points to a subclass instance)

    - **used for**:
      - casting from a superclass pointer type to a subclass pointer type, SUCCEEDS IF **the superclass pointer points to a subclass instance**
    - only works with **polymorphic** classes (classes that define or inherit at least one virtual function)
    - performs a runtime check that the pointer refers to a complete object of the destination type
    - throws `bad_cast` exception if you cast something other than a reference or pointer, or if you try to cast a superclass reference to a subclass
    - returns `nullptr` if you try to cast a superclass pointer to a subclass pointer
    - why not just use `static_cast`? sometimes, you can have a superclass pointer point to a subclass instance, in which case it will succeed or a superclass pointer point to a superclass instance, which will fail - you don't know until runtime
    - solves polymorphic assignment problem by casting superclass to subclass of that type first before assigning

  - `dynamic_pointer_cast`, `static_pointer_cast`, `const_pointer_cast` do the same thing as the above but for `shared_ptr`, 

- __Smart pointers__

  - `make_shared` and `make_unique` are exception safe, compared to `unique_ptr` and equivalent which can throw when constructing the value they're holding

    - `make_shared/unique` can only construct new objects, can't take in existing pointers

  - make sure you're constructing shared pointers from each other, otherwise there will be a double free

  - code such as `f(std::shared_ptr<int>(new int(42)), g())` can cause a memory leak if `g` gets called after `new int(42)` and throws an exception, 

    - this is bc you need all parameters to be values in a function before evaluating the entire function (think CS 135)
    - so `new int(42)` gets called, then `g()`, then `shared_ptr<int>()`, so if `g()` throws, then `new int(42)` is leaked

    | Pointer Type   | Can Copy?               | Can Move?                                                    |
    | -------------- | ----------------------- | ------------------------------------------------------------ |
    | Unique Pointer | No, pointers are unique | Yes, use `std::move(uptr)` to invoke move assignment operator and turn it into an _rvalue_, exception safe |
    | Shared pointer | Yes, exception safe     | Yes, exception safe                                          |

- __Template Functions__

  - functions that will work for any type `T` that has operators or iterators
  - uses functions passed in to perform on the object being iterated on
    - objects can be used by template functions too: known as **function objects**, can maintain state, use `operator()` override to define behaviour when called by template functions

- __Virtual pointers with single inheritance, virtual tables, dynamic dispatch__

  - each class w/ `virtual` method  has a **vtable**
    - _vtable_ has pointers to implementations of methods specific to that class
  - each instance of class has **vptr** to its _vtable_ created at object construction
  - versions of virtual methods are chosen to run based on runtime types of objects, and it, **adds to runtime speed cost**, known as **dynamic dispatch**
    1. follows the object's _vptr_ to the _vtable_
    2. looks for pointer to the `virtual` method being called
    3. runs the method from the pointer
  - **adds increased space cost** of additional pointer to objects of classes with a `virtual` method



- [ ] write code for:
  - [ ] `Node`
    - [ ] copy constructor
    - [ ] copy assignment operator
    - [ ] move constructor
    - [ ] move assignment operator
    - [ ] destructor
  - [ ] `LinkedList`
    - [ ] Iterator
- [ ] go over what each type of casting does
- [ ] practice writing templates
- [ ] 











# Concept Review from Midterm

### Bash Scripting

- Piping (`|`) hands output to another __program__ or __utility__; output redirection (`>`) passes output to another __file__ or __stream__.
- `stderr` is not buffered unlike other streams `stdin` `stdout`, displays output instantly
  - use `2>` to redirect `stderr` stream
- `#!/bin/bash` at the top for scripts
- single quotes suppress everything, double quotes allow for command interpretation inside the quote

| Purpose                                        | Syntax                                                       | Notes                                                        |
| ---------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| embed commands inside quotes or other commands | `$(your_cmd_here)`                                           | Single quotes will suppress everything                       |
| get arguments from bash command line           | `$1 $2 $# $*`, `$0` is name of program                       | 1st/2nd arg, # of args, all args                             |
| if statement                                   | `if [ $1 -neq "pass" ]; then` and `fi` to close              | `fi` to end if statement flow, **SPACES ARE MANDATORY**      |
| for loops                                      | `for i in {START_VAL..END_VAL..STEP_VAL}; do` and `done` to close | can also use `$(COMMAND)` or file                            |
| subroutines                                    | `foo() { do things }` and call with `foo`                    | functions get their own parameter set, so make sure to pass in command line parameters explicitly if needed |
| quit program                                   | `exit`                                                       |                                                              |
| AND, OR for if statements                      | `-a` and `-o`                                                |                                                              |
| file existence                                 | `-e`                                                         |                                                              |
| string length > 0                              | `-n`                                                         |                                                              |
| string equality                                | `=`                                                          |                                                              |
| integer equality                               | `-eq`, `-ne`, `-lt`, `-le`, `-gt`, `-ge`                     |                                                              |
| redirect to `stderr`                           | `echo MSG >&2`                                               |                                                              |
| swallow output                                 | redirect to `/dev/null`                                      |                                                              |
| loop through lines in file                     | `cat FILENAME | while read line; do` line is in `$line`, close with `done` |                                                              |

####Regex

| Syntax           | Signifies                                                    |
| ---------------- | ------------------------------------------------------------ |
| `^`              | Beginning of line                                            |
| `$`              | End of line                                                  |
| `|`              | OR groups (`(a|b)` matches stuff that matches either pattern `a` or `b`) |
| `()`             | Groups                                                       |
| `\b`             | Word boundary                                                |
| `\s`             | Whitespace (`\s` for NOT whitespace)                         |
| `\d`             | Digit                                                        |
| `.`              | any character except `\n`                                    |
| `[abc]`, `[a-z]` | `a` or `b` or `c`, letters from `a` to `z`                   |
| `[^a]`           | NOT `a`                                                      |
| `*`, `+`         | 0 or more, 1 or more (goes after char to be matched)         |
| `{n}`            | exactly `n `(goes after char to be matched)                  |
| `{n, m}`         | any amount from `n` to `m` (goes after char to be matched)   |
| `?`              | makes preceding pattern ungreedy                             |



------

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

------

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

------

### General Tips

- be aware of when you're using the stack and when you're using the heap
  - Heap is use when calling `new OBJ{}`
- don't use `using namespace std;` in `.h` files
- _separate compilation_ produces `.o` files called __object files__
- `static` fields and methods are associated with class, not specific instances
- `int main(int argc, char *argv[]){ }` to get arguments, `argv[0]` is always name of program, so `argc` is off by 1

------

### `Makefile`s

- the `.d` files keep track of all the dependencies of certain files, essentially creating a list of _all_ files that need to be checked, even if the file itself doesn't change
  - _e.g. changing the `.h` file should recompile the `.cc` file, but the `.cc` file itself doesn't change_ 

```makefile
CXX = g++
CXXFLAGS = -std=c++14 -Wall -MMD
EXEC = canvas
OBJECTS = canvas.o point.o rectangle.o a3q3.o
DEPENDS = ${OBJECTS:.o=.d}

${EXEC}: ${OBJECTS}
	${CXX} ${CXXFLAGS} ${OBJECTS} -o ${EXEC}

-include ${DEPENDS}

.PHONY: clean

clean:
	rm ${OBJECTS} ${EXEC} ${DEPENDS}

```

------

### Invariants

- 



------

#### Random

- `new X{}` returns an _rvalue_
- defining a destructor for a class preserves all other methods in the "big 5"
- if you write a class $A$ with no copy constructor (by making that copy constructor nonsensical) and you write another class $B$ with said class $A$ as a field, then you lose the copy constructor for $B$
- 