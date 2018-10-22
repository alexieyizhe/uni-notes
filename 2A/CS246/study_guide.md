- be aware of when you're using the stack and when you're using the heap 
- MIL for everything but especially
  - `const` member fields
  - members that are references (`&`)
  - members that are objects without a default constructor (default was overwritten by user)
  - MIL takes precedence over inline declarations/initializations
- The 5 methods we should work with for class/object creation:
  - copy constructor
    - called when: obj is constructed as a copy, pass by value, returning a value
  - copy assignment operator
  - move constructor
  - move assignment operator
  - destructor
- don't use `using namespace std;` in `.h` files
- 