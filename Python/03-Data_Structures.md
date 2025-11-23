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
- [[#Core-Containers|📦 Core Containers]]
  - [[#Lists|Lists]]
  - [[#Tuples|Tuples]]
  - [[#Sets|Sets]]
  - [[#Dictionaries|Dictionaries]]
- [[#String-Manipulation|🔤 String Manipulation]]
- [[#Comprehensions|✏️ Comprehensions]]
- [[#Best-Practices|✅ Best Practices]]
- [[#Common-Pitfalls|⚠️ Common Pitfalls]]
- [[#Interview-QA|🎯 Interview Q&A]]
- [[#Navigation|🔗 Navigation]]

---

## 📝 Overview
Data structures help you **store, organize, and manage** data efficiently.

Python provides **built-in, powerful, and easy-to-use** data structures:

- Lists  
- Tuples  
- Sets  
- Dictionaries  
- Strings  
- Comprehensions for fast structure creation  

Understanding these makes your code faster, cleaner, and more efficient.  
These are also among the *most frequently asked* topics in interviews.

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

### **Q1. List vs Tuple?**

* List → Mutable
* Tuple → Immutable (faster & safer)

---

### **Q2. When do you use a set?**

* To remove duplicates
* To check membership quickly: `item in set`

---

### **Q3. Can dictionary keys be mutable?**

No. Keys must be immutable (like strings, numbers, tuples).

---

### **Q4. How do you loop through a dictionary?**

```python
for k, v in person.items():
    print(k, v)
```

---

### **Q5. Difference: `.append()` vs `.extend()`?**

* `append(x)` → adds element as a single item
* `extend([x, y])` → adds each element individually

---

### **Q6. Remove duplicates from a list?**

```python
unique_list = list(set(my_list))
```

---

### **Q7. What are comprehension advantages?**

* Short
* Clean
* Faster than loops

---

### ⭐ Bonus Mini Interview Tasks

1. Reverse a string
2. Count frequency of characters
3. Merge two dictionaries
4. Find common elements between two lists
5. Convert two lists into a dictionary

---

# 🔗 Navigation

### Next Chapter

➡️ [[04_Functions|📘 4. Functions in Python]]

### Previous Chapter

⬅️ [[02_Control_Flow|🔁 2. Control Flow]]
