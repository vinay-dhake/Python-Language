# 🐍 Data Types, Number Systems, Base Conversion & Type Checking

This section covers Python's built-in data types, object identity, number systems, base conversion functions, and common TypeErrors encountered while working with binary, octal, and hexadecimal representations.

---

# 1️⃣ Introduction to Data Types

In Python, assigning a value automatically assigns a data type.

Python is a **dynamically typed language**, meaning variables do not require explicit type declarations.

---

## The `type()` Function

The `type()` function returns the class of an object.

### Example

```python
x = 25

print(type(x))
```

Output:

```text
<class 'int'>
```

---

## The `id()` Function

Every object in Python possesses a unique identifier.

The `id()` function returns the memory address (object identity) of that object.

### Example

```python
x = 25

print(id(x))
```

Output:

```text
140733522204520
```

> The exact value may differ from system to system.

---

# 2️⃣ Number Systems

Python supports four number systems.

| Number System | Base | Allowed Symbols | Prefix       |
| ------------- | ---- | --------------- | ------------ |
| Binary        | 2    | 0, 1            | `0b` or `0B` |
| Octal         | 8    | 0–7             | `0o` or `0O` |
| Decimal       | 10   | 0–9             | None         |
| Hexadecimal   | 16   | 0–9, A-F or a-f | `0x` or `0X` |

---

## Binary Numbers

Uses only:

```text
0 and 1
```

Example:

```python
binary_val = 0b1101

print(binary_val)
```

Output:

```text
13
```

---

## Octal Numbers

Uses digits:

```text
0 1 2 3 4 5 6 7
```

Example:

```python
octal_val = 0o31

print(octal_val)
```

Output:

```text
25
```

---

## Hexadecimal Numbers

Uses:

```text
0 1 2 3 4 5 6 7 8 9
A B C D E F
```

or

```text
a b c d e f
```

Example:

```python
hex_val = 0x19

print(hex_val)
```

Output:

```text
25
```

---

# 3️⃣ Base Conversion Functions

Python provides built-in functions for converting decimal integers into various number systems.

---

## `bin()`

Converts an integer to binary.

```python
num = 25

print(bin(num))
```

Output:

```text
0b11001
```

---

## `oct()`

Converts an integer to octal.

```python
print(oct(num))
```

Output:

```text
0o31
```

---

## `hex()`

Converts an integer to hexadecimal.

```python
print(hex(num))
```

Output:

```text
0x19
```

---

# Example

```python
num = 25

print(bin(num))
print(oct(num))
print(hex(num))
```

Output:

```text
0b11001
0o31
0x19
```

---

# Re-evaluating Number Literals

Python internally converts literals into integers before processing.

### Example

```python
print(bin(0b1101))
```

Output:

```text
0b1101
```

---

```python
print(bin(0o31))
```

Output:

```text
0b11001
```

---

```python
print(hex(0b1101))
```

Output:

```text
0xd
```

---

# 4️⃣ Common TypeErrors

---

## Case 1: Passing a String to `bin()`

Incorrect:

```python
print(bin("Sachin"))
```

Output:

```text
TypeError: 'str' object cannot be interpreted as an integer
```

### Why?

The `bin()` function expects an integer.

Strings cannot be converted directly into binary using `bin()`.

---

## Case 2: Using `bin()` on Floating Point Numbers

```python
a = 1.2

print(type(a))
```

Output:

```text
<class 'float'>
```

Trying:

```python
print(bin(a))
```

Results in:

```text
TypeError: 'float' object cannot be interpreted as an integer
```

---

### Why?

Binary, octal, and hexadecimal conversion functions operate only on integers.

Floating-point numbers follow IEEE-754 representation and are not directly supported by these functions.

---

# 5️⃣ Object Verification Techniques

Before performing operations, we can verify the object's type.

---

## Example

```python
val = 35.4

print(id(val))

if type(val) == int:
    print(bin(val))
else:
    print(f"Cannot convert {type(val)} objects directly using bin()")
```

Output:

```text
Cannot convert <class 'float'> objects directly using bin()
```

---

# Using `isinstance()`

A better approach is:

```python
val = 35

if isinstance(val, int):
    print(bin(val))
```

Output:

```text
0b100011
```

---

# Quick Summary Table

| Expression            | Output          |
| --------------------- | --------------- |
| `bin(25)`             | `0b11001`       |
| `oct(25)`             | `0o31`          |
| `hex(25)`             | `0x19`          |
| `bin(0o31)`           | `0b11001`       |
| `hex(0b1101)`         | `0xd`           |
| `bin("Sachin")`       | TypeError       |
| `bin(1.2)`            | TypeError       |
| `type(25)`            | `<class 'int'>` |
| `id(25)`              | Memory Address  |
| `isinstance(25, int)` | `True`          |

---

# 🎯 Key Takeaways

* Python assigns data types automatically.
* `type()` returns the class of an object.
* `id()` returns the object's unique identity (memory address).
* Python supports Binary, Octal, Decimal, and Hexadecimal number systems.
* Binary literals use the prefix `0b`.
* Octal literals use the prefix `0o`.
* Hexadecimal literals use the prefix `0x`.
* `bin()`, `oct()`, and `hex()` operate only on integers.
* Passing strings or floats to these functions raises a `TypeError`.
* Type checking can be performed using `type()` or `isinstance()`.
* Every value in Python is an object.
==============================================================================================================
# 🐍 Python Lecture Notes: Strings, Slicing, Boolean Arithmetic & Type Mechanics

This document covers string indexing, slicing, immutability, Boolean arithmetic, and Python's internal type behavior.

---

# 1️⃣ String Indexing

A string in Python is an **ordered and immutable sequence of characters**.

Python supports two types of indexing:

* Positive Indexing (Left → Right)
* Negative Indexing (Right → Left)

---

## Example

```python
name = "Sachin"
```

### Index Layout

| Character      | S  | a  | c  | h  | i  | n  |
| -------------- | -- | -- | -- | -- | -- | -- |
| Positive Index | 0  | 1  | 2  | 3  | 4  | 5  |
| Negative Index | -6 | -5 | -4 | -3 | -2 | -1 |

---

## Positive Indexing

```python
name = "Sachin"

print(name[0])
print(name[3])
```

Output

```text
S
h
```

---

## Negative Indexing

```python
print(name[-1])
print(name[-4])
```

Output

```text
n
c
```

---

## IndexError

Accessing an invalid index raises:

```python
name[6]
```

Output

```text
IndexError: string index out of range
```

---

# 2️⃣ String Slicing

Slicing extracts a portion of a string.

## Syntax

```python
string[start:end]
```

* Start index → Inclusive
* End index → Exclusive

---

## Example

```python
msg = "PythonProgramming"

print(msg[0:6])
print(msg[6:10])
```

Output

```text
Python
Prog
```

---

# Default Values

---

### Omitting Start Index

```python
msg = "Python"

print(msg[:4])
```

Output

```text
Pyth
```

---

### Omitting End Index

```python
print(msg[2:])
```

Output

```text
thon
```

---

### Copy Entire String

```python
print(msg[:])
```

Output

```text
Python
```

---

# 3️⃣ Slicing with Step

## Syntax

```python
string[start:end:step]
```

By default:

```python
step = 1
```

---

## Positive Step

```python
numbers = "0123456789"

print(numbers[0:10:2])
print(numbers[::3])
```

Output

```text
02468
0369
```

---

## Negative Step

Negative step traverses from right to left.

### Reverse String

```python
numbers = "0123456789"

print(numbers[::-1])
```

Output

```text
9876543210
```

---

### Backward Slicing

```python
print(numbers[7:2:-1])
```

Output

```text
76543
```

---

## Impossible Slice

```python
numbers[2:7:-1]
```

Output

```text
''
```

Python simply returns an empty string instead of raising an error.

---

# 4️⃣ String Immutability

Strings are immutable.

Characters can be read but cannot be modified.

---

## Invalid Operation

```python
name = "Sachin"

name[0] = "K"
```

Output

```text
TypeError:
'str' object does not support item assignment
```

---

## Important Fact

Slicing never changes the original string.

It creates a completely new string object in memory.

---

# 5️⃣ Boolean Arithmetic

In Python:

```python
bool ⊂ int
```

Boolean is a subclass of integer.

---

## Internal Representation

| Boolean Value | Integer Equivalent |
| ------------- | ------------------ |
| True          | 1                  |
| False         | 0                  |

---

# Addition

### True + True

```python
result = True + True

print(result)
print(type(result))
```

Output

```text
2
<class 'int'>
```

---

### True + False

```python
print(True + False)
```

Output

```text
1
```

---

### False + False

```python
print(False + False)
```

Output

```text
0
```

---

# Subtraction

```python
print(True - False)
print(False - True)
```

Output

```text
1
-1
```

---

# Multiplication

```python
print(True * True)
print(True * False)
```

Output

```text
1
0
```

---

# Division

```python
result = False / True

print(result)
print(type(result))
```

Output

```text
0.0
<class 'float'>
```

---

## Why Float?

Division operator `/` always returns a floating-point value.

---

# ZeroDivisionError

Since

```python
False = 0
```

this is invalid:

```python
print(True / False)
```

Output

```text
ZeroDivisionError:
division by zero
```

---

# 6️⃣ Mixing Boolean and Integer Values

Since Booleans behave like integers, they can participate in arithmetic operations.

---

## Example

```python
x = 10
y = 5

print(x + True)
print(y * False)

print(x - True + False)
```

Output

```text
11
0
9
```

---

# 7️⃣ Explicit Conversion

The `int()` constructor reveals the underlying integer values.

```python
print(int(True))
print(int(False))
```

Output

```text
1
0
```

---

# Quick Summary Table

| Expression        | Output            |
| ----------------- | ----------------- |
| `True + True`     | 2                 |
| `True + False`    | 1                 |
| `False + False`   | 0                 |
| `True - False`    | 1                 |
| `False - True`    | -1                |
| `True * False`    | 0                 |
| `False / True`    | 0.0               |
| `True / False`    | ZeroDivisionError |
| `int(True)`       | 1                 |
| `int(False)`      | 0                 |
| `numbers[::-1]`   | Reverse String    |
| `numbers[7:2:-1]` | 76543             |
| `numbers[2:7:-1]` | Empty String      |
| `name[0]='K'`     | TypeError         |

---

# 🎯 Key Takeaways

* Strings are ordered and immutable sequences.
* Python supports positive and negative indexing.
* Slicing follows the format:

```python
string[start:end:step]
```

* Start index is inclusive.
* End index is exclusive.
* Negative step traverses the string backward.
* Strings cannot be modified after creation.
* Boolean is a subclass of integer.
* Internally:

```python
True = 1
False = 0
```

* Arithmetic operations on Booleans follow normal integer arithmetic.
* Division by `False` raises a `ZeroDivisionError`.
* The `int()` function exposes the numeric representation of Boolean values.
