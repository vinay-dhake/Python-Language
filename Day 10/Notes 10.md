# 🐍 Python Comments, Constants & `print()` Function

> **Complete GitHub Notes** on Python Comments, Constants, PEP 8, `print()` Function, `sep` Keyword Argument, and Best Practices.

---

# 📚 Table of Contents

- Introduction
- Comments in Python
- Why Comments are Important
- Types of Comments
- Single-Line Comments
- Multi-Line Comments (Official Way)
- Multi-Line Comments (Unofficial Way)
- Why Triple Quotes are Not Real Comments
- PEP & PEP 8
- Why PEP is Needed
- Constants
- Constants in C++, Java & Python
- Constant Naming Convention
- `print()` Function
- Printing Variables
- String Concatenation
- Printing Multiple Values
- Automatic Spaces in `print()`
- `sep` Keyword Argument
- Changing the Separator
- Best Practices
- Common Mistakes
- Interview Questions
- Quick Revision
- Summary

---

# Introduction

Comments are an essential part of programming. They make code easier to understand, maintain, and debug. Along with comments, Python follows a standard coding style known as **PEP 8**, which helps developers write clean and consistent code.

This chapter also introduces **constants** in Python and explores the `print()` function in greater detail, including how it handles multiple arguments and separators.

---

# Comments in Python

A **comment** is a piece of text in the source code that is **ignored by the Python interpreter** during execution.

Comments are written for humans, not for the computer.

They help explain:

- Why a particular piece of code exists.
- What a block of code does.
- Important assumptions.
- Future improvements (TODOs).
- Warnings for other developers.

Since comments are ignored during execution, they **do not affect the program's output**.

---

## Why are Comments Important?

Imagine opening a project that contains thousands of lines of code but no explanations.

Understanding the program would become extremely difficult.

Good developers always write meaningful comments because they:

- Improve code readability.
- Help teammates understand the logic.
- Simplify debugging.
- Make maintenance easier.
- Save time in future development.

> **Remember:** Code is written once but read many times.

---

# Types of Comments in Python

Python commonly uses two styles of comments:

| Type | Official? |
|-------|-----------|
| Single-Line Comment (`#`) | ✅ Yes |
| Triple Quotes (`''' '''` or `""" """`) | ⚠️ Unofficial |

Although many beginners call triple quotes "multi-line comments", they are **not true comments**.

We'll understand why shortly.

---

# Single-Line Comments (Official Way)

Single-line comments begin with the **hash (`#`)** character.

Everything after `#` on that line is ignored by Python.

## Syntax

```python
# This is a comment
```

---

## Example

```python
a = 10

# a = a + 1

print(a)
```

### Output

```text
10
```

### Explanation

The statement

```python
a = a + 1
```

never executes because it has been commented out.

Python behaves as if that line doesn't exist.

---

# Characteristics of Single-Line Comments

- Begin with `#`
- End automatically at the end of the line
- Ignored by the interpreter
- Most widely used
- Officially recommended by Python

---

# Multi-Line Comments (Official Way)

Python does not provide a special syntax for multi-line comments.

Instead, the official recommendation is to write multiple single-line comments.

Example

```python
# Add one to a
# Add five to b
# Add ten to c
```

Although writing `#` repeatedly may seem repetitive, this is the **official style recommended by PEP 8**.

---

# VS Code Shortcut

In Visual Studio Code, you don't need to manually type `#` on every line.

Simply:

1. Select the lines.
2. Press

```
Ctrl + /
```

VS Code automatically comments or uncomments all selected lines.

This is the fastest way to create multi-line comments.

---

# Multi-Line Comments (Unofficial Way)

Many programmers use **triple quotes** to temporarily disable multiple lines of code.

Example

```python
a = 10

'''
a = a + 1
a = a + 1
'''

print(a)
```

### Output

```text
10
```

The code inside the triple quotes is not executed in this case.

This looks like a multi-line comment, but technically it is **not**.

---

# Triple Quotes

Python supports both:

```python
'''
Text
'''
```

and

```python
"""
Text
"""
```

Both create **multi-line string literals**.

---

# Why Triple Quotes are NOT Real Comments

This is one of the most misunderstood topics among beginners.

Consider

```python
'''
Hello
World
'''
```

Many people think Python ignores this completely.

Actually, Python creates a **string object**.

Since that string is not assigned to any variable,

```python
'''
Hello
World
'''
```

Python creates it,

then immediately discards it because nothing refers to it.

Later, it is removed by the Garbage Collector.

So,

Triple quotes create a **string object**, not a comment.

---

# Why Are They Called "Unofficial Comments"?

Because Python still processes them as string literals.

True comments are skipped entirely by the interpreter.

Triple-quoted strings are parsed as valid objects before being discarded.

Therefore,

> Triple quotes are **not ignored in the same way as `#` comments**.

---

# Official vs Unofficial Comments

| Feature | `#` Comment | Triple Quotes |
|----------|-------------|---------------|
| Official | ✅ Yes | ❌ No |
| Interpreter Ignores Completely | ✅ Yes | ❌ No |
| Creates Object | ❌ No | ✅ Yes (String) |
| Recommended by PEP 8 | ✅ Yes | ❌ No |

---

# Best Practice

Use:

```python
# Single-line comments
```

or

```python
# Line 1
# Line 2
# Line 3
```

Avoid using triple quotes as regular comments.

Reserve triple quotes mainly for:

- Docstrings
- Documentation
- Multi-line strings

rather than code comments.

---

# Python Enhancement Proposal (PEP)

Python follows official coding standards called

## PEP

PEP stands for

> **Python Enhancement Proposal**

These are documents that describe improvements, standards, and conventions for Python.

One of the most famous is **PEP 8**.

---

# What is PEP 8?

PEP 8 is Python's official **Style Guide**.

It provides recommendations on:

- Naming conventions
- Indentation
- Blank lines
- Comments
- Maximum line length
- Imports
- Function names
- Class names
- Variables
- Code formatting

The main goal is to make Python code **clean, readable, and consistent**.

---

# Why is PEP Needed?

Imagine ten developers working on the same project.

If each developer follows a different coding style, the codebase becomes difficult to read and maintain.

PEP 8 ensures that everyone follows the same standards.

Benefits include:

- Improved readability
- Consistent formatting
- Easier collaboration
- Better maintainability
- Professional code quality

---

# PEP 8 Examples

### Good Function Name

```python
def calculate_area():
    pass
```

### Bad Function Name

```python
def CalculateArea():
    pass
```

According to PEP 8,

Function names should use

```
snake_case
```

rather than CamelCase.

---

# Official PEP 8 Documentation

The complete style guide is available at:

https://peps.python.org/pep-0008/

Every professional Python developer should be familiar with PEP 8.

============================================================================================================================================================
---

# Constants in Python

A **constant** is a value that is intended to remain unchanged throughout the execution of a program.

Many programming languages provide special keywords that prevent the value of a constant from being modified.

For example:

- C++ uses the `const` keyword.
- Java uses the `final` keyword.

Python, however, takes a different approach.

---

# Constants in C++

In C++, constants are created using the `const` keyword.

Example

```cpp
const float PI = 3.14;

PI = 5.0;    // Error
```

The compiler immediately reports an error because constants cannot be modified.

---

# Constants in Java

Java uses the `final` keyword.

```java
final double PI = 3.14;

PI = 5.0;    // Compile Time Error
```

Once a variable is declared as `final`, its value cannot be changed.

---

# Constants in Python

Unlike C++ and Java,

Python **does not provide any keyword** such as

- `const`
- `final`

to create true constants.

Example

```python
PI = 3.14

PI = 4.14

print(PI)
```

Output

```text
4.14
```

Python allows the reassignment without producing any error.

---

# Why Doesn't Python Have Constants?

Python is a **dynamically typed language**.

Everything in Python is based on objects and references.

Variables are simply references to objects.

Because references can always point to another object,

Python intentionally does not provide a mechanism to lock a variable permanently.

This design keeps the language simple and flexible.

---

# Constant Naming Convention

Although Python cannot enforce constants,

the Python community follows an important convention.

If a variable should never be modified,

write its name entirely in **UPPERCASE**.

Example

```python
PI = 3.14

MAX_MARKS = 100

MAX_SIZE = 500
```

Uppercase names communicate to other developers that the value should be treated as constant.

---

# Is It Really Constant?

Consider

```python
PI = 3.14

PI = 100

print(PI)
```

Output

```text
100
```

Python happily changes the value.

Therefore,

UPPERCASE variables are **not actual constants**.

They are only a **coding convention**.

---

# Why Follow the Convention?

Imagine working with ten developers.

If one developer writes

```python
MAX_USERS = 500
```

everyone immediately understands

> "This value should not be modified."

Although Python cannot stop another programmer from changing it,

doing so violates professional coding etiquette.

---

# Examples

Example 1

```python
PI = 3.14

print(PI)
```

Output

```text
3.14
```

---

Example 2

```python
MAX_MARKS = 100

print(MAX_MARKS)
```

Output

```text
100
```

---

Example 3

```python
PI = 3.14

PI = 4.14

print(PI)
```

Output

```text
4.14
```

This demonstrates that Python constants are based on convention rather than language rules.

---

# Best Practice for Constants

Use uppercase variable names whenever the value is intended to remain unchanged.

Examples

```python
PI = 3.14159

GRAVITY = 9.8

MAX_SPEED = 120

DEFAULT_PORT = 8080
```

Avoid

```python
pi = 3.14

gravity = 9.8
```

because lowercase names suggest ordinary variables.

---

# The `print()` Function

The `print()` function is one of the most frequently used functions in Python.

Its primary purpose is to display information on the screen.

Syntax

```python
print(object1, object2, object3, ...)
```

The `print()` function can display

- Strings
- Numbers
- Variables
- Expressions
- Multiple values simultaneously

---

# Printing a Single Variable

Example

```python
name = "Sachin"

print(name)
```

Output

```text
Sachin
```

---

Example

```python
age = 42

print(age)
```

Output

```text
42
```

---

# Printing Multiple Variables

Example

```python
name = "Sachin"

age = 42

print(name, age)
```

Output

```text
Sachin 42
```

Notice the automatically inserted space between the values.

---

# String Concatenation Using `+`

Suppose

```python
a = "Good"

b = "Morning"

print(a + b)
```

Output

```text
GoodMorning
```

The `+` operator joins the two strings together without inserting any extra spaces.

---

# Another Example

```python
first = "Python"

second = "Programming"

print(first + second)
```

Output

```text
PythonProgramming
```

---

# What if One Value is a Number?

Consider

```python
a = "Good"

b = 10

print(a + b)
```

Output

```text
TypeError
```

Why?

Because

```python
+
```

can concatenate only compatible data types.

Python cannot automatically combine a string and an integer using `+`.

---

# Correct Way

Instead of

```python
print(a + b)
```

use

```python
print(a, b)
```

Output

```text
Good 10
```

The `print()` function automatically converts the integer into text before displaying it.

---

# Using Commas Inside `print()`

Example

```python
print("Good", "Morning")
```

Output

```text
Good Morning
```

Notice

A space is inserted automatically.

---

Example

```python
a = "Good"

b = 10

print(a, b)
```

Output

```text
Good 10
```

Again,

Python automatically inserts one space.

---

# Another Example

```python
a = 10

b = 20

print(a, b)
```

Output

```text
10 20
```

---

# Printing Messages Along With Variables

Example

```python
name = "Sachin"

print("My name is", name)
```

Output

```text
My name is Sachin
```

---

Example

```python
age = 42

print("My age is", age)
```

Output

```text
My age is 42
```

---

# Printing Multiple Variables in a Sentence

Example

```python
name = "Sachin"

age = 42

print("My name is", name, "and my age is", age)
```

Output

```text
My name is Sachin and my age is 42
```

Notice

Even though no spaces were written after

```python
"My name is",

name,

"and my age is",
```

Python automatically inserted spaces between every argument.

This behavior is controlled by the `sep` keyword argument, which we'll explore next.
============================================================================================================================================================
---

# Automatic Spaces in `print()`

One of the most convenient features of Python's `print()` function is that it automatically inserts a space between multiple arguments.

Consider the following example:

```python
print("Good", "Morning")
```

Output

```text
Good Morning
```

Notice that we never typed a space after `"Good"`.

Python inserted it automatically.

---

Another example

```python
print("Python", "Programming", "Language")
```

Output

```text
Python Programming Language
```

Again,

a single space appears between every argument.

---

# How Does Python Generate These Spaces?

Many beginners think Python magically inserts spaces.

Actually,

the `print()` function has a keyword argument called

```python
sep
```

whose default value is

```python
" "
```

(a single space)

Internally,

```python
print("Good", "Morning")
```

behaves approximately like

```python
print("Good", "Morning", sep=" ")
```

Since the default separator is a space,

the output becomes

```text
Good Morning
```

---

# What is `sep`?

`sep` stands for

> **Separator**

It specifies what should appear between two consecutive arguments printed by the `print()` function.

General Syntax

```python
print(arg1, arg2, arg3, ..., sep="separator")
```

---

# Default Value of `sep`

```python
sep = " "
```

This means

```python
print(10, 20)
```

is internally treated as

```python
print(10, 20, sep=" ")
```

Output

```text
10 20
```

---

# Changing the Separator

We can replace the default space with any character or string.

Example

```python
print("Good", "Morning", sep=", ")
```

Output

```text
Good, Morning
```

Instead of a space,

a comma followed by a space appears.

---

# Example: Hash (`#`) Separator

```python
a = 10
b = 20

print(a, b, sep="#")
```

Output

```text
10#20
```

The space is replaced with `#`.

---

# Example: Colon (`:`) Separator

Suppose we want to display time.

```python
hh = 10
mm = 30
ss = 45

print(hh, mm, ss, sep=":")
```

Output

```text
10:30:45
```

This is much cleaner than manually joining strings.

---

# Example: Hyphen Separator

```python
print("2026", "07", "02", sep="-")
```

Output

```text
2026-07-02
```

---

# Example: Arrow Separator

```python
print("Python", "Java", "C++", sep=" -> ")
```

Output

```text
Python -> Java -> C++
```

---

# Example: No Separator

```python
print("Hello", "World", sep="")
```

Output

```text
HelloWorld
```

Notice that this behaves similarly to string concatenation.

---

# Difference Between `+` and `,`

Many beginners confuse these two approaches.

### Using `+`

```python
a = "Good"
b = "Morning"

print(a + b)
```

Output

```text
GoodMorning
```

Requirements

- Both operands must be strings.
- No automatic spaces are added.

---

### Using `,`

```python
a = "Good"
b = "Morning"

print(a, b)
```

Output

```text
Good Morning
```

Advantages

- Works with different data types.
- Automatically inserts separators.
- Easier to read.

---

# Comparing `+` and `,`

| Feature | `+` | `,` inside `print()` |
|---------|-----|----------------------|
| Joins Strings | ✅ | ❌ |
| Prints Multiple Values | ❌ | ✅ |
| Automatic Space | ❌ | ✅ |
| Works with Integers Directly | ❌ | ✅ |
| Controlled by `sep` | ❌ | ✅ |

---

# Best Practices

### ✅ Use comments to explain **why**, not **what**.

Bad

```python
# Increment i
i = i + 1
```

Good

```python
# Skip the first record because it contains invalid data
i = i + 1
```

---

### ✅ Prefer `#` for comments.

Instead of

```python
'''
Temporary comment
'''
```

write

```python
# Temporary comment
```

---

### ✅ Follow PEP 8.

- Use meaningful variable names.
- Use lowercase function names.
- Use proper indentation.
- Write readable code.

---

### ✅ Write constants in uppercase.

Good

```python
PI = 3.14159

MAX_SPEED = 120
```

Bad

```python
pi = 3.14159
```

---

### ✅ Use commas inside `print()` whenever possible.

Instead of

```python
print("Age : " + str(age))
```

write

```python
print("Age:", age)
```

Cleaner,

simpler,

and easier to maintain.

---

# Common Mistakes

### ❌ Mistake 1

```python
print("Age is " + 20)
```

Output

```text
TypeError
```

Correct

```python
print("Age is", 20)
```

---

### ❌ Mistake 2

Thinking triple quotes are comments.

Actually,

they create string objects.

---

### ❌ Mistake 3

Believing uppercase variables are true constants.

Example

```python
PI = 3.14

PI = 5
```

This is completely valid in Python.

---

### ❌ Mistake 4

Using comments excessively.

Avoid

```python
# Assign 10 to x
x = 10
```

The code is already obvious.

Comments should explain intent, not repeat the code.

---

# Interview Questions

### 1. What are comments?

Statements ignored during program execution and used for documentation.

---

### 2. How many types of comments are commonly used in Python?

- Single-line comments (`#`)
- Triple-quoted strings (commonly used but unofficial)

---

### 3. Why are triple quotes not real comments?

Because they create **string objects**, not actual comments.

---

### 4. What does PEP stand for?

**Python Enhancement Proposal**

---

### 5. What is PEP 8?

Python's official style guide for writing clean and readable code.

---

### 6. Does Python support true constants?

No.

Python has no `const` or `final` keyword.

---

### 7. How are constants represented in Python?

By convention, using **UPPERCASE** variable names.

Example

```python
PI = 3.14
```

---

### 8. What is the default value of `sep`?

```python
" "
```

(a single space)

---

### 9. What does `sep` do?

It specifies the separator inserted between multiple arguments of `print()`.

---

### 10. Difference between `+` and `,` in `print()`?

- `+` concatenates strings.
- `,` prints multiple objects and automatically inserts the separator.

---

# Quick Revision

- Comments improve readability.
- `#` is the official comment syntax.
- Triple quotes create string objects.
- PEP stands for Python Enhancement Proposal.
- PEP 8 defines Python coding standards.
- Python has no true constants.
- Uppercase variable names indicate constants by convention.
- `print()` can print multiple values.
- `+` concatenates strings.
- `,` prints multiple objects.
- `sep` controls the separator.
- Default `sep` is a single space.

---

# Summary

In this chapter, we explored how comments improve code readability and why Python officially recommends using `#` comments instead of triple-quoted strings. We also learned about **PEP 8**, Python's official style guide, and understood that Python does not support true constants, relying instead on uppercase naming conventions.

Finally, we studied the `print()` function in detail, including printing multiple values, automatic spacing, string concatenation, and the `sep` keyword argument. Mastering these concepts helps you write cleaner, more readable, and more professional Python programs that follow widely accepted coding standards.
