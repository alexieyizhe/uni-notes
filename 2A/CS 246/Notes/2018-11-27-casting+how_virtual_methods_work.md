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

>A useful situation for `const_cast` is if you have no control over methods you're using but you know they are `const` (_i.e. someone who doesn't use `const` parameters in their code_).

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



#Virtual Methods

If we have a virtual method, the class also contains a pointer that's known as a `vptr`. The location of the base class obect is stored in a **Vtable**. 