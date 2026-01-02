---
tags:
  - python
  - data-structures
  - programming
  - basics
aliases:
  - Python Data Structures
  - Python Collections
  - Python Containers
date: 2025-11-17
---
# 🗂️ 3. Data Structures — Python

## 📜 Table of Contents
- [[#Overview|Overview]]
- [[#Python-Data-Types|🔢 Python Data Types]]
  - [[#Numeric-Types|Numeric Types]]
  - [[#Boolean-Type|Boolean Type]]
  - [[#None-Type|None Type]]
- [[#Core-Containers|📦 Core Containers]]
  - [[#Lists|Lists]]
  - [[#Tuples|Tuples]]
  - [[#Sets|Sets]]
  - [[#Dictionaries|Dictionaries]]
- [[#String-Manipulation|🔤 String Manipulation]]
- [[#Comprehensions|✏️ Comprehensions]]
- [[#Type-Conversion|🔄 Type Conversion]]
- [[#Best-Practices|✅ Best Practices]]
- [[#Common-Pitfalls|⚠️ Common Pitfalls]]
- [[#Interview-QA|🎯 Interview Q&A]]
- [[#Navigation|🔗 Navigation]]

---

## 📝 Overview
Data structures help you **store, organize, and manage** data efficiently.

Python provides **built-in, powerful, and easy-to-use** data structures:

- **Data Types**: int, float, complex, bool, None
- **Sequences**: Lists, Tuples, Strings, Range
- **Sets**: Set, Frozenset
- **Mappings**: Dictionaries
- **Comprehensions** for fast structure creation

Understanding these makes your code faster, cleaner, and more efficient.  
These are also among the *most frequently asked* topics in interviews.

---

# 🔢 Python Data Types

Python has several built-in data types that form the foundation of all data structures.

---

## 🔢 Numeric Types

### **1. Integer (int)**

Whole numbers without decimal points. No size limit in Python 3.

```python
age = 25
big_num = 123456789012345678901234567890
negative = -42
```

**Operations:**
```python
x = 10
y = 3

print(x + y)   # Addition: 13
print(x - y)   # Subtraction: 7
print(x * y)   # Multiplication: 30
print(x / y)   # Division: 3.333...
print(x // y)  # Floor division: 3
print(x % y)   # Modulus: 1
print(x ** y)  # Exponentiation: 1000
```

---

### **2. Float (float)**

Numbers with decimal points.

```python
pi = 3.14159
temperature = -40.5
scientific = 1.5e-4  # 0.00015
```

**Precision Note:**
```python
# Floating point precision issues
print(0.1 + 0.2)  # 0.30000000000000004
# Use decimal module for precise calculations
from decimal import Decimal
print(Decimal('0.1') + Decimal('0.2'))  # 0.3
```

---

### **3. Complex (complex)**

Numbers with real and imaginary parts.

```python
z = 3 + 4j
print(z.real)  # 3.0
print(z.imag)  # 4.0
print(abs(z))  # 5.0 (magnitude)
```

---

## ✅ Boolean Type

Represents `True` or `False`. Used in conditional statements.

```python
is_active = True
is_admin = False

# Boolean operations
print(True and False)  # False
print(True or False)   # True
print(not True)        # False
```

**Truthy and Falsy Values:**
```python
# Falsy values (evaluate to False)
bool(0)          # False
bool(0.0)        # False
bool("")         # False (empty string)
bool([])         # False (empty list)
bool({})         # False (empty dict)
bool(None)       # False

# Truthy values (evaluate to True)
bool(1)          # True
bool("hello")    # True
bool([1, 2])     # True
bool({"a": 1})   # True
```

---

## ⭕ None Type

Represents the absence of a value. Similar to `null` in other languages.

```python
result = None

def no_return():
    pass  # implicitly returns None

x = no_return()
print(x)  # None

# Checking for None
if result is None:
    print("No value")
```

**Important:** Use `is` or `is not` to check for None, not `==`.

```python
# Correct
if x is None:
    pass

# Avoid
if x == None:  # Works but not Pythonic
    pass
```

---

# 📦 Core Containers

---

## 🟩 Lists
### **Features**
- Ordered  
- Mutable (you can change them)  
- Allow duplicates  
- Can store mixed data types  

### **Syntax**
```python
numbers = [10, 20, 30]
````

### **Common Methods**

```python
numbers.append(40)
numbers.insert(1, 15)
numbers.remove(20)
numbers.pop()     # removes last item
numbers.sort()    # in-place sort
```

### **Example**

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "blueberry"
print(fruits)
```

---

## 🟧 Tuples

### **Features**

* Ordered
* Immutable
* Faster than lists
* Good for fixed data

### **Syntax**

```python
point = (4, 5)
```

### **Use Cases**

* Returning multiple values from a function
* Storing configuration or fixed data

### **Example**

```python
coordinates = (12.5, 45.3)
x, y = coordinates
```

---

## 🟥 Sets

### **Features**

* Unordered
* No duplicates
* Fast lookup
* Mutable (but elements must be immutable)

### **Syntax**

```python
unique_nums = {1, 2, 3}
```

### **Common Operations**

```python
unique_nums.add(4)
unique_nums.remove(2)
print(3 in unique_nums)
```

### **Set Operations**

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a.union(b))
print(a.intersection(b))
print(a.difference(b))
```

---

## 🟦 Dictionaries

### **Features**

* Key-value pairs
* Mutable
* Fast lookups
* Keys must be unique & immutable

### **Syntax**

```python
person = {"name": "Alice", "age": 25}
```

### **Common Operations**

```python
person["city"] = "Delhi"
print(person.get("age"))
print(person.keys())
print(person.values())
```

### **Removing Items**

```python
# Method 1: del keyword
person = {"name": "Alice", "age": 25, "city": "Delhi"}
del person["age"]  # Removes 'age' key

# Method 2: pop() - removes and returns value
age = person.pop("age")  # Returns 25 and removes key
city = person.pop("city", "Unknown")  # With default if key not found

# Method 3: popitem() - removes and returns last inserted item
last_item = person.popitem()  # Returns ('city', 'Delhi')

# Method 4: clear() - removes all items
person.clear()  # Empty dict: {}
```

### **Checking Before Removing**

```python
person = {"name": "Alice", "age": 25}

# Safe removal - check if key exists
if "age" in person:
    del person["age"]

# Or use pop with default
age = person.pop("age", None)  # Returns None if key doesn't exist
```

### **Looping**

```python
for key, value in person.items():
    print(key, value)
```

---

# 🔤 String Manipulation

Strings are a sequence of characters.

### **Common Methods**

```python
s = "  Hello Python  "

s.strip()
s.upper()
s.lower()
s.replace("Python", "World")
s.split(" ")
```

### **Example**

```python
text = "  Hello, Python!  "
print(text.strip().upper())
```

---

# ✏️ Comprehensions

### ✔️ List Comprehension

```python
squares = [x*x for x in range(6)]
```

### ✔️ Dictionary Comprehension

```python
nums = [1, 2, 3]
sq = {n: n*n for n in nums}
```

### ✔️ Set Comprehension

```python
unique = {c for c in "banana"}
```

### ✔️ Filtering in Comprehensions

```python
even = [x for x in range(10) if x % 2 == 0]
```

---

# 🔄 Type Conversion

Converting between different data types.

### **To Integer**
```python
int("123")      # 123
int(45.67)      # 45 (truncates)
int(True)       # 1
int(False)      # 0
```

### **To Float**
```python
float("3.14")   # 3.14
float(42)       # 42.0
float(True)     # 1.0
```

### **To String**
```python
str(123)        # "123"
str(3.14)       # "3.14"
str(True)       # "True"
str([1, 2])     # "[1, 2]"
```

### **To Boolean**
```python
bool(1)         # True
bool(0)         # False
bool("text")    # True
bool("")        # False
```

### **To List/Tuple/Set**
```python
list("abc")           # ['a', 'b', 'c']
tuple([1, 2, 3])      # (1, 2, 3)
set([1, 2, 2, 3])     # {1, 2, 3}
```

---

# ✅ Best Practices

* Use **lists** when order matters
* Use **tuples** for fixed data
* Use **sets** for unique items & fast membership testing
* Use **dictionaries** for key-value relationships
* Prefer **comprehensions** for clean, readable transformations
* Avoid changing dictionary size while iterating

---

# ⚠️ Common Pitfalls

* ❌ Trying to modify a tuple → causes error
* ❌ Using mutable types (like lists) as dictionary keys
* ❌ Assuming set order
* ❌ Forgetting that list `.remove()` removes *first occurrence only*
* ❌ Attempting to index a set (sets don’t support indexing)

---

# 🎯 Interview Q&A

### **Q1. What are Python's built-in data types?**

**Numeric:** int, float, complex  
**Boolean:** bool  
**Sequence:** str, list, tuple, range  
**Mapping:** dict  
**Set:** set, frozenset  
**None:** NoneType

---

### **Q2. List vs Tuple?**

* List → Mutable, slower, more memory
* Tuple → Immutable, faster, less memory, hashable

---

### **Q3. When do you use a set?**

* To remove duplicates
* To check membership quickly: `item in set`
* For set operations (union, intersection, difference)

---

### **Q4. Can dictionary keys be mutable?**

No. Keys must be immutable (like strings, numbers, tuples).

---

### **Q5. How to remove items from a dictionary?**

```python
person = {"name": "Alice", "age": 25, "city": "Delhi"}

# Method 1: del
del person["age"]

# Method 2: pop() - returns value
age = person.pop("age", None)

# Method 3: popitem() - removes last item
last = person.popitem()

# Method 4: clear() - removes all
person.clear()
```

---

### **Q6. How do you loop through a dictionary?**

```python
for k, v in person.items():
    print(k, v)
```

---

### **Q6. Difference: `.append()` vs `.extend()`?**

* `append(x)` → adds element as a single item
* `extend([x, y])` → adds each element individually

---

### **Q7. Remove duplicates from a list?**

```python
unique_list = list(set(my_list))
```

---

### **Q9. What are comprehension advantages?**

* Short and clean syntax
* Faster than traditional loops
* More Pythonic and readable

---

### **Q10. Difference between `is` and `==`?**

* `is` → checks if two variables point to same object (identity)
* `==` → checks if values are equal (equality)

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (same values)
print(a is b)  # False (different objects)
print(a is c)  # True (same object)
```

---

### **Q11. What is the difference between `None`, `0`, and `False`?**

* `None` → absence of value (NoneType)
* `0` → integer zero (int)
* `False` → boolean false (bool)

All are falsy but different types:
```python
print(type(None))   # <class 'NoneType'>
print(type(0))      # <class 'int'>
print(type(False))  # <class 'bool'>
```

---

### **Q12. How to check data type?**

```python
x = 42
print(type(x))           # <class 'int'>
print(isinstance(x, int)) # True
```

---

### **Q12. What is mutable vs immutable?**

**Immutable** (cannot be changed):
- int, float, complex, bool, str, tuple, frozenset

**Mutable** (can be changed):
- list, dict, set

```python
# Immutable
s = "hello"
s[0] = "H"  # Error!

# Mutable
lst = [1, 2, 3]
lst[0] = 10  # Works!
```

---

### ⭐ Bonus Mini Interview Tasks

1. Reverse a string
2. Count frequency of characters
3. Merge two dictionaries
4. Find common elements between two lists
5. Convert two lists into a dictionary

---

## 🔗 Links & Navigation

- **Home**: [[Table Of Content]]
- **Previous**: [[02-Control_Flow]]
- **Next**: [[04-Functions_&_Functional_Programming]]
