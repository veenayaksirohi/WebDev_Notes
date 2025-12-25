---
tags:
  - python
  - iterators
  - generators
  - context-managers
aliases:
  - Python Iterators
  - Python Generators
  - Python Context Managers
date: 2025-11-19
---

# 🔁 8. Iterators, Generators & Context Managers — Python

## 📜 Table of Contents
- Iterable Protocol & Iterators
- Generators (`yield`)
- Context Managers (`with`, `__enter__`, `__exit__`)
- Best Practices
- Interview Q&A

***

## 🧷 Iterable Protocol & Iterators

### **What Is an Iterator?**
- An iterator is an object that lets you traverse elements one at a time, using the iterator protocol.
- **Protocol:** Implements `__iter__()` (returns self) and `__next__()` (returns next value or `StopIteration`).

### **Why Use Iterators?**
- Lazy evaluation: compute items only when needed, saves memory.
- Stateful traversal: iterator keeps its position in the sequence.
- Uniform interface: for-loops and other tools work the same with built-in or custom iterators.

### **Custom Iterator Example**
```python
class EvenNumbers:
    def __init__(self, limit):
        self.current = 2
        self.limit = limit
    def __iter__(self):
        return self
    def __next__(self):
        if self.current > self.limit:
            raise StopIteration
        val = self.current
        self.current += 2
        return val

evens = EvenNumbers(10)
for num in evens:
    print(num)  # 2, 4, 6, 8, 10
```

**Notes:**
- Once an iterator is exhausted, you need a new iterator object to “reset” it.
- In many built-in cases (e.g. lists), calling `iter(list)` returns a fresh iterator.

***

## 🔄 Generators

### **What Is a Generator?**
- A generator is a special iterator built using a function with the `yield` keyword.
- Calling a generator function returns a generator object, but does **not** start execution immediately.
- Each call to `next()` resumes execution from the last `yield`.

### **Why Use Generators?**
- Memory-efficient: values are computed on the fly, not stored.
- Lazy evaluation: only computes when needed.
- Can represent infinite sequences.
- Useful for pipelines and large data processing.

### **Generator Example**
```python
def count_up_to(n):
    i = 1
    while i <= n:
        yield i
        i += 1

counter = count_up_to(5)
for num in counter:
    print(num)  # 1, 2, 3, 4, 5
```

**Advanced Generator: Infinite Sequence**
```python
import random
def random_color(colors):
    while True:
        yield random.choice(colors)

color_gen = random_color(["red", "green", "blue"])
print(next(color_gen))
print(next(color_gen))
# Keeps generating forever unless stopped
```

**Behind the Scenes:**
- Function with `yield` becomes a generator; it saves state each time it yields.
- Generator objects implement `__iter__` and `__next__`.
- `yield` pauses function and returns a value; next call resumes from there.

***

## 🧼 Context Managers

### **Why Use Context Managers?**
- To manage resources (files, DB connections) cleanly.
- Guarantees clean-up, even if errors occur.
- Replaces try...finally blocks for resource management.

### **The Protocol**
- Must implement `__enter__()` (sets up, returns object) and `__exit__()` (tears down, cleans up, handles exceptions).

**Simple Context Manager Example**
```python
class MyContext:
    def __enter__(self):
        print("Entering context")
        return self
    def __exit__(self, exc_type, exc_value, tb):
        print("Exiting context")
        return False  # propagate exceptions

with MyContext():
    print("Inside with-block")
# Output:
# Entering context
# Inside with-block
# Exiting context
```

**File Handling Example**
```python
with open("data.txt", "w") as f:
    f.write("Hello, context manager!")
# File automatically closed, even if error occurred
```

**Generator-based Context Manager**
```python
from contextlib import contextmanager

@contextmanager
def managed_resource():
    print("Setup resource")
    try:
        yield "resource"
    finally:
        print("Clean up resource")

with managed_resource() as res:
    print("Using", res)
# Output:
# Setup resource
# Using resource
# Clean up resource
```

***

## ✅ Best Practices

- Use generators to process large/infinite sequences without loading into memory.
- Implement custom iterators when you need complex iteration or state.
- Use context managers for any resource that needs clean-up (files, locks, DB connections).
- Prefer `contextlib.contextmanager` for simple context managers — less boilerplate.

***

## 🎯 Interview Q&A

**Q1. What is the difference between an iterable and an iterator?**
- Iterable: object you can loop over (like a list).
- Iterator: object that manages iteration (`__iter__()` and `__next__()` methods).

**Q2. Why do we raise `StopIteration` in a custom iterator?**
- To signal that iteration is complete. Required by iterator protocol.

**Q3. What does `yield` do in Python?**
- Pauses the function, returns a value, and saves state. Next iteration resumes from last yield.

**Q4. Can a generator function be used as an iterator?**
- Yes. The generator object implements the iterator protocol.

**Q5. What is a context manager in Python?**
- Object that defines `__enter__` and `__exit__`, manages resource setup/cleanup, and is used with `with`.

**Q6. What do the parameters of `__exit__` mean?**
- `exc_type`, `exc_value`, `traceback` give info about any exception in the with-block; can be used to suppress or propagate error.

**Q7. How to create a context manager using a generator?**
- Use `@contextmanager` decorator on a generator function: code before yield is setup; after yield is cleanup.



---

## 🔗 Links & Navigation

- **Home**: [[Table Of Content]]
- **Previous**: [[07-Object-Oriented_Programming_(OOP)]]
- **Next**: [[09-Advanced_Python_Concepts]]
