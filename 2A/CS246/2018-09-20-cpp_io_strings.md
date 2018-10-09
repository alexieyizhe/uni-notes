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
| C Strings | C++ Strings |
| ------ | ----- |
| stored in char arrays | stored as a `string` type |
| forces writer to manage memory   | dynamically change their size  |
| requires a null terminator to properly signal EOS  | no null terminator required, safer to manipulate  |

 - Use by including `#include <string>`
 - Define with `string s = "hello";`
 - Note that this string is __still a C-style string__ (_i.e._ a char array), but a C++ string is created from the C string on initialization

### String Operations
| Operation | Syntax |
| ------ | ----- |
| Equality/Inequality | `s1 == s2`/`s1 != s2` |
| Comparison (lexicographic) | `s1 <= s2`/`s1 >= s2` |
| Length   | `s1.length() // O(1) efficiency !!`  |
| Extracting Chars  | `s[0]`, `s[20]`, _etc_  |
| Concatenation | `s3 = s1 + s2`, `s4 += s3` |
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
