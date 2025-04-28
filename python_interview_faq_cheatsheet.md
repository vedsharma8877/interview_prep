# Python Interview FAQ & Cheatsheet (with Detailed Explanations)

A comprehensive list of frequently asked Python interview questions, concepts, and code examples for quick reference. Each section contains explanations and examples.

---

## 1. What are the key features of Python?

**Explanation:**  
Python is a versatile, high-level programming language known for its readability and simplicity. Its key features include:

- **Easy to Read, Learn, and Write:** Python syntax is designed to be intuitive and its code is easy to read.
- **Interpreted Language:** Python code is executed line-by-line, which makes debugging easier.
- **Dynamically Typed:** You don’t need to declare variable types; Python infers types at runtime.
- **Garbage Collection & Memory Management:** Python handles memory management automatically.
- **Object-Oriented & Functional Programming:** Supports both paradigms, allowing for flexibility in programming style.
- **Large Standard Library:** Comes with a “batteries included” philosophy, providing modules for almost everything.
- **Cross-Platform:** Runs on Windows, macOS, Linux, and more.
- **Vast Ecosystem & Libraries:** Rich third-party ecosystem for web, data, AI, networking, etc.
- **Ideal for Prototyping and Rapid Development:** Quick to write and iterate code.
- **Community Support:** Extensive documentation, forums, and open-source contributions.

---

## 2. Difference between Python 2 and Python 3

**Explanation:**  
Python 3 is the future and actively maintained, while Python 2 is obsolete. The main differences are:

| Feature              | Python 2                    | Python 3                         |
|----------------------|----------------------------|----------------------------------|
| 📆 Release Year      | 2000                       | 2008                             |
| 🚫 End of Life       | January 1, 2020            | Actively maintained              |
| 🖨️ Print Statement  | `print "Hello"`            | `print("Hello")` (function)      |
| 🔢 Integer Division  | `5 / 2 = 2` (floor)        | `5 / 2 = 2.5` (true division)    |
| 🧵 Unicode Support   | ASCII strings by default    | Unicode strings by default       |
| 📥 Input Function    | `raw_input()`, `input()`   | `input()` always returns string  |
| ⏪ Backward Compat.  | Yes                        | No (not compatible with Py2)     |
| 🛠 Library Support   | Some older libraries        | Most modern libraries            |
| ✨ Syntax            | Limited                     | Type hints, async/await, f-strings, etc. |

**Example:**  
```python
# Python 2
print "Hello"
# Python 3
print("Hello")
```
---

## 3. Python Memory Management & Garbage Collection

**Explanation:**  
Python automatically manages memory through:

- **Automatic Memory Management:** Programmers do not need to allocate or free memory manually.
- **Private Heap Space:** All Python objects and data structures are stored in a private heap managed internally.
- **Memory Allocation:** Python uses object-specific allocators and memory pools (`pymalloc`) for efficiency.
- **Garbage Collection:** Unused objects are automatically deleted using reference counting and a cyclic garbage collector for reference cycles.
- **gc Module:** Allows manual control over garbage collection.

**Example:**  
```python
import gc
gc.collect()   # Force garbage collection
gc.get_stats() # Get GC stats
```
---

## 4. What are Python’s built-in data types?

**Explanation:**  
Python provides several built-in data types:

- **Basic Types:** `int`, `float`, `complex`, `bool`, `str`
- **Sequence Types:** `list` (mutable), `tuple` (immutable), `range`
- **Set Types:** `set` (mutable, unique), `frozenset` (immutable)
- **Mapping Type:** `dict` (key-value pairs)
- **None Type:** `NoneType` (absence of value)
- **Binary Types:** `bytes`, `bytearray`, `memoryview`

**Example Table:**

| Type      | Example                   | Description                       |
|-----------|---------------------------|-----------------------------------|
| int       | `x = 10`                  | Integer numbers                   |
| list      | `[1, 2, 3]`               | Ordered, mutable sequence         |
| dict      | `{"a": 1, "b": 2}`        | Key-value pairs                   |
| set       | `{1, 2, 3}`               | Unordered, unique elements        |
| NoneType  | `x = None`                | Represents 'no value'             |

---

## 5. Mutable vs Immutable Data Types

**Explanation:**  
- **Mutable objects** can be changed in place (e.g., lists, dicts, sets, bytearray).
- **Immutable objects** cannot be changed after creation (e.g., int, float, str, tuple, frozenset, bytes).

**Example:**
```python
# Immutable
s = "Hello"
print(id(s))
s += " World"
print(id(s))  # Different address

# Mutable
l = [1, 2, 3]
print(id(l))
l.append(4)
print(id(l))  # Same address
```
---

## 6. Difference between shallow and deep copy

**Explanation:**  
- **Shallow Copy (`copy.copy()`):** Copies the outer object but not nested objects; inner objects are shared.
- **Deep Copy (`copy.deepcopy()`):** Copies everything recursively; inner objects are cloned.

**Example:**
```python
import copy
original = [[1, 2], [3, 4]]
shallow = copy.copy(original)
deep = copy.deepcopy(original)
original[0][0] = 99
print("Original:", original)   # [[99, 2], [3, 4]]
print("Shallow:", shallow)     # [[99, 2], [3, 4]] ← affected
print("Deep:", deep)           # [[1, 2], [3, 4]] ← not affected
```
---

## 7. How to swap two variables in Python?

**Explanation:**  
Python allows swapping variables without using a temporary variable thanks to tuple unpacking.

**Example:**
```python
a = 5
b = 10
a, b = b, a
print(a, b)  # 10 5
```
---

## 8. Difference between `is` and `==`

**Explanation:**
- `==` compares values (contents).
- `is` compares identities (memory addresses).

**Example:**
```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b)   # True (values equal)
print(a is b)   # False (different objects)
```
---

## 9. How to handle exceptions in Python?

**Explanation:**  
Python uses `try`, `except`, `else`, and `finally` blocks for exception handling.

- `try`: Code that might cause an exception.
- `except`: Code that runs if an exception occurs.
- `else`: Runs if no exception occurs.
- `finally`: Always runs (for cleanup).

**Example:**
```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("You can't divide by zero!")
finally:
    print("Cleanup actions")
```

**Common Exceptions:**  
| Exception         | Triggered When…           | Example            |
|-------------------|--------------------------|--------------------|
| ZeroDivisionError | Division by zero          | `10 / 0`           |
| ValueError        | Wrong value type          | `int("abc")`       |
| TypeError         | Wrong data type           | `"2" + 2`          |
| KeyError          | Missing dict key          | `mydict['x']`      |
| FileNotFoundError | File doesn’t exist        | `open('nofile.txt')`|

---

## 10. What are Python’s built-in functions?

**Explanation:**  
Python provides many built-in functions for type conversion, math, sequence operations, introspection, and more.

**Examples:**
```python
# Type conversion
int("10"), float("3.14"), str(123)
# Math
abs(-5), max(1, 2, 3), sum([1,2,3])
# Iterables
len("hello"), sorted([3,2,1]), list(zip([1,2],[3,4]))
# Introspection
type(42), isinstance(42, int), dir(list)
```

---

## 11. Difference between lists and tuples

**Explanation:**

| Feature         | List                | Tuple                   |
|-----------------|---------------------|-------------------------|
| Syntax          | `[1, 2, 3]`         | `(1, 2, 3)`             |
| Mutability      | ✅ Mutable          | ❌ Immutable            |
| Methods         | Many (`append()`)   | Few (`count()`, `index()`)|
| Performance     | Slower              | Faster                  |
| Use Case        | Dynamic data        | Fixed, constant data    |
| Dict Key        | ❌ No               | ✅ Yes (if immutables)  |

**Example:**
```python
my_list = [1, 2, 3]
my_list.append(4)     # ✅ Works

my_tuple = (1, 2, 3)
# my_tuple.append(4)  # ❌ AttributeError
```
---

## 12. Comprehensions

**Explanation:**  
Comprehensions provide a syntactic way to construct sequences (lists, sets, dicts) from other iterables.

**Examples:**
```python
# List comprehension
squares = [x**2 for x in range(5)]
# Dict comprehension
d = {x: x**2 for x in range(5)}
# Set comprehension
s = {x % 2 for x in range(5)}
# Nested comprehension
matrix = [[i * j for j in range(3)] for i in range(3)]
```

---

## 13. Lambda, map, filter, reduce

**Explanation:**
- **lambda:** Small anonymous function.
- **map:** Applies a function to every item in an iterable.
- **filter:** Filters items based on a function returning True/False.
- **reduce:** Cumulatively applies a function to items in a sequence.

**Examples:**
```python
add = lambda x, y: x + y
list(map(str, [1,2,3]))  # ['1','2','3']
list(filter(lambda x: x%2==0, range(5)))  # [0,2,4]
from functools import reduce
reduce(lambda x, y: x+y, [1,2,3,4])  # 10
```

---

## 14. Modules and Packages

**Explanation:**
- **Module:** Any `.py` file containing Python definitions.
- **Package:** A directory with an `__init__.py` file and modules/sub-packages.
- **Importing:** Use `import module` or `from module import name`.

**Example:**
```
project/
  mymodule.py
  mypackage/
    __init__.py
    submodule.py
```
Usage:
```python
import mymodule
from mypackage import submodule
```

---

## 15. Virtual Environments & pip

**Explanation:**
- **Virtual environment:** Isolates project dependencies.
- **pip:** Python’s package installer.

**Example:**
```bash
python -m venv myenv
source myenv/bin/activate  # Linux/Mac
myenv\Scripts\activate     # Windows
pip install requests
```

---

## 16. File Handling & Context Managers

**Explanation:**
File operations are handled using the built-in `open()` function and context managers ensure proper resource management.

**Example:**
```python
with open('file.txt', 'r') as f:
    data = f.read()
with open('file.txt', 'w') as f:
    f.write("Hello")
```

---

## 17. OOP Concepts: Inheritance, Multiple Inheritance, MRO

**Explanation:**
- **Inheritance:** Classes can derive behavior and attributes from other classes.
- **Multiple Inheritance:** A class can inherit from multiple classes.
- **MRO (Method Resolution Order):** Defines the order in which base classes are searched when executing a method.

**Example:**
```python
class Animal: pass
class Dog(Animal): pass
class A: pass
class B: pass
class C(A, B): pass
print(C.mro())  # Shows method resolution order
```
**super():**
```python
class Parent:
    def foo(self): print("parent")
class Child(Parent):
    def foo(self):
        super().foo()
        print("child")
```

---

## 18. Custom Exceptions

**Explanation:**  
You can define custom exceptions by subclassing `Exception`.

**Example:**
```python
class MyError(Exception): pass
raise MyError("Something went wrong")
```

---

## 19. Regular Expressions

**Explanation:**  
The `re` module handles regular expressions for string matching and manipulation.

**Example:**
```python
import re
pattern = r"\bfoo\b"
text = "foo bar"
print(re.search(pattern, text))  # Match object if 'foo' is found
```

---

## 20. Useful Standard Libraries

- **datetime:** Work with dates and times.
- **collections:** Specialized container datatypes.
- **os, sys:** Interact with the operating system and interpreter.
- **json:** Parse and write JSON data.

**Example:**
```python
from datetime import datetime
now = datetime.now()
from collections import Counter
c = Counter("hello")
import os
print(os.getcwd())
import json
data = json.loads('{"a": 1}')
```

---

## 21. Unit Testing

**Explanation:**  
Python’s `unittest` module supports test automation, sharing of setup and shutdown code, aggregation of tests, and independence of the tests from the reporting framework.

**Example:**
```python
import unittest
class TestMath(unittest.TestCase):
    def test_add(self):
        self.assertEqual(1+1, 2)
if __name__ == '__main__':
    unittest.main()
```

---

## 22. Multithreading vs Multiprocessing

**Explanation:**
- **Multithreading:** Multiple threads run in the same process; suitable for I/O-bound tasks. Python’s Global Interpreter Lock (GIL) can limit CPU-bound multithreading.
- **Multiprocessing:** Multiple processes run in separate memory spaces; true parallelism for CPU-bound tasks.

**Examples:**
```python
import threading
def foo(): print("Thread")
t = threading.Thread(target=foo)
t.start()

from multiprocessing import Process
def bar(): print("Process")
p = Process(target=bar)
p.start()
```

---

## 23. Decorators (with Arguments, Advanced)

**Explanation:**
- **Decorator:** A function that modifies another function. Used for logging, access control, timing, etc.
- **Decorator with Arguments:** Decorator can accept arguments for customization.

**Examples:**
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result
    return wrapper

@my_decorator
def hello(name):
    print(f"Hello, {name}")

# Decorator with arguments
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def hi():
    print("Hi!")
```

---

## 24. Context Managers

**Explanation:**
Context managers allow you to allocate and release resources precisely when you want, using the `with` statement.

**Example:**
```python
class MyCtx:
    def __enter__(self):
        print("Enter")
        return self
    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Exit")

with MyCtx():
    print("Inside")
```

---

## 25. Type Hinting / Annotations

**Explanation:**
Type hints improve code readability and allow static analysis tools to catch bugs early.

**Example:**
```python
def add(x: int, y: int) -> int:
    return x + y
```

---

## 26. PEP8 and Coding Style

**Explanation:**
PEP8 is the official style guide for Python code. It promotes code readability and consistency.

**Tips:**
- Use 4 spaces per indentation level.
- Limit lines to 79 characters.
- Name variables descriptively.
- Use tools like `flake8`, `black`, `isort`, and `pylint` for style enforcement.

---

## 27. The `zip()` Function

**Explanation:**
Combines multiple iterables element-wise into tuples.

**Example:**
```python
names = ['Alice', 'Bob', 'Charlie']
scores = [85, 90, 78]
zipped = zip(names, scores)
print(list(zipped))  # [('Alice', 85), ('Bob', 90), ('Charlie', 78)]
```

---

## 28. Sorting a Dictionary by Values

**Explanation:**
Use the built-in `sorted()` function with a lambda for sorting by dictionary values.

**Example:**
```python
my_dict = {'apple': 3, 'banana': 1, 'cherry': 2}
sorted_dict = dict(sorted(my_dict.items(), key=lambda item: item[1]))
print(sorted_dict)  # {'banana': 1, 'cherry': 2, 'apple': 3}
```

---

## 29. Static Methods vs Class Methods vs Instance Methods

**Explanation:**
- **Instance Methods:** Default, operate on object instance.
- **Class Methods:** Operate on the class itself, not instance. Use `@classmethod` and `cls`.
- **Static Methods:** Behave like plain functions but reside in the class. Use `@staticmethod`.

| Feature                | Static Method (@staticmethod) | Class Method (@classmethod) | Instance Method |
|------------------------|------------------------------|----------------------------|----------------|
| Access `self`          | ❌ No                        | ❌ No                      | ✅ Yes         |
| Access `cls`           | ❌ No                        | ✅ Yes                     | ❌ No          |
| Modify Class Attrs     | ❌ No                        | ✅ Yes                     | ❌ No          |
| Modify Instance Attrs  | ❌ No                        | ❌ No                      | ✅ Yes         |

**Example:**
```python
class Employee:
    base_salary = 50000
    def __init__(self, name, age):
        self.name = name
        self.age = age
    @staticmethod
    def is_workday(day):
        return day.lower() not in ['saturday', 'sunday']
    @classmethod
    def set_base_salary(cls, new_salary):
        cls.base_salary = new_salary

print(Employee.is_workday('Monday'))  # True
Employee.set_base_salary(60000)
print(Employee.base_salary)           # 60000
```

---

## 30. Dunders (Magic Methods)

**Explanation:**
Special methods that start and end with double underscores (`__`). Used for object construction, representation, operator overloading, etc.

| Method        | Description                                      |
|---------------|--------------------------------------------------|
| `__init__`    | Constructor (object creation)                    |
| `__new__`     | Instance creation (rarely used)                  |
| `__del__`     | Destructor (object deletion)                     |
| `__repr__`    | Official string representation                   |
| `__str__`     | Human-readable string representation             |

**Example:**
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __str__(self):
        return f"{self.name} is {self.age} years old."
    def __repr__(self):
        return f"Person('{self.name}', '{self.age}')"

p = Person("John", 36)
print(str(p))
print(repr(p))
```

---

## 31. Iterators & Generators

**Explanation:**
- **Iterator:** An object with `__iter__()` and `__next__()` methods.
- **Generator:** A simpler way to create iterators using `yield`. Automatically handles state.

**Examples:**
```python
# Iterator example
class MyIterator:
    def __init__(self, numbers):
        self.numbers = numbers
        self.index = 0
    def __iter__(self):
        return self
    def __next__(self):
        if self.index >= len(self.numbers):
            raise StopIteration
        value = self.numbers[self.index]
        self.index += 1
        return value

nums = MyIterator([1, 2, 3, 4])
for num in nums:
    print(num)

# Generator example
def my_generator():
    yield 1
    yield 2
    yield 3

gen = my_generator()
for val in gen:
    print(val)
```

---

## 32. Frequently Used Python Interview Questions (Quick List)

1. What are the key features of Python?
2. Difference between Python 2 and Python 3?
3. What are Python’s built-in data types?
4. Mutable vs immutable types with examples.
5. Difference between shallow and deep copy.
6. How to swap two variables in Python?
7. Difference between `is` and `==` operators.
8. How to handle exceptions in Python?
9. How do you sort a dictionary by value?
10. What is a list comprehension? Give an example.
11. What are lambda functions? Use cases?
12. What is a decorator? How do you write one?
13. What are static, class, and instance methods?
14. Explain Python's memory management and garbage collection.
15. What are dunder (magic) methods? Example?
16. How do you create and use modules/packages?
17. How does Python’s GIL affect multithreading?
18. What is a generator? How is it different from an iterator?
19. How do you read/write files in Python?
20. How do you test code in Python?

---

*This cheatsheet is designed for quick review before interviews and covers both beginner and advanced Python concepts with code examples and detailed explanations!*