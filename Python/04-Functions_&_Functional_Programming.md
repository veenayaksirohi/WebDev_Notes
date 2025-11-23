---
tags:
  - python
  - functions
  - programming
  - functional-programming
aliases:
  - Python Functions
  - Functional Programming in Python
date: 2025-11-17
---

# 🛠️ 4. Functions & Functional Programming — Detailed (Syntax + Explanation)

## 📜 Table of Contents
- [[#Overview|Overview]]
- [[#Function-Basics|🔹 Function Basics (definition, call, return, docstrings)]]
- [[#Arguments|🔸 Arguments (positional, keyword, default, positional-only, keyword-only)]]
  - `*args` / `**kwargs`
  - Argument unpacking
  - Parameter order rules
- [[#Type-Annot|🧾 Type annotations & docstrings]]
- [[#Lambda-Functions|🪄 Lambda Functions (syntax, use-cases, limitations)]]
- [[#Higher-Order-Functions|🔝 Higher-Order Functions (map/filter/reduce + custom impls)]]
- [[#Closures-Decorators|🧠 Closures & Decorators (wraps, decorator args, ordering)]]
- [[#Best-Practices|✅ Best Practices]]
- [[#Common-Pitfalls|⚠️ Common Pitfalls & How to Fix]]
- [[#Interview-QA|🎯 Interview Q&A (expanded answers)]]
- [[#Navigation|🔗 Navigation]]

---

## 📝 Overview
Functions are named blocks of reusable code. Python functions are **first-class** objects: they can be passed and returned like other values. This enables powerful patterns (callbacks, decorators, closures) and functional-style constructs.

---

# 🔹 Function Basics

### ✅ Defining a simple function
```python
def greet(name):
    """Say hello to name (simple example)."""
    print("Hello,", name)
````

* `def` keyword starts a function definition.
* `name` is a parameter (a local variable inside the function).
* The function body is indented.
* A function that does not explicitly `return` returns `None`.

### ✅ Calling a function

```python
greet("Alex")   # prints: Hello, Alex
```

### ✅ Returning values

```python
def add(a, b):
    return a + b

result = add(2, 3)   # result == 5
```

### ✅ Docstrings (recommended)

```python
def add(a: int, b: int) -> int:
    """
    Add two integers and return the sum.

    Args:
        a: first integer
        b: second integer

    Returns:
        Sum of a and b
    """
    return a + b
```

* Triple-quoted string at top of function is the *docstring* — visible in `help()` and auto docs.

---

# 🔸 Arguments

### 1. Positional arguments

Order matters:

```python
def divide(a, b):
    return a / b

divide(10, 2)  # 5.0
```

### 2. Keyword arguments

Pass by name; order not required:

```python
divide(b=2, a=10)  # 5.0
```

### 3. Default arguments

Provide defaults so arguments become optional:

```python
def greet(name, msg="Hello"):
    print(msg, name)

greet("Alex")          # Hello Alex
greet("Alex", "Hi!")   # Hi! Alex
```

**Important:** avoid mutable default values — see Common Pitfalls.

### 4. Positional-only and keyword-only (Python 3.8+)

You can enforce argument usage style.

* Positional-only: use `/` in signature
* Keyword-only: use `*` in signature

```python
def fn(pos_only, /, normal, *, kw_only):
    print(pos_only, normal, kw_only)

fn(1, 2, kw_only=3)   # OK
# fn(pos_only=1, normal=2, kw_only=3)  # TypeError
```

### 5. `*args` and `**kwargs`

Use when you want flexible argument counts.

* `*args` collects extra positional args into a tuple.
* `**kwargs` collects extra keyword args into a dict.

```python
def f(a, b, *args, **kwargs):
    print("a:", a)
    print("b:", b)
    print("args:", args)
    print("kwargs:", kwargs)

f(1, 2, 3, 4, x=5, y=6)
# a:1 b:2 args:(3,4) kwargs:{'x':5,'y':6}
```

### 6. Argument unpacking

Use `*` / `**` when calling functions to unpack iterables/dicts.

```python
nums = [1, 2]
print(add(*nums))           # add(1,2)

params = {"a": 1, "b": 2}
print(add(**params))        # add(a=1, b=2)
```

### 7. Parameter order rules (recommended order)

1. Positional-only parameters (if any)
2. Regular positional/keyword parameters
3. `*args`
4. Keyword-only parameters (after `*`)
5. `**kwargs`

Example:

```python
def fn(a, b=2, *args, c=3, **kwargs):
    ...
```

---

# 🧾 Type annotations & docstrings

Type hints help readability and tooling (linters, editors). They do not enforce types at runtime (unless you use runtime checkers).

```python
from typing import List, Dict, Any, Callable, Optional

def process(items: List[int]) -> int:
    """Return the sum of integers in items."""
    return sum(items)

def handler(fn: Callable[[int], int], x: int) -> int:
    return fn(x)
```

Use `Optional[T]` for `T | None` (or `T | None` in Python 3.10+).

---

# 🪄 Lambda Functions (Anonymous Functions)

Short single-expression functions.

Syntax:

```python
lambda args: expression
```

Examples:

```python
double = lambda x: x * 2
print(double(5))   # 10

# Often used inline:
squared = list(map(lambda x: x*x, [1, 2, 3]))
```

**Limitations**

* Single expression only — no statements, no multiple lines.
* Harder to debug — prefer named functions for complex logic.

---

# 🔝 Higher-Order Functions

Functions that accept or return other functions.

## `map`, `filter`, `reduce` — usage and custom implementations

### `map(func, iterable)`

Applies `func` to each item.

```python
nums = [1, 2, 3]
doubled = list(map(lambda x: x*2, nums))  # [2, 4, 6]
```

**Custom `map`**

```python
def my_map(func, iterable):
    for item in iterable:
        yield func(item)

list(my_map(lambda x: x*2, [1,2,3]))
```

### `filter(func, iterable)`

Keeps items where `func(item)` is truthy.

```python
evens = list(filter(lambda x: x%2==0, range(10)))
```

**Custom `filter`**

```python
def my_filter(func, iterable):
    for x in iterable:
        if func(x):
            yield x
```

### `reduce(func, iterable)` — from `functools`

Cumulatively apply operation.

```python
from functools import reduce
prod = reduce(lambda a, b: a*b, [1, 2, 3, 4])  # 24
```

**Custom `reduce`**

```python
def my_reduce(func, iterable, initial=None):
    it = iter(iterable)
    if initial is None:
        total = next(it)
    else:
        total = initial
    for x in it:
        total = func(total, x)
    return total
```

### When to use

* `map`/`filter` are concise; list comprehensions are often more Pythonic and readable:

  ```python
  doubled = [x*2 for x in nums]
  evens = [x for x in nums if x%2==0]
  ```

---

# 🧠 Closures & Decorators

## Closures

A closure is a function remembering the environment where it was created.

```python
def make_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

times3 = make_multiplier(3)
print(times3(5))  # 15
```

* `multiplier` remembers `n` even after `make_multiplier` returns.

## Decorators

Decorators wrap a function to extend behavior.

### Basic decorator

```python
def simple_decorator(fn):
    def wrapper(*args, **kwargs):
        print("Before")
        result = fn(*args, **kwargs)
        print("After")
        return result
    return wrapper

@simple_decorator
def say_hi():
    print("Hi")

say_hi()
# Before
# Hi
# After
```

### Preserving metadata with `functools.wraps`

Without `wraps`, the wrapped function loses its `__name__`, `__doc__`.

```python
from functools import wraps

def logged(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        print(f"Calling {fn.__name__}")
        return fn(*args, **kwargs)
    return wrapper
```

### Decorators with arguments

If a decorator needs parameters, add another nesting level:

```python
def repeat(n):
    def decorator(fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                fn(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet():
    print("Hello")
```

### Decorating functions that return values

Ensure wrapper returns the value when needed.

```python
def timeit(fn):
    import time
    @wraps(fn)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = fn(*args, **kwargs)
        end = time.perf_counter()
        print(f"{fn.__name__} took {end-start:.6f}s")
        return result
    return wrapper
```

### Multiple decorators

Decorators apply top-to-bottom visually but execution is bottom-to-top:

```python
@d1
@d2
def f(): pass
# Equivalent to f = d1(d2(f))
```

---

# ✅ Best Practices

* Keep functions **short** and do one thing.
* Use **docstrings** and type hints for clarity.
* Prefer **list/dict comprehensions** to `map`/`filter` unless readability suffers.
* Use `functools.wraps` when writing decorators.
* Avoid excessive side effects in functions (favor returning values).
* Validate inputs and raise meaningful exceptions.
* Use `*` / `/` to make APIs explicit (positional-only / keyword-only) when helpful.

---

# ⚠️ Common Pitfalls & How to Fix

### 1. Mutable default argument

Bad:

```python
def append_item(x, items=[]):
    items.append(x)
    return items
```

This shares the same list across calls.

Fix:

```python
def append_item(x, items=None):
    if items is None:
        items = []
    items.append(x)
    return items
```

### 2. Forgetting to return

Function that computes but forgets to `return` => returns `None`.

### 3. Overusing `*args`/`**kwargs`

They’re powerful but hide the real API. Use explicit parameters first.

### 4. Complex lambdas

Move complex logic into named functions for readability and debugging.

### 5. Not using `wraps` in decorators

Loses helpful metadata and breaks introspection.

---

# 🎯 Interview Q&A (Expanded)

**Q1. What is a lambda function?**
A lambda is an anonymous single-expression function: `lambda x: x+1`. Use it for short, throwaway functions (callbacks, key functions). For complex logic, use a named `def`.

**Q2. Differences between `*args` and `**kwargs`?**

* `*args` collects extra positional arguments as a tuple.
* `**kwargs` collects extra named arguments as a dict.

**Q3. What is a higher-order function?**
A function that accepts other functions as arguments and/or returns a function. Examples: `map`, `filter`, decorators.

**Q4. Explain a decorator with example.**
A decorator is a callable that takes a function and returns a function (often a wrapper that adds behavior). Example: `@timeit` that times function execution.

**Q5. What is a closure?**
A nested function that captures variables from its enclosing scope; useful for creating function factories and maintaining state without using globals.

**Q6. Why use `reduce()`?**
For cumulative operations (sum, product, fold). Often replaced by loops or built-in `sum()`/`math.prod()` for readability.

**Q7. Can functions be stored in data structures?**
Yes — because functions are first-class. Example: `ops = [lambda x: x+1, lambda x: x*2]`.

**Q8. How do you write a decorator that works with functions with any signature?**
Use `*args, **kwargs` in the wrapper and `@wraps` to preserve metadata.

**Q9. How to avoid mutable default argument bug?**
Use `None` as default and create the mutable inside the function.

**Q10. What’s the order of parameters in function signature?**
(positional-only) / positional_or_keyword, *args, keyword_only, **kwargs — follow this to avoid syntax errors.

---

# 🔗 Navigation

### Next Chapter

➡️ [[05_Modules_and_Packages|📦 5. Modules & Packages]]

### Previous Chapter

⬅️ [[03_Data_Structures|🗂️ 3. Data Structures]]
