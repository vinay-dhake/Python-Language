# Python Programming – Advanced User Input (`split()` Method)

---

# Introduction

In the previous lecture, we learned how to take input using the `input()` function. However, if we wanted multiple values, we had to call `input()` multiple times.

Example:

```python
roll = input("Enter Roll Number: ")
name = input("Enter Name: ")
percentage = input("Enter Percentage: ")
```

Although this works, it is not efficient because the user has to press **Enter** after every value.

Python provides a much better solution using the **`split()`** method, allowing us to accept multiple values in a **single line**.

This concept is introduced at the beginning of the lecture before discussing `eval()`. :contentReference[oaicite:0]{index=0}

---

# The `split()` Method

The `split()` method belongs to the **string** data type.

Its purpose is to divide a string into multiple smaller strings.

Syntax:

```python
string.split(separator)
```

- `separator` is optional.
- If no separator is given, Python uses **space** as the default separator.

The result of `split()` is always a **list of strings**.

---

# How `split()` Works

Suppose we have the following string:

```python
text = "I love India"
```

Calling

```python
text.split()
```

produces

```python
["I", "love", "India"]
```

Python finds every space and separates the words.

Internally,

```
"I love India"

↓

split()

↓

["I", "love", "India"]
```

---

# Example 1 – Basic Splitting

```python
text = "I love India"

a, b, c = text.split()

print(a)
print(b)
print(c)
```

### Output

```text
I
love
India
```

### Explanation

The list returned by `split()` is automatically unpacked into three variables.

This is the first classroom example used to explain the `split()` method.

---

# What is Unpacking?

Python allows multiple variables to receive values from a sequence simultaneously.

Example

```python
a, b, c = [10, 20, 30]
```

Memory

```
10 → a

20 → b

30 → c
```

This feature is called **Sequence Unpacking** (or simply **Unpacking**).

---

# Default Separator

If no separator is specified,

Python assumes

```python
split(" ")
```

Therefore,

```python
"Python Programming Language".split()
```

returns

```python
["Python", "Programming", "Language"]
```

---

# Custom Separators

Sometimes the values are not separated by spaces.

Instead,

they may use

- `_`
- `,`
- `-`
- `:`
- `|`

In such cases,

we must specify the separator explicitly.

---

# Example 2 – Splitting Using Underscore

```python
text = "I_love_India"

a, b, c = text.split("_")

print(a)
print(b)
print(c)
```

### Output

```text
I
love
India
```

This example is demonstrated in the lecture after showing the default space separator.

---

# What Happens Without the Separator?

Consider

```python
text = "I_love_India"

a, b, c = text.split()
```

Python searches only for spaces.

Since there are no spaces,

it returns

```python
["I_love_India"]
```

Now Python tries to store

one value

into

three variables.

Result

```text
ValueError:
not enough values to unpack
```

This is exactly why the lecture emphasizes specifying `"_"` as the separator when underscores are used.

---

# Taking Multiple Inputs in One Line

The biggest advantage of `split()` is accepting several inputs simultaneously.

Example

```python
roll, name, percentage = input(
    "Enter roll number, name and percentage: "
).split()
```

User Input

```text
101 Sumit 85.5
```

Variables become

```
roll

↓

"101"

name

↓

"Sumit"

percentage

↓

"85.5"
```

Notice that **all three values are still strings**.

No automatic type conversion takes place.

This example is one of the primary practical demonstrations in the lecture. :contentReference[oaicite:1]{index=1}

---

# Example 3 – Printing Multiple Inputs

```python
roll, name, percentage = input(
    "Enter roll number, name and percentage: "
).split()

print("Roll Number :", roll)
print("Name :", name)
print("Percentage :", percentage)
```

### Sample Output

```text
Enter roll number, name and percentage:
101 Sumit 85.5

Roll Number : 101
Name : Sumit
Percentage : 85.5
```

---

# Data Types After `split()`

Even if the user enters

```text
101 Sumit 85.5
```

Python stores

```python
roll = "101"

name = "Sumit"

percentage = "85.5"
```

Checking the type

```python
print(type(roll))
```

Output

```python
<class 'str'>
```

Similarly,

```python
print(type(percentage))
```

Output

```python
<class 'str'>
```

Therefore,

explicit conversion is still required.

---

# Converting the Values

Example

```python
roll, name, percentage = input(
    "Enter details: "
).split()

roll = int(roll)
percentage = float(percentage)

print(type(roll))
print(type(name))
print(type(percentage))
```

Output

```python
<class 'int'>
<class 'str'>
<class 'float'>
```

---

# Advantages of `split()`

✔ Accepts multiple values in one line.

✔ Reduces the number of `input()` calls.

✔ Makes code shorter.

✔ Improves readability.

✔ Very useful in competitive programming.

---

# Common Mistakes

### Forgetting the Separator

```python
text = "A_B_C"

print(text.split())
```

Output

```python
['A_B_C']
```

Correct

```python
text.split("_")
```

---

### Mismatch During Unpacking

```python
a, b = "A B C".split()
```

Output

```text
ValueError
```

because

three values

cannot fit into

two variables.

---

### Assuming Automatic Type Conversion

```python
roll, marks = input().split()

print(type(roll))
```

Output

```python
<class 'str'>
```

Always remember:

`split()` **only separates** strings.

It **does not** convert data types.

---

# Key Points

- `split()` is a string method.
- It returns a list.
- Default separator is a space.
- Custom separators like `"_"`, `","`, and `"-"` can be specified.
- Python supports unpacking directly into variables.
- Values returned by `split()` are always strings.
- Type conversion must be performed separately if numeric operations are required.

---
==============================================================================================================================================================
# The `eval()` Function

In the previous section, we learned that the `split()` method only separates strings. Whenever we wanted numerical calculations, we had to manually convert the values using functions like `int()` or `float()`.

Python provides another powerful built-in function called **`eval()`** that can automatically evaluate Python expressions and determine the appropriate data type.

Unlike `int()` and `float()`, which convert to only one specific type, `eval()` analyzes the given string and executes it as a valid Python expression.

The lecture introduces `eval()` as a function that can both evaluate expressions and perform automatic type conversion. :contentReference[oaicite:0]{index=0}

---

# What is `eval()`?

The word **eval** stands for **Evaluate**.

The `eval()` function takes a string as input and evaluates it as a valid Python expression.

Syntax

```python
eval(expression)
```

Where

- **expression** is a string containing a valid Python expression.

---

# How `eval()` Works

Consider

```python
eval("2 + 3")
```

Python internally performs

```
String

↓

"2 + 3"

↓

Python Interpreter

↓

2 + 3

↓

5
```

Instead of treating `"2 + 3"` as plain text,

Python actually performs the calculation.

---

# Example 1 – Evaluating a Simple Expression

```python
print(eval("2 + 3"))
```

Output

```text
5
```

---

# Example 2 – Following Operator Precedence

```python
print(eval("3 * 6 + 2"))
```

Output

```text
20
```

### Explanation

Python evaluates the expression according to operator precedence.

```
3 × 6

↓

18

↓

18 + 2

↓

20
```

This example is shown in the lecture to demonstrate that `eval()` follows normal arithmetic rules (BODMAS/precedence). :contentReference[oaicite:1]{index=1}

---

# `eval()` is More Than a Calculator

Many beginners think `eval()` only performs calculations.

Actually,

it can evaluate **any valid Python expression**.

Examples

```python
eval("'Python'")
```

returns

```text
Python
```

Example

```python
eval("True")
```

returns

```python
True
```

Example

```python
eval("[10, 20, 30]")
```

returns

```python
[10, 20, 30]
```

---

# Automatic Type Conversion

One of the biggest advantages of `eval()` is that it automatically detects the correct data type.

---

# Example 3 – Integer Conversion

```python
x = eval("25")

print(x)
print(type(x))
```

Output

```text
25

<class 'int'>
```

---

# Example 4 – Float Conversion

```python
x = eval("25.1")

print(x)
print(type(x))
```

Output

```text
25.1

<class 'float'>
```

Unlike

```python
input()
```

which always returns a string,

`eval()` returns the appropriate Python object.

This automatic type detection is one of the main concepts emphasized in the lecture. :contentReference[oaicite:2]{index=2}

---

# Combining `input()` and `eval()`

Instead of writing

```python
age = int(input("Enter Age: "))
```

we can write

```python
age = eval(input("Enter Age: "))
```

If the user enters

```text
20
```

then

```python
age
```

becomes

```python
20
```

(Integer)

If the user enters

```text
20.5
```

then

```python
age
```

becomes

```python
20.5
```

(Float)

No manual conversion is required.

---

# Example 5 – Smart Calculator

```python
expression = input("Enter expression: ")

result = eval(expression)

print("Result is", result)
```

### Sample Output

```text
Enter expression:
25 + 10

Result is 35
```

Another Example

```text
Enter expression:
5 * 12

Result is 60
```

Another Example

```text
Enter expression:
50 / 4

Result is 12.5
```

This calculator example is one of the most important demonstrations of `eval()` in the lecture. :contentReference[oaicite:3]{index=3}

---

# Execution Flow

```
User Input

↓

"25+10"

↓

eval()

↓

Python executes

↓

35

↓

print()
```

---

# The `None` Return Value

The lecture also discusses an important side concept.

Not every Python function returns a useful value.

Some functions perform an action and return

```python
None
```

---

# Example 6

```python
x = print("Hello")

print(x)
```

Output

```text
Hello

None
```

### Why?

The

```python
print()
```

function displays text on the screen.

However,

it does **not** return any meaningful value.

Therefore,

Python automatically returns

```python
None
```

The variable

```python
x
```

stores

```python
None
```

This example is included in the lecture while explaining return values and `NoneType`. :contentReference[oaicite:4]{index=4}

---

# What is `None`?

`None` is a special built-in object in Python.

It represents

> **No Value** or **Nothing**.

Data Type

```python
print(type(None))
```

Output

```python
<class 'NoneType'>
```

---

# Advantages of `eval()`

✔ Automatically detects data type.

✔ Evaluates mathematical expressions.

✔ Reduces manual type conversion.

✔ Useful for quick calculators.

---

# Disadvantages of `eval()`

⚠ **Security Risk**

`eval()` executes whatever the user enters.

Example

```python
eval(input())
```

If a malicious user enters harmful Python code,

it may get executed.

Because of this,

`eval()` should **never** be used on untrusted user input in real-world applications.

Instead,

prefer explicit conversion using

```python
int()

float()

str()

bool()
```

---

# Common Mistakes

### Using `eval()` for Every Input

Wrong

```python
name = eval(input())
```

If the user enters

```text
Sachin
```

Python raises

```text
NameError
```

because

```python
Sachin
```

is treated as a variable name.

Correct

```python
name = input()
```

---

### Forgetting Quotes

```python
eval(Python)
```

Output

```text
NameError
```

Correct

```python
eval("'Python'")
```

---

# Key Points

- `eval()` evaluates a string as a Python expression.
- It follows normal operator precedence.
- It automatically detects data types.
- `eval("25")` returns an integer.
- `eval("25.5")` returns a float.
- `print()` returns `None`.
- `None` belongs to the `NoneType` class.
- Avoid using `eval()` with untrusted input because of security risks.

---
=============================================================================================================================================================
# Command Line Arguments (`sys.argv`)

Until now, all user input was taken **after** the program started using the `input()` function.

However, Python also provides another method of supplying input **before the program starts**.

This method is called **Command Line Arguments (CLA)**.

Instead of asking the user for values while the program is running, the values are supplied directly when executing the Python file from the terminal.

The lecture introduces Command Line Arguments as another technique for passing data to a Python program without using `input()`. :contentReference[oaicite:0]{index=0}

---

# What are Command Line Arguments?

Command Line Arguments are values passed to a Python program **at the time of execution**.

Example

```bash
python program.py Sachin
```

Here,

```
python
```

starts the Python interpreter.

```
program.py
```

is the Python file.

```
Sachin
```

is the command line argument.

Instead of asking

```python
name = input("Enter Name: ")
```

the value

```
Sachin
```

is supplied directly.

---

# Why are Command Line Arguments Used?

Command Line Arguments are commonly used in

- System utilities
- Automation scripts
- File processing programs
- Backup tools
- Batch processing
- Server-side applications

Many operating system commands internally use command line arguments.

For example,

```bash
mkdir PythonNotes
```

Here,

```
PythonNotes
```

is a command line argument passed to the `mkdir` command.

This real-world comparison is discussed in the lecture to explain why command line arguments are useful.

---

# The `sys` Module

Python stores all command line arguments inside a list called

```python
argv
```

which belongs to the built-in

```python
sys
```

module.

Before using it,

we must import it.

```python
from sys import argv
```

---

# What is `argv`?

`argv` stands for

> **Argument Vector**

It is a list containing every argument passed to the program.

Structure

```
argv

↓

[
    File Name,
    Argument 1,
    Argument 2,
    Argument 3,
    ...
]
```

Every element inside

```python
argv
```

is stored as a **string**.

This is emphasized in the lecture before performing arithmetic using command line arguments. :contentReference[oaicite:1]{index=1}

---

# Understanding `argv[0]`

The first element

```python
argv[0]
```

always stores

> **the name (or path) of the Python file**.

Example

```bash
python hello.py Sachin
```

Internally

```
argv

↓

[
    "hello.py",
    "Sachin"
]
```

Therefore,

```python
print(argv[0])
```

Output

```text
hello.py
```

---

# Understanding `argv[1]`

The first actual user argument is stored in

```python
argv[1]
```

Example

```bash
python hello.py Sachin
```

Memory

```
argv

↓

0

↓

hello.py

1

↓

Sachin
```

Therefore

```python
print(argv[1])
```

Output

```text
Sachin
```

---

# Example 1 – Greeting User

```python
from sys import argv

print("Hello", argv[1])
```

Execution

```bash
python hello.py Sachin
```

Output

```text
Hello Sachin
```

This is the first practical example used in the lecture for `sys.argv`. :contentReference[oaicite:2]{index=2}

---

# What Happens if No Argument is Given?

Suppose we execute

```bash
python hello.py
```

Now,

```
argv

↓

[
    "hello.py"
]
```

There is no

```python
argv[1]
```

Therefore,

Python raises

```text
IndexError:
list index out of range
```

Always ensure the required number of arguments are supplied.

---

# Accepting Multiple Arguments

Example

```bash
python demo.py Sachin Naman Ravi
```

Memory

```
argv

↓

[
    "demo.py",

    "Sachin",

    "Naman",

    "Ravi"
]
```

Now

```python
argv[1]
```

contains

```
Sachin
```

```python
argv[2]
```

contains

```
Naman
```

```python
argv[3]
```

contains

```
Ravi
```

---

# Example 2 – Unknown Number of Arguments

Sometimes we don't know how many arguments the user will pass.

Instead of accessing each index separately,

Python provides **list slicing**.

Example

```python
from sys import argv

print("Hello", argv[1:])
```

Execution

```bash
python demo.py Sachin Naman Ravi
```

Output

```text
Hello ['Sachin', 'Naman', 'Ravi']
```

### Explanation

The slice

```python
argv[1:]
```

means

```
Start from index 1

↓

Go till the end
```

This example is shown in the lecture to demonstrate handling a variable number of command line arguments. :contentReference[oaicite:3]{index=3}

---

# Why Does Addition Fail?

Consider

```python
from sys import argv

print(argv[1] + argv[2])
```

Execution

```bash
python sum.py 10 20
```

Output

```text
1020
```

Why?

Because

```
argv

↓

Strings
```

Python performs

```python
"10" + "20"
```

instead of

```python
10 + 20
```

The result is string concatenation.

---

# Example 3 – Addition Using `eval()`

To perform arithmetic,

we can use

```python
eval()
```

```python
from sys import argv

sum_val = eval(argv[1]) + eval(argv[2])

print("Their Sum is", sum_val)
```

Execution

```bash
python sum.py 10.1 20.2
```

Output

```text
Their Sum is 30.299999999999997
```

The slight difference is caused by normal floating-point precision.

This example combines `sys.argv` with `eval()` exactly as demonstrated in the lecture. :contentReference[oaicite:4]{index=4}

---

# Execution Flow

```
Terminal

↓

python sum.py 10 20

↓

argv

↓

["sum.py", "10", "20"]

↓

eval()

↓

10

20

↓

Addition

↓

30

↓

print()
```

---

# `input()` vs Command Line Arguments

| `input()` | `sys.argv` |
|------------|------------|
| Takes input after the program starts | Takes input before execution |
| Interactive | Non-interactive |
| Uses keyboard during execution | Uses terminal command |
| Suitable for normal applications | Suitable for automation and scripts |

---

# Advantages of Command Line Arguments

✔ Faster execution.

✔ Useful for automation.

✔ No interactive input required.

✔ Widely used in scripting.

✔ Ideal for batch processing.

---

# Common Mistakes

### Forgetting to Import `argv`

Wrong

```python
print(argv[1])
```

Correct

```python
from sys import argv
```

---

### Assuming `argv` Contains Integers

Wrong

```python
print(argv[1] + argv[2])
```

Output

```text
1020
```

Correct

```python
print(eval(argv[1]) + eval(argv[2]))
```

or

```python
print(int(argv[1]) + int(argv[2]))
```

---

### Accessing Missing Arguments

```python
print(argv[5])
```

without enough command line arguments results in

```text
IndexError
```

---

# Key Points

- Command Line Arguments are supplied before program execution.
- They are stored inside `sys.argv`.
- `argv` is a list.
- `argv[0]` stores the program name.
- `argv[1]`, `argv[2]`, etc., store user arguments.
- All command line arguments are stored as strings.
- Use `eval()` or explicit type conversion for arithmetic operations.
- `argv[1:]` returns all user-supplied arguments as a list.

---
============================================================================================================================================================
# C-Style String Formatting (Format Specifiers)

Before modern formatting methods like **f-strings** and `str.format()`, Python used **C-style formatting**.

This formatting style comes from the C programming language and is still supported in Python for backward compatibility.

It allows variables to be inserted directly into a string using **format specifiers**.

The lecture introduces C-style formatting after Command Line Arguments to demonstrate formatted output. :contentReference[oaicite:0]{index=0}

---

# Why Do We Need String Formatting?

Suppose we want to display the value of a variable.

Without formatting

```python
a = 25

print("Value of A is", a)
```

Output

```text
Value of A is 25
```

Although correct,

sometimes we want complete control over the output format.

This is where format specifiers become useful.

---

# General Syntax

```python
"Message %specifier" % value
```

If multiple variables are present,

```python
"Message %specifier %specifier" % (value1, value2)
```

Notice

There is **no comma** between the string and `%`.

Correct

```python
print("Value is %d" % a)
```

Incorrect

```python
print("Value is %d", a)
```

The lecture specifically points out this syntax difference. :contentReference[oaicite:1]{index=1}

---

# Common Format Specifiers

| Specifier | Used For |
|------------|----------|
| `%d` | Integer |
| `%i` | Integer |
| `%f` | Floating Point Number |
| `%s` | String |
| `%c` | Single Character |

---

# `%d` — Integer Formatting

The `%d` format specifier is used for integers.

Example

```python
a = 25

print("Value of A is %d" % a)
```

Output

```text
Value of A is 25
```

This is the first formatting example demonstrated in the lecture.

---

# `%i` — Integer Formatting

`%i` behaves exactly like `%d`.

Example

```python
a = 50

print("Value of A is %i" % a)
```

Output

```text
Value of A is 50
```

Both `%d` and `%i` are interchangeable for integers.

---

# `%f` — Floating Point Formatting

The `%f` specifier is used for decimal numbers.

Example

```python
price = 99.5

print("Price is %f" % price)
```

Output

```text
Price is 99.500000
```

Notice

Python prints **6 decimal places** by default.

This default behavior is highlighted during the lecture. :contentReference[oaicite:2]{index=2}

---

# Controlling Decimal Places

To display only two decimal places,

use

```python
%.2f
```

Example

```python
price = 99.56789

print("Price is %.2f" % price)
```

Output

```text
Price is 99.57
```

Similarly,

```python
print("%.3f" % 5.67891)
```

Output

```text
5.679
```

---

# `%s` — String Formatting

Used for strings.

Example

```python
name = "Sachin"

print("Welcome %s" % name)
```

Output

```text
Welcome Sachin
```

---

# `%c` — Character Formatting

Used for a single character.

Example

```python
ch = 'A'

print("Character is %c" % ch)
```

Output

```text
Character is A
```

**Important**

`%c` expects exactly **one character**.

Passing a complete string causes an error.

---

# Formatting Multiple Variables

When multiple variables are inserted,

they must be placed inside parentheses.

Example

```python
a = 25
b = 2.5

print("Value of A is %d and Value of B is %f" % (a, b))
```

Output

```text
Value of A is 25 and Value of B is 2.500000
```

This is one of the main examples demonstrated in the lecture. :contentReference[oaicite:3]{index=3}

---

# Another Example

```python
name = "Sumit"
age = 22

print("Name = %s Age = %d" % (name, age))
```

Output

```text
Name = Sumit Age = 22
```

---

# Matching Specifiers and Variables

The number of format specifiers

must match

the number of variables.

Correct

```python
print("%d %d" % (10, 20))
```

Incorrect

```python
print("%d %d" % 10)
```

Output

```text
TypeError
```

Similarly,

```python
print("%d" % (10, 20))
```

also raises an error because extra values are supplied.

---

# Common Mistakes

### Using Wrong Specifier

```python
name = "Sachin"

print("%d" % name)
```

Output

```text
TypeError
```

Correct

```python
print("%s" % name)
```

---

### Using `%c` with Multiple Characters

```python
print("%c" % "ABC")
```

Output

```text
TypeError
```

Correct

```python
print("%c" % 'A')
```

---

### Forgetting Parentheses

Wrong

```python
print("%d %f" % a, b)
```

Correct

```python
print("%d %f" % (a, b))
```

---

# C-Style Formatting vs Modern Formatting

| C-Style | Modern |
|----------|---------|
| `%d` | `{}` or `f""` |
| `%f` | `{:.2f}` |
| `%s` | `{}` |
| Older syntax | Recommended today |

Although modern Python prefers **f-strings** and `str.format()`, understanding `%` formatting is useful because it still appears in older codebases.

---

# Best Practices

- Use the correct format specifier for the data type.
- Match the number of specifiers with the number of variables.
- Use `%.2f` for cleaner floating-point output.
- Prefer modern formatting (`f-strings`) in new projects, but know `%` formatting for legacy code.

---

# Key Points

- C-style formatting uses the `%` operator.
- `%d` and `%i` are used for integers.
- `%f` is used for floating-point numbers.
- `%f` prints 6 decimal places by default.
- `%.2f` limits output to two decimal places.
- `%s` formats strings.
- `%c` formats a single character.
- Multiple variables must be enclosed in parentheses.
- The number of specifiers must match the number of supplied values.

---

# Quick Revision

- `split()` separates strings into multiple parts.
- `eval()` evaluates Python expressions and performs automatic type detection.
- `print()` returns `None`.
- Command Line Arguments are stored in `sys.argv`.
- `argv[0]` stores the script name.
- `argv[1:]` returns all user-supplied arguments.
- `%d` → Integer
- `%f` → Float
- `%s` → String
- `%c` → Character
- `%.2f` displays two decimal places.

---

# Summary

In this lecture, we learned advanced techniques for handling user input using the `split()` method, allowing multiple values to be accepted in a single line. We explored the powerful `eval()` function, which can evaluate Python expressions and automatically determine appropriate data types, while also discussing its advantages and security concerns.

We then introduced **Command Line Arguments** using `sys.argv`, understanding how arguments are passed from the terminal, how `argv` is structured, and how it can be combined with `eval()` for arithmetic operations. Finally, we studied **C-style string formatting**, including format specifiers such as `%d`, `%f`, `%s`, and `%c`, learned how to format both single and multiple variables, and discussed common mistakes and best practices.

---
=============================================================================================================================================================
# Practice Programs

The following practice programs help strengthen the concepts covered in this lecture.

---

## Program 1 — Accept Three Values in One Line

```python
roll, name, percentage = input(
    "Enter Roll Number, Name and Percentage: "
).split()

print("Roll Number :", roll)
print("Name :", name)
print("Percentage :", percentage)
```

---

## Program 2 — Sum of Two Numbers Using `eval()`

```python
a = eval(input("Enter First Number: "))
b = eval(input("Enter Second Number: "))

print("Sum =", a + b)
```

---

## Program 3 — Smart Calculator

```python
expression = input("Enter Mathematical Expression: ")

print("Answer =", eval(expression))
```

Example

```text
Input

25+15*2

Output

55
```

---

## Program 4 — Addition Using Command Line Arguments

```python
from sys import argv

a = eval(argv[1])
b = eval(argv[2])

print("Sum =", a + b)
```

Execution

```bash
python demo.py 15 25
```

Output

```text
Sum = 40
```

---

## Program 5 — Display Student Information

```python
roll = int(input("Enter Roll Number : "))
name = input("Enter Name : ")
percentage = float(input("Enter Percentage : "))

print("Roll :", roll)
print("Name :", name)
print("Percentage :", percentage)
```

---

# Important Notes

- `split()` always returns a list.
- Values returned by `split()` are strings.
- `eval()` executes Python expressions.
- `argv` is a list.
- Every command line argument is stored as a string.
- `%f` prints six decimal places by default.
- `%.2f` prints two decimal places.
- `print()` returns `None`.
- `eval()` should never be used with untrusted input.

---

# Frequently Asked Interview Questions

## 1. What is the return type of `split()`?

A list of strings.

---

## 2. Does `split()` perform type conversion?

No.

It only separates strings.

---

## 3. What is the default separator used by `split()`?

A space character.

---

## 4. Can we specify our own separator?

Yes.

Example

```python
split(",")
split("_")
split("-")
```

---

## 5. What is unpacking?

Assigning multiple values to multiple variables in one statement.

Example

```python
a, b, c = [10, 20, 30]
```

---

## 6. What is `eval()`?

A built-in function that evaluates a string as a valid Python expression.

---

## 7. What are the advantages of `eval()`?

- Automatic type detection
- Expression evaluation
- Useful for calculators

---

## 8. Why is `eval()` considered unsafe?

Because it executes whatever code the user enters.

---

## 9. What is `None`?

A special object representing the absence of a value.

---

## 10. Which data type does `None` belong to?

```python
NoneType
```

---

## 11. What is Command Line Argument?

Input supplied while executing the Python program from the terminal.

---

## 12. What is `argv`?

Argument Vector.

A list containing command line arguments.

---

## 13. What does `argv[0]` contain?

The program (Python file) name.

---

## 14. What does `argv[1]` contain?

The first command line argument.

---

## 15. Which module contains `argv`?

```python
sys
```

---

## 16. Why does

```python
argv[1] + argv[2]
```

perform concatenation?

Because both values are strings.

---

## 17. Which format specifier is used for integers?

```text
%d
```

or

```text
%i
```

---

## 18. Which format specifier is used for floating-point numbers?

```text
%f
```

---

## 19. Which format specifier is used for strings?

```text
%s
```

---

## 20. Which format specifier is used for characters?

```text
%c
```

---

# Exam-Oriented Points

✔ `split()` returns a list.

✔ Default separator is a space.

✔ `eval()` executes Python expressions.

✔ `input()` always returns a string.

✔ `argv` stores command line arguments.

✔ `argv[0]` stores the filename.

✔ Command line arguments are always strings.

✔ `print()` returns `None`.

✔ `%f` displays six digits after the decimal by default.

✔ `%.2f` limits output to two decimal places.

✔ `%d` and `%i` both represent integers.

---

# Comparison Tables

## `input()` vs `eval()`

| `input()` | `eval()` |
|------------|-----------|
| Returns a string | Evaluates expression |
| Does not execute code | Executes Python expressions |
| Safe | Unsafe for untrusted input |
| Requires explicit conversion | Automatically detects numeric types |

---

## `input()` vs Command Line Arguments

| `input()` | Command Line Arguments |
|------------|------------------------|
| Interactive | Non-interactive |
| Values entered after program starts | Values passed before execution |
| Suitable for general applications | Suitable for scripts and automation |

---

## `%d` vs `%f`

| `%d` | `%f` |
|-------|-------|
| Integer | Floating-point number |
| No decimal places | Six decimal places by default |

---

# Quick Revision

- `split()` separates strings.
- Default separator is space.
- Custom separators can be specified.
- Unpacking assigns multiple values simultaneously.
- `eval()` evaluates expressions.
- `eval("2+3")` returns `5`.
- `print()` returns `None`.
- `argv` stores command line arguments.
- `argv[0]` stores the program name.
- `argv[1:]` returns all user arguments except the filename.
- `%d` formats integers.
- `%f` formats floating-point numbers.
- `%s` formats strings.
- `%c` formats a single character.
- `%.2f` limits decimal precision.

---

# Complete Lecture Summary

In this lecture, we explored advanced techniques for handling user input and formatting output in Python. We began by learning how to accept multiple values efficiently using the `split()` method and understood how Python performs sequence unpacking. We also learned that `split()` always returns a list of strings, making explicit type conversion necessary for numerical operations.

Next, we studied the powerful `eval()` function, which evaluates strings as valid Python expressions and automatically determines the appropriate data type. We saw how it can simplify calculator-like programs, while also discussing its security risks and why it should be avoided with untrusted user input.

The lecture then introduced **Command Line Arguments** through the `sys.argv` list, explaining how programs can receive input directly from the terminal. We learned the purpose of `argv[0]`, `argv[1]`, list slicing with `argv[1:]`, and how to combine `eval()` with command line arguments for arithmetic operations.

Finally, we explored **C-style string formatting** using format specifiers such as `%d`, `%i`, `%f`, `%s`, and `%c`. We learned how to format integers, floating-point numbers, strings, and characters, format multiple variables in a single statement, control decimal precision using `%.2f`, and avoid common formatting mistakes.

Overall, this lecture introduced several practical Python features that are widely used in scripting, automation, command-line applications, and day-to-day programming.
===============================================================================================================================================================
