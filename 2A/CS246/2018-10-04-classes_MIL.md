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

Every class already comes with a default (0-arg) constructor (_ex._ `Vec v;`), but it goes away if you define your own constructor.

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

> Lushman says: Embrace the MIL! (use it anywhere you possibly can)
