---
title: "Python Fundamentals for Interviews"
tags: ["languages","python","backend"]
difficulty: medium
status: learning
last_reviewed: 2026-10-02
---

# Python Fundamentals

## 1. Core Language Features

### List Comprehensions & Generators
Python provides concise ways to create collections and iterate over data.
- **List Comprehension**: Creates a list in memory. `[x**2 for x in range(10)]`
- **Generator Expression**: Returns an iterator; computes values on-the-fly (lazy evaluation). `(x**2 for x in range(10))` $\rightarrow$ saves memory for large datasets.

### Decorators
A decorator is a function that takes another function and extends its behavior without explicitly modifying it.
```python
def debug(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with {args}")
        return func(*args, **kwargs)
    return wrapper

@debug
def add(a, b):
    return a + b
```

### Dunder Methods (Magic Methods)
Methods starting and ending with `__` that allow you to define how objects behave with built-in operations.
- `__init__`: Constructor.
- `__str__` / `__repr__`: String representation.
- `__len__`: Enables `len(obj)`.
- `__getitem__`: Enables indexing `obj[i]`.

## 2. Advanced Concepts

### The Global Interpreter Lock (GIL)
The GIL is a mutex that allows only one thread to hold control of the Python interpreter.
- **Impact**: Multi-threading in Python does not provide true parallelism for CPU-bound tasks.
- **Solution**: 
    - Use `multiprocessing` module for CPU-bound tasks (spawns separate interpreters).
    - Use `asyncio` or `threading` for I/O-bound tasks.

### Asyncio & Concurrency
Python uses `async`/`await` for single-threaded concurrent code.
```python
import asyncio

async def fetch_data():
    print("Start fetching")
    await asyncio.sleep(1) # Non-blocking I/O
    print("Done fetching")

asyncio.run(fetch_data())
```

### Memory Management
- **Reference Counting**: Primary mechanism; objects are deleted when count hits zero.
- **Garbage Collection (GC)**: Handles reference cycles using a generational collector.

## 3. Interview Complexity & Pitfalls

| Feature | Time Complexity | Space Complexity | Note |
| :--- | :--- | :--- | :--- |
| `list.append()` | $O(1)$ amortized | $O(1)$ | |
| `list.insert(0, x)`| $O(n)$ | $O(1)$ | Shifting all elements |
| `dict` lookup | $O(1)$ | $O(n)$ | Hash map |
| `set` lookup | $O(1)$ | $O(n)$ | Hash set |
| `sorted()` | $O(n \log n)$ | $O(n)$ | Timsort |

**Common Pitfall: Mutable Default Arguments**
```python
def add_item(item, my_list=[]): # WRONG: list is created once at definition
    my_list.append(item)
    return my_list

# Fix: Use None as default
def add_item_fixed(item, my_list=None):
    if my_list is None: my_list = []
    my_list.append(item)
    return my_list
```

## Related notes

- [Complexity Cheat Sheet](01-dsa/complexity-cheat-sheet.md)
- [Agentic AI](09-agentic-ai/llm-basics.md)
