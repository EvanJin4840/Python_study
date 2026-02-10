# Python Key Concepts Guide

A quick reference for Python essentials, coming from C/C++/Java background.

## Dynamic Typing

| Feature | C/C++/Java | Python |
|---------|------------|--------|
| Variable Declaration | `int x = 5;` | `x = 5` |
| Type Declaration | Required | Optional (inferred at runtime) |
| Type Annotations | Not available (except C++11+) | Supported from Python 3.5+ |

**Example:**
```python
x = 5          # Integer
name = "John"  # String
price = 9.99   # Float
```
* Type annotations (also called "type hints") are a Python feature that let you explicitly specify the expected data types of variables, function parameters, and return values. They were introduced in Python 3.5 (PEP 484) to bring optional static typing to Python's dynamically typed nature.

#### Iterators and Generators

- Iterators are objects that can be looped over, implementing __iter__() and __next__() methods. Generators use the yield keyword to produce values on-demand, making them memory-efficient for large datasets:
- Generators are useful when processing large files or infinite sequences without loading everything into memory.

### Decorators

- A decorator is a higher‑order function that takes another function as input, wraps it inside an inner function (often called wrapper) where it can run extra code before and/or after the original function call, and then returns this wrapper as the new version of the function.
- Using the @decorator_name syntax above a function definition is just shorthand for “pass this function into the decorator and replace it with the decorated version.”
This lets you add reusable cross‑cutting features like logging, timing, authentication checks, caching, or validation to many functions, without changing their original bodies and while keeping their core logic clean.

### context managers

- A context manager is a Python object that manages resources (files, database connections, locks, etc.) by automatically handling setup and cleanup around a block of code. You use it with the with statement, and it guarantees that cleanup code runs even if the block raises an exception or exits early.

- Internally, context managers implement __enter__ (runs when entering the block) and __exit__ (runs when leaving the block, regardless of how). This abstracts the try...finally pattern for resource management.

Key difference from decorators:
- Decorators modify or replace a function/class at definition time
- Context managers execute setup/teardown code around a runtime block

* Creating context managers easily:
- Instead of writing a class with __enter__/__exit__, you can use the @contextmanager decorator from contextlib on a generator function that yields exactly once
from contextlib import contextmanager

``` @contextmanager
def my_resource():
    print("acquire")    # before yield = __enter__
    yield              # with block runs here
    print("release")   # after yield = __exit__

with my_resource():
    print("using resource")
```
Everything before yield acts as __enter__, and everything after acts as __exit__. Context managers created this way can also be used as function decorators.

### Metaclasses

- A metaclass is a "class of a class" - it defines how classes are created, just as a class defines how objects are created. The relationship is:

``Metaclass creates → Class creates → Object``

- By default, all Python classes are instances of the built-in type metaclass. You can create custom metaclasses by inheriting from type and overriding methods like __new__ (runs when the class is being created) or __init__ (runs after class creation):


``` python
class MyMeta(type):
    def __new__(cls, name, bases, attrs):
        print(f"Creating class: {name}")
        attrs['injected'] = 42  # Add attribute to every class
        return super().__new__(cls, name, bases, attrs)
class MyClass(metaclass=MyMeta):
    pass
print(MyClass.injected)  # 42
```

* Common use cases:
- Singleton patterns
- Abstract base classes (ABC)
- ORM frameworks (Django models, SQLAlchemy)
- Automatic code generation (like dataclasses)
- Enforcing coding standards or conventions

* Important caveat: Metaclasses are advanced magic that 99% of developers don't need. If you're wondering whether you need a metaclass, you probably don't - decorators or class decorators usually suffice. Metaclasses are primarily used in frameworks and libraries, not application code.

* Multithreading runs multiple threads within a single process that share the same memory space. Due to Python's Global Interpreter Lock (GIL), only one thread executes at a time, providing concurrency but not true parallelism. It's ideal for I/O-bound tasks (file operations, network requests, database queries) where threads can work on other tasks while waiting.

* Multiprocessing creates separate processes, each with its own Python interpreter and memory space. This bypasses the GIL and enables true parallelism across multiple CPU cores. It's best for CPU-bound tasks (heavy computations, data processing, image/video processing) but has higher overhead due to process creation and memory duplication.

### Multithreading and Multiprocessing

* Quick decision guide:

- I/O-bound (waiting for external resources) → Use multithreading
- CPU-bound (intensive calculations) → Use multiprocessing

### Dunder Methods

Dunder methods (double underscore methods) are special predefined methods with names starting and ending with __ that define how custom objects interact with Python's built-in operations and functions. They're also called "magic methods".

* Key categories:
- Initialization & representation: __init__ (constructor), __str__ (user-friendly string), __repr__ (developer-friendly representation)
- Operator overloading: __add__ (+), __sub__ (-), __mul__ (*), __eq__ (==), __lt__ (<) let your objects work with arithmetic and comparison operators
- Container behavior: __len__ (len()), __getitem__ (indexing obj[i]), __contains__ (in operator) make objects behave like lists/dicts
- Callable objects: __call__ makes instances callable like functions

### Generators and yield
A generator is a function that uses yield to return values one at a time instead of building a full list in memory. This is great for large datasets or infinite sequences.
```python
Example:
def count_up():
    n = 0
    while True:
        yield n
        n += 1
```
### Comprehensions (list, dict, set)
A concise way to create collections using a loop‑like syntax in one line.
```python
Examples:
squares = [x**2 for x in range(10)]
pairs = {x: x**2 for x in range(5)}
evens = {x for x in range(10) if x % 2 == 0}```