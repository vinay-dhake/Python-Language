# Python Programming - User Input & Modules

---

# Introduction

Most programs become useful only when they can interact with users.

Until now, all values in our programs were **hardcoded**, meaning they were written directly inside the code.

Example:

```python
a = 10
b = 20
print(a + b)
```

Output

```text
30
```

The above program always produces the same output because the values are fixed.

To make programs dynamic, Python allows us to accept values from the keyboard using the **`input()`** function.

This enables users to provide their own data while the program is running.

Examples include:

- Login systems
- Calculator applications
- Banking software
- Student management systems
- Online forms
- Registration portals

Python provides a built-in function called **`input()`** to perform this task. :contentReference[oaicite:0]{index=0}

---

# The `input()` Function

`input()` is a built-in function used to accept data from the keyboard.

Whenever Python encounters an `input()` statement, it temporarily pauses program execution and waits for the user to type something.

After the user presses the **Enter** key, the entered value is returned to the program.

---

## Syntax

```python
input([prompt])
```

The parameter **`prompt`** is optional.

If provided, Python displays the prompt before waiting for user input.

---

# How `input()` Works

Execution takes place in the following order:

1. Python displays the prompt message.
2. The program pauses.
3. The user types a value.
4. The user presses **Enter**.
5. Python returns the entered value.

---

# Important Characteristics of `input()`

✔ Execution pauses until input is entered.

✔ It accepts a single optional prompt.

✔ The returned value is **always a string (`str`)**.

✔ It can read complete lines including spaces.

These characteristics are introduced in the lecture slides before the practical examples. :contentReference[oaicite:1]{index=1}

---

# Return Value of `input()`

One of the most important facts about Python is:

> **Regardless of what the user types, `input()` always returns a string.**

Whether the user enters

```text
10
```

or

```text
3.14
```

or

```text
Sachin
```

Python internally stores all of them as strings.

For example,

```python
x = input()
```

If the user enters

```text
25
```

then internally

```python
x = "25"
```

not

```python
25
```

This concept is emphasized in the PDF because it explains why type conversion is often required. :contentReference[oaicite:2]{index=2}

---

# Example 1 — Using `input()` Without a Prompt

The traditional way is to print a message first and then call `input()`.

```python
print("Enter your name")
name = input()

print("Hello", name)
```

### Sample Output

```text
Enter your name
Sachin
Hello Sachin
```

### Explanation

Execution flow:

```
Print message

↓

Wait for user input

↓

Store entered value in 'name'

↓

Print greeting
```

This example is demonstrated in the lecture slides. :contentReference[oaicite:3]{index=3}

---

# Example 2 — Using `input()` with a Prompt

Instead of writing a separate `print()` statement, we can directly pass the message to `input()`.

```python
name = input("Enter your name")

print("Hello", name)
```

### Sample Output

```text
Enter your nameSachin
Hello Sachin
```

Notice that the cursor remains on the same line because `input()` does **not** automatically move to the next line.

This example is included in both the PDF and lecture. :contentReference[oaicite:4]{index=4}

---

# Example 3 — Accepting Full Name

`input()` can also accept strings containing spaces.

```python
name = input("Enter your full name: ")

print("Hello", name)
```

### Sample Output

```text
Enter your full name: Sachin Kapoor

Hello Sachin Kapoor
```

Unlike some languages, Python reads the **entire line** until the Enter key is pressed.

Therefore,

```
Sachin Kapoor
```

is stored as a single string.

This behavior is demonstrated in the lecture using the "full name" example. :contentReference[oaicite:5]{index=5}

---

# `print()` vs `input()`

Although both functions interact with the console, they behave differently.

| `print()` | `input()` |
|-----------|-----------|
| Displays output | Accepts input |
| Automatically moves to a new line | Cursor stays on the same line |
| Uses `end="\n"` by default | No automatic newline |
| Returns `None` | Returns a string |

---

# Moving the Cursor to the Next Line

If you want the user to enter the value on the next line, use `\n`.

Example

```python
name = input("Enter your name:\n")

print("Hello", name)
```

Output

```text
Enter your name:
Sachin

Hello Sachin
```

---

# How `input()` Stores Data

Suppose the user enters

```text
Python
```

Memory representation:

```
Keyboard

↓

Python

↓

input()

↓

"Python"

↓

name
```

The variable stores the returned string object.

---

# Common Beginner Mistake

Many beginners assume

```python
age = input("Enter age: ")
```

stores an integer.

It does **not**.

If the user enters

```text
18
```

then

```python
type(age)
```

returns

```python
<class 'str'>
```

This is why arithmetic operations require **type conversion**, which we'll cover in the next section.

---

# Key Points

- `input()` makes programs interactive.
- Execution pauses until the user presses Enter.
- The prompt argument is optional.
- `input()` always returns a **string**.
- It can accept complete lines containing spaces.
- `print()` and `input()` behave differently with respect to newlines.

---

```
===============================================================================================================================================================
# Type Conversion (Type Casting)

As discussed earlier,

the `input()` function **always returns a string**, regardless of what the user enters.

For example,

If the user types

```text
10
```

Python stores it as

```python
"10"
```

not

```python
10
```

This becomes a problem whenever we perform mathematical operations.

---

# Why Do We Need Type Conversion?

Suppose we ask the user to enter two numbers.

```python
A = input("Enter first number: ")
B = input("Enter second number: ")

print(A + B)
```

User Input

```text
10
20
```

Output

```text
1020
```

Instead of adding the numbers,

Python joins the two strings together.

This process is called **String Concatenation**.

Since

```python
A
```

contains

```python
"10"
```

and

```python
B
```

contains

```python
"20"
```

Python performs

```python
"10" + "20"
```

which becomes

```text
1020
```

This example is one of the first demonstrations in the lecture when introducing type conversion. :contentReference[oaicite:0]{index=0}

---

# What is Type Conversion?

Type Conversion (also called **Type Casting**) is the process of converting one data type into another.

Python provides several built-in functions for this purpose.

Some commonly used conversion functions are:

| Function | Converts To |
|----------|-------------|
| `int()` | Integer |
| `float()` | Floating Point Number |
| `str()` | String |
| `bool()` | Boolean |

---

# Converting String to Integer

The `int()` function converts a numeric string into an integer.

Syntax

```python
int(value)
```

Example

```python
num = "25"

print(int(num))
print(type(int(num)))
```

Output

```text
25
<class 'int'>
```

---

# Example 1 — Converting During Calculation

Instead of adding strings,

convert them into integers first.

```python
A = input("Enter first integer: ")
B = input("Enter second integer: ")

C = int(A) + int(B)

print("Sum is", C)
```

### Sample Output

```text
Enter first integer: 10
Enter second integer: 20

Sum is 30
```

### Execution Flow

```
User enters

↓

"10"

↓

int("10")

↓

10

+

User enters

↓

"20"

↓

int("20")

↓

20

↓

30
```

This approach is shown in the lecture as the first solution to the concatenation problem. :contentReference[oaicite:1]{index=1}

---

# Example 2 — Converting While Taking Input (Recommended)

Instead of converting later,

we can convert immediately while accepting input.

```python
A = int(input("Enter first integer: "))
B = int(input("Enter second integer: "))

C = A + B

print("Sum is", C)
```

### Sample Output

```text
Enter first integer: 50
Enter second integer: 40

Sum is 90
```

### Why is this Better?

Once converted,

the variables already contain integers.

Therefore,

future calculations become simpler.

This is the recommended approach demonstrated in the lecture. :contentReference[oaicite:2]{index=2}

---

# Example 3 — One-Line Solution

Python allows function nesting.

Therefore,

the entire program can be written in one line.

```python
print(
    "Sum is",
    int(input("Enter first integer: "))
    + int(input("Enter second integer: "))
)
```

### Sample Output

```text
Enter first integer: 100
Enter second integer: 200

Sum is 300
```

---

# Understanding Function Nesting

Consider

```python
print(int(input()))
```

Execution happens from **inside to outside**.

```
input()

↓

Returns String

↓

int()

↓

Converts to Integer

↓

print()

↓

Displays Result
```

Python always evaluates the innermost function first.

This inside-out evaluation order is explained in the lecture while discussing the one-line solution. :contentReference[oaicite:3]{index=3}

---

# Taking Floating-Point Input

Many real-world applications require decimal numbers.

Examples include

- Height
- Weight
- Temperature
- Radius
- Percentage

For such cases,

we use

```python
float()
```

---

# Example 4 — Area and Circumference of a Circle

```python
radius = float(input("Enter radius: "))

area = 3.14 * (radius ** 2)
circumference = 2 * 3.14 * radius

print("Area is", area)
print("Circumference is", circumference)
```

### Sample Output

```text
Enter radius: 10

Area is 314.0
Circumference is 62.800000000000004
```

---

# Why So Many Decimal Places?

Many beginners expect

```text
62.8
```

Instead,

Python prints

```text
62.800000000000004
```

This happens because computers store floating-point numbers in **binary format**.

Some decimal values cannot be represented exactly in binary,

which leads to tiny precision errors.

This is normal behavior in floating-point arithmetic.

---

# The `round()` Function

Python provides the built-in `round()` function to control the number of decimal places.

Syntax

```python
round(number, digits)
```

Where

- **number** → value to round
- **digits** → number of decimal places

---

# Example 5 — Using `round()`

```python
radius = float(input("Enter radius: "))

area = 3.14 * (radius ** 2)
circumference = 2 * 3.14 * radius

print("Area is", round(area, 2))
print("Circumference is", round(circumference, 2))
```

### Sample Output

```text
Enter radius: 10

Area is 314.00
Circumference is 62.80
```

Instead of displaying long floating-point values,

`round()` produces cleaner and more readable output.

The lecture demonstrates `round()` immediately after the circle example to solve the floating-point precision issue. :contentReference[oaicite:4]{index=4}

---

# Advantages of `round()`

- Produces cleaner output.
- Useful in financial calculations.
- Improves readability.
- Prevents unnecessary decimal digits.
- Commonly used in scientific calculations.

---

# Key Points

- `input()` always returns a string.
- Mathematical operations require type conversion.
- `int()` converts strings into integers.
- `float()` converts strings into decimal numbers.
- Function calls execute from the **inside outward**.
- `round()` controls decimal precision.
- Floating-point numbers may contain tiny precision errors because of binary representation.

---

```
==============================================================================================================================================================
# Working with Python Modules

As programs become larger, writing every function ourselves becomes difficult and time-consuming.

Fortunately, Python provides thousands of **built-in modules** that contain ready-made functions, constants, and utilities.

Instead of reinventing common mathematical formulas or algorithms, we can simply import a module and use its features.

Examples of built-in modules include:

- `math`
- `datetime`
- `random`
- `os`
- `platform`
- `statistics`

One of the most commonly used modules is the **`math` module**.

The lecture introduces the `math` module to demonstrate how Python organizes reusable functionality into modules. :contentReference[oaicite:0]{index=0}

---

# What is a Module?

A **module** is simply a Python file containing:

- Functions
- Variables
- Constants
- Classes

Instead of writing everything from scratch,

we can import the required module and directly use its members.

Think of a module as a **toolbox**.

```
Math Module

├── pi
├── e
├── tau
├── factorial()
├── floor()
├── ceil()
├── pow()
└── many more...
```

---

# Why Use Modules?

Modules provide many advantages.

- Reduce coding effort.
- Improve code reusability.
- Save development time.
- Avoid rewriting common algorithms.
- Improve readability.
- Use well-tested built-in functions.

---

# The `math` Module

Python provides a built-in module called **`math`** for mathematical operations.

It contains:

- Mathematical constants
- Mathematical functions

Before using it, we must import it.

---

# Common Mathematical Constants

| Constant | Description |
|----------|-------------|
| `math.pi` | Value of π (3.141592653...) |
| `math.e` | Euler's Number |
| `math.tau` | 2 × π |

Example

```python
import math

print(math.pi)
print(math.e)
print(math.tau)
```

Possible Output

```text
3.141592653589793
2.718281828459045
6.283185307179586
```

---

# Common Mathematical Functions

| Function | Description |
|----------|-------------|
| `floor(x)` | Greatest integer less than or equal to x |
| `ceil(x)` | Smallest integer greater than or equal to x |
| `pow(x, y)` | Raises x to the power y |
| `factorial(n)` | Returns factorial of n |

These are some of the most frequently used functions demonstrated in the lecture. :contentReference[oaicite:1]{index=1}

---

# `floor()` Function

`floor()` returns the **largest integer less than or equal to the given number**.

Syntax

```python
math.floor(number)
```

Example

```python
import math

print(math.floor(2.7))
```

Output

```text
2
```

Another Example

```python
import math

print(math.floor(8.99))
```

Output

```text
8
```

---

# `ceil()` Function

`ceil()` returns the **smallest integer greater than or equal to the given number**.

Syntax

```python
math.ceil(number)
```

Example

```python
import math

print(math.ceil(2.7))
```

Output

```text
3
```

Another Example

```python
import math

print(math.ceil(8.01))
```

Output

```text
9
```

---

# `pow()` Function

`pow()` calculates powers.

Syntax

```python
math.pow(base, exponent)
```

Example

```python
import math

print(math.pow(2, 5))
```

Output

```text
32.0
```

Notice that `math.pow()` returns a **float**, even when the result is a whole number.

---

# `factorial()` Function

The factorial of a positive integer `n` is

```
n × (n−1) × (n−2) × ... × 1
```

Example

```python
import math

print(math.factorial(5))
```

Output

```text
120
```

---

# Four Ways to Import Modules

Python provides four different ways to import modules.

Each approach has its own advantages.

---

# Method 1 — Standard Import

Syntax

```python
import module_name
```

Example

```python
import math

radius = float(input("Enter radius: "))

area = math.pi * math.pow(radius, 2)
circumference = math.tau * radius

print("Area is", round(area, 2))
print("Circumference is", round(circumference, 2))
```

### Explanation

Every function and constant must be prefixed with

```python
math.
```

Examples

```python
math.pi
math.pow()
math.floor()
math.ceil()
```

This is the most common and recommended method.

---

# Method 2 — Module Aliasing (`as`)

Sometimes module names are long.

Python allows us to assign a shorter name.

Syntax

```python
import module_name as alias
```

Example

```python
import math as m

radius = float(input("Enter radius: "))

area = m.pi * m.pow(radius, 2)
circumference = m.tau * radius

print("Area is", round(area, 2))
print("Circumference is", round(circumference, 2))
```

Now,

instead of writing

```python
math.pi
```

we simply write

```python
m.pi
```

This reduces typing while keeping the code readable.

---

# Another Example of Aliasing

```python
import platform as p

print(p.system())
```

Possible Output

```text
Windows
```

or

```text
Linux
```

or

```text
Darwin
```

depending on your operating system.

The lecture uses this example to show that once a module is aliased, you must use the alias instead of the original module name. :contentReference[oaicite:2]{index=2}

---

# Method 3 — Import Specific Members

Instead of importing the entire module,

we can import only the required functions or constants.

Syntax

```python
from module_name import member1, member2
```

Example

```python
from math import pi, pow, tau

radius = float(input("Enter radius: "))

area = pi * pow(radius, 2)
circumference = tau * radius

print("Area is", round(area, 2))
print("Circumference is", round(circumference, 2))
```

Notice that

we no longer write

```python
math.pi
```

Instead,

we directly use

```python
pi
```

This makes the code shorter.

**Important:** When importing functions, write only the function names.

Correct

```python
from math import pow
```

Incorrect

```python
from math import pow()
```

---

# Method 4 — Import Everything

Python also allows importing every member of a module.

Syntax

```python
from module_name import *
```

Example

```python
from math import *

print("Floor:", floor(2.7))
print("Ceil :", ceil(2.7))
print("PI   :", pi)
```

Output

```text
Floor: 2
Ceil : 3
PI   : 3.141592653589793
```

Although convenient,

this method is **generally discouraged** because it imports everything into the current namespace, making name conflicts more likely.

The lecture introduces this as the fourth import style while noting its convenience. :contentReference[oaicite:3]{index=3}

---

# Comparison of Import Methods

| Method | Example | Need Module Prefix? |
|---------|---------|---------------------|
| Standard Import | `import math` | ✅ Yes |
| Alias Import | `import math as m` | ✅ Yes (`m.`) |
| Specific Import | `from math import pi` | ❌ No |
| Wildcard Import | `from math import *` | ❌ No |

---

# Key Points

- A module is a reusable Python file containing functions, constants, and classes.
- The `math` module provides ready-made mathematical tools.
- `floor()` returns the nearest smaller integer.
- `ceil()` returns the nearest greater integer.
- `pow()` calculates powers.
- `factorial()` calculates factorials.
- Python supports four different import methods.
- Aliasing with `as` makes long module names shorter.
- Import only the required members whenever possible for cleaner code.

---
=============================================================================================================================================================
# Discovering Module Contents

Python contains hundreds of built-in modules, and many of them have dozens (or even hundreds) of functions, constants, and classes.

Remembering every function inside every module is practically impossible.

To solve this problem, Python provides two very useful built-in functions:

- `dir()`
- `help()`

These functions help programmers explore modules without opening external documentation.

---

# The `dir()` Function

The `dir()` function returns a **list** containing the names of all the members available inside a module or object.

These members may include:

- Functions
- Constants
- Variables
- Classes
- Special methods

Syntax

```python
dir(module_name)
```

---

# Example 1

```python
import math

members = dir(math)

print(members)
```

### Sample Output (Shortened)

```python
[
'__doc__',
'__name__',
'ceil',
'comb',
'copysign',
'e',
'exp',
'factorial',
'floor',
'gcd',
'isfinite',
'isinf',
'log',
'pi',
'pow',
'sqrt',
'tau',
...
]
```

Instead of remembering every function,

Python shows everything available inside the module.

This is exactly how `dir()` is demonstrated in the lecture. :contentReference[oaicite:0]{index=0}

---

# Counting Total Members

Since `dir()` returns a list,

we can use the `len()` function.

Example

```python
import math

members = dir(math)

print("Total Members:", len(members))
```

Possible Output

```text
Total Members: 67
```

The exact number may differ depending on the Python version.

---

# Why is `dir()` Useful?

Suppose you forget whether the math module contains

```python
sqrt()
```

or

```python
square()
```

Instead of searching online,

simply write

```python
import math

print(dir(math))
```

and Python will display every available member.

---

# The `help()` Function

The `help()` function displays the official documentation for modules, functions, classes, or objects.

Syntax

```python
help(module_name)
```

---

# Example

```python
import math

help(math)
```

Output (Shortened)

```text
Help on built-in module math:

NAME
    math

DESCRIPTION
    Mathematical functions.

FUNCTIONS
    ceil(...)
    floor(...)
    factorial(...)
    gcd(...)
    sqrt(...)
    pow(...)

DATA
    pi
    e
    tau
```

Instead of only listing names,

`help()` explains

- what a function does,
- what parameters it accepts,
- what it returns,
- and how it should be used.

The lecture introduces `help()` immediately after `dir()` as a way to view detailed documentation. :contentReference[oaicite:1]{index=1}

---

# Difference Between `dir()` and `help()`

| `dir()` | `help()` |
|----------|-----------|
| Lists available members | Explains each member |
| Returns a Python list | Displays documentation |
| Quick overview | Detailed explanation |
| Used for discovery | Used for learning usage |

---

# Practical Example

Suppose you want to learn about

```python
math.factorial()
```

You can write

```python
import math

help(math.factorial)
```

Python displays

- purpose,
- syntax,
- parameters,
- return value.

This saves time and reduces dependency on external references.

---

# Real-World Tip

Professional Python developers frequently use

```python
dir()
```

and

```python
help()
```

while learning new libraries such as

- NumPy
- Pandas
- Matplotlib
- TensorFlow

These two functions are among the easiest ways to explore unfamiliar modules.

---

# The `datetime` Module

Many programs need the current

- date,
- month,
- year,
- time,
- day,
- or timestamp.

Python provides the built-in **`datetime`** module for this purpose.

Instead of hardcoding dates,

we can fetch the current system date dynamically.

---

# Importing `datetime`

Example

```python
from datetime import datetime
```

Here,

the first

```python
datetime
```

is the **module**,

while the second

```python
datetime
```

is a **class** inside that module.

```
datetime Module

↓

datetime Class

↓

now() Method
```

This hierarchy is explained in the lecture before using `datetime.now()`. :contentReference[oaicite:2]{index=2}

---

# Getting Current Date and Time

Example

```python
from datetime import datetime

obj = datetime.now()

print(obj)
```

Possible Output

```text
2026-07-06 08:15:34.582341
```

The returned object contains

- Year
- Month
- Day
- Hour
- Minute
- Second
- Microsecond

---

# Extracting Individual Components

Once the datetime object is created,

we can access its properties.

Example

```python
from datetime import datetime

obj = datetime.now()

print("Year :", obj.year)
print("Month:", obj.month)
print("Day  :", obj.day)
```

Possible Output

```text
Year : 2026
Month: 7
Day  : 6
```

---

# Practical Program — Year When You Turn 100

This is one of the practical programs discussed in the lecture.

Instead of hardcoding the current year,

we fetch it dynamically.

```python
from datetime import datetime

current_date = datetime.now()

current_year = current_date.year

age = int(input("Enter your age: "))

years_left = 100 - age

target_year = current_year + years_left

print("You will turn 100 in the year", target_year)
```

### Sample Output

```text
Enter your age: 21

You will turn 100 in the year 2105
```

---

# How the Program Works

Suppose

Current Year

```text
2026
```

User Age

```text
21
```

Years Remaining

```text
100 - 21

↓

79
```

Final Calculation

```text
2026 + 79

↓

2105
```

Formula

```text
Year at Age 100

=

Current Year + (100 − Current Age)
```

Using `datetime.now().year` makes the program future-proof because it automatically uses the system's current year instead of a hardcoded value. This is the main objective of the lecture's final example. :contentReference[oaicite:3]{index=3}

---

# Key Points

- `dir()` lists all members of a module.
- `help()` displays detailed documentation.
- `dir()` returns a list.
- `help()` explains syntax and usage.
- The `datetime` module is used for date and time operations.
- `datetime.now()` returns the current date and time.
- `.year`, `.month`, and `.day` extract individual components.
- Dynamic dates are better than hardcoded dates in real-world programs.

---
=============================================================================================================================================================
# Taking Different Types of User Input

In real-world applications, we rarely work with just one type of data.

A program may need to accept

- Roll Number (Integer)
- Name (String)
- Percentage (Float)
- Gender (String)
- Salary (Float)
- Age (Integer)

Python allows us to take different types of input by combining the `input()` function with appropriate type conversion functions.

---

# Example – Taking Multiple Data Types

```python
roll = int(input("Enter Roll Number: "))
name = input("Enter Name: ")
percentage = float(input("Enter Percentage: "))

print("Roll Number :", roll)
print("Name        :", name)
print("Percentage  :", percentage)
```

### Sample Output

```text
Enter Roll Number: 101
Enter Name: Sachin Kapoor
Enter Percentage: 92.45

Roll Number : 101
Name        : Sachin Kapoor
Percentage  : 92.45
```

### Explanation

- `roll` is converted to an integer.
- `name` remains a string.
- `percentage` is converted to a floating-point number.

This example demonstrates how different data types can be collected within the same program. :contentReference[oaicite:0]{index=0}

---

# Accepting Multiple Inputs in One Line

Sometimes we want the user to enter multiple values in a single line.

Example

```text
10 20 30
```

Instead of asking for each value separately.

Python provides the `split()` method for this purpose.

---

# The `split()` Method

`split()` divides a string into multiple parts and returns them as a list.

Syntax

```python
string.split()
```

By default,

`split()` separates values using spaces.

---

# Example

```python
numbers = input("Enter three numbers: ").split()

print(numbers)
```

### Sample Output

```text
Enter three numbers: 10 20 30

['10', '20', '30']
```

Notice that every value is still stored as a **string**.

---

# Taking Three Integers in One Line

```python
a, b, c = input("Enter three integers: ").split()

print(a)
print(b)
print(c)
```

### Sample Output

```text
Enter three integers: 10 20 30

10
20
30
```

Although the values look like numbers,

their data type is still

```python
str
```

---

# Converting Multiple Inputs into Integers

We can convert them individually.

```python
a, b, c = input("Enter three integers: ").split()

a = int(a)
b = int(b)
c = int(c)

print(a + b + c)
```

### Sample Output

```text
Enter three integers: 10 20 30

60
```

---

# Using `map()` (Advanced)

Python programmers often use `map()` to perform conversion in a cleaner way.

```python
a, b, c = map(int, input("Enter three integers: ").split())

print(a + b + c)
```

Output

```text
60
```

> **Note:** If your lecture/PDF hasn't introduced `map()` yet, you can skip using it for now and stick to individual `int()` conversions.

---

# Custom Separator in `split()`

By default,

`split()` separates using spaces.

However,

you can specify a custom separator.

---

# Example – Comma Separated Input

```python
data = input("Enter values separated by commas: ").split(",")

print(data)
```

### Sample Output

```text
Enter values separated by commas:
10,20,30

['10', '20', '30']
```

---

# Example – Hyphen Separated Input

```python
data = input("Enter values: ").split("-")

print(data)
```

### Sample Output

```text
Enter values:
A-B-C-D

['A', 'B', 'C', 'D']
```

---

# Common Mistakes

## ❌ Forgetting Type Conversion

```python
a = input()
b = input()

print(a + b)
```

Input

```text
10
20
```

Output

```text
1020
```

Correct

```python
print(int(a) + int(b))
```

---

## ❌ Using Wrong Conversion

```python
age = int(input())

name = int(input())
```

If the user enters

```text
Sachin
```

Python raises

```text
ValueError
```

because

```python
int("Sachin")
```

is invalid.

---

## ❌ Forgetting Module Prefix

```python
import math

print(pi)
```

Output

```text
NameError
```

Correct

```python
print(math.pi)
```

or

```python
from math import pi
print(pi)
```

---

## ❌ Using Alias Incorrectly

```python
import math as m

print(math.pi)
```

Output

```text
NameError
```

Correct

```python
print(m.pi)
```

---

## ❌ Forgetting `()` with `input`

Wrong

```python
name = input
```

Correct

```python
name = input()
```

---

# Best Practices

✔ Always convert numeric input immediately.

```python
age = int(input("Enter Age: "))
```

instead of

```python
age = input("Enter Age: ")
age = int(age)
```

---

✔ Use meaningful prompts.

Good

```python
input("Enter Salary: ")
```

Bad

```python
input()
```

---

✔ Prefer built-in module constants.

Instead of

```python
3.14
```

use

```python
math.pi
```

---

✔ Round floating-point values before displaying them.

```python
print(round(area, 2))
```

---

✔ Import only the required members whenever possible.

```python
from math import pi
```

instead of

```python
from math import *
```

---

# Interview Questions

### 1. What is the return type of `input()`?

`input()` always returns a **string (`str`)**.

---

### 2. Why is type conversion necessary?

Because `input()` returns strings, mathematical operations require conversion to numeric types.

---

### 3. Difference between `int()` and `float()`?

| `int()` | `float()` |
|----------|-----------|
| Converts to integer | Converts to decimal number |

---

### 4. What is the purpose of `round()`?

It rounds a number to the specified number of decimal places.

Example

```python
round(3.14159, 2)
```

Output

```text
3.14
```

---

### 5. Name the four ways to import a module.

- `import math`
- `import math as m`
- `from math import pi`
- `from math import *`

---

### 6. What is the difference between `dir()` and `help()`?

- `dir()` lists members.
- `help()` explains them.

---

### 7. What does `datetime.now()` return?

The current system date and time.

---

### 8. What is `math.tau`?

`math.tau` represents

```text
2 × π
```

---

# Quick Revision

- `input()` makes programs interactive.
- It always returns a string.
- Use `int()` or `float()` for numeric calculations.
- `round()` controls decimal precision.
- The `math` module provides mathematical functions and constants.
- Python supports four import methods.
- `dir()` lists module members.
- `help()` shows documentation.
- `datetime.now()` returns the current date and time.
- `split()` accepts multiple inputs from one line.
- Custom separators can be used with `split(",")`, `split("-")`, etc.

---

# Summary

In this lecture, we learned how to make Python programs interactive using the `input()` function. We explored how `input()` always returns a string and why type conversion with functions like `int()` and `float()` is essential for mathematical operations. We also practiced calculating the area and circumference of a circle and formatting output with the `round()` function.

Next, we explored Python modules, particularly the `math` module, and learned four different ways to import modules. We also used `dir()` and `help()` to inspect module contents and documentation. Finally, we worked with the `datetime` module to retrieve the current date and time and built a practical program to calculate the year in which a user will turn 100. We concluded by learning how to accept multiple inputs efficiently using the `split()` method.

---
