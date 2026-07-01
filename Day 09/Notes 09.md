# 🐍 Python Variables & Memory Management

---

# 📚 Table of Contents

- Introduction
- What is a Variable?
- Variables in C/C++
- Variables in Python
- Heap Memory
- Objects
- References
- How Python Creates Variables
- Memory Diagrams
- Variable Reassignment
- Immutable Objects
- Mutable Objects
- String Immutability
- Immutable vs Mutable Data Types
- Benefits of Immutability
- Garbage Blocks
- Garbage Collection
- Reference Counting
- `sys.getrefcount()`
- `id()` Function
- `is` Operator
- Integer Caching
- String & Boolean Caching
- Object Introspection
- Interview Questions
- Summary

---

# Introduction

Every programming language stores data somewhere inside the computer's memory.

Whenever we write

```python
a = 10
```

the computer must store the value `10` in memory.

Different programming languages use different techniques for storing and managing memory.

Languages like

- C
- C++
- Java

follow one memory management model.

Python follows a completely different object-based memory model.

Understanding this model is extremely important because it explains concepts like

- Variables
- Objects
- References
- Heap Memory
- Immutability
- Mutable Objects
- Garbage Collection
- Reference Counting
- id()
- is operator

Once you understand these concepts, Python becomes much easier.

---

# What is a Variable?

A variable is simply a name that allows us to access stored data.

Think of it as a label attached to some information.

Example

```python
age = 20
name = "Vinay"
marks = 95
```

Here,

- `age`
- `name`
- `marks`

are variable names.

Their purpose is to access values stored somewhere in memory.

While a program executes, variables may

- store data
- update data
- point to new data

---

# Variables in C / C++

Understanding C memory helps us appreciate why Python behaves differently.

Suppose we write

```c
int a = 42;
```

The compiler creates

- one variable named `a`
- one memory location
- stores value 42 directly inside that location

Memory

```
Address       Variable      Value

6000 --------> a ----------> 42
```

The variable itself contains the value.

---

## Another Variable

```c
int a = 42;
int b = 42;
```

Memory

```
Address

6000
+------+
| 42   |
+------+
   ^
   |
   a

7000
+------+
| 42   |
+------+
   ^
   |
   b
```

Notice something important.

Although both variables contain the same value,

```
42
```

there are

- two variables
- two memory locations
- two copies of 42

Each variable owns its own storage.

---

## Reassigning Value

```c
a = 43;
```

Memory becomes

```
Address

6000
+------+
| 43   |
+------+
   ^
   |
   a

7000
+------+
| 42   |
+------+
   ^
   |
   b
```

The original value is overwritten.

No new memory block is created.

---

# Variables in Python

Python behaves completely differently.

Suppose we write

```python
a = 42
```

Python does **NOT** create a variable that directly stores `42`.

Instead, Python creates two things.

## Step 1

Create an object.

```
Heap Memory

+------------+
| Integer 42 |
+------------+
```

This object stores the value.

---

## Step 2

Create a reference.

```
a
```

does not store

```
42
```

Instead it stores

```
Address of the object
```

Memory

```
Reference

a
|
|
v

Heap

+------------+
|     42     |
+------------+
```

---

# Important Rule

In Python,

> Variables do **NOT** store values.

They store

**references to objects.**

This is one of the biggest differences between Python and languages like C.

---

# What is an Object?

Everything in Python is an object.

Examples

```python
10

3.14

"Python"

True

[1,2,3]

{"name":"Vinay"}
```

All these values are objects.

Each object lives inside Heap Memory.

---

# Heap Memory

Heap Memory is a special memory area where Python stores objects.

Examples

```
Heap

+------------------+
| Integer Object   |
+------------------+

+------------------+
| String Object    |
+------------------+

+------------------+
| List Object      |
+------------------+
```

Objects remain inside heap until Python removes them.

---

# References

A reference is simply an address pointing to an object.

Suppose

```python
a = 42
```

Python internally behaves like

```
Reference

a
|
|
v

Heap

Address 8000

+--------+
|   42   |
+--------+
```

Notice carefully

The variable

```
a
```

does NOT contain

```
42
```

Instead it contains

```
8000
```

which is the object's address.

---

# Multiple Variables

```python
a = 42
b = 42
```

Does Python create

```
42
42
```

(two objects)?

No.

Python creates only ONE object.

Memory

```
Reference

a -----

        \
         \
          v

      +--------+
      |   42   |
      +--------+

          ^
         /
        /

b -----
```

Both references point to exactly the same object.

This is possible because integers are immutable.

Advantages

- Saves memory
- Faster execution
- Avoids duplicate objects
- Reduces memory usage

---

# Variable Reassignment

Suppose

```python
a = 42
b = 42

a = 43
```

Many beginners think

```
42

becomes

43
```

This is WRONG.

Python never modifies the existing integer object.

Instead

Step 1

Create a new object

```
43
```

Step 2

Move reference

```
a
```

towards the new object.

Memory

```
Before

a ----\
       \
        > 42

b ----/

After

a ------> 43

b ------> 42
```

Notice

The object

```
42
```

still exists because

```
b
```

is still referring to it.

Nothing is overwritten.

---

# Key Rule

Python changes

✅ References

NOT

❌ Objects

Objects remain unchanged.

References move.

This single idea explains most of Python's memory behaviour.

---

# Quick Comparison

| C/C++ | Python |
|--------|---------|
| Variable stores value | Variable stores reference |
| Values overwritten | New object created |
| Duplicate values create duplicate memory | Same value can reuse existing object |
| Variables own memory | Objects own memory |
| Manual-style memory model | Automatic object-based memory model |

---

# Check Your Understanding

### Example 1

```python
a = 10
```

Question:

- How many objects are created?

✅ Answer:

One integer object.

---

### Example 2

```python
a = 10
b = 10
```

Question:

How many objects?

✅ Answer

Only ONE integer object.

Two references point to it.

---

### Example 3

```python
a = 10
b = 10

a = 20
```

Question

Where does `b` point?

✅ Answer

`b` still points to

```
10
```

because integers are immutable.

---
