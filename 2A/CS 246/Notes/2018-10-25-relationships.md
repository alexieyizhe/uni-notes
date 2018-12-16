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

---

__Ex. Ownership and Compositions__
A car owns four wheels - a wheel is part of a car. 

1. Destroying the car $\Longrightarrow$ destroying the wheels. 
2. Duplicating the car $\Longrightarrow$ duplicating (copying) the wheels.

---

#### Modelling a Relationship: Compositions of Classes

We model this through containing each class as a box, and drawing an arrow from the owner to the owned class. The other end of the arrow (the end on the owner) has a _solid filled-in_ diamond on it.

## Aggregation

Suppose now instead of having wheels in a car ("__owns a__"), you now have wheels in a catalogue. The catalogue contains the parts, but the parts have an independent existence. This is also known as an aggregation, or a "__has a__" relationship.

If $A$ _owns a_ $B$, then _typically:_

1. $B$ exists apart from its association with $A$.
2. If $A$ is destroyed, $B$ is __not__ destroyed - it lives on.
3. If $A$ is copied, $B$ is not (shallow copy).
   - This means copies of $A$ share the same $B$ as the original.

---

__Ex. Aggregation__: Ducks in a pond

```cpp
class Pond {
    Duck *duck[maxDucks]; // notice this is an array: we don't want ducks to be deleted if the pond is
    ...
}
```

---

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

If you want to give subclass access to certain members, we can use `protected` visibility, like so:

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





