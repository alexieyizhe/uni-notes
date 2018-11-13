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