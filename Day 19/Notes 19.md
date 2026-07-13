# Python Functions (User Defined Functions)

## Introduction to Functions

As programs become larger and more complex, writing the same piece of code repeatedly becomes inefficient. Python solves this problem using **functions**.

A **function** is a reusable block of code that performs a specific task. Instead of writing the same logic multiple times, we define it once and call it whenever required.

This concept is known as **Code Reusability**.

> **Definition**
>
> A function is a named block of code that performs a particular task and can be executed whenever it is called.

According to the lecture, a function is:

- A block of executable statements.
- Designed to perform one specific task.
- Defined once and used multiple times.
- One of the most important tools for writing modular programs. :contentReference[oaicite:0]{index=0}

---

# Why Do We Need Functions?

Imagine writing a program that calculates the sum of two numbers in twenty different places.

Without functions, you would have to write the same code twenty times.

If later you wanted to change the logic, you would again have to modify it twenty times.

Functions solve this problem by allowing you to write the code only once.

Example without functions:

```python
a = 10
b = 20
print(a + b)

x = 50
y = 30
print(x + y)

m = 100
n = 40
print(m + n)
```

The addition logic is repeated several times.

Instead, we can define one function and reuse it.

```python
def add(a, b):
    print(a + b)

add(10, 20)
add(50, 30)
add(100, 40)
```

The same code becomes much shorter, cleaner, and easier to maintain.

---

# Real-Life Analogy

The lecture compares a function to a **machine**.

Every machine works in three stages.

```
Input

↓

Processing

↓

Output
```

Exactly the same happens inside a function.

You provide input to the function.

↓

The function processes the input.

↓

The function returns or displays the output.

---

## Washing Machine Analogy

The lecture uses the example of a **washing machine**.

```
Dirty Clothes
        │
        ▼
 Washing Machine
 (Processing)
        │
        ▼
 Clean Clothes
```

Here,

- **Input:** Dirty clothes
- **Processing:** Washing
- **Output:** Clean clothes

Similarly, in a Python function,

```
Numbers

↓

Addition Logic

↓

Result
```

This makes functions easy to understand because every function behaves like a machine that transforms input into output. :contentReference[oaicite:1]{index=1}

---

# Benefits of Functions

Functions provide many advantages while developing software.

## 1. Code Reusability

The biggest advantage is that the same code can be reused multiple times.

Instead of writing the same logic repeatedly,

you simply call the function.

```
Define Once

↓

Call Many Times
```

---

## 2. Avoids Code Repetition

Repeated code increases program size and makes maintenance difficult.

Functions eliminate duplicate code.

---

## 3. Better Code Organization

Large programs become easier to understand when divided into small functions.

Instead of one huge file,

you have several small logical units.

Example

```
Main Program

│

├── Login Function

├── Payment Function

├── Search Function

└── Logout Function
```

---

## 4. Easy Testing

Small functions are easier to test independently.

If a bug appears,

you only test the affected function instead of the entire program.

---

## 5. Easy Debugging

Finding errors becomes much simpler because each function performs only one task.

---

## 6. Modularity

Functions divide a large application into smaller independent modules.

Each module performs a specific job.

---

## 7. Improves Readability

Meaningful function names explain the program automatically.

Instead of

```python
# 25 lines of addition code
```

we simply write

```python
calculate_total()
```

which immediately tells us the purpose.

---

# Function Development Process

According to the lecture and PDF, there are **two important steps** in working with user-defined functions.

```
Step 1

↓

Function Definition

↓

Step 2

↓

Function Call
```

Both steps are mandatory.

Only defining a function is not enough.

The function executes only when it is called. :contentReference[oaicite:2]{index=2}

---

# Step 1 — Function Definition

Creating the body of a function is called **Function Definition**.

This is where we write all the statements that should execute whenever the function is called.

General Syntax

```python
def function_name(parameters):
    statements
```

The function body must always be properly indented.

---

# Understanding the Syntax

```python
def add(a, b):
    c = a + b
    print(c)
```

### `def`

A reserved keyword that tells Python a function definition is beginning.

Without `def`, Python cannot recognize the function.

---

### Function Name

Every function must have a unique identifier.

```python
add()
calculate()
factorial()
```

Avoid using names of built-in functions like

```python
print
input
len
sum
```

---

### Parentheses

The parentheses contain the parameters.

```python
def add(a, b):
```

The parameters receive values when the function is called.

Parameters are optional.

Some functions take no parameters.

Example

```python
def greet():
    print("Hello")
```

---

### Colon

Every function header ends with

```python
:
```

Omitting it produces a SyntaxError.

---

### Indentation

Everything inside the function must have the same indentation.

Correct

```python
def add(a, b):
    c = a + b
    print(c)
```

Wrong

```python
def add(a, b):
c = a + b
print(c)
```

This raises an `IndentationError`.

---

# Example – Function Definition

The lecture demonstrates the following example.

```python
def add(a, b):
    print("Values are", a, "and", b)
    c = a + b
    print("Their sum is", c)
```

Notice that nothing executes simply by writing this code.

The function has only been **defined**, not executed. :contentReference[oaicite:3]{index=3}

---

# Important Rule

A function **never executes automatically**.

Python stores the function definition in memory.

The body executes only when the function is called.

```
Function Definition

↓

Stored in Memory

↓

Waiting...

↓

Function Call

↓

Execution Starts
```

---

# Program Execution Flow

One of the most important concepts explained in class is how Python executes programs.

Python begins execution from the first executable statement that is **not inside a function body**.

Consider

```python
def greet():
    print("Hello")

print("Start")
greet()
print("End")
```

Execution

```
Start

↓

greet()

↓

Hello

↓

End
```

Notice that Python skipped the function body initially because it was only defining the function.

The function body executed only when `greet()` was called.

---

# Interview Points

- A function is a reusable block of code.
- Functions promote code reusability.
- Functions improve readability and maintainability.
- A function must first be defined and then called.
- The keyword used to define a function is `def`.
- Python uses indentation to define the function body.
- Defining a function does not execute it.
- The function executes only after a function call.

---

# Quick Revision

- Function = Reusable block of code.
- Code Reusability = Define once, use many times.
- Functions reduce code duplication.
- Functions make programs modular.
- Two steps:
  - Function Definition
  - Function Call
- `def` is the keyword used to define a function.
- Proper indentation is mandatory.
- A function never runs automatically.
==============================================================================================================================================================
# Function Definition vs Function Call

While working with functions, two separate concepts are involved.

1. **Function Definition**
2. **Function Call**

Many beginners think writing a function automatically executes it.

This is **not true**.

A function must first be defined and then explicitly called.

---

# Function Definition

A **Function Definition** is the process of creating a function.

During function definition,

- Python reads the function.
- Stores it in memory.
- Waits for a function call.

It **does not execute** the statements inside the function.

General Syntax

```python
def function_name(parameters):
    statements
```

---

# Function Call

A **Function Call** tells Python to execute the statements written inside the function.

Syntax

```python
function_name(arguments)
```

Whenever Python encounters a function call,

it jumps to the function body,

executes all statements,

and then returns back to the calling statement.

---

# Execution Flow

```
Program Starts

↓

Function Definition

↓

Stored in Memory

↓

Main Program Executes

↓

Function Call

↓

Function Body Executes

↓

Control Returns

↓

Remaining Program Executes
```

---

# Example 1 – Simple Function

```python
def greet():
    print("Hello User Ji")
    print("How was your Diwali?")

greet()
```

### Output

```text
Hello User Ji
How was your Diwali?
```

---

# Dry Run

Initially,

Python reads

```python
def greet():
```

and stores the function in memory.

Nothing is printed.

Then Python reaches

```python
greet()
```

Now the function body starts executing.

```
greet()

↓

Hello User Ji

↓

How was your Diwali?

↓

Function Ends

↓

Control Returns
```

---

# Calling the Same Function Multiple Times

One of the biggest advantages of functions is that the same function can be called repeatedly.

```python
def greet():
    print("Hello User Ji")
    print("How was your Diwali?")

greet()

print("----------------")

greet()
```

### Output

```text
Hello User Ji
How was your Diwali?
----------------
Hello User Ji
How was your Diwali?
```

Notice that

the function definition was written only once,

but it executed twice because it was called twice.

This demonstrates **Code Reusability**. :contentReference[oaicite:0]{index=0}

---

# Example 2 – Function Executes Only When Called

```python
def demo():
    print("Inside Function")

print("Program Started")
```

### Output

```text
Program Started
```

Why wasn't

```text
Inside Function
```

printed?

Because the function was never called.

---

# Example 3 – Calling the Function

```python
def demo():
    print("Inside Function")

print("Program Started")

demo()

print("Program Ended")
```

### Output

```text
Program Started
Inside Function
Program Ended
```

Execution

```
Program Started

↓

demo()

↓

Inside Function

↓

Return

↓

Program Ended
```

---

# Parameters and Arguments

These two terms are often confused,

but technically they have different meanings.

---

## Parameters

Parameters are the variables written in the function definition.

Example

```python
def greet(name):
    print("Hello", name)
```

Here,

```python
name
```

is called a **Parameter**.

Parameters are also known as

- Formal Parameters
- Formal Arguments

---

## Arguments

Arguments are the actual values supplied while calling the function.

Example

```python
greet("Sachin")
```

Here,

```text
Sachin
```

is an **Argument**.

Arguments are also called

- Actual Arguments

---

# Difference Between Parameters and Arguments

| Parameters | Arguments |
|------------|-----------|
| Present in function definition | Present in function call |
| Receive values | Supply values |
| Formal Arguments | Actual Arguments |
| Variables | Real values |

---

# Example – Greeting Multiple Users

```python
def greet(name):
    print("Hello", name, "Ji")
    print("How was your Diwali?")

greet("Sachin")
greet("Nitin")
greet("Ravi")
```

### Output

```text
Hello Sachin Ji
How was your Diwali?

Hello Nitin Ji
How was your Diwali?

Hello Ravi Ji
How was your Diwali?
```

---

## Explanation

The parameter

```python
name
```

receives different values during different calls.

### First Call

```
name = "Sachin"
```

### Second Call

```
name = "Nitin"
```

### Third Call

```
name = "Ravi"
```

The same function behaves differently depending on the argument passed.

---

# Example – Calculator Function

The lecture demonstrates taking user input outside the function and passing it as arguments.

```python
def calculate(x, y):
    z = x + y
    print("Sum is", z)

a = int(input("Enter first integer: "))
b = int(input("Enter second integer: "))

calculate(a, b)
```

Suppose the user enters

```text
10
20
```

Output

```text
Sum is 30
```

---

## Dry Run

```
a = 10

b = 20

↓

calculate(a, b)

↓

x = 10

y = 20

↓

z = 30

↓

Print Sum is 30
```

---

# Important Observation

Notice the parameter names

```python
x

y
```

and the argument names

```python
a

b
```

are different.

This is perfectly valid.

Only the **values** matter,

not the variable names.

Python internally performs

```
x ← a

↓

y ← b
```

---

# Common Mistakes

## Mistake 1

Defining a function but never calling it.

```python
def greet():
    print("Hello")
```

Nothing is printed.

---

## Mistake 2

Calling a function before defining it.

```python
greet()

def greet():
    print("Hello")
```

Output

```text
NameError
```

Python executes programs from top to bottom.

The function must be defined before it is called.

---

## Mistake 3

Forgetting parentheses.

Wrong

```python
greet
```

Correct

```python
greet()
```

Without parentheses,

the function is not executed.

---

# Interview Points

- Function Definition creates the function.
- Function Call executes the function.
- Parameters belong to the function definition.
- Arguments belong to the function call.
- Parameters receive values.
- Arguments supply values.
- Parameter names and argument variable names need not be the same.
- A function can be called any number of times.

---

# Quick Revision

- Function Definition → Creates the function.
- Function Call → Executes the function.
- Parameters → Variables in the function definition.
- Arguments → Values supplied during function call.
- Functions execute only when called.
- Python executes programs from top to bottom.

---

**End of Part 2**
==============================================================================================================================================================
# The `return` Statement in Python Functions

Until now, all the functions we created directly displayed the result using the `print()` function.

However, in real-world programming, functions generally **return** values instead of printing them.

The **`return`** statement sends the computed result back to the function caller.

---

# Why Do We Need `return`?

Consider the following function.

```python
def add(a, b):
    print(a + b)

add(10, 20)
```

Output

```text
30
```

This function only displays the answer.

Suppose we now want to

- store the result,
- multiply it by another number,
- pass it to another function,
- or write it into a file.

We cannot do that because the function never gives the value back.

Instead,

```python
def add(a, b):
    return a + b

ans = add(10, 20)

print(ans)
```

Output

```text
30
```

Now the result can be reused anywhere in the program.

---

# Definition

> **The `return` statement terminates the execution of a function and sends a value back to the calling statement.**

After executing a `return` statement,

the function immediately stops executing.

Control goes back to the place where the function was called.

---

# Syntax

```python
def function_name(parameters):

    statements

    return value
```

The value may be

- a constant
- a variable
- an expression
- multiple values

---

# Ways of Returning Values

Python allows several ways to return a value.

---

## Method 1 – Returning a Constant

```python
def demo():
    return 100

x = demo()

print(x)
```

Output

```text
100
```

---

## Method 2 – Returning a Variable

```python
def add(a, b):

    c = a + b

    return c

result = add(10, 20)

print(result)
```

Output

```text
30
```

---

## Method 3 – Returning an Expression

Instead of storing the result in another variable,

we can directly return the expression.

```python
def add(a, b):

    return a + b

print(add(10, 20))
```

Output

```text
30
```

This is shorter and commonly used.

---

# Example – Returning the Sum

```python
def calculate(x, y):

    z = x + y

    return z

ans = calculate(10, 20)

print("Sum is", ans)
```

Output

```text
Sum is 30
```

---

# Execution Flow

```
calculate(10,20)

↓

x = 10

↓

y = 20

↓

z = 30

↓

return z

↓

ans = 30

↓

Print Answer
```

---

# What Happens After `return`?

One very important property of the `return` statement is

> **It immediately terminates the function.**

Any statement written after `return`

never executes.

Example

```python
def demo():

    print("One")

    return

    print("Two")

demo()
```

Output

```text
One
```

Notice

```text
Two
```

is never printed.

---

# Functions Without a `return` Statement

Many beginners believe that if a function has no `return` statement,

it returns nothing.

Actually,

every Python function returns **something**.

If you don't explicitly write a `return` statement,

Python automatically adds

```python
return None
```

at the end of the function.

---

# Example

```python
def calculate(x, y):

    z = x + y

result = calculate(10,20)

print(result)
```

Output

```text
None
```

---

# Why Does It Print `None`?

The function computes

```
30
```

but never returns it.

Therefore,

Python automatically executes

```python
return None
```

Execution

```
calculate()

↓

Compute Sum

↓

No Return Found

↓

return None

↓

result = None

↓

Print None
```

---

# What is `None`?

`None` is a special object in Python.

It represents

> **No Value**

or

> **Nothing**

It is different from

```
0

False

""

[]
```

---

# NoneType

The data type of

```python
None
```

is

```python
NoneType
```

Example

```python
print(type(None))
```

Output

```text
<class 'NoneType'>
```

---

# Practical Example – Absolute Value Function

The lecture demonstrates creating your own version of Python's built-in `abs()` function.

```python
def absolute(n):

    if n > 0:
        return n

    else:
        return -n

num = int(input("Enter number : "))

ans = absolute(num)

print("Absolute value is", ans)
```

---

## Example 1

Input

```text
25
```

Output

```text
Absolute value is 25
```

---

## Example 2

Input

```text
-25
```

Output

```text
Absolute value is 25
```

---

## Dry Run

Suppose

```
num = -15
```

Execution

```
absolute(-15)

↓

n > 0 ?

↓

False

↓

return -(-15)

↓

15

↓

Print 15
```

---

# Calling Functions Before Definition

Unlike Java and C++,

Python executes programs from top to bottom.

Therefore,

the function definition must appear before the function call.

Wrong

```python
greet()

def greet():

    print("Hello")
```

Output

```text
NameError
```

Correct

```python
def greet():

    print("Hello")

greet()
```

Output

```text
Hello
```

---

# Common Mistakes

## Mistake 1

Using `print()` instead of `return`.

Wrong

```python
def add(a,b):

    print(a+b)
```

Correct

```python
def add(a,b):

    return a+b
```

---

## Mistake 2

Writing statements after `return`.

Wrong

```python
return x

print(x)
```

The second statement never executes.

---

## Mistake 3

Forgetting to store the returned value.

Wrong

```python
add(10,20)
```

Correct

```python
ans = add(10,20)
```

---

# Interview Points

- `return` sends a value back to the caller.
- `return` immediately terminates the function.
- Every Python function returns something.
- If no return statement is present, Python automatically returns `None`.
- The data type of `None` is `NoneType`.
- Functions should generally return values instead of printing them.

---

# Quick Revision

- `return` sends data back to the caller.
- A function may return a constant, variable, or expression.
- Statements after `return` never execute.
- Missing `return` means Python returns `None`.
- `None` belongs to the `NoneType` data type.
- Python functions must be defined before they are called.

---

**End of Part 3**
==============================================================================================================================================================
# Returning Multiple Values from a Function

One of the powerful features of Python is that a function can return **multiple values** at once.

Many programming languages such as **C, C++ and Java** allow a function to return only a single value directly. Python, however, makes returning multiple values simple and elegant.

Internally, Python **packs** all returned values into a **tuple**, and when required, it can **unpack** them automatically.

> **Note**
>
> Although it looks like multiple values are being returned, Python actually returns **one tuple object** containing all the values.

---

# Returning Multiple Values

General Syntax

```python
def function_name():
    ...
    return value1, value2, value3
```

Python internally converts this into

```python
return (value1, value2, value3)
```

This automatic process is known as **Tuple Packing**.

---

# Example – Returning Sum and Difference

The lecture demonstrates the following example.

```python
def calculate(x, y):

    total = x + y
    difference = x - y

    return total, difference
```

Notice

```python
return total, difference
```

Internally becomes

```python
return (total, difference)
```

The function returns one tuple containing two values. :contentReference[oaicite:0]{index=0}

---

# Receiving Multiple Returned Values

There are two common ways to receive the returned tuple.

1. Store the complete tuple.
2. Unpack the tuple into separate variables.

---

# Method 1 – Store as a Tuple

```python
def calculate(x, y):

    total = x + y
    difference = x - y

    return total, difference

result = calculate(5, 9)

print(result)
```

### Output

```text
(14, -4)
```

Notice that the returned object is a tuple.

---

# Accessing Individual Values

Since the returned object is a tuple,

individual values can be accessed using indexing.

```python
def calculate(x, y):

    total = x + y
    difference = x - y

    return total, difference

result = calculate(5, 9)

print("Sum is", result[0])

print("Difference is", result[1])
```

### Output

```text
Sum is 14
Difference is -4
```

---

# Dry Run

```
calculate(5,9)

↓

total = 14

↓

difference = -4

↓

return (14,-4)

↓

result = (14,-4)

↓

result[0] → 14

↓

result[1] → -4
```

---

# Method 2 – Tuple Unpacking (Recommended)

Instead of storing the tuple,

Python allows us to unpack it directly into multiple variables.

```python
def calculate(x, y):

    total = x + y
    difference = x - y

    return total, difference

s, d = calculate(5, 9)

print("Sum is", s)

print("Difference is", d)
```

### Output

```text
Sum is 14
Difference is -4
```

---

# How Tuple Unpacking Works

The function returns

```text
(14, -4)
```

Python automatically performs

```
s = 14

↓

d = -4
```

No indexing is required.

This approach is cleaner and more readable.

---

# Another Example

```python
def student():

    return "Rahul", 95, "A"

name, marks, grade = student()

print(name)
print(marks)
print(grade)
```

### Output

```text
Rahul
95
A
```

Python automatically unpacks all three values.

---

# Packing and Unpacking

These are two important interview concepts.

---

## Packing

Combining multiple values into one tuple.

Example

```python
x = 10
y = 20

t = x, y
```

Python automatically creates

```python
t = (10,20)
```

This is called **Packing**.

---

## Unpacking

Extracting values from a tuple into individual variables.

Example

```python
a, b = (10,20)
```

Python performs

```text
a = 10

b = 20
```

This process is called **Unpacking**.

---

# Function Arguments

Until now,

the values were passed simply by their position.

These are called **Positional Arguments**.

Python supports four types of arguments.

1. Positional Arguments
2. Keyword Arguments
3. Default Arguments
4. Variable Length Arguments

In this lecture,

only the first two types are discussed.

The remaining two are covered in the next lecture. :contentReference[oaicite:1]{index=1}

---

# Positional Arguments

In positional arguments,

values are assigned to parameters **based on their position**.

General Syntax

```python
def function(parameter1, parameter2):

    statements

function(argument1, argument2)
```

Parameter mapping

```
parameter1 ← argument1

↓

parameter2 ← argument2
```

The order is extremely important.

---

# Example

```python
def grocery(name, price):

    print("Item is", name)

    print("Price is", price)

grocery("Bread", 20)
```

### Output

```text
Item is Bread
Price is 20
```

Python performs

```
name = "Bread"

↓

price = 20
```

---

# Ordering Problem

Suppose we reverse the arguments.

```python
grocery(250, "Butter")
```

Output

```text
Item is 250
Price is Butter
```

Although the program executes,

the output becomes logically incorrect.

This is one drawback of positional arguments.

---

# Number of Arguments Must Match

Another important rule discussed in class is

> The number of arguments must exactly match the number of parameters.

Example

```python
def check(n1, n2):

    pass

check(5.4)
```

### Output

```text
TypeError:
missing 1 required positional argument: 'n2'
```

Python expected

```
2 Parameters

↓

Only 1 Argument Supplied
```

Therefore,

a `TypeError` is raised.

---

# More Examples

Correct

```python
def add(a, b):

    return a + b

add(10,20)
```

Incorrect

```python
add(10)
```

Output

```text
TypeError
```

---

# Common Mistakes

## Mistake 1

Passing fewer arguments.

```python
check(5)
```

Produces

```text
TypeError
```

---

## Mistake 2

Passing extra arguments.

```python
check(1,2,3)
```

Produces

```text
TypeError
```

---

## Mistake 3

Changing the order accidentally.

Wrong

```python
grocery(200,"Milk")
```

Correct

```python
grocery("Milk",200)
```

---

# Interview Points

- Python functions can return multiple values.
- Internally, multiple returned values are packed into a tuple.
- Tuple unpacking automatically distributes values into variables.
- Positional arguments are matched according to position.
- The number of positional arguments must equal the number of parameters.
- Incorrect ordering may produce logical errors even if the program runs successfully.

---

# Quick Revision

- Multiple values are returned as a tuple.
- Packing combines values into a tuple.
- Unpacking extracts tuple values into variables.
- Positional arguments depend on order.
- The number of arguments and parameters must match exactly.

---

**End of Part 4**
=============================================================================================================================================================
# Keyword Arguments

In the previous section, we learned about **Positional Arguments**, where arguments are matched with parameters according to their position.

Although positional arguments are simple to use, they have one major drawback:

- The order of arguments must always be correct.
- Swapping the arguments may produce logically incorrect results.

Python solves this problem using **Keyword Arguments**.

---

# What are Keyword Arguments?

Keyword arguments allow us to explicitly specify **which argument belongs to which parameter** by writing the parameter name during the function call.

Instead of relying on position,

Python uses the **parameter names** for mapping.

---

# General Syntax

```python
def function_name(parameter1, parameter2):

    statements

function_name(parameter1=value1, parameter2=value2)
```

Instead of

```python
function_name(value1, value2)
```

we write

```python
function_name(parameter1=value1,
              parameter2=value2)
```

Now Python performs mapping using the parameter names instead of their positions.

---

# Why Keyword Arguments?

Consider the following function.

```python
def grocery(name, price):

    print("Item :", name)
    print("Price:", price)
```

Using positional arguments

```python
grocery("Bread", 20)
```

Output

```text
Item : Bread
Price: 20
```

Everything is correct because

```
name ← Bread

↓

price ← 20
```

---

# The Problem with Positional Arguments

Suppose we accidentally reverse the arguments.

```python
grocery(20, "Bread")
```

Output

```text
Item : 20
Price: Bread
```

Although the program executes successfully,

the result becomes meaningless.

Python has no idea that

```
20

```

is actually the price.

It simply assigns values according to their positions.

---

# Solving the Problem

Keyword arguments eliminate this dependency on position.

```python
def grocery(name, price):

    print("Item :", name)
    print("Price:", price)

grocery(price=20, name="Bread")
```

Output

```text
Item : Bread
Price: 20
```

Notice

The arguments were supplied in reverse order,

yet the output is perfectly correct.

Python performs

```
name ← "Bread"

↓

price ← 20
```

because the parameter names were explicitly mentioned.

---

# Another Example

```python
def student(name, marks):

    print("Name :", name)
    print("Marks:", marks)

student(marks=92, name="Rahul")
```

Output

```text
Name : Rahul
Marks: 92
```

Again,

the order of arguments does not matter.

---

# How Python Maps Keyword Arguments

Suppose we call

```python
student(marks=80,
        name="Amit")
```

Python internally performs

```
marks

↓

80

name

↓

Amit
```

It completely ignores the argument positions.

---

# Advantages of Keyword Arguments

## 1. Order Does Not Matter

Positional

```python
add(10,20)
```

Keyword

```python
add(b=20,
    a=10)
```

Both are valid.

---

## 2. Improves Readability

Compare

```python
calculate(15000,
          12,
          6.5)
```

with

```python
calculate(
    salary=15000,
    experience=12,
    tax=6.5
)
```

The second version immediately explains what every value represents.

---

## 3. Prevents Logical Errors

Keyword arguments eliminate mistakes caused by incorrect ordering.

---

# Restrictions of Keyword Arguments

Although keyword arguments are very flexible,

there are some important rules.

---

## Rule 1 – Parameter Names Must Match Exactly

Python matches arguments using parameter names.

Therefore,

the spelling must be exactly the same.

Example

```python
def grocery(name, price):

    print(name, price)
```

Correct

```python
grocery(name="Milk",
        price=40)
```

Incorrect

```python
grocery(Name="Milk",
        price=40)
```

Output

```text
TypeError
```

because

```
Name

≠

name
```

Python is case-sensitive.

---

## Rule 2 – Unknown Parameter Names Are Not Allowed

Wrong

```python
grocery(item="Milk",
        cost=40)
```

Output

```text
TypeError
```

because

```
item

cost
```

are not parameters of the function.

---

## Rule 3 – Keyword Names are Case Sensitive

Example

Function

```python
def display(price):

    print(price)
```

Correct

```python
display(price=500)
```

Incorrect

```python
display(Price=500)
```

Output

```text
TypeError
```

Python treats

```
price

and

Price
```

as completely different identifiers.

---

# Positional vs Keyword Arguments

| Positional Arguments | Keyword Arguments |
|----------------------|-------------------|
| Mapping depends on position | Mapping depends on parameter names |
| Order is important | Order is not important |
| Easier to make mistakes | More readable |
| Simple syntax | Slightly longer syntax |

---

# Class Example

```python
def employee(name, salary):

    print("Employee :", name)

    print("Salary   :", salary)

employee(salary=35000,
         name="Sachin")
```

Output

```text
Employee : Sachin
Salary   : 35000
```

---

# Common Mistakes

## Mistake 1

Using the wrong parameter name.

```python
display(cost=500)
```

Produces

```text
TypeError
```

---

## Mistake 2

Changing the capitalization.

```python
display(Price=100)
```

Produces

```text
TypeError
```

---

## Mistake 3

Assuming Python ignores spelling mistakes.

Python matches parameters **exactly**.

Even one incorrect letter causes an error.

---

# Interview Points

- Keyword arguments map values using parameter names.
- Order of keyword arguments does not matter.
- Parameter names must match exactly.
- Python is case-sensitive.
- Keyword arguments improve code readability.
- They reduce logical mistakes caused by incorrect ordering.

---

# Lecture 19 Summary

In this lecture, we introduced **User Defined Functions**, one of the most important concepts in Python programming. We learned that functions improve **code reusability**, reduce duplication, and make programs modular and easier to maintain.

We studied the complete process of working with functions, beginning with **function definition** and **function calls**. We then understood the difference between **parameters** and **arguments**, and how values are passed to functions.

Next, we explored the **`return` statement**, learning that functions can return constants, variables, expressions, or even multiple values. We also saw that if a function does not explicitly return anything, Python automatically returns **`None`**, whose data type is **`NoneType`**.

The lecture also introduced **Tuple Packing** and **Tuple Unpacking**, demonstrating how Python internally returns multiple values as a tuple.

Finally, we studied the first two types of function arguments:

- **Positional Arguments**, where mapping depends on the order of arguments.
- **Keyword Arguments**, where mapping depends on parameter names rather than position.

The remaining argument types—**Default Arguments** and **Variable-Length Arguments**—are introduced in the next lecture.

---

# Quick Revision

- A function is a reusable block of code.
- Functions must be **defined** before they are **called**.
- **Parameters** belong to the function definition.
- **Arguments** belong to the function call.
- The `return` statement sends a value back to the caller.
- If no value is returned, Python returns `None`.
- Multiple returned values are automatically packed into a tuple.
- Tuple unpacking assigns returned values directly to variables.
- Positional arguments depend on order.
- Keyword arguments depend on parameter names.

---

> **Lecture 19 Completed ✅**

---

**End of Part 1**
