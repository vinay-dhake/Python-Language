# 🐍 Python Number Systems, Data Types, Identifiers & Keywords

This document covers Python's Interactive Shell (REPL), number system representations, data type inspection, identifier rules, and reserved keywords.

---

# 1️⃣ Python REPL (Interactive Shell)

The Python Interactive Shell, also known as the **REPL (Read-Eval-Print Loop)**, provides an environment for quickly testing Python statements and expressions.

When Python starts in interactive mode, the prompt appears as:

```python
>>>
```

This prompt indicates that Python is ready to accept input.

---

## How REPL Works

REPL stands for:

| Letter | Meaning  |
| ------ | -------- |
| R      | Read     |
| E      | Evaluate |
| P      | Print    |
| L      | Loop     |

### REPL Flow

```text
Read Input
     │
     ▼
Evaluate Expression
     │
     ▼
Print Result
     │
     ▼
Loop Back
```

---

## Example

```python
>>> 10 + 20
30

>>> 5 * 5
25
```

Notice that Python automatically displays the result without explicitly using `print()`.

---

# 2️⃣ Integer Representations in Python

Python supports multiple number systems.

Regardless of representation, Python internally converts values into decimal form.

---

## Supported Number Systems

| Number System | Base | Prefix       |
| ------------- | ---- | ------------ |
| Decimal       | 10   | No Prefix    |
| Binary        | 2    | `0b` or `0B` |
| Octal         | 8    | `0o` or `0O` |
| Hexadecimal   | 16   | `0x` or `0X` |

---

## Decimal Numbers

```python
>>> a = 10
>>> print(a)
10
```

---

## Binary Numbers

```python
>>> a = 0b1010
>>> print(a)
```

Output:

```python
10
```

---

## Octal Numbers

```python
>>> a = 0o12
>>> print(a)
```

Output:

```python
10
```

---

## Hexadecimal Numbers

```python
>>> a = 0x1A
>>> print(a)
```

Output:

```python
26
```

---

# Binary Number Examples

```python
>>> a = 0b101
>>> print(a)
```

Output:

```python
5
```

---

```python
>>> a = 0b1111
>>> print(a)
```

Output:

```python
15
```

---

```python
>>> a = 0b10101
>>> print(a)
```

Output:

```python
21
```

---

## Unary Minus with Binary Numbers

```python
>>> a = -0b1010
>>> print(a)
```

Output:

```python
-10
```

### Explanation

Python first evaluates:

```python
0b1010
```

which equals:

```python
10
```

Then applies the unary negative operator:

```python
-10
```

---

# Invalid Binary Literals

Binary numbers can only contain:

```text
0 and 1
```

---

## Example

```python
>>> a = 0b12
```

Output:

```python
SyntaxError: invalid digit '2' in binary literal
```

### Why?

The digit `2` is not valid in the binary number system.

---

# 3️⃣ Data Type Inspection Using `type()`

Python is a **dynamically typed language**.

Variables do not require explicit type declarations.

The built-in `type()` function is used to inspect the data type of an object.

---

## Integer Example

```python
>>> item_count = 50
>>> type(item_count)
```

Output:

```python
<class 'int'>
```

---

## Float Example

```python
>>> user_rating = 4.8
>>> type(user_rating)
```

Output:

```python
<class 'float'>
```

---

## String Example

```python
>>> user_name = "Python"
>>> type(user_name)
```

Output:

```python
<class 'str'>
```

---

## Important Concept

In Python:

> Everything is an Object.

Even simple values such as integers, strings, and floats are objects created from classes.

---

# 4️⃣ Identifiers in Python

An **Identifier** is a user-defined name used to identify:

* Variables
* Functions
* Classes
* Modules
* Packages

---

## Rules for Identifiers

### Allowed Characters

Identifiers may contain:

* A-Z
* a-z
* 0-9
* Underscore (_)

---

### First Character Rule

The first character must be:

* An alphabet
* An underscore (_)

An identifier cannot begin with a number.

---

### Case Sensitivity

Python is case-sensitive.

These are all different identifiers:

```python
totalAmount
TotalAmount
TOTALAMOUNT
```

---

## Valid Identifiers

```python
total_sum = 250

_session_id = "A8FD9"

value2 = 9.9
```

---

## Invalid Identifier

```python
2value = 9.9
```

Output:

```python
SyntaxError: invalid decimal literal
```

### Reason

Identifiers cannot start with digits.

---

# 5️⃣ Reserved Keywords

Keywords are predefined words reserved by Python.

They have special meanings and cannot be used as identifiers.

---

## Viewing Keywords

Python provides the `keyword` module.

```python
import keyword
```

---

## List of Keywords

```python
keyword.kwlist
```

Output:

```python
['False', 'None', 'True', 'and', 'as', 'assert', 'async',
 'await', 'break', 'class', 'continue', 'def', 'del',
 'elif', 'else', 'except', 'finally', 'for', 'from',
 'global', 'if', 'import', 'in', 'is', 'lambda',
 'nonlocal', 'not', 'or', 'pass', 'raise', 'return',
 'try', 'while', 'with', 'yield']
```

---

## Counting Keywords

```python
len(keyword.kwlist)
```

Output:

```python
35
```

Python 3.13 contains **35 reserved keywords**.

---

## Keyword Error Example

```python
def = 400
```

Output:

```python
SyntaxError: invalid syntax
```

### Why?

`def` is a reserved keyword used for defining functions.

Python does not allow keywords to be used as variable names.

---

# 📋 Quick Reference Table

| Expression            | Output          | Explanation                        |
| --------------------- | --------------- | ---------------------------------- |
| `0b1010`              | `10`            | Binary to Decimal Conversion       |
| `0o17`                | `15`            | Octal to Decimal Conversion        |
| `0xF`                 | `15`            | Hexadecimal to Decimal Conversion  |
| `0b1012`              | `SyntaxError`   | Invalid Binary Digit               |
| `type("Hello")`       | `<class 'str'>` | String Type Inspection             |
| `1st_value = 5`       | `SyntaxError`   | Identifier Cannot Start With Digit |
| `import keyword`      | Module Imported | Loads Keyword Module               |
| `len(keyword.kwlist)` | `35`            | Total Reserved Keywords            |

---

# 🎯 Key Takeaways

* Python Interactive Mode follows the REPL model.
* Python supports Decimal, Binary, Octal, and Hexadecimal number systems.
* Binary literals use the prefix `0b`.
* Octal literals use the prefix `0o`.
* Hexadecimal literals use the prefix `0x`.
* Invalid digits in a number system generate a `SyntaxError`.
* Python is dynamically typed.
* The `type()` function is used to inspect object types.
* Everything in Python is an object.
* Identifiers must follow naming rules.
* Python keywords are reserved and cannot be used as identifiers.
* Python 3.13 contains 35 reserved keywords.


===================================================================================================================
## Number Systems and Allowed Symbols

### Decimal (Base-10)

Uses digits:

```text
0 1 2 3 4 5 6 7 8 9
```

Example:

```python
a = 125
```

---

### Binary (Base-2)

Uses digits:

```text
0 1
```

Prefix:

```python
0b
```

Example:

```python
a = 0b1010
print(a)
```

Output:

```text
10
```

Invalid Example:

```python
a = 0b102
```

Reason:

```text
2 is not allowed in Binary numbers.
```

---

### Octal (Base-8)

Uses digits:

```text
0 1 2 3 4 5 6 7
```

Prefix:

```python
0o
```

Example:

```python
a = 0o17
print(a)
```

Output:

```text
15
```

Invalid Example:

```python
a = 0o18
```

Reason:

```text
8 is not allowed in Octal numbers.
```

---

### Hexadecimal (Base-16)

Uses symbols:

```text
0 1 2 3 4 5 6 7 8 9
A B C D E F
```

or

```text
a b c d e f
```

Where:

| Symbol | Value |
| ------ | ----- |
| A      | 10    |
| B      | 11    |
| C      | 12    |
| D      | 13    |
| E      | 14    |
| F      | 15    |

Prefix:

```python
0x
```

Example:

```python
a = 0x1A
print(a)
```

Output:

```text
26
```

Invalid Example:

```python
a = 0x1G
```

Reason:

```text
G is not a valid hexadecimal symbol.
```

---

## Quick Summary

| Number System | Base | Allowed Symbols | Prefix |
| ------------- | ---- | --------------- | ------ |
| Decimal       | 10   | 0-9             | None   |
| Binary        | 2    | 0, 1            | 0b     |
| Octal         | 8    | 0-7             | 0o     |
| Hexadecimal   | 16   | 0-9, A-F        | 0x     |
