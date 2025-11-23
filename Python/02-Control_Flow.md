---
tags:
  - python
  - control-flow
  - basics
aliases:
  - Python Flow Control
  - If Else While For
date: 2025-11-17
---

# 🔁 Control Flow — Python

## Table of Contents  
- [What is Control Flow?](#what-is-control-flow)  
- [Decision-Making: `if`, `elif`, `else`](#decision-making-if-elif-else)  
- [Looping: `for` and `while`](#looping-for-and-while)  
- [Loop Control: `break`, `continue`, `pass`](#loop-control-break-continue-pass)  
- [Loop-`else`](#loop-else)  
- [Best Practices & Tips](#best-practices--tips)  
- [Common Mistakes](#common-mistakes)  
- [Interview Questions](#interview-questions)  

---

## What is Control Flow?  
Control flow is how you make your Python program **do different things** or **repeat things**, instead of just going line by line. It's what gives your code logic — like decision-making or repeating tasks. Real Python explains that control flow is what changes the “normal” sequential execution of code.

---

## Decision-Making: `if`, `elif`, `else`  
- Use `if` when you want to do something only if a condition is true.  
- Use `elif` (“else if”) to check another condition if the first one didn’t match.  
- Use `else` to run code when none of the `if` / `elif` conditions are true.

**Example:**
```python
score = 85
if score >= 90:
    print("A grade")
elif score >= 80:
    print("B grade")
else:
    print("Keep trying!")
````

**Why this matters:** This is how your program *makes choices*. Without it, your program would just run from top to bottom doing the same thing always.

---

## Looping: `for` and `while`

Loops let you **repeat** actions.

* **`for` loop:** Use this when you want to loop over a sequence (like a list, string, or `range`).
  Example:

  ```python
  for color in ["red", "green", "blue"]:
      print(color)
  ```

* **`while` loop:** Use this when you want to repeat something **as long as a condition is true**.
  Example:

  ```python
  count = 1
  while count <= 3:
      print("Counting:", count)
      count += 1
  ```

---

## Loop Control: `break`, `continue`, `pass`

These keywords give you more control inside loops.

* **`break`** — Exit the loop immediately.

  ```python
  for num in range(10):
      if num == 5:
          break  
      print(num)
  # Prints: 0 1 2 3 4  
  ```

  (GeeksforGeeks explains this usage.) ([GeeksforGeeks][1])

* **`continue`** — Skip the rest of the code for this iteration, and go to the next iteration.

  ```python
  for num in range(5):
      if num == 2:
          continue  
      print(num)
  # Prints: 0 1 3 4  
  ```

  (Also from GeeksforGeeks.) ([GeeksforGeeks][2])

* **`pass`** — Does nothing. It’s a placeholder where code is syntactically required but you don’t want anything to happen now.

  ```python
  for num in range(3):
      pass  # I will write logic here later
  ```

  (Useful for scaffolding / planning) ([Python Guild][3])

---

## Loop-`else`

* In Python, you can attach an `else` to loops (`for` or `while`).
* This `else` runs **only when the loop finishes normally** (i.e., not by `break`). ([Python documentation][4])
* Example (from Python docs):

  ```python
  for n in range(2, 10):
      for x in range(2, n):
          if n % x == 0:
              break
      else:
          print(n, "is a prime number")
  ```

  Here, the inner `else:` is tied to the `for x …` loop and runs only if the loop didn’t `break`. ([Python documentation][4])

---

## Best Practices & Tips

* Use **clear conditions** in `if` statements — avoid very complicated boolean logic without comments.
* Be careful with indentation — Python uses indentation to define blocks. ([csee.umbc.edu][5])
* When using `while`, make sure the loop will eventually stop (otherwise you’ll get an infinite loop).
* Use `break`, `continue`, and `pass` sparingly — too many of them can make your loops hard to read.
* Use `pass` when sketching out code, but replace it later with real logic.

---

## Common Mistakes

* Forgetting to indent properly under `if`, `for`, `while` → Syntax errors. ([csee.umbc.edu][5])
* Using `break` / `continue` outside of a loop → error. RealPython warns about this. ([Real Python][6])
* Not realizing `else` on a loop only runs if there was **no** `break`. ([Python documentation][7])
* Using `pass` as a “temporary do-nothing” but forgetting to replace it later.

---

## Interview Questions

Here are some common interview-style questions you can add to your notes / use for practice:

1. What is the difference between `if`, `elif`, and `else` in Python?
2. When would you use a `while` loop vs a `for` loop?
3. What does the `break` statement do? Give an example.
4. What does `continue` do? How is it different from `break`?
5. What is the use of `pass` in Python? Why not just leave the block empty?
6. How does the `else` clause on a loop work in Python? When will it execute?

---

## 🔍 Interview Questions

|#|Question|What They Expect|
|---|---|---|
|1|What is the difference between `for` and `while` loops?|`for` → known repeats, `while` → condition-based|
|2|Can you explain `break` vs `continue`?|Stop loop vs skip iteration|
|3|What happens if you forget to update the condition in a `while` loop?|Infinite loop|
|4|What is the purpose of `pass`?|Placeholder for future code|
|5|How does Python handle indentation in control flow?|Mandatory indentation defines scope|
|6|Can you nest loops and conditions in Python?|Yes — used in many algorithms|
|7|Can `else` be used with loops?|Yes → executes if loop ends normally (no break)|
|8|Why is control flow important?|Adds logic, decision-making, flexibility|
