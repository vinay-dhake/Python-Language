# 🐍 Python Logical Operators (Lecture 13)

> Complete GitHub Notes on Python Logical Operators (`and`, `or`, `not`), Boolean Logic, Truthy & Falsy Values, Short-Circuit Evaluation, Non-Boolean Behavior, Practical Examples, Best Practices, Interview Questions, and Summary.

---

# 📚 Table of Contents

- Introduction
- What are Logical Operators?
- Why Do We Need Logical Operators?
- Types of Logical Operators
- Logical AND (`and`)
- Logical OR (`or`)
- Logical NOT (`not`)
- Truth Tables
- Logical Operators with Boolean Values
- Truthy & Falsy Values
- Logical Operators with Non-Boolean Values
- Short-Circuit Evaluation
- Practical Examples
- Best Practices
- Common Mistakes
- Interview Questions
- Quick Revision
- Summary

---

# Introduction

Until now, we have learned arithmetic operators, relational operators, assignment operators, identity operators, and membership operators.

However, real-world applications rarely depend on a single condition.

For example,

- Is a student **older than 18** **and** has passed the entrance exam?
- Is the user **an admin** **or** a moderator?
- Is a value **not** empty?

To solve such problems, Python provides **Logical Operators**.

Logical operators allow us to combine multiple conditions and produce a single result.

They are heavily used in:

- `if` statements
- `elif` statements
- `while` loops
- Login systems
- Form validation
- Authentication
- Searching and filtering
- Decision-making algorithms

---

# What are Logical Operators?

Logical operators combine two or more conditions and return a result based on Boolean logic.

Python provides three logical operators.

| Operator | Meaning |
|----------|---------|
| `and` | Logical AND |
| `or` | Logical OR |
| `not` | Logical NOT |

Unlike C, C++, and Java, Python uses **keywords** instead of symbols.

| C/C++/Java | Python |
|------------|---------|
| `&&` | `and` |
| `||` | `or` |
| `!` | `not` |

This makes Python code easier to read.

---

# Why Do We Need Logical Operators?

Imagine writing the following condition.

> The student must score above 40 **and** have attendance above 75%.

This requires checking **two conditions simultaneously**.

Similarly,

A user should be allowed access if

- they are an Admin **or**
- they are a Teacher.

Without logical operators,

writing such conditions would be impossible.

---

# Types of Logical Operators

Python has only three logical operators.

## 1. `and`

Returns **True** only if **both conditions are True**.

---

## 2. `or`

Returns **True** if **at least one condition is True**.

---

## 3. `not`

Reverses the Boolean value.

```
True

↓

False

False

↓

True
```

---

# Logical AND (`and`)

The `and` operator returns **True** only when **both operands are True**.

If even one operand is False,

the final result becomes False.

---

## Truth Table

| A | B | A and B |
|---|---|----------|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

---

# Example 1 (From the Lecture)

```python
a = 40
b = 20
c = 50

print(a > b and a > c)
```

Step-by-step

```
40 > 20

↓

True

40 > 50

↓

False

True and False

↓

False
```

Output

```text
False
```

---

# Example 2 (From the Lecture)

```python
a = 40
b = 20
c = 50

print(a > b and c > a)
```

Evaluation

```
40 > 20

↓

True

50 > 40

↓

True

True and True

↓

True
```

Output

```text
True
```

These examples demonstrate that `and` only returns `True` when **both** comparisons succeed. :contentReference[oaicite:1]{index=1}

---

# Logical OR (`or`)

The `or` operator returns **True** if **at least one operand is True**.

It returns False only when **both operands are False**.

---

## Truth Table

| A | B | A or B |
|---|---|---------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

---

# Example 1 (From the Lecture)

```python
a = 40
b = 20
c = 50

print(a > b or a > c)
```

Evaluation

```
40 > 20

↓

True

40 > 50

↓

False

True or False

↓

True
```

Output

```text
True
```

---

# Example 2 (From the Lecture)

```python
a = 40
b = 20
c = 50

print(b > a or b > c)
```

Evaluation

```
20 > 40

↓

False

20 > 50

↓

False

False or False

↓

False
```

Output

```text
False
```

These examples show that `or` requires only **one** condition to be true. :contentReference[oaicite:2]{index=2}

---

# Logical NOT (`not`)

The `not` operator works on only **one operand**.

It simply reverses the Boolean value.

---

## Truth Table

| A | not A |
|---|-------|
| True | False |
| False | True |

---

# Example 1 (From the Lecture)

```python
a = True

print(not a)
```

Output

```text
False
```

---

# Example 2 (From the Lecture)

```python
b = False

print(not b)
```

Output

```text
True
```

The `not` operator is commonly used to invert conditions inside `if` statements. :contentReference[oaicite:3]{index=3}

---

# Summary of Boolean Logical Operators

| Operator | Condition | Result |
|-----------|-----------|--------|
| `and` | Both operands must be True | True |
| `or` | At least one operand must be True | True |
| `not` | Reverses Boolean value | Opposite Boolean |

---

# Transition to Non-Boolean Operands

One of Python's most unique features is that logical operators are **not limited to Boolean values**.

They can also work with:

- Integers
- Floating-point numbers
- Strings
- Lists
- Tuples
- Dictionaries
- Sets
- None

Understanding this behavior is essential because it is frequently asked in interviews and widely used in professional Python code.
==============================================================================================================================================================
---

# Logical Operators with Non-Boolean Values

One of Python's most interesting features is that logical operators are **not limited to Boolean values**.

Unlike many programming languages, Python allows logical operators to work with:

- Integers
- Floating-point numbers
- Strings
- Lists
- Tuples
- Dictionaries
- Sets
- None

However, before understanding this behavior, we must understand two important concepts.

---

# Important Rule 1: Truthy and Falsy Values

Every object in Python has a Boolean value.

Some objects behave as **False**, while all others behave as **True**.

Python internally converts objects into Boolean values whenever logical operators are used.

---

# Falsy Values

The following values are considered **Falsy**.

```python
False
None
0
0.0
0j
""
[]
()
{}
set()
```

Example

```python
print(bool(0))
print(bool(""))
print(bool([]))
print(bool(None))
```

Output

```text
False
False
False
False
```

These are the only commonly encountered values that behave as `False` in Boolean contexts. :contentReference[oaicite:0]{index=0}

---

# Truthy Values

Everything that is **not falsy** is considered **Truthy**.

Examples

```python
10
-5
3.14
"Python"
"Sachin"
[10]
(True)
```

Example

```python
print(bool(10))
print(bool("Hello"))
print(bool([1, 2]))
```

Output

```text
True
True
True
```

---

# Important Rule 2

When logical operators are applied to **non-Boolean operands**, Python usually **does not return `True` or `False`**.

Instead, it returns **one of the original operands**.

This is one of the most important Python interview concepts.

The lecture PDF specifically highlights this behavior before introducing the examples. :contentReference[oaicite:1]{index=1}

---

# Rules for `and`

The `and` operator follows these rules:

### Rule 1

If the **first operand is Falsy**,

return the **first operand immediately**.

The second operand is **never evaluated**.

---

### Rule 2

If the **first operand is Truthy**,

evaluate and return the **second operand**.

---

# Why Does This Happen?

Python uses **Short-Circuit Evaluation**.

The moment Python can determine the final result,

it stops evaluating the remaining expression.

This improves efficiency and avoids unnecessary computations.

---

# Example 1 (From the Lecture)

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

# Example 2 (From the Lecture)

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

# Example 3 (From the Lecture)

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

Python never evaluates

```
10
```

Output

```text
0
```

---

# Example 4 (From the Lecture)

```python
print(6 and 0)
```

Evaluation

```
6

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

# Example 5 (From the Lecture)

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

# Example 6 (From the Lecture)

```python
print("Sachin" and 0)
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
0
```

---

# Example 7 (From the Lecture)

```python
print("Indore" and "Bhopal")
```

Evaluation

```
"Indore"

↓

Truthy

↓

Return second operand
```

Output

```text
Bhopal
```

---

# Example 8 (From the Lecture)

```python
print("Bhopal" and "Indore")
```

Evaluation

```
"Bhopal"

↓

Truthy

↓

Return second operand
```

Output

```text
Indore
```

These examples show that `and` does **not** return a Boolean value when used with non-Boolean objects. It returns one of the operands depending on their truthiness. :contentReference[oaicite:2]{index=2}

---

# Short-Circuit Evaluation

Short-circuit evaluation means that Python stops evaluating an expression as soon as the final result is known.

This not only improves performance but can also prevent runtime errors.

---

# Example 9 (From the Lecture)

```python
print(10 / 0 and 0)
```

Evaluation

Python first evaluates

```python
10 / 0
```

Immediately,

```
ZeroDivisionError
```

is raised.

Python never reaches

```python
and 0
```

Output

```text
ZeroDivisionError
```

---

# Example 10 (From the Lecture)

```python
print(0 and 10 / 0)
```

Evaluation

```
0

↓

Falsy

↓

Return first operand
```

The second operand is **never evaluated**.

Therefore,

Output

```text
0
```

No exception occurs because of short-circuit evaluation. This behavior is one of the key demonstrations in the lecture. :contentReference[oaicite:3]{index=3}

---

# Summary of `and`

| Expression | Output | Reason |
|------------|--------|--------|
| `5 and 6` | `6` | First operand is Truthy |
| `5 and 0` | `0` | First Truthy, return second |
| `0 and 10` | `0` | First Falsy |
| `6 and 0` | `0` | First Truthy |
| `"Sachin" and 10` | `10` | String is Truthy |
| `"Sachin" and 0` | `0` | Second operand returned |
| `"Indore" and "Bhopal"` | `"Bhopal"` | Second operand returned |
| `"Bhopal" and "Indore"` | `"Indore"` | Second operand returned |
| `10/0 and 0` | `ZeroDivisionError` | First operand evaluated first |
| `0 and 10/0` | `0` | Short-circuit prevents evaluation |

---
=============================================================================================================================================================
---

# Rules for `or`

The `or` operator follows behavior opposite to `and`.

## Rule 1

If the **first operand is Truthy**,

Python immediately returns the **first operand**.

The second operand is **never evaluated**.

---

## Rule 2

If the **first operand is Falsy**,

Python evaluates and returns the **second operand**.

---

# Why Does `or` Behave This Way?

The purpose of the `or` operator is to find the **first Truthy value**.

As soon as Python encounters a Truthy operand,

it already knows the entire expression will evaluate as True.

Therefore,

it stops evaluating the remaining operands.

This optimization is known as **Short-Circuit Evaluation**.

---

# Example 1 (From the Lecture)

```python
print(5 or 6)
```

Evaluation

```
5

↓

Truthy

↓

Return first operand
```

Output

```text
5
```

---

# Example 2 (From the Lecture)

```python
print(5 or 0)
```

Evaluation

```
5

↓

Truthy

↓

Return first operand
```

Output

```text
5
```

---

# Example 3 (From the Lecture)

```python
print(0 or 10)
```

Evaluation

```
0

↓

Falsy

↓

Evaluate second operand

↓

10
```

Output

```text
10
```

---

# Example 4 (From the Lecture)

```python
print(6 or 0)
```

Evaluation

```
6

↓

Truthy

↓

Return first operand
```

Output

```text
6
```

---

# Example 5 (From the Lecture)

```python
print("Sachin" or 10)
```

Evaluation

```
"Sachin"

↓

Truthy

↓

Return first operand
```

Output

```text
Sachin
```

---

# Example 6 (From the Lecture)

```python
print("Sachin" or 0)
```

Output

```text
Sachin
```

Again,

Python returns the first Truthy operand.

---

# Example 7 (From the Lecture)

```python
print("Indore" or "Bhopal")
```

Output

```text
Indore
```

---

# Example 8 (From the Lecture)

```python
print("Bhopal" or "Indore")
```

Output

```text
Bhopal
```

These examples illustrate that `or` returns the **first Truthy operand**, not necessarily `True`. :contentReference[oaicite:0]{index=0}

---

# Short-Circuit Evaluation with `or`

Short-circuit evaluation also applies to the `or` operator.

If the first operand is Truthy,

Python skips evaluating the second operand.

---

# Example 9 (From the Lecture)

```python
print(0 or 10 / 0)
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
10 / 0
```

Output

```text
ZeroDivisionError
```

---

# Example 10 (From the Lecture)

```python
print(10 / 0 or 0)
```

Python starts by evaluating

```python
10 / 0
```

Immediately,

```
ZeroDivisionError
```

is raised.

Python never reaches

```python
or 0
```

---

# Summary of `or`

| Expression | Output | Reason |
|------------|--------|--------|
| `5 or 6` | `5` | First operand is Truthy |
| `5 or 0` | `5` | First Truthy |
| `0 or 10` | `10` | First Falsy, return second |
| `6 or 0` | `6` | First Truthy |
| `"Sachin" or 10` | `"Sachin"` | First Truthy |
| `"Sachin" or 0` | `"Sachin"` | First Truthy |
| `"Indore" or "Bhopal"` | `"Indore"` | First Truthy |
| `"Bhopal" or "Indore"` | `"Bhopal"` | First Truthy |
| `0 or 10/0` | `ZeroDivisionError` | Second operand evaluated |
| `10/0 or 0` | `ZeroDivisionError` | Error before `or` can short-circuit |

---

# Logical NOT (`not`) with Non-Boolean Values

Unlike `and` and `or`,

the `not` operator **always returns a Boolean value**.

It first converts the operand into its Boolean equivalent,

then reverses it.

---

## Rule of `not`

- Truthy value → `False`
- Falsy value → `True`

---

# Example 1 (From the Lecture)

```python
print(not 5)
```

Evaluation

```
5

↓

Truthy

↓

False
```

Output

```text
False
```

---

# Example 2 (From the Lecture)

```python
print(not 0)
```

Evaluation

```
0

↓

Falsy

↓

True
```

Output

```text
True
```

---

# Example 3 (From the Lecture)

```python
print(not "Sachin")
```

Evaluation

```
"Sachin"

↓

Truthy

↓

False
```

Output

```text
False
```

---

# Example 4 (From the Lecture)

```python
print(not "")
```

Evaluation

```
""

↓

Falsy

↓

True
```

Output

```text
True
```

These examples demonstrate that `not` always returns either `True` or `False`, unlike `and` and `or`, which often return one of their operands. :contentReference[oaicite:1]{index=1}

---

# Difference Between `and`, `or`, and `not`

| Operator | Returns |
|-----------|---------|
| `and` | First Falsy operand, otherwise the last operand |
| `or` | First Truthy operand, otherwise the last operand |
| `not` | Always a Boolean value (`True` or `False`) |

---

# Real-World Applications

Logical operators are used extensively in Python programs.

### Login Authentication

```python
username == "admin" and password == "python123"
```

Both conditions must be true.

---

### Scholarship Eligibility

```python
marks >= 85 and attendance >= 75
```

A student qualifies only if both requirements are satisfied.

---

### Admin Access

```python
role == "Admin" or role == "Moderator"
```

Either role is allowed access.

---

### Default Values Using `or`

```python
name = input("Enter your name: ") or "Guest"
```

If the user presses **Enter** without typing anything,

`input()` returns an empty string (`""`), which is Falsy.

Therefore,

`"Guest"` becomes the default value.

This is a clean, Pythonic technique commonly used in real-world code.

---
============================================================================================================================================================
---

# Best Practices

Following good programming practices makes your code more readable, maintainable, and less prone to bugs.

---

## ✅ Use Parentheses for Complex Conditions

Although Python follows operator precedence rules, parentheses make conditions much easier to understand.

Instead of writing

```python
marks > 40 and attendance > 75 or sports_quota
```

write

```python
(marks > 40 and attendance > 75) or sports_quota
```

This clearly expresses your intended logic and avoids confusion.

---

## ✅ Use Meaningful Variable Names

Good

```python
is_logged_in = True
has_permission = False
```

Bad

```python
a = True
b = False
```

Meaningful names make programs self-explanatory.

---

## ✅ Use `or` for Default Values

Python programmers often use the `or` operator to provide fallback values.

Example

```python
username = input("Enter username: ") or "Guest"

print(username)
```

If the user enters nothing,

```
Guest
```

is automatically assigned.

This is cleaner than writing a full `if-else` block.

---

## ✅ Keep Logical Expressions Simple

Instead of writing one very long condition,

break it into smaller parts.

Example

```python
is_eligible = marks >= 40 and attendance >= 75

if is_eligible:
    print("Eligible")
```

This improves readability and debugging.

---

## ✅ Understand Truthy and Falsy Values

Never assume that only `True` and `False` participate in logical operations.

Remember:

- Non-zero numbers → Truthy
- Non-empty strings → Truthy
- Empty containers → Falsy
- `None` → Falsy

Understanding these rules prevents unexpected behavior.

---

# Common Mistakes

## ❌ Mistake 1

Assuming `and` always returns `True` or `False`.

Example

```python
print(5 and 6)
```

Many beginners expect

```text
True
```

Actual Output

```text
6
```

Python returns the second operand because the first operand is Truthy.

---

## ❌ Mistake 2

Assuming `or` always returns `True` or `False`.

Example

```python
print(5 or 6)
```

Expected by beginners

```text
True
```

Actual Output

```text
5
```

Python returns the first Truthy operand.

---

## ❌ Mistake 3

Ignoring Short-Circuit Evaluation

Example

```python
print(0 and 10 / 0)
```

Many beginners expect a `ZeroDivisionError`.

Actual Output

```text
0
```

Reason

The second operand is never evaluated.

---

## ❌ Mistake 4

Confusing Empty and Non-Empty Strings

```python
bool("")
```

Output

```text
False
```

Whereas

```python
bool("False")
```

Output

```text
True
```

Because `"False"` is **not empty**.

---

## ❌ Mistake 5

Using `== True`

Instead of

```python
if is_logged_in == True:
```

write

```python
if is_logged_in:
```

It is shorter and follows Python's style guidelines.

---

## ❌ Mistake 6

Forgetting That `not` Always Returns a Boolean

Example

```python
print(not 10)
```

Output

```text
False
```

Unlike `and` and `or`, `not` **always** returns either `True` or `False`.

---

# Interview Questions

## 1. How many logical operators does Python provide?

Three:

- `and`
- `or`
- `not`

---

## 2. Difference between `and` and `or`?

| `and` | `or` |
|--------|-------|
| Returns first Falsy operand, otherwise the last operand | Returns first Truthy operand, otherwise the last operand |

---

## 3. What is Short-Circuit Evaluation?

Python stops evaluating an expression as soon as the final result becomes known.

Example

```python
0 and 10 / 0
```

The second operand is never evaluated.

---

## 4. What are Truthy and Falsy Values?

Falsy values include:

- `False`
- `None`
- `0`
- `0.0`
- `0j`
- `""`
- `[]`
- `()`
- `{}`
- `set()`

Everything else is Truthy.

---

## 5. Why does `5 and 6` return `6`?

Because `5` is Truthy.

The `and` operator returns the second operand when the first operand is Truthy.

---

## 6. Why does `5 or 6` return `5`?

Because `5` is already Truthy.

The `or` operator immediately returns the first Truthy operand.

---

## 7. Why does `not 0` return `True`?

Because

```python
0
```

is Falsy.

`not` reverses it.

---

## 8. Why does `not "Sachin"` return `False`?

Because

```python
"Sachin"
```

is a non-empty string.

Non-empty strings are Truthy.

---

## 9. Difference between Boolean and Non-Boolean Logical Operations?

With Boolean operands,

logical operators return Boolean results.

With non-Boolean operands,

`and` and `or` return one of the operands,

while `not` always returns a Boolean.

---

## 10. Why are logical operators important?

They are essential for:

- Decision making
- Validation
- Authentication
- Searching
- Filtering
- Loops
- Conditional statements

---

# Quick Revision

- Python provides three logical operators:
  - `and`
  - `or`
  - `not`
- `and` returns the first Falsy operand, otherwise the last operand.
- `or` returns the first Truthy operand, otherwise the last operand.
- `not` always returns a Boolean value.
- Python uses Short-Circuit Evaluation.
- Empty strings, empty collections, `0`, and `None` are Falsy.
- Non-empty strings and non-zero numbers are Truthy.
- Logical operators work with both Boolean and non-Boolean values.
- Using `or` for default values is a common Python idiom.

---

# Key Takeaways

- Logical operators are the foundation of decision-making in Python.
- Python extends logical operators beyond simple Boolean values by allowing them to work directly with objects.
- Understanding Truthy and Falsy values helps explain why expressions like `5 and 6` or `0 or 10` behave the way they do.
- Short-circuit evaluation improves both performance and safety by avoiding unnecessary computations.
- Mastering these concepts makes your code more concise, readable, and Pythonic.

---

# Summary

In this lecture, we explored Python's three logical operators—`and`, `or`, and `not`—and learned how they behave with both Boolean and non-Boolean operands. We studied Truthy and Falsy values, examined Python's short-circuit evaluation strategy, and worked through numerous examples involving integers, strings, and expressions that could raise exceptions.

We also saw practical uses of logical operators, such as providing default values with `or` and combining multiple conditions in real-world applications. These concepts form the backbone of conditional programming in Python and are essential for writing efficient, readable, and professional Python code.

---
