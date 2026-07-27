```md id="lecture27-part1"
# Lecture 27 - Part 1

# Tuples in Python (Introduction)

## What is a Tuple?

A **Tuple** is an **ordered** and **immutable** collection of elements in Python.

- **Ordered** means the elements are stored in a fixed sequence.
- **Immutable** means once a tuple is created, its elements **cannot be changed**.
- A tuple can store **duplicate values**.
- A tuple can store **different data types** (heterogeneous data).

Unlike a list, a tuple does **not** allow operations such as:
- Adding new elements
- Removing existing elements
- Modifying existing elements

Once created, its contents remain fixed.

---

## Definition

> **Tuple:** An ordered, immutable collection of elements.

---

## Example

```python
numbers = (10, 20, 30, 40)
print(numbers)
```

**Output**

```text
(10, 20, 30, 40)
```

Here,

- `10` is stored at index `0`
- `20` is stored at index `1`
- `30` is stored at index `2`
- `40` is stored at index `3`

The order never changes unless an entirely new tuple is created.

---

# Tuple Representation

Tuples are written using **round brackets `()`**.

## Example

```python
numbers = (10, 20, 30, 40)
print(numbers)
```

Output

```text
(10, 20, 30, 40)
```

---

# Tuple with Different Data Types

A tuple can store values of different data types together.

Example:

```python
student = ("Rahul", 21, "CSE")
print(student)
```

Output

```text
('Rahul', 21, 'CSE')
```

Here,

| Element | Data Type |
|---------|-----------|
| Rahul | String |
| 21 | Integer |
| CSE | String |

This ability is called **heterogeneous storage**.

---

# Key Properties of Tuple

## 1. Ordered

Elements are stored in a fixed order.

```python
t = (10, 20, 30)
```

Memory Representation

```text
Index : 0    1    2
        ↓    ↓    ↓
      +----+----+----+
      |10  |20  |30  |
      +----+----+----+
```

Python always remembers the order.

---

## 2. Immutable

After creation, elements cannot be modified.

```python
t = (10, 20, 30)

# Not Allowed
# t[0] = 100
```

Output

```text
TypeError:
'tuple' object does not support item assignment
```

Unlike lists, tuples do not support:

- append()
- extend()
- insert()
- remove()
- pop()
- clear()

because these operations change the contents of the collection.

---

## 3. Allows Duplicate Values

Duplicate values are perfectly valid.

```python
numbers = (10, 20, 10, 30, 10)

print(numbers)
```

Output

```text
(10, 20, 10, 30, 10)
```

There is no restriction that every element must be unique.

---

## 4. Heterogeneous Collection

Different data types can exist together.

```python
data = (
    10,
    "Python",
    True,
    25.6
)

print(data)
```

Output

```text
(10, 'Python', True, 25.6)
```

A tuple may contain

- Integer
- Float
- String
- Boolean
- List
- Dictionary
- Another Tuple
- Any Python object

---

# Tuple vs List

| Feature | Tuple | List |
|----------|-------|------|
| Syntax | `( )` | `[ ]` |
| Mutable | ❌ No | ✅ Yes |
| Can add/remove elements | ❌ No | ✅ Yes |
| Performance | Faster | Slightly slower |
| Memory Usage | Less | More |
| Typical Use | Fixed data | Changing data |

---

# Why are Tuples Faster?

Lists are designed to support operations like

- append()
- insert()
- remove()
- pop()

To support these operations, Python reserves extra memory and performs additional bookkeeping.

Tuples never change after creation.

Therefore,

- Less memory is required.
- Fewer internal checks are performed.
- Access is slightly faster.

---

# When Should We Use Tuples?

Use tuples when the data should remain constant.

Examples:

### Days of Week

```python
days = (
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday",
    "Sunday"
)
```

---

### Coordinates

```python
point = (15, 28)
```

---

### RGB Color

```python
color = (255, 120, 60)
```

---

### Student Record

```python
student = (
    "Rahul",
    21,
    "CSE"
)
```

If the information should not accidentally change, tuples are a better choice than lists.

---

# Advantages of Tuples

✅ Faster than lists

✅ Uses less memory

✅ Protects data from accidental modification

✅ Excellent for storing constant values

✅ Can be used as dictionary keys (if all elements are hashable)

---

# Real-Life Analogy

Imagine your **Date of Birth**.

```
12 / 05 / 2004
```

Your date of birth never changes.

It is fixed.

A tuple is ideal for storing such fixed information.

On the other hand, a shopping cart changes continuously.

```
Add Item
Remove Item
Update Quantity
```

For such data, a **list** is a better choice.

---

# Interview Questions

### Q1. Why is a tuple called immutable?

Because after creation, its elements cannot be modified, inserted, or deleted.

---

### Q2. Can tuples contain duplicate values?

Yes.

```python
t = (1, 2, 1, 3)
```

is perfectly valid.

---

### Q3. Can tuples store different data types?

Yes.

```python
t = (10, "Python", True, 5.5)
```

---

### Q4. Which consumes less memory?

**Tuple**

---

### Q5. Which is faster?

**Tuple**

---

# Key Takeaways

- Tuple is an ordered collection.
- Tuple is immutable.
- Duplicate values are allowed.
- Different data types can be stored together.
- Tuples use round brackets `()`.
- Tuples are faster and consume less memory than lists.
- Use tuples whenever the data should remain fixed.
```
==============================================================================================================================================================

# Lecture 27 - Part 2

# Creating Tuples and the Single-Element Tuple Trap

## Table of Contents

- Creating Tuples
- Empty Tuple
- Tuple with Multiple Elements
- Heterogeneous Tuple
- How Python Identifies a Tuple
- The Single-Element Tuple Trap
- Why `(10)` is Not a Tuple
- The Importance of the Trailing Comma
- Tuple Without Parentheses
- Memory Diagram
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Creating Tuples

A tuple is created by separating values using **commas**.

Although tuples are commonly written inside **round brackets `()`**, the **comma (` , `)** is what actually tells Python to create a tuple.

General Syntax

```python
tuple_name = (value1, value2, value3)
```

Example

```python
numbers = (10, 20, 30)

print(numbers)
```

Output

```text
(10, 20, 30)
```

---

# Empty Tuple

An empty tuple contains no elements.

```python
t1 = ()

print(t1)

print(type(t1))
```

Output

```text
()

<class 'tuple'>
```

This is useful when you need an immutable collection that initially contains no values.

---

# Tuple with Multiple Elements

A tuple may contain any number of elements.

Example

```python
numbers = (10, 20, 30, 40, 50)

print(numbers)
```

Output

```text
(10, 20, 30, 40, 50)
```

Python stores every element in the same order.

---

# Heterogeneous Tuple

Tuples can store different types of data together.

Example

```python
data = ("Python", 100, 3.14)

print(data)
```

Output

```text
('Python', 100, 3.14)
```

Here,

| Value | Data Type |
|--------|-----------|
| Python | String |
| 100 | Integer |
| 3.14 | Float |

This example is discussed in the lecture to demonstrate that tuples are **heterogeneous collections**. :contentReference[oaicite:0]{index=0}

---

# How Does Python Know It Is a Tuple?

Many beginners believe that **parentheses create a tuple**.

Actually,

**the comma creates the tuple.**

For example,

```python
numbers = (10, 20, 30)
```

Python sees

```text
10,

20,

30
```

The commas indicate that multiple values belong to one tuple.

The parentheses simply improve readability.

---

# The Single-Element Tuple Trap ⭐

This is one of the most important concepts in the lecture.

Suppose you write

```python
a = (10)
```

Many beginners think this creates a tuple.

It **does not**.

---

# Example

```python
a = (10)

print(type(a))
```

Output

```text
<class 'int'>
```

Why?

Because Python interprets

```python
(10)
```

as a **grouped expression**, just like

```python
(5 + 3)
```

The parentheses are treated only as grouping symbols.

No tuple is created.

---

# Creating a Single-Element Tuple

To create a tuple containing exactly one element,

a **trailing comma** is mandatory.

Example

```python
b = (10,)

print(type(b))
```

Output

```text
<class 'tuple'>
```

Notice the comma

```python
(10,)
```

Without the comma,

Python creates an integer.

With the comma,

Python creates a tuple.

This is one of the most frequently asked Python interview questions. :contentReference[oaicite:1]{index=1}

---

# Why is the Comma Required?

Consider these two statements.

### Example 1

```python
a = (10)
```

Python interprets this as

```python
a = 10
```

Result

```text
<class 'int'>
```

---

### Example 2

```python
a = (10,)
```

Python now sees

```text
One value,

followed by a comma.
```

The comma tells Python,

> "This is a tuple."

Result

```text
<class 'tuple'>
```

---

# Memory Representation

### Integer

```python
a = (10)
```

Memory

```text
a
│
▼
10
```

---

### Tuple

```python
b = (10,)
```

Memory

```text
b
│
▼
+------+
| 10   |
+------+
```

Even though both contain the value `10`, they are completely different objects.

---

# Tuple Without Parentheses

Another interesting feature explained in the lecture is that **parentheses are optional**.

Example

```python
c = 10, 20, 30

print(c)

print(type(c))
```

Output

```text
(10, 20, 30)

<class 'tuple'>
```

Python automatically creates a tuple because of the commas.

---

# Another Example

```python
colors = "Red", "Green", "Blue"

print(colors)
```

Output

```text
('Red', 'Green', 'Blue')
```

Even without parentheses,

Python creates a tuple.

---

# Which Style Should We Use?

Although parentheses are optional,

the recommended style is

```python
colors = ("Red", "Green", "Blue")
```

because

- it is easier to read,
- it improves code clarity,
- it avoids confusion.

---

# Important Rule

Remember this statement:

> **Tuples are defined by commas, not by parentheses.**

This single sentence explains why

```python
(10)
```

is **not** a tuple,

while

```python
10,
```

**is** a tuple.

---

# Common Mistakes

## Mistake 1

```python
a = (10)
```

Expecting a tuple.

Actual result

```text
Integer
```

---

## Mistake 2

Forgetting the comma.

Incorrect

```python
single = ("Python")
```

Correct

```python
single = ("Python",)
```

---

## Mistake 3

Thinking parentheses always create tuples.

Remember,

the comma creates the tuple.

---

## Mistake 4

Writing

```python
a = ,
```

This is invalid syntax.

At least one value is required before the comma.

---

# Interview Questions

### Q1. Which symbol actually creates a tuple?

**Answer:**

The **comma (` , `)** creates a tuple.

---

### Q2. What is the output?

```python
a = (10)

print(type(a))
```

Output

```text
<class 'int'>
```

---

### Q3. What is the output?

```python
a = (10,)

print(type(a))
```

Output

```text
<class 'tuple'>
```

---

### Q4. Is this valid?

```python
a = 10, 20, 30
```

Yes.

Python automatically creates a tuple.

---

### Q5. Which is the preferred style?

```python
(10, 20, 30)
```

Using parentheses improves readability, even though they are optional.

---

# Key Takeaways

- Tuples are usually written using parentheses.
- The **comma** is what actually creates a tuple.
- `(10)` is an integer, **not** a tuple.
- `(10,)` is a single-element tuple.
- Parentheses are optional when creating tuples.
- Always use parentheses for better readability.

---

# End of Part 2

➡️ **Next Part:** Tuple Packing, Tuple Unpacking, Variable Swapping, Returning Multiple Values from Functions, and the `*` (star) operator with detailed dry runs, memory diagrams, and all classroom examples.
========================================================================================================================================================================================================================
```md id="lecture27-part3"
# Lecture 27 - Part 3

# Tuple Packing and Unpacking

## Table of Contents

- Introduction
- What is Tuple Packing?
- Packing vs Normal Tuple Creation
- Why Packing is Useful
- What is Tuple Unpacking?
- Rules of Tuple Unpacking
- Internal Working of Packing & Unpacking
- Variable Swapping using Tuples
- Returning Multiple Values from Functions
- Explicit Unpacking using the `*` Operator
- Dry Runs
- Memory Diagrams
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

One of the biggest advantages of tuples is that Python can **automatically combine multiple values into a tuple** and later **separate them back into individual variables**.

This process is known as:

- **Packing**
- **Unpacking**

These concepts are widely used in real-world Python programming.

Examples include:

- Swapping variables
- Returning multiple values from functions
- Passing tuple values to functions
- Reading multiple inputs
- Parallel assignment

These topics are introduced in the lecture after tuple creation. :contentReference[oaicite:0]{index=0}

---

# What is Tuple Packing?

Packing means **combining multiple values into a single tuple**.

Instead of writing

```python
numbers = (1, 2, 3)
```

Python also allows

```python
numbers = 1, 2, 3
```

Both statements create exactly the same tuple.

---

## Example

```python
a = 1, 2, 3

print(a)

print(type(a))
```

Output

```text
(1, 2, 3)

<class 'tuple'>
```

Python automatically packs

```
1

2

3
```

into one tuple.

---

# Packing vs Normal Tuple Creation

Normal method

```python
a = (1, 2, 3)
```

Packing

```python
a = 1, 2, 3
```

Result

```python
(1, 2, 3)
```

Both create exactly the same tuple.

The only difference is the syntax.

---

# Memory Diagram

Before Assignment

```text
1

2

3
```

↓

Python packs them

↓

```text
+-----+-----+-----+
|  1  |  2  |  3  |
+-----+-----+-----+
```

↓

Variable

```text
a
```

points to the tuple.

```text
a
│
▼
(1, 2, 3)
```

---

# Why is it Called "Packing"?

Imagine placing three books inside one box.

Books

```text
Book 1

Book 2

Book 3
```

↓

Packed into

```text
📦
```

Now instead of carrying three books separately,

you carry one box.

Similarly,

Python packs multiple values into one tuple.

---

# What is Tuple Unpacking?

Unpacking is the reverse of packing.

Instead of storing many values inside one tuple,

Python separates the tuple into individual variables.

Example

```python
a = (10, 20, 30)

x, y, z = a

print(x)

print(y)

print(z)
```

Output

```text
10

20

30
```

Python distributes each element to the corresponding variable.

---

# Dry Run

Tuple

```python
(10, 20, 30)
```

Variables

```python
x, y, z
```

Assignment

```text
10 → x

20 → y

30 → z
```

Result

```text
x = 10

y = 20

z = 30
```

---

# Memory Diagram

Initially

```text
a
│
▼
(10,20,30)
```

After unpacking

```text
x ─► 10

y ─► 20

z ─► 30
```

Each variable now stores its own value.

---

# Rule of Tuple Unpacking

The number of variables **must exactly match** the number of tuple elements.

Correct

```python
a = (10,20,30)

x, y, z = a
```

Incorrect

```python
a = (10,20,30)

x, y = a
```

Output

```text
ValueError:
too many values to unpack
```

Similarly,

```python
a = (10,20)

x, y, z = a
```

Output

```text
ValueError:
not enough values to unpack
```

This rule is emphasized in the lecture. :contentReference[oaicite:1]{index=1}

---

# Internal Working of Packing and Unpacking

Consider

```python
x, y, z = 1, 2, 3
```

It looks like Python directly assigns values.

Actually,

Python performs three steps internally.

---

## Step 1

Pack values

```text
1

2

3
```

↓

```text
(1,2,3)
```

---

## Step 2

Assign the tuple

```text
x, y, z = (1,2,3)
```

---

## Step 3

Unpack

```text
1 → x

2 → y

3 → z
```

Final

```text
x = 1

y = 2

z = 3
```

The lecture explains this internal process using diagrams. :contentReference[oaicite:2]{index=2}

---

# Variable Swapping Using Tuples

One of the most popular uses of tuple packing and unpacking is variable swapping.

Traditional Method

```python
temp = a

a = b

b = temp
```

Python Method

```python
a = 10

b = 20

a, b = b, a
```

Output

```text
a = 20

b = 10
```

---

# What Happens Internally?

Initially

```text
a = 10

b = 20
```

Python packs

```text
(b,a)
```

↓

```text
(20,10)
```

Then

Python unpacks

```text
20 → a

10 → b
```

Final

```text
a = 20

b = 10
```

No temporary variable is required.

---

# Returning Multiple Values from Functions

Functions in Python can return more than one value.

Example

```python
def calculate(a, b):

    c = a + b

    d = a - b

    return c, d

x, y = calculate(5, 3)

print("Sum =", x)

print("Difference =", y)
```

Output

```text
Sum = 8

Difference = 2
```

Although it appears that two values are returned,

Python actually returns

```python
(8, 2)
```

which is a tuple.

Then

```python
x, y
```

unpack it.

This classroom example is covered in the lecture. :contentReference[oaicite:3]{index=3}

---

# Another Example

```python
result = calculate(15, 23)

print(result)
```

Output

```text
(38, -8)
```

Now

```python
result
```

stores the complete tuple.

Accessing values

```python
print(result[0])

print(result[1])
```

Output

```text
38

-8
```

---

# Explicit Unpacking Using the `*` Operator

Consider the function

```python
def add(a, b, c, d):

    print(a + b + c + d)
```

Tuple

```python
numbers = (10,20,30,40)
```

If we write

```python
add(numbers)
```

Python treats the tuple as **one argument**.

Output

```text
TypeError
```

because the function expects **four arguments**, not one.

This example is shown in the lecture. :contentReference[oaicite:4]{index=4}

---

# Solution

Use the star operator.

```python
add(*numbers)
```

The `*` tells Python

> "Unpack this tuple."

Now Python converts

```python
(10,20,30,40)
```

into

```python
10,

20,

30,

40
```

Function call becomes

```python
add(10,20,30,40)
```

Output

```text
100
```

---

# Dry Run

Tuple

```text
(10,20,30,40)
```

↓

Star Operator

```python
*
```

↓

Converted into

```text
10

20

30

40
```

↓

Function receives

```text
a = 10

b = 20

c = 30

d = 40
```

↓

Output

```text
100
```

---

# Where Else is `*` Useful?

The star operator can also unpack tuples while printing.

Example

```python
numbers = (10,20,30,40)

print(numbers)
```

Output

```text
(10, 20, 30, 40)
```

Using

```python
print(*numbers)
```

Output

```text
10 20 30 40
```

Instead of printing the tuple object,

Python prints every element separately.

---

# Common Mistakes

## Mistake 1

```python
x, y = (10,20,30)
```

Number of variables does not match.

---

## Mistake 2

```python
add(numbers)
```

Passing one tuple instead of four arguments.

Correct

```python
add(*numbers)
```

---

## Mistake 3

Thinking

```python
return a,b
```

returns two separate values.

Actually,

Python packs them into one tuple.

---

## Mistake 4

Believing

```python
x, y = 10,20
```

does not use tuples.

Internally,

Python still performs packing and unpacking.

---

# Interview Questions

### Q1. What is tuple packing?

Packing combines multiple values into one tuple.

---

### Q2. What is tuple unpacking?

Unpacking distributes tuple elements into separate variables.

---

### Q3. Why does

```python
add(numbers)
```

produce an error?

Because the function expects four arguments, but receives one tuple.

---

### Q4. What does the `*` operator do?

It unpacks a tuple (or other iterable) into individual values.

---

### Q5. Does Python use packing and unpacking internally while swapping variables?

Yes.

Variable swapping is implemented using tuple packing and unpacking.

---

# Key Takeaways

- Packing combines multiple values into a tuple.
- Unpacking separates tuple elements into variables.
- The number of variables must equal the number of tuple elements.
- Python uses packing and unpacking internally for variable swapping.
- Returning multiple values from a function actually returns a tuple.
- The `*` operator explicitly unpacks a tuple into individual arguments.

---

# End of Part 3

➡️ **Next Part:** Accessing Tuples, Positive & Negative Indexing, Subscript Operator, Slicing, Traversing Tuples using `while` and `for` loops, and the complete **Aashiqui 2 Album** nested tuple exercise with detailed dry runs and memory diagrams.
```
=====================================================================================================================================================================================================================================================================
```md id="lecture27-part4"
# Lecture 27 - Part 4

# Accessing Tuple Elements

## Table of Contents

- Introduction
- Three Ways to Access a Tuple
- Printing the Entire Tuple
- Understanding Tuple Indexing
- Positive Indexing
- Negative Indexing
- Accessing Individual Elements
- Traversing Tuples using `while`
- Traversing Tuples using `for`
- Tuple Slicing
- Dry Runs
- Memory Diagrams
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

Creating a tuple is only the first step.

Once a tuple has been created, we usually need to

- read its elements,
- process each element,
- search for values,
- print the entire tuple,
- or access only a specific portion of it.

Since tuples are **ordered collections**, every element has a fixed position called an **index**.

Like lists, tuples use indexing and slicing to access their elements. The lecture introduces these techniques immediately after packing and unpacking. :contentReference[oaicite:0]{index=0}

---

# Three Ways to Access a Tuple

According to the lecture, there are three common ways to access a tuple.

### 1. Print the Entire Tuple

```python
print(tuple_name)
```

---

### 2. Access Individual Elements

```python
tuple_name[index]
```

---

### 3. Access Multiple Elements (Slicing)

```python
tuple_name[start:end]
```

These three methods cover almost every basic tuple access operation.

---

# Printing the Entire Tuple

The simplest way to display all elements is to pass the tuple directly to the `print()` function.

Example

```python
values = (10, 20, 30, 40)

print(values)
```

Output

```text
(10, 20, 30, 40)
```

Python prints the tuple exactly as it is stored.

This classroom example is demonstrated in the lecture. :contentReference[oaicite:1]{index=1}

---

# Understanding Tuple Indexing

Every element inside a tuple has an index.

Indexes always begin from **0**.

Consider

```python
numbers = (10, 20, 30, 40, 50)
```

Memory Representation

```text
            Positive Index

              0    1    2    3    4
              ↓    ↓    ↓    ↓    ↓
          +----+----+----+----+----+
Tuple --->|10  |20  |30  |40  |50  |
          +----+----+----+----+----+
              ↑    ↑    ↑    ↑    ↑
             -5   -4   -3   -2   -1

            Negative Index
```

The lecture uses this logical indexing diagram to explain both positive and negative indexing. :contentReference[oaicite:2]{index=2}

---

# Positive Indexing

Positive indexing starts from the beginning.

```python
numbers = (10,20,30,40,50)
```

| Index | Value |
|-------:|------:|
| 0 | 10 |
| 1 | 20 |
| 2 | 30 |
| 3 | 40 |
| 4 | 50 |

---

# Example

```python
numbers = (10,20,30,40,50)

print(numbers[0])

print(numbers[1])
```

Output

```text
10

20
```

Python simply moves to the required position and returns the value.

---

# Negative Indexing

Negative indexing starts from the end.

The last element always has index

```text
-1
```

The second last

```text
-2
```

and so on.

---

# Example

```python
numbers = (10,20,30,40,50)

print(numbers[-1])

print(numbers[-2])

print(numbers[-3])
```

Output

```text
50

40

30
```

Negative indexing is useful when we want elements from the end without knowing the tuple's length.

---

# Accessing Individual Elements

The lecture demonstrates the following program.

```python
mynums = (10,20,30,40,50)

print(mynums[0])

print(mynums[1])

print(mynums[-3])

print(mynums[-2])
```

Output

```text
10

20

30

40
```

This exact example is covered during the lecture. :contentReference[oaicite:3]{index=3}

---

# Dry Run

Tuple

```python
(10,20,30,40,50)
```

---

### Statement

```python
mynums[0]
```

Python starts counting from

```text
0
```

Result

```text
10
```

---

### Statement

```python
mynums[1]
```

Moves to

```text
Index 1
```

Result

```text
20
```

---

### Statement

```python
mynums[-3]
```

Starts from the end

```text
-1 → 50

-2 → 40

-3 → 30
```

Result

```text
30
```

---

### Statement

```python
mynums[-2]
```

Result

```text
40
```

---

# Memory Diagram

```text
Tuple

+----+----+----+----+----+
|10  |20  |30  |40  |50  |
+----+----+----+----+----+
 0    1    2    3    4

-5   -4   -3   -2   -1
```

Reading

```python
mynums[-2]
```

Python moves

```text
Last Element

↓

50

↓

One Step Left

↓

40
```

Result

```text
40
```

---

# Traversing a Tuple using a `while` Loop

Sometimes we want to process every element one by one.

The lecture first demonstrates using a `while` loop.

Program

```python
mynums = (10,20,30,40,50)

n = len(mynums)

i = 0

while i < n:

    print(mynums[i])

    i = i + 1
```

Output

```text
10

20

30

40

50
```

This is the exact classroom example shown in the lecture. :contentReference[oaicite:4]{index=4}

---

# Dry Run

Initially

```text
n = 5

i = 0
```

---

Iteration 1

```text
i = 0
```

Print

```python
mynums[0]
```

↓

```text
10
```

Increment

```text
i = 1
```

---

Iteration 2

```text
i = 1
```

↓

Print

```text
20
```

---

Iteration 3

```text
i = 2
```

↓

Print

```text
30
```

Python continues until

```text
i = 5
```

The condition

```python
i < n
```

becomes False.

Loop stops.

---

# Traversing a Tuple using a `for` Loop

Python provides a simpler way to iterate over a tuple.

Program

```python
mynums = (10,20,30,40,50)

for x in mynums:

    print(x)
```

Output

```text
10

20

30

40

50
```

This is also demonstrated in the lecture. :contentReference[oaicite:5]{index=5}

---

# Dry Run

Tuple

```python
(10,20,30,40,50)
```

Python automatically performs

```text
x = 10

↓

Print

↓

x = 20

↓

Print

↓

x = 30

↓

Print

↓

x = 40

↓

Print

↓

x = 50

↓

Print

↓

End
```

Unlike the `while` loop,

no index variable is required.

---

# Which Loop Should We Prefer?

### While Loop

Advantages

- Useful when index is needed.
- Gives complete control over iteration.

Disadvantages

- More code.
- Manual index management.

---

### For Loop

Advantages

- Simple.
- Readable.
- Less error-prone.
- Recommended for most situations.

---

# Tuple Slicing

Just like lists,

tuples also support slicing.

General Syntax

```python
tuple[start:end]
```

The element at `start` is included.

The element at `end` is excluded.

---

# Example 1

```python
numbers = (10,20,30,40,50)

print(numbers[1:4])
```

Output

```text
(20, 30, 40)
```

---

# Example 2

```python
print(numbers[:3])
```

Output

```text
(10,20,30)
```

---

# Example 3

```python
print(numbers[2:])
```

Output

```text
(30,40,50)
```

---

# Example 4

```python
print(numbers[::-1])
```

Output

```text
(50,40,30,20,10)
```

Unlike lists,

tuple slicing **always creates a new tuple**.

---

# Common Mistakes

## Mistake 1

Using parentheses instead of square brackets.

Incorrect

```python
numbers(0)
```

Correct

```python
numbers[0]
```

---

## Mistake 2

Using an invalid index.

```python
numbers[10]
```

Output

```text
IndexError
```

---

## Mistake 3

Forgetting that indexing starts from zero.

The first element is

```python
numbers[0]
```

not

```python
numbers[1]
```

---

## Mistake 4

Using a `while` loop without incrementing `i`.

```python
i = i + 1
```

If omitted,

the loop runs forever.

---

# Interview Questions

### Q1. Which operator is used to access tuple elements?

The **subscript operator** `[]`.

---

### Q2. What is the index of the last element?

```text
-1
```

---

### Q3. Which loop is generally preferred for traversing tuples?

The **for loop**, because it is simpler and more readable.

---

### Q4. Does slicing modify the original tuple?

No.

It creates and returns a **new tuple**.

---

### Q5. Can tuple indexing be negative?

Yes.

Negative indexing starts from the last element.

---

# Key Takeaways

- Tuple elements are accessed using the **subscript operator `[]`**.
- Positive indexing starts from `0`.
- Negative indexing starts from `-1`.
- Tuples can be traversed using both `while` and `for` loops.
- Slicing works exactly like list slicing but returns a new tuple.
- The `for` loop is usually the preferred way to iterate over tuples.

---

# End of Part 4

➡️ **Next Part:** Complete classroom exercise on the **Aashiqui 2 Album** (nested tuple), nested unpacking, iteration through song tuples, immutability rules, mutable objects inside tuples, `del` statement, and detailed dry runs with memory diagrams.
```
======================================================================================================================================================================================================================================================================
```md id="lecture27-part5"
# Lecture 27 - Part 5

# Nested Tuples, Immutability and Deleting Tuples

## Table of Contents

- Introduction
- Exercise – Aashiqui 2 Album
- Understanding Nested Tuples
- Unpacking the Album Tuple
- Iterating Through Songs
- Complete Dry Run
- Memory Diagram
- Tuple Immutability
- Mutable Objects Inside Tuples
- Deleting Tuples using `del`
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

Until now, we have learned

- Creating tuples
- Packing and unpacking
- Accessing tuple elements
- Traversing tuples

In this part, we will learn how tuples can contain **other tuples**, how to process such nested structures, and understand one of the most important concepts of tuples—**immutability**.

The lecture uses a practical example of an **Aashiqui 2** music album represented using nested tuples. :contentReference[oaicite:0]{index=0}

---

# Exercise – Aashiqui 2 Album

The lecture provides the following tuple.

```python
album = (
    "Aashiqui 2",
    2013,
    "Arijit Singh",
    (
        (1, "Tum Hi Ho"),
        (2, "Chahun Mai Ya Na"),
        (3, "Meri Aashiqui"),
        (4, "Aasan Nahin Yahaan")
    )
)
```

This tuple stores

- Movie name
- Release year
- Singer
- Songs

Notice that the fourth element itself is another tuple containing song details. :contentReference[oaicite:1]{index=1}

---

# Understanding the Structure

The tuple is not flat.

Instead, it contains another tuple.

Structure

```text
album
│
├── "Aashiqui 2"
├── 2013
├── "Arijit Singh"
└── Songs
      │
      ├── (1,"Tum Hi Ho")
      ├── (2,"Chahun Mai Ya Na")
      ├── (3,"Meri Aashiqui")
      └── (4,"Aasan Nahin Yahaan")
```

This type of structure is called a **Nested Tuple**.

---

# Unpacking the Album

Instead of accessing every element using indexes,

Python allows us to unpack the tuple.

Program

```python
movie_name, year, singer, songs = album

print("Title :", movie_name)
print("Year  :", year)
print("Singer:", singer)
```

Output

```text
Title : Aashiqui 2

Year  : 2013

Singer: Arijit Singh
```

Python automatically assigns

```text
"Aashiqui 2" → movie_name

2013 → year

"Arijit Singh" → singer

Songs Tuple → songs
```

---

# Iterating Through Songs

The fourth element is itself a tuple.

Each song is another tuple containing

```text
(song_number, song_name)
```

We can iterate over them directly.

```python
for song_no, song_name in songs:

    print(f"Song #{song_no} : {song_name}")
```

Output

```text
Song #1 : Tum Hi Ho

Song #2 : Chahun Mai Ya Na

Song #3 : Meri Aashiqui

Song #4 : Aasan Nahin Yahaan
```

This nested unpacking example is demonstrated in the lecture. :contentReference[oaicite:2]{index=2}

---

# How Does Nested Unpacking Work?

Consider the first song.

```python
(1, "Tum Hi Ho")
```

During the first iteration,

Python performs

```text
song_no = 1

song_name = "Tum Hi Ho"
```

During the second iteration,

```python
(2, "Chahun Mai Ya Na")
```

becomes

```text
song_no = 2

song_name = "Chahun Mai Ya Na"
```

The process continues until every song tuple has been unpacked.

---

# Complete Dry Run

Initially

```text
album
```

↓

Unpack

```text
movie_name = "Aashiqui 2"

year = 2013

singer = "Arijit Singh"

songs = (
    (1,"Tum Hi Ho"),
    (2,"Chahun Mai Ya Na"),
    (3,"Meri Aashiqui"),
    (4,"Aasan Nahin Yahaan")
)
```

↓

Start loop

---

Iteration 1

```text
song = (1,"Tum Hi Ho")
```

↓

Unpack

```text
song_no = 1

song_name = Tum Hi Ho
```

↓

Print

```text
Song #1 : Tum Hi Ho
```

---

Iteration 2

```text
song = (2,"Chahun Mai Ya Na")
```

↓

Print

```text
Song #2 : Chahun Mai Ya Na
```

---

Iteration 3

↓

```text
Song #3 : Meri Aashiqui
```

---

Iteration 4

↓

```text
Song #4 : Aasan Nahin Yahaan
```

Loop Ends.

---

# Memory Diagram

```text
album
│
├── "Aashiqui 2"
├── 2013
├── "Arijit Singh"
└── songs
      │
      ├── (1,"Tum Hi Ho")
      ├── (2,"Chahun Mai Ya Na")
      ├── (3,"Meri Aashiqui")
      └── (4,"Aasan Nahin Yahaan")
```

After unpacking

```text
movie_name ──► "Aashiqui 2"

year ───────► 2013

singer ─────► "Arijit Singh"

songs ──────► Nested Tuple
```

---

# Tuple Immutability

One of the defining characteristics of tuples is **immutability**.

Once a tuple has been created,

its elements cannot be

- modified,
- inserted,
- removed,
- or reordered.

Example

```python
numbers = (10, 20, 30)

numbers[0] = 100
```

Output

```text
TypeError:

'tuple' object does not support item assignment
```

The lecture emphasizes that tuples are **read-only collections** after creation. :contentReference[oaicite:3]{index=3}

---

# Why Are Tuples Immutable?

When Python creates a tuple,

it allocates memory for all its elements.

Since the tuple will never change,

Python does not provide methods like

- append()
- insert()
- remove()
- pop()
- clear()

This makes tuples

- faster,
- memory efficient,
- and safer for storing constant data.

---

# Mutable Objects Inside Tuples ⭐

This is one of the most important interview concepts.

Consider

```python
numbers = (
    [10, 20],
    30,
    40
)
```

Can we modify it?

Most beginners say

"No, because tuples are immutable."

But the answer is

**Yes — partially.**

---

# Example

```python
numbers = (
    [10,20],
    30,
    40
)

numbers[0][0] = 15

print(numbers)
```

Output

```text
([15, 20], 30, 40)
```

Why is this allowed?

Because

the tuple itself is **not changing**.

The first element still points to the **same list**.

Only the contents **inside the list** are changing.

---

# Memory Diagram

Initially

```text
Tuple

+-----------+-----+-----+
|  List     | 30  | 40  |
+-----------+-----+-----+
      │
      ▼
+----+----+
|10  |20  |
+----+----+
```

After

```python
numbers[0][0] = 15
```

```text
Tuple

+-----------+-----+-----+
|  List     | 30  | 40  |
+-----------+-----+-----+
      │
      ▼
+----+----+
|15  |20  |
+----+----+
```

Notice

The tuple still points to **the same list**.

Only the list's contents changed.

---

# Deleting Tuples

Since tuples are immutable,

individual elements cannot be deleted.

Incorrect

```python
numbers = (10,20,30)

del numbers[0]
```

Output

```text
TypeError
```

---

# Deleting the Entire Tuple

Although individual elements cannot be deleted,

the entire tuple variable can be removed.

```python
numbers = (10,20,30)

del numbers
```

Now,

```python
print(numbers)
```

Output

```text
NameError

name 'numbers' is not defined
```

The lecture explains this distinction between deleting an element and deleting the entire tuple object. :contentReference[oaicite:4]{index=4}

---

# Common Mistakes

## Mistake 1

Trying to modify a tuple.

```python
numbers[0] = 50
```

Raises

```text
TypeError
```

---

## Mistake 2

Thinking nested lists cannot change.

Lists remain mutable even when stored inside tuples.

---

## Mistake 3

Using

```python
del numbers[1]
```

Individual tuple elements cannot be deleted.

---

## Mistake 4

Confusing tuple immutability with object immutability.

The tuple is immutable,

but objects stored inside it may still be mutable.

---

# Interview Questions

### Q1. Can tuples contain other tuples?

Yes.

These are called **nested tuples**.

---

### Q2. Why is modifying

```python
numbers[0] = 50
```

not allowed?

Because tuples are immutable.

---

### Q3. Why is

```python
numbers[0][0] = 15
```

allowed?

Because the tuple still refers to the same list.

Only the list contents change.

---

### Q4. Can we delete one tuple element?

No.

---

### Q5. Can we delete the entire tuple?

Yes.

Using

```python
del tuple_name
```

---

# Key Takeaways

- Tuples can contain other tuples.
- Nested unpacking makes complex tuple processing easy.
- Tuples are immutable after creation.
- Mutable objects inside tuples can still be modified.
- Individual tuple elements cannot be deleted.
- The entire tuple object can be removed using `del`.

---

# End of Part 5

➡️ **Next Part:** Built-in Functions with Tuples (`len()`, `max()`, `min()`, `sum()`, `sorted()`, `tuple()`, `any()`, `all()`), Tuple Methods (`count()` and `index()`), additional lecture examples, interview questions, and the complete Lecture 27 summary.
```
===========================================================================================================================================================================================================================================================================
```md id="lecture27-part6"
# Lecture 27 - Part 6

# Built-in Functions, Tuple Methods and Lecture Summary

## Table of Contents

- Introduction
- Built-in Functions
  - len()
  - max()
  - min()
  - sum()
  - sorted()
  - tuple()
  - any()
  - all()
- Tuple Methods
  - count()
  - index()
- Complete Lecture Examples
- Tuple vs List Revision
- Common Mistakes
- Interview Questions
- Complete Lecture Summary
- Key Takeaways

---

# Introduction

Like lists, tuples can also be used with many of Python's built-in functions.

However, because tuples are **immutable**, functions that modify the sequence (such as `append()` or `pop()`) do not exist.

Instead, tuples mainly work with

- built-in functions, and
- two special tuple methods.

These topics conclude the lecture. :contentReference[oaicite:0]{index=0}

---

# Built-in Functions with Tuples

Python provides many built-in functions that work directly with tuples.

These functions **do not modify** the tuple.

Instead, they either

- return information,
- calculate a result,
- or create a new object.

---

# 1. `len()`

The `len()` function returns the total number of elements present in a tuple.

### Syntax

```python
len(tuple_name)
```

---

### Example

```python
numbers = (10, 20, 30, 40)

print(len(numbers))
```

Output

```text
4
```

---

### Dry Run

Tuple

```text
(10,20,30,40)
```

Count elements

```text
10 → 1

20 → 2

30 → 3

40 → 4
```

Return

```text
4
```

---

# 2. `max()`

Returns the largest element.

Example

```python
numbers = (5, 2, 11, 3)

print(max(numbers))
```

Output

```text
11
```

Python compares every element and returns the greatest value.

---

# 3. `min()`

Returns the smallest element.

Example

```python
numbers = (5,2,11,3)

print(min(numbers))
```

Output

```text
2
```

---

# 4. `sum()`

Returns the sum of all numerical values.

Example

```python
numbers = (10,20,30)

print(sum(numbers))
```

Output

```text
60
```

---

### Dry Run

```text
10 + 20 + 30

↓

60
```

---

# 5. `sorted()`

The `sorted()` function sorts the tuple.

However,

there is one very important point.

**It does not return a tuple.**

It returns a **list**.

Example

```python
numbers = (5,2,11,3)

print(sorted(numbers))
```

Output

```text
[2,3,5,11]
```

Notice

The output uses

```python
[]
```

not

```python
()
```

because `sorted()` always returns a list.

This behavior is highlighted in the lecture notes. :contentReference[oaicite:1]{index=1}

---

# Getting a Sorted Tuple

If a tuple is required,

wrap the result inside `tuple()`.

```python
numbers = (5,2,11,3)

sorted_tuple = tuple(sorted(numbers))

print(sorted_tuple)
```

Output

```text
(2,3,5,11)
```

---

# 6. `tuple()`

The `tuple()` constructor converts an iterable into a tuple.

Example

```python
text = "BHOPAL"

letters = tuple(text)

print(letters)
```

Output

```text
('B','H','O','P','A','L')
```

Python creates one tuple element for every character.

---

### Memory Diagram

```text
"BHOPAL"

↓

B

H

O

P

A

L

↓

('B','H','O','P','A','L')
```

---

# 7. `any()`

Returns

```text
True
```

if **at least one element** is truthy.

Example

```python
values = (0, False, 5)

print(any(values))
```

Output

```text
True
```

Why?

Because

```text
5
```

is truthy.

---

### Another Example

```python
values = (0, False, "")

print(any(values))
```

Output

```text
False
```

All values are falsy.

---

# 8. `all()`

Returns

```text
True
```

only if **every element** is truthy.

Example

```python
values = (1, True, "Hi")

print(all(values))
```

Output

```text
True
```

---

Example

```python
values = (1, True, 0)

print(all(values))
```

Output

```text
False
```

because

```text
0
```

is falsy.

---

# Summary of Built-in Functions

| Function | Purpose | Example Output |
|----------|---------|----------------|
| `len()` | Number of elements | `4` |
| `max()` | Largest value | `11` |
| `min()` | Smallest value | `2` |
| `sum()` | Sum of numbers | `60` |
| `sorted()` | Returns sorted **list** | `[2,3,5]` |
| `tuple()` | Converts iterable to tuple | `('A','B')` |
| `any()` | At least one truthy value | `True` |
| `all()` | Every value truthy | `True` |

---

# Tuple Methods

Unlike lists,

tuples provide only **two methods**.

Why?

Because tuples are immutable.

Methods like

- append()
- remove()
- pop()
- extend()

would modify the tuple,

so Python does not provide them.

---

# Method 1 — `count()`

Returns how many times a value occurs.

Syntax

```python
tuple.count(value)
```

---

### Example

```python
numbers = (10,20,10,30,10)

print(numbers.count(10))
```

Output

```text
3
```

Python counts every occurrence of

```text
10
```

---

### Dry Run

Tuple

```text
10

20

10

30

10
```

Occurrences

```text
1

2

3
```

Return

```text
3
```

---

# Method 2 — `index()`

Returns the **first occurrence** of a value.

Syntax

```python
tuple.index(value)
```

Example

```python
numbers = (10,20,30,40)

print(numbers.index(30))
```

Output

```text
2
```

because

```text
30
```

is located at index

```text
2
```

---

### If the Value Does Not Exist

Example

```python
numbers = (10,20,30)

print(numbers.index(50))
```

Output

```text
ValueError
```

because

```text
50
```

is not present.

---

# Complete Revision

| Topic | Important Point |
|--------|-----------------|
| Ordered | Yes |
| Mutable | No |
| Duplicate Values | Allowed |
| Heterogeneous Data | Allowed |
| Indexing | Yes |
| Slicing | Yes |
| Packing | Supported |
| Unpacking | Supported |
| Star Operator | Supported |
| Built-in Methods | Only 2 |

---

# Tuple vs List Revision

| Feature | Tuple | List |
|---------|-------|------|
| Brackets | `()` | `[]` |
| Mutable | ❌ | ✅ |
| Memory Usage | Less | More |
| Speed | Faster | Slightly Slower |
| Methods | 2 | Many |
| Best Used For | Fixed Data | Dynamic Data |

---

# Common Mistakes

## Mistake 1

Expecting

```python
sorted(tuple)
```

to return a tuple.

It returns a **list**.

---

## Mistake 2

Using

```python
append()
```

with tuples.

```python
numbers.append(50)
```

Output

```text
AttributeError
```

---

## Mistake 3

Confusing

```python
count()
```

with

```python
index()
```

`count()`

↓

Returns frequency.

`index()`

↓

Returns first position.

---

## Mistake 4

Believing tuples have the same methods as lists.

They do not.

Tuples provide only

- count()
- index()

---

# Interview Questions

### Q1. Why do tuples have only two methods?

Because tuples are immutable.

---

### Q2. Which built-in function returns a list?

```python
sorted()
```

---

### Q3. Which function converts a string into a tuple?

```python
tuple()
```

---

### Q4. What is the difference between `any()` and `all()`?

`any()`

↓

At least one truthy value.

`all()`

↓

Every value must be truthy.

---

### Q5. Which tuple method returns the first occurrence?

```python
index()
```

---

### Q6. Which tuple method returns the frequency?

```python
count()
```

---

# Complete Lecture 27 Summary

In this lecture, we studied Python **Tuples**, one of the most commonly used immutable data structures.

We learned:

- What tuples are
- Why tuples are immutable
- Properties of tuples
- Differences between tuples and lists
- Creating tuples
- Single-element tuple syntax
- Tuple packing
- Tuple unpacking
- Internal working of packing and unpacking
- Variable swapping
- Returning multiple values from functions
- Explicit unpacking using the `*` operator
- Accessing tuple elements
- Positive and negative indexing
- Slicing
- Traversing tuples using `while` and `for`
- Nested tuples
- Nested unpacking
- Immutability rules
- Mutable objects inside tuples
- Deleting tuples
- Built-in functions
- Tuple methods

Although tuples are simple, they are extremely important because they provide

- faster execution,
- lower memory usage,
- and protection against accidental modification.

---

# Key Takeaways

- Tuples are immutable ordered collections.
- A single-element tuple requires a trailing comma.
- Packing and unpacking simplify Python code.
- Functions returning multiple values actually return tuples.
- The `*` operator unpacks tuple elements.
- Tuples support indexing, slicing, and iteration.
- Mutable objects inside tuples can still be modified.
- Only two tuple methods exist: `count()` and `index()`.
- `sorted()` returns a list, not a tuple.
- Tuples are preferred when the data should remain fixed.

---

# End of Lecture 27 ✅

You have now completed the entire Tuple lecture, covering every major concept from the lecture slides and examples, along with additional explanations, dry runs, memory diagrams, interview questions, and practical examples.
```
