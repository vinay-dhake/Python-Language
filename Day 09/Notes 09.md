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
==============================================================================================================================================================
---

# Immutability in Python

One of the most important concepts in Python memory management is **Immutability**.

The word **Immutable** means:

> **Cannot be changed after creation.**

Once an immutable object is created, Python never modifies its internal value.

Instead, whenever a new value is assigned, Python creates a completely new object and updates the reference.

This behavior is responsible for Python's efficient memory management and object sharing.

---

## What is an Immutable Object?

Suppose we write

```python
a = 10
```

Python creates

```
Reference

a
|
v

Heap

+--------+
|   10   |
+--------+
```

Now suppose we execute

```python
a = 20
```

Python **does NOT** replace the value 10 with 20.

Instead it performs these steps:

### Step 1

Create a new object

```
Heap

+--------+
|   10   |
+--------+

+--------+
|   20   |
+--------+
```

### Step 2

Move reference `a`

```
Before

a -----> 10


After

a -----> 20

10
```

If no reference points to `10`, it eventually becomes a **Garbage Block** and is removed by Python.

---

# Why Doesn't Python Modify Objects?

Suppose

```python
a = 10
b = 10
```

Memory

```
        a
         \
          \
           v

      +--------+
      |   10   |
      +--------+
           ^
          /
         /

        b
```

Now execute

```python
a = 20
```

If Python modified the object directly,

```
10

↓

20
```

then **both**

```
a
```

and

```
b
```

would suddenly become

```
20
```

which would be completely wrong.

Instead Python creates a new object.

```
Before

a ----\
       \
        > 10

b ----/


After

a -----> 20

b -----> 10
```

Notice

Only **a** changed.

**b** remains completely safe.

This is the biggest benefit of immutable objects.

---

# Immutable Objects Never Change

Consider

```python
a = 100

b = a

a = 200
```

Memory

Initially

```
      a
       \
        \
         v

      +---------+
      |   100   |
      +---------+
          ^
         /
        /

      b
```

After

```python
a = 200
```

```
a ---------> 200

b --------->100
```

The object

```
100
```

still exists.

Python simply moved the reference.

---

# References are Mutable

A very important interview point.

People often say

> Variables are mutable.

Technically,

Variables in Python are **references**.

References can change.

Example

```python
a = 10
a = 20
a = 30
```

Here

Reference

```
a
```

changes three times.

```
a → 10

↓

a → 20

↓

a → 30
```

So,

**References are mutable.**

---

# Objects are Immutable

The objects

```
10

20

30
```

never changed.

Python simply created new ones.

Therefore

> Objects are immutable.

---

# Mutable vs Immutable

There is a huge difference between these two terms.

### Immutable Object

- Cannot change after creation.
- Any modification creates a new object.
- Safe to share between multiple variables.

Examples

```python
10

3.14

True

"Python"

(1,2,3)
```

---

### Mutable Object

A mutable object **can change** without creating another object.

Example

```python
numbers = [10,20,30]

numbers.append(40)
```

Python simply updates the same list.

No new list is created.

---

# Immutable Data Types

Python has several immutable built-in data types.

| Data Type | Immutable |
|------------|-----------|
| int | ✅ |
| float | ✅ |
| bool | ✅ |
| str | ✅ |
| tuple | ✅ |
| complex | ✅ |
| range | ✅ |
| frozenset | ✅ |
| bytes | ✅ |
| NoneType | ✅ |

---

# Mutable Data Types

These objects can be modified after creation.

| Data Type | Mutable |
|------------|----------|
| list | ✅ |
| dict | ✅ |
| set | ✅ |
| bytearray | ✅ |

---

# String Immutability

Strings are immutable.

Suppose

```python
city = "Bhopal"
```

Memory

```
city

|

v

+-------------+
|  "Bhopal"   |
+-------------+
```

Now try

```python
city[0] = "C"
```

Python immediately raises an error.

```
TypeError

'str' object does not support item assignment
```

Why?

Because Python never allows changing characters inside an existing string object.

---

# Valid String Assignment

Instead of modifying the object,

Python creates a completely new string.

```python
city = "Indore"
```

Memory

Initially

```
city

↓

"Bhopal"
```

After reassignment

```
city

↓

"Indore"


"Bhopal"
```

The object

```
"Bhopal"
```

remains unchanged.

Only the reference moves.

---

# Example

```python
city = "Bhopal"

print(city)
```

Output

```
Bhopal
```

Attempt

```python
city[0] = "C"
```

Output

```
TypeError:
'str' object does not support item assignment
```

Now

```python
city = "Indore"

print(city)
```

Output

```
Indore
```

Notice

Python never edited

```
Bhopal
```

It created another string object.

---

# Why is Immutability Useful?

One common question is

> If Python keeps creating new objects, won't memory be wasted?

The answer is **No.**

Immutability actually **reduces** memory usage.

Suppose

```python
a = 42
b = 42
```

If integers were mutable,

Python would need

```
42

42
```

(two objects)

Instead

```
        a
         \
          \
           v

      +--------+
      |   42   |
      +--------+
           ^
          /
         /

        b
```

Only **one** object exists.

Advantages

- Saves memory
- Faster execution
- Less object creation
- Better optimization
- Safe object sharing
- Reduced memory overhead

---

# Another Important Question

Consider

```python
a = 10

a = 20

a = 30
```

How many objects are created?

Answer

Three objects.

```
10

20

30
```

But finally

```
a
```

points only to

```
30
```

Question

What happens to

```
10

20
```

Do they remain forever?

No.

Python automatically removes them using **Garbage Collection** after they are no longer referenced.

This is the next important concept in Python memory management.

==============================================================================================================================================================
---

# Garbage Blocks

Now let's answer an important question.

Consider the following code:

```python
a = 10
a = 20
a = 30
```

Step by step, Python performs the following operations.

### Step 1

```python
a = 10
```

Memory

```
Reference

a
|
v

+--------+
|   10   |
+--------+
```

---

### Step 2

```python
a = 20
```

Python creates a new object.

```
a
|
v

+--------+
|   20   |
+--------+

+--------+
|   10   |
+--------+
```

Notice carefully.

No reference is pointing to

```
10
```

anymore.

The object still exists in memory but is no longer accessible.

---

### Step 3

```python
a = 30
```

Again Python creates another object.

```
a
|
v

+--------+
|   30   |
+--------+

+--------+
|   20   |
+--------+

+--------+
|   10   |
+--------+
```

Again,

both

```
10

20
```

have no references.

---

# What is a Garbage Block?

A **Garbage Block** is an object in memory that is **not referenced by any variable or object**.

Since nothing can access it anymore, it only occupies memory unnecessarily.

Definition

> A Garbage Block is an object whose reference count has become zero.

Example

```python
a = 10
a = 20
```

After execution

```
10
```

is a garbage block because nothing points to it.

---

# Live Object vs Garbage Block

### Live Object

A live object is still being used by the program.

Example

```python
name = "Python"
```

Memory

```
name
|
v

+-------------+
|  "Python"   |
+-------------+
```

The object is still useful.

Hence,

✅ Live Object

---

### Garbage Block

Example

```python
name = "Python"

name = "Java"
```

Memory

```
name

↓

"Java"




"Python"
```

Nobody refers to

```
"Python"
```

Therefore,

❌ Garbage Block

---

# What is Garbage Collection?

Imagine you clean your study table every day.

Old notebooks,

unused papers,

broken pens,

all are removed.

Python performs the same task inside memory.

This cleaning process is called

## Garbage Collection (GC)

Definition

> Garbage Collection is the automatic process of removing unused objects from memory.

Python performs this automatically.

The programmer never has to manually free memory.

---

# Why Garbage Collection?

Suppose a program creates millions of objects.

```
10

20

30

40

50

...
```

If unused objects stayed forever,

RAM would eventually become full.

Programs would slow down.

Memory leaks would occur.

Therefore Python continuously removes unused objects.

---

# Python Garbage Collector

Python has a built-in component called the

**Garbage Collector (GC)**

Its responsibilities are

- Find unused objects
- Detect garbage blocks
- Release memory
- Return memory back to Python

This process happens automatically.

Programmers don't need to call it manually in normal situations.

---

# Reference Counting

Python uses a technique called

## Reference Counting

Every object stores a count indicating

> How many references currently point to this object.

This number is called the

**Reference Count (RC)**

---

# Why Reference Count?

Python needs to know

whether an object is still useful.

The easiest way is

```
Count references
```

If the count becomes

```
0
```

then nobody can access the object.

Hence it is garbage.

---

# Internal Structure of an Object

A Python object contains much more than its actual value.

Simplified representation

```
+---------------------------+
| Actual Value              |
+---------------------------+
| Data Type Information     |
+---------------------------+
| Reference Count           |
+---------------------------+
| Other Internal Metadata   |
+---------------------------+
```

For example,

an integer object stores

- integer value
- object type
- reference count
- internal metadata used by Python

This is one reason why a Python integer occupies much more memory than a raw integer in C.

---

# Example of Reference Counting

Consider

```python
a = 10
```

Memory

```
       a
       |
       v

+--------------+
| Value : 10   |
| RC = 1       |
+--------------+
```

Reference Count = **1**

---

Now execute

```python
b = 10
```

Memory

```
      a
       \
        \
         v

+--------------+
| Value : 10   |
| RC = 2       |
+--------------+
         ^
        /
       /

      b
```

Reference Count becomes

```
2
```

because

```
a

b
```

both point to the same object.

---

Now execute

```python
a = 20
```

Memory

```
a ---------->20




b ---------->10
```

Reference Count of

```
10
```

becomes

```
1
```

because only

```
b
```

is referring to it.

---

Finally

```python
b = 20
```

Memory

```
      a
       \
        \
         v

+--------------+
| Value : 20   |
| RC = 2       |
+--------------+
```

The object

```
10
```

has

```
Reference Count = 0
```

Therefore

Python immediately marks it as garbage.

---

# Complete Reference Counting Lifecycle

```python
a = 10
```

RC of 10

```
1
```

---

```python
b = 10
```

RC

```
2
```

---

```python
a = 20
```

RC

```
1
```

---

```python
b = 20
```

RC

```
0
```

Result

```
Object 10 becomes Garbage Block.
```

Python removes it from memory.

---

# Another Example

```python
a = 10
a = 20
a = 30
```

Execution

After first line

```
10

RC = 1
```

---

Second line

```
10

RC = 0

↓

Garbage
```

New object

```
20

RC = 1
```

---

Third line

```
20

RC = 0

↓

Garbage
```

New object

```
30

RC = 1
```

Only

```
30
```

remains alive.

---

# Advantages of Reference Counting

✅ Automatic memory management

✅ No manual deletion

✅ Prevents memory leaks

✅ Keeps memory clean

✅ Makes programming easier

✅ Frees unused memory automatically

---

# Disadvantages of Reference Counting

Nothing comes free.

Python constantly checks the reference count of every object.

Whenever a reference changes,

Python updates the count.

This continuous monitoring consumes CPU time.

Therefore,

Python is generally slower than languages like C and C++ in raw execution speed.

---

# Can We See the Reference Count?

Yes.

Python provides

```python
sys.getrefcount()
```

First import the module.

```python
import sys
```

Example

```python
import sys

a = 10

print(sys.getrefcount(a))
```

Output

```
(Depends on the Python implementation)
```

The value is usually **one greater than expected**.

---

# Why Does `getrefcount()` Show One Extra?

Consider

```python
import sys

a = 10

print(sys.getrefcount(a))
```

When Python executes

```python
sys.getrefcount(a)
```

the object `a` is temporarily passed as an argument to the function.

That temporary function argument is itself another reference.

Therefore,

Actual RC

```
1
```

Displayed RC

```
2
```

General Rule

> `sys.getrefcount()` always returns one more than the actual reference count because the function itself temporarily references the object.

=============================================================================================================================================================

---

# How Can We Prove Python Creates Only One Object?

Consider the following code.

```python
a = 42
b = 42
```

We already know that Python creates **only one integer object**, and both variables point to that same object.

But how can we prove it?

Python provides two ways:

1. `id()` function
2. `is` operator

Both are commonly asked in interviews.

---

# The `id()` Function

`id()` is a built-in Python function that returns the **identity** of an object.

In CPython (the most common Python implementation), this identity is the object's memory address.

## Syntax

```python
id(object)
```

---

## Example 1

```python
a = 42

print(id(a))
```

Output

```text
140733924593232
```

*(Your output will be different because memory addresses vary.)*

The returned number uniquely identifies the object during its lifetime.

---

## Example 2

```python
a = 42
b = 42

print(id(a))
print(id(b))
```

Possible Output

```text
140733924593232
140733924593232
```

Both IDs are identical.

Therefore,

```
a

and

b
```

refer to the **same object**.

---

## Example 3

```python
a = 42
b = 42

print(id(a) == id(b))
```

Output

```python
True
```

Meaning

Both references point to the same object.

---

# Reassignment Example

```python
a = 42

print(id(a))

a = 100

print(id(a))
```

Possible Output

```text
140733924593232
140733924595184
```

Notice

The ID changes.

This proves Python did **not** modify the original object.

Instead,

- a new object was created.
- `a` now points to the new object.

---

# Important Note

Never assume that the numeric value returned by `id()` is the same on every computer or every execution.

The only important thing is:

- Same ID → Same object
- Different ID → Different object

---

# The `is` Operator

Python provides another way to check object identity.

The `is` operator compares whether **two references point to the exact same object**.

It does **not** compare values.

## Syntax

```python
a is b
```

Returns

- `True` → both variables refer to the same object.
- `False` → different objects.

---

# `is` vs `==`

Many beginners confuse these two operators.

## `==`

Checks whether **values** are equal.

```python
a = [1,2,3]
b = [1,2,3]

print(a == b)
```

Output

```python
True
```

Because both lists contain the same values.

---

## `is`

Checks whether they are the **same object**.

```python
a = [1,2,3]
b = [1,2,3]

print(a is b)
```

Output

```python
False
```

Because Python created two separate list objects.

---

## Comparison Table

| Operator | Checks |
|-----------|--------|
| `==` | Value equality |
| `is` | Object identity |

---

# Example

```python
a = 42
b = 42

print(a is b)
```

Output

```python
True
```

Explanation

Both variables point to the same integer object.

---

# Another Example

```python
a = "Python"
b = "Python"

print(a is b)
```

Output

```python
True
```

Because Python reuses many string objects.

---

# Integer Caching

Now comes a very interesting concept.

Look at this code.

```python
a = 256
b = 256

print(a is b)
```

Output

```python
True
```

Now change only one value.

```python
a = 257
b = 257

print(a is b)
```

Output

```python
False
```

Why?

Both values are the same.

Why did Python suddenly create two objects?

The answer is **Integer Caching**.

---

# What is Integer Caching?

Python internally stores some commonly used integers in a special cache.

Instead of creating new objects repeatedly, Python simply reuses the existing cached object.

This improves

- performance
- memory efficiency
- execution speed

---

# Cached Integer Range

In CPython,

the following integers are cached.

```
-5

to

256
```

Therefore,

all integers in this range are reused.

---

## Example

```python
a = 100
b = 100

print(a is b)
```

Output

```python
True
```

Because

```
100
```

is inside the cached range.

---

## Example

```python
a = -5
b = -5

print(a is b)
```

Output

```python
True
```

Again,

Python uses the cached object.

---

## Example

```python
a = -6
b = -6

print(a is b)
```

Output

```python
False
```

Because

```
-6
```

is outside the cached range.

---

## Example

```python
a = 256
b = 256

print(a is b)
```

Output

```python
True
```

---

## Example

```python
a = 257
b = 257

print(a is b)
```

Output

```python
False
```

Python creates two different integer objects.

---

# Why Does Python Cache Small Integers?

Imagine writing programs containing

```python
0
1
2
3
4
5
```

These numbers are used constantly.

Creating millions of identical integer objects would waste

- memory
- CPU time

Instead,

Python creates them once and reuses them.

Benefits

- Faster execution
- Less memory allocation
- Less garbage collection
- Better performance

---

# Why Specifically -5 to 256?

These numbers are extremely common in programs.

Examples include:

- loop counters
- indexing
- slicing
- Boolean calculations
- arithmetic operations
- array positions
- character codes

Caching these values significantly reduces memory churn.

---

# Important Note About Integer Caching

Integer caching is an **implementation detail of CPython**.

Although it is commonly observed, you should **not write program logic that depends on it**.

Use `==` to compare values and `is` only when you intentionally want to check object identity.

============================================================================================================================================================
---

# String & Boolean Caching

The concept of object reuse is not limited to integers.

Python also reuses certain immutable objects like **strings** and **Boolean values**.

This improves memory efficiency and reduces unnecessary object creation.

---

## String Caching

Consider the following code.

```python
a = "Bhopal"
b = "Bhopal"

print(a is b)
```

Output

```python
True
```

Explanation

Python reuses the same string object.

Memory

```
        a
         \
          \
           v

+----------------+
|   "Bhopal"     |
+----------------+
           ^
          /
         /

        b
```

Only one string object exists.

---

## Boolean Caching

Python has only two Boolean objects.

```
True

False
```

Whenever you write

```python
a = False
b = False

print(a is b)
```

Output

```python
True
```

Both references point to the same Boolean object.

The same applies to

```python
a = True
b = True

print(a is b)
```

Output

```python
True
```

---

# Float Objects

Now consider

```python
a = 1.0
b = 1.0

print(a is b)
```

Output

```python
False
```

Unlike integers,

Python generally **does not cache float objects**.

Even though the values are equal,

different float objects are usually created.

Memory

```
a -------> 1.0

b -------> 1.0
```

Two different objects.

---

# Complex Numbers

Example

```python
a = (2+3j)
b = (2+3j)

print(a is b)
```

Output

```python
False
```

Complex objects are generally **not reused**.

Each assignment creates a separate object.

---

# Summary of Object Reuse

| Data Type | Object Reuse |
|------------|--------------|
| Small Integers (-5 to 256) | ✅ Yes |
| Strings | ✅ Yes (commonly) |
| Boolean | ✅ Yes |
| Float | ❌ No |
| Complex | ❌ No |

> **Note:** Object reuse depends on Python's implementation (such as CPython). Do not write code that depends on these optimizations.

---

# Object Introspection

Python provides several built-in functions and modules to inspect objects.

This process is called **Object Introspection**.

It allows us to obtain information about an object's identity, type, memory usage, methods, attributes, and reference relationships.

---

## `type()`

Returns the type (class) of an object.

Example

```python
a = [10, 20, 30]

print(type(a))
```

Output

```python
<class 'list'>
```

---

## `id()`

Returns the unique identity of an object.

Example

```python
name = "Python"

print(id(name))
```

Output

```text
140621234567824
```

(The exact value depends on your system.)

---

## `sys.getsizeof()`

Returns the memory occupied by an object (in bytes).

Example

```python
import sys

a = 10

print(sys.getsizeof(a))
```

Possible Output

```python
28
```

Notice that an integer occupies more than 4 bytes because Python stores additional metadata like type information and reference count.

---

## `dir()`

Returns all attributes and methods available for an object.

Example

```python
name = "Python"

print(dir(name))
```

Sample Output (shortened)

```python
['capitalize',
 'casefold',
 'center',
 'count',
 'endswith',
 'find',
 'index',
 'isalnum',
 'isalpha',
 'join',
 'lower',
 'replace',
 'split',
 'strip',
 'upper']
```

This is useful for discovering available methods.

---

## `help()`

Displays documentation for an object.

Example

```python
help(str)
```

or

```python
help(list)
```

Python displays detailed documentation including available methods and descriptions.

---

## `inspect.getmembers()`

The `inspect` module can list all members of an object.

Example

```python
import inspect

print(inspect.getmembers(str))
```

This returns methods, properties, and other members associated with the object.

---

## `__dict__`

User-defined objects store their instance attributes inside a dictionary called `__dict__`.

Example

```python
class Person:
    def __init__(self):
        self.name = "Alice"
        self.age = 25

p = Person()

print(p.__dict__)
```

Output

```python
{
 'name': 'Alice',
 'age': 25
}
```

---

## `gc.get_referents()`

Returns the objects directly referred to by another object.

Example

```python
import gc

a = [1, 2, 3]

print(gc.get_referents(a))
```

---

## `gc.get_referrers()`

Returns objects that currently refer to the given object.

Example

```python
import gc

a = [1, 2, 3]

print(gc.get_referrers(a))
```

This function is mainly used for debugging and memory analysis.

---

# Object Introspection Summary

| What You Want | Function |
|---------------|----------|
| Object identity | `id(obj)` |
| Object type | `type(obj)` |
| Memory size | `sys.getsizeof(obj)` |
| Reference count | `sys.getrefcount(obj)` |
| Methods & attributes | `dir(obj)` |
| Documentation | `help(obj)` |
| All members | `inspect.getmembers(obj)` |
| Instance attributes | `obj.__dict__` |
| Referenced objects | `gc.get_referents(obj)` |
| Referring objects | `gc.get_referrers(obj)` |

---

# Best Practices

- Use `==` when comparing values.
- Use `is` only when checking object identity.
- Do not rely on integer or string caching in program logic.
- Remember that variables in Python are references, not containers of values.
- Understand the difference between mutable and immutable objects.
- Avoid unnecessary object creation where possible.
- Trust Python's automatic garbage collector instead of manually managing memory.

---

# Interview Questions

### 1. What is a variable in Python?

A variable is a **reference** that points to an object stored in memory.

---

### 2. Where are Python objects stored?

In the **Heap Memory**.

---

### 3. What does a Python variable actually store?

It stores the **reference (address)** of an object, not the object itself.

---

### 4. What is Immutability?

An immutable object cannot be modified after it is created.

---

### 5. Name some immutable data types.

- int
- float
- bool
- str
- tuple
- complex
- range
- frozenset
- bytes
- NoneType

---

### 6. Name some mutable data types.

- list
- dict
- set
- bytearray

---

### 7. What is a Garbage Block?

An object with **Reference Count = 0**.

---

### 8. What is Garbage Collection?

The automatic process of removing unused objects from memory.

---

### 9. What is Reference Counting?

A mechanism that tracks how many references point to an object.

---

### 10. What does `id()` return?

The identity (memory address in CPython) of an object.

---

### 11. What does `is` check?

Whether two references point to the same object.

---

### 12. Difference between `==` and `is`?

- `==` compares values.
- `is` compares object identity.

---

### 13. Why does Python cache integers?

To improve performance and reduce memory allocation for frequently used values.

---

### 14. What integer range is cached in CPython?

```
-5 to 256
```

---

# Quick Revision

- Variables store references.
- Objects live in Heap Memory.
- Immutable objects never change.
- Mutable objects can change.
- References can change.
- Objects cannot (if immutable).
- Python automatically removes garbage blocks.
- Reference Count decides whether an object is still alive.
- `id()` returns object identity.
- `is` checks object identity.
- `==` checks value equality.
- Small integers, strings, and Booleans are commonly reused.
- Float and complex objects are generally not cached.

---

# Conclusion

Python follows an **object-oriented memory model** in which every value is an object and every variable is a reference to that object. This design enables automatic memory management, efficient object sharing, and safer programming through immutability. Features such as reference counting, garbage collection, object reuse, and introspection make Python both powerful and developer-friendly, allowing programmers to focus on solving problems instead of managing memory manually.
