__CS 246 |__ Nov 8, 2018

# Exceptions (cont.)

A handler can act as a catch-all.

```cpp
try { 
	// do stuff here
} catch(...) { // the ellipses are literal
    // do other stuff here    
}
```

You can throw any type you want, not just exceptions. 

```cpp
class BadInput{};
...
throw BadInput{};
```

However, exceptions are not optimized since they are intended for exceptional circumstances, like their name implies. You shouldn't be using them for more general use cases like returning values, etc.

#### Exceptions & The Big 5

When `new` fails, it throws a `std::bad_alloc` exception. 

You should __never let a destructor throw an exception.__  It will cause the program to abort immediately. If you want to let a destructor throw, you can tag it with `noexcept(false)`, but if a destructor is running during stack unwinding while dealing with another exception and _that_ destructor throws as well, you now have 2 active (unhandled) exceptions. This will _also_ cause the program to abort immediately. 

_exceptions will be covered more later on_



# More Design Patterns

## Observer ==Pattern==

This pattern is used when you have classes that need to react to another class's data. It follows the publish/subscribe model. 

- One class is the __publisher/subject__: it generates data. 
- One or more classes are __subscriber/observer__ classes: they receive data and react to it.

> You can obviously have multiple classes subscribed to a single subject: think about people listening to a radio station (a single subject).
>
> You can also have a subscriber class subscribed to more than one subject: think about a graph in Excel - it's subscribed to all the cells it's pulling data from and will update automatically if any of them change.

#### UML Diagram

![Image result for observer pattern uml](https://www.cs.mcgill.ca/~hv/classes/CS400/01.hchen/doc/observer/observer.gif)

The following sequence occurs when something changes in the publisher/subject:

1. Subject's state is updated.
2. `Subject::notify()` is invoked -it calls each observer's `update()` 
   - This is going to be the `ConcreteObserver`'s `update()` since `Observer` is an abstract class and `update()` is virtual.
3. Each observer calls `ConcreteSubject::getState()` to query the state and reacts to this updated state accordingly.

#### Implementation

One implementation of the pattern is as follows:

```cpp
class Subject {
    vector <Observer *> observers;
    
public:
    void attach(Observer *ob) { observers.emplace_back(ob); }
    void detach(Observer *ob) { ... } // just look for this observer in observers list and remove it
    void notifyObservers() { for(auto &ob:observers) ob->notify(); }
    virtual ~Subject() = 0; // so that the Subject class is abstract
};
    
Subject::~Subject() {}


class Observer {
    
public:
    virtual void notify() = 0;
    virtual ~Observer();
} 
```

To give a concrete example, imagine running a horse race. You will need a subject to publish winners of the race, and the observers will be the individual bettors. That implementation will be as follows:

```cpp
class HorseRace::public Subject {
    ifstream in; // source of horse race results
    string lastWinner;
    
public:
    HorseRace(string source): in{source} {}
    bool runRace() { // we return a bool to indicate if a race has been run (if we haven't reached EOF)
        in >> lastWinner;
        return in;
    }
    string getState() { return lastWinner; }
};


class Bettor:public Observer {
    HorseRace *subject;
    string name, myHorse;
    
public:
    Bettor(...): ,,, {
        subject->attach(this);
    }
    ~Bettor() { subject->detach(this); } // we do not delete subject
    void notify() {
        string winner = subject->getState();
        if(winner == myHorse) cout << "I won!" << endl;
        else cout << ":(" << endl;
    }
}


// main.cc
HorseRace hr;
Bettor Larry(&hr, "Larry", "RunsLikeACow"); // amazing name (both the horse and the bettor)
... // probably other bettors

while(hr.runRace()) {
    hr.notifyObservers();
}
```

## Decorator ==Pattern==

This pattern is used when we want to add/remove functionality from an object at runtime.

#### UML Diagram

The following classes exist:

- A `Component` is an interface with operations that your objects will provide.
- A `ConcreteComponent` implements the interface: it is a basic object.
- Many subclasses will all inherit from `Decorator`, which inherits from `Component`
  - This means every Decorator _is a_ `Component` and _has a_ `Component`.

![Image result for decorator pattern uml](https://mertarauh.com/wp-content/uploads/2016/05/Decorator.gif)

> As an example, take a windowing system in an operating system. 
>
> A `Window w/ scrollbar` _is a_ `Window`, and _has a_ pointer to the underlying plain `Window`.
> A `Window w/ scrollbar+menu` _is a_ `Window`, and _has a_ pointer to a `Window w/ scrollbar`, which _has a_ pointer to a plain `Window`.
>
> All of these will inherit from `AbstractWindow`, so `Window` methods can be used polymorphically on all of the above.

#### Implementation

We take the example of a pizza. _yum_

```cpp
class Pizza {
public:
	virtual float price() const = 0;
    virtual string desc() const = 0;
    virtual ~Pizza() {}
    
};


class CrustAndSauce: public Pizza {
public:
    float price() const override { return 5.99; }
    string desc() const override { return "Pizza"; }
    
};


class Decorator:public Pizza {
protected:
    Pizza *component;
    
public:
    Decorator(Pizza *p): component{p} {}
    virtual ~Decorator() { delete component; }
    
};


class StuffedCrust:public Decorator {
public:
    float price() { return component->price() + 2.69; }
    string desc() { return component->desc() + " with Stuffed Crust"; }
    
};

// similarly for other subclasses like toppings, dipping sauce, etc
```



> There isn't an abstract general implementation of the pattern itself, since a `Decorator` is always a subclass that inherits from some implemented class (so we had to start with the pizza example).

