# Python Programming — Comprehensive Study Notes

---

## UNIT 1: Basics of Python (15 Lectures)

### 1.1 Introduction & Overview of Python
- Python is a high-level, interpreted, general-purpose programming language created by **Guido van Rossum**, first released in 1991.
- Key features: simple syntax, dynamically typed, interpreted (not compiled), object-oriented, extensive standard library, huge third-party ecosystem (PyPI).
- Used in: web development, data science, AI/ML, automation/scripting, embedded systems, GUI apps.
- Python 2 vs Python 3: Python 2 is end-of-life; always use Python 3.x.

### 1.2 Installation and Setup
- Download from [python.org](https://python.org) or use a distribution like **Anaconda** (bundles data-science libraries).
- Verify installation:
  ```bash
  python --version
  # or on some systems
  python3 --version
  ```
- `pip` is Python's package manager, bundled with Python 3.4+:
  ```bash
  pip install package_name
  pip list
  pip uninstall package_name
  ```
- Virtual environments (isolate project dependencies):
  ```bash
  python -m venv myenv
  myenv\Scripts\activate      # Windows
  source myenv/bin/activate   # macOS/Linux
  ```

### 1.3 Python IDEs and Basic Usage
- Common IDEs/editors: **IDLE** (bundled), **VS Code**, **PyCharm**, **Jupyter Notebook** (great for data science/interactive work), **Google Colab**.
- Two modes of running Python:
  - **Interactive mode**: type `python` in terminal → REPL (Read-Eval-Print Loop).
  - **Script mode**: write code in a `.py` file and run `python filename.py`.

### 1.4 Variables and Data Types
- Variables are created by assignment — no explicit declaration needed:
  ```python
  x = 10
  name = "Alice"
  ```
- Python is **dynamically typed**: a variable's type is determined at runtime and can change.
- Core built-in data types:
  | Type | Example | Description |
  |---|---|---|
  | `int` | `10` | Whole numbers |
  | `float` | `3.14` | Decimal numbers |
  | `complex` | `3+4j` | Complex numbers |
  | `str` | `"hello"` | Text |
  | `bool` | `True`/`False` | Boolean |
  | `list` | `[1,2,3]` | Ordered, mutable |
  | `tuple` | `(1,2,3)` | Ordered, immutable |
  | `dict` | `{"a":1}` | Key-value pairs |
  | `set` | `{1,2,3}` | Unordered, unique items |
  | `NoneType` | `None` | Represents absence of value |
- Type checking and conversion:
  ```python
  type(x)          # check type
  int("5")         # str -> int
  str(5)           # int -> str
  float("3.14")    # str -> float
  ```
- Naming rules: must start with letter/underscore, case-sensitive, cannot use reserved keywords.

### 1.5 Operators and Expressions
- **Arithmetic**: `+  -  *  /  //  %  **`
  - `/` always returns a float; `//` is floor division; `%` is modulus; `**` is exponentiation.
- **Comparison**: `==  !=  >  <  >=  <=`
- **Logical**: `and  or  not`
- **Assignment**: `=  +=  -=  *=  /=  //=  %=  **=`
- **Identity**: `is`, `is not` (compares object identity, not value)
- **Membership**: `in`, `not in`
- **Bitwise**: `&  |  ^  ~  <<  >>`
- Operator precedence follows standard math conventions (PEMDAS), with logical operators lowest.

### 1.6 Input and Output
- Input is always read as a string:
  ```python
  name = input("Enter your name: ")
  age = int(input("Enter your age: "))
  ```
- Output with `print()`:
  ```python
  print("Hello", name, sep=", ", end="!\n")
  print(f"My name is {name} and I am {age} years old")   # f-strings (preferred)
  print("{} is {}".format(name, age))                      # .format() method
  print("%s is %d" % (name, age))                          # old-style formatting
  ```

### 1.7 Conditional Statements
```python
if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")
```
- Python has no `switch` statement (Python 3.10+ has `match-case` as an alternative).
- Ternary/conditional expression: `result = "Adult" if age >= 18 else "Minor"`

### 1.8 Loops
```python
# while loop
i = 0
while i < 5:
    print(i)
    i += 1

# for loop (iterates over a sequence)
for i in range(5):        # 0,1,2,3,4
    print(i)

for char in "hello":
    print(char)
```
- `range(start, stop, step)` generates a sequence of numbers.
- Loop control statements: `break` (exit loop), `continue` (skip to next iteration), `pass` (do nothing/placeholder).
- `else` clause on loops: executes if the loop completes **without** hitting `break`.

### 1.9 Control Flow Summary
- Control flow = the order in which statements execute: sequential → conditional (`if/elif/else`) → iterative (`for`/`while`) → function calls (jump to function and back).

### 1.10 Function Definition and Syntax
```python
def greet(name, greeting="Hello"):
    """Docstring: returns a greeting message."""
    return f"{greeting}, {name}!"

message = greet("Alice")
```
- Defined using `def`, indentation defines the function body, `return` sends a value back (returns `None` if omitted).

### 1.11 Scope and Lifetime of Variables
- **Local scope**: variables defined inside a function, exist only during function execution.
- **Global scope**: variables defined at module level, accessible everywhere in that module.
- **Enclosing scope**: applies to nested functions (closures).
- **Built-in scope**: names pre-defined in Python (e.g., `print`, `len`).
- This is the **LEGB rule**: Local → Enclosing → Global → Built-in (order Python searches for a name).
- Use `global` keyword to modify a global variable inside a function:
  ```python
  count = 0
  def increment():
      global count
      count += 1
  ```
- `nonlocal` is used similarly for enclosing (not global) scope in nested functions.

### 1.12 Function Arguments and Return Values
- Types of arguments:
  ```python
  def func(a, b, *args, c=10, **kwargs):
      pass
  ```
  - **Positional arguments**: `a, b`
  - **Default arguments**: `c=10`
  - **`*args`**: variable-length positional arguments (tuple)
  - **`**kwargs`**: variable-length keyword arguments (dict)
  - **Keyword arguments**: `func(a=1, b=2)` — order doesn't matter
- Functions can return multiple values (as a tuple):
  ```python
  def min_max(nums):
      return min(nums), max(nums)
  lo, hi = min_max([3,1,4,1,5])
  ```

---

## UNIT 2: Data Structures & OOP (12 Lectures)

### 2.1 Lists
- Ordered, **mutable**, allow duplicates, can hold mixed types.
```python
lst = [1, 2, 3, "four"]
lst.append(5)          # add to end
lst.insert(0, 0)        # insert at index
lst.remove("four")      # remove by value
lst.pop()                # remove & return last item (or by index)
lst.sort()               # sort in place
lst.reverse()
lst.extend([6,7])
len(lst)
```
- **Indexing**: `lst[0]` (first), `lst[-1]` (last)
- **Slicing**: `lst[start:stop:step]` → `lst[1:4]`, `lst[:3]`, `lst[::-1]` (reversed)
- List comprehension: `squares = [x**2 for x in range(10) if x % 2 == 0]`

### 2.2 Tuples
- Ordered, **immutable**, allow duplicates.
```python
t = (1, 2, 3)
single = (5,)     # note the comma — required for single-element tuple
t.count(2)
t.index(3)
```
- Immutability makes tuples hashable (usable as dict keys) and slightly faster than lists.
- Tuple unpacking: `a, b, c = (1, 2, 3)`

### 2.3 Dictionaries
- Unordered (insertion-ordered since Python 3.7+ as implementation detail, guaranteed since 3.7), key-value pairs, keys must be unique & hashable.
```python
d = {"name": "Alice", "age": 25}
d["city"] = "Pune"          # add/update
d.get("name", "default")     # safe access
d.keys(); d.values(); d.items()
d.pop("age")
for k, v in d.items():
    print(k, v)
```
- Dict comprehension: `{x: x**2 for x in range(5)}`

### 2.4 Sets
- Unordered, **unique** elements, mutable (but elements must be hashable).
```python
s = {1, 2, 3}
s.add(4)
s.remove(2)
a = {1,2,3}; b = {2,3,4}
a | b   # union
a & b   # intersection
a - b   # difference
a ^ b   # symmetric difference
```
- `frozenset` is the immutable version of a set.

### 2.5 Object-Oriented Programming (OOP)
```python
class Animal:
    species_count = 0            # class variable

    def __init__(self, name, sound):
        self.name = name          # instance variable
        self.sound = sound
        Animal.species_count += 1

    def make_sound(self):         # instance method
        return f"{self.name} says {self.sound}"

    def __str__(self):            # dunder/magic method for print()
        return f"Animal({self.name})"

class Dog(Animal):                # inheritance
    def __init__(self, name):
        super().__init__(name, "Woof")

    def make_sound(self):         # method overriding (polymorphism)
        return f"{self.name} barks: Woof!"

d = Dog("Rex")
print(d.make_sound())
```
- **Four Pillars of OOP**:
  1. **Encapsulation** — bundling data + methods; using naming conventions `_protected`, `__private` for access control.
  2. **Inheritance** — a class derives from another (`class Child(Parent)`); supports multiple inheritance.
  3. **Polymorphism** — same method name behaves differently across classes (method overriding).
  4. **Abstraction** — hiding implementation details (via abstract base classes, `abc` module).
- Class vs instance variables; `self` refers to the current instance; `__init__` is the constructor.
- Common dunder methods: `__init__`, `__str__`, `__repr__`, `__len__`, `__eq__`.

### 2.6 Importing Modules & Creating Packages
```python
import math
from math import sqrt, pi
import numpy as np
from mypackage import mymodule
```
- A **module** is a single `.py` file; a **package** is a directory of modules containing an `__init__.py` file.
```
mypackage/
    __init__.py
    module1.py
    module2.py
```
- Import your own module: `import module1` (if in same directory or on `sys.path`).

---

## UNIT 3: Functions (5 Lectures)
*(Reinforces Unit 1's function concepts — likely covered in more depth/practice)*

- Function definition, syntax, docstrings, and calling conventions (see 1.10).
- Scope & lifetime — LEGB rule, `global`/`nonlocal` (see 1.11).
- Arguments & return values — positional, default, `*args`, `**kwargs`, multiple returns (see 1.12).
- Additional concepts often covered here:
  - **Recursion**: a function calling itself (e.g., factorial, Fibonacci) — needs a base case to avoid infinite recursion.
    ```python
    def factorial(n):
        return 1 if n == 0 else n * factorial(n - 1)
    ```
  - **Lambda functions**: anonymous, single-expression functions: `square = lambda x: x**2`
  - **Higher-order functions**: `map()`, `filter()`, `reduce()` (from `functools`)
    ```python
    list(map(lambda x: x*2, [1,2,3]))
    list(filter(lambda x: x % 2 == 0, [1,2,3,4]))
    ```
  - **Decorators**: functions that wrap other functions to extend behavior (`@decorator_name`).

---

## UNIT 4: File Handling (5 Lectures)

### 4.1 Reading and Writing Files
```python
# Writing
with open("data.txt", "w") as f:
    f.write("Hello, World!\n")

# Appending
with open("data.txt", "a") as f:
    f.write("New line\n")

# Reading
with open("data.txt", "r") as f:
    content = f.read()         # entire file as string
    # OR
    lines = f.readlines()      # list of lines
    # OR
    for line in f:             # line-by-line iteration
        print(line.strip())
```
- The `with` statement (context manager) auto-closes the file — always preferred over manual `open()`/`close()`.
- File modes: `"r"` (read), `"w"` (write, overwrites), `"a"` (append), `"r+"` (read+write), `"b"` suffix for binary (e.g., `"rb"`, `"wb"`).

### 4.2 Operations on Files
```python
import os
os.path.exists("data.txt")
os.remove("data.txt")
os.rename("old.txt", "new.txt")
os.path.getsize("data.txt")
```
- Working with CSV: `import csv` → `csv.reader()`, `csv.writer()`, `csv.DictReader()`.
- Working with JSON: `import json` → `json.dump(obj, file)`, `json.load(file)`.

### 4.3 Exception Handling
```python
try:
    with open("missing.txt") as f:
        data = f.read()
except FileNotFoundError as e:
    print(f"File not found: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
else:
    print("File read successfully")   # runs if no exception
finally:
    print("Done attempting file read")  # always runs
```
- Common built-in exceptions: `ValueError`, `TypeError`, `IndexError`, `KeyError`, `ZeroDivisionError`, `FileNotFoundError`.
- `raise Exception("custom message")` — manually raise exceptions.
- Custom exceptions: `class MyError(Exception): pass`

---

## UNIT 5: Working with Libraries (18 Lectures)

### 5.1 NumPy (Numerical Python)
```python
import numpy as np
arr = np.array([1, 2, 3, 4])
arr.shape; arr.dtype; arr.ndim
zeros = np.zeros((2,3))
ones = np.ones((3,3))
arange = np.arange(0, 10, 2)
reshaped = arr.reshape(2, 2)

# Vectorized operations (fast, no explicit loops)
arr * 2
arr + arr
np.sum(arr); np.mean(arr); np.max(arr); np.std(arr)

# Indexing/slicing (similar to lists, but supports multi-dim)
matrix = np.array([[1,2],[3,4]])
matrix[0, 1]     # row 0, col 1
matrix[:, 0]     # entire first column
```
- Key advantage over lists: NumPy arrays are stored contiguously in memory → much faster for numerical computation, support broadcasting.

### 5.2 Pandas (Data Manipulation Library)
```python
import pandas as pd

df = pd.read_csv("data.csv")
df.head(); df.tail(); df.info(); df.describe()
df["column_name"]                 # select column (Series)
df[["col1", "col2"]]              # select multiple columns
df.loc[0]                         # select row by label
df.iloc[0]                        # select row by position
df[df["age"] > 25]                # filter rows

df["new_col"] = df["col1"] * 2
df.dropna()                        # remove missing values
df.fillna(0)                       # fill missing values
df.groupby("category").mean()
df.sort_values("age", ascending=False)
df.to_csv("output.csv", index=False)
```
- Core data structures: **Series** (1D labeled array) and **DataFrame** (2D labeled table).

### 5.3 Tkinter (GUI Library)
```python
import tkinter as tk

root = tk.Tk()
root.title("My App")
root.geometry("300x200")

label = tk.Label(root, text="Hello!")
label.pack()

def on_click():
    label.config(text="Button Clicked!")

button = tk.Button(root, text="Click Me", command=on_click)
button.pack()

entry = tk.Entry(root)
entry.pack()

root.mainloop()      # starts the GUI event loop
```
- Common widgets: `Label`, `Button`, `Entry`, `Text`, `Frame`, `Canvas`, `Checkbutton`, `Radiobutton`, `Listbox`, `Menu`.
- Layout managers: `.pack()` (simple stacking), `.grid()` (row/column), `.place()` (absolute positioning) — **don't mix these in the same container**.
- Event binding: `widget.bind("<Button-1>", callback_function)`

### 5.4 Basic GUI Application Development
- Typical structure: create root window → add widgets → define event handlers/callbacks → start `mainloop()`.
- Simple example — a basic calculator or to-do list app is a common practical exercise combining Entry, Button, and Label widgets with functions tied to button commands.

---

## UNIT 6: Web Development Basics (Flask)

### 6.1 Introduction to Web Frameworks
- A **web framework** provides tools/libraries to build web applications without handling low-level HTTP details from scratch.
- **Flask** is a lightweight, "micro" web framework for Python — minimal core, extensible via extensions (unlike Django, which is a full-featured "batteries-included" framework).
- Install: `pip install flask`

### 6.2 Building a Simple Web Application
```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, Flask!"

@app.route("/greet/<name>")
def greet(name):
    return f"Hello, {name}!"

@app.route("/form", methods=["GET", "POST"])
def form():
    if request.method == "POST":
        user_input = request.form["username"]
        return f"Received: {user_input}"
    return """<form method="post">
                <input name="username">
                <button type="submit">Submit</button>
              </form>"""

if __name__ == "__main__":
    app.run(debug=True)
```
- **Routing**: `@app.route()` decorator maps a URL path to a Python function (a "view function").
- **Dynamic routes**: `<name>` captures a URL segment as a function parameter; type converters like `<int:id>` are available.
- **HTTP methods**: `GET` (retrieve data, default) vs `POST` (submit data).
- **Templates**: Flask uses the **Jinja2** templating engine; templates go in a `templates/` folder and are rendered with `render_template("index.html", variable=value)`.
  ```html
  <!-- templates/index.html -->
  <h1>Hello, {{ name }}!</h1>
  {% if user %}
    <p>Welcome back!</p>
  {% endif %}
  ```
- **Static files** (CSS, JS, images) go in a `static/` folder, referenced via `url_for('static', filename='style.css')`.
- **`request` object**: gives access to form data (`request.form`), query params (`request.args`), and JSON body (`request.json`).
- `debug=True` enables auto-reload and detailed error pages during development (never use in production).

---
