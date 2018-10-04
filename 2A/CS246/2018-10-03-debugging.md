**CS 246 |** Oct 3, 2018


# Debugging
This courses uses __Valgrind__ as a test suite (_Marmoset_). Valgrind checks for memory leaks.

### Valgrind
  - Invoke using `valgrind VALGRIND_ARG ... PROG_NAME PROG_ARG ...`
  - Valgrind will report memory as __definitely lost__, __possibly lost__, __indirectly lost__, and __still reachable__
    - _indirectly lost_ means first pointer is lost
    - _still reachable_ means valid pointer found right before program terminates
