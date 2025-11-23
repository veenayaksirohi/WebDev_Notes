---
tags:
  - python
  - advanced
  - decorators
  - abc
  - typing
  - concurrency
  - asyncio
aliases:
  - Advanced Python
  - Python Expert Concepts
  - Python Meta-programming
date: 2025-11-19
---

# 🚀 9. Advanced Python Concepts — Full Detailed Guide

## 📜 Table of Contents
- Advanced Function Patterns
- Decorators (deep dives)
- Descriptors
- Properties
- Abstract Base Classes (ABC)
- Type Annotations (`typing`)
- Memory Management & Garbage Collection
- Meta-programming & Metaclasses
- Async Programming (`asyncio`, `await`)
- Concurrency (Threading & Multiprocessing)
- Interview Q&A

***

## 🟣 Advanced Function Patterns

**Functions in Python are “first-class citizens” — you can treat them like any other variable. Pass them around, store them, return them, and use them anywhere.**  
This is the foundation for functional programming, decorators, event handlers, and callback systems.

**Passing, Returning, and Storing Functions**
```python
def greet(name):
    return f"Hello {name}"

def apply_twice(func, value):
    return func(func(value))

def make_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

say = greet  # You can assign functions to variables
print(say("Alex"))  # Output: Hello Alex
print(apply_twice(lambda x: x*2, 5))  # Output: 20
triple = make_multiplier(3)
print(triple(10))   # Output: 30
```
**Explanation:**  
- `apply_twice` takes a function as argument and calls it twice.
- `make_multiplier` generates custom multiplier functions (“function factory”).
- Storing or passing functions enables flexible patterns like callbacks and higher-order functions.

***

## 🟦 Decorators

**Decorators wrap a function (or class) to modify its behavior without changing the original code.**  
You can log, validate, cache, retry, enforce rules, or transparently add features — all by one line of code using `@your_decorator`.

### Basic Decorator (No Arguments)
```python
def log(func):
    def wrapper(*args, **kwargs):
        print(f"{func.__name__} called")
        return func(*args, **kwargs)
    return wrapper

@log
def add(x, y): return x+y
add(2, 3)
```
**Explanation:**  
- `@log` replaces `add(x, y)` with a version that prints logs before calling the original code.
- Decorators are powerful for tracing and debugging.

### Decorator with Arguments
```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def hello(): print("Hello!")
hello()
```
**Explanation:**  
- `repeat(3)` runs `hello()` three times.  
- You can pass parameters to decorators, making them reusable and configurable.

### Class-Based Decorator
```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0
    def __call__(self, *args, **kwargs):
        self.count += 1
        print("Call:", self.count)
        return self.func(*args, **kwargs)

@CountCalls
def foo(): print("Hi!")
foo()
foo()
```
**Explanation:**  
- Class decorators keep state (like counting calls).  
- The class must implement `__call__` to act like a function.

### Chaining Decorators
```python
def uppercase(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs).upper()
    return wrapper

def exclaim(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) + "!!!"
    return wrapper

@exclaim
@uppercase
def greet(name): return f"hello, {name}"
print(greet("alex"))  # HELLO, ALEX!!!
```
**Explanation:**  
- Decorators can be stacked; order matters!
- Here, `greet` is first uppercased, then has exclamation marks added.

***

## 🟩 Descriptors

**Descriptors are advanced objects used to customize attribute access in classes.**  
They enable validation, computed properties, logging access, and many advanced patterns (used by built-in `property` and Django ORM).

```python
class Positive:
    def __set_name__(self, owner, name):
        self.name = name
    def __get__(self, instance, owner):
        return instance.__dict__[self.name]
    def __set__(self, instance, value):
        if value < 0:
            raise ValueError("Must be positive")
        instance.__dict__[self.name] = value

class Person:
    age = Positive()
p = Person()
p.age = 25
# p.age = -5  # ValueError
```
**Explanation:**  
- `__set_name__` saves the field name.
- Setting to negative raises an error — direct, automatic validation.
- Common frameworks (like Django) use descriptors for model fields.

***

## 🟨 Properties (@property)

**Properties let a method act like an attribute.**  
With `@property`, you can run code, validate, or perform calculation on access or update.

```python
class Circle:
    def __init__(self, r):
        self._r = r  # Convention: _ means "internal use"
    @property
    def radius(self): return self._r
    @radius.setter
    def radius(self, v):
        if v <= 0: raise ValueError("positive only")
        self._r = v
    @property
    def area(self):
        import math
        return math.pi * self._r**2

c = Circle(5)
print(c.area)   # Computed property
c.radius = 10
print(c.area)
```
**Explanation:**  
- `@property` for controlled, elegant access.  
- Validation and computation are hidden from end user.

**With Deleter:**
```python
class Account:
    def __init__(self, bal):
        self._bal = bal
    @property
    def balance(self): return self._bal
    @balance.deleter
    def balance(self):
        print("Account closed"); del self._bal
acc = Account(1000)
del acc.balance
```
**Explanation:**  
- You can use `del acc.balance` to run code when an attribute is removed, e.g., close an account.

***

## 🟥 Abstract Base Classes (ABC)

**ABC enforce rules/protocols and prevent incomplete implementations.**  
They make code consistent; especially for large projects (e.g., shapes must all have `area()`).

```python
from abc import ABC, abstractmethod
class Animal(ABC):
    @abstractmethod
    def sound(self): pass
    @abstractmethod
    def move(self): pass
    def info(self): return "Animal info"

class Dog(Animal):
    def sound(self): return "Bark"
    def move(self): return "Run"
dog = Dog()
print(dog.sound(), dog.info())
```
**Explanation:**  
- You cannot create an `Animal()` directly (abstract).
- All child classes **must** define `sound` and `move`.

***

## 🟧 Type Annotations (`typing`)

**Type hints are annotations, purely for documentation, static checks, and better IDE/tooling.**  
They make code easier to read and help catch bugs early.

```python
def add(x: int, y: int) -> int:
    return x + y

from typing import List, Dict, Tuple, Union, Optional, Callable

numbers: List[int] = [1,2,3]
scores: Dict[str,int] = {"Alice":90, "Bob":85}
coord: Tuple[int,int] = (10,20)
value: Union[int,str] = 42
name: Optional[str] = None

def apply(func: Callable[[int], int], x: int) -> int: return func(x)
```
**Explanation:**  
- Use `mypy` or IDE plugins to check for type consistency.
- No runtime enforcement; just warnings/errors for wrong types in development.

***

## 🧠 Memory Management & Garbage Collection

**Python auto-manages memory through reference counting and the garbage collector.**  
Programmers rarely need to free memory manually.

```python
import sys
a = []
print(sys.getrefcount(a))  # 2
b = a
print(sys.getrefcount(a))  # 3 (a, b, internal call)
del b
print(sys.getrefcount(a))  # 2
```
**Explanation:**  
- Every variable increases the reference count.
- When count reaches zero, memory is freed.

```python
import gc
class Node:
    def __init__(self, v): self.v = v; self.next = None
a = Node(1)
b = Node(2)
a.next = b; b.next = a  # Circular ref
del a, b
gc.collect()
```
**Explanation:**  
- For circular references, garbage collector periodically finds cycles and frees them.

***

## 🌀 Meta-programming & Metaclasses

**Meta-programming means writing code to manipulate code itself; metaclasses create classes.**  
Used for auto-registration, validation, advanced ORM features.

```python
class Meta(type):
    def __new__(cls, name, bases, attrs):
        attrs["flag"] = True
        return super().__new__(cls, name, bases, attrs)
class Test(metaclass=Meta): pass
print(Test.flag)
```
**Explanation:**  
- `Test.flag` is automatically added at class creation by the metaclass.
- Frameworks use metaclasses for plugin systems and validation.

**Auto-Registry:**
```python
class Registry(type):
    items = {}
    def __new__(cls, name, bases, attrs):
        obj = super().__new__(cls, name, bases, attrs)
        cls.items[name] = obj
        return obj
class Base(metaclass=Registry):pass
class A(Base):pass
class B(Base):pass
print(Registry.items)
```
**Explanation:**  
- Any subclass of `Base` is automatically registered for later lookup.

***

## ⚡ Async Programming (`asyncio`, `await`)

**Async functions enable concurrent (not parallel) programming — awesome for IO-bound tasks.**  
You can run many things “at once” (one thread, coroutines pause and resume).

```python
import asyncio
async def hello():
    print("Hello"); await asyncio.sleep(1); print("World")
asyncio.run(hello())
```
**Explanation:**  
- `async def` creates a coroutine.
- `await` pauses it and lets others run until resume.

```python
async def t(i): await asyncio.sleep(1); print(i)
async def main():
    await asyncio.gather(t(1), t(2))
asyncio.run(main())
```
**Explanation:**  
- `asyncio.gather` runs several coroutines at once.
- Only IO tasks benefit — CPU tasks stay single-threaded.

***

## 🧵 Concurrency: Threading & Multiprocessing

**Threading:** Multiple threads (sharing memory, GIL).  
**Multiprocessing:** Multiple processes (parallel, separate memory, no GIL).

Threading (I/O-bound):
```python
import threading
def worker(n): print("Thread", n)
threads = [threading.Thread(target=worker, args=(i,)) for i in range(3)]
for t in threads: t.start()
for t in threads: t.join()
```
**Explanation:**  
- Good for network, disk, waiting, servers.

Multiprocessing (CPU-bound):
```python
from multiprocessing import Process
def heavy(): print("Heavy work")
plist = [Process(target=heavy) for _ in range(3)]
for p in plist: p.start()
for p in plist: p.join()
```
**Explanation:**  
- Use when you need true parallelism (e.g., data crunching, ML models).

***

## 🎯 Interview Q&A

- **Q:** What is a decorator?  
  **A:** Wraps functions; can add logging, validate inputs, cache results, control access, retry.
- **Q:** How are decorators different from higher-order functions?  
  **A:** Decorators only wrap; HOFs can wrap, be passed as, or return functions.
- **Q:** What is a descriptor?  
  **A:** Object with custom attribute access logic via `__get__`, `__set__`, or `__delete__`.
- **Q:** What's `@property`?  
  **A:** Turns a method into a getter/setter, so you can validate or compute on access via dot notation.
- **Q:** Why use ABC?  
  **A:** Enforces contract across subclasses, great for large codebases or APIs.
- **Q:** Are type annotations enforced?  
  **A:** No, they’re only hints for IDEs/tools (optional, but help readability).
- **Q:** What is the GIL?  
  **A:** Global Interpreter Lock — means only one thread runs Python code at once (affects threading, not processes).
- **Q:** When use threading vs multiprocessing?  
  **A:** Threading = I/O or waiting tasks. Multiprocessing = CPU heavy (fully parallel).
- **Q:** What is a metaclass?  
  **A:** Defines how classes get created, allowing advanced custom rules.
- **Q:** What does async/await do?  
  **A:** Enables coroutines to yield control for concurrent IO (great for servers, APIs).
- **Q:** Coroutines vs generators?  
  **A:** Coroutines = `async/await` for async IO; generators = `yield` for memory-efficient iteration.
- **Q:** How does GC work in Python?  
  **A:** Reference counting and cyclic checking — no need for manual "free"/`delete`.

***