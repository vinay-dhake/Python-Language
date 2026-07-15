# Python Programming – Lecture 21
# Globals, Locals & Argument Passing

> **Topics Covered**
>
> - Global Variables
> - Local Variables
> - Variable Shadowing
> - `global` Keyword
> - UnboundLocalError
> - Scope inside Loops and Conditions
> - Argument Passing
> - Pass by Object Reference
> - Mutable vs Immutable Objects

---

# Introduction

In the previous lecture, we learned about **Global Variables** and **Local Variables**. We saw that variables declared outside a function belong to the entire program, whereas variables created inside a function exist only during the execution of that function.

In this lecture, we build upon those concepts and study how Python actually searches for variables, how global variables can be modified from inside functions, why `UnboundLocalError` occurs, and how Python passes arguments to functions.

Unlike many programming languages, Python follows its own unique execution model. Understanding these concepts is essential because they frequently appear in interviews and are used extensively in real-world Python programs.

---

# Learning Objectives

After completing this lecture, you should be able to:

- Differentiate between Global and Local variables.
- Explain the lifetime of variables.
- Understand Variable Shadowing.
- Use the `global` keyword correctly.
- Explain why `UnboundLocalError` occurs.
- Understand Python's scope rules.
- Explain Python's Pass by Object Reference mechanism.
- Differentiate between Mutable and Immutable objects.

---

# Variable Scope

Before learning Global and Local variables in detail, we must understand the meaning of **Scope**.

## What is Scope?

Scope refers to the **region of a program where a variable is accessible**.

In simple words,

> Scope determines **where a variable can be used**.

If a variable is outside its scope, Python cannot access it and raises an error.

---

# Types of Scope

Python mainly follows the **LEGB Rule**:

```
L → Local

↓

E → Enclosing

↓

G → Global

↓

B → Built-in
```

In this lecture, we focus on the first two scopes that beginners encounter:

- Global Scope
- Local Scope

The remaining scopes are studied in later lectures.

---

# Global Variables

A variable declared **outside every function** is known as a **Global Variable**.

Global variables belong to the entire program and remain available until the program finishes execution.

---

## Characteristics of Global Variables

- Declared outside functions.
- Accessible throughout the program.
- Can be read inside functions.
- Exist until program termination.

---

# Example 1 – Reading a Global Variable

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

The variable

```python
s
```

is created outside the function.

Therefore,

it belongs to the global scope.

When

```python
print(s)
```

executes,

Python searches for `s`.

Since it is not present inside the function,

Python finds the global variable.

---

## Memory Representation

```
Global Memory

↓

s

↓

"I love Python"

↓

Function f()

↓

Reads Global Variable

↓

Print
```

Notice that

the function does **not** create another variable.

It simply reads the global variable.

---

# Important Observation

A function **can read** a global variable without any special keyword.

No additional syntax is required.

---

# Example 2 – Global Variable Declared After Function Definition

Many beginners believe that a global variable must always appear before the function definition.

That is **not true**.

Consider the following example.

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

## Why Does This Work?

Python does **not** execute a function when it is defined.

It only stores the function definition.

Execution begins from the first executable statement.

Flow of execution:

```
Function Definition

↓

Stored

↓

Global Variable Created

↓

Function Call

↓

print(s)

↓

Output
```

By the time `f()` is called,

the variable `s` already exists in memory.

Therefore,

Python successfully prints it.

---

# Important Concept

There is a huge difference between

- Function Definition
- Function Execution

Writing

```python
def f():
```

does **not** execute the function.

Execution begins only after

```python
f()
```

is encountered.

---

# Example 3 – Global Variable Declared After Function Call

Now consider the following example.

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

## Dry Run

Python executes statements from top to bottom.

Execution Flow

```
Function Definition

↓

Stored

↓

Function Call

↓

print(s)

↓

Search for s

↓

Not Found

↓

NameError

↓

Program Stops

↓

Remaining Statements Never Execute
```

Notice that

Python never reaches

```python
s = "I love Python"
```

because execution already stopped due to the error.

---

# Why Does This Error Occur?

Although the variable exists later in the program,

it does **not** exist **at the moment the function executes**.

Python always executes sequentially.

It never looks ahead.

---

# Important Interview Point

Python executes statements **line by line**.

Variables must exist **before** they are used.

---

# Local Variables

A variable declared **inside a function** is called a **Local Variable**.

Local variables belong only to that function.

They are created when the function starts executing and destroyed immediately after it finishes.

---

## Characteristics

- Declared inside functions.
- Accessible only inside the function.
- Destroyed automatically after execution.
- Cannot be accessed outside the function.

---

# Example 4 – Local Variable

```python
def f():

    s = "I love Python"

    print(s)

f()
```

### Output

```text
I love Python
```

---

## Explanation

The variable

```python
s
```

exists only during the execution of `f()`.

Execution Flow

```
Function Starts

↓

Create Local Variable

↓

Print

↓

Function Ends

↓

Local Variable Destroyed
```

---

# Example 5 – Accessing a Local Variable Outside the Function

```python
def f():

    s = "I love Python"

f()

print(s)
```

### Output

```text
NameError:
name 's' is not defined
```

---

## Why?

The variable was destroyed immediately after the function completed.

Therefore,

outside the function,

it no longer exists.

---

## Memory Diagram

```
Function Starts

↓

Local Memory Created

↓

s = "I love Python"

↓

Print

↓

Function Ends

↓

Local Memory Removed

↓

Outside Function

↓

s ?

↓

Not Found

↓

NameError
```

---

# Lifetime of a Local Variable

A Local Variable has a very short lifetime.

```
Function Call

↓

Variable Created

↓

Function Executes

↓

Function Ends

↓

Variable Destroyed
```

This is one of the most important properties of local variables.

---

# Difference Between Global and Local Variables

| Global Variable | Local Variable |
|-----------------|----------------|
| Declared outside functions | Declared inside functions |
| Accessible throughout the program | Accessible only inside the function |
| Exists until the program terminates | Exists only during function execution |
| Shared by multiple functions | Private to one function |

---

# Common Mistakes

## Mistake 1

```python
def show():

    x = 10

show()

print(x)
```

Output

```text
NameError
```

Reason:

`x` is a local variable.

---

## Mistake 2

Assuming function parameters remain after execution.

```python
def add(a,b):

    print(a+b)

add(10,20)

print(a)
```

Output

```text
NameError
```

Function parameters are also local variables.

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

### Q4. Can a local variable be accessed outside its function?

**No.**

---

### Q5. When is a local variable destroyed?

Immediately after the function finishes execution.

---

> **End of Part 1**
================================================================================================================================================================
# Variable Shadowing and the `global` Keyword

In the previous section, we learned that a function can **read** a global variable without any difficulty.

A very common question now arises:

> **What happens if we create another variable inside the function having the same name as the global variable?**

Will Python modify the global variable?

Or will it create another variable?

The answer leads us to one of the most important concepts in Python called **Variable Shadowing**.

---

# Variable Shadowing

## What is Variable Shadowing?

When a variable declared inside a function has the **same name** as a global variable, the local variable **hides** the global variable inside that function.

This phenomenon is known as **Variable Shadowing**.

> The local variable **shadows** the global variable.

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

```
Global Memory

↓

s

↓

"I love Python"
```

Now the function starts.

```
Function f()

↓

Create Local Variable

↓

s

↓

"I love C"
```

Inside the function,

Python first searches for

```
s
```

It immediately finds

```
Local s
```

Therefore,

```
"I love C"
```

is printed.

After the function ends,

the local variable is destroyed.

Outside the function,

only the global variable remains.

Therefore,

```
"I love Python"
```

is printed.

---

# Memory Diagram

Before Function Call

```
Global Memory

↓

s

↓

"I love Python"
```

During Function Execution

```
Global Memory

↓

s

↓

"I love Python"

            ↑

Local Memory

↓

s

↓

"I love C"
```

Inside the function,

Python always chooses

```
Local Variable

↓

Highest Priority
```

After Function Ends

```
Local Variable Destroyed

↓

Only Global Variable Remains

↓

"I love Python"
```

---

# Important Observation

Notice carefully.

The statement

```python
s = "I love C"
```

**does not modify**

the global variable.

Instead,

Python creates

an entirely **new local variable**.

---

# Why Does This Happen?

Python follows a simple rule.

Whenever it sees

```python
variable = something
```

inside a function,

Python assumes

that variable belongs to the local scope

unless instructed otherwise.

---

# Interview Point

Assignment inside a function

```
=

```

creates a **local variable by default**.

---

# Example 2

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

the global variable remains unchanged.

---

# Can We Modify the Global Variable?

Yes.

Python provides a special keyword called

```python
global
```

---

# The `global` Keyword

The `global` keyword tells Python

> "Do not create a local variable.

Use the existing global variable instead."

---

# Syntax

```python
global variable_name
```

---

# Example 3 – Modifying a Global Variable

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

# Why Did the Output Change?

Without

```python
global s
```

Python creates

```
Local s
```

With

```python
global s
```

Python directly accesses

```
Global s
```

and modifies it.

---

# Dry Run

Initially

```
Global Memory

↓

s

↓

"I love Python"
```

Function Starts

```
global s

↓

Use Existing Global Variable
```

Assignment

```
s = "I love C"
```

changes

```
Global Memory

↓

s

↓

"I love C"
```

After Function Ends

```
Global Variable Still Exists

↓

"I love C"
```

Therefore,

both print statements display

```
I love C
```

---

# Memory Comparison

## Without `global`

```
Global

↓

s = "Python"

↓

Function

↓

Create Local s

↓

"C"

↓

Global Unchanged
```

---

## With `global`

```
Global

↓

s = "Python"

↓

Function

↓

global s

↓

Modify Same Variable

↓

"C"
```

---

# Example 4

```python
count = 10

def increment():

    global count

    count += 1

increment()

print(count)
```

### Output

```text
11
```

The global variable was successfully updated.

---

# Why is `global` Required?

Imagine

```python
count = 10
```

Inside the function

```python
count = count + 1
```

Python becomes confused.

Should

```
count
```

refer to

```
Local Variable

or

Global Variable?
```

The keyword

```python
global
```

removes this confusion.

---

# Rules for Using `global`

### Rule 1

Declare it before using the variable.

Correct

```python
def show():

    global x

    x = 20
```

---

### Rule 2

It is required only when **modifying** a global variable.

Reading a global variable does **not** require `global`.

Example

```python
x = 50

def show():

    print(x)
```

Works perfectly.

---

### Rule 3

Avoid unnecessary use of global variables.

Excessive use of globals makes programs difficult to maintain.

Professional Python code tries to minimize their usage.

---

# Global Variable vs Shadowing

Without `global`

```python
x = 10

def f():

    x = 20

f()

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

def f():

    global x

    x = 20

f()

print(x)
```

Output

```text
20
```

---

# Common Mistakes

## Mistake 1

Expecting this

```python
x = 10

def f():

    x = 20
```

to change the global variable.

It doesn't.

It creates a local variable.

---

## Mistake 2

Using `global` unnecessarily.

```python
x = 10

def f():

    global x

    print(x)
```

This works,

but `global` isn't needed because we are only reading the variable.

---

# Interview Questions

### Q1. What is Variable Shadowing?

Creating a local variable with the same name as a global variable.

---

### Q2. Does assignment inside a function modify the global variable?

No.

It creates a new local variable unless `global` is used.

---

### Q3. When should the `global` keyword be used?

Whenever we want to modify a global variable inside a function.

---

### Q4. Can a global variable be read without `global`?

Yes.

The `global` keyword is required only for modification.

---

# Key Takeaways

- Local variables have higher priority than global variables.
- Assignment inside a function creates a local variable by default.
- Variable Shadowing hides the global variable.
- `global` tells Python to use the existing global variable.
- Reading a global variable does not require `global`.
- Modifying a global variable requires `global`.

---

> **End of Part 2**
==============================================================================================================================================================
# The `UnboundLocalError`

In the previous section, we learned that Python automatically creates a **local variable** whenever it encounters an assignment statement inside a function.

Most beginners believe Python executes statements one by one while deciding whether a variable is local or global.

**This is not true.**

Before executing a function, Python first **analyzes the entire function body**. If it finds an assignment (`=`) to a variable anywhere inside that function, it assumes that variable is **local throughout the entire function**.

This behavior leads to one of Python's most common beginner errors:

> **UnboundLocalError**

---

# What is UnboundLocalError?

`UnboundLocalError` occurs when Python treats a variable as **local**, but the program tries to access that local variable **before it has received any value**.

Unlike `NameError`, the variable **does exist in the function's scope**, but it has not yet been initialized.

---

# Difference Between NameError and UnboundLocalError

| NameError | UnboundLocalError |
|-----------|-------------------|
| Variable does not exist anywhere in the current scope. | Variable belongs to the local scope but has not been assigned a value yet. |
| Python cannot find the variable. | Python finds the variable but it is uninitialized. |

---

# Example 1 – Pre-Assignment Access Trap

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

# Many Students Expect

Most beginners think

```
Global x

↓

10

↓

10 + 1

↓

11
```

So they expect

```text
11
```

But Python behaves differently.

---

# What Python Actually Does

Before executing the function,

Python scans the function body.

It finds

```python
x = x + 1
```

Since there is an assignment,

Python immediately decides

```
x

↓

Local Variable
```

Now execution begins.

```
x = x + 1
```

Python tries to evaluate

```
x + 1
```

But

```
Local x

↓

No Value Yet
```

Therefore,

Python raises

```text
UnboundLocalError
```

---

# Memory Diagram

Global Memory

```
x

↓

10
```

Function Starts

```
Assignment Found

↓

Python Creates Local x
```

Execution

```
x = x + 1

↓

Need Local x

↓

Local x Empty

↓

UnboundLocalError
```

Notice that

Python **never even looks at the global variable**.

---

# Why Doesn't Python Use the Global Variable?

Because

the moment Python detects

```python
x =
```

inside the function,

it permanently classifies

```
x

↓

Local Variable
```

for that entire function.

The global variable becomes invisible.

---

# Fixing the Problem

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

```
Global Memory

↓

x = 10
```

Function starts

```
global x

↓

Use Global Variable
```

Now

```
x = x + 1

↓

10 + 1

↓

11

↓

Store Back

↓

Global Memory Updated
```

Everything works correctly.

---

# Example 2 – Post-Usage Assignment Trap

Consider another interesting example.

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

# Why?

Many students argue:

> "Sir, `print(s)` comes before the assignment."

Therefore,

they expect

```text
I love Python
```

Unfortunately,

Python does not think that way.

---

# Python's Internal Logic

Before executing,

Python scans the entire function.

It notices

```python
s = "I love C"
```

Therefore,

it immediately decides

```
s

↓

Local Variable
```

Now execution begins.

First statement

```python
print(s)
```

Python searches

```
Local s
```

But

```
Local s

↓

Not Assigned Yet
```

Hence

```text
UnboundLocalError
```

---

# Dry Run

Function Definition

↓

Python scans

↓

Assignment found

↓

`s` becomes Local

↓

Execution starts

↓

`print(s)`

↓

Looks for Local `s`

↓

No Value

↓

UnboundLocalError

---

# Memory Representation

Global Memory

```
s

↓

"I love Python"
```

Function

```
Compiler Detects

↓

Assignment

↓

Local s Reserved
```

Execution

```
print(s)

↓

Need Local s

↓

No Value

↓

Error
```

---

# Fix

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

---

# Why Does `global` Solve It?

The statement

```python
global s
```

tells Python

> "Do not create a local variable named `s`. Use the existing global variable."

Now both statements operate on the same variable.

---

# Important Rule

If Python finds an assignment to a variable anywhere inside a function,

that variable becomes **local for the entire function**,

unless declared using `global`.

This is one of the most important interview questions in Python.

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

---

## Mistake 2

Thinking Python executes line by line while deciding scope.

It doesn't.

Python determines variable scope **before execution**.

---

# Interview Questions

### Q1. Why does `UnboundLocalError` occur?

Because Python treats the variable as local due to an assignment statement, but the variable is accessed before receiving any value.

---

### Q2. Why doesn't Python use the global variable?

Because assignment inside a function automatically makes that variable local unless `global` is used.

---

### Q3. Difference between NameError and UnboundLocalError?

**NameError**

- Variable doesn't exist.

**UnboundLocalError**

- Variable exists in the local scope but hasn't been assigned a value yet.

---

# Key Takeaways

- Python determines local variables before executing the function.
- Assignment inside a function makes a variable local.
- Accessing that variable before assignment causes `UnboundLocalError`.
- `global` tells Python to use the global variable instead.
- Python scans the entire function body before execution.

---

> **End of Part 3**
=============================================================================================================================================================
# Scope in Conditional Statements and Loops

After understanding **Global Variables**, **Local Variables**, and **UnboundLocalError**, the instructor discussed another very common misconception among beginners.

Many students coming from **C**, **C++**, **Java**, or **JavaScript** believe that an `if` statement or a loop creates a new scope.

**In Python, this is not true.**

Only a **function**, **class**, and **module** create a new scope.

Statements like:

- `if`
- `for`
- `while`
- `match` (Python 3.10+)

**do not create a separate local scope.**

This is an important interview question.

---

# Does an `if` Statement Create a Scope?

**Answer: No**

Variables created inside an `if` block remain accessible outside that block (provided the block executes).

---

## Example 1

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

## Explanation

Execution Flow

```
Start

↓

if True

↓

x = 100

↓

Exit if Block

↓

print(x)

↓

100
```

Unlike C++ or Java,

Python does **not** destroy the variable after leaving the `if` block.

---

# Example 2 (Class Example)

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

## Dry Run

Initially

```
Global Memory

↓

a = 0
```

Condition

```
True
```

Therefore,

```
b = 1
```

is created.

Since the `if` statement does **not** create a new scope,

both variables now exist in the **Global Scope**.

```
Global Memory

↓

a = 0

↓

b = 1
```

Therefore,

both print statements execute successfully.

---

# Comparison with C/C++

### C++

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

### Python

```python
if True:

    x = 10

print(x)
```

Output

```text
10
```

---

# Interview Question

**Does Python have block-level scope?**

**Answer:**

No.

Python does **not** have block-level scope for

- `if`
- `for`
- `while`

Only functions, classes, and modules create a new scope.

---

# Scope Inside Functions

Now consider the following example.

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

Initially

```
Global Memory

↓

a = 0
```

Execution enters

```
if True
```

```
b = 1
```

Since

`if`

does not create a scope,

```
Global Memory

↓

a = 0

↓

b = 1
```

Now

```
f(7)
```

creates a new function scope.

Inside the function,

```
c = 7

↓

Parameter

↓

Local Variable
```

```
d = 3

↓

Local Variable
```

Inside the function

```
print(c)

↓

7

print(d)

↓

3
```

Function ends.

Immediately

```
c

↓

Destroyed

d

↓

Destroyed
```

Execution continues.

```
print(a)

↓

0
```

```
print(b)

↓

1
```

Finally

```
print(c)
```

Python searches

```
Global Scope

↓

No c
```

Function scope

```
Already Destroyed
```

Result

```text
NameError
```

---

# Memory Diagram

```
Global Memory

↓

a = 0

↓

b = 1

↓

Function Call

↓

Local Memory

↓

c = 7

↓

d = 3

↓

Function Ends

↓

Local Memory Destroyed

↓

Only a and b remain
```

---

# Important Observation

Notice carefully.

```
b
```

survives because

it belongs to the global scope.

```
c

and

d
```

are destroyed because

they belong to the function scope.

---

# Function Parameters are Local Variables

One important point mentioned in class is that

function parameters are **also local variables**.

Example

```python
def square(number):

    print(number)

square(5)

print(number)
```

Output

```text
5

NameError
```

Reason

```
number

↓

Local Variable
```

Parameters disappear when the function finishes.

---

# Summary of Python Scope

| Construct | Creates Scope? |
|------------|----------------|
| Function | ✅ Yes |
| Class | ✅ Yes |
| Module | ✅ Yes |
| if | ❌ No |
| for | ❌ No |
| while | ❌ No |

---

# Common Mistakes

## Mistake 1

Assuming

```python
if True:

    x = 5
```

creates a local variable.

It doesn't.

---

## Mistake 2

Trying to access a function parameter outside the function.

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

Assuming loop variables disappear.

```python
for i in range(3):

    pass

print(i)
```

Output

```text
2
```

The variable `i` still exists because the `for` loop does **not** create a new scope.

---

# Interview Questions

### Q1. Does an `if` statement create a new scope in Python?

**No.**

---

### Q2. Does a `for` loop create a new scope?

**No.**

---

### Q3. Which statements create a new scope?

- Functions
- Classes
- Modules

---

### Q4. Are function parameters local variables?

**Yes.**

---

# Key Takeaways

- Python does not support block-level scope.
- Variables declared inside `if`, `for`, and `while` remain accessible outside those blocks.
- Functions create a completely separate local scope.
- Function parameters behave exactly like local variables.
- Local variables are destroyed immediately after the function finishes.

---

# Introduction to Argument Passing

So far, we have studied how functions receive arguments.

The next question is:

> **What actually happens when an argument is passed to a function?**

Does Python create a copy of the variable?

Does it pass the original variable?

Does it pass the memory address?

Different programming languages use different techniques, such as:

- **Call by Value**
- **Call by Reference**

Python follows a different mechanism known as:

> **Pass by Object Reference**

Before understanding this concept, we must first understand the difference between **Mutable** and **Immutable** objects, because Python's argument passing behavior depends entirely on the type of object being passed.

---

> **End of Part 4**
=============================================================================================================================================================
# Argument Passing in Python

After understanding **Variable Scope**, the lecture shifts to another important concept:

> **How does Python pass arguments to functions?**

This topic often creates confusion because different programming languages use different techniques.

For example,

- C uses **Call by Value**.
- C++ supports **Call by Reference**.
- Java is often described as **Pass by Value of Object References**.

Python follows a different model known as:

> **Pass by Object Reference** (also called *Call by Sharing*).

To understand this properly, we must first know the difference between **Mutable** and **Immutable** objects.

---

# Ways of Passing Arguments

Generally, programmers discuss three argument passing mechanisms.

```
Call by Value

↓

Call by Reference

↓

Pass by Object Reference (Python)
```

Python does **not** strictly follow the first two.

Instead, it follows **Pass by Object Reference**.

---

# Call by Value

In Call by Value,

a **copy** of the variable is passed to the function.

The original variable remains completely unaffected.

Memory Diagram

```
Main Function

↓

a = 10

↓

Copy

↓

Function Parameter

↓

10
```

Since the function works on the copy,

changing the parameter does **not** affect the original variable.

---

# Example (Call by Value Concept)

```text
Main Variable

↓

10

↓

Function Receives Copy

↓

10

↓

Change Copy to 20

↓

Original Still 10
```

This is how C behaves.

---

# Call by Reference

In Call by Reference,

instead of sending a copy,

the memory address of the variable is passed.

Both variables refer to the same memory location.

```
Main Variable

↓

Address

↓

Function Parameter

↓

Same Address
```

Now,

changing the parameter changes the original variable.

This mechanism is commonly seen in C++ using reference variables.

---

# Does Python Follow Call by Value?

**No.**

---

# Does Python Follow Call by Reference?

**No.**

---

# Then What Does Python Use?

Python uses

> **Pass by Object Reference**

Some books also call it

- Call by Sharing
- Pass Object Reference
- Pass Object

All these terms describe the same mechanism.

---

# Why Is It Called "Pass by Object Reference"?

Everything in Python is an **object**.

Variables do **not** directly store values.

Instead,

they store **references to objects**.

Example

```python
a = 10
```

Memory Representation

```
Variable

↓

a

↓

Reference

↓

Object

↓

10
```

When a function is called,

Python passes the **reference** to the object,

not the actual variable.

---

# Important Point

Python never passes

- a copy of the variable,
- nor the actual variable itself.

It passes

```
Reference

↓

Object
```

What happens afterwards depends entirely on

whether the object is

- Mutable
- Immutable

---

# Mutable vs Immutable Objects

Python objects are divided into two categories.

## Immutable Objects

Once created,

their value cannot be changed.

Examples

- Integer (`int`)
- Float (`float`)
- Boolean (`bool`)
- String (`str`)
- Tuple (`tuple`)

---

## Mutable Objects

Their contents can be modified after creation.

Examples

- List (`list`)
- Dictionary (`dict`)
- Set (`set`)

---

# Why Is This Important?

Python's argument passing behaves differently for

```
Immutable Objects

and

Mutable Objects
```

For immutable objects,

changes inside the function usually do **not** affect the original object.

For mutable objects,

methods like `.append()` modify the same object,

so changes become visible outside the function.

---

# Argument Passing with Immutable Objects

Let's begin with integers.

---

# Class Example 1

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

---

## Output

```text
Before calling: 10

Inside before change: 10

Inside after change: 20

After calling: 10
```

---

# Many Beginners Expect

Some students think

```
a = 20

↓

Original Variable Changes
```

Therefore,

they expect

```
After calling: 20
```

This is incorrect.

---

# What Actually Happens?

Initially

```
Main Function

↓

a

↓

Object

↓

10
```

Function Call

Python passes

```
Reference

↓

Object 10
```

Now both variables refer to

```
10
```

```
Main a

↓

10

Function Parameter a

↓

10
```

---

# Assignment Inside the Function

Now Python executes

```python
a = 20
```

This does **not** modify

```
Object 10
```

Integers are immutable.

Therefore,

Python creates

```
New Object

↓

20
```

The function parameter

now points to

```
20
```

while

the original variable still points to

```
10
```

---

# Memory Diagram

Before Function Call

```
Main a

↓

10
```

Function Starts

```
Main a

↓

10

Function a

↓

10
```

Assignment

```
Function a

↓

20

Main a

↓

10
```

The connection is broken.

The original variable remains unchanged.

---

# Important Observation

The object

```
10
```

was never modified.

Instead,

Python simply changed

the **reference** of the local variable.

This is why

the global variable remains unchanged.

---

# Key Rule for Immutable Objects

Assignment creates

```
New Object

↓

New Reference
```

It does **not**

modify the original object.

---

# Interview Question

### Why does changing an integer inside a function not affect the original variable?

Because integers are **immutable**.

The assignment creates a **new integer object**.

Only the local reference changes.

The original reference remains unchanged.

---

# Common Mistakes

## Mistake

Thinking

```python
a = 20
```

changes the integer

```
10
```

Integers cannot be modified.

A brand new integer object is created.

---

# Key Takeaways

- Python passes **object references**.
- Integers are immutable.
- Assignment changes the reference, not the object.
- Original integer remains unchanged.

---

In the next part, we'll study **Mutable Objects (Lists)** and see why methods like `append()` modify the original list, while assigning a completely new list does not.

---

> **End of Part 5**
=================================================================================================================================================================================
# Argument Passing with Mutable Objects

In the previous section, we studied **Immutable Objects** such as integers and saw that assigning a new value inside a function creates a **new object**, leaving the original object unchanged.

Now let us study **Mutable Objects**, where Python behaves differently.

This is one of the most important concepts in Python because it explains why lists sometimes change unexpectedly after a function call.

---

# What are Mutable Objects?

A mutable object is an object whose contents **can be modified after it is created**.

Common mutable data types include:

- List (`list`)
- Dictionary (`dict`)
- Set (`set`)
- Bytearray (`bytearray`)

Unlike integers or strings, mutable objects allow in-place modification.

---

# Why are Mutable Objects Special?

When Python passes a mutable object to a function, both the caller and the function parameter initially refer to the **same object**.

If the object is modified **using one of its methods**, both variables observe the change because they still point to the same object.

---

# Class Example 1 – Modifying a List using `append()`

```python
def show(a):

    a.append(40)

    print("Inside show:", a)


a = [10, 20, 30]

print("Before calling:", a)

show(a)

print("After calling:", a)
```

---

## Output

```text
Before calling: [10, 20, 30]

Inside show: [10, 20, 30, 40]

After calling: [10, 20, 30, 40]
```

---

# Dry Run

Initially

```
Main Function

↓

a

↓

List Object

↓

[10,20,30]
```

Function Call

Python passes the **reference**.

```
Main a

↓

[10,20,30]

Function Parameter a

↓

[10,20,30]
```

Notice that **both references point to the same list object**.

---

# What Happens During `append()`?

Python executes

```python
a.append(40)
```

The method **does not create a new list**.

Instead,

it modifies the existing list object.

```
Before

↓

[10,20,30]

append(40)

↓

After

↓

[10,20,30,40]
```

Since both variables point to the same object,

both see the updated contents.

---

# Memory Diagram

Before Function Call

```
Main a

↓

List Object

↓

[10,20,30]
```

After Function Starts

```
Main a

↓

List Object

↓

[10,20,30]

↑

Function a
```

After `append(40)`

```
Main a

↓

List Object

↓

[10,20,30,40]

↑

Function a
```

Both references still point to the same object.

Therefore,

the original list changes.

---

# Important Observation

The statement

```python
a.append(40)
```

**does not create a new list**.

It modifies the existing list object in memory.

---

# Interview Point

List methods like

- `append()`
- `extend()`
- `insert()`
- `remove()`
- `pop()`
- `sort()`
- `reverse()`

modify the original list.

---

# Example 2 – Using `append()` Multiple Times

```python
def add_numbers(values):

    values.append(100)

    values.append(200)

numbers = [10,20]

add_numbers(numbers)

print(numbers)
```

Output

```text
[10,20,100,200]
```

Again,

the original list changes because

`append()`

modifies the same object.

---

# Reassignment is Different

Now let us look at another classroom example.

```python
def show(a):

    a = [40,50,60]

    print("Inside show:", a)


a = [10,20,30]

print("Before calling:", a)

show(a)

print("After calling:", a)
```

---

## Output

```text
Before calling: [10,20,30]

Inside show: [40,50,60]

After calling: [10,20,30]
```

---

# Many Students Get Confused

Students ask,

> "Sir, the list changed in the previous example. Why didn't it change here?"

The answer lies in the difference between

- **Modification**
- **Reassignment**

---

# Dry Run

Initially

```
Main a

↓

List Object A

↓

[10,20,30]
```

Function Starts

```
Main a

↓

List Object A

↓

[10,20,30]

↑

Function a
```

Now Python executes

```python
a = [40,50,60]
```

This is **not** a modification.

Instead,

Python creates a completely new list object.

```
New List Object

↓

[40,50,60]
```

Now the local variable changes its reference.

```
Function a

↓

List Object B

↓

[40,50,60]
```

The original variable still points to

```
List Object A

↓

[10,20,30]
```

---

# Memory Diagram

Before Assignment

```
Main a

↓

List A

↓

[10,20,30]

↑

Function a
```

After Assignment

```
Main a

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

The connection between the two references has been broken.

---

# Important Rule

Methods like

```python
append()

remove()

sort()
```

modify the same object.

Assignment

```python
=
```

creates a **new object**.

---

# Comparing Both Cases

## Case 1

```python
a.append(40)
```

```
Same Object

↓

Modified
```

Original list changes.

---

## Case 2

```python
a = [40,50,60]
```

```
New Object

↓

New Reference
```

Original list remains unchanged.

---

# Immutable vs Mutable Behaviour

| Immutable Objects | Mutable Objects |
|-------------------|-----------------|
| Assignment creates a new object | Methods modify the same object |
| Original object remains unchanged | Original object changes |
| Examples: int, float, str, tuple | Examples: list, dict, set |

---

# Common Mistakes

## Mistake 1

Thinking

```python
a.append(40)
```

creates a new list.

It doesn't.

It modifies the existing list.

---

## Mistake 2

Thinking

```python
a = [40,50,60]
```

changes the original list.

It doesn't.

It simply points the local variable to a different list object.

---

# Interview Questions

### Q1. Why does `append()` change the original list?

Because `append()` modifies the same list object instead of creating a new one.

---

### Q2. Why doesn't

```python
a = [40,50,60]
```

change the original list?

Because assignment creates a completely new list object.

Only the local reference changes.

---

### Q3. What is Python's argument passing mechanism?

Python uses **Pass by Object Reference**.

The behavior depends on whether the object is mutable or immutable.

---

# Summary

- Python passes references to objects.
- Immutable objects create new objects on reassignment.
- Mutable objects can be modified in place.
- List methods modify the original list.
- Assignment (`=`) creates a new object and changes only the local reference.

---

> **End of Part 6**
================================================================================================================================================================
# Deep Dive: Why Does Python Behave This Way?

After studying immutable and mutable objects separately, the instructor explained **why Python behaves differently** in both cases.

Many beginners memorize the outputs but fail to understand the actual reason.

The answer lies in two concepts:

1. **Object Mutability**
2. **Object References**

Once these two concepts are clear, every output becomes easy to predict.

---

# Python Variables Do Not Store Values

One of the biggest misconceptions among beginners is that variables store values directly.

This is **not true**.

Variables in Python store **references** to objects.

Example

```python
a = 10
```

Most beginners imagine

```
a

↓

10
```

Actually Python stores

```
Variable

↓

Reference

↓

Integer Object

↓

10
```

The variable only knows **where the object is**.

It does not contain the object itself.

---

# Example

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

a

↑

b
```

Both variables point to the **same object**.

No copy is created.

---

# What Happens After Assignment?

Now suppose

```python
b = 20
```

Since integers are immutable,

Python creates a **new integer object**.

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

Notice

The integer **10 never changed**.

Only the reference of **b** changed.

---

# Why Doesn't This Happen with Lists?

Consider

```python
a = [10,20,30]

b = a
```

Memory

```
List Object

↓

[10,20,30]

↑

a

↑

b
```

Now execute

```python
b.append(40)
```

The list itself changes.

Memory becomes

```
List Object

↓

[10,20,30,40]

↑

a

↑

b
```

Both variables still point to the same object.

Therefore,

both variables observe the modification.

---

# Why Doesn't Assignment Modify the Original List?

Consider

```python
a = [10,20,30]

b = a

b = [40,50,60]
```

Initially

```
List A

↓

[10,20,30]

↑

a

↑

b
```

After assignment

```
List A

↓

[10,20,30]

↑

a


List B

↓

[40,50,60]

↑

b
```

The original list never changed.

Only **b** started pointing to another object.

---

# Important Rule

Always ask yourself one question:

> **Did Python modify the object or did it create a new object?**

If the object was modified,

every reference observes the change.

If a new object was created,

only the reference changes.

---

# Method vs Assignment

This is probably the most important comparison of the lecture.

---

## Case 1 — Method Call

```python
a.append(40)
```

Memory

```
Same Object

↓

Modified
```

Output

Original list changes.

---

## Case 2 — Assignment

```python
a = [40,50]
```

Memory

```
New Object

↓

Reference Updated
```

Output

Original list remains unchanged.

---

# How to Predict Output

Whenever you see a function,

follow these steps.

---

## Step 1

Identify the object type.

```
Integer?

↓

Immutable

List?

↓

Mutable
```

---

## Step 2

Inside the function,

look for

```
Method Call

or

Assignment
```

---

## Step 3

If

```
Method

↓

Same Object Modified
```

If

```
Assignment

↓

New Object Created
```

---

# Example 1

```python
def show(a):

    a.append(100)

numbers = [10,20]

show(numbers)

print(numbers)
```

Prediction

```
Mutable Object

↓

append()

↓

Original Modified
```

Output

```text
[10,20,100]
```

---

# Example 2

```python
def show(a):

    a = [100]

numbers = [10,20]

show(numbers)

print(numbers)
```

Prediction

```
Mutable Object

↓

Assignment

↓

New Object

↓

Original Unchanged
```

Output

```text
[10,20]
```

---

# Example 3

```python
def show(a):

    a = a + [40]

numbers = [10,20]

show(numbers)

print(numbers)
```

Output

```text
[10,20]
```

---

## Why?

Many beginners think

```python
a + [40]
```

modifies the list.

It doesn't.

The `+` operator creates a **new list**.

Equivalent to

```
Old List

↓

Copy

↓

Append 40

↓

Return New List
```

Therefore,

only the local variable changes.

---

# Summary Table

| Operation | Original Object Changes? |
|-----------|--------------------------|
| `append()` | ✅ Yes |
| `extend()` | ✅ Yes |
| `insert()` | ✅ Yes |
| `remove()` | ✅ Yes |
| `pop()` | ✅ Yes |
| `sort()` | ✅ Yes |
| `reverse()` | ✅ Yes |
| `=` Assignment | ❌ No |
| `+` Operator | ❌ No |
| Slicing (`[:]`) | ❌ Creates New List |

---

# Common Interview Questions

## Q1. Why does `append()` affect the original list?

Because `append()` modifies the same list object.

---

## Q2. Why doesn't assignment affect the original list?

Because assignment changes the reference instead of modifying the object.

---

## Q3. Why are integers unaffected after function calls?

Because integers are immutable.

Python creates a new integer object during reassignment.

---

## Q4. What argument passing mechanism does Python use?

**Pass by Object Reference (Call by Sharing).**

---

# Lecture 21 Summary

In this lecture, we explored Python's scope rules and argument-passing mechanism in depth.

We learned that variables declared outside functions belong to the **Global Scope**, while variables declared inside functions or received as parameters belong to the **Local Scope**.

We studied **Variable Shadowing**, where a local variable hides a global variable with the same name, and learned how the **`global` keyword** allows us to modify global variables directly from inside a function.

A major focus of the lecture was **UnboundLocalError**, which occurs because Python scans the entire function before execution and treats any assigned variable as local unless explicitly declared global.

We also discovered that Python **does not have block-level scope**, meaning variables declared inside `if`, `for`, and `while` statements remain accessible outside those blocks. Only **functions, classes, and modules** create new scopes.

Finally, we studied **Pass by Object Reference**, Python's unique argument-passing mechanism. We compared immutable and mutable objects and understood why methods such as `append()` modify the original list while assignment creates a completely new object.

---

# Quick Revision

- Global variables are declared outside functions.
- Local variables are declared inside functions.
- Function parameters are local variables.
- Local variables disappear after function execution.
- Assignment inside a function creates a local variable unless `global` is used.
- `global` allows modification of global variables.
- Python scans the function before execution.
- `UnboundLocalError` occurs when a local variable is accessed before assignment.
- Python does not have block-level scope.
- Only functions, classes, and modules create new scopes.
- Python uses **Pass by Object Reference**.
- Immutable objects create new objects during reassignment.
- Mutable objects can be modified in place.
- Methods like `append()` modify the original object.
- Assignment (`=`) changes the reference to a new object.

---

> **🎉 Lecture 21 Completed Successfully**
