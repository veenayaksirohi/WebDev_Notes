---
tags:
  - python
  - basics
  - programming-fundamentals
  - interview-prep
aliases:
  - Python Fundamentals  Interview Questions
date: 2025-11-17
---
# 🐍 Overview & Fundamentals — Python

## Table of Contents  
- [🐍 Overview \& Fundamentals — Python](#-overview--fundamentals--python)
  - [Table of Contents](#table-of-contents)
  - [📝 Overview](#-overview)
  - [🏗️ Language Structure](#️-language-structure)
  - [🗃️ Data Handling](#️-data-handling)
  - [➕ Operators](#-operators)
  - [🔄 Interactivity](#-interactivity)
  - [✅ Best Practices](#-best-practices)
  - [⚠️ Common Pitfalls](#️-common-pitfalls)
  - [🌐 Real-World Applications](#-real-world-applications)
  - [🔍 Interview Questions](#-interview-questions)
  - [🔗 Links \& Navigation](#-links--navigation)

---

## 📝 Overview  
Python is a high-level, interpreted language that emphasises readability and simplicity. It supports **multiple paradigms** — object-oriented, procedural, and functional — making it very versatile. Because it is open-source, there’s a large, active community contributing to its growth.

**Core Strengths:**
- Readable syntax → easy to write & maintain  
- Massive standard library + third-party ecosystem  
- Cross-platform compatibility (Windows / macOS / Linux)  
- Rapid prototyping via REPL & scripting  
- Strong community + documentation

### What This Means, in Simple Language

1. **High-Level & Interpreted**
    
    - _High-level_ means Python handles a lot of the “hard work” of programming — you don’t need to manage low-level details like memory as much.
        
    - _Interpreted_ means Python runs your code line by line (rather than first converting all of it into machine code), which makes testing and debugging easier.
        
2. **Readable and Simple**
    
    - Python’s syntax (how you write code) is very clean and looks close to English — this makes it easy to read, even for beginners.
        
    - Because it’s easy to read, writing and understanding programs is less stressful, and teams can maintain code more easily.
        
3. **Supports Multiple Paradigms**
    
    - Python is very flexible: you can write code in different styles:
        
        - **Procedural** (step-by-step)
            
        - **Object-oriented** (using classes and objects)
            
        - **Functional** (using functions as first-class elements)
            
    - This means you can choose the best style for a particular problem.
    
4. **Open-Source & Community**
    
    - Python is _open-source_, so anyone can see, use, and contribute to its code. 
        
    - There is a **very active community** of developers who build libraries, help each other, and keep improving Python.

---

## 🏗️ Language Structure  
- **Syntax**: Uses whitespace (indentation) to define blocks instead of braces.  
- **Indentation**: Essential — inconsistent indentation leads to syntax errors.  
- **Semantics**:  
  - Statements usually end at a newline.  
  - For multi-line, you can use `\` or parentheses:  
    ```python
    total = (a + b +
             c + d)
    ```

---

## 🗃️ Data Handling  
- **Variables**: Dynamically typed; you don’t declare the type.  
- **Common Data Types**:  
  - Integer: `x = 10`  
  - Float: `price = 19.99`  
  - String: `name = "Python"`  
  - Boolean: `flag = True`  
- **Other Types**: Lists, tuples, sets, dictionaries, etc.

**Example:**
```python
count = 5
temperature = 36.6
greeting = "Hello, Python!"
is_active = False
````

---

## ➕ Operators

| Category   | Operators                           | Use Case                |                            |
| ---------- | ----------------------------------- | ----------------------- | -------------------------- |
| Arithmetic | `+`, `-`, `*`, `/`, `%`, `**`, `//` | Math operations         |                            |
| Comparison | `==`, `!=`, `>`, `<`, `>=`, `<=`    | Conditional checks      |                            |
| Logical    | `and`, `or`, `not`                  | Boolean logic           |                            |
| Bitwise    | `&`, `                              | `, `^`, `~`, `<<`, `>>` | Low-level bit manipulation |

**Example:**

```python
a = 7
b = 3
print(a + b)    # 10  
print(a ** b)   # 343  
print((a & b), (a | b))  # bitwise and / or  
```

---

## 🔄 Interactivity

* **Input**: Use `input()` to read from the user.
* **Output**: Use `print()` to display output to the console.

**Example:**

```python
username = input("Enter your name: ")
print("Welcome,", username)
```

---

## ✅ Best Practices

* Use clear, descriptive variable names (`total_cost`, `num_items`)
* Stick to 4 spaces for indentation (PEP 8 style)
* Write comments when logic is non-trivial
* Use functions to break code into meaningful pieces

---

## ⚠️ Common Pitfalls

* Mixing tabs and spaces → syntax errors
* Forgetting indentation or mis-indenting
* Reassigning variables without thinking about type

---

## 🌐 Real-World Applications

* Scripting / Automation 🛠️
* Web backend development 🌍
* Data Science / Machine Learning 📊
* Prototyping & MVPs

---

## 🔍 Interview Questions

Here are common interview questions related to this “Basics & Fundamentals” topic — good to include in your notes for revision.

| # | Question                                                         | Key Points to Cover                                                                                                                   |
| - | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| 1 | Is Python a compiled language or an interpreted language?        | Explain that in practice, Python uses a compilation to bytecode stage then execution via Python virtual machine. ([GeeksforGeeks][1]) |
| 2 | What is the difference between `/` and `//` in Python?           | Division vs floor division. ([GeeksforGeeks][1])                                                                                      |
| 3 | What is indentation in Python, and why is it important?          | Code blocks defined by indentation — mandatory in Python. ([w3schools.com][2])                                                        |
| 4 | What are built-in data types in Python?                          | e.g., `int`, `float`, `str`, `list`, `tuple`, `dict`, `set`, etc. ([w3schools.com][2])                                                |
| 5 | What is the difference between mutable and immutable data types? | Lists/dicts mutable, strings/tuples immutable. ([DataCamp][3])                                                                        |

**Tip for your interviews:**

* For each question, practice **not just answering**, but also **explaining** *why* something is that way (e.g., why Python uses indentation).
* Write a **short code example** in your notes that illustrates each concept.
* Link these questions to deeper pages (e.g., “Data Structures”, “Functions”) to revisit when you go further.

---

## 🔗 Links & Navigation

* Next: [[Python Data Structures]]
* Previous / See also: [[Introduction to Programming Concepts]]

---