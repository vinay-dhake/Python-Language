# 🐍 Python Miscellaneous Operators (Lecture 13 Part 2 (Lec 14 in slide)

> Complete GitHub Notes on Assignment Operators, Compound Assignment Operators, Identity Operators, Membership Operators, Operator Precedence, Associativity, and Python's Increment & Decrement Behavior.

---

# 📚 Table of Contents

- Introduction
- Assignment Operators
- Types of Assignment
- Multiple Assignment
- Tuple Unpacking
- Compound Assignment Operators
- Increment & Decrement Operators
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

Operators are one of the most fundamental building blocks of every programming language.

In previous lectures, we studied:

- Arithmetic Operators
- Relational Operators
- Logical Operators

In this lecture, we will study another important category known as **Miscellaneous Operators**.

These operators help us

- Assign values efficiently
- Check object identity
- Check membership inside collections
- Understand operator precedence
- Write shorter and cleaner code

Mastering these operators is essential because they are used almost everywhere in Python programming.

---

# Assignment Operators

Assignment operators are used to assign values to variables.

The most commonly used assignment operator is

```python
=
```

Syntax

```python
variable = value
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

After execution

```
a

↓

10
```

The assignment operator creates a reference from the variable to the object stored in memory.

Python uses assignment operators extensively because variables are created simply by assigning values.

The PDF introduces the assignment operator as the basic mechanism for assigning values to declared variables. :contentReference[oaicite:0]{index=0}

---

# Why Assignment Operators are Needed

Imagine writing

```python
marks = 95
```

Without assignment,

Python would have no way of storing

```
95
```

inside a variable.

Assignment operators provide the connection between

```
Variable

↓

Object
```

---

# Types of Assignment

Python supports two common assignment styles.

## 1. Same Value Assignment

Multiple variables can point to the same value.

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

Python first evaluates

```
10
```

and then assigns it to every variable.

Internally,

all three variables reference the same integer object because integers are immutable.

---

# Different Value Assignment

Python can also assign different values simultaneously.

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

This feature makes Python code shorter and more readable than many other programming languages.

The lecture slides demonstrate both assigning the same value to multiple variables and assigning different values using comma-separated variables. :contentReference[oaicite:1]{index=1}

---

# Tuple Unpacking

When multiple values are assigned together,

Python internally creates a tuple.

Example

```python
a, b, c = 100, 200, 300
```

Internally it behaves approximately like

```python
(a, b, c) = (100, 200, 300)
```

Each value is unpacked into the corresponding variable.

This process is known as

> **Tuple Unpacking**

---

# Rules of Tuple Unpacking

The number of variables on the left side

must exactly match

the number of values on the right side.

Otherwise,

Python raises an exception.

---

# Example 1

```python
a, b, c = 10, 20

print(a, b, c)
```

Output

```text
ValueError: not enough values to unpack
```

### Why?

Python expected

```
3 variables
```

but received only

```
2 values
```

Therefore,

Python cannot assign a value to

```
c
```

and raises an error.

---

# Example 2

```python
a, b, c = 10, 20, 30, 40

print(a, b, c)
```

Output

```text
ValueError: too many values to unpack
```

### Why?

Python expected

```
3 variables
```

but received

```
4 values
```

One value remains unused,

so Python raises

```text
ValueError
```

These unpacking errors are illustrated in the "Guess the Output" section of the PDF. :contentReference[oaicite:2]{index=2}

---

# Important Rule

Always ensure

```
Number of Variables

=

Number of Values
```

Correct

```python
a, b, c = 1, 2, 3
```

Incorrect

```python
a, b = 1
```

Incorrect

```python
a, b = 1, 2, 3
```

Both produce

```text
ValueError
```

---

# Advantages of Multiple Assignment

Python's multiple assignment provides several benefits.

- Less code
- Better readability
- Faster assignment
- Cleaner syntax
- Easy swapping of variables

Example

```python
a = 10
b = 20

a, b = b, a

print(a, b)
```

Output

```text
20 10
```

Unlike many programming languages,

Python does not require a temporary variable for swapping.

---

# Key Points

- `=` assigns values to variables.
- Python supports assigning one value to multiple variables.
- Python supports assigning multiple values to multiple variables.
- Multiple assignment uses tuple unpacking internally.
- The number of variables and values must always match.
- Otherwise, Python raises a `ValueError`.

---
==============================================================================================================================================================
---

# Compound Assignment Operators

Writing the variable name repeatedly after every arithmetic operation makes the code longer and less readable.

For example,

Instead of writing

```python
a = a + 5
```

Python provides a shorter way

```python
a += 5
```

This type of operator is called a **Compound Assignment Operator**.

A compound assignment operator performs two operations in one step:

1. Performs the arithmetic operation.
2. Stores the result back into the same variable.

---

# Why Use Compound Assignment Operators?

Consider the following example.

Without compound assignment

```python
salary = 50000

salary = salary + 5000

print(salary)
```

Output

```text
55000
```

Using compound assignment

```python
salary = 50000

salary += 5000

print(salary)
```

Output

```text
55000
```

Both programs produce the same result.

However,

```python
salary += 5000
```

is shorter, cleaner, and easier to understand.

---

# List of Compound Assignment Operators

| Operator | Equivalent Expression |
|-----------|------------------------|
| `+=` | `a = a + b` |
| `-=` | `a = a - b` |
| `*=` | `a = a * b` |
| `/=` | `a = a / b` |
| `%=` | `a = a % b` |
| `//=` | `a = a // b` |
| `**=` | `a = a ** b` |

These operators combine an arithmetic operation with assignment.

---

# Addition Assignment (`+=`)

Example

```python
a = 10

a += 5

print(a)
```

Internal Working

```python
a = a + 5
```

becomes

```python
10 + 5

↓

15
```

Output

```text
15
```

---

# Subtraction Assignment (`-=`)

Example

```python
a = 25

a -= 10

print(a)
```

Internal Working

```python
a = a - 10
```

Output

```text
15
```

---

# Multiplication Assignment (`*=`)

Example

```python
a = 8

a *= 4

print(a)
```

Internal Working

```python
8 × 4

↓

32
```

Output

```text
32
```

---

# Division Assignment (`/=`)

Example

```python
a = 20

a /= 5

print(a)
```

Output

```text
4.0
```

Notice that `/=` always produces a floating-point value because `/` performs floating-point division.

---

# Floor Division Assignment (`//=`)

Example

```python
a = 17

a //= 5

print(a)
```

Internal Working

```python
17 // 5

↓

3
```

Output

```text
3
```

---

# Modulus Assignment (`%=`)

Example

```python
a = 17

a %= 5

print(a)
```

Internal Working

```python
17 % 5

↓

2
```

Output

```text
2
```

---

# Exponentiation Assignment (`**=`)

Example

```python
a = 2

a **= 5

print(a)
```

Internal Working

```python
2 ** 5

↓

32
```

Output

```text
32
```

The lecture notes list all seven compound assignment operators and their shorthand behavior. :contentReference[oaicite:0]{index=0}

---

# Advantages of Compound Assignment

Compound assignment operators are widely used because they

- reduce typing,
- improve readability,
- simplify updates,
- make loops cleaner,
- reduce repetition.

For example,

instead of writing

```python
count = count + 1
```

we simply write

```python
count += 1
```

---

# Does Python Support `++` and `--`?

One of the biggest surprises for beginners coming from C, C++, or Java is that **Python does not support increment (`++`) or decrement (`--`) operators**.

Languages like C, C++, and Java allow

```cpp
a++;
++a;
a--;
--a;
```

Python does **not**.

---

# Why Doesn't Python Have `++`?

Python's philosophy emphasizes simplicity and readability.

Instead of using special increment operators,

Python encourages writing

```python
a += 1
```

or

```python
a = a + 1
```

This keeps the language simple and avoids confusion between pre-increment and post-increment operations.

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

Python cannot interpret `a++` as an increment operation.

Instead,

it considers the second `+` incomplete,

which makes the statement invalid.

---

# What About `++a`?

Many beginners believe

```python
++a
```

increments the variable.

Actually,

it does **not**.

Example

```python
a = 10

print(++a)
```

Python interprets this as

```python
+(+(10))
```

The unary plus operator simply returns the number unchanged.

Evaluation

```
+(+(10))

↓

10
```

Output

```text
10
```

Notice that

```
a

↓

10
```

still remains unchanged.

No increment happens.

The lecture demonstrates this behavior by showing that multiple unary plus signs do not increase the value. :contentReference[oaicite:1]{index=1}

---

# Understanding Unary Plus

The unary plus operator

```python
+
```

does **not** add anything.

It simply indicates that the number is positive.

Example

```python
a = 15

print(+a)
```

Output

```text
15
```

Even writing

```python
++++a
```

still means

```python
+(+(+(+15)))
```

Output

```text
15
```

---

# What About `--a`?

Similarly,

```python
--a
```

is **not** a decrement operation.

Example

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

the variable is **not decremented**.

---

# Multiple Unary Minus Operators

Example

```python
a = 10

print(-----a)
```

Evaluation

```
-(-(-(-(-10))))
```

Step-by-step

```
-10

↓

10

↓

-10

↓

10

↓

-10
```

Output

```text
-10
```

Python simply keeps applying unary minus repeatedly.

There is **no decrement operator** involved.

---

# Important Interview Point

The following statements are **not equivalent**.

```python
++a
```

means

```python
+(+(a))
```

Whereas

```cpp
++a
```

in C++ means

> Increment first, then use the value.

Similarly,

Python's

```python
--a
```

is simply repeated unary negation,

not a decrement.

---

# Key Points

- Python has **no** increment operator.
- Python has **no** decrement operator.
- `++a` does **not** increment the value.
- `--a` does **not** decrement the value.
- Use `+= 1` instead of `++`.
- Use `-= 1` instead of `--`.

---
=============================================================================================================================================================
---

# Identity Operators

Identity operators are used to check whether two variables refer to the **same object in memory**.

Unlike the equality operator (`==`), which compares values, identity operators compare **memory references**.

Python provides two identity operators.

| Operator | Meaning |
|----------|---------|
| `is` | Returns `True` if both variables refer to the same object |
| `is not` | Returns `True` if both variables refer to different objects |

---

# Identity vs Equality

Many beginners confuse `==` and `is`.

Although they sometimes produce the same result, they perform completely different operations.

| `==` | `is` |
|------|------|
| Compares values | Compares memory addresses |
| Checks equality | Checks identity |
| Used for value comparison | Used for object comparison |

Example

```python
a = [10, 20]
b = [10, 20]

print(a == b)
print(a is b)
```

Output

```text
True
False
```

### Explanation

Both lists contain the same values.

Therefore,

```python
a == b
```

returns

```text
True
```

However,

Python creates **two different list objects**.

Therefore,

```python
a is b
```

returns

```text
False
```

---

# The `is` Operator

The `is` operator checks whether two variables point to the **same object**.

Syntax

```python
a is b
```

If both variables refer to the same object,

Python returns

```text
True
```

Otherwise,

```text
False
```

---

# Example

```python
a = 2
b = 3

print(a is b)
```

Output

```text
False
```

### Explanation

Variable

```
a

↓

2
```

Variable

```
b

↓

3
```

Since both variables refer to different integer objects,

Python returns

```text
False
```

This simple example is used in the lecture to introduce the `is` operator. :contentReference[oaicite:0]{index=0}

---

# Using `is` with `type()`

Identity operators are commonly used while checking object types.

Example

```python
a = 100

print(type(a) is int)
```

Output

```text
True
```

### Why?

```python
type(a)
```

returns

```python
<class 'int'>
```

which is exactly the same object as

```python
int
```

Therefore,

```python
type(a) is int
```

returns

```text
True
```

---

Another example

```python
a = 100

print(type(a) is float)
```

Output

```text
False
```

Because

```
int

≠

float
```

---

# The `is not` Operator

`is not` performs the opposite operation.

Syntax

```python
a is not b
```

It returns

```text
True
```

when both variables refer to different objects.

---

# Example

```python
a = "Delhi"
b = "Delhi"

print(a is not b)
```

Output

```text
False
```

### Explanation

Python usually **interns** simple string literals.

Both variables point to the same string object.

Therefore,

```
Same Object

↓

False
```

---

# Example

```python
a = "Delhi"
b = "delhi"

print(a is not b)
```

Output

```text
True
```

### Why?

Python is case-sensitive.

```
Delhi

≠

delhi
```

Therefore,

two different string objects are created.

The lecture uses these examples to demonstrate the behavior of `is not` with cached strings. :contentReference[oaicite:1]{index=1}

---

# When Should You Use Identity Operators?

Identity operators are useful when

- Checking whether two references point to the same object.
- Comparing an object with `None`.
- Performing explicit type checks.

Example

```python
data = None

if data is None:
    print("No Data")
```

Using

```python
is None
```

is considered better practice than

```python
== None
```

---

# Membership Operators

Membership operators check whether an element exists inside a collection.

Python provides two membership operators.

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

### Explanation

The substring

```
om
```

appears inside

```
Welcome
```

Therefore,

Python returns

```text
True
```

---

# Another Example

```python
print("mom" in "Welcome")
```

Output

```text
False
```

### Why?

The substring

```
mom
```

does not appear anywhere inside

```
Welcome
```

Therefore,

Python returns

```text
False
```

These string membership examples appear in the lecture slides to explain how `in` works with strings. :contentReference[oaicite:2]{index=2}

---

# Using `not in`

`not in` checks whether an element is **absent** from a collection.

---

# Example

```python
print(4 not in [1, 2, 3, 5])
```

Output

```text
True
```

### Explanation

The list contains

```
1
2
3
5
```

The value

```
4
```

is missing.

Therefore,

Python returns

```text
True
```

---

# Example

```python
x = 5

print(x not in [1, 2, 3, 5])
```

Output

```text
False
```

### Why?

The value

```
5
```

already exists inside the list.

Therefore,

the statement

```
5 not in [...]
```

is incorrect.

Python returns

```text
False
```

---

# Membership Operators with Other Collections

They also work with tuples.

Example

```python
print(20 in (10, 20, 30))
```

Output

```text
True
```

---

They work with sets.

Example

```python
print(50 in {10, 20, 30})
```

Output

```text
False
```

---

They work with dictionaries.

Example

```python
student = {
    "name": "Rahul",
    "age": 20
}

print("name" in student)
```

Output

```text
True
```

### Important Note

For dictionaries,

membership operators check **keys**, not values.

---

# Real-Life Applications

Membership operators are frequently used in real-world programs.

Example

```python
allowed_users = ["admin", "teacher", "student"]

user = "teacher"

print(user in allowed_users)
```

Output

```text
True
```

Another example

```python
email = "abc@gmail.com"

print("@" in email)
```

Output

```text
True
```

This is commonly used while validating email addresses.

---

# Key Points

- `is` compares object identity.
- `==` compares values.
- `is not` checks whether two references are different.
- `in` checks membership.
- `not in` checks absence.
- Membership operators work with strings, lists, tuples, sets, and dictionaries.
- Dictionary membership checks keys, not values.

---
=============================================================================================================================================================
---

# Operator Precedence

In Python, an expression may contain multiple operators.

Example

```python
10 + 5 * 2
```

A natural question is:

> **Which operation will Python perform first?**

Python follows a predefined priority system known as **Operator Precedence**.

Operator precedence determines **which operator is evaluated first** when multiple operators appear in the same expression.

Understanding operator precedence is essential because it ensures that expressions are evaluated correctly and predictably.

---

# Why Do We Need Operator Precedence?

Consider the expression

```python
10 + 5 * 2
```

If addition happened first,

```
10 + 5

↓

15

↓

15 × 2

↓

30
```

If multiplication happened first,

```
5 × 2

↓

10

↓

10 + 10

↓

20
```

Both results are different.

To remove this ambiguity,

Python follows a fixed order of execution called **Operator Precedence**.

---

# Operator Precedence Table

The following table lists common operators from **highest** to **lowest** priority.

| Priority | Operator | Description |
|-----------|----------|-------------|
| 1 | `()` | Parentheses |
| 2 | `**` | Exponentiation |
| 3 | `*`, `/`, `//`, `%` | Multiplication, Division, Floor Division, Modulus |
| 4 | `+`, `-` | Addition, Subtraction |
| 5 | `>`, `<`, `>=`, `<=`, `==`, `!=` | Relational Operators |
| 6 | `not` | Logical NOT |
| 7 | `and` | Logical AND |
| 8 | `or` | Logical OR |
| 9 | `=` | Assignment |

---

# Easy Way to Remember

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

Exponentiation has the highest priority after parentheses.

```
3 ** 2

↓

9
```

Expression becomes

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

Expression becomes

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

Expression becomes

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

Expression becomes

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

The lecture includes these examples to demonstrate how precedence determines the order of evaluation. :contentReference[oaicite:0]{index=0}

---

# Associativity

Sometimes two operators have the **same precedence**.

In that case,

Python uses **Associativity**.

Associativity determines the direction in which operators of the same priority are evaluated.

There are two types:

- Left-to-Right Associativity
- Right-to-Left Associativity

---

# Left-to-Right Associativity

Most arithmetic operators follow

```
Left

↓

Right
```

These include

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

Therefore,

Python evaluates from left to right.

### Step 1

```
5 × 2

↓

10
```

Expression becomes

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

# Parentheses Override Associativity

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

Expression becomes

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

Parentheses always have the highest priority.

---

# Right-to-Left Associativity

Only one arithmetic operator follows

```
Right

↓

Left
```

That operator is

```python
**
```

---

# Example

```python
2 ** 3 ** 2
```

Many beginners evaluate

```
2³

↓

8

↓

8²

↓

64
```

This is incorrect.

Python evaluates

```
3²

↓

9

↓

2⁹

↓

512
```

Output

```text
512
```

---

# Example

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

Expression becomes

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

These examples show why exponentiation is evaluated from right to left unless parentheses change the order. :contentReference[oaicite:1]{index=1}

---

# Best Practices

## ✅ Use Parentheses

Instead of depending entirely on operator precedence,

write

```python
result = (price * quantity) + tax
```

This improves readability.

---

## ✅ Prefer Compound Assignment

Instead of

```python
count = count + 1
```

write

```python
count += 1
```

---

## ✅ Use `is` Only for Identity

Correct

```python
if value is None:
```

Incorrect

```python
if value == None:
```

---

## ✅ Use `==` for Value Comparison

Correct

```python
if a == b:
```

Avoid using `is` when comparing numbers or strings for equality.

---

## ✅ Use Membership Operators

Instead of

```python
if color == "red" or color == "blue":
```

write

```python
if color in ["red", "blue"]:
```

This is cleaner and easier to maintain.

---

# Common Mistakes

### ❌ Confusing `==` and `is`

```python
a == b
```

compares values.

```python
a is b
```

compares object identity.

---

### ❌ Assuming `++` Works

```python
a++
```

Python raises

```text
SyntaxError
```

---

### ❌ Believing `++a` Increments the Variable

```python
++a
```

is simply interpreted as

```python
+(+(a))
```

It does **not** increase the value.

---

### ❌ Forgetting Operator Precedence

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

because multiplication has higher precedence.

---

### ❌ Ignoring Tuple Unpacking Rules

```python
a, b = 10
```

Output

```text
ValueError
```

because the number of variables and values does not match.

---

# Interview Questions

### 1. What is an Assignment Operator?

An assignment operator assigns a value to a variable.

Example

```python
a = 10
```

---

### 2. What is Tuple Unpacking?

Assigning multiple values to multiple variables simultaneously.

Example

```python
a, b = 10, 20
```

---

### 3. Why doesn't Python support `++`?

Python uses

```python
+= 1
```

instead of increment operators to keep the language simple and readable.

---

### 4. Difference between `==` and `is`?

| `==` | `is` |
|------|------|
| Compares values | Compares object identity |

---

### 5. What are Membership Operators?

- `in`
- `not in`

Used to check whether an element exists in a collection.

---

### 6. Which operator has the highest precedence?

Parentheses

```text
()
```

---

### 7. Which operator follows Right-to-Left associativity?

Exponentiation

```python
**
```

---

### 8. Which operators follow Left-to-Right associativity?

- `+`
- `-`
- `*`
- `/`
- `//`
- `%`

---

### 9. Why are parentheses important?

They override the default precedence rules and make expressions easier to understand.

---

# Quick Revision

- `=` assigns values to variables.
- Python supports multiple assignment.
- Tuple unpacking requires equal numbers of variables and values.
- Compound assignment operators make code shorter.
- Python has no `++` or `--`.
- `++a` and `--a` are unary operators, not increment/decrement operators.
- `is` compares object identity.
- `==` compares values.
- `in` checks membership.
- `not in` checks absence.
- Parentheses have the highest precedence.
- `**` is right-associative.
- Most arithmetic operators are left-associative.

---

# Summary

In this lecture, we explored Python's assignment operators, including simple assignment, multiple assignment, tuple unpacking, and compound assignment operators. We learned how compound assignments simplify code and why Python does not include traditional increment (`++`) and decrement (`--`) operators found in languages like C++ and Java.

We also studied identity operators (`is`, `is not`) for comparing object identity, membership operators (`in`, `not in`) for checking elements inside collections, and operator precedence and associativity, which determine how Python evaluates complex expressions.

Understanding these concepts helps you write cleaner, more readable, and more reliable Python programs while avoiding common mistakes related to expression evaluation and object comparison.

---
