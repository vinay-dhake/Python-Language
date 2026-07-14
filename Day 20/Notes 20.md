# Python Programming – Lecture 20
# Advanced Function Arguments & Variable Scope

## Topics Covered

- Mixing Positional and Keyword Arguments
- Default Arguments
- Function Overloading in Python
- Variable-Length Arguments (*args)
- Variable Scope
- Global Variables
- Local Variables

---

# Introduction

In the previous lecture, we learned about Positional Arguments and Keyword Arguments.

In this lecture, we extend those concepts by studying more advanced function argument techniques. These features make Python functions more flexible and allow programmers to write cleaner, reusable, and more maintainable code.

By the end of this lecture, you will understand:

- How positional and keyword arguments can be mixed.
- How default values simplify function calls.
- Why Python doesn't support function overloading.
- How *args allows functions to accept any number of arguments.
- How variable scope determines where variables can be accessed.

---

# Mixing Positional and Keyword Arguments

Python allows both Positional Arguments and Keyword Arguments in the same function call.

However, there is one important rule that every programmer must remember.

> Rule
>
> Positional arguments must always appear before keyword arguments.

---

## Correct Usage

def grocery(item, price, company):
    print(f"Item: {item}")
    print(f"Price: {price}")
    print(f"Company: {company}")

grocery("Sauce", price=200, company="Kissan")

### Output

Item: Sauce
Price: 200
Company: Kissan

### Explanation

Python maps the values as follows:

item      ← "Sauce"
price     ← 200
company   ← "Kissan"

Since positional arguments come first and keyword arguments follow, the function executes successfully.

---

## Incorrect Usage

def grocery(item, price):
    print(item, price)

grocery(price=250, "Butter")

### Output

SyntaxError:
positional argument follows keyword argument

---

## Why Does This Error Occur?

When Python encounters

price=250

it understands that keyword arguments have started.

After this point, Python expects all remaining arguments to also be keyword arguments.

Therefore,

"Butter"

cannot be supplied as a positional argument.

---

## Visual Representation

Correct

Positional

↓

Positional

↓

Keyword

↓

Keyword

Incorrect

Keyword

↓

Positional

---

# Rule to Remember

✔️ Valid

display(10, b=20)

✔️ Valid

display(10,20)

✔️ Valid

display(a=10,b=20)

❌ Invalid

display(a=10,20)

Produces

SyntaxError

---

# Memory Trick

Think of keyword arguments as the final stage of a function call.

Once keyword arguments begin,

you cannot go back to positional arguments.

---

# Default Arguments

Many times a function contains parameters whose values remain the same most of the time.

Instead of asking the user to provide those values repeatedly,

Python allows us to assign default values to parameters.

These parameters are known as Default Arguments.

---

# Syntax

def function_name(parameter=default_value):
    statements

Example

def greet(name, message="Good Morning"):
    print("Hello", name)
    print(message)

Here,

message

↓

Good Morning

is the default value.

---

# Example 1 – Using the Default Value

def greet(name, message="Good Morning"):
    print("Hello", name)
    print(message)

greet("Sachin")

### Output

Hello Sachin
Good Morning

### Explanation

Only one argument is supplied.

Therefore,

Python automatically assigns

message = "Good Morning"

---

# Example 2 – Overriding the Default Value

greet("Sachin", "Happy Diwali")

### Output

Hello Sachin
Happy Diwali

Now Python ignores the default value because a new value has been supplied.

---

# How Default Arguments Work

Python checks whether an argument has been supplied.

If yes,

it uses that value.

Otherwise,

it falls back to the default value.

Argument Given?

      │

 Yes──┴──No

 │         │

Use      Use Default
Argument   Value

---

# Rule of Default Arguments

> Non-default parameters cannot appear after default parameters.

---

## Incorrect Definition

def grocery(name="Coffee", price, company):
    pass

### Output
SyntaxError

---

## Correct Definition

def grocery(name="Coffee",
             price=350,
             company="Nestle"):

    print(name, price, company)

---

# Why This Rule Exists

Suppose Python allowed

def demo(a=10,b):

Now if someone calls

demo(20)

Python cannot decide

whether

20

↓

a

or

20

↓

b

To avoid this ambiguity,

Python enforces the rule.

---

# Skipping Default Arguments

Suppose

def grocery(name="Coffee",
             price=350,
             company="Nestle"):

    print(name, price, company)

---

## Using All Default Values

grocery()

Output

Coffee 350 Nestle

---

## Overriding One Value

grocery(company="ITC")

Output

Coffee 350 ITC

Notice

name

↓

Default

price

↓

Default

company

↓

Overridden

This is possible because we used a keyword argument.

---

## Invalid Attempt

grocery("Tea", , "ITC")

Output

SyntaxError

Python never allows blank arguments.

---

## Correct Way

grocery("Tea", company="ITC")

Output

Tea 350 ITC

Here,

name

↓

Tea

price

↓

Default

company

↓

ITC

---

# Class Assignment – Area of Circle

The lecture demonstrated using a default argument for π.

import math

def calc_area(radius, pi=3.14):

    area = pi * math.pow(radius,2)

    print("Area is:", area)

radius = int(input("Enter radius: "))

calc_area(radius)

### Sample Input

4

### Output

Area is: 50.24

Since the user did not provide the value of π,

Python automatically used

pi = 3.14

---

# Advantages of Default Arguments

- Makes parameters optional.
- Reduces repetitive code.
- Produces cleaner function calls.
- Improves readability.
- Makes functions more flexible.

---

# Common Mistakes

### Incorrect Order

def show(a=10,b):

❌ SyntaxError

---

### Leaving Blank Arguments

show(10,,20)

❌ SyntaxError

---

### Forgetting Keyword Arguments

show(company="ITC")

✔️ Correct

---

# Interview Points

- Positional arguments must always come before keyword arguments.
- Once keyword arguments begin, all remaining arguments must also be keyword arguments.
- Default arguments make parameters optional.
- Required parameters cannot follow default parameters.
- Default values can always be overridden by supplying new arguments.
- Keyword arguments are useful when skipping intermediate default parameters.

---

End of Part 1
===============================================================================================================================================================
# Function Overloading in Python

## What is Function Overloading?

In programming languages like Java, C++, and C#, we can create multiple functions having the same name but different parameter lists.

This concept is known as Function Overloading.

### Example (Java)

add(int a, int b)

add(int a, int b, int c)

add(double a, double b)

All these functions have the same name but different parameter lists.

The compiler automatically decides which function should execute based on the arguments supplied.

---

# Does Python Support Function Overloading?

> No. Python does not support Function Overloading.

Unlike Java or C++, Python allows only one function with a particular name.

If another function with the same name is defined, the previous function is completely overwritten.

---

# Why Doesn't Python Support Function Overloading?

The lecture explains a very important reason.

In Python,

> Everything is an Object.

Functions are also objects.

When we define a function,

Python creates a Function Object in memory.

The function name is simply a reference variable pointing to that object.

Function Object

        ▲

        │

 add_number

Now suppose another function with the same name is created.

Python simply changes the reference.

Old Function Object

        ▲

        │

 add_number

↓

New Function Defined

↓

Reference shifts

↓

New Function Object

        ▲

        │

 add_number

The previous function becomes unreachable and is eventually removed by Python's Garbage Collector.

Therefore,

only the newest function remains.

---

# Example
def add_number(a, b):
    return a + b

def add_number(a, b, c):
    return a + b + c

Many beginners expect Python to store both functions.

Actually,

the second definition completely replaces the first one.

---

# What Happens Internally?

Initially,

add_number

↓

Function (2 Parameters)

After the second definition,

add_number

↓

Function (3 Parameters)

The first function no longer exists.

---

# Example

def add_number(a, b):
    return a + b

def add_number(a, b, c):
    return a + b + c

print(add_number(5,7))

### Output

TypeError:
add_number() missing 1 required positional argument: 'c'

---

# Why Did This Error Occur?

Many students think

5

↓

a

7

↓

b

should work.

But Python only remembers

def add_number(a,b,c)

The previous function

def add_number(a,b)

was overwritten.

Therefore,

Python expects

a

b

c

Three arguments.

Only two were supplied.

Hence,

TypeError

---

# Memory Diagram

Initially

add_number

↓

Function (2 Parameters)

After redefining

add_number

↓

Function (3 Parameters)

Old Function

↓

Garbage Collection

---

# Interview Question

Q. Why doesn't Python support Function Overloading?

Answer:

Python treats functions as objects.

The function name is merely a reference variable.

Whenever another function with the same name is defined,

the reference simply points to the latest function object,

overwriting the previous one.

---

# Variable-Length Arguments (*args)

Since Python does not support function overloading,

how can we create functions that accept

- two arguments,
- three arguments,
- five arguments,
- or even fifty arguments?

Python solves this problem using

## Variable-Length Arguments

written using

*args

---

# What are Variable-Length Arguments?

Variable-length arguments allow a function to accept any number of positional arguments.

Instead of defining

add(a,b)

add(a,b,c)

add(a,b,c,d)

we write

add(*args)

Now the same function works for every case.

---

# Syntax

def function_name(*args):

    statements

The name

args

is not compulsory.

Only

*

is mandatory.

These are all valid.

def add(*args):

def add(*numbers):

def add(*values):

---

# What is the Data Type of args?

The lecture explains that

Python automatically packs all arguments into a Tuple.

Example

def demo(*x):

    print(type(x))

demo(10,20,30)

### Output

<class 'tuple'>

So,

10

20

30

becomes

(10,20,30)

---

# Class Example – Dynamic Addition

def add_number(*x):

    print(type(x))

    total_sum = 0

    for value in x:
        total_sum += value

    print("Sum =", total_sum)

---

## Call 1

add_number(5,7)

Output

<class 'tuple'>

Sum = 12

---

## Call 2

add_number(5,7,9)

Output

<class 'tuple'>

Sum = 21

---

## Call 3

add_number(5,7,9,11)

Output

<class 'tuple'>

Sum = 32

Notice that

the same function handled

- 2 arguments
- 3 arguments
- 4 arguments

without any changes.

---

# Dry Run

Suppose

add_number(5,7,9)

Python performs

x

↓

(5,7,9)

↓

Loop Starts

↓

5

↓

7

↓

9

↓

Sum = 21

---

# Advantages of *args

- Accepts unlimited positional arguments.
- Eliminates the need for function overloading.
- Makes functions highly flexible.
- Frequently used in library development.
- Very useful when the number of inputs is unknown.

---

# Interview Points

- Python does not support function overloading.
- Functions are objects.
- Function names are references.
- Redefining a function overwrites the previous one.
- *args accepts any number of positional arguments.
- Python stores *args as a tuple.

---

# Quick Revision

- Function overloading is not supported in Python.
- The latest function definition replaces the previous one.
- *args allows unlimited positional arguments.
- args is a tuple.
- The name args is optional; only * is mandatory.

---

End of Part 2
==============================================================================================================================================================
# Variable-Length Arguments (*args) – More Examples
In the previous section, we learned that *args allows a function to accept any number of positional arguments.

The arguments supplied during the function call are automatically packed into a tuple, allowing us to iterate over them using a loop.

One of the most common applications of *args is processing an unknown amount of data.

---

# Class Example – Finding the Largest String

Suppose a user passes multiple strings to a function.

The number of strings is not fixed.

Our task is to determine the length of the largest string.

---

## Program

def find_largest(*args):

    max_len = 0

    for s in args:

        if len(s) > max_len:
            max_len = len(s)

    return max_len


result = find_largest("Hi", "Welcome", "Hello")

print(result)

---

## Output

7

---

## Explanation

Python automatically packs

"Hi"

"Welcome"

"Hello"

into

("Hi", "Welcome", "Hello")

The loop checks

Length("Hi")

↓

2

Length("Welcome")

↓

7

Length("Hello")

↓

5

The maximum length is

7

which is returned.

---

# Dry Run

args

↓

("Hi","Welcome","Hello")

↓

max_len = 0

↓

2 > 0

↓

max_len = 2

↓

7 > 2

↓

max_len = 7

↓

5 > 7

↓

False

↓

return 7

---

# Another Example

Find the maximum number.

def maximum(*numbers):

    max_value = numbers[0]

    for num in numbers:

        if num > max_value:

            max_value = num

    return max_value


print(maximum(5,7,2,18,10))

Output

18

---

# Restrictions on *args

Although *args is flexible, Python imposes a few important rules.

---

# Rule 1 – Only One *args Parameter

A function can contain only one variable-length argument.

Correct

def show(*numbers):
    pass

Incorrect

def show(*x,*y):
    pass

Output

SyntaxError

---

# Rule 2 – *args Usually Appears at the End

Normally, *args is written as the last parameter.

def show(a,b,*args):
    pass

This is the most common and recommended style.

---

# What Happens If a Parameter Appears After *args?

Python actually allows parameters after *args, but they cannot be supplied positionally.

They must be passed using keyword arguments (or have a default value).

Example

def show(*numbers, message):

    print(numbers)

    print(message)

show(10,20,30,message="Completed")

Output

(10, 20, 30)

Completed

Notice that

message

was supplied using a keyword argument.

---

# Why?

Python cannot determine where

*args

ends

↓

message

begins

Therefore,

keyword arguments remove this ambiguity.

---

# Summary of *args Rules

| Rule | Description |
|-------|-------------|
| Only one *args | A function can contain only one variable-length parameter. |
| Stored as Tuple | All arguments are packed into a tuple. |
| Unlimited Inputs | Accepts any number of positional arguments. |
| Usually Last | It is recommended to place *args at the end of the parameter list. |
| Parameters after *args | Must be supplied using keyword arguments or default values. |

---

# Introduction to Variable Scope

Until now, every variable we created existed inside a single program.

However,

in large applications,

variables may be created

- inside functions,
- outside functions,
- inside nested functions,
- inside classes.

Can every variable be accessed from everywhere?

No.

The accessibility of a variable depends on its Scope.

---

# What is Scope?

> Scope is the region of a program where a variable can be accessed.

Simply put,

Scope determines

- where a variable is visible,
- where it can be used,
- and where it becomes inaccessible.

---

# LEGB Rule (Introduction)

Python follows the LEGB Rule for variable lookup.

L

↓

Local

↓

E

↓

Enclosing

↓

G

↓

Global

↓

B

↓

Built-in

In this lecture,

only the first two scopes are introduced:

- Global Scope
- Local Scope

The remaining scopes are covered in later lectures.

---

# Global Variables

A variable declared outside every function is called a Global Variable.

These variables belong to the entire program.

They can be accessed both

- inside functions,
- and outside functions.

---

## Example
a = 10

def show():

    print("Inside Function:", a)

show()

print("Outside Function:", a)

### Output

Inside Function: 10

Outside Function: 10

---

## Memory Representation

Global Memory

↓

a = 10

↓

show()

↓

Reads Global Variable

↓

Program Ends

The function does not create another variable.

It simply reads the global variable.

---

# Advantages of Global Variables

- Can be accessed by multiple functions.
- Useful for constants and configuration values.
- Eliminates repeated declarations.

> Note: Excessive use of global variables is discouraged because it can make programs harder to understand and maintain.

---

# Interview Points

- *args accepts any number of positional arguments.
- Python stores *args as a tuple.
- Only one *args parameter is allowed in a function.
- Scope determines where variables are accessible.
- Global variables are declared outside functions.
- Global variables can be accessed inside and outside functions.

---

End of Part 3
==============================================================================================================================================================
# Local Variables

A variable that is created inside a function is known as a Local Variable.

Unlike global variables, local variables belong only to the function in which they are created.

They exist only while the function is executing.

Once the function finishes execution, the local variables are automatically destroyed from memory.

> Definition
>
> A variable declared inside a function or received as a function parameter is called a Local Variable.

---

# Characteristics of Local Variables

- Created when the function starts executing.
- Destroyed automatically when the function finishes.
- Accessible only inside that function.
- Cannot be accessed from outside the function.

---

# Example 1 – Local Variable

def show():

    local_var = 10

    print("Inside Function:", local_var)

show()

### Output

Inside Function: 10

---

# Explanation

The variable

local_var

is created only inside the function.

Execution Flow

show()

↓

local_var = 10

↓

Print 10

↓

Function Ends

↓

local_var Destroyed

---

# Example 2 – Trying to Access a Local Variable Outside the Function

def show():

    local_var = 10

    print("Inside Function:", local_var)

show()

print("Outside Function:", local_var)

### Output

Inside Function: 10

NameError:
name 'local_var' is not defined

---

# Why Does This Error Occur?

The variable

local_var

exists only while the function is executing.

After the function ends,

Python removes it from memory.

Therefore,

outside the function,

the variable simply does not exist.

---

# Memory Representation

During execution

Global Memory

↓

show()

↓

Local Memory

↓

local_var = 10

↓

Print

↓

Function Ends

↓

Local Memory Destroyed

---

# Lifetime of a Local Variable

A local variable has a very short lifetime.

Function Starts

↓

Variable Created

↓

Function Executes

↓

Function Ends

↓

Variable Destroyed

---

# Parameters are also Local Variables

Many beginners think only variables created inside the function body are local.

Actually,

function parameters are also local variables.

Example

def add(a, b):

    print(a)

    print(b)

add(10,20)

Here,

a

↓

Local Variable

b

↓

Local Variable

They exist only while the function is executing.

---

# Global Variable vs Local Variable

## Example

x = 100

def demo():

    y = 200

    print("Inside Function")

    print(x)

    print(y)

demo()

print("Outside Function")

print(x)

### Output

Inside Function

100

200

Outside Function

100

Notice

x

↓

Accessible Everywhere

y

↓

Accessible Only Inside demo()

---

# What Happens Here?

Global Variable

x

belongs to the entire program.

Local Variable

y

belongs only to

demo()

---

# Comparison
| Global Variable | Local Variable |
|-----------------|----------------|
| Declared outside functions | Declared inside functions |
| Accessible throughout the program | Accessible only inside the function |
| Lifetime is the entire program | Lifetime is only during function execution |
| Exists in global memory | Exists in local function memory |

---

# Scope Visualization

Global Scope

↓

a = 10

↓

Function show()

    ↓

    Local Scope

    b = 20

Outside the function

a

✓ Accessible

b

✗ Not Accessible

---

# Common Mistakes

## Mistake 1

Trying to access a local variable outside the function.

def demo():

    x = 10

demo()

print(x)

Output

NameError

---

## Mistake 2

Assuming parameters remain after function execution.

def add(a,b):

    print(a+b)

add(10,20)

print(a)

Output

NameError

Parameters disappear after the function finishes.

---

# Interview Questions

## Q1. What is the difference between a Global Variable and a Local Variable?

### Global Variable

- Declared outside functions.
- Accessible throughout the program.
- Exists until program termination.

### Local Variable

- Declared inside a function.
- Accessible only inside that function.
- Destroyed after function execution.

---

## Q2. Are function parameters local variables?

Yes.

Every function parameter is treated as a local variable.

---

## Q3. When is a local variable created?

When the function starts executing.

---

## Q4. When is a local variable destroyed?

Immediately after the function finishes execution.

---

# Lecture 20 Summary

In this lecture, we explored advanced concepts related to Python functions and variable scope.

We began by learning the rules for mixing Positional Arguments and Keyword Arguments, understanding that positional arguments must always appear before keyword arguments.

Next, we studied Default Arguments, which allow functions to use predefined values when arguments are omitted. We also learned the important rule that once a parameter has a default value, every parameter to its right must also have default values.

The lecture then explained why Python does not support Function Overloading. Since functions are objects and function names are simply references, redefining a function replaces the previous definition.

To overcome this limitation, Python provides Variable-Length Arguments (`*args`), which allow a function to accept any number of positional arguments. We learned that all these arguments are automatically packed into a tuple, making it easy to process an unknown number of inputs.

Finally, we were introduced to the concept of Variable Scope. We learned the difference between Global Variables, which are accessible throughout the program, and Local Variables, which exist only during the execution of a function. We also saw that function parameters are themselves local variables.

---

# Quick Revision

- Positional arguments must always come before keyword arguments.
- Default arguments provide optional parameter values.
- Required parameters cannot follow default parameters.
- Python does not support function overloading.
- *args allows functions to accept any number of positional arguments.
- *args is stored internally as a tuple.
- A function can have only one *args parameter.
- Scope determines where variables can be accessed.
- Global variables are declared outside functions.
- Local variables are declared inside functions.
- Function parameters are local variables.
- Local variables are created when the function starts and destroyed when it ends.

---

> Lecture 20 Completed ✅
===================================================================================================================================================================
