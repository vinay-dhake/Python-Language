# 🐍 Python Operators, Logical Operators & Operator Precedence (Lecture 12)

> **Complete GitHub Notes** on Cascading Relational Operators, Equality & Inequality, Logical Operators, Assignment Operators, Identity Operators, Membership Operators, Operator Precedence, Associativity, and Interview Questions.

---

# 📚 Table of Contents

- Introduction
- Cascading Relational Operators
- Equality (`==`) Operator
- Inequality (`!=`) Operator
- Type Compatibility in Comparisons
- Boolean Comparisons
- Integer, Float and Complex Comparisons
- String Comparisons
- Logical Operators
- Truthy & Falsy Values
- Short-Circuit Evaluation
- Assignment Operators
- Multiple Assignment
- Compound Assignment Operators
- Why Python Doesn't Support `++` and `--`
- Identity Operators
- Membership Operators
- Operator Precedence
- Associativity
- Best Practices
- Common Mistakes
- Interview Questions
- Quick Revision
- Summary

---

# Introduction

Until now, we have learned about arithmetic operators and comparison operators individually.

In this lecture, we move one step further and study how Python evaluates multiple operators together. We will also learn about logical operators, assignment operators, identity operators, membership operators, and operator precedence.

These concepts are extremely important because they are used in almost every Python program, from simple conditional statements to advanced algorithms.

---

# Cascading (Chaining) Relational Operators

One of Python's unique features is that it allows **multiple comparison operators** to be written together.

This is called **Operator Cascading** or **Comparison Chaining**.

Unlike C, C++, or Java, Python directly supports expressions like

```python
5 < x < 10
```

This makes Python code more readable and mathematically natural.

---

## General Syntax

```python
a < b < c
```

Python internally converts it into

```python
(a < b) and (b < c)
```

Both conditions must be `True` for the entire expression to be `True`.

---

# How Python Evaluates Cascading Comparisons

Python checks the comparisons from **left to right**.

Each comparison is connected internally using the logical `and` operator.

If every comparison evaluates to `True`, the final result is `True`.

If even one comparison is `False`, the final result becomes `False`.

---

# Example 1

```python
print(7 > 6 > 5)
```

Python internally evaluates

```python
(7 > 6) and (6 > 5)
```

Step 1

```python
7 > 6
```

Result

```python
True
```

Step 2

```python
6 > 5
```

Result

```python
True
```

Final Result

```python
True and True
```

Output

```text
True
```

---

# Example 2

```python
print(7 > 6 < 5)
```

Internal Evaluation

```python
(7 > 6) and (6 < 5)
```

Step 1

```python
True
```

Step 2

```python
False
```

Final Result

```python
False
```

Output

```text
False
```

---

# Example 3

```python
print(5 < 6 > 7)
```

Internal Evaluation

```python
(5 < 6) and (6 > 7)
```

Step 1

```python
True
```

Step 2

```python
False
```

Final Result

```python
False
```

Output

```text
False
```

---

# Why is Comparison Chaining Useful?

Instead of writing

```python
age > 18 and age < 60
```

we can simply write

```python
18 < age < 60
```

This is shorter, easier to read, and resembles mathematical notation.

---

# Equality Operator (`==`)

The equality operator checks whether **two operands have equal values**.

Syntax

```python
a == b
```

Returns

```python
True
```

if the values are equal, otherwise

```python
False
```

---

# Example

```python
print(10 == 10)
```

Output

```text
True
```

---

Example

```python
print(10 == 20)
```

Output

```text
False
```

---

# Type Compatibility in Equality Comparisons

Python behaves differently depending on the data types involved.

There are three common situations:

1. Same data types
2. Compatible data types
3. Incompatible data types

---

# Case 1: Same Data Types

Example

```python
print(100 == 100)
```

Output

```text
True
```

Both operands are integers.

---

Example

```python
print("Python" == "Python")
```

Output

```text
True
```

Both operands are strings.

---

# Case 2: Compatible Data Types

Some data types can be compared after implicit conversion.

Example

```python
print(15 == 15.0)
```

Python converts

```
15

↓

15.0
```

Comparison

```python
15.0 == 15.0
```

Output

```text
True
```

---

Another example

```python
print(15 == 15.01)
```

Output

```text
False
```

Because

```
15.0

≠

15.01
```

---

# Integer and Boolean Comparison

Python internally treats

```python
True
```

as

```python
1
```

and

```python
False
```

as

```python
0
```

---

Example

```python
print(1 == True)
```

Internal Evaluation

```python
1 == 1
```

Output

```text
True
```

---

Example

```python
print(10 == True)
```

Internal Evaluation

```python
10 == 1
```

Output

```text
False
```

---

Example

```python
print(0 == False)
```

Internal Evaluation

```python
0 == 0
```

Output

```text
True
```

---

Example

```python
print(False == 0.0)
```

Python converts

```
False

↓

0

↓

0.0
```

Output

```text
True
```

---

# Case 3: Incompatible Data Types

If Python cannot safely compare the data types,

it simply returns

```python
False
```

instead of trying to convert them.

---

Example

```python
print(10 == "10")
```

Output

```text
False
```

Why?

Because

```
Integer

≠

String
```

Python never automatically converts

```
"10"

↓

10
```

---

Another example

```python
print("A" == 65)
```

Output

```text
False
```

Even though

```python
ord("A")
```

is

```python
65
```

Python does **not** perform this conversion automatically.

---

Example

```python
print("A" == "65")
```

Output

```text
False
```

Both are strings,

but their contents are different.

---

# Complex Number Comparison

Example

```python
print(2 + 5j == 2 + 5j)
```

Output

```text
True
```

---

Example

```python
print(2 + 5j == 2)
```

Output

```text
False
```

A complex number and an integer represent different values.

---

# Inequality Operator (`!=`)

The inequality operator checks whether two values are **different**.

Syntax

```python
a != b
```

Returns

```python
True
```

if the values are different.

Otherwise,

returns

```python
False
```

---

# Examples

```python
print(10 != 20)
```

Output

```text
True
```

---

```python
print(15 != "15")
```

Output

```text
True
```

Integer

```
15
```

is different from String

```
"15"
```

---

```python
print(0 != False)
```

Internal Evaluation

```python
0 != 0
```

Output

```text
False
```

---

```python
print(False != True)
```

Internal Evaluation

```python
0 != 1
```

Output

```text
True
```

---

```python
print(False != 0.0)
```

Output

```text
False
```

---

# Summary of Equality Examples

| Expression | Output | Reason |
|------------|--------|--------|
| `10 == 10` | `True` | Same type and value |
| `10 == 20` | `False` | Different values |
| `10 == "10"` | `False` | Different data types |
| `1 == True` | `True` | `True` equals `1` |
| `10 == True` | `False` | `10 ≠ 1` |
| `15 == 15.0` | `True` | Integer promoted to float |
| `15 == 15.01` | `False` | Values differ |
| `"A" == 65` | `False` | No implicit Unicode conversion |
| `2+5j == 2+5j` | `True` | Same complex value |
| `2+5j != 2` | `True` | Different types and values |

---
==============================================================================================================================================================
---

# Logical Operators

Logical operators are used to combine multiple conditions into a single expression.

Unlike arithmetic operators, logical operators primarily work with **Boolean values**. However, Python is unique because logical operators can also operate on **non-Boolean objects**.

Python provides three logical operators:

| Operator | Meaning |
|----------|---------|
| `and` | Logical AND |
| `or` | Logical OR |
| `not` | Logical NOT |

Unlike C, C++, and Java, Python uses words instead of symbols.

| C/C++/Java | Python |
|------------|---------|
| `&&` | `and` |
| `||` | `or` |
| `!` | `not` |

---

# Truthy and Falsy Values

Before understanding logical operators, we must understand **truthy** and **falsy** objects.

Every object in Python has an inherent Boolean value.

Some objects behave as

```
False
```

while all remaining objects behave as

```
True
```

---

# Falsy Values

Python treats the following as **False**.

- `False`
- `None`
- `0`
- `0.0`
- `0j`
- `""` (Empty String)
- `[]` (Empty List)
- `()` (Empty Tuple)
- `{}` (Empty Dictionary)
- `set()` (Empty Set)

Example

```python
print(bool(0))
print(bool(""))
print(bool([]))
```

Output

```text
False
False
False
```

---

# Truthy Values

Everything that is **not falsy** becomes truthy.

Examples

```python
10

-5

3.14

"Python"

"Sachin"

[1,2]

(True)
```

Example

```python
print(bool(100))
print(bool("Hello"))
print(bool([1,2]))
```

Output

```text
True
True
True
```

---

# Logical AND (`and`)

The `and` operator returns **True** only if **both conditions are True**.

Truth Table

| A | B | A and B |
|---|---|----------|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

---

# Python's Special Behavior

Unlike many programming languages,

Python's `and`

does **not always return True or False**.

Instead,

it returns one of the operands.

This surprises many beginners.

---

# Rule of `and`

Python first evaluates the **left operand**.

### If the left operand is Falsy

Return the left operand immediately.

The second operand is never evaluated.

### If the left operand is Truthy

Evaluate and return the second operand.

This behavior is called **Short-Circuit Evaluation**.

---

# Example

```python
print(5 and 6)
```

Evaluation

```
5

↓

Truthy

↓

Return second operand
```

Output

```text
6
```

---

# Example

```python
print(5 and 0)
```

Evaluation

```
5

↓

Truthy

↓

Return second operand
```

Output

```text
0
```

---

# Example

```python
print(0 and 10)
```

Evaluation

```
0

↓

Falsy

↓

Return first operand
```

Output

```text
0
```

Notice

Python never evaluates

```
10
```

---

# Example

```python
print(6 and 0)
```

Output

```text
0
```

---

# Example

```python
print("Sachin" and 10)
```

Evaluation

```
"Sachin"

↓

Truthy

↓

Return second operand
```

Output

```text
10
```

---

# Example

```python
print("Sachin" and 0)
```

Output

```text
0
```

---

# Example

```python
print("Indore" and "Bhopal")
```

Output

```text
Bhopal
```

Because

```
"Indore"

↓

Truthy

↓

Return second operand
```

---

# Example

```python
print("Bhopal" and "Indore")
```

Output

```text
Indore
```

---

# Short-Circuit Evaluation

Short-circuiting means

Python stops evaluating an expression as soon as the final answer becomes known.

---

## Example

```python
print(10/0 and 0)
```

Python first evaluates

```python
10/0
```

Immediately

```
ZeroDivisionError
```

occurs.

Python never reaches

```
and 0
```

Output

```text
ZeroDivisionError
```

---

## Example

```python
print(0 and 10/0)
```

Evaluation

```
0

↓

Falsy

↓

Return first operand
```

Python never evaluates

```python
10/0
```

Therefore

Output

```text
0
```

No exception occurs.

This is one of the most important examples from the lecture because it demonstrates short-circuit evaluation. :contentReference[oaicite:0]{index=0}

---

# Logical OR (`or`)

The `or` operator returns **True** if at least one condition is True.

Truth Table

| A | B | A or B |
|---|---|---------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

---

# Python's Rule for `or`

Python first evaluates the left operand.

### If the left operand is Truthy

Return the first operand immediately.

Second operand is never evaluated.

### If the left operand is Falsy

Evaluate and return the second operand.

---

# Example

```python
print(5 or 6)
```

Output

```text
5
```

---

# Example

```python
print(5 or 0)
```

Output

```text
5
```

---

# Example

```python
print(0 or 10)
```

Evaluation

```
0

↓

Falsy

↓

Return second operand
```

Output

```text
10
```

---

# Example

```python
print(6 or 0)
```

Output

```text
6
```

---

# Example

```python
print("Sachin" or 10)
```

Output

```text
Sachin
```

---

# Example

```python
print("Sachin" or 0)
```

Output

```text
Sachin
```

---

# Example

```python
print("Indore" or "Bhopal")
```

Output

```text
Indore
```

---

# Example

```python
print("Bhopal" or "Indore")
```

Output

```text
Bhopal
```

---

# Another Short-Circuit Example

```python
print(0 or 10/0)
```

Evaluation

```
0

↓

Falsy

↓

Evaluate second operand
```

Python now executes

```python
10/0
```

Output

```text
ZeroDivisionError
```

---

Another example

```python
print(10/0 or 0)
```

Python evaluates

```python
10/0
```

first.

Immediately

```
ZeroDivisionError
```

occurs.

---

# Logical NOT (`not`)

`not` reverses the Boolean value.

Truth Table

| A | not A |
|---|-------|
| True | False |
| False | True |

---

# Examples

```python
print(not 5)
```

Output

```text
False
```

Because

```
5

↓

Truthy

↓

False
```

---

```python
print(not 0)
```

Output

```text
True
```

---

```python
print(not "Sachin")
```

Output

```text
False
```

---

```python
print(not "")
```

Output

```text
True
```

---

# Practical Use of `or`

A common real-world use case is assigning a default value.

```python
name = input("Enter name: ") or "Default User"

print(name)
```

If the user presses **Enter** without typing anything, `input()` returns an empty string (`""`), which is falsy.

Therefore, the `or` operator returns `"Default User"`.

This is a clean alternative to writing an `if-else` statement and is a practical example highlighted in the lecture. :contentReference[oaicite:1]{index=1}

===============================================================================================================================================================
---

# Assignment Operators

Assignment operators are used to assign values to variables.

The most common assignment operator is

```python
=
```

Example

```python
a = 10
```

Here,

```
10
```

is assigned to the variable

```
a
```

---

# Multiple Assignment

Python allows assigning the **same value** to multiple variables in a single statement.

Syntax

```python
x = y = z = value
```

Example

```python
x = y = z = 10

print(x)
print(y)
print(z)
```

Output

```text
10
10
10
```

Python first evaluates the value on the right-hand side and then assigns it to all variables from right to left.

---

# Assigning Different Values

Python also allows assigning different values simultaneously.

Syntax

```python
x, y, z = value1, value2, value3
```

Example

```python
x, y, z = 10, 20, 30

print(x)
print(y)
print(z)
```

Output

```text
10
20
30
```

This feature is called **Tuple Unpacking** because Python internally packs the values into a tuple and unpacks them into the variables.

---

# Tuple Unpacking

Consider

```python
a, b, c = 100, 200, 300
```

Internally Python behaves approximately like

```python
(a, b, c) = (100, 200, 300)
```

Each variable receives the corresponding value.

---

# Important Rule

The number of variables on the left **must exactly match** the number of values on the right.

Correct

```python
a, b = 10, 20
```

Incorrect

```python
a, b = 10, 20, 30
```

Output

```text
ValueError
```

Similarly,

```python
a, b, c = 10, 20
```

also produces

```text
ValueError
```

because the number of variables and values do not match.

---

# Compound Assignment Operators

Python provides shorthand assignment operators that combine an arithmetic operation with assignment.

Instead of writing

```python
a = a + 5
```

we can write

```python
a += 5
```

This makes the code shorter and easier to read.

---

# List of Compound Assignment Operators

| Operator | Equivalent Expression |
|----------|------------------------|
| `+=` | `a = a + b` |
| `-=` | `a = a - b` |
| `*=` | `a = a * b` |
| `/=` | `a = a / b` |
| `%=` | `a = a % b` |
| `//=` | `a = a // b` |
| `**=` | `a = a ** b` |

---

# Examples

### Addition Assignment

```python
a = 10

a += 5

print(a)
```

Output

```text
15
```

---

### Subtraction Assignment

```python
a = 20

a -= 8

print(a)
```

Output

```text
12
```

---

### Multiplication Assignment

```python
a = 10

a *= 5

print(a)
```

Output

```text
50
```

---

### Division Assignment

```python
a = 20

a /= 4

print(a)
```

Output

```text
5.0
```

Notice

Division assignment also produces a floating-point result.

---

### Floor Division Assignment

```python
a = 17

a //= 5

print(a)
```

Output

```text
3
```

---

### Modulus Assignment

```python
a = 17

a %= 5

print(a)
```

Output

```text
2
```

---

### Exponentiation Assignment

```python
a = 2

a **= 5

print(a)
```

Output

```text
32
```

---

# Why Use Compound Assignment?

Advantages

- Shorter code
- Better readability
- Less typing
- Commonly used in loops and counters

---

# Why Doesn't Python Have `++` and `--`?

Many languages such as

- C
- C++
- Java

support

```cpp
++

--
```

Python does **not**.

This is one of the most frequently asked interview questions.

---

# Example

```python
a = 10

a++
```

Output

```text
SyntaxError
```

Python has **no increment operator**.

---

# What About `++a`?

Many beginners think

```python
++a
```

increments the value.

It does **not**.

Suppose

```python
a = 10

print(++a)
```

Python interprets it as

```python
+(+(10))
```

The unary plus operator simply returns the number unchanged.

Output

```text
10
```

No increment happens.

---

# What About `--a`?

Similarly,

```python
a = 10

print(--a)
```

Python interprets it as

```python
-(-10)
```

Evaluation

```
-10

↓

10
```

Output

```text
10
```

Again,

no decrement occurs.

---

# Multiple Unary Operators

Example

```python
a = 10

print(-----a)
```

Evaluation

```text
-(-(-(-(-10))))
```

Result

```text
-10
```

Python simply applies unary minus repeatedly.

It is **not** a decrement operator.

---

# Identity Operators

Identity operators compare whether two variables refer to the **same object in memory**.

Python provides

| Operator | Meaning |
|----------|---------|
| `is` | Same object |
| `is not` | Different objects |

Unlike `==`, identity operators compare **object identity**, not just values.

---

# `is` Operator

Example

```python
a = 10
b = 10

print(a is b)
```

Output

```text
True
```

Small integers are cached, so both variables usually refer to the same object.

---

Example from the lecture

```python
a = 2
b = 3

print(a is b)
```

Output

```text
False
```

Because `a` and `b` contain different objects. :contentReference[oaicite:0]{index=0}

---

# Using `is` with `type()`

Identity operators are often used for explicit type checking.

Example

```python
a = 10

print(type(a) is int)
```

Output

```text
True
```

---

```python
print(type(a) is float)
```

Output

```text
False
```

---

# `is not` Operator

Example

```python
a = "Delhi"
b = "Delhi"

print(a is not b)
```

Output

```text
False
```

Python generally interns simple string literals, so both references point to the same object.

---

Example

```python
a = "Delhi"
b = "delhi"

print(a is not b)
```

Output

```text
True
```

Because the strings are different (case-sensitive), they are different objects. :contentReference[oaicite:1]{index=1}

---

# Membership Operators

Membership operators check whether an element exists inside a collection.

Python provides

| Operator | Meaning |
|----------|---------|
| `in` | Element exists |
| `not in` | Element does not exist |

These operators work with

- Strings
- Lists
- Tuples
- Sets
- Dictionaries

---

# Using `in` with Strings

Example

```python
print("om" in "Welcome")
```

Output

```text
True
```

The substring

```
om
```

appears inside

```
Welcome
```

---

Example

```python
print("mom" in "Welcome")
```

Output

```text
False
```

---

# Using `not in`

Example

```python
print(4 not in [1, 2, 3, 5])
```

Output

```text
True
```

---

Example

```python
x = 5

print(x not in [1, 2, 3, 5])
```

Output

```text
False
```

Because

```
5
```

already exists in the list. :contentReference[oaicite:2]{index=2}

---
=============================================================================================================================================================
---

# Operator Precedence

In real-world programs, expressions often contain multiple operators.

Example

```python
10 + 20 * 5
```

A natural question arises:

> **Which operation will Python perform first?**

Python follows a predefined set of rules known as **Operator Precedence**.

Operator precedence determines **which operator has higher priority** when multiple operators appear in the same expression.

---

# Why is Operator Precedence Important?

Consider

```python
10 + 5 * 2
```

If addition happened first,

```
10 + 5 = 15

15 × 2 = 30
```

If multiplication happened first,

```
5 × 2 = 10

10 + 10 = 20
```

Two different answers!

Therefore, Python follows a fixed priority system.

---

# Operator Precedence Table

Higher priority operators are evaluated before lower priority operators.

| Priority | Operator |
|-----------|----------|
| 1 | `()` Parentheses |
| 2 | `**` Exponentiation |
| 3 | `*`, `/`, `//`, `%` |
| 4 | `+`, `-` |
| 5 | Relational Operators (`>`, `<`, `>=`, `<=`, `==`, `!=`) |
| 6 | `not` |
| 7 | `and` |
| 8 | `or` |
| 9 | Assignment (`=`) |

A simple way to remember:

```
()

↓

**

↓

*, /, //, %

↓

+, -

↓

Comparison

↓

not

↓

and

↓

or

↓

=
```

---

# Example 1

```python
81 + 6 / 2
```

### Step 1

Division has higher priority.

```
6 / 2

↓

3.0
```

Expression becomes

```python
81 + 3.0
```

### Step 2

Addition

```
81 + 3.0

↓

84.0
```

Output

```text
84.0
```

---

# Example 2

```python
20 - 12 // 3 ** 2
```

### Step 1

Exponentiation

```
3 ** 2

↓

9
```

Expression

```python
20 - 12 // 9
```

### Step 2

Floor Division

```
12 // 9

↓

1
```

Expression

```python
20 - 1
```

### Step 3

Subtraction

```
20 - 1

↓

19
```

Output

```text
19
```

---

# Example 3

```python
(2 + 3) ** 2 / 25
```

### Step 1

Parentheses

```
2 + 3

↓

5
```

Expression

```python
5 ** 2 / 25
```

### Step 2

Exponentiation

```
5 ** 2

↓

25
```

Expression

```python
25 / 25
```

### Step 3

Division

```
25 / 25

↓

1.0
```

Output

```text
1.0
```

---

# Associativity

Sometimes two operators have the **same precedence**.

In such cases,

Python uses **Associativity**.

Associativity determines the order in which operators of the same precedence are evaluated.

---

# Left-to-Right Associativity

Most arithmetic operators follow

```
Left

↓

Right
```

Examples

- `+`
- `-`
- `*`
- `/`
- `//`
- `%`

---

# Example

```python
5 * 2 // 3
```

Both

```
*

//

```

have the same precedence.

Python evaluates

from

```
Left

↓

Right
```

### Step 1

```
5 × 2

↓

10
```

Expression

```python
10 // 3
```

### Step 2

```
10 // 3

↓

3
```

Output

```text
3
```

---

# Parentheses Override Precedence

Consider

```python
5 * (2 // 3)
```

### Step 1

Parentheses first

```
2 // 3

↓

0
```

Expression

```python
5 * 0
```

### Step 2

Multiplication

```
0
```

Output

```text
0
```

Notice

Without parentheses

```
3
```

With parentheses

```
0
```

Parentheses completely change the result.

---

# Right-to-Left Associativity

Only one arithmetic operator behaves differently.

```
**
```

Exponentiation follows

```
Right

↓

Left
```

---

# Example

```python
2 ** 3 ** 2
```

Many beginners calculate

```
2³

↓

8

↓

8²

↓

64
```

This is **incorrect**.

Python evaluates

from

```
Right

↓

Left
```

### Step 1

```
3²

↓

9
```

Expression

```python
2 ** 9
```

### Step 2

```
2⁹

↓

512
```

Output

```text
512
```

---

# Parentheses Change Associativity

Example

```python
(2 ** 3) ** 2
```

### Step 1

Parentheses

```
2³

↓

8
```

Expression

```python
8 ** 2
```

### Step 2

```
64
```

Output

```text
64
```

Notice

```
2 ** 3 ** 2

↓

512
```

whereas

```
(2 ** 3) ** 2

↓

64
```

---

# Best Practices

## ✅ Use Parentheses

Instead of relying on precedence,

write

```python
total = (price * quantity) + tax
```

This improves readability.

---

## ✅ Avoid Very Complex Expressions

Bad

```python
a+b*c-d/e+f//g**2
```

Better

```python
power = g ** 2
division = f // power
multiplication = b * c
result = a + multiplication - (d / e) + division
```

---

## ✅ Use Meaningful Variable Names

Good

```python
total_price
discount_amount
```

Bad

```python
a
b
c
```

---

## ✅ Use Identity Operators Carefully

Use

```python
is
```

only when checking object identity or special singletons like `None`.

Use

```python
==
```

for value comparison.

Example

```python
if value is None:
    ...
```

---

## ✅ Use Membership Operators for Readability

Instead of

```python
if color == "red" or color == "blue":
```

you can write

```python
if color in ["red", "blue"]:
```

Cleaner and easier to read.

---

# Common Mistakes

### ❌ Confusing `==` with `is`

```python
a == b
```

compares values.

```python
a is b
```

compares object identity.

---

### ❌ Expecting `++` to Work

```python
a++
```

Python raises

```text
SyntaxError
```

---

### ❌ Assuming `and` and `or` Always Return Boolean Values

Incorrect assumption

```python
5 and 6
```

returns

```python
True
```

Actual Output

```python
6
```

Python returns operands, not just Boolean values.

---

### ❌ Forgetting Short-Circuit Evaluation

```python
0 and 10/0
```

No exception occurs because Python never evaluates the second operand.

---

### ❌ Ignoring Operator Precedence

```python
2 + 3 * 4
```

Output

```text
14
```

Not

```text
20
```

because multiplication happens before addition.

---

# Interview Questions

### 1. What is comparison chaining?

Writing multiple comparisons together, such as:

```python
5 < x < 10
```

Python internally evaluates it using the `and` operator.

---

### 2. Difference between `==` and `!=`?

- `==` checks equality.
- `!=` checks inequality.

---

### 3. Difference between `==` and `is`?

| `==` | `is` |
|------|------|
| Compares values | Compares object identity |

---

### 4. What are Truthy and Falsy values?

Falsy values include:

- `False`
- `None`
- `0`
- `0.0`
- `0j`
- `""`
- `[]`
- `{}`
- `()`
- `set()`

Everything else is Truthy.

---

### 5. Why does `5 and 6` return `6`?

Because `5` is Truthy, so `and` returns the second operand.

---

### 6. Why does `5 or 6` return `5`?

Because `5` is Truthy, so `or` immediately returns the first operand.

---

### 7. Does Python support `++` or `--`?

No.

Python has no increment or decrement operators.

---

### 8. What are Identity Operators?

- `is`
- `is not`

They compare object identity.

---

### 9. What are Membership Operators?

- `in`
- `not in`

Used to check whether an element exists inside a collection.

---

### 10. Which operator has the highest precedence?

Parentheses

```
()
```

---

### 11. Which operator has Right-to-Left associativity?

Exponentiation

```python
**
```

---

### 12. Which operators follow Left-to-Right associativity?

- `+`
- `-`
- `*`
- `/`
- `//`
- `%`

---

# Quick Revision

- Python supports cascading relational operators.
- `==` compares values.
- `!=` checks inequality.
- `and`, `or`, and `not` are logical operators.
- `and` returns the first falsy or the last operand.
- `or` returns the first truthy or the last operand.
- Python uses short-circuit evaluation.
- Multiple assignment and tuple unpacking simplify variable assignment.
- Python has no `++` or `--`.
- `is` checks object identity.
- `in` checks membership.
- Parentheses have the highest precedence.
- `**` is right-associative.
- Most arithmetic operators are left-associative.

---

# Summary

In this lecture, we explored advanced operator concepts in Python, including **comparison chaining**, **logical operators**, **assignment operators**, **identity operators**, **membership operators**, and **operator precedence**. We learned how Python evaluates expressions using **truthy** and **falsy** values, how **short-circuit evaluation** improves efficiency, and why `and` and `or` return operands instead of just Boolean values.

We also studied Python's flexible assignment mechanisms, understood why increment (`++`) and decrement (`--`) operators do not exist, and explored the differences between **value equality (`==`)** and **object identity (`is`)**. Finally, we examined operator precedence and associativity, which are essential for correctly evaluating complex expressions.

Mastering these concepts will help you write cleaner, more efficient, and more Pythonic code while avoiding common logical and syntactic mistakes.
