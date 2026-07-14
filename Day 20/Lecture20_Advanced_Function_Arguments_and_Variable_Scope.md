# Python Programming -- Lecture 20

## Advanced Function Arguments & Variable Scope

> **Topics Covered**
>
> -   Mixing Positional & Keyword Arguments
> -   Default Arguments
> -   Function Overloading in Python
> -   Variable-Length Arguments (`*args`)
> -   Variable Scope
> -   Global Variables
> -   Local Variables

------------------------------------------------------------------------

# Introduction

In the previous lecture, we learned about **Positional Arguments** and
**Keyword Arguments**. This lecture extends those concepts with advanced
function argument techniques, Python's approach to overloading,
variable-length arguments, and variable scope.

------------------------------------------------------------------------

# 1. Mixing Positional and Keyword Arguments

## Rule

**Positional arguments must always come before keyword arguments.**

### Correct

``` python
def grocery(item, price, company):
    print(item, price, company)

grocery("Sauce", price=200, company="Kissan")
```

### Incorrect

``` python
def grocery(item, price):
    print(item, price)

grocery(price=250, "Butter")
```

Output:

``` text
SyntaxError: positional argument follows keyword argument
```

Once keyword arguments begin, every remaining argument must also be a
keyword argument.

------------------------------------------------------------------------

# 2. Default Arguments

Default arguments allow parameters to have predefined values.

``` python
def greet(name, message="Good Morning"):
    print("Hello", name)
    print(message)
```

``` python
greet("Sachin")
```

Output

``` text
Hello Sachin
Good Morning
```

Override the default:

``` python
greet("Sachin", "Happy Diwali")
```

## Important Rule

A non-default parameter **cannot** appear after a default parameter.

❌ Incorrect

``` python
def demo(a=10, b):
    pass
```

✔ Correct

``` python
def demo(a, b=10):
    pass
```

## Skipping Default Arguments

``` python
def grocery(name="Coffee", price=350, company="Nestle"):
    print(name, price, company)

grocery(company="ITC")
```

Output

``` text
Coffee 350 ITC
```

## Class Example

``` python
import math

def calc_area(radius, pi=3.14):
    area = pi * math.pow(radius, 2)
    print("Area is:", area)

calc_area(4)
```

------------------------------------------------------------------------

# 3. Function Overloading in Python

Python **does not support function overloading**.

``` python
def add_number(a, b):
    return a + b

def add_number(a, b, c):
    return a + b + c

print(add_number(5, 7))
```

Output

``` text
TypeError: add_number() missing 1 required positional argument: 'c'
```

Reason:

-   Functions are objects.
-   Function names are references.
-   A later definition replaces the previous one.

------------------------------------------------------------------------

# 4. Variable-Length Arguments (`*args`)

`*args` allows a function to accept any number of positional arguments.

``` python
def add_number(*x):
    total = 0
    for value in x:
        total += value
    print(total)

add_number(5, 7)
add_number(5, 7, 9)
add_number(5, 7, 9, 11)
```

Python stores `*args` as a **tuple**.

## Largest String Example

``` python
def find_largest(*args):
    max_len = 0
    for s in args:
        if len(s) > max_len:
            max_len = len(s)
    return max_len

print(find_largest("Hi", "Welcome", "Hello"))
```

Output

``` text
7
```

## Rules

-   Only one `*args` parameter is allowed.
-   `*args` is usually placed last.
-   Parameters after `*args` must be supplied using keyword arguments.

------------------------------------------------------------------------

# 5. Variable Scope

Scope determines where a variable can be accessed.

Python follows the **LEGB** rule:

-   Local
-   Enclosing
-   Global
-   Built-in

This lecture introduces **Global** and **Local** scope.

------------------------------------------------------------------------

# Global Variables

Declared outside every function.

``` python
a = 10

def show():
    print(a)

show()
print(a)
```

Accessible inside and outside functions.

------------------------------------------------------------------------

# Local Variables

Declared inside a function.

``` python
def show():
    local_var = 10
    print(local_var)

show()
```

Trying to access it outside the function:

``` python
print(local_var)
```

Output

``` text
NameError
```

Function parameters are also local variables.

------------------------------------------------------------------------

# Global vs Local Variables

  Global Variable                 Local Variable
  ------------------------------- ---------------------------------
  Declared outside functions      Declared inside functions
  Accessible throughout program   Accessible only inside function
  Exists until program ends       Destroyed after function ends

------------------------------------------------------------------------

# Interview Points

-   Positional arguments must come before keyword arguments.
-   Required parameters cannot follow default parameters.
-   Python does not support function overloading.
-   `*args` stores arguments as a tuple.
-   Only one `*args` parameter is allowed.
-   Global variables are accessible throughout the program.
-   Local variables exist only during function execution.
-   Function parameters are local variables.

------------------------------------------------------------------------

# Quick Revision

-   Mixing positional and keyword arguments follows strict ordering
    rules.
-   Default arguments make parameters optional.
-   Python replaces earlier function definitions with later ones.
-   `*args` accepts unlimited positional arguments.
-   Scope controls variable accessibility.
-   Global variables are shared across functions.
-   Local variables disappear after function execution.

------------------------------------------------------------------------

> **Lecture 20 Completed ✅**
