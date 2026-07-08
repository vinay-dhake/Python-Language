# Python Programming - Lecture 15 Notes

# String Formatting Rules & Decision Control Statements (`if`, `if-else`, `if-elif-else`, Nested `if`)

---

# Introduction

In the previous lecture, we learned how to display variables inside strings using **C-style format specifiers** (`%d`, `%f`, `%s`, `%c`).

In this lecture, we first study the rules that must be followed while using format specifiers. After that, we move to one of the most important topics in programming—**Decision Control Statements**.

Decision control statements allow a program to make decisions based on conditions. Instead of executing every statement one after another, the program checks whether a condition is **True** or **False** and executes only the appropriate block of code.

Python mainly provides four decision control statements:

- `if`
- `if-else`
- `if-elif-else`
- Nested `if`

Unlike languages such as C, C++, and Java, Python uses **indentation** instead of curly braces `{}` to define code blocks. :contentReference[oaicite:0]{index=0}

---

# Part 1 — Rules for Format Specifiers

Python follows strict rules while using C-style formatting.

If these rules are violated, Python immediately raises an exception.

---

# Rule 1 — Number of Specifiers Must Match Number of Variables

The total number of format specifiers inside the string must exactly match the number of variables supplied after `%`.

Correct Example

```python
a = 10
b = 20

print("A = %d B = %d" % (a, b))
```

Output

```text
A = 10 B = 20
```

---

## Error Case 1

Two specifiers but only one variable.

```python
a = 10

print("Value is %d and %d" % (a))
```

Output

```text
TypeError
```

Reason

- Two `%d` specifiers exist.
- Only one value is supplied.

---

## Error Case 2

One specifier but two variables.

```python
a = 10
b = 20

print("Value is %d" % (a, b))
```

Output

```text
TypeError
```

Reason

Python doesn't know what to do with the extra variable.

---

# Rule 2 — Data Types Must Match

Each format specifier expects a compatible data type.

Example

```python
print("%d" % 10)
```

Correct because `%d` expects an integer.

---

## `%s` Works With Almost Everything

The `%s` specifier converts any object into a string before printing.

Example

```python
print("%s" % 10)
```

Output

```text
10
```

Example

```python
print("%s" % True)
```

Output

```text
True
```

Example

```python
print("%s" % 10.5)
```

Output

```text
10.5
```

---

## `%f` With Integer

Example

```python
print("%f" % 10)
```

Output

```text
10.000000
```

Notice that `%f` always prints **six digits after the decimal** by default.

---

## Restricting Decimal Places

Example

```python
print("%.2f" % 10.6)
```

Output

```text
10.60
```

This behaves similarly to `round()` while displaying the output.

---

## `%d` With Float

Example

```python
print("%d" % 10.6)
```

Output

```text
10
```

Only the integer portion is displayed.

The decimal part is discarded.

---

## `%d` With Boolean

Python treats

- `True` as `1`
- `False` as `0`

Example

```python
print("%d" % True)
```

Output

```text
1
```

Similarly,

```python
print("%d" % False)
```

Output

```text
0
```

---

## `%d` With String

Example

```python
print("%d" % "Bhopal")
```

Output

```text
TypeError
```

Reason

Strings cannot be formatted using `%d`.

Use `%s` instead.

---

## `%c` With Character

Example

```python
print("%c" % 'A')
```

Output

```text
A
```

---

## `%c` With Multiple Characters

Example

```python
print("%c" % "AB")
```

Output

```text
TypeError
```

Reason

`%c` expects exactly one character.

---

## `%c` With Integer

Example

```python
print("%c" % 65)
```

Output

```text
A
```

Python converts the Unicode value 65 into its corresponding character.

Similarly,

```python
print("%c" % 97)
```

Output

```text
a
```

---

# Summary of Format Specifiers

| Specifier | Accepts | Example |
|-----------|----------|----------|
| `%d` | Integer | 10 |
| `%i` | Integer | 25 |
| `%f` | Float | 12.45 |
| `%s` | Any object | "Hello" |
| `%c` | Single character / Unicode integer | 'A', 65 |

---

# Important Points

- Number of variables must equal number of specifiers.
- `%s` accepts almost every data type.
- `%f` displays six decimal places by default.
- `%.2f` restricts output to two decimal places.
- `%d` prints only the integer portion.
- `%c` accepts one character or a Unicode integer.
- `%c` cannot print multiple-character strings.

---

# Quick Revision

✔ Number of format specifiers must equal number of variables.

✔ `%s` converts almost anything into a string.

✔ `%f` prints six decimal places.

✔ `%.2f` prints only two decimal places.

✔ `%d` truncates decimal values while displaying.

✔ `%c` prints a single character or converts a Unicode integer into its corresponding character.

---

**Next Part:** `.format()` Method and Decision Control Statements (`if` Statement & Indentation).
=============================================================================================================================================================
# Part 2 – String Formatting Using `.format()` Method

Python still supports the old C-style formatting (`%d`, `%f`, `%s`, etc.), but starting with Python 3, a much more flexible and readable formatting technique was introduced using the **`format()`** method.

Instead of remembering format specifiers like `%d` and `%f`, we simply place **curly braces `{}`** inside the string, and Python replaces them with the supplied values.

The `format()` method is easier to read, easier to maintain, and is widely used in Python programs.

---

# Why was `.format()` Introduced?

Consider the following C-style formatting:

```python
name = "Sachin"
age = 45

print("My name is %s and my age is %d" % (name, age))
```

Although correct,

you must remember

- `%s`
- `%d`
- `%f`
- `%c`

and use the correct specifier for each data type.

To simplify formatting,

Python introduced

```python
format()
```

where data types are automatically handled.

---

# Basic Syntax

```python
"String {}".format(value)
```

The curly braces `{}` are called **placeholders**.

Each placeholder is replaced by the corresponding value supplied inside `format()`.

---

# Example 1 – Single Variable

```python
name = "Sachin"

print("My name is {}".format(name))
```

### Output

```text
My name is Sachin
```

Python replaces

```
{}

↓

Sachin
```

This is the first example shown while introducing the `format()` method.

---

# Example 2 – Multiple Variables

```python
name = "Sachin"
age = 45

print("My name is {} and my age is {}".format(name, age))
```

### Output

```text
My name is Sachin and my age is 45
```

### Explanation

Python fills the placeholders from **left to right**.

```
First {}

↓

name

↓

Sachin

Second {}

↓

age

↓

45
```

---

# How Python Matches Placeholders

Consider

```python
print("{} {}".format(10, 20))
```

Python internally performs

```
First {}

↓

10

Second {}

↓

20
```

Output

```text
10 20
```

---

# Field Specification (Indexed Placeholders)

Sometimes we may want to display values in a different order than they are supplied.

For this purpose,

Python provides **field specification**.

Instead of empty braces,

we use

```python
{0}

{1}

{2}
```

where the numbers represent the **index position** of the arguments.

---

# Example 3 – Changing the Order

```python
name = "Sachin"
age = 45

print("My name is {1} and my age is {0}".format(age, name))
```

### Output

```text
My name is Sachin and my age is 45
```

### Explanation

Although

```python
age
```

is supplied first,

the placeholder

```python
{1}
```

refers to

the **second argument**,

which is

```python
name
```

Similarly,

```python
{0}
```

refers to

the **first argument**,

which is

```python
age
```

This example is demonstrated in the lecture to explain indexed placeholders.

---

# Visual Representation

Arguments

```
format(age, name)

↓

Index 0

↓

age

↓

45

Index 1

↓

name

↓

Sachin
```

Placeholders

```
{1}

↓

Sachin

{0}

↓

45
```

Final Output

```text
My name is Sachin and my age is 45
```

---

# Reusing the Same Variable

One advantage of indexed placeholders is that the same variable can be reused multiple times.

Example

```python
name = "Python"

print("{0} is easy. {0} is powerful.".format(name))
```

Output

```text
Python is easy. Python is powerful.
```

---

# Mixing Indexed and Empty Placeholders

Python does **not** allow mixing

```python
{}
```

with

```python
{0}
```

Example

```python
print("{} {0}".format(10))
```

Output

```text
ValueError
```

Rule

Either

use **all empty placeholders**

```python
{} {}
```

or

use **all indexed placeholders**

```python
{0} {1}
```

Never mix them.

This warning is specifically mentioned during the lecture.

---

# Advantages of `.format()`

✔ Easier to read.

✔ No need to remember `%d`, `%f`, `%s`.

✔ Works with every data type.

✔ Allows reordering of variables.

✔ Supports reuse of the same variable.

✔ More flexible than old C-style formatting.

---

# Comparison

## C-Style Formatting

```python
name = "Sachin"
age = 45

print("My name is %s and my age is %d" % (name, age))
```

---

## Using `.format()`

```python
name = "Sachin"
age = 45

print("My name is {} and my age is {}".format(name, age))
```

Both produce

```text
My name is Sachin and my age is 45
```

However,

`.format()` is much easier to understand.

---

# Decision Control Statements

Until now,

our programs have executed statements one after another.

Example

```python
print("Hello")

print("Python")

print("Programming")
```

Output

```text
Hello

Python

Programming
```

The execution always follows the same path.

But real-world programs often need to make **decisions**.

Examples

- Can the user vote?
- Is the number even or odd?
- Is the student passed or failed?
- Is the entered character a digit or a letter?

To perform such tasks,

Python provides **Decision Control Statements**.

These statements control the flow of execution based on conditions.

A condition always evaluates to either

```text
True
```

or

```text
False
```

Depending on the result,

different blocks of code are executed.

---

# Types of Decision Control Statements

Python mainly provides four decision-making statements.

- `if`
- `if-else`
- `if-elif-else`
- Nested `if`

These are among the most important concepts in Python programming.

---

# Indentation in Python

One of the biggest differences between Python and languages like

- C
- C++
- Java

is that Python **does not use curly braces `{}`** to define code blocks.

Instead,

Python uses **indentation**.

Example

```python
if True:
    print("Hello")
```

Notice

The line

```python
print("Hello")
```

begins with **4 spaces** (or one Tab).

This indentation tells Python that the statement belongs to the `if` block.

---

# Why is Indentation Important?

Incorrect indentation causes an error.

Correct

```python
if True:
    print("Python")
```

Incorrect

```python
if True:
print("Python")
```

Output

```text
IndentationError
```

Python treats indentation as part of its syntax.

Unlike C or Java,

indentation is **not optional**.

---

# Rules of Indentation

- Every statement inside the same block must have identical indentation.
- Mixing different indentation levels within the same block causes errors.
- Four spaces are recommended (PEP 8).
- A colon (`:`) must always appear after the condition.

---

# Example

```python
if True:
    print("Line 1")
    print("Line 2")
    print("Line 3")
```

All three statements belong to the same block because they have equal indentation.

---

# Key Points

- `.format()` replaces `%` formatting in modern Python.
- `{}` are placeholders.
- Values are inserted using `.format()`.
- Indexed placeholders (`{0}`, `{1}`) allow custom ordering.
- Do not mix `{}` with `{0}`.
- Decision control statements help programs make decisions.
- Python uses indentation instead of curly braces.
- Incorrect indentation raises `IndentationError`.
- A colon (`:`) is mandatory after conditions.

---

**Next Part:** The `if` statement, Voting Eligibility program, single-line `if`, and multiple statements on one line.
===============================================================================================================================================================
# Part 3 – The `if` Statement

The simplest decision-making statement in Python is the **`if` statement**.

It is used when we want to execute a block of code **only if a condition is True**.

If the condition becomes **False**, Python simply skips the block and continues executing the remaining statements.

The `if` statement is the foundation of all other decision control statements in Python.

---

# Syntax of `if`

```python
if condition:
    statement(s)
```

### Syntax Explanation

- `if` is a keyword.
- `condition` is any expression that evaluates to `True` or `False`.
- A colon (`:`) is mandatory.
- The body of the `if` statement must be properly indented.

---

# Flow of Execution

```
           Condition

               │

        ┌──────┴──────┐

      True          False

        │              │

 Execute Block      Skip Block

        │              │

        └──────┬───────┘

               │

        Next Statement
```

---

# Conditions Used in `if`

A condition may contain

- Relational operators

```python
>

<

>=

<=

==

!=
```

- Logical operators

```python
and

or

not
```

- Boolean values

```python
True

False
```

Python evaluates the condition first.

If the result is

```python
True
```

the block executes.

Otherwise,

it is skipped.

---

# Example 1 – Simple `if`

```python
age = 20

if age >= 18:
    print("Eligible to Vote")
```

Output

```text
Eligible to Vote
```

Since

```
20 >= 18

↓

True
```

Python executes the block.

---

# Example 2 – Condition Becomes False

```python
age = 15

if age >= 18:
    print("Eligible to Vote")

print("Program Finished")
```

Output

```text
Program Finished
```

Since

```
15 >= 18

↓

False
```

the `if` block is skipped.

Execution directly continues with the next statement.

---

# Practical Example – Voting Eligibility

This is the first practical program demonstrated in the lecture.

```python
age = int(input("Enter your age: "))

if age >= 18:
    print("You can vote")

if age < 18:
    print("You cannot vote")
```

### Sample Output 1

```text
Enter your age:
21

You can vote
```

---

### Sample Output 2

```text
Enter your age:
15

You cannot vote
```

Notice that two independent `if` statements are used.

Only one condition becomes true.

The other block is skipped.

This example is discussed before introducing `if-else`. :contentReference[oaicite:0]{index=0}

---

# Why Do We Use `int()`?

Remember,

```python
input()
```

always returns a string.

Example

```python
age = input("Enter Age: ")
```

If the user enters

```text
18
```

then

```python
age
```

contains

```python
"18"
```

(String)

Now consider

```python
if age >= 18:
```

Python tries to compare

```
"18"

with

18
```

which is invalid.

Result

```text
TypeError
```

Therefore,

we convert the input using

```python
int()
```

```python
age = int(input("Enter Age: "))
```

Now

```
18

(Integer)
```

can be compared correctly.

---

# Parentheses Around the Condition

Unlike C, C++, and Java,

parentheses are **optional**.

Both are valid.

```python
if age >= 18:
    print("Eligible")
```

```python
if (age >= 18):
    print("Eligible")
```

Most Python programmers omit the parentheses.

---

# Importance of Colon (`:`)

Every `if` statement **must** end with a colon.

Correct

```python
if age >= 18:
```

Incorrect

```python
if age >= 18
```

Output

```text
SyntaxError
```

---

# Single-Line `if`

If the body of an `if` statement contains only **one statement**, Python allows it to be written on the same line.

Example

```python
age = 20

if age >= 18: print("You can vote")
```

Output

```text
You can vote
```

This syntax is valid but should be used only for very small statements.

---

# Multiple Statements on One Line

Python also allows multiple statements after the colon by separating them with semicolons (`;`).

Example

```python
age = 20

if age >= 18: print("You can vote"); print("Welcome")
```

Output

```text
You can vote

Welcome
```

Although valid,

this style is **rarely used** because it reduces readability.

The lecture demonstrates this to show Python's syntax flexibility. :contentReference[oaicite:1]{index=1}

---

# When Should We Use Multi-Line `if`?

Preferred

```python
if age >= 18:
    print("You can vote")
    print("Welcome")
```

This style is

- easier to read,
- easier to debug,
- recommended by PEP 8.

---

# Common Mistakes

## Missing Colon

Wrong

```python
if age >= 18
    print("Eligible")
```

Output

```text
SyntaxError
```

---

## Missing Indentation

Wrong

```python
if age >= 18:
print("Eligible")
```

Output

```text
IndentationError
```

---

## Comparing String with Integer

Wrong

```python
age = input()

if age >= 18:
    print("Eligible")
```

Output

```text
TypeError
```

Correct

```python
age = int(input())

if age >= 18:
    print("Eligible")
```

---

## Using Assignment Instead of Comparison

Wrong

```python
if age = 18:
```

Output

```text
SyntaxError
```

Correct

```python
if age == 18:
```

---

# Advantages of the `if` Statement

- Executes code only when required.
- Makes programs intelligent.
- Prevents unnecessary execution.
- Forms the basis of all decision-making structures.

---

# Real-Life Examples of `if`

### ATM Machine

```text
If PIN is correct

↓

Allow transaction
```

---

### Login System

```text
If password is correct

↓

Login successful
```

---

### College Admission

```text
If percentage >= 60

↓

Eligible
```

---

### Voting System

```text
If age >= 18

↓

Eligible to Vote
```

---

# Key Points

- `if` executes code only when the condition is `True`.
- Parentheses around the condition are optional.
- A colon (`:`) is mandatory.
- Proper indentation is compulsory.
- `input()` should be converted using `int()` before numeric comparisons.
- Single-line `if` is allowed.
- Multiple statements on one line can be separated using `;`, though it is not recommended.

---

# Quick Revision

✔ `if` is the simplest decision control statement.

✔ Condition must evaluate to `True` or `False`.

✔ Python uses indentation instead of `{}`.

✔ Colon is mandatory.

✔ `int(input())` is required for numeric comparisons.

✔ Single-line `if` is valid.

✔ Multi-line `if` is preferred for readability.

---

**Next Part:** `if-else` statement, Even/Odd program, Capital/Small letter checker, Relational Cascading vs `and`, and using `ord()`.
=============================================================================================================================================================
# Part 4 – The `if-else` Statement

The `if` statement is useful when we want to execute code only when a condition is **True**.

However, many real-world situations have **exactly two possible outcomes**.

For example:

- A number is either **Even** or **Odd**.
- A student is either **Pass** or **Fail**.
- A person is either **Eligible to Vote** or **Not Eligible**.

For such situations, Python provides the **`if-else` statement**.

---

# What is `if-else`?

The `if-else` statement allows Python to choose **one block out of two**.

- If the condition is **True**, the `if` block executes.
- Otherwise, the `else` block executes.

Exactly **one** block will execute.

---

# Syntax

```python
if condition:
    statements
else:
    statements
```

---

# Flow Diagram

```
            Condition

                │

         ┌──────┴──────┐

       True         False

         │              │

   Execute if      Execute else

         │              │

         └──────┬───────┘

                │

          Next Statement
```

---

# Important Rules

- `else` never has a condition.
- `else` must be written immediately after the `if` block.
- Only **one** block executes.
- Proper indentation is mandatory.

---

# Example 1 – Even or Odd Number

This is the first `if-else` example demonstrated in the lecture.

```python
num = int(input("Enter an integer: "))

if num % 2 == 0:
    print("Number is Even")
else:
    print("Number is Odd")
```

---

### Sample Output 1

```text
Enter an integer:
12

Number is Even
```

---

### Sample Output 2

```text
Enter an integer:
17

Number is Odd
```

---

# How It Works

Suppose

```python
num = 12
```

Python checks

```
12 % 2

↓

0
```

Now

```
0 == 0

↓

True
```

Therefore,

the `if` block executes.

---

Suppose

```python
num = 17
```

Now

```
17 % 2

↓

1
```

```
1 == 0

↓

False
```

Therefore,

Python executes the `else` block.

---

# Why is `if-else` Better Than Two `if` Statements?

Earlier we wrote

```python
if age >= 18:
    print("You can vote")

if age < 18:
    print("You cannot vote")
```

This works because the two conditions are opposite.

However,

`if-else` is more efficient.

```python
if age >= 18:
    print("You can vote")
else:
    print("You cannot vote")
```

Python checks only **one condition**.

If it becomes true,

the `else` block is automatically skipped.

---

# Example 2 – Capital or Small Letter

The lecture next demonstrates checking whether an entered character is an uppercase or lowercase letter.

```python
ch = input("Enter a character: ")

if 'A' <= ch <= 'Z':
    print("It is a Capital Letter")
else:
    print("It is a Small Letter")
```

---

### Sample Output

```text
Enter a character:
M

It is a Capital Letter
```

---

Another Example

```text
Enter a character:
p

It is a Small Letter
```

---

# Relational Cascading

One of Python's most powerful features is **Relational Cascading**.

Instead of writing

```python
if ch >= 'A' and ch <= 'Z':
```

Python allows

```python
if 'A' <= ch <= 'Z':
```

Both statements mean exactly the same thing.

---

## Traditional Style

```python
if ch >= 'A' and ch <= 'Z':
    print("Capital")
```

---

## Pythonic Style

```python
if 'A' <= ch <= 'Z':
    print("Capital")
```

The second version is shorter, cleaner, and is generally preferred in Python.

This comparison is emphasized in the lecture. :contentReference[oaicite:0]{index=0}

---

# Why Does This Work?

Characters are compared using their **Unicode values**.

For example

| Character | Unicode |
|-----------|---------:|
| A | 65 |
| B | 66 |
| C | 67 |
| Z | 90 |

When Python checks

```python
'A' <= ch <= 'Z'
```

it is actually comparing Unicode values internally.

---

# Using `ord()`

Sometimes we may want to compare using numeric Unicode values directly.

For that,

Python provides

```python
ord()
```

The `ord()` function converts a character into its Unicode value.

Example

```python
print(ord('A'))
```

Output

```text
65
```

Example

```python
print(ord('a'))
```

Output

```text
97
```

---

# Example 3 – Using `ord()`

```python
ch = input("Enter a character: ")

if 65 <= ord(ch) <= 90:
    print("It is a Capital Letter")
else:
    print("It is a Small Letter")
```

Output

```text
Enter a character:
A

It is a Capital Letter
```

This is the second approach shown in class after relational cascading.

---

# Why Can't We Write This?

Many beginners write

```python
if 65 <= ch <= 90:
```

This produces

```text
TypeError
```

---

# Reason

Here,

```
65

↓

Integer
```

while

```
ch

↓

String
```

Python cannot compare

```
Integer

and

String
```

Therefore,

we first convert

```python
ch
```

into its Unicode value

using

```python
ord(ch)
```

---

# Character Comparison Methods

## Method 1 – Character Comparison

```python
if 'A' <= ch <= 'Z':
```

---

## Method 2 – Unicode Comparison

```python
if 65 <= ord(ch) <= 90:
```

Both methods produce exactly the same result.

---

# Common Mistakes

## Forgetting `ord()`

Wrong

```python
if 65 <= ch <= 90:
```

Output

```text
TypeError
```

Correct

```python
if 65 <= ord(ch) <= 90:
```

---

## Forgetting `int()`

Wrong

```python
num = input()

if num % 2 == 0:
```

Output

```text
TypeError
```

Correct

```python
num = int(input())
```

---

## Missing Colon

Wrong

```python
if num % 2 == 0
```

Output

```text
SyntaxError
```

---

## Incorrect Indentation

Wrong

```python
if num % 2 == 0:
print("Even")
else:
print("Odd")
```

Output

```text
IndentationError
```

---

# Advantages of `if-else`

- Only one condition needs to be checked.
- Exactly one block executes.
- Code becomes cleaner than writing two separate `if` statements.
- Suitable for binary decisions (Yes/No, Even/Odd, Pass/Fail).

---

# Real-Life Examples

### ATM

```text
If PIN is correct

↓

Allow Transaction

Else

↓

Display Invalid PIN
```

---

### Login System

```text
If Password is Correct

↓

Login

Else

↓

Access Denied
```

---

### Voting

```text
If Age ≥ 18

↓

Eligible

Else

↓

Not Eligible
```

---

# Key Points

- `if-else` is used when there are exactly two possible outcomes.
- `else` never contains a condition.
- Only one block executes.
- Python supports relational cascading.
- `'A' <= ch <= 'Z'` is preferred over `ch >= 'A' and ch <= 'Z'`.
- `ord()` converts a character into its Unicode value.
- `65 <= ch <= 90` is invalid because integers and strings cannot be compared directly.

---

# Quick Revision

✔ `if-else` executes one of two blocks.

✔ `else` has no condition.

✔ Even/Odd is a classic `if-else` problem.

✔ Python supports relational cascading.

✔ `ord()` returns the Unicode value of a character.

✔ Use `ord()` when comparing characters with numeric values.

---

**Next Part:** `if-elif-else`, Character Analyzer (Capital, Small, Digit, Special Symbol), Nested `if`, Greatest of Three Numbers, and lecture assignments.
============================================================================================================================================================
# Part 5 – The `if-elif-else` Statement

In many real-world situations, there are **more than two possible outcomes**.

For example:

- A character may be an uppercase letter.
- It may be a lowercase letter.
- It may be a digit.
- It may be a special symbol.

Similarly,

- A student may receive Grade A, B, C, D, or Fail.
- Weather may be Sunny, Rainy, Cloudy, or Snowy.
- Traffic light may be Red, Yellow, or Green.

In such cases, writing multiple independent `if` statements is inefficient.

Python provides the **`if-elif-else` statement**, which allows multiple conditions to be checked one after another.

---

# What is `if-elif-else`?

The `if-elif-else` statement is used when there are **multiple mutually exclusive conditions**.

Python checks each condition one by one.

- If the first condition is `True`, its block executes and the remaining conditions are skipped.
- Otherwise, Python checks the next `elif`.
- If none of the conditions are `True`, the `else` block executes.

---

# Syntax

```python
if condition1:
    statements

elif condition2:
    statements

elif condition3:
    statements

else:
    statements
```

---

# Flow Diagram

```text
            Condition 1
                 │
         ┌───────┴────────┐
       True             False
         │                 │
 Execute Block 1     Condition 2
                           │
                    ┌──────┴───────┐
                  True          False
                    │               │
             Execute Block 2   Condition 3
                                     │
                              ┌──────┴──────┐
                            True         False
                              │             │
                      Execute Block 3   Else Block
```

---

# Important Rule

The moment Python finds **one True condition**, it executes that block and immediately exits the entire `if-elif-else` chain.

The remaining conditions are **never checked**.

This behavior makes `if-elif-else` faster than writing multiple separate `if` statements.

---

# Example – Character Analyzer

This is one of the main examples discussed in class.

```python
ch = input("Enter a character: ")

if 'A' <= ch <= 'Z':
    print("Capital Letter")

elif 'a' <= ch <= 'z':
    print("Small Letter")

elif '0' <= ch <= '9':
    print("Digit")

else:
    print("Special Symbol")
```

---

## Sample Output 1

```text
Enter a character:
A

Capital Letter
```

---

## Sample Output 2

```text
Enter a character:
g

Small Letter
```

---

## Sample Output 3

```text
Enter a character:
8

Digit
```

---

## Sample Output 4

```text
Enter a character:
@

Special Symbol
```

This complete character analyzer is demonstrated in the lecture to explain how multiple conditions are handled using `if-elif-else`. :contentReference[oaicite:0]{index=0}

---

# Step-by-Step Working

Suppose

```text
Input

g
```

Python checks

```
'A' <= 'g' <= 'Z'

↓

False
```

Moves to

```
'a' <= 'g' <= 'z'

↓

True
```

Therefore,

Python prints

```text
Small Letter
```

The remaining conditions are skipped.

---

Suppose

```text
Input

@
```

Python checks

```
Capital?

↓

False

Small?

↓

False

Digit?

↓

False
```

None of the conditions match.

Therefore,

the `else` block executes.

---

# Why Use `elif` Instead of Multiple `if`s?

### Incorrect Approach

```python
if 'A' <= ch <= 'Z':
    print("Capital")

if 'a' <= ch <= 'z':
    print("Small")

if '0' <= ch <= '9':
    print("Digit")
```

Python evaluates **every condition**, even after finding a match.

---

### Correct Approach

```python
if 'A' <= ch <= 'Z':
    print("Capital")

elif 'a' <= ch <= 'z':
    print("Small")

elif '0' <= ch <= '9':
    print("Digit")

else:
    print("Special Symbol")
```

As soon as one condition is true,

Python stops checking further conditions.

This improves efficiency.

---

# Nested `if` Statement

A **Nested `if`** means placing one `if` statement inside another `if` or `else` block.

It is useful when a second condition should only be checked after the first condition becomes true.

---

# Syntax

```python
if condition1:

    if condition2:
        statements

    else:
        statements

else:
    statements
```

---

# Flow

```text
Condition 1

│

├── True

│      │

│      Condition 2

│      │

│      ├── True

│      └── False

│

└── False
```

---

# Example

```python
age = 20
citizen = True

if age >= 18:

    if citizen:
        print("Eligible to Vote")

    else:
        print("Not a Citizen")

else:
    print("Minor")
```

---

## Output

```text
Eligible to Vote
```

---

# Working

Python first checks

```
age >= 18

↓

True
```

Only then does it enter the second `if`.

```
citizen

↓

True
```

Therefore,

```text
Eligible to Vote
```

is printed.

---

# Why Use Nested `if`?

Nested `if` is useful when

- the second condition depends on the first,
- checking the second condition before the first would not make sense.

Examples

- ATM PIN → Balance Check
- Login → Role Verification
- College Admission → Document Verification

---

# Lecture Assignment – Greatest of Three Numbers

At the end of the lecture, the instructor gives the following assignment.

### Problem

Accept three integers from the user and print the greatest number.

### Constraints

- Do **not** use logical operators (`and`, `or`).
- Do **not** use relational cascading.
- Solve the problem using **Nested `if` statements**.

Example

```text
Input

10

20

15

Output

20 is Greatest
```

This assignment is meant to strengthen your understanding of nested decision-making. It is solved in the next lecture.

---

# Common Mistakes

### Using Multiple `if`s Instead of `elif`

Wrong

```python
if condition1:
    ...

if condition2:
    ...
```

Preferred

```python
if condition1:
    ...

elif condition2:
    ...
```

---

### Forgetting the Colon

Wrong

```python
elif condition
```

Output

```text
SyntaxError
```

---

### Incorrect Indentation

Wrong

```python
if condition:

print("Hello")
```

Output

```text
IndentationError
```

---

# Comparison

| `if` | `if-else` | `if-elif-else` |
|------|-----------|----------------|
| One condition | Two outcomes | Multiple outcomes |
| Executes when condition is True | Chooses one of two blocks | Chooses one among many blocks |
| Simplest decision statement | Binary decision | Multi-way decision |

---

# Key Points

- `if-elif-else` is used for multiple conditions.
- Python checks conditions from top to bottom.
- Only the **first true condition** executes.
- Remaining conditions are skipped.
- Nested `if` means placing one `if` inside another.
- Nested `if` is useful when one condition depends on another.
- Greatest of three numbers is a classic Nested `if` problem.

---

# Quick Revision

✔ `elif` stands for **else if**.

✔ Python stops checking after the first `True` condition.

✔ Use `elif` instead of multiple `if`s for mutually exclusive conditions.

✔ Nested `if` is an `if` inside another `if`.

✔ The lecture assignment is to find the greatest of three numbers using Nested `if` without using logical operators.

---

**Next Part:** Single-line `if-else` (Python's ternary-style expression), Kid/Teenager/Adult examples, lecture exercises, practice programs, interview questions, and complete lecture summary.
========================================================================================================================================================================================================
# Part 6 – Single-Line `if-else` (Conditional Expression)

In previous sections, we learned the standard `if` and `if-else` statements.

Sometimes, however, the body of an `if-else` consists of only **one statement**. Writing multiple lines for such simple decisions can make the code unnecessarily long.

Python provides a shorter and cleaner way of writing such conditions, commonly called the **Conditional Expression** or **Single-Line `if-else`**.

Although many programmers informally call it the **ternary operator**, Python does **not** use the `?:` operator like C, C++, or Java.

Instead, Python uses a readable English-like syntax.

---

# Syntax

```python
value_if_true if condition else value_if_false
```

General form

```python
result = expression1 if condition else expression2
```

### Working

- If the condition is `True`, `expression1` is evaluated.
- Otherwise, `expression2` is evaluated.

Unlike the normal `if-else` statement, this expression **returns a value**.

---

# Comparison with Normal `if-else`

### Normal `if-else`

```python
age = 20

if age >= 18:
    print("Eligible")
else:
    print("Not Eligible")
```

---

### Single-Line Version

```python
age = 20

print("Eligible") if age >= 18 else print("Not Eligible")
```

Both programs produce the same output.

---

# Example 1 – Even or Odd Number

```python
num = int(input("Enter a Number: "))

print("Even") if num % 2 == 0 else print("Odd")
```

### Output

```text
Enter a Number:
12

Even
```

Another Output

```text
Enter a Number:
17

Odd
```

This example demonstrates how a complete `if-else` block can be written in a single line.

---

# Example 2 – Store Result in a Variable

Instead of printing directly, we can store the result.

```python
num = 15

result = "Even" if num % 2 == 0 else "Odd"

print(result)
```

Output

```text
Odd
```

---

# Example 3 – Voting Eligibility

```python
age = int(input("Enter Age: "))

print("Eligible to Vote") if age >= 18 else print("Not Eligible")
```

Output

```text
Enter Age:
21

Eligible to Vote
```

---

# Nested Conditional Expression

Python also allows one conditional expression inside another.

Example

```python
age = 15

status = "Adult" if age >= 18 else "Minor"

print(status)
```

Output

```text
Minor
```

---

# Multiple Conditions in One Line

Sometimes there are more than two possible outcomes.

Python allows multiple conditional expressions.

### Example – Kid / Teenager / Adult

```python
age = int(input("Enter Age: "))

print("Kid") if age < 13 else print("Teenager") if age < 18 else print("Adult")
```

### Output 1

```text
Enter Age:
8

Kid
```

---

### Output 2

```text
Enter Age:
16

Teenager
```

---

### Output 3

```text
Enter Age:
25

Adult
```

This style is shown in class to demonstrate that multiple conditions can also be expressed in a single line, though readability may suffer for complex logic. :contentReference[oaicite:0]{index=0}

---

# Should We Always Use Single-Line `if-else`?

**No.**

Use it only when:

- The condition is simple.
- Only one statement is executed.
- Readability is maintained.

For longer logic, always use the normal multi-line `if-else`.

---

# Advantages

- Short and concise.
- Easy to write for simple decisions.
- Improves readability for very small conditions.
- Useful for assigning values.

---

# Disadvantages

- Difficult to read when multiple conditions are nested.
- Not suitable for large code blocks.
- Can reduce maintainability if overused.

---

# Practice Programs

## Program 1 – Even or Odd

```python
num = int(input("Enter Number: "))

if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```

---

## Program 2 – Single-Line Even/Odd

```python
num = int(input("Enter Number: "))

print("Even") if num % 2 == 0 else print("Odd")
```

---

## Program 3 – Capital, Small, Digit or Symbol

```python
ch = input("Enter Character: ")

if 'A' <= ch <= 'Z':
    print("Capital Letter")

elif 'a' <= ch <= 'z':
    print("Small Letter")

elif '0' <= ch <= '9':
    print("Digit")

else:
    print("Special Symbol")
```

---

## Program 4 – Voting Eligibility

```python
age = int(input("Enter Age: "))

if age >= 18:
    print("Eligible to Vote")
else:
    print("Not Eligible")
```

---

## Program 5 – Unicode Value

```python
ch = input("Enter Character: ")

print("Unicode Value =", ord(ch))
```

---

# Interview Questions

### 1. Why does Python use indentation?

To define code blocks instead of curly braces.

---

### 2. What is relational cascading?

Writing multiple comparisons together.

Example

```python
'A' <= ch <= 'Z'
```

---

### 3. What does `ord()` return?

The Unicode (ASCII) value of a character.

---

### 4. Difference between `if` and `if-else`?

- `if` executes only when the condition is true.
- `if-else` executes one of two blocks.

---

### 5. Difference between `if-else` and `if-elif-else`?

- `if-else` handles two outcomes.
- `if-elif-else` handles multiple outcomes.

---

### 6. What is a Nested `if`?

An `if` statement inside another `if` or `else` block.

---

### 7. Does Python have the `?:` ternary operator?

No.

Python uses

```python
value_if_true if condition else value_if_false
```

---

### 8. Why is `65 <= ch <= 90` invalid?

Because `ch` is a string.

Use

```python
ord(ch)
```

instead.

---

# Exam-Oriented Points

- `if` executes only when the condition is `True`.
- `else` never has a condition.
- `elif` is used for multiple conditions.
- Python stops checking after the first `True` condition.
- Python uses indentation instead of `{}`.
- `ord()` converts a character to its Unicode value.
- `if 'A' <= ch <= 'Z'` is preferred over `ch >= 'A' and ch <= 'Z'`.
- Single-line `if-else` is useful only for simple statements.

---

# Complete Lecture Summary

In this lecture, we first explored the rules governing C-style string formatting and learned that the number of format specifiers must match the number of supplied variables. We also studied how different format specifiers behave with various data types, including integers, floats, strings, characters, and Boolean values.

Next, we learned the modern **`.format()`** method introduced in Python 3, which replaces `%`-style formatting with placeholders (`{}`), supports indexed placeholders, and offers better readability and flexibility.

The second half of the lecture focused on **Decision Control Statements**, beginning with the `if` statement, followed by `if-else`, `if-elif-else`, and Nested `if`. We understood how Python evaluates conditions, why indentation is mandatory, and how relational cascading makes conditions more concise.

Practical programs included **Voting Eligibility**, **Even/Odd**, **Capital/Small Letter Checker**, **Character Analyzer (Capital, Small, Digit, Special Symbol)**, and discussions on using `ord()` to compare characters through Unicode values.

Finally, we learned Python's **single-line conditional expression**, which provides a compact alternative to the traditional `if-else` statement for simple decisions.

---

# Quick Revision

- `%d` → Integer
- `%f` → Floating-point number
- `%s` → String
- `%c` → Character
- `.format()` replaces `%` formatting in modern Python.
- `{}` are placeholders.
- `if` → One condition.
- `if-else` → Two outcomes.
- `if-elif-else` → Multiple outcomes.
- Nested `if` → `if` inside another `if`.
- Python uses indentation instead of braces.
- `ord()` returns a character's Unicode value.
- Relational cascading (`'A' <= ch <= 'Z'`) is preferred over using `and`.
- Python's conditional expression is written as:

```python
value_if_true if condition else value_if_false
```

---
