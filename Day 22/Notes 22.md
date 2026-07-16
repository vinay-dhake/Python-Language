# 🐍 Complete Python Programming Series – Lecture 21

# Globals, Locals & Argument Passing

> **Lecture 21 Topics**
>
> - Global Variables
> - Local Variables
> - Variable Scope
> - Variable Lifetime
> - Execution Flow
> - NameError
> - Variable Lookup
> - Interview Notes

---

# 📚 Introduction

In the previous lectures, we learned how to create functions and pass arguments to them. However, one important question still remains:

> **How does Python know which variable to use inside a function?**

For example,

```python
x = 10

def show():
    print(x)
```

Where does Python find the variable `x`?

Similarly,

```python
def show():
    x = 20
```

Is this `x` the same as the previous one?

To answer these questions, Python introduces the concept of **Variable Scope**.

---

# What is Variable Scope?

Variable Scope defines **where a variable can be accessed inside a program**.

In simple words,

> Scope tells Python **which parts of the program are allowed to use a variable**.

Not every variable can be accessed everywhere.

Some variables are available throughout the entire program, while others exist only inside a specific function.

---

# Why Do We Need Scope?

Imagine writing a Python project with thousands of variables.

If every variable were accessible everywhere:

- Variables would accidentally overwrite each other.
- Debugging would become difficult.
- Programs would become confusing.
- Functions would no longer remain independent.

Scope solves this problem by restricting where variables can be used.

---

# Types of Variables Covered in this Lecture

This lecture mainly discusses two types of variables.

| Variable Type | Declared | Accessible |
|---------------|----------|------------|
| Global Variable | Outside a function | Entire program |
| Local Variable | Inside a function | Only inside that function |

---

# Global Variables

A variable declared **outside every function** is called a **Global Variable**.

## Syntax

```python
name = "Sachin"
age = 25
country = "India"
```

All the above variables are global variables.

---

## Characteristics of Global Variables

- Declared outside every function.
- Created in global memory.
- Accessible throughout the program.
- Can be read inside functions.
- Exist until the program terminates.

---

# Example 1 – Accessing a Global Variable

```python
s = "I love Python"

def f():
    print(s)

f()
```

### Output

```text
I love Python
```

---

## Explanation

Initially,

```text
Global Memory

↓

s

↓

"I love Python"
```

The function `f()` contains only one statement.

```python
print(s)
```

Python first searches for a **local variable** named `s`.

Since no local variable exists, Python searches the **global scope**.

The global variable is found successfully.

Therefore,

```text
I love Python
```

is printed.

---

# Variable Lookup Order (Simplified)

Whenever Python encounters

```python
print(variable)
```

it searches in the following order:

```text
Inside Function

↓

Local Variable?

↓

Yes → Use Local Variable

↓

No

↓

Search Global Variable

↓

Found?

↓

Yes → Use Global Variable

↓

No

↓

NameError
```

---

# Example 2 – Global Variable Declared After Function Definition

```python
def f():
    print(s)

s = "I love Python"

f()
```

### Output

```text
I love Python
```

---

## Why Does It Work?

Many beginners think the global variable must always appear before the function definition.

This is incorrect.

Python only **stores** the function definition.

The function body is **not executed** until the function is called.

Execution Flow:

```text
Function Definition

↓

Stored in Memory

↓

Global Variable Created

↓

Function Call

↓

print(s)

↓

Global Variable Found

↓

Output
```

Since the variable exists before `f()` executes, everything works correctly.

---

# Example 3 – Global Variable Declared After Function Call

```python
def f():
    print(s)

f()

s = "I love Python"
```

### Output

```text
NameError:
name 's' is not defined
```

---

## Why Does This Fail?

Python executes programs **line by line**.

Execution Flow:

```text
Function Definition

↓

Function Call

↓

print(s)

↓

Search Local Variable

↓

Not Found

↓

Search Global Variable

↓

Not Found

↓

NameError

↓

Program Stops
```

The statement

```python
s = "I love Python"
```

is never reached because the program has already terminated.

---

# NameError

Whenever Python cannot find a variable in the current scope, it raises

```text
NameError
```

Common reasons:

- Variable not created.
- Variable created after use.
- Misspelled variable name.
- Local variable accessed outside its function.

---

# Local Variables

A variable declared inside a function is called a **Local Variable**.

Example

```python
def show():

    x = 10
    y = 20

    print(x)
```

Both `x` and `y` are local variables.

---

## Characteristics of Local Variables

- Declared inside functions.
- Created only when the function starts executing.
- Accessible only inside that function.
- Automatically destroyed after function execution.

---

# Example 4 – Local Variable Lifetime

```python
def f():

    s = "I love Python"

f()

print(s)
```

### Output

```text
NameError
```

---

## Explanation

When `f()` starts,

Python creates

```text
s
```

inside the function.

After the function finishes,

Python removes the local variable from memory.

Later,

```python
print(s)
```

tries to access it.

Since the variable no longer exists,

Python raises

```text
NameError
```

---

# Memory Diagram

During Function Execution

```text
Function Memory

↓

s

↓

"I love Python"
```

After Function Ends

```text
Function Memory Destroyed

↓

s Removed
```

Outside the function

```python
print(s)
```

results in

```text
NameError
```

---

# Lifetime of Local Variables

A local variable exists only while the function is executing.

```text
Function Call

↓

Local Variable Created

↓

Function Executes

↓

Function Returns

↓

Local Variable Destroyed
```

---

# Global vs Local Variables

| Global Variable | Local Variable |
|-----------------|----------------|
| Declared outside functions | Declared inside functions |
| Accessible throughout the program | Accessible only inside the function |
| Exists until program termination | Destroyed after function execution |
| Shared across functions | Private to one function |

---

# Interview Questions

### Q1. What is a Global Variable?

A variable declared outside every function.

---

### Q2. What is a Local Variable?

A variable declared inside a function.

---

### Q3. Can a function read a global variable?

**Yes.**

---

### Q4. When are local variables destroyed?

Immediately after the function returns.

---

### Q5. Which error occurs when Python cannot find a variable?

```text
NameError
```

---

# Key Takeaways

- Scope determines where a variable can be accessed.
- Global variables are accessible throughout the program.
- Local variables exist only inside functions.
- Python executes programs sequentially.
- Function definitions are stored but not executed immediately.
- Local variables are destroyed after function execution.
- Accessing an unavailable variable raises `NameError`.

---

> **End of Part 1**
===============================================================================================================================================================
# Variable Shadowing and the `global` Keyword

In the previous section, we learned that a function can directly **read a global variable**. However, an important question arises:

> **What happens if a function creates another variable having the same name as a global variable?**

Will Python modify the global variable?

Or

Will Python create a completely new variable?

The answer introduces one of the most important concepts in Python programming:

> **Variable Shadowing**

Understanding this concept is essential before learning the `global` keyword.

---

# What is Variable Shadowing?

Variable Shadowing occurs when a **local variable has the same name as a global variable**.

In this situation,

the local variable **hides** the global variable inside that function.

In other words,

inside the function,

Python completely ignores the global variable and starts using the local variable instead.

---

# Example 1 – Variable Shadowing

```python
s = "I love Python"

def f():

    s = "I love C"

    print(s)

f()

print(s)
```

### Output

```text
I love C
I love Python
```

---

# Dry Run

Initially,

```text
Global Memory

↓

s

↓

"I love Python"
```

Now,

the function starts executing.

Python encounters

```python
s = "I love C"
```

Immediately,

Python creates a **new local variable**.

Memory now becomes

```text
Global Memory

↓

s

↓

"I love Python"


Function Memory

↓

s

↓

"I love C"
```

Notice that **two different variables** now exist.

Although both have the same name,

they belong to different scopes.

---

# What Happens Inside the Function?

Inside

```python
print(s)
```

Python follows its lookup rule.

It first searches for

```
Local Variable
```

A local variable named

```text
s
```

exists.

Therefore,

Python prints

```text
I love C
```

without even checking the global variable.

---

# What Happens After the Function Ends?

Once the function finishes,

its local memory is destroyed.

The local variable disappears.

Only the global variable remains.

Therefore,

```python
print(s)
```

outside the function prints

```text
I love Python
```

---

# Memory Diagram

Before Function Call

```text
Global Memory

↓

s

↓

"I love Python"
```

During Function Execution

```text
Global Memory

↓

s

↓

"I love Python"


Local Memory

↓

s

↓

"I love C"
```

After Function Ends

```text
Global Memory

↓

s

↓

"I love Python"
```

Local memory no longer exists.

---

# Important Observation

Many beginners think

```python
s = "I love C"
```

changes the global variable.

It does **not**.

Instead,

Python creates an entirely new local variable.

---

# Why Does Python Do This?

Python follows a very simple rule.

Whenever it sees an assignment inside a function,

```python
variable = value
```

it assumes

that variable belongs to the local scope,

unless instructed otherwise.

This prevents accidental modification of global variables.

---

# Interview Point

> **Assignment inside a function creates a local variable by default.**

Remember this statement.

It explains many interview questions and programming errors.

---

# Another Example

```python
x = 50

def show():

    x = 100

    print("Inside:", x)

show()

print("Outside:", x)
```

### Output

```text
Inside: 100
Outside: 50
```

Again,

the global variable remains unchanged because a new local variable was created.

---

# Modifying Global Variables

Suppose we actually want to modify the global variable.

Can we do that?

**Yes.**

Python provides a special keyword called

```python
global
```

---

# The `global` Keyword

The `global` keyword tells Python

> "Do not create a new local variable. Use the existing global variable instead."

---

# Syntax

```python
global variable_name
```

Example

```python
global count
```

---

# Example 2 – Using `global`

```python
s = "I love Python"

def f():

    global s

    s = "I love C"

    print(s)

f()

print(s)
```

### Output

```text
I love C
I love C
```

---

# Dry Run

Initially,

```text
Global Memory

↓

s

↓

"I love Python"
```

Now the function starts.

Python encounters

```python
global s
```

This tells Python

> **Do not create a local variable named `s`.**

Instead,

use the existing global variable.

Now the assignment

```python
s = "I love C"
```

changes the global variable itself.

Memory becomes

```text
Global Memory

↓

s

↓

"I love C"
```

The function prints

```text
I love C
```

After the function ends,

the global variable still contains

```text
I love C
```

Therefore,

the second `print(s)` also prints

```text
I love C
```

---

# Memory Comparison

## Without `global`

```text
Global Memory

↓

s = "Python"


Function

↓

Creates Local s

↓

"C"

↓

Global Variable Unchanged
```

---

## With `global`

```text
Global Memory

↓

s = "Python"

↓

global s

↓

Modify Same Variable

↓

"C"
```

Only one variable exists.

---

# Example 3

```python
count = 10

def increment():

    global count

    count = count + 1

increment()

print(count)
```

### Output

```text
11
```

Since the global variable was modified,

the new value becomes visible everywhere.

---

# Rules for Using `global`

## Rule 1

Use `global` only when you want to modify a global variable.

---

## Rule 2

Reading a global variable **does not require** the `global` keyword.

Example

```python
x = 100

def show():
    print(x)
```

This works perfectly.

---

## Rule 3

Declare `global` before using the variable.

Correct

```python
def show():

    global x

    x = 50
```

---

## Rule 4

Avoid excessive use of global variables.

Professional Python programs prefer returning values instead of modifying globals because excessive global variables make programs difficult to debug and maintain.

---

# Global Variable vs Local Variable

Without `global`

```python
x = 10

def show():

    x = 20

show()

print(x)
```

Output

```text
10
```

---

With `global`

```python
x = 10

def show():

    global x

    x = 20

show()

print(x)
```

Output

```text
20
```

---

# Common Mistakes

## Mistake 1

Thinking

```python
x = 20
```

inside a function modifies the global variable.

It doesn't.

It creates a local variable.

---

## Mistake 2

Using `global` unnecessarily.

```python
x = 10

def show():

    global x

    print(x)
```

This works,

but `global` isn't required because we are only reading the variable.

---

## Interview Questions

### Q1. What is Variable Shadowing?

Variable Shadowing occurs when a local variable has the same name as a global variable, causing the local variable to hide the global one inside the function.

---

### Q2. Does assignment inside a function modify a global variable?

**No.**

It creates a new local variable unless `global` is used.

---

### Q3. When should we use the `global` keyword?

Whenever we want to modify a global variable from inside a function.

---

### Q4. Can a global variable be read without using `global`?

**Yes.**

The `global` keyword is needed only for modification.

---

# Key Takeaways

- Assignment inside a function creates a local variable by default.
- Local variables hide global variables having the same name.
- This behavior is called **Variable Shadowing**.
- The `global` keyword tells Python to use the global variable instead of creating a local one.
- Reading a global variable never requires the `global` keyword.
- Modifying a global variable requires the `global` keyword.

---

> **End of Part 2**
==============================================================================================================================================================
# UnboundLocalError – Python's Unique Behaviour

In the previous section, we learned that whenever Python encounters an assignment statement (`=`) inside a function, it **creates a local variable** by default.

This rule leads to one of the most common errors beginners face while learning Python:

> **UnboundLocalError**

This error often confuses beginners because the variable **already exists globally**, yet Python still reports an error.

To understand why this happens, we first need to understand **how Python compiles and executes functions**.

---

# How Python Executes a Function

Many beginners think Python executes a function **line by line**, deciding whether a variable is local or global as it moves through the code.

**This is NOT how Python works.**

Before executing a function, Python first scans the **entire function body**.

During this scan, Python identifies all the variables that are assigned values.

If Python finds even one assignment to a variable inside a function,

```python
x = something
```

then Python marks that variable as **local for the entire function**.

This decision is made **before** the first line of the function executes.

---

# What is UnboundLocalError?

> **Definition**

`UnboundLocalError` occurs when Python treats a variable as **local**, but the program tries to use that local variable **before assigning any value to it**.

Unlike `NameError`, the variable **does exist** in the local scope.

The problem is that it has **not yet been initialized**.

---

# Difference Between NameError and UnboundLocalError

| NameError | UnboundLocalError |
|-----------|-------------------|
| Variable cannot be found. | Variable exists locally but has no value yet. |
| Python cannot locate the variable. | Python located the local variable but it is uninitialized. |
| Usually occurs when a variable never existed. | Usually occurs because of assignment inside a function. |

---

# Example 1 – Pre-Assignment Access Trap

This was one of the most important examples demonstrated in class.

```python
x = 10

def f():

    x = x + 1

    print(x)

f()
```

### Output

```text
UnboundLocalError:
cannot access local variable 'x'
where it is not associated with a value
```

---

# What Most Beginners Think

Many students expect Python to execute the code like this:

```text
Global x

↓

10

↓

10 + 1

↓

11

↓

Print 11
```

Therefore, they expect the output to be

```text
11
```

However,

this is **not** what Python does.

---

# What Python Actually Does

Before execution,

Python scans the entire function.

It finds

```python
x = x + 1
```

Since there is an assignment,

Python immediately decides

```text
x

↓

Local Variable
```

Now execution begins.

Python evaluates

```python
x + 1
```

But remember,

Python is searching for the **local variable**.

The local variable has not yet received any value.

Therefore,

Python raises

```text
UnboundLocalError
```

---

# Dry Run

Initially

```text
Global Memory

↓

x

↓

10
```

Python scans the function.

```
Assignment Found

↓

x becomes Local
```

Execution begins.

```
x = x + 1

↓

Need Local x

↓

Local x has no value

↓

UnboundLocalError
```

Notice something very important.

Python never even looks at the global variable.

---

# Memory Diagram

Before Function Call

```text
Global Memory

↓

x

↓

10
```

Function Starts

```text
Compiler

↓

Detects Assignment

↓

Creates Local x
```

Execution

```text
Local x

↓

No Value

↓

Trying to Evaluate

↓

x + 1

↓

Error
```

---

# Why Doesn't Python Use the Global Variable?

Because Python already decided

```text
x

↓

Local Variable
```

during compilation.

Once that decision is made,

the global variable becomes invisible inside that function.

---

# Correct Solution

If our intention is to modify the global variable,

we must explicitly declare it.

```python
x = 10

def f():

    global x

    x = x + 1

    print(x)

f()

print(x)
```

### Output

```text
11

11
```

---

# Dry Run

Initially

```text
Global Memory

↓

x = 10
```

Function starts.

Python sees

```python
global x
```

Therefore,

Python **does not create a local variable**.

Instead,

the existing global variable is used.

Now

```python
x = x + 1
```

becomes

```text
10 + 1

↓

11

↓

Stored Back into Global Memory
```

Both print statements therefore produce

```text
11
```

---

# Example 2 – Post-Usage Assignment Trap

Now consider another interesting example discussed in class.

```python
s = "I love Python"

def f():

    print(s)

    s = "I love C"

f()
```

### Output

```text
UnboundLocalError
```

---

# Why Does This Error Occur?

Many beginners say

> "Sir, `print(s)` comes before the assignment."

So they expect

```text
I love Python
```

Unfortunately,

Python has already scanned the function.

During scanning,

it noticed

```python
s = "I love C"
```

Therefore,

Python marked

```text
s

↓

Local Variable
```

for the **entire function**.

Now execution begins.

The first statement is

```python
print(s)
```

Python searches for the local variable.

It exists,

but has not yet been assigned any value.

Result

```text
UnboundLocalError
```

---

# Execution Flow

```text
Function Definition

↓

Python Scans Function

↓

Assignment Found

↓

s marked as Local

↓

Execution Starts

↓

print(s)

↓

Search Local Variable

↓

No Value Assigned

↓

UnboundLocalError
```

---

# Memory Representation

Initially

```text
Global Memory

↓

s

↓

"I love Python"
```

Compiler Scan

```text
Assignment Found

↓

Create Local s
```

Execution

```text
print(s)

↓

Need Local Variable

↓

No Value

↓

Error
```

Again,

the global variable is completely ignored.

---

# Correct Version

```python
s = "I love Python"

def f():

    global s

    print(s)

    s = "I love C"

f()

print(s)
```

### Output

```text
I love Python

I love C
```

Now both statements operate on the same global variable.

---

# Common Mistakes

## Mistake 1

```python
count = 5

def increment():

    count = count + 1
```

Produces

```text
UnboundLocalError
```

because `count` is treated as a local variable.

---

## Mistake 2

Thinking Python decides scope while executing each line.

It doesn't.

Python decides the scope **before execution**.

---

## Mistake 3

Using a variable before assigning it inside a function.

Always remember:

> Assignment anywhere inside a function makes that variable local (unless `global` is used).

---

# Interview Questions

### Q1. What is UnboundLocalError?

It occurs when Python treats a variable as local but the variable is accessed before receiving any value.

---

### Q2. Why doesn't Python use the global variable?

Because assignment inside the function makes the variable local during compilation.

---

### Q3. Difference between NameError and UnboundLocalError?

| NameError | UnboundLocalError |
|-----------|-------------------|
| Variable not found | Local variable exists but has no value |
| Scope lookup fails | Local variable accessed before assignment |

---

### Q4. How can we fix UnboundLocalError?

By using the `global` keyword when we intend to modify a global variable.

---

# Key Takeaways

- Python scans the entire function before execution.
- Assignment inside a function automatically creates a local variable.
- Accessing that local variable before assignment raises `UnboundLocalError`.
- The global variable is ignored once Python classifies the variable as local.
- The `global` keyword instructs Python to use the global variable instead of creating a local one.

---

> **End of Part 3**
=============================================================================================================================================================
# Scope of Conditional Statements and Loops

After understanding **Global Variables**, **Local Variables**, the **`global` keyword**, and **UnboundLocalError**, the instructor discussed another concept that confuses beginners coming from C, C++, Java, or JavaScript.

Many students assume that every pair of curly braces (`{}`) or every block of code creates a new scope.

However,

> **Python does not have block-level scope.**

This is one of the most frequently asked Python interview questions.

---

# What is Block-Level Scope?

In many programming languages,

blocks like

- `if`
- `else`
- `for`
- `while`

create a completely new scope.

Variables declared inside those blocks disappear after the block finishes.

For example, in C++:

```cpp
if(true)
{
    int x = 10;
}

cout << x;
```

Output

```text
Compilation Error
```

because

```
x

↓

Destroyed
```

after leaving the block.

---

# Does Python Have Block-Level Scope?

**No.**

Python **does not** create a new scope for:

- `if`
- `elif`
- `else`
- `for`
- `while`

Variables declared inside these blocks remain accessible after the block finishes (provided the block executed).

Only these create a new scope:

- Functions
- Classes
- Modules

---

# Example 1 – Variable Inside an `if` Block

```python
if True:

    x = 100

print(x)
```

### Output

```text
100
```

---

# Dry Run

Execution starts.

Python checks

```python
if True
```

The condition is true.

Therefore,

```python
x = 100
```

is executed.

Unlike C++,

Python does **not** destroy `x` after leaving the `if` block.

Hence,

```python
print(x)
```

prints

```text
100
```

---

# Memory Representation

Initially

```text
Global Memory

↓

(No x)
```

Inside `if`

```text
Global Memory

↓

x

↓

100
```

After leaving the `if` block

```text
Global Memory

↓

x

↓

100
```

Notice that the variable is still available.

---

# Example 2 – Example from Class

```python
a = 0

if True:

    b = 1

print(a)

print(b)
```

### Output

```text
0
1
```

---

# Explanation

Initially

```text
Global Memory

↓

a

↓

0
```

The condition

```python
if True
```

is satisfied.

Python executes

```python
b = 1
```

Since `if` does not create a new scope,

`b` also becomes a global variable.

Memory becomes

```text
Global Memory

↓

a

↓

0

↓

b

↓

1
```

Both variables are available after the `if` block.

---

# Scope Inside Functions

Now consider the classroom example.

```python
a = 0

if True:

    b = 1

def f(c):

    d = 3

    print(c)

    print(d)

f(7)

print(a)

print(b)

print(c)
```

---

## Output

```text
7
3
0
1
NameError
```

---

# Dry Run

Initially,

Python creates

```text
Global Variables

↓

a = 0
```

The `if` block executes.

```python
b = 1
```

Since there is no block scope,

both variables remain global.

Now,

```python
f(7)
```

is called.

The parameter

```python
c
```

is created.

Inside the function,

another local variable

```python
d
```

is created.

Memory becomes

```text
Global Memory

↓

a = 0

↓

b = 1


Function Memory

↓

c = 7

↓

d = 3
```

Inside the function,

```python
print(c)
```

prints

```text
7
```

Then,

```python
print(d)
```

prints

```text
3
```

The function finishes.

Immediately,

the local variables

```text
c

↓

Destroyed

d

↓

Destroyed
```

Execution continues.

```python
print(a)
```

prints

```text
0
```

```python
print(b)
```

prints

```text
1
```

Finally,

```python
print(c)
```

Python searches

Local Scope

↓

Destroyed

Global Scope

↓

No Variable Named `c`

Result

```text
NameError
```

---

# Memory Diagram

Before Function Call

```text
Global Memory

↓

a = 0

↓

b = 1
```

During Function Execution

```text
Global Memory

↓

a = 0

↓

b = 1


Local Memory

↓

c = 7

↓

d = 3
```

After Function Ends

```text
Local Memory Destroyed


Global Memory

↓

a = 0

↓

b = 1
```

---

# Function Parameters are Local Variables

One important point emphasized in class was:

> **Function parameters are also local variables.**

Example

```python
def square(number):

    print(number)

square(5)

print(number)
```

### Output

```text
5

NameError
```

---

# Why?

The parameter

```python
number
```

exists only while

```python
square()
```

is executing.

After the function returns,

it is destroyed.

---

# Scope Summary

| Structure | Creates New Scope? |
|------------|--------------------|
| Function | ✅ Yes |
| Class | ✅ Yes |
| Module | ✅ Yes |
| if | ❌ No |
| elif | ❌ No |
| else | ❌ No |
| for | ❌ No |
| while | ❌ No |

---

# Common Mistakes

## Mistake 1

Thinking

```python
if True:

    x = 10
```

creates a local variable.

It doesn't.

---

## Mistake 2

Trying to access function parameters outside the function.

```python
def show(a):

    print(a)

show(10)

print(a)
```

Output

```text
NameError
```

---

## Mistake 3

Thinking loop variables disappear.

```python
for i in range(5):

    pass

print(i)
```

Output

```text
4
```

The loop variable still exists because Python has no block-level scope.

---

# Interview Questions

### Q1. Does Python have block-level scope?

**No.**

---

### Q2. Which structures create a new scope?

- Functions
- Classes
- Modules

---

### Q3. Are function parameters local variables?

**Yes.**

---

### Q4. Can variables declared inside an `if` block be accessed outside?

**Yes.**

---

### Q5. Why does `print(c)` produce `NameError` in the classroom example?

Because `c` is a function parameter (local variable), and it is destroyed after the function finishes.

---

# Key Takeaways

- Python does **not** have block-level scope.
- Variables declared inside `if`, `for`, and `while` remain accessible outside those blocks.
- Functions create a completely separate local scope.
- Function parameters are local variables.
- Local variables are destroyed immediately after the function returns.
- Attempting to access a local variable after function execution results in `NameError`.

---

# Next Topic

Now that we understand **Variable Scope**, the next topic is **Argument Passing**.

We will answer questions such as:

- Does Python use **Pass by Value**?
- Does Python use **Pass by Reference**?
- What is **Pass by Object Reference**?
- Why do integers behave differently from lists?

These concepts form the foundation of how Python functions work internally.

---

> **End of Part 4**
=============================================================================================================================================================
# Argument Passing in Python

After understanding **Variable Scope**, the instructor introduced another fundamental concept:

> **How are arguments actually passed to functions in Python?**

Many beginners think Python follows either:

- **Pass by Value**
- **Pass by Reference**

However, Python follows **neither** of these exactly.

Instead, Python uses a unique mechanism called:

> **Pass by Object Reference**

Understanding this concept is essential because it explains why integers behave differently from lists when passed to functions.

---

# Ways of Passing Arguments

Before understanding Python's mechanism, let's briefly look at the two traditional mechanisms used by other programming languages.

```
Call by Value
        ↓
Call by Reference
        ↓
Pass by Object Reference (Python)
```

---

# Call by Value

In **Call by Value**, a **copy** of the original variable is passed to the function.

The function works only on this copy.

Therefore,

changes made inside the function do **not** affect the original variable.

---

## Concept Diagram

```
Original Variable

↓

10

↓

Copy Created

↓

Function Parameter

↓

10
```

The function modifies only the copy.

The original variable remains unchanged.

---

# Example (Conceptual)

Suppose a language follows Call by Value.

```
Original

↓

10

↓

Function receives

↓

10

↓

Function changes

↓

20

↓

Original

↓

Still 10
```

This is how C works.

---

# Call by Reference

In **Call by Reference**, instead of creating a copy,

the memory address of the variable is passed to the function.

Both variables point to exactly the same memory location.

---

## Concept Diagram

```
Main Variable

↓

Address

↓

Function Parameter

↓

Same Address
```

If the function changes the variable,

the original variable also changes.

This mechanism is commonly used in C++ (using reference variables).

---

# Does Python Use Call by Value?

**No.**

---

# Does Python Use Call by Reference?

**No.**

---

# Python's Mechanism

Python uses

> **Pass by Object Reference**

This mechanism is also known as

- Call by Sharing
- Pass Object Reference
- Object Reference Passing

All these terms refer to the same concept.

---

# Why is it Called "Pass by Object Reference"?

Everything in Python is an **object**.

Variables do **not** directly store values.

Instead,

variables store **references to objects**.

For example,

```python
a = 10
```

Most beginners imagine memory like this:

```
a

↓

10
```

But Python actually stores

```
Variable

↓

Reference

↓

Integer Object

↓

10
```

The variable doesn't contain the integer itself.

It only stores a reference to the integer object.

---

# Object Reference Example

```python
a = 10
b = a
```

Memory Representation

```
Integer Object

↓

10

↑
│
a
│
b
```

Both variables refer to the same integer object.

Python does **not** create another integer object.

---

# What Happens After Reassignment?

Now consider

```python
b = 20
```

Integers are immutable.

Therefore,

Python creates a brand new integer object.

Memory becomes

```
Integer Object

↓

10

↑
a


Integer Object

↓

20

↑
b
```

The original object

```
10
```

never changes.

Only

```
b
```

starts referring to another object.

---

# Mutable vs Immutable Objects

Python's argument passing depends entirely on the type of object being passed.

Objects are classified into two categories.

---

## Immutable Objects

These objects **cannot be modified** after creation.

Examples

- `int`
- `float`
- `bool`
- `str`
- `tuple`

---

## Mutable Objects

These objects **can be modified** after creation.

Examples

- `list`
- `dict`
- `set`
- `bytearray`

---

# Why is This Important?

The behavior of a function depends on whether the object is mutable or immutable.

For **immutable objects**,

reassignment creates a **new object**.

For **mutable objects**,

methods such as

```python
append()
```

modify the existing object.

This is why integers and lists behave differently.

---

# Argument Passing with Immutable Objects

The instructor first demonstrated argument passing using integers.

Consider the following classroom example.

```python
def show(a):

    print("Inside before change:", a)

    a = 20

    print("Inside after change:", a)

a = 10

print("Before calling:", a)

show(a)

print("After calling:", a)
```

### Output

```text
Before calling: 10

Inside before change: 10

Inside after change: 20

After calling: 10
```

---

# Dry Run

Initially,

```
Global Memory

↓

a

↓

10
```

When

```python
show(a)
```

is executed,

Python passes the **reference** to the integer object.

Memory now looks like

```
Global Variable

↓

10

↑
│
a
│
Function Parameter
```

Both references point to the same integer object.

---

# What Happens During Assignment?

Python executes

```python
a = 20
```

Integers are immutable.

Therefore,

Python **cannot modify** the integer object

```
10
```

Instead,

Python creates a **new integer object**.

Memory becomes

```
Global Variable

↓

10


Function Parameter

↓

20
```

The function parameter now points to a different object.

The original variable still points to

```
10
```

Therefore,

after the function returns,

the original variable remains unchanged.

---

# Memory Diagram

Before Function Call

```
Global a

↓

10
```

During Function Call

```
Global a

↓

10

↑

Function a
```

After Assignment

```
Global a

↓

10


Function a

↓

20
```

The two variables now point to different objects.

---

# Key Observation

The statement

```python
a = 20
```

does **not** modify the integer

```
10
```

Instead,

it creates a brand new integer object.

---

# Interview Point

Whenever an immutable object is reassigned,

Python creates a new object rather than modifying the existing one.

---

# Common Mistake

Many beginners believe

```python
a = 20
```

changes the value

```
10
```

This is incorrect.

The integer object

```
10
```

never changes.

Python simply changes the reference.

---

# Key Takeaways

- Python passes **object references**, not copies.
- Variables store references to objects.
- Integers are immutable.
- Reassigning an immutable object creates a new object.
- The original object remains unchanged.

---

# Next Topic

In the next section, we will study **Mutable Objects**.

We'll understand why methods like

- `append()`
- `extend()`
- `insert()`

modify the original list,

while assignment

```python
=
```

creates a completely new list.

---

> **End of Part 5**
=============================================================================================================================================================
# Argument Passing with Mutable Objects

In the previous section, we studied how **immutable objects** (such as integers, strings, tuples, etc.) behave when passed to a function.

We observed that assigning a new value to an immutable object inside a function **does not affect** the original object.

Now let's study what happens when **mutable objects** are passed to a function.

This is one of the most important topics in Python because it explains why **lists, dictionaries, and sets behave differently** from integers.

---

# What are Mutable Objects?

A **mutable object** is an object whose contents can be modified after it has been created.

Common mutable data types in Python include:

- List (`list`)
- Dictionary (`dict`)
- Set (`set`)
- Bytearray (`bytearray`)

Unlike immutable objects, mutable objects allow in-place modification.

---

# Why are Mutable Objects Different?

When a mutable object is passed to a function,

both the original variable and the function parameter initially refer to the **same object**.

If the object is modified,

the modification is visible everywhere because **both variables still point to the same object**.

---

# Example 1 – Modifying a List using `append()`

```python
def show(a):

    a.append(40)

    print("Inside show:", a)

a = [10, 20, 30]

print("Before calling:", a)

show(a)

print("After calling:", a)
```

### Output

```text
Before calling: [10, 20, 30]

Inside show: [10, 20, 30, 40]

After calling: [10, 20, 30, 40]
```

---

# Dry Run

Initially,

```
Global Memory

↓

a

↓

[10,20,30]
```

Now the function is called.

Python passes the reference to the list.

Memory becomes

```
Global Variable

↓

List Object

↓

[10,20,30]

↑

Function Parameter
```

Notice that both variables point to the **same list object**.

---

# What Happens During `append()`?

Python executes

```python
a.append(40)
```

The `append()` method modifies the existing list object.

It **does not create a new list**.

Memory changes to

```
List Object

↓

[10,20,30,40]
```

Since both references point to the same object,

both variables observe the updated list.

---

# Memory Diagram

Before Function Call

```
Global a

↓

List

↓

[10,20,30]
```

During Function Call

```
Global a

↓

List

↓

[10,20,30]

↑

Function a
```

After `append()`

```
Global a

↓

List

↓

[10,20,30,40]

↑

Function a
```

Both variables still refer to the same list object.

---

# Important Observation

The statement

```python
a.append(40)
```

does **not** create another list.

Instead,

it modifies the existing list object.

This is why the original list also changes.

---

# Example 2 – Reassigning the List

Now consider another example discussed in class.

```python
def show(a):

    a = [40, 50, 60]

    print("Inside show:", a)

a = [10, 20, 30]

print("Before calling:", a)

show(a)

print("After calling:", a)
```

### Output

```text
Before calling: [10, 20, 30]

Inside show: [40, 50, 60]

After calling: [10, 20, 30]
```

---

# Why Didn't the Original List Change?

Many students expect the output to be

```text
[40, 50, 60]
```

But that is **incorrect**.

The reason is that

```python
a = [40, 50, 60]
```

is **assignment**, not modification.

Assignment creates a **completely new list object**.

---

# Dry Run

Initially,

```
Global Variable

↓

List A

↓

[10,20,30]
```

Function starts.

Both references point to List A.

```
Global a

↓

List A

↓

[10,20,30]

↑

Function a
```

Now Python executes

```python
a = [40,50,60]
```

Python creates

```
List B

↓

[40,50,60]
```

The function parameter now points to List B.

Memory becomes

```
Global a

↓

List A

↓

[10,20,30]


Function a

↓

List B

↓

[40,50,60]
```

The connection between the two variables is broken.

Therefore,

the original list remains unchanged.

---

# Method Call vs Assignment

This is one of the most important comparisons of the lecture.

## Case 1 – Method Call

```python
a.append(40)
```

Result

```
Same Object

↓

Modified
```

Original list changes.

---

## Case 2 – Assignment

```python
a = [40,50,60]
```

Result

```
New Object

↓

Reference Updated
```

Original list remains unchanged.

---

# Another Example

```python
def add_item(lst):

    lst.append("Python")

subjects = ["Java", "C"]

add_item(subjects)

print(subjects)
```

### Output

```text
['Java', 'C', 'Python']
```

Reason:

`append()` modifies the original list.

---

# Another Example

```python
def change_list(lst):

    lst = ["HTML", "CSS"]

subjects = ["Java", "Python"]

change_list(subjects)

print(subjects)
```

### Output

```text
['Java', 'Python']
```

Reason:

Assignment creates a new list.

---

# Immutable vs Mutable Behaviour

| Immutable Objects | Mutable Objects |
|-------------------|-----------------|
| Cannot be modified | Can be modified |
| Assignment creates a new object | Methods modify the existing object |
| Original object remains unchanged | Original object changes |
| Examples: int, float, str, tuple | Examples: list, dict, set |

---

# Common Mistakes

## Mistake 1

Thinking

```python
append()
```

creates a new list.

It doesn't.

It modifies the same list.

---

## Mistake 2

Thinking

```python
a = [1,2,3]
```

modifies the original list.

It doesn't.

It creates a new list object.

---

## Mistake 3

Confusing assignment with modification.

Remember:

- Assignment (`=`) → New Object
- Methods (`append()`, `extend()`, `remove()`) → Modify Existing Object

---

# Interview Questions

### Q1. Why does `append()` modify the original list?

Because `append()` changes the existing list object instead of creating a new one.

---

### Q2. Why doesn't assignment modify the original list?

Because assignment creates a new object and changes only the local reference.

---

### Q3. Which data types are mutable?

- List
- Dictionary
- Set
- Bytearray

---

### Q4. Which data types are immutable?

- Integer
- Float
- Boolean
- String
- Tuple

---

# Key Takeaways

- Python passes references to objects.
- Mutable objects can be modified in place.
- List methods modify the original object.
- Assignment creates a new object.
- Whether changes are visible outside the function depends on whether the original object is modified or a new object is created.

---

# Next Topic

In the final section of this lecture, we'll understand **why Python behaves this way internally**, compare mutable and immutable objects side by side, discuss **Pass by Object Reference** in depth, and conclude the lecture with interview questions and a complete summary.

---

> **End of Part 6**
============================================================================================================================================================================================================================================================================================
# Deep Dive into Pass by Object Reference

In the previous sections, we studied how **immutable** and **mutable** objects behave when passed to functions.

Many beginners memorize the outputs of the programs but fail to understand **why** Python behaves differently in each case.

To truly master this topic, we need to understand two important concepts:

1. **Objects**
2. **References**

Once these concepts become clear, you will be able to predict the output of almost every function-related interview question.

---

# Everything in Python is an Object

One of Python's most important design philosophies is:

> **Everything in Python is an Object.**

Examples:

- Integer → Object
- Float → Object
- Boolean → Object
- String → Object
- List → Object
- Tuple → Object
- Dictionary → Object
- Function → Object

Variables themselves **do not store data**.

Instead,

they store a **reference** to an object.

---

# Variables Store References

Consider

```python
a = 10
```

Many beginners imagine memory like this:

```
a
↓

10
```

This is **incorrect**.

Python actually stores

```
Variable

↓

Reference

↓

Object

↓

10
```

The variable only stores the address (reference) of the object.

---

# Example

```python
a = 10

b = a
```

Memory

```
        Integer Object
             10
            ↑  ↑
            │  │
            a  b
```

Notice carefully.

Python does **not** create another integer object.

Both variables refer to the same object.

---

# Reassignment Creates a New Object

Now execute

```python
b = 20
```

Since integers are immutable,

Python creates another integer object.

Memory becomes

```
      Integer Object
           10
           ↑
           │
           a


      Integer Object
           20
           ↑
           │
           b
```

The original integer

```
10
```

was never modified.

Only the reference stored inside `b` changed.

---

# Why Lists Behave Differently

Now consider

```python
a = [10,20,30]

b = a
```

Memory

```
          List Object

      [10,20,30]

         ↑      ↑

         │      │

         a      b
```

Again,

both variables refer to the same list object.

---

# Using append()

Now execute

```python
b.append(40)
```

The method modifies the existing object.

Memory becomes

```
          List Object

   [10,20,30,40]

         ↑      ↑

         │      │

         a      b
```

Since both variables refer to the same object,

both variables observe the modification.

---

# Assignment is Different

Now execute

```python
b = [40,50,60]
```

Python creates a brand new list.

Memory becomes

```
        List A

   [10,20,30]

      ↑

      │

      a



        List B

   [40,50,60]

      ↑

      │

      b
```

The original list remains unchanged.

---

# Golden Rule

Whenever you see a function,

ask yourself only one question.

> **Did Python modify the existing object or create a new object?**

If the object is modified,

all references observe the change.

If a new object is created,

only the local reference changes.

---

# Method Call vs Assignment

This comparison is extremely important for interviews.

## Case 1

```python
a.append(40)
```

```
Existing Object

↓

Modified
```

Original list changes.

---

## Case 2

```python
a = [40,50]
```

```
New Object

↓

Reference Changed
```

Original list remains unchanged.

---

# Predict the Output

## Example 1

```python
def show(a):

    a.append(100)

numbers = [10,20]

show(numbers)

print(numbers)
```

### Output

```text
[10, 20, 100]
```

Reason:

`append()` modifies the original list object.

---

## Example 2

```python
def show(a):

    a = [100]

numbers = [10,20]

show(numbers)

print(numbers)
```

### Output

```text
[10, 20]
```

Reason:

Assignment creates a new list object.

---

## Example 3

```python
def show(a):

    a = a + [40]

numbers = [10,20]

show(numbers)

print(numbers)
```

### Output

```text
[10, 20]
```

---

## Why?

Many students think

```python
a + [40]
```

modifies the list.

It **does not**.

The `+` operator creates a **new list**.

Equivalent to

```
Old List

↓

Create Copy

↓

Append 40

↓

Return New List
```

Therefore,

the original list remains unchanged.

---

# Summary Table

| Operation | Modifies Original Object? |
|-----------|---------------------------|
| `append()` | ✅ Yes |
| `extend()` | ✅ Yes |
| `insert()` | ✅ Yes |
| `remove()` | ✅ Yes |
| `pop()` | ✅ Yes |
| `sort()` | ✅ Yes |
| `reverse()` | ✅ Yes |
| Assignment (`=`) | ❌ No |
| `+` Operator | ❌ No |
| List Slicing (`[:]`) | ❌ Creates a New List |

---

# Common Mistakes

## Mistake 1

Thinking

```python
a.append(40)
```

creates another list.

It doesn't.

---

## Mistake 2

Thinking

```python
a = [1,2,3]
```

modifies the original list.

It doesn't.

---

## Mistake 3

Confusing **modification** with **reassignment**.

Remember:

- Methods → Modify existing object.
- Assignment → Create new object.

---

# Frequently Asked Interview Questions

### Q1. Does Python use Pass by Value?

**No.**

---

### Q2. Does Python use Pass by Reference?

**No.**

---

### Q3. What argument passing mechanism does Python use?

**Pass by Object Reference** (also known as **Call by Sharing**).

---

### Q4. Why do integers remain unchanged after a function call?

Because integers are **immutable**. Reassignment creates a new object.

---

### Q5. Why does `append()` modify the original list?

Because it modifies the existing list object instead of creating a new one.

---

### Q6. Why doesn't assignment modify the original list?

Because assignment changes the reference to a newly created object.

---

# Complete Lecture Summary

In this lecture, we explored Python's **scope rules** and **argument passing mechanism** in depth.

We learned the difference between **Global Variables** and **Local Variables**, understood how Python resolves variables using scope, and saw that function definitions are stored first and executed only when called.

We studied **Variable Shadowing**, where a local variable hides a global variable with the same name, and learned how the `global` keyword allows us to modify global variables from inside functions.

Next, we explored **UnboundLocalError**, one of Python's most confusing beginner errors, and understood that Python scans the entire function before execution. If an assignment to a variable is found anywhere inside the function, Python treats that variable as local throughout the function.

We also learned that Python **does not have block-level scope**. Statements such as `if`, `for`, and `while` do not create a new scope. Only **functions**, **classes**, and **modules** create their own scope.

Finally, we studied **Pass by Object Reference**, Python's unique argument-passing mechanism. We compared immutable and mutable objects, observed why integers remain unchanged after reassignment inside functions, and why methods like `append()` modify the original list while assignment creates a completely new object.

---

# Quick Revision

- Variable Scope defines where a variable can be accessed.
- Variables declared outside functions are Global Variables.
- Variables declared inside functions are Local Variables.
- Function parameters are Local Variables.
- Local variables are destroyed after the function returns.
- Assignment inside a function creates a local variable by default.
- The `global` keyword allows modification of global variables.
- Python scans the function before execution.
- `UnboundLocalError` occurs when a local variable is accessed before assignment.
- Python does not have block-level scope.
- Functions, classes, and modules create scopes.
- Python uses **Pass by Object Reference**.
- Immutable objects create new objects during reassignment.
- Mutable objects can be modified in place.
- Methods like `append()` modify the original object.
- Assignment (`=`) changes the reference to a new object.

---

# Key Takeaway

> **In Python, variables do not store values—they store references to objects.**
>
> Understanding this single concept makes topics like **scope, mutable vs immutable objects, and argument passing** much easier to understand.

---

**🎉 End of Lecture 21 – Globals, Locals & Argument Passing**
