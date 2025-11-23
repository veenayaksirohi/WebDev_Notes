---
tags:
  - python
  - oop
  - classes
  - objects
  - programming
aliases:
  - Python OOP
  - Object Oriented Programming
date: 2025-11-17
---

# 🧱 7. Object-Oriented Programming (OOP) — Python

## 📜 Table of Contents
- [[#Overview|📝 Overview]]
- [[#Classes-and-Objects|🏗️ Classes & Objects]]
- [[#Attributes-and-Methods|🔹 Attributes & Methods]]
- [[#Object-Lifecycle|🔄 Object Lifecycle]]
- [[#OOP-Principles|🧬 OOP Principles]]
  - Inheritance
  - Polymorphism
  - Encapsulation
  - Abstraction
- [[#Magic-Methods|💫 Magic (Dunder) Methods]]
- [[#Advanced-OOP|🏛️ Advanced OOP]]
  - Class Methods  
  - Static Methods  
  - Metaclasses
- [[#Interview-QA|🎯 Interview Q&A]]
- [[#Navigation|🔗 Navigation]]

---

# 📝 Overview

Object-Oriented Programming (OOP) is a way of structuring Python programs using:

- **Classes** → Blueprints  
- **Objects** → Real implementations  
- **Attributes** → Data part  
- **Methods** → Behavior part  

OOP helps you build:

✔ Modular code  
✔ Reusable logic  
✔ Scalable software  
✔ Real-world models (Dog, Car, BankAccount, User, Employee…)

Python supports all major OOP pillars:

- **Encapsulation**  
- **Inheritance**  
- **Polymorphism**  
- **Abstraction**

---

# 🏗️ Classes and Objects

### ✔ What is a class?

A **class** is a blueprint/template for creating objects.

```python
class Dog:
    pass
````

### ✔ What is an object?

An **object** is an instance (copy) of a class.

```python
d = Dog()
print(type(d))  
# <class '__main__.Dog'>
```

---

## 📌 Real-Example Class

```python
class Dog:
    species = "Canine"   # class variable

    def __init__(self, name, age):
        self.name = name   # instance variable
        self.age = age     # instance variable

dog1 = Dog("Buddy", 3)
dog2 = Dog("Charlie", 4)
```

---

## 🧪 Object Components

Each object has:

### **1. Identity** → memory location

### **2. State** → attributes

### **3. Behavior** → methods

Example:

```python
dog1.name   # state  
dog1.age    # state
dog1.bark() # behavior
```

---

## 👤 Self Parameter (VERY IMPORTANT)

* `self` refers to the **current object**.
* Used to access variables and methods inside the class.

```python
class Dog:
    def __init__(self, name):
        self.name = name

    def bark(self):
        print(self.name, "is barking")
```

---

## 📌 Example — Multiple Objects

```python
dog1 = Dog("Rocky")
dog2 = Dog("Milo")

print(dog1.name)  
print(dog2.name)
```

Both objects have THEIR OWN copy of `name`.

---

## 🧪 Difference Between Class & Object

| Concept    | Meaning         | Example      |
| ---------- | --------------- | ------------ |
| **Class**  | Blueprint       | `class Car:` |
| **Object** | Instance create |              |
#  **Attributes, Methods & Object Lifecycle**
# 🔹 Attributes & Methods

In Python OOP, objects store **data** in *attributes* and define **behavior** in *methods*.

---

## 🧩 Types of Attributes

### ✔ 1. **Instance Variables** (object-level)

- Unique for **each object**
- Defined inside `__init__` or inside methods using `self`

```python
class Dog:
    def __init__(self, name):
        self.name = name        # instance variable
````

📌 Every object gets its own value:

```python
d1 = Dog("Rocky")
d2 = Dog("Milo")

print(d1.name)  # Rocky
print(d2.name)  # Milo
```

---

### ✔ 2. **Class Variables** (shared across objects)

* Declared **outside methods**
* Same value for **all objects**

```python
class Dog:
    species = "Canine"     # class variable
```

```python
print(Dog.species)
print(d1.species)          # also works
```

---

## 🆚 Instance vs Class Variables

| Feature    | Instance Variable | Class Variable   |
| ---------- | ----------------- | ---------------- |
| Stored in  | object memory     | class memory     |
| Shared?    | ❌ No              | ✔ Yes            |
| Access via | `self.variable`   | `Class.variable` |

---

# 🔧 Methods in Python OOP

### ✔ 1. **Instance Methods** (most common)

* Take `self`
* Work with instance data

```python
class Dog:
    def bark(self):
        print("Woof!")
```

---

### ✔ 2. **Class Methods**

Use `@classmethod` and `cls`.

```python
class Dog:
    species = "Canine"

    @classmethod
    def info(cls):
        return cls.species
```

---

### ✔ 3. **Static Methods**

No `self`
No `cls`
General-purpose utilities.

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b
```

---

# 🔄 Object Lifecycle

(Constructors & Destructors)

---

## 🟩 **Constructor — `__init__`**

Runs **automatically** when an object is created.

```python
class Dog:
    def __init__(self, name):
        self.name = name
        print("Dog created!")
```

---

## 🟥 **Destructor — `__del__`**

Runs when object is destroyed.

```python
class Dog:
    def __del__(self):
        print("Dog object deleted")
```

📌 Python garbage collector calls it automatically.
❗ Do NOT rely on destructors for important cleanup.

---

# 📘 Example — Full Lifecycle

```python
class Car:
    wheels = 4                # class variable

    def __init__(self, brand):
        self.brand = brand    # instance variable
        print("Car created:", brand)

    def info(self):
        print(self.brand, self.wheels)

    @classmethod
    def change_wheels(cls, n):
        cls.wheels = n

    @staticmethod
    def greet():
        print("Welcome!")

    def __del__(self):
        print("Car destroyed")
```

Usage:

```python
c1 = Car("BMW")
c1.info()

Car.change_wheels(6)
c1.info()

Car.greet()
```

---

# 📌 Best Practices (Very Important for Interviews)

* Always use **meaningful variable names**
* Keep **instance variables inside `__init__`**
* Use **class variables for shared constants**
* Prefer `@staticmethod` for helper utilities
* Prefer `@classmethod` for alternative constructors
  Example:

```python
@classmethod
def from_year(cls, year):
    return cls(f"Car-{year}")
```

* Don’t overuse `__del__` (unpredictable in Python)

---

# 🎯 Interview Snippets (Fast Revision)

### **Q1. Instance vs Class variables?**

Instance → each object has its own
Class → shared by all objects

### **Q2. What does `self` do?**

Points to the current object

### **Q3. Why use `@classmethod`?**

To modify class state and create alternative constructors

### **Q4. What’s th# 🧵 Core OOP Principles**


_(Inheritance, Polymorphism, Encapsulation, Abstractiona
Obsidian:

# 🧵 7.3 — Core OOP Principles

Python supports the **four pillars of Object-Oriented Programming**, making code reusable, modular, and scalable.

- Inheritance  
- Polymorphism  
- Encapsulation  
- Abstraction  

---

# 🟩 1. Inheritance  
Allows one class (**child**) to use properties/methods of another class (**parent**).

### ✔ Basic Example

```python
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):     # Dog inherits Animal
    def bark(self):
        print("Woof!")
````

Usage:

```python
d = Dog()
d.speak()   # from Animal
d.bark()    # from Dog
```

---

## 🧱 Types of Inheritance in Python

|Type|Example|
|---|---|
|Single|A → B|
|Multilevel|A → B → C|
|Multiple|A, B → C|
|Hierarchical|A → B, C, D|
|Hybrid|Mixed|

### ✔ Examples

#### **Single Inheritance**

```python
class Animal:
    pass

class Dog(Animal):
    pass
```

#### **Multilevel**

```python
class A:
    pass

class B(A):
    pass

class C(B):
    pass
```


# 🟦 . Polymorphism

Polymorphism means "**many forms**."

- The **same method or operation** behaves differently for different objects.
    
- **Flexible code**: You don’t care about the type, just that it supports the operation.
    

## **Types of Polymorphism in Python**

## 1. **Compile-Time Polymorphism** (Fake in Python)

Python doesn’t do true **method overloading**, but mimics it using default/variable arguments.

**Example:**
```python
class Animal:
    def sound(self):
        return "Some generic sound"

class Dog(Animal):
    def sound(self):
        return "Bark"

class Cat(Animal):
    def sound(self):
        return "Meow"

animals = [Dog(), Cat(), Animal()]
for animal in animals:
    print(animal.sound())
# Output:
# Bark
# Meow
# Some generic sound
```

**Explanation:**

- One method handles any number of arguments, giving illusion of overloading.
    

## 2. **Run-Time Polymorphism** (Method Overriding, Duck Typing, Operator Overloading)

**A. Method Overriding**

- **Child class redefines parent class method.**
    

```python
class Pen:
    def use(self):
        return "Writing"

class Eraser:
    def use(self):
        return "Erasing"

def perform_task(tool):
    print(tool.use())

perform_task(Pen())     # Writing
perform_task(Eraser())  # Erasing
```
**Output:**

text

`Bark Meow Some generic sound`

- The same method name (`sound`), different behaviors depending on object.
    

**B. Duck Typing**

- As long as an object has the right method, it works!
    

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(2, 3)
v2 = Vector(4, 5)
print(v1 + v2)  # Output: Vector(6, 8)
```

**Output:**

text

`Writing Erasing`

- `perform_task` works with any object that has a `use()` method.
    

**C. Operator Overloading**

- Same operator (`+`) does different things based on type.
    

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(2, 3)
v2 = Vector(4, 5)
print(v1 + v2)  # Output: Vector(6, 8)
```

## **Polymorphism in Built-In Functions**

Many built-in Python functions are naturally polymorphic:

```python

print(len("Hello"))         # Output: 5 (string length)
print(len([1, 2, 3]))       # Output: 3 (list length)
print(max(1, 3, 2))         # Output: 3 (max of ints)
print(max("a", "z", "m"))   # Output: z (max in strings)
```

---
# 🟥 . Encapsulation

Encapsulation is **bundling data and methods** together and restricting direct access to some attributes.

- **Public**: `self.name` — accessible anywhere.
    
- **Protected**: `self._breed` — accessible in class and subclasses. Use single `_` by convention.
    
- **Private**: `self.__age` — accessible only inside the class. Double underscore triggers name mangling.
    

**Example:**

```python

class Dog:
    def __init__(self, name, breed, age):
        self.name = name         # public
        self._breed = breed      # protected (convention)
        self.__age = age         # private (name mangling)

    def get_age(self):
        return self.__age

    def set_age(self, age):
        if age > 0:
            self.__age = age
        else:
            print("Invalid age!")

dog = Dog("Buddy", "Labrador", 3)
print(dog.name)          # Buddy (public)
print(dog._breed)        # Labrador (protected, accessible but not recommended)
# print(dog.__age)       # AttributeError: 'Dog' object has no attribute '__age'
print(dog.get_age())     # 3
dog.set_age(5)
print(dog.get_age())     # 5
```

**Usage:**

- Restricts direct access to sensitive data.
    
- Use getter and setter methods for control.
    

---

# 🟨 . Abstraction
### What Is Abstraction?

- Abstraction is one of the core OOP principles: **hiding complexity** and **exposing only what’s necessary**.
    
- It means creating a simple interface to work with, while the inner implementation (the “how”) is hidden.
    
- Think of abstraction like a TV remote: you press buttons to change volume or channel without knowing how the electronics inside work.

---

### Why Use Abstraction?

- To **simplify** complex systems: you don’t need to expose all inner details of a class.
    
- To **enforce a contract**: ensure subclasses implement certain methods (via abstract methods).
    
- To **make code more maintainable**: internal changes can be made without affecting external user-interface.
    
- To **provide a blueprint** (interface) for related classes: abstract base classes define common behavior.
    

---

### How to Implement Abstraction in Python

Python provides the `abc` module (Abstract Base Classes) to define abstract classes and methods. 
#### Key Steps:

1. **Import** `ABC` and `@abstractmethod` from `abc` module. 
    
2. **Define** a class inheriting from `ABC` — this becomes an abstract base class (cannot be instantiated if it has abstract methods).
    
3. **Decorate** methods with `@abstractmethod` to mark them as abstract: subclasses must implement these. 
    
4. **Implement** those abstract methods in concrete subclasses.
    

---

### Code Example

```python
from abc import ABC, abstractmethod

class Vehicle(ABC):
    @abstractmethod
    def start_engine(self):
        pass

    @abstractmethod
    def stop_engine(self):
        pass

    def honk(self):
        print("Beep beep!")  # concrete method

class Car(Vehicle):
    def start_engine(self):
        print("Car engine started.")

    def stop_engine(self):
        print("Car engine stopped.")

class Bike(Vehicle):
    def start_engine(self):
        print("Bike engine started.")

    def stop_engine(self):
        print("Bike engine stopped.")

# Usage:
c = Car()
c.start_engine()  # Car engine started.
c.honk()          # Beep beep!

b = Bike()
b.start_engine()  # Bike engine started.
```

- `Vehicle` is **abstract** because it defines abstract methods `start_engine` and `stop_engine`. 
    
- You **cannot** do `Vehicle()` directly — you'd get a `TypeError` because it has unimplemented abstract methods.
    
- Subclasses (`Car`, `Bike`) must implement both abstract methods, or they remain ab

# 📘 Summary Diagram

```
             OOP Principles
   ┌────────────────────────────────┐
   │  Inheritance   → Code reuse    │
   │  Polymorphism  → Many forms    │
   │  Encapsulation → Data hiding   │
   │  Abstraction   → Simplify use  │
   └────────────────────────────────┘
```

---

# 🎯 Interview Q&A (High-yield)

### **Q1. What is inheritance? Why is it useful?**

→ Allows reusing code and creating class hierarchies.

---

### **Q2. Difference between overriding & overloading?**

- **Overriding** → redefining method in child class (Python supports).
    
- **Overloading** → same method name with different parameters (Python does NOT support; simulated with `*args`).
    

---

### **Q3. What is polymorphism?**

Same interface, different implementations. Example: `speak()` in Dog, Cat.

---

### **Q4. What is encapsulation?**

Bundling data + methods, using private/protected members.

---

### **Q5. What is abstraction?**

Hiding implementation details using ABCs and abstract methods.

---

### **Q6. What is duck typing?**

"If it acts like a duck, we treat it as a duck."  
Python checks **behavior**, not type.

---

# **Magic (Dunder) Methods & Advanced OOP**

*(Dunder methods, class methods, static methods, metaclasses)*

Magic methods (also called **dunder methods**) let you control how your objects behave with:
- operators (`+`, `-`, `==`, `>`)
- built-in functions (`len()`, `str()`)
- object creation (`__new__`, `__init__`)
- iteration
- context managers (`with`)

They unlock Python's most powerful OOP features.

---

# ✨ 1. What Are Dunder Methods?

**Dunder** = “Double UNDERSCORE”  
Example: `__init__`, `__str__`, `__len__`.

They **customize object behavior**, making classes feel like built-in types.

---

# 🟩 2. Core Magic Methods (Most Used)

## ✔ `__init__` — Constructor
Runs when an object is created.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
````

---

## ✔ `__str__` — User-friendly String

Controls `print(obj)`.

```python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return f"Book: {self.title}"

print(Book("Python"))  # Book: Python
```

---

## ✔ `__repr__` — Developer-friendly String

Used in debugging, interactive console.

```python
def __repr__(self):
    return f"Book({self.title!r})"
```

---

## ✔ `__len__` — Length of object

```python
class Team:
    def __init__(self, members):
        self.members = members

    def __len__(self):
        return len(self.members)

t = Team(["Alex", "Bob"])
len(t)   # 2
```

---

## ✔ `__add__` — Custom + Operator

```python
class Vector:
    def __init__(self, x, y):
        self.x = x; self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
```

---

## ✔ `__eq__` — Equality `==`

```python
def __eq__(self, other):
    return self.x == other.x and self.y == other.y
```

---

## ✔ `__gt__`, `__lt__` — Comparisons

```python
def __lt__(self, other):
    return self.age < other.age
```

---

## ✔ `__call__` — Make object callable like a function

```python
class Greeter:
    def __call__(self, name):
        print("Hello", name)

g = Greeter()
g("Alex")  # behaves like a function
```

---

## ✔ `__getitem__`, `__setitem__`

Make objects act like lists/dictionaries.

```python
class Box:
    def __init__(self):
        self.items = {}

    def __setitem__(self, key, value):
        self.items[key] = value

    def __getitem__(self, key):
        return self.items[key]
```

---

## ✔ `__iter__` — Make class iterable

```python
class Counter:
    def __init__(self, n):
        self.n = n

    def __iter__(self):
        return iter(range(self.n))
```

---

## ✔ `__enter__` and `__exit__` — Context Manager (`with`)

```python
class FileManager:
    def __init__(self, filename):
        self.filename = filename

    def __enter__(self):
        self.f = open(self.filename)
        return self.f

    def __exit__(self, *args):
        self.f.close()
```

Usage:

```python
with FileManager("data.txt") as f:
    print(f.read())
```

---

# 🔥 3. Advanced OOP Features

---

# 🟦 Class Methods (`@classmethod`)

* First argument is **cls**
* Works on the class, not the object
* Useful for alternative constructors

### Example:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, data):
        name, age = data.split("-")
        return cls(name, int(age))
```

Usage:

```python
p = Person.from_string("Alex-25")
```

---

# 🟨 Static Methods (`@staticmethod`)

* No `self`
* No `cls`
* Utility/helper functions inside a class

```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b
```

Usage:

```python
Math.add(4, 5)
```

---

# 🟥 Class vs Static vs Instance Methods

| Method Type | Decorator       | First Arg | Uses                                     |
| ----------- | --------------- | --------- | ---------------------------------------- |
| Instance    | None            | `self`    | Access object data                       |
| Class       | `@classmethod`  | `cls`     | Alternate constructors, class-level data |
| Static      | `@staticmethod` | none      | Utilities, helpers                       |

---

# 🧬 4. Metaclasses (High-level Concept)

Metaclass = “Class that creates classes”.

Default metaclass in Python = `type`.

### You rarely need to create custom metaclasses.

Example:

```python
class MyMeta(type):
    def __new__(cls, name, bases, attrs):
        attrs["tag"] = "AUTO"
        return super().__new__(cls, name, bases, attrs)

class MyClass(metaclass=MyMeta):
    pass

print(MyClass.tag)   # AUTO
```

Use cases:

* Auto-registering classes
* Enforcing rules
* Code generation

(Advanced interviews only.)

---

# 🧠 Summary Table — Magic Methods

| Category   | Methods                          | Purpose                  |
| ---------- | -------------------------------- | ------------------------ |
| String     | `__str__`, `__repr__`            | Object representation    |
| Math       | `__add__`, `__sub__`, `__mul__`  | Arithmetic               |
| Comparison | `__eq__`, `__lt__`, `__gt__`     | Comparing objects        |
| Iteration  | `__iter__`, `__next__`           | Looping                  |
| Callable   | `__call__`                       | Treat object as function |
| Indexing   | `__getitem__`, `__setitem__`     | List-like behavior       |
| Context    | `__enter__`, `__exit__`          | `with` statements        |
| Lifecycle  | `__new__`, `__init__`, `__del__` | Object creation          |

---

# 🎯 Interview Q&A — Advanced OOP & Dunder Methods

### **Q1. Difference between `__str__` and `__repr__`?**

* `__str__` → User readable
* `__repr__` → Developer readable (ideally unambiguous)

---

### **Q2. When is `__call__` used?**

When you want objects to behave like functions.

---

### **Q3. What is operator overloading?**

Redefining how operators (`+`, `==`) behave for user-defined classes via dunder methods.

---

### **Q4. What are class methods used for?**

Alternative constructors, working with class-level data.

---

### **Q5. Why use static methods?**

Utility methods that logically belong to a class but don't need object/class data.

---

### **Q6. What does `__enter__` and `__exit__` do?**

Used in context managers (with statement) for setup and cleanup.

---

### **Q7. What is the role of metaclasses?**

Control how classes are created.

---

### ⭐ Task-Level Interview Questions (Advanced)

* Implement custom `__add__` for complex numbers
* Write a class that works in a `with` block
* Create a class that supports indexing + slicing
* Implement your own iterator using `__iter__` and `__next__`
* Show difference between instance/class/static methods with examples

---

# 🧠 **OOP Interview Q&A + Coding Tasks + Summary**

This section strengthens your interview preparation with:
- Core conceptual questions  
- Scenario-based questions  
- Coding tasks  
- Complete OOP summary  

---

# 🎯 1. High-Level OOP Interview Questions

### **Q1. What is OOP?**
OOP (Object-Oriented Programming) organizes code using **classes** and **objects** to make it modular, maintainable, and reusable.

---

### **Q2. Difference between class and object?**
- **Class** → Blueprint  
- **Object** → Real instance created from the class  

---

### **Q3. What is `self`?**
Reference to the **current object**. Used to access instance variables and methods.

---

### **Q4. What is `__init__`?**
Constructor. Initializes object attributes during creation.

---

### **Q5. Explain class variables vs instance variables.**
| Class Variable | Instance Variable |
|---------------|-------------------|
| Shared by all objects | Unique to each object |
| Declared outside `__init__` | Declared inside `__init__` |

---

### **Q6. What is encapsulation?**
Bundling data + methods and restricting access using `_protected` and `__private`.

---

### **Q7. What is abstraction?**
Hiding internal details while exposing only necessary functionality (using abstract classes).

---

### **Q8. What is inheritance?**
One class acquiring features of another to support code reuse.

---

### **Q9. What is polymorphism?**
Same method name → different behavior depending on the object.

---

### **Q10. What is method overriding?**
A child class **redefines** a method from the parent class.

---

### **Q11. What is method overloading?**
Python does NOT support it directly. Achieved using:
- default arguments  
- `*args`, `**kwargs`  

---

### **Q12. What are dunder (magic) methods?**
Special built-in methods like:
- `__str__`, `__repr__`, `__len__`
- `__add__`, `__eq__`, `__lt__`

Used for operator overloading and custom object behavior.

---

### **Q13. Difference between `__str__` and `__repr__`?**
- `__str__` → Human readable  
- `__repr__` → Developer readable, precise  

---

### **Q14. What is multiple inheritance?**
A class inheriting from **more than one** parent.

---

### **Q15. What is MRO?**
Method Resolution Order. Order in which Python searches for methods.  
Use:  
```python
ClassName.mro()
````

---

### **Q16. What is a class method?**

Method bound to the class (not object). Uses `@classmethod` + `cls`.

---

### **Q17. What is a static method?**

Utility method that does NOT take `self` or `cls`.

---

### **Q18. What are metaclasses?**

“Classes of classes” that define HOW classes are created (advanced concept).

---

### **Q19. What is composition?**

Creating complex classes by combining other classes (HAS-A relationship).

---

### **Q20. What is the difference between inheritance and composition?**

| Inheritance       | Composition        |
| ----------------- | ------------------ |
| IS-A relationship | HAS-A relationship |
| Parent-child      | Combine classes    |

---

# 🧩 2. Scenario-Based Interview Questions

### **Q21. When to use inheritance vs composition?**

* Inheritance: When subclass *is a* type of parent.
* Composition: When you want to *use* another class inside.

---

### **Q22. Why is multiple inheritance risky?**

It can cause:

* Method resolution conflicts
* Diamond problem
* Increased complexity

---

### **Q23. What happens if a class has no `__init__`?**

It inherits parent’s `__init__`.

---

### **Q24. How do you prevent a class from being inherited?**

Make it a `final` class using metaclasses (advanced) or raise errors in `__init_subclass__`.

---

### **Q25. What is the diamond problem?**

Multiple inheritance causing ambiguity.
Solved using **MRO** (C3 linearization).

---

### **Q26. What happens if both parent and child have same variable?**

Child variable **overrides** parent's.

---

### **Q27. How do you call a parent constructor?**

```python
super().__init__()
```

---

# 🖥 3. Coding-Level Interview Questions

### **Q28. Write a class for a Rectangle with area & perimeter.**

```python
class Rectangle:
    def __init__(self, w, h):
        self.w = w
        self.h = h

    def area(self):
        return self.w * self.h

    def perimeter(self):
        return 2 * (self.w + self.h)
```

---

### **Q29. Create a class that overloads the `+` operator.**

```python
class Vector:
    def __init__(self, x, y):
        self.x = x; self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
```

---

### **Q30. Create a custom iterator.**

```python
class Counter:
    def __init__(self, n):
        self.n = n

    def __iter__(self):
        self.i = 0
        return self

    def __next__(self):
        if self.i < self.n:
            self.i += 1
            return self.i
        raise StopIteration
```

---

### **Q31. Write a decorator that prints function time.**

```python
import time

def timer(func):
    def wrapper(*a, **kw):
        s = time.time()
        result = func(*a, **kw)
        print("Time:", time.time() - s)
        return result
    return wrapper
```

---

### **Q32. Write a class that works inside a `with` block.**

```python
class File:
    def __init__(self, name):
        self.name = name

    def __enter__(self):
        self.f = open(self.name)
        return self.f

    def __exit__(self, *args):
        self.f.close()
```

---

### **Q33. Make a class callable.**

```python
class Greet:
    def __call__(self, name):
        print("Hello", name)
```

---

# 🧱 4. Advanced-Level Questions (Meta, Dunder, OOP Design)

### **Q34. Explain the role of `__new__`.**

It creates the object in memory (constructor before `__init__`).

---

### **Q35. Why is `__repr__` important?**

Helpful for debugging; used in REPL, logs, dev tools.

---

### **Q36. What happens when you override `__eq__` but not `__hash__`?**

Instances become **unhashable**, cannot be used in sets/dicts.

---

### **Q37. Explain duck typing with example.**

“If it walks like a duck and quacks like a duck, it’s a duck.”

```python
def make_sound(animal):
    animal.sound()
```

Works for any object with a `.sound()` method.

---

### **Q38. How to enforce abstract methods?**

Using ABC module:

```python
from abc import ABC, abstractmethod
```

---

### **Q39. What is the role of `super()`?**

Used to call parent class methods/constructors.

---

### **Q40. Explain cooperative multiple inheritance.**

Classes cooperate using `super()` calls following **MRO** rules.

---

# 🧠 5. Complete OOP Summary Sheet (One Page)

### ✔ OOP Building Blocks

* **Class**
* **Object**
* **Attributes**
* **Methods**

### ✔ Lifecycle

* `__new__`, `__init__`, `__del__`

### ✔ OOP Principles

* Inheritance
* Polymorphism
* Encapsulation
* Abstraction

### ✔ Magic Methods

* `__str__`, `__repr__`
* `__add__`, `__eq__`, `__lt__`
* `__len__`, `__getitem__`
* `__enter__`, `__exit__`

### ✔ Advanced

* Class methods
* Static methods
* Metaclasses
* MRO

---
