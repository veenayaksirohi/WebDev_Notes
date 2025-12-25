---
tags:
  - python
  - modules
  - packages
  - standard-library
  - python-basics
aliases:
  - Python Modules
  - Python Packages
  - Python Standard Library
date: 2025-11-17
---

# 📦 5. Modules, Packages & Standard Library — Python

## 📜 Table of Contents
- [[#Overview|Overview]]
- [[#Modules|🧩 Modules]]
  - Import styles (import, from-import, alias)
  - Reloading modules
  - dir(), __name__ usage
- [[#Standard-Library|📚 Standard Library]]
- [[#Custom-Modules|🛠️ Creating Custom Modules]]
- [[#Packages|📁 Python Packages]]
  - __init__.py
  - Subpackages
- [[#Virtual-Environments|🌱 Environment Management]]
  - venv
  - pip
  - conda
- [[#Interview-QA|🎯 Interview Q&A]]
- [[#Navigation|🔗 Navigation]]

---

# 📝 Overview
Python encourages clean organization of code using **modules** and **packages**.  
These help you:

- Reuse functions and classes
- Keep code organized and readable
- Break big projects into smaller logical files
- Avoid repeating logic (DRY principle)

Python also comes with a **rich Standard Library**, a collection of ready-made modules for file handling, networking, math, OS interaction, and more.

---

# 🧩 Modules

A **module** is simply a Python file (`.py`) that contains:

- Variables  
- Functions  
- Classes  
- Code you want to reuse  

Example of a module file `math_utils.py`:

```python
# math_utils.py
def add(a, b):
    return a + b

PI = 3.14159
````

You can import this into any other file.

---

## ✔️ Importing Modules (All 4 Methods)

### 1️⃣ **Basic Import**

```python
import math
print(math.sqrt(16))
```

### 2️⃣ **Import Specific Names**

```python
from math import sqrt, pi
print(sqrt(25))
```

### 3️⃣ **Alias (Renaming during import)**

```python
import datetime as dt
print(dt.datetime.now())
```

### 4️⃣ **Import Everything (not recommended)**

```python
from math import *
```

⚠️ **Avoid `*` imports** — they pollute the namespace and make debugging difficult.

---

## ✔️ Checking Contents of a Module

Use `dir()`:

```python
import math
print(dir(math))
```

---

## ✔️ The `__name__` Variable

Every module has a special built-in variable:

* If file is run directly → `__name__ == "__main__"`
* If imported → `__name__ == "modulename"`

```python
if __name__ == "__main__":
    print("Run directly")
else:
    print("Imported")
```

Useful for writing test code at bottom of modules.

---

## ✔️ Reloading a Module (during Testing)

```python
import importlib
importlib.reload(module_name)
```

---

# 📚 Standard Library (Most Useful Modules)

Python comes with **hundreds of built-in modules**:

### 🔢 **math**

```python
import math
math.sqrt(16)
math.floor(3.7)
```

### 🗓️ **datetime**

```python
from datetime import datetime
print(datetime.now())
```

### 🗂️ **os**

```python
import os
print(os.getcwd())
os.listdir()
```

### 💻 **sys**

```python
import sys
print(sys.version)
```

### 🎲 **random**

```python
import random
random.randint(1, 10)
```

### 📄 **json**

```python
import json
data = json.loads('{"x":10}')
```

These modules save huge development time—no need to reinvent the wheel.

---

# 🛠️ Creating Custom Modules

1. Create a file → `utils.py`
2. Add functions/classes
3. Import in another script

```python
# utils.py
def greet(name):
    return f"Hello {name}"

# main.py
from utils import greet
print(greet("Alex"))
```

---

# 📁 Python Packages

A **package** is a folder containing multiple modules + an `__init__.py` file.

```
mypackage/
│── __init__.py
│── math_ops.py
│── string_ops.py
```

### Importing from a package

```python
from mypackage.math_ops import add
```

---

## 🧩 `__init__.py` — What It Does?

* Marks the folder as a Python package
* Can define what gets imported via `mypackage`
* Can run initialization code

Example:

```python
# __init__.py
from .math_ops import add
```

Now:

```python
from mypackage import add
```

---

## 📦 Subpackages (Nested Packages)

```
mypackage/
│── data/
│    ├── __init__.py
│    ├── loader.py
│── utils/
│    ├── __init__.py
│    ├── formatter.py
```

Usage:

```python
from mypackage.data.loader import load_csv
```

---

# 🌱 Virtual Environments & Dependency Management

To avoid mixing project dependencies, always use a **virtual environment**.

---

## ✔️ Virtual Environment (venv)

### Create:

```bash
python -m venv venv
```

### Activate:

Windows:

```bash
venv\Scripts\activate
```

Mac/Linux:

```bash
source venv/bin/activate
```

### Deactivate:

```bash
deactivate
```

---

## ✔️ pip — Package Installer

Install:

```bash
pip install requests
```

List:

```bash
pip list
```

Freeze:

```bash
pip freeze > requirements.txt
```

Install from requirements:

```bash
pip install -r requirements.txt
```

---

## ✔️ conda — Popular in Data Science

Create:

```bash
conda create -n myenv python=3.10
```

Activate:

```bash
conda activate myenv
```

Install:

```bash
conda install numpy
```

---

# 🎯 Interview Q&A

### **Q1. What is a module in Python?**

A module is a single `.py` file containing reusable code.

---

### **Q2. What is the difference between a module and a package?**

| Module              | Package                                     |
| ------------------- | ------------------------------------------- |
| A single `.py` file | A folder containing modules + `__init__.py` |
| Small unit          | Larger collection of modules                |
| Example: `math.py`  | Example: `numpy`                            |

---

### **Q3. Why is `__init__.py` needed?**

It tells the interpreter to treat a directory as a package.

---

### **Q4. Why use virtual environments?**

To isolate dependencies per project and avoid version conflicts.

---

### **Q5. What are some commonly used built-in modules?**

* math
* datetime
* os
* sys
* random
* json

---

### **Q6. How do you import a module with an alias?**

```python
import numpy as np
```

---

### **Q7. How do you import from a subpackage?**

```python
from package.subpackage.module import function
```

---

### **Q8. How to check what functions a module contains?**

```python
dir(module)
```

---

### **Q9. What is `pip freeze` used for?**

Creating a list of installed packages for sharing / deployment.

---

### **Q10. How do you reload a module while testing?**

```python
import importlib
importlib.reload(module)
```

---

## 🔗 Links & Navigation

- **Home**: [[Table Of Content]]
- **Previous**: [[04-Functions_&_Functional_Programming]]
- **Next**: [[06-Error_Handling_and_File_IO]]
