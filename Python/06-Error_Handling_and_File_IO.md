---
tags:
  - python
  - error-handling
  - exceptions
  - file-io
  - python-basics
aliases:
  - Python Error Handling
  - Python File I/O
date: 2025-11-17
---
# 🚨 6. Error Handling & File I/O — Python

## 📜 Table of Contents
- [[#Overview|Overview]]
- [[#Exception-Handling|🔥 Exception Handling]]
  - try / except / else / finally
  - Multiple exceptions
  - Exception hierarchy
  - Raising exceptions
  - Custom exceptions
- [[#File-IO|📁 File I/O]]
  - Reading & writing text files
  - Modes (r, w, a, x, rb, wb)
  - CSV handling
  - JSON handling
- [[#Best-Practices|✅ Best Practices]]
- [[#Common-Pitfalls|⚠️ Common Pitfalls]]
- [[#Interview-QA|🎯 Interview Q&A]]
- [[#Navigation|🔗 Navigation]]

---

# 📝 Overview
Errors are common in programs. Python provides **exception handling** so your program doesn't crash unexpectedly.

File I/O (Input/Output) lets you **read and write files** such as text, CSV, and JSON.

Understanding error handling + file operations is essential for **backend, automation, scripting, and system-level Python work**.

---

# 🔥 Exception Handling

Python uses:

- `try`
- `except`
- `else`
- `finally`
- `raise`

to safely manage errors.

---

## ✔️ Basic Syntax

```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
finally:
    print("This runs no matter what.")
````

### 📌 Block meanings:

* **try** → risky code
* **except** → what to do when error happens
* **else** → runs if **no** error
* **finally** → *always* runs (cleanup, closing files)

---

## ✔️ Using `else` with try-except

```python
try:
    num = int("10")
except ValueError:
    print("Invalid number")
else:
    print("Conversion successful:", num)
```

---

## ✔️ Catching Multiple Exceptions

### Separate except blocks:

```python
try:
    result = 10 / 0
except ValueError:
    print("Value error!")
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

### Using a tuple:

```python
except (ValueError, TypeError):
    print("One of these errors occurred.")
```

---

## ✔️ The Exception Hierarchy (Simplified)

```
BaseException
 ├── Exception
 │    ├── ArithmeticError
 │    │    └── ZeroDivisionError
 │    ├── ValueError
 │    ├── TypeError
 │    └── KeyError
 └── SystemExit
```

---

## ✔️ Raising Your Own Exception

```python
def check_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative!")
```

---

## ✔️ Custom Exceptions

```python
class InvalidScoreError(Exception):
    pass

def set_score(score):
    if score > 100:
        raise InvalidScoreError("Score cannot exceed 100")
```

---

# 📁 File I/O

Python uses `open()` to interact with files.

### 📌 File Modes

| Mode | Meaning                       |
| ---- | ----------------------------- |
| `r`  | read (default)                |
| `w`  | write (overwrite)             |
| `a`  | append                        |
| `x`  | create file (error if exists) |
| `rb` | read binary                   |
| `wb` | write binary                  |

---

## ✔️ Reading & Writing Text Files

### Writing:

```python
with open("notes.txt", "w") as f:
    f.write("Hello, world!")
```

### Reading:

```python
with open("notes.txt", "r") as f:
    data = f.read()
    print(data)
```

### Read line-by-line:

```python
with open("notes.txt") as f:
    for line in f:
        print(line.strip())
```

Using `with` ensures the file closes automatically.

---

## ✔️ CSV Files

### Writing:

```python
import csv

with open("data.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["name", "age"])
    writer.writerow(["Alex", 25])
```

### Reading:

```python
with open("data.csv") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

---

## ✔️ JSON Files

### Writing JSON:

```python
import json

data = {"name": "Alex", "age": 25}

with open("info.json", "w") as f:
    json.dump(data, f, indent=4)
```

### Reading JSON:

```python
with open("info.json") as f:
    info = json.load(f)
    print(info)
```

---

# ✅ Best Practices

* Always use **`with open()`** to handle files.
* Catch specific exceptions (not plain `except:`).
* Add helpful messages to raised exceptions.
* Validate file existence using `os.path.exists()`.
* Use `try/except` around file operations (I/O is risky).
* Don’t expose raw exceptions directly in APIs.

---

# ⚠️ Common Pitfalls

### ❌ Forgetting to close files

Fix: Always use `with open()`.

### ❌ Using bare except

```python
except:
    pass   # BAD
```

This hides bugs. Always catch specific exceptions.

### ❌ Incorrect file paths

Use `r"path\file.txt"` or `os.path.join()`.

### ❌ Assuming JSON/CSV format correctness

Always use try-except with JSON parsing.

```python
try:
    json.load(f)
except json.JSONDecodeError:
    print("Invalid JSON")
```

### ❌ Using write mode accidentally

Using `"w"` will delete file contents.

---

# 🎯 Interview Q&A

### **Q1. Difference between `except` and `finally`?**

* `except` runs **only when an error happens**.
* `finally` runs **always**, even after return or crash.

---

### **Q2. What is the use of `else` in try-except?**

Runs **only if no exception** occurs in the try block.

---

### **Q3. Why is `with open()` recommended?**

* Automatic file closing
* Handles exceptions cleanly
* Prevents resource leaks

---

### **Q4. How do you raise a custom exception?**

```python
raise MyError("message")
```

---

### **Q5. What exception occurs when converting `"abc"` to int?**

`ValueError`

---

### **Q6. What is the difference between `w` and `a` modes?**

* `w` overwrites the file
* `a` appends to the end of the file

---

### **Q7. How to catch multiple exceptions?**

```python
except (ValueError, TypeError):
```

---

### **Q8. What happens if you don’t close files?**

It can cause:

* Memory leaks
* File corruption
* OS limits getting exhausted

---

### **Q9. How to parse JSON safely?**

```python
try:
    data = json.load(f)
except json.JSONDecodeError:
    print("Invalid JSON")
```

---

### **Q10. What is the role of `__enter__` and `__exit__` in file I/O?**

They run behind the scenes in `with open()`, managing cleanup and auto-closing files.

---

# 🔗 Navigation

### Next Chapter

➡️ [[07_OOP|🏛️ 7. Object-Oriented Programming]]

### Previous Chapter

⬅️ [[05_Modules_and_Packages|📦 5. Modules & Packages]]
