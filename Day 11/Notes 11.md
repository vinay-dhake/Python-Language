# 🐍 Python Operators in Python (Lecture 11)

> **Complete GitHub Notes** on Python Operators including Arithmetic Operators, Floor Division, Power Operator, String Operations, Comparison Operators, Unicode Comparison, `ord()` Function, and important interview concepts.

---

# 📚 Table of Contents

- Introduction
- What are Operators?
- Operands
- Types of Operators in Python
- Arithmetic Operators
- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)
- Modulus (`%`)
- Floor Division (`//`)
- Exponentiation (`**`)
- Difference Between `/` and `//`
- Double Role of `+`
- Double Role of `*`
- Relational (Comparison) Operators
- String Comparison
- Unicode Values
- `ord()` Function
- Case Sensitivity
- Quiz Concepts
- Best Practices
- Common Mistakes
- Interview Questions
- Quick Revision
- Summary

---

# Introduction

Operators are one of the most fundamental concepts in programming. Almost every Python program performs operations such as addition, comparison, multiplication, logical testing, or assignment. Python provides a rich set of built-in operators that work not only with numbers but also with strings, lists, sets, and many other objects.

Unlike many programming languages, Python also **overloads** some operators. For example, the `+` operator performs addition for numbers but concatenation for strings, while the `*` operator performs multiplication for numbers but repetition for strings. These behaviors make Python expressive and easy to read. :contentReference[oaicite:0]{index=0}

---

# What are Operators?

An **operator** is a special symbol that instructs Python to perform a specific operation on one or more values.

Example

```python
2 + 3
```

Here,

```
+
```

is the operator.

```
2

3
```

are called operands.

Result

```
5
```

---

## Operands

The values on which operators work are called **operands**.

Example

```python
10 * 5
```

```
10

5
```

are operands.

```
*
```

is the operator.

---

# Operators vs Operands

| Term | Meaning |
|------|---------|
| Operator | Symbol that performs an operation |
| Operand | Value on which the operation is performed |

Example

```python
50 / 10
```

```
Operator

/

Operands

50

10
```

---

# Types of Operators in Python

Python provides several categories of operators.

| Operator Type | Purpose |
|--------------|----------|
| Arithmetic Operators | Mathematical calculations |
| Relational (Comparison) Operators | Compare values |
| Assignment Operators | Assign values |
| Logical Operators | Combine conditions |
| Identity Operators | Compare object identity |
| Membership Operators | Test membership in collections |

In this lecture, the focus is primarily on **Arithmetic Operators** and **Relational Operators**. :contentReference[oaicite:1]{index=1}

---

# Arithmetic Operators

Arithmetic operators perform mathematical calculations.

Python provides **seven arithmetic operators**.

| Operator | Name |
|-----------|------|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Float Division |
| `%` | Modulus |
| `//` | Floor Division |
| `**` | Exponentiation |

---

# Addition Operator (`+`)

The addition operator adds two numeric values.

Example

```python
a = 10
b = 4

print(a + b)
```

Output

```text
14
```

---

# Subtraction Operator (`-`)

Subtracts the second operand from the first.

```python
a = 10
b = 4

print(a - b)
```

Output

```text
6
```

---

# Multiplication Operator (`*`)

Multiplies two values.

```python
a = 10
b = 4

print(a * b)
```

Output

```text
40
```

---

# Division Operator (`/`)

Performs **floating-point division**.

Regardless of whether the division is exact, Python returns a floating-point result.

Example

```python
a = 10
b = 4

print(a / b)
```

Output

```text
2.5
```

Another example

```python
print(10 / 5)
```

Output

```text
2.0
```

Notice

Even though the mathematical answer is `2`, Python returns

```
2.0
```

because `/` always performs float division.

---

# Modulus Operator (`%`)

Returns the remainder after division.

Example

```python
print(10 % 3)
```

Output

```text
1
```

Example

```python
print(20 % 6)
```

Output

```text
2
```

The modulus operator is commonly used to:

- Check if a number is even or odd
- Extract digits
- Implement cyclic operations

---

# Example Program (From the Lecture)

```python
a = 10
b = 4

print("Sum of", a, "and", b, "is", a + b)
print("Difference of", a, "and", b, "is", a - b)
print("Product of", a, "and", b, "is", a * b)
print("Division of", a, "and", b, "is", a / b)
print("Remainder of", a, "and", b, "is", a % b)
```

Output

```text
Sum of 10 and 4 is 14
Difference of 10 and 4 is 6
Product of 10 and 4 is 40
Division of 10 and 4 is 2.5
Remainder of 10 and 4 is 2
```

This example demonstrates the five basic arithmetic operators exactly as discussed in the lecture. :contentReference[oaicite:2]{index=2}

---

# Exponentiation Operator (`**`)

The exponentiation operator calculates the power of a number.

Syntax

```python
base ** exponent
```

Example

```python
a = 10
b = 3

print(a ** b)
```

Output

```text
1000
```

Explanation

```
10 × 10 × 10 = 1000
```

More examples

```python
print(5 ** 2)
```

Output

```text
25
```

```python
print(2 ** 5)
```

Output

```text
32
```

---

# Floor Division Operator (`//`)

The `//` operator is called the **Floor Division Operator**.

It performs division but **returns the floor of the result** instead of the exact decimal value.

Example

```python
print(5 // 2)
```

Output

```text
2
```

Actual division

```
5 / 2 = 2.5
```

Floor division removes the fractional part for positive numbers and returns

```
2
```

---

# Why is it called Floor Division?

In mathematics,

the **floor** of a number means the **greatest integer less than or equal to that number**.

Examples

| Value | Floor |
|--------|------|
| 2.9 | 2 |
| 5.1 | 5 |
| -2.5 | -3 |
| -9.5 | -10 |

This becomes especially important when negative numbers are involved.
===============================================================================================================================================================
---

# Floor Division (`//`) in Detail

The floor division operator (`//`) divides two numbers and returns the **floor** of the result instead of the exact decimal value.

The term **floor** means:

> The greatest integer that is **less than or equal to** the given number.

Unlike normal division (`/`), floor division removes the fractional part by rounding **down** toward negative infinity.

---

# Floor Division with Positive Numbers

Consider

```python
print(59 // 10)
```

Mathematical Division

```
59 / 10 = 5.9
```

Floor Value

```
5
```

Output

```text
5
```

Another example

```python
print(10 // 4)
```

Calculation

```
10 / 4 = 2.5

Floor = 2
```

Output

```text
2
```

---

# Floor Division with Negative Numbers

This is where many beginners make mistakes.

Consider

```python
print(-10 // 4)
```

Mathematical Result

```
-10 / 4 = -2.5
```

Many students think the answer should be

```
-2
```

This is **incorrect**.

Floor means

> The greatest integer that is **less than or equal to** -2.5.

Numbers around -2.5

```
-4

-3

-2

-1
```

Since

```
-3 ≤ -2.5
```

and

```
-2 > -2.5
```

the floor becomes

```
-3
```

Output

```text
-3
```

---

Another example

```python
print(19 // -2)
```

Division

```
19 / -2

=

-9.5
```

Floor

```
-10
```

Output

```text
-10
```

---

# Visual Understanding of Floor

```
Positive Numbers

2.8

↓

2



Negative Numbers

-2.8

↓

-3
```

Notice

For negative numbers,

Python always moves **towards negative infinity**, not towards zero.

---

# Data Type Preservation

The result type depends upon the operands.

If **both operands are integers**, the result is an integer.

Example

```python
print(10 // 4)
```

Output

```python
2
```

Type

```python
int
```

---

If **one operand is float**, the result becomes float.

Example

```python
print(10 // 4.0)
```

Output

```python
2.0
```

Type

```python
float
```

---

More examples

```python
print(15 // 2)
```

Output

```text
7
```

---

```python
print(15 // 2.0)
```

Output

```text
7.0
```

---

# Difference Between `/` and `//`

| `/` | `//` |
|------|-------|
| Performs normal division | Performs floor division |
| Returns decimal value | Returns floor value |
| Always returns float | Returns int or float depending on operands |

Example

```python
print(10 / 4)
```

Output

```text
2.5
```

---

```python
print(10 // 4)
```

Output

```text
2
```

---

```python
print(10 // 4.0)
```

Output

```text
2.0
```

---

# Division by Zero

Python does not allow division by zero.

The following operators

- `/`
- `//`
- `%`

all raise the same exception.

Example

```python
print(10 / 0)
```

Output

```text
ZeroDivisionError
```

---

Example

```python
print(10 // 0)
```

Output

```text
ZeroDivisionError
```

---

Example

```python
print(10 % 0)
```

Output

```text
ZeroDivisionError
```

---

The same applies to floating-point zero.

```python
print(10 / 0.0)
```

Output

```text
ZeroDivisionError
```

---

# Why Does Division by Zero Fail?

Mathematically,

division asks

> "How many times can the denominator fit into the numerator?"

If the denominator is zero,

the answer is undefined.

Therefore,

Python immediately raises an exception to prevent invalid calculations.

---

# Operator Overloading

One of Python's powerful features is **Operator Overloading**.

Operator overloading means

> The same operator can perform different operations depending on the type of operands.

Example

```
+

can perform

Addition

OR

String Concatenation
```

Similarly,

```
*

can perform

Multiplication

OR

String Repetition
```

---

# Double Role of `+`

## Addition

```python
print(10 + 20)
```

Output

```text
30
```

---

## String Concatenation

```python
print("Hello" + "World")
```

Output

```text
HelloWorld
```

The strings are joined together.

---

Another example

```python
name = "Sachin"

surname = "Tendulkar"

print(name + surname)
```

Output

```text
SachinTendulkar
```

Notice

No space is inserted automatically.

If a space is required,

you must include it manually.

```python
print(name + " " + surname)
```

Output

```text
Sachin Tendulkar
```

---

# Invalid Addition

Python does not automatically convert integers into strings when using `+`.

Example

```python
print("Age = " + 20)
```

Output

```text
TypeError
```

Correct approach

```python
print("Age =", 20)
```

or

```python
print("Age = " + str(20))
```

---

# Double Role of `*`

Normally

```
*

means multiplication.
```

Example

```python
print(10 * 5)
```

Output

```text
50
```

But with strings,

it behaves differently.

It repeats the string multiple times.

---

# String Repetition

Example

```python
print("Hello" * 3)
```

Output

```text
HelloHelloHello
```

Python creates

```
Hello

Hello

Hello
```

and joins them together.

---

Another example

```python
print(3 * "Sachin")
```

Output

```text
SachinSachinSachin
```

Notice

The integer may appear either before or after the string.

Both are valid.

---

More examples

```python
print("*" * 20)
```

Output

```text
********************
```

Useful for decorative output.

---

```python
print("=" * 40)
```

Output

```text
========================================
```

---

# Invalid String Multiplication

Python only allows multiplication by an integer.

Example

```python
print("Sachin" * 3.0)
```

Output

```text
TypeError
```

---

Example

```python
print("Hi" * "Bye")
```

Output

```text
TypeError
```

Why?

Python cannot determine

how many times a string should be repeated

when multiplied by another string or a floating-point number.

---

# Summary of Operator Overloading

| Expression | Meaning |
|------------|---------|
| `10 + 20` | Addition |
| `"A" + "B"` | String Concatenation |
| `10 * 5` | Multiplication |
| `"Hi" * 3` | String Repetition |

---

# Important Note

Operator overloading makes Python expressive and easy to read.

However,

always ensure that the operand types are compatible.

Otherwise,

Python raises a `TypeError`, indicating that the operation is not supported for the given data types.
=============================================================================================================================================================
---

# Relational (Comparison) Operators

Relational operators are used to compare two values.

Unlike arithmetic operators, they do **not** perform mathematical calculations.

Instead, they evaluate a condition and return a Boolean value.

The result is always either

```python
True
```

or

```python
False
```

---

# Why Do We Need Comparison Operators?

In programming, we often need to answer questions such as:

- Is a student eligible?
- Is a number positive?
- Are two values equal?
- Is the password correct?
- Has the user entered the correct OTP?

These questions produce only two possible answers.

```
Yes

or

No
```

Python represents these answers using

```
True

False
```

---

# Relational Operators

Python provides six relational operators.

| Operator | Meaning |
|-----------|---------|
| `>` | Greater Than |
| `<` | Less Than |
| `>=` | Greater Than or Equal To |
| `<=` | Less Than or Equal To |
| `==` | Equal To |
| `!=` | Not Equal To |

---

# Greater Than (`>`)

Returns `True` if the left operand is greater than the right operand.

Example

```python
print(20 > 10)
```

Output

```text
True
```

---

Example

```python
print(5 > 20)
```

Output

```text
False
```

---

# Less Than (`<`)

Returns `True` if the left operand is smaller.

Example

```python
print(10 < 20)
```

Output

```text
True
```

---

Example

```python
print(30 < 5)
```

Output

```text
False
```

---

# Greater Than or Equal To (`>=`)

Example

```python
print(20 >= 20)
```

Output

```text
True
```

---

Example

```python
print(30 >= 50)
```

Output

```text
False
```

---

# Less Than or Equal To (`<=`)

Example

```python
print(10 <= 20)
```

Output

```text
True
```

---

Example

```python
print(30 <= 20)
```

Output

```text
False
```

---

# Equal To (`==`)

Checks whether both values are equal.

Example

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

# Not Equal To (`!=`)

Returns `True` if the values are different.

Example

```python
print(10 != 20)
```

Output

```text
True
```

---

Example

```python
print(50 != 50)
```

Output

```text
False
```

---

# Comparison Operators Return Boolean Values

Every comparison operator returns either

```python
True
```

or

```python
False
```

Example

```python
a = 10
b = 20

print(a < b)
print(a == b)
print(a != b)
```

Output

```text
True
False
True
```

---

# String Comparison

Many beginners think Python compares strings based on

- length
- number of characters

This is **incorrect**.

Python compares strings **lexicographically**, i.e., character by character using their Unicode values.

---

# What is Lexicographical Comparison?

Python compares two strings from **left to right**.

It checks one character at a time.

If both characters are equal,

Python moves to the next character.

The comparison stops at the **first different character**.

Their Unicode values decide the result.

---

# Example

```python
print("A" > "B")
```

Output

```text
False
```

Why?

Unicode values

```
A = 65

B = 66
```

Since

```
65 < 66
```

Result

```
False
```

---

# Example

```python
print("B" > "A")
```

Output

```text
True
```

---

# Example

```python
print("Apple" > "Ant")
```

Comparison

```
A == A

p > n
```

Unicode

```
p = 112

n = 110
```

Since

```
112 > 110
```

Output

```text
True
```

---

# Example from the Lecture

```python
print("Ahmedabad" > "Bhopal")
```

Output

```text
False
```

Comparison

```
A

vs

B
```

Unicode

```
65

66
```

Therefore

```
False
```

Python never compares the remaining characters because the decision is already made at the first mismatch. :contentReference[oaicite:0]{index=0}

---

# Another Lecture Example

```python
print("Ramesh" > "Rajesh")
```

Let's compare character by character.

```
R == R

a == a

m

j
```

Unicode values

```
m = 109

j = 106
```

Since

```
109 > 106
```

Output

```text
True
```

Again,

Python stops comparing after the first unequal characters.

---

# The `ord()` Function

Python provides a built-in function called `ord()`.

It returns the Unicode (code point) value of a single character.

Syntax

```python
ord(character)
```

---

# Example

```python
print(ord("A"))
```

Output

```text
65
```

---

Example

```python
print(ord("U"))
```

Output

```text
85
```

---

Example

```python
print(ord("b"))
```

Output

```text
98
```

These examples help explain why string comparisons behave the way they do. :contentReference[oaicite:1]{index=1}

---

# Important Rule

`ord()` accepts **exactly one character**.

Correct

```python
ord("A")
```

Incorrect

```python
ord("Apple")
```

Output

```text
TypeError
```

because the string contains more than one character.

---

# Case Sensitivity

Python is **case-sensitive**.

Uppercase and lowercase letters have different Unicode values.

Examples

```
A = 65

B = 66

a = 97

b = 98
```

Notice

All uppercase letters have smaller Unicode values than lowercase letters.

---

# Example

```python
print("Bhopal" > "bhopal")
```

Comparison

```
B

b
```

Unicode

```
66

98
```

Since

```
66 < 98
```

Output

```text
False
```

This example demonstrates that Python distinguishes between uppercase and lowercase characters. :contentReference[oaicite:2]{index=2}

---

# Real-Life Use of Comparison Operators

Comparison operators are widely used in:

- Login authentication
- Password validation
- Age eligibility checks
- Student grading systems
- Banking applications
- E-commerce discounts
- Searching and sorting algorithms
- Conditional statements (`if`, `elif`, `while`)

Without comparison operators, decision-making in programs would not be possible.

---

# Quick Quiz Concepts (From the Lecture)

### Variable Name Length

Python does **not** impose a practical limit on the length of variable names (although extremely long names are discouraged for readability).

Example

```python
this_is_a_very_long_variable_name_used_for_demonstration = 100
```

Python accepts it.

---

### Does Python Have a `char` Data Type?

No.

Python does **not** have a separate `char` data type.

A single character is simply a string of length **1**.

Example

```python
ch = "A"

print(type(ch))
```

Output

```python
<class 'str'>
```

---

### Truth Value of Strings

Example

```python
print(bool("False"))
```

Output

```text
True
```

Why?

Because `"False"` is a **non-empty string**.

In Python:

- Empty string `""` → `False`
- Any non-empty string → `True`

This often surprises beginners.

---

### Strings are Immutable

```python
city = "Bhopal"

city = "Indore"
```

The reference `city` changes, but the original `"Bhopal"` string object is **not modified**. Instead, Python creates a new string object and updates the reference.

This reinforces the concept of **immutable string objects**.
=============================================================================================================================================================
---

# Best Practices

Following good programming practices makes your code cleaner, easier to understand, and easier to maintain.

## ✅ Use Meaningful Variable Names

Good

```python
student_name = "Vinay"
total_marks = 450
```

Bad

```python
a = "Vinay"
b = 450
```

Meaningful names make programs self-explanatory.

---

## ✅ Use Parentheses in Complex Expressions

Instead of writing

```python
result = a + b * c - d / e
```

write

```python
result = (a + (b * c)) - (d / e)
```

Even though Python follows operator precedence, parentheses improve readability.

---

## ✅ Avoid Division by Zero

Always validate the denominator before performing division.

```python
if b != 0:
    print(a / b)
else:
    print("Division by zero is not allowed.")
```

This prevents a `ZeroDivisionError`.

---

## ✅ Use `//` Only When Floor Division is Required

Use

```python
/
```

when you need the exact decimal result.

Use

```python
//
```

only when the integer floor value is required.

Examples:

- Pagination
- Number of complete groups
- Bucketing calculations

---

## ✅ Remember That `+` Behaves Differently for Strings

```python
print("Hello" + "World")
```

joins strings.

Whereas

```python
print(10 + 20)
```

adds numbers.

Always ensure the operand types are compatible.

---

## ✅ Prefer Comma in `print()`

Instead of

```python
print("Age = " + str(age))
```

write

```python
print("Age =", age)
```

It is shorter, cleaner, and automatically handles type conversion.

---

# Common Mistakes

## ❌ Mistake 1

Thinking

```python
10 / 5
```

returns

```python
2
```

Actually,

```python
10 / 5
```

returns

```python
2.0
```

because `/` always performs floating-point division.

---

## ❌ Mistake 2

Confusing `/` with `//`

```python
10 / 4
```

Output

```text
2.5
```

Whereas

```python
10 // 4
```

Output

```text
2
```

---

## ❌ Mistake 3

Assuming Floor Division Truncates Towards Zero

Many beginners expect

```python
-10 // 4
```

to return

```text
-2
```

Incorrect.

Python returns

```text
-3
```

because floor division always rounds **towards negative infinity**.

---

## ❌ Mistake 4

Trying to Multiply a String by a Float

```python
print("Hello" * 3.0)
```

Output

```text
TypeError
```

Only integers are allowed.

---

## ❌ Mistake 5

Trying to Concatenate String and Integer

```python
print("Age = " + 20)
```

Output

```text
TypeError
```

Correct

```python
print("Age =", 20)
```

or

```python
print("Age = " + str(20))
```

---

## ❌ Mistake 6

Thinking Strings Are Compared by Length

```python
"Cat"

"Elephant"
```

Python does **not** compare string lengths.

It compares Unicode values character by character.

---

## ❌ Mistake 7

Passing Multiple Characters to `ord()`

Incorrect

```python
ord("Hello")
```

Correct

```python
ord("H")
```

`ord()` accepts exactly one character.

---

# Interview Questions

## 1. What is an operator?

An operator is a special symbol that performs an operation on one or more operands.

---

## 2. What are operands?

Operands are the values on which an operator performs its operation.

---

## 3. How many arithmetic operators are available in Python?

Seven:

- `+`
- `-`
- `*`
- `/`
- `%`
- `//`
- `**`

---

## 4. Difference between `/` and `//`?

| `/` | `//` |
|------|-------|
| Normal division | Floor division |
| Always returns float | Returns floor value |
| Example: `10 / 4 = 2.5` | Example: `10 // 4 = 2` |

---

## 5. What is Floor Division?

Floor division returns the greatest integer less than or equal to the actual division result.

---

## 6. Why does `-10 // 4` return `-3`?

Because Python rounds towards **negative infinity**, not towards zero.

---

## 7. What is Operator Overloading?

The same operator performs different operations depending on operand types.

Example:

```python
10 + 20
```

Addition

```python
"Hello" + "World"
```

Concatenation

---

## 8. Can Strings be Multiplied?

Yes.

Only by integers.

Example

```python
print("Hi" * 3)
```

Output

```text
HiHiHi
```

---

## 9. What happens if a string is multiplied by a float?

Python raises

```text
TypeError
```

---

## 10. Which operator calculates powers?

```python
**
```

Example

```python
2 ** 5
```

Output

```text
32
```

---

## 11. What do comparison operators return?

Always

```python
True
```

or

```python
False
```

---

## 12. How are strings compared?

Strings are compared lexicographically using Unicode values.

---

## 13. What does `ord()` do?

Returns the Unicode code point of a single character.

Example

```python
ord("A")
```

Output

```text
65
```

---

## 14. Does Python have a `char` data type?

No.

A single character is simply a string of length one.

---

## 15. Why is `bool("False")` equal to `True`?

Because `"False"` is a **non-empty string**.

Any non-empty string evaluates to `True`.

---

# Quick Revision

- Operators perform operations on operands.
- Python has seven arithmetic operators.
- `/` always returns a floating-point result.
- `//` performs floor division.
- `%` returns the remainder.
- `**` calculates powers.
- Division by zero raises `ZeroDivisionError`.
- `+` performs addition or string concatenation.
- `*` performs multiplication or string repetition.
- Strings can only be multiplied by integers.
- Comparison operators return Boolean values.
- Strings are compared lexicographically.
- `ord()` returns the Unicode value of one character.
- Python is case-sensitive.
- Python has no separate `char` data type.
- Any non-empty string is truthy.

---

# Key Takeaways

- Operators are the building blocks of expressions in Python.
- Arithmetic operators work with numbers, while some operators such as `+` and `*` are overloaded to work with strings.
- Understanding the difference between `/` and `//` is essential, especially when working with negative numbers.
- Comparison operators form the foundation of decision-making using `if`, `elif`, and `while` statements.
- Python compares strings based on **Unicode values**, not string length.
- Functions like `ord()` help explain how string comparisons work internally.
- Mastering these operators is essential because they are used throughout Python programming, from simple calculations to advanced algorithms.

---

# Summary

In this lecture, we explored Python operators in detail, beginning with arithmetic operators such as addition, subtraction, multiplication, division, modulus, floor division, and exponentiation. We learned how Python overloads operators like `+` and `*` to work with both numeric and string data types.

We then studied relational operators, which compare values and return Boolean results. We also examined lexicographical string comparison, Unicode values, the `ord()` function, case sensitivity, and several important Python concepts discussed during the class quiz, such as truthy strings, unlimited variable name lengths, and the absence of a dedicated `char` type.

Understanding these concepts provides a strong foundation for writing expressions, making decisions, and solving programming problems effectively in Python.
---
