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
   - __WARNING:__ this will compile, but is syntax for something different (deals with rvalues) - be careful!
 - Create an array of references

You __can__ do the following with references:
 - Pass them as function parameters
   - useful for keeping the speed of pass-by-pointer while not needing to dereference every time you use it in the f'n
 - Set a reference to const
   - useful in same case as above but with the added requirement of the f'n not modifying the value  
   - also allows you to pass in values that are not normally lvalues - so:
     - for `if int g(const int &n) {...}`, `g(5)` is valid even though `5` is not an lvalue
