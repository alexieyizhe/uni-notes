__CS 246 |__ Nov 13, 2018

# Maps & Design Patterns (cont.)

## Factory Method ==Pattern== 

This pattern is used when a creator class relies on different subclasses to do different things.



#### UML Diagram

![Image result for factory method design pattern uml](https://upload.wikimedia.org/wikipedia/commons/e/ed/Factory_Method_UML_class_diagram.png)



#### Implementation

We take the example of a video game with two kinds of enemies: turtles and bullets. The system randomly sends turtles or bullets, but bullets are more frequently seen in harder levels. Our problem is that we never know exactly which enemy comes next, so we can't call the turtle and bullet constructors directly.

```cpp
class Level { 
public:
    virtual Enemy* createEnemy() = 0; // this is known as a *factory method*
};


class Easy:public Level {
public:
    Enemy *createEnemy() override {
        // this method will create mostly turtles
    }
};

class Hard:public Level {
public:
    Enemy *createEnemy() override {
        // this will create more bullets
    }
};


// In the client:
Level *l = ...;
Enemy *e = l->createEnemy(); // factory method decides what we get
```



## Template Method ==Pattern==

This pattern is used when we want subclasses to override superclass behaviour but some aspects must stay the same.

#### UML Diagram

![Image result for template method design pattern uml](https://sourcemaking.com/files/v2/content/patterns/Template_method_example.png)



#### Implementation

Consider the video game example in the Factory Method design pattern above. We now extend it to say that there are two types of turtle enemies: red turtles and green turtles. They are mostly drawn the same, but differ slightly in their shell colour.

```cpp
class Turtle {
public:
    void draw() {
        drawHead();
        drawShell();
        drawFeet();
    }
private:
    void drawHead() { ... };
    virtual void drawshell() = 0;
    void drawFeet() { ... };
}


class RedTurtle:public Turtle {
    void drawShell() override { ... } // draw red shell
};

class GreenTurtle:public Turtle {
    void drawShell() override { ... } // draw green shell
};
```

- Subclasses cannot change the way a turtle is drawn, but can change the way the shell is drawn
- Reduces code repetition as well

> This has nothing to do with C++ templates.



### The Non-Virtual Interface (NVI) idiom

Notice that a public virtual method is really two things:

1. An interface to the client: *it indicates provided behaviour with pre/post conditions.*
2. An interface to subclasses: *it provides a "hook" to insert specialized behaviour.*

This is a bit conflicting: it's hard to separate these ideas if they are tied to the same one function. If you want to be able to split a virtual method into two, maybe with some constant code in between, you risk changing the client's interface. 

To make sure that overriding functions conform to the pre/post conditions, the __NVI__ says that:

- All `public` methods should be non-`virtual`.
- All `virtual` methods should be `private` (or at least `protected`).
  - With the one exception of the destructor

---

__Ex. Digital Media__

```cpp
// initial implementation
class DigitalMedia {
public:
    virtual voide play() = 0;
};

// NVI-approved implementation
class DigitalMedia {
public:
    void play() {
        // could add code before ( ex. checkCopyright() )
        doPlay();
        // could add code after ( ex. updatePlayCount() )
        // guarantees pre/post code will be called
    }
    
private:
    virtual voide doPlay() = 0; // subclasses override this method
};
```

---

This generalizes the Template Method design pattern by essentially __putting every virtual function inside a template method.__



## Maps

Maps are a part of the STL. They are used for creating dictionaries: "arrays" that map a __key__ to a __value__. You can use it by placing `#include <map>`in the file.

| Syntax                       | Purpose                                                      |
| ---------------------------- | ------------------------------------------------------------ |
| `std::map<string, int> m;`   | Initialize a map                                             |
| `m["abc"] = 1;`              | Add key-value pair to map                                    |
| `m.erase("abc");`            | Removing pair from map                                       |
| `cout << m["ghi"];`          | Accessing pair in map (if `key` is not present, it is inserted with the value default constructed) |
| `if(m.count("abc")) { ... }` | Checking for existence of key in map (returns `0` if not found, `1` if found) |



> Lushman says: use `map` if you want to implement a balanced BST.





## Visitor ==Pattern==

This pattern is used for implementing __double dispatch__: choosing virtual methods based on the type of _two_ objects at runtime (as opposed to one).

#### Implementation

Consider the case of the video game example above again. Suppose we want to implement attacking, which determines what happens based on which `Weapon` is used _and_ on which `Enemy` is being attacked.

If `attack()` is a method of `Enemy`|`Weapon` (choose 1), we determine based on the type of `Enemy`|`Weapon` but not on `Weapon`|`Enemy`.

```cpp
class Enemy {
public:
    virtual void beStruckBy(Weapon &w) = 0;
};

class Turtle:public Enemy {
public:
    void beStruckBy(Weapon &w) override { w.strike(*this); } // *this is a Turtle
};

class Bullet:public Enemy {
public:
    void beStruckBy(Weapon &w) override { w.strike(*this); } // *this is a Bullet    
};



class Weapon {
public: 
    virtual void strike(Turtle &t) = 0; // these are
    virtual void strike(Bullet &b) = 0; // overloads
};

class Stick:public Weapon {
public:
    void strike(Turtle &t) override {
        // strike Turtle t with this Stick
    }
    void strike(Bullet &b) override {
        // strike Bullet with this Stick
    }
};
// something similar for a Rock Weapon



// In client:
Enemy *e = new Bullet { ... };
Weapon *w = new Rock { ... };

c->beStruckBy(*w);
```

On line 41:

1. `Bullet:beStruckBy` runs (virtual method)
2. `Weapon::strike` is called (`*this` is Bullet, so Bullet version is chosen at compile time)
3. Virtual method call resolves to `Rock::strike(Bullet &)`



#### Adding Functionality to Existing Classes

The Visitor pattern can also be used to add functionality to existing classes, without changing or recompiling the classes themselves.

```cpp
class Book {
public:
    ...
    virtual void accept(BookVisitor &v) { v.visit(*this); }
};

class Text:public Book {
public:
    ...
    void accept(BookVisitor &v) { v.visit(*this); }
};
// this is the Visitor pattern in a different form
```



