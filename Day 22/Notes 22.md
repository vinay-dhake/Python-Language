# Python Programming 🐍
## Anonymous (Lambda) Functions & Introduction to `map()
> **Topic:** Anonymous (Lambda) Functions & `map()` Function

---

# Table of Contents

- Introduction
- What are Anonymous Functions?
- Why are they called Lambda Functions?
- Features of Lambda Functions
- Syntax of Lambda Functions
- Understanding Expressions
- What Can Be Written Inside a Lambda?
- Restrictions of Lambda Functions
- Creating Lambda Functions
- Why Lambda Functions are Needed
- Ways to Use Lambda Functions
- Lambda Examples
- Practical Exercises
- Introduction to `map()`
- Summary

---

# Introduction

Until now, we have been creating our own functions using the `def` keyword.

Example:

```python
def add(a, b):
    return a + b
```

This is known as a **named function** because the function has a name (`add`).

Python also provides another way to create functions **without giving them any name**.

These are called:

- Anonymous Functions
- Lambda Functions

This lecture introduces one of the most important Python concepts that is widely used in

- Data Science
- Machine Learning
- Automation
- Functional Programming

and later with built-in functions like

- `map()`
- `filter()`
- `reduce()`

---

# Today's Agenda

According to the lecture slides:

- User Defined Functions – IV
- Anonymous Functions (Lambda Functions)

This lecture mainly focuses on understanding **Lambda Functions**, their syntax, limitations, and practical applications before introducing the **`map()`** function.

---

# What are Anonymous Functions?

An **Anonymous Function** is simply a function **without a name**.

Normally, we create functions using the `def` keyword.

Example:

```python
def greet():
    print("Hello")
```

Here,

```text
greet
```

is the name of the function.

Instead of using `def`, Python allows us to create functions using the **`lambda`** keyword.

Example:

```python
lambda: print("Hello")
```

Notice that this function has **no name**.

Therefore,

- Normal Function → uses `def`
- Anonymous Function → uses `lambda`

Hence,

> **Anonymous Functions are also called Lambda Functions.**

---

# Why are they called Lambda Functions?

Python uses the keyword

```python
lambda
```

to create anonymous functions.

Therefore,

Anonymous Function = Lambda Function

Both terms mean exactly the same thing.

---

# Characteristics of Lambda Functions

A Lambda Function is

- Small
- Anonymous
- Usually written in one line
- Returns a value automatically
- Mostly used for short operations

Unlike normal functions, lambda functions are **not intended for writing long business logic**.

Instead, they are designed for **small one-line tasks**.

---

# Normal Function vs Lambda Function

| Normal Function | Lambda Function |
|----------------|-----------------|
| Uses `def` | Uses `lambda` |
| Has a name | No name |
| Multiple statements allowed | Only one expression |
| Uses `return` keyword | Returns automatically |
| Better for long programs | Better for short operations |
| Easy for complex logic | Easy for one-line logic |

---

# Why Do We Need Lambda Functions?

A common question is:

> **If we can already create functions using `def`, why do we need Lambda Functions?**

The answer is simple.

Suppose we only need a function **once**.

Creating an entire named function becomes unnecessary.

Example:

```python
def square(x):
    return x * x
```

If this function is used only one time,

writing all these lines becomes unnecessary.

Instead,

```python
lambda x: x * x
```

does exactly the same work in a single line.

This is the biggest advantage of lambda functions.

---

# Real-Life Analogy

Imagine you need a calculator only once to add two numbers.

Instead of purchasing a complete calculator,

you borrow one from a friend,

perform the addition,

and return it.

Similarly,

Lambda Functions are temporary, lightweight functions created for very small tasks.

---

# Key Points

- Lambda functions have no name.
- They are created using the `lambda` keyword.
===============================================================================================================================================================
# Syntax of Lambda Functions

After understanding **what Lambda Functions are** and **why they are used**, let's learn their syntax.

Unlike normal functions, Lambda Functions have a very compact syntax.

## Syntax

```python
lambda arguments : expression
```

General form:

```python
lambda parameter1, parameter2, ... : expression
```

### Components of Lambda Syntax

A Lambda Function consists of only **three parts**.

1. **`lambda` keyword**
2. **Arguments (Parameters)**
3. **Expression**

Example

```python
lambda a, b : a + b
```

Here,

- `lambda` → Keyword
- `a, b` → Parameters
- `a + b` → Expression

---

# Understanding the Syntax

Let's compare a normal function with a lambda function.

## Normal Function

```python
def add(a, b):
    return a + b
```

The same function using Lambda becomes

```python
lambda a, b: a + b
```

Notice how much shorter it is.

---

# Rule 1 — Lambda Must Start with `lambda`

Every Lambda Function must begin with the keyword

```python
lambda
```

Example

```python
lambda x: x*x
```

Without the keyword

```python
x:x*x
```

Python will generate a syntax error.

---

# Rule 2 — No Function Name

Unlike a normal function,

```python
def add():
```

Lambda Functions do **not** have names.

Normal Function

```python
def add(a,b):
    return a+b
```

Lambda Function

```python
lambda a,b:a+b
```

Notice

There is no function name like

```text
add
```

This is why Lambda Functions are called **Anonymous Functions**.

---

# Rule 3 — Arguments Do Not Use Parentheses

Normal Function

```python
def add(a,b):
```

Lambda Function

```python
lambda a,b:
```

There are **no parentheses** around the parameter list.

Correct

```python
lambda a,b:a+b
```

Incorrect

```python
lambda (a,b):a+b
```

---

# Rule 4 — Colon (`:`)

A colon separates the parameters from the expression.

General Syntax

```python
lambda arguments : expression
```

Example

```python
lambda x:x*x
```

Everything before the colon

↓

Arguments

Everything after the colon

↓

Expression

---

# Rule 5 — Only One Expression

This is the most important rule.

A Lambda Function can contain **only one expression**.

Correct

```python
lambda a,b:a+b
```

Incorrect

```python
lambda a,b:

x=a+b

return x
```

The above code is invalid because Lambda Functions do not support multiple statements.

---

# What is an Expression?

Many students confuse **statements** and **expressions**.

An **expression** is anything that produces a value.

Examples

```python
10+20
```

```python
x*x
```

```python
len(name)
```

```python
a>b
```

```python
"Even" if n%2==0 else "Odd"
```

All of these produce a value.

Hence,

they are valid expressions.

---

# Expression vs Statement

| Expression | Statement |
|------------|-----------|
| Produces a value | Performs an action |
| Can appear inside Lambda | Cannot appear inside Lambda (mostly) |

Examples of expressions

```python
a+b
```

```python
x*x
```

```python
len(s)
```

Examples of statements

```python
for
```

```python
while
```

```python
if
```

```python
return
```

```python
=
```

Statements generally cannot be used inside Lambda Functions.

---

# Rule 6 — No `return` Keyword

A normal function requires

```python
return
```

Example

```python
def square(x):
    return x*x
```

Lambda Functions automatically return the evaluated expression.

Therefore,

Correct

```python
lambda x:x*x
```

Incorrect

```python
lambda x:return x*x
```

Python automatically evaluates the expression after the colon and returns the result.

---

# Rule 7 — No Assignment Operator

Assignments are not allowed inside Lambda Functions.

Incorrect

```python
lambda x:y=x*x
```

Incorrect

```python
lambda x:x=10
```

Assignments are statements.

Lambda supports only expressions.

---

# Rule 8 — No Loops

Loops are statements.

Therefore,

they cannot be written inside Lambda Functions.

Incorrect

```python
lambda x:

for i in range(5):

print(i)
```

Similarly,

```python
while
```

is also not allowed.

---

# Rule 9 — Single-Line If-Else is Allowed

Although normal `if` statements are not allowed,

Python allows **conditional expressions**.

Example

```python
lambda n:"Even" if n%2==0 else "Odd"
```

This is a valid expression.

Hence,

it is perfectly valid inside a Lambda Function.

---

# Rule 10 — Function Calls are Allowed

Calling another function is perfectly valid.

Example

```python
lambda x:len(x)
```

Example

```python
lambda x:abs(x)
```

Example

```python
lambda x:print(x)
```

Since function calls return values,

they are expressions.

---

# Summary of Allowed Operations

The lecture explains that the following operations are allowed because they are expressions.

✅ Arithmetic Operations

```python
lambda x:x+5
```

```python
lambda x:x*x
```

---

✅ Relational Operations

```python
lambda x:x>10
```

---

✅ Logical Operations

```python
lambda x:x>5 and x<20
```

---

✅ String Operations

```python
lambda s:s.upper()
```

---

✅ Function Calls

```python
lambda s:len(s)
```

---

✅ Single-Line If-Else

```python
lambda n:"Even" if n%2==0 else "Odd"
```

---

# Summary of Restrictions

The following are **not allowed** inside a Lambda Function.

❌ Multiple statements

❌ Assignment (`=`)

❌ `for` loop

❌ `while` loop

❌ Normal `if` statement

❌ `return` keyword

❌ Multi-line function body

---

# Interview Questions

### Q1. What is the syntax of a Lambda Function?

```python
lambda arguments: expression
```

---

### Q2. Why is `return` not used inside Lambda Functions?

Because Python automatically returns the evaluated expression.

---

### Q3. Can a Lambda Function contain multiple statements?

**No.**

A Lambda Function can contain only one expression.

---

### Q4. Can we use loops inside Lambda Functions?

**No.**

`for` and `while` are statements.

---

### Q5. Can we use Single-Line If-Else?

**Yes.**

Because it is an expression.

---

# Key Takeaways

- Lambda Functions use the syntax `lambda arguments: expression`.
- They consist of a single expression.
- Parentheses are not used around parameters.
- The `return` keyword is not required.
- Assignment statements are not allowed.
- Loops are not allowed.
- Single-line conditional expressions are allowed.
- Lambda Functions automatically return the value of the expression.

---

> **End of Part 2**
==============================================================================================================================================================
# Creating Lambda Functions

Now that we understand the syntax and rules of Lambda Functions, let's create our first Lambda Function.

In this section, we will compare every Lambda Function with its equivalent **normal function** so that the difference becomes crystal clear.

---

# Example 1 – Addition of Three Numbers

The first classroom example was to create a function that adds three numbers.

## Using a Normal Function

```python
def add(a, b, c):
    x = a + b + c
    return x

result = add(2, 3, 4)
print(result)
```

### Output

```text
9
```

---

## Dry Run

Step 1

```python
add(2,3,4)
```

is called.

---

Step 2

The parameters receive

```text
a = 2
b = 3
c = 4
```

---

Step 3

```python
x = a+b+c
```

becomes

```text
x = 9
```

---

Step 4

```python
return x
```

returns

```text
9
```

---

Step 5

```python
print(result)
```

prints

```text
9
```

---

# The Same Example Using Lambda

```python
x = lambda a, b, c: a + b + c
```

Many beginners think this executes the function.

**It does NOT.**

This line **only creates a Lambda Function** and stores its reference inside the variable `x`.

---

## What is Stored in `x`?

The variable

```python
x
```

does **not** store the answer.

Instead,

it stores the **reference (memory address)** of the Lambda Function.

Think of it exactly like this:

```python
def add(a,b,c):
    return a+b+c
```

Here,

```python
add
```

stores the function's reference.

Similarly,

```python
x = lambda a,b,c:a+b+c
```

stores the lambda function's reference.

---

# Calling the Lambda Function

Just like a normal function,

we call the Lambda Function using parentheses.

```python
x = lambda a, b, c: a + b + c

result = x(2, 3, 4)

print(result)
```

### Output

```text
9
```

---

## Dry Run

Initially

```python
x = lambda a,b,c:a+b+c
```

creates the function.

No calculation happens.

---

Later

```python
x(2,3,4)
```

executes the function.

Parameters become

```text
a = 2
b = 3
c = 4
```

Expression

```python
a+b+c
```

becomes

```text
9
```

Python automatically returns

```text
9
```

without writing the `return` keyword.

---

# Memory Representation

```
Variable

↓

x

↓

Lambda Function

↓

lambda a,b,c:a+b+c
```

The function executes **only** when

```python
x(...)
```

is called.

---

# Defining and Calling in One Line

The instructor also demonstrated another style where the Lambda Function is defined **and immediately executed**.

```python
print((lambda a, b, c: a + b + c)(2, 3, 4))
```

### Output

```text
9
```

---

## How Does This Work?

Let's divide the statement.

First,

```python
lambda a,b,c:a+b+c
```

creates the anonymous function.

Immediately after that,

```python
(2,3,4)
```

calls it.

Equivalent to

```python
def add(a,b,c):
    return a+b+c

print(add(2,3,4))
```

Everything happens in one line.

---

# Example 2 – Lambda Without Arguments

Many beginners think Lambda Functions must always have parameters.

This is incorrect.

A Lambda Function can also have **zero arguments**.

Example

```python
import math

x = lambda: math.pi

print(x())
```

### Output

```text
3.141592653589793
```

---

## Explanation

Notice carefully.

There are **no parameters**.

```python
lambda:
```

is perfectly valid.

The expression

```python
math.pi
```

is evaluated.

Its value is automatically returned.

---

# Dry Run

Step 1

```python
lambda: math.pi
```

creates the function.

---

Step 2

```python
x()
```

calls the function.

---

Step 3

Expression

```python
math.pi
```

is evaluated.

---

Step 4

Python automatically returns

```text
3.141592653589793
```

---

# Why No `return`?

Normal Function

```python
def get_pi():
    return math.pi
```

Lambda

```python
lambda: math.pi
```

Python automatically returns the value of the expression.

---

# Comparison – Normal Function vs Lambda

## Normal Function

```python
def add(a,b,c):
    x=a+b+c
    return x
```

---

## Lambda Function

```python
lambda a,b,c:a+b+c
```

---

## Normal Function

```python
def get_pi():
    return math.pi
```

---

## Lambda Function

```python
lambda:math.pi
```

---

# Advantages Seen So Far

Compared to normal functions,

Lambda Functions

- require less code
- are easier to write
- are useful for one-time operations
- automatically return the result
- eliminate unnecessary function definitions

---

# Interview Questions

### Q1. Does defining a Lambda Function execute it?

**No.**

It only creates the function object.

---

### Q2. What does the variable store?

It stores the **reference (memory address)** of the Lambda Function.

---

### Q3. Can a Lambda Function have zero parameters?

**Yes.**

Example

```python
lambda: math.pi
```

---

### Q4. Can a Lambda Function be called immediately after creation?

**Yes.**

Example

```python
(lambda a,b:a+b)(2,3)
```

---

# Key Takeaways

- A Lambda Function is created using the `lambda` keyword.
- Creating a Lambda Function does not execute it.
- The variable stores the function's reference.
- Lambda Functions are called exactly like normal functions.
- A Lambda Function can have zero or more parameters.
- Lambda Functions can be defined and executed in a single statement.
- Python automatically returns the result of the expression.

---

# Next Topic

In the next section, we'll solve all the practical classroom exercises:

- Return the first character of a string
- Return the last character of a string
- Check whether a number is even
- Return "Even" or "Odd"
- Find the maximum of two numbers using Lambda Functions

These are the exact examples demonstrated during the lecture.

> **End of Part 3**
==============================================================================================================================================================
# Practical Exercises Using Lambda Functions

After learning the syntax of Lambda Functions, the instructor solved several practical examples in class.

These examples demonstrate how Lambda Functions can replace small, simple functions written using the `def` keyword.

---

# Exercise 1 – Return the First Character of a String

## Using a Normal Function

```python
def first_char(string):
    return string[0]

print(first_char("Bhopal"))
print(first_char("Sachin"))
```

### Output

```text
B
S
```

---

## Using Lambda Function

```python
first_char = lambda string: string[0]

print(first_char("Bhopal"))
print(first_char("Sachin"))
```

### Output

```text
B
S
```

---

## Dry Run

For

```python
first_char("Bhopal")
```

Parameter

```text
string = "Bhopal"
```

Expression

```python
string[0]
```

becomes

```python
"Bhopal"[0]
```

Result

```text
B
```

Python automatically returns

```text
B
```

---

# Exercise 2 – Return the Last Character of a String

Instead of positive indexing,

the instructor used **negative indexing**.

Remember,

Python allows indexing from the end.

```
B h o p a l
0 1 2 3 4 5

-6 -5 -4 -3 -2 -1
```

Therefore,

```python
string[-1]
```

always returns the last character.

---

## Using Lambda Function

```python
last_char = lambda string: string[-1]

print(last_char("Bhopal"))
print(last_char("Sachin"))
```

### Output

```text
l
n
```

---

## Dry Run

```python
last_char("Sachin")
```

Parameter

```text
string = "Sachin"
```

Expression

```python
string[-1]
```

becomes

```python
"Sachin"[-1]
```

Result

```text
n
```

---

# Exercise 3 – Check Whether a Number is Even

The next classroom example was checking whether a number is even.

Instead of returning the words

```text
Even
```

or

```text
Odd
```

the function returns a Boolean value.

---

## Lambda Function

```python
is_even = lambda n: n % 2 == 0

print(is_even(7))
print(is_even(10))
```

### Output

```text
False
True
```

---

## Explanation

For

```python
is_even(7)
```

Expression

```python
7 % 2 == 0
```

becomes

```python
1 == 0
```

Result

```text
False
```

---

For

```python
is_even(10)
```

Expression

```python
10 % 2 == 0
```

becomes

```python
0 == 0
```

Result

```text
True
```

---

# Why Does It Return True or False?

The expression

```python
n % 2 == 0
```

is a **relational expression**.

Relational expressions always produce

- True
- False

Therefore,

Python automatically returns the Boolean value.

---

# Exercise 4 – Return "Even" or "Odd"

The previous example returned only

```text
True
```

or

```text
False
```

Now the instructor wanted the Lambda Function to return

```text
Even
```

or

```text
Odd
```

using **Single-Line If-Else**.

---

## Lambda Function

```python
check_even_odd = lambda n: "Even" if n % 2 == 0 else "Odd"

print(check_even_odd(7))
print(check_even_odd(10))
```

### Output

```text
Odd
Even
```

---

## Dry Run

### Input

```python
check_even_odd(7)
```

Expression

```python
"Even" if 7 % 2 == 0 else "Odd"
```

becomes

```python
"Even" if False else "Odd"
```

Result

```text
Odd
```

---

### Input

```python
check_even_odd(10)
```

Expression

```python
"Even" if 10 % 2 == 0 else "Odd"
```

becomes

```python
"Even" if True else "Odd"
```

Result

```text
Even
```

---

# Why Does This Work?

Earlier we learned that Lambda Functions cannot contain normal

```python
if
```

statements.

However,

they **can contain conditional expressions**.

Syntax

```python
value_if_true if condition else value_if_false
```

This entire statement is considered a **single expression**.

Therefore,

it is valid inside Lambda Functions.

---

# Exercise 5 – Find Maximum of Two Numbers

The final classroom exercise was finding the larger of two numbers.

---

## Normal Function

```python
def maximum(a, b):

    if a > b:
        return a
    else:
        return b
```

---

## Lambda Function

```python
max_num = lambda a, b: a if a > b else b

print(max_num(3, 4))
print(max_num(9, 5))
```

### Output

```text
4
9
```

---

## Dry Run

### Input

```python
max_num(3,4)
```

Expression

```python
3 if 3 > 4 else 4
```

Condition

```python
3 > 4
```

Result

```text
False
```

Therefore,

```text
4
```

is returned.

---

### Input

```python
max_num(9,5)
```

Expression

```python
9 if 9 > 5 else 5
```

Condition

```python
9 > 5
```

Result

```text
True
```

Therefore,

```text
9
```

is returned.

---

# Summary of Classroom Exercises

| Problem | Lambda Function |
|----------|-----------------|
| First Character | `lambda s: s[0]` |
| Last Character | `lambda s: s[-1]` |
| Even Check | `lambda n: n % 2 == 0` |
| Even/Odd | `lambda n: "Even" if n % 2 == 0 else "Odd"` |
| Maximum | `lambda a, b: a if a > b else b` |

---

# Common Mistakes

## Mistake 1

```python
lambda s:s(0)
```

Incorrect.

Correct

```python
lambda s:s[0]
```

because strings use indexing.

---

## Mistake 2

Using normal `if` statements.

Incorrect

```python
lambda n:

if n%2==0:

return "Even"
```

Correct

```python
lambda n:"Even" if n%2==0 else "Odd"
```

---

## Mistake 3

Forgetting negative indexing.

```python
string[-1]
```

returns the last character.

---

# Interview Questions

### Q1. How do you return the first character using Lambda?

```python
lambda s:s[0]
```

---

### Q2. How do you return the last character?

```python
lambda s:s[-1]
```

---

### Q3. How do you check whether a number is even?

```python
lambda n:n%2==0
```

---

### Q4. Can Single-Line If-Else be used inside Lambda Functions?

**Yes.**

---

### Q5. How do you return the maximum of two numbers?

```python
lambda a,b:a if a>b else b
```

---

# Key Takeaways

- Lambda Functions can work with strings.
- Lambda Functions can return Boolean values.
- Single-Line If-Else is extremely useful inside Lambda Functions.
- Negative indexing can easily return the last character.
- Small utility functions are best written using Lambda Functions.

---

# Next Topic

In the next section, we'll learn the **most important application of Lambda Functions**:

# `map()` Function

This is where Lambda Functions become truly powerful and useful in real-world Python programming.

> **End of Part 4**
=============================================================================================================================================================
# The `map()` Function

So far, we have learned how to create **Lambda Functions**.

Now comes the most important part of this lecture.

The instructor explained that **the real power of Lambda Functions is realized when they are used with higher-order functions such as `map()` and `filter()`.**

In fact, one of the primary reasons Lambda Functions exist is to make working with these higher-order functions simple and elegant.

---

# Why Do We Need `map()`?

Suppose we have a list of numbers.

```python
numbers = [2, 3, 6, 8, 4]
```

Now suppose we want to calculate the **square of every element**.

One approach is to use a loop.

Another approach is to use the built-in **`map()`** function.

The second approach is shorter, cleaner, and more "Pythonic".

---

# What is the `map()` Function?

`map()` is a built-in Python function.

It applies a given function to **every element** of an iterable (such as a list, tuple, or string) and returns a new **map object**.

---

## Definition

> The `map()` function takes two arguments:
>
> 1. A function
> 2. An iterable
>
> It applies the function to every element of the iterable and returns the results.

---

# Syntax

```python
map(function, iterable)
```

General Syntax

```python
map(function_name, collection)
```

where

- **function** → Function to apply
- **iterable** → List, Tuple, String, etc.

---

# Parameters of `map()`

## First Parameter

The first parameter is a **function**.

Example

```python
square
```

Notice

We write

```python
square
```

NOT

```python
square()
```

---

### Why?

Because

```python
square
```

represents the **function object (reference)**.

Whereas

```python
square()
```

means

> Execute the function immediately.

But `map()` itself is responsible for calling the function.

Therefore,

Correct

```python
map(square, numbers)
```

Incorrect

```python
map(square(), numbers)
```

---

## Second Parameter

The second parameter must be an **iterable**.

Examples

```python
list
```

```python
tuple
```

```python
string
```

```python
range
```

---

# How Does `map()` Work?

Suppose we have

```python
numbers = [2,3,6,8,4]
```

and

```python
square(x)
```

The execution becomes

```text
2

↓

square(2)

↓

4

------------------

3

↓

square(3)

↓

9

------------------

6

↓

square(6)

↓

36

------------------

8

↓

square(8)

↓

64

------------------

4

↓

square(4)

↓

16
```

Finally,

Python combines all returned values into a **map object**.

---

# Example 1 – Traditional Approach (Using `for` Loop)

Before learning `map()`, let's solve the problem using a loop.

```python
def square(n):
    return n * n

numbers = [2, 3, 6, 8, 4]

for x in numbers:
    print(square(x))
```

### Output

```text
4
9
36
64
16
```

---

## Dry Run

Initially,

```python
numbers = [2,3,6,8,4]
```

Loop starts.

Iteration 1

```text
x = 2
```

```
square(2)

↓

4
```

Iteration 2

```
square(3)

↓

9
```

Iteration 3

```
square(6)

↓

36
```

Iteration 4

```
square(8)

↓

64
```

Iteration 5

```
square(4)

↓

16
```

---

# Problem with This Approach

Although it works,

we still have

- a function
- a loop
- repeated function calls

Python provides a much shorter solution.

---

# Example 2 – Using `map()` with a Normal Function

```python
def square(n):
    return n * n

numbers = [2, 3, 6, 8, 4]

result = map(square, numbers)

print(list(result))
```

### Output

```text
[4, 9, 36, 64, 16]
```

---

# Why `list()`?

This is an important point discussed in class.

The `map()` function **does not return a list**.

It returns a **map object**.

If we print it directly,

```python
print(result)
```

Output

```text
<map object at 0x...>
```

To actually see the values,

we convert it into a list.

```python
list(result)
```

Now Python displays

```text
[4,9,36,64,16]
```

---

# What Happens Internally?

Execution

```python
map(square, numbers)
```

becomes

```text
square(2)

↓

4

square(3)

↓

9

square(6)

↓

36

square(8)

↓

64

square(4)

↓

16
```

Then Python creates

```text
Map Object

↓

Convert to List

↓

[4,9,36,64,16]
```

---

# Important Note

Notice carefully.

We passed

```python
square
```

NOT

```python
square()
```

because `map()` needs the function itself,

not the result of calling it.

---

# Example 3 – Using `map()` with a Lambda Function

Now comes the most important application of Lambda Functions.

Instead of writing

```python
def square(n):
    return n*n
```

we can directly write

```python
numbers = [2, 3, 6, 8, 4]

result = list(map(lambda x: x * x, numbers))

print(result)
```

### Output

```text
[4, 9, 36, 64, 16]
```

---

# Dry Run

Initially,

```python
numbers = [2,3,6,8,4]
```

Lambda Function

```python
lambda x:x*x
```

is passed to

```python
map()
```

Execution

```text
2

↓

2×2

↓

4

------------

3

↓

3×3

↓

9

------------

6

↓

6×6

↓

36

------------

8

↓

8×8

↓

64

------------

4

↓

4×4

↓

16
```

Python creates

```text
Map Object

↓

Convert to List

↓

[4,9,36,64,16]
```

---

# Why is Lambda Better Here?

Without Lambda

```python
def square(n):
    return n*n

result = map(square, numbers)
```

With Lambda

```python
result = map(lambda x:x*x, numbers)
```

No separate function is required.

The code becomes shorter and cleaner.

---

# One-Line Version

The instructor also demonstrated the shortest possible solution.

```python
print(list(map(lambda x: x * x, [2, 3, 6, 8, 4])))
```

### Output

```text
[4, 9, 36, 64, 16]
```

Everything happens in a single statement.

---

# Comparison

## Using `for` Loop

```python
for x in numbers:
    print(square(x))
```

---

## Using `map()`

```python
list(map(square, numbers))
```

---

## Using `map()` + Lambda

```python
list(map(lambda x:x*x, numbers))
```

This is the cleanest approach.

---

# Advantages of `map()`

- Less code
- More readable
- No explicit loop
- Faster to write
- Commonly used in Python libraries
- Works beautifully with Lambda Functions

---

# Interview Questions

### Q1. What does `map()` return?

A **map object**.

---

### Q2. How do we display the results?

Convert it into a list.

```python
list(map(...))
```

---

### Q3. Why do we pass `square` instead of `square()`?

Because `square` is the function object.

`square()` executes the function immediately.

---

### Q4. Can `map()` be used with Lambda Functions?

**Yes.**

This is one of the primary uses of Lambda Functions.

---

# Key Takeaways

- `map()` applies a function to every element of an iterable.
- It returns a **map object**.
- Use `list()` to display the mapped values.
- Pass the **function name**, not the function call.
- Lambda Functions make `map()` code shorter and cleaner.
- `map()` is one of the most common real-world applications of Lambda Functions.

---

> **End of Part 5**
==============================================================================================================================================================
# Complete Lecture Summary

In this lecture, we explored one of Python's most powerful functional programming features — **Anonymous Functions**, commonly known as **Lambda Functions**, along with their most common application using the **`map()`** function.

Unlike traditional functions created using the `def` keyword, Lambda Functions allow us to create **small, anonymous, one-line functions** without explicitly defining a function name. They are especially useful when a function is required only once or for a very short duration.

---

# What We Learned

## 1. Anonymous (Lambda) Functions

A Lambda Function is simply a function without a name.

Instead of using

```python
def
```

we use

```python
lambda
```

General Syntax

```python
lambda arguments: expression
```

Example

```python
lambda a, b: a + b
```

---

## 2. Characteristics of Lambda Functions

- Anonymous (No Function Name)
- Defined using the `lambda` keyword
- Usually written in one line
- Automatically returns the result
- Can contain only one expression
- Mostly used for small tasks

---

## 3. Restrictions of Lambda Functions

A Lambda Function **cannot contain**

- Multiple statements
- `return`
- Assignment (`=`)
- `for` loop
- `while` loop
- Multi-line function body

A Lambda Function **can contain**

- Arithmetic expressions
- Relational expressions
- Logical expressions
- Function calls
- String operations
- Single-Line If-Else expressions

---

## 4. Lambda Function Examples

### Addition of Three Numbers

```python
add = lambda a, b, c: a + b + c

print(add(2, 3, 4))
```

Output

```text
9
```

---

### Lambda Without Arguments

```python
import math

pi_value = lambda: math.pi

print(pi_value())
```

Output

```text
3.141592653589793
```

---

### First Character of a String

```python
first_char = lambda string: string[0]

print(first_char("Bhopal"))
```

Output

```text
B
```

---

### Last Character of a String

```python
last_char = lambda string: string[-1]

print(last_char("Python"))
```

Output

```text
n
```

---

### Even Number Check

```python
is_even = lambda n: n % 2 == 0

print(is_even(10))
```

Output

```text
True
```

---

### Even or Odd

```python
check = lambda n: "Even" if n % 2 == 0 else "Odd"

print(check(7))
```

Output

```text
Odd
```

---

### Maximum of Two Numbers

```python
maximum = lambda a, b: a if a > b else b

print(maximum(10, 15))
```

Output

```text
15
```

---

# The `map()` Function

After understanding Lambda Functions, we learned the **`map()`** function.

The `map()` function applies a given function to every element of an iterable and returns a **map object**.

General Syntax

```python
map(function, iterable)
```

Example

```python
numbers = [2, 3, 6, 8, 4]

result = map(lambda x: x * x, numbers)

print(list(result))
```

Output

```text
[4, 9, 36, 64, 16]
```

---

# How `map()` Works

Suppose

```python
numbers = [2, 3, 6]
```

Execution Flow

```text
2
↓
lambda
↓
4

3
↓
lambda
↓
9

6
↓
lambda
↓
36
```

Final Result

```text
[4, 9, 36]
```

---

# Why `list()` is Required

The `map()` function does **not** return a list.

It returns a **map object**.

```python
result = map(lambda x: x*x, numbers)

print(result)
```

Output

```text
<map object at 0x...>
```

To display the actual values,

convert the map object into a list.

```python
print(list(result))
```

---

# Traditional Approach vs `map()`

### Traditional Method

```python
def square(n):
    return n * n

numbers = [2, 3, 6, 8, 4]

for num in numbers:
    print(square(num))
```

---

### Using `map()`

```python
def square(n):
    return n * n

numbers = [2, 3, 6, 8, 4]

result = list(map(square, numbers))

print(result)
```

---

### Using `map()` + Lambda

```python
numbers = [2, 3, 6, 8, 4]

result = list(map(lambda x: x * x, numbers))

print(result)
```

This is the shortest and most Pythonic solution.

---

# Why Lambda Functions are Popular

Lambda Functions are widely used because they

- reduce code size
- improve readability for simple operations
- eliminate unnecessary function definitions
- integrate perfectly with higher-order functions like `map()`
- are heavily used in Data Science and Machine Learning libraries

---

# Interview Questions

### Q1. What is a Lambda Function?

A Lambda Function is an anonymous function created using the `lambda` keyword.

---

### Q2. Can a Lambda Function contain multiple statements?

No.

It can contain only one expression.

---

### Q3. Is the `return` keyword used in Lambda Functions?

No.

The expression is returned automatically.

---

### Q4. Can loops be written inside Lambda Functions?

No.

`for` and `while` are statements and are not allowed.

---

### Q5. Can Single-Line If-Else be used?

Yes.

Because it is an expression.

---

### Q6. What does the `map()` function return?

A **map object**.

---

### Q7. Why do we use `list()` with `map()`?

To convert the map object into a list so that the values can be displayed.

---

### Q8. What should be passed as the first argument to `map()`?

The **function itself**, not the function call.

Correct

```python
map(square, numbers)
```

Incorrect

```python
map(square(), numbers)
```

---

# Quick Revision

- Lambda Functions are anonymous functions.
- They are created using the `lambda` keyword.
- Lambda Functions contain only one expression.
- They automatically return the expression's value.
- Assignment, loops, and multiple statements are not allowed.
- Single-Line If-Else expressions are allowed.
- `map()` applies a function to every element of an iterable.
- `map()` returns a map object.
- Convert the map object into a list using `list()`.
- Lambda Functions are commonly used with `map()` because they avoid creating unnecessary named functions.

---

# Key Takeaway

> **Use a normal function (`def`) when the logic is large or reused multiple times.**
>
> **Use a Lambda Function when the logic is small, simple, and needed only temporarily—especially with functions like `map()`.**

---

# What's Next?

In the next lecture, you'll continue functional programming concepts by exploring additional higher-order functions such as **`filter()`** (and possibly `reduce()`, depending on the course sequence), where Lambda Functions become even more useful.

---


- They are mostly written in one line.
- They automatically return the result.
- They are widely used with `map()`, `filter()`, and other higher-order functions.
