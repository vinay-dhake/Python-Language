# Lecture 25 - Part 1
# Python Lists - List Methods (Functions vs Methods & `append()`)

> **Lecture:** 25 - Operations on List / List Methods  

---

# Table of Contents

- Introduction
- What are List Methods?
- Function vs Method
- Why are List Methods Needed?
- `append()` Method
- Syntax
- Working of `append()`
- Example 1
- Dry Run
- Memory Diagram
- Return Value of `append()`
- Important Notes
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

In the previous lecture, we learned that Python lists are **mutable**, which means they can be modified after creation.

We modified lists using

- Index Assignment

```python
numbers[2] = 100
```

- Slice Assignment

```python
numbers[1:3] = [20,30]
```

- `del`

```python
del numbers[2]
```

In this lecture, we move one step further.

Instead of modifying lists manually using indexing, Python provides many **built-in methods** that make list operations easier.

Some important list methods are

- `append()`
- `extend()`
- `insert()`
- `index()`
- `count()`
- `remove()`
- `pop()`
- `clear()`
- `sort()`

These methods are used in almost every Python program and are among the most frequently asked topics in interviews.

---

# What is a Method?

A **method** is simply a function that belongs to an object.

Since a list is an object, it has its own methods.

Example

```python
numbers.append(10)
```

Here,

- `numbers` is a list object.
- `append()` is a method of the list.

---

# Function vs Method

This is one of the most important concepts for Python beginners.

Many students confuse functions with methods.

Let's understand the difference.

---

# Function

A function is called directly by its name.

General Syntax

```python
function_name(arguments)
```

Example

```python
len(numbers)
```

Here,

- `len` is a function.
- `numbers` is passed as an argument.

---

# Method

A method belongs to an object.

General Syntax

```python
object.method(arguments)
```

Example

```python
numbers.append(10)
```

Here,

- `numbers` is the object.
- `append()` belongs to the list object.

---

# Visual Comparison

Function

```text
Function

↓

len(numbers)
```

Method

```text
Object

↓

numbers

↓

append()

↓

numbers.append(10)
```

---

# Comparison Table

| Function | Method |
|-----------|---------|
| Called directly | Called through an object |
| `len(numbers)` | `numbers.append(10)` |
| Independent | Belongs to an object |
| Works on many objects | Specific to that object |

---

# Remember

Most list operations are methods.

Examples

```python
append()

extend()

insert()

remove()

pop()

sort()

clear()
```

Whereas

```python
len()

sum()

max()

min()

sorted()
```

are functions.

---

# Why Do We Need List Methods?

Imagine a list

```python
numbers = [10,20,30]
```

Suppose you want to add

```python
40
```

Without methods, you may need complicated operations.

Instead,

Python simply provides

```python
numbers.append(40)
```

One line.

Simple.

Readable.

Efficient.

---

# The `append()` Method

The first and probably the most commonly used list method is

```python
append()
```

---

# Purpose

`append()` adds **exactly one element** to the **end** of a list.

---

# Syntax

```python
list_name.append(item)
```

where

```python
item
```

is the value that you want to add.

---

# Important Rule

`append()` always inserts the element at the **last position**.

It never inserts anywhere else.

---

# Example 1

```python
primes = [2, 3, 5, 7]

print("Initial length:", len(primes))

primes.append(11)

print("Updated list:", primes)

print("Updated length:", len(primes))
```

Output

```python
Initial length: 4

Updated list: [2, 3, 5, 7, 11]

Updated length: 5
```

---

# Step-by-Step Dry Run

Initially

```python
primes = [2,3,5,7]
```

Memory

```text
Index

0 → 2

1 → 3

2 → 5

3 → 7
```

Length

```python
len(primes)
```

returns

```text
4
```

---

Python executes

```python
primes.append(11)
```

The new element

```text
11
```

is placed at the end.

Memory becomes

```text
Index

0 → 2

1 → 3

2 → 5

3 → 7

4 → 11
```

Now

```python
len(primes)
```

returns

```text
5
```

---

# Visual Representation

Before

```text
+----+----+----+----+

| 2 | 3 | 5 | 7 |

+----+----+----+----+
```

↓

Append

```python
11
```

↓

After

```text
+----+----+----+----+----+

| 2 | 3 | 5 | 7 |11 |

+----+----+----+----+----+
```

---

# Internal Working

When Python executes

```python
append(11)
```

it performs

```text
Find the last index

↓

Create one new position

↓

Store 11 there

↓

Increase list size
```

---

# Does `append()` Return Anything?

No.

It modifies the existing list.

Its return value is

```python
None
```

Example

Wrong

```python
numbers = [1,2]

result = numbers.append(3)

print(result)
```

Output

```python
None
```

because

```python
append()
```

changes the list directly.

---

# Correct Usage

```python
numbers = [1,2]

numbers.append(3)

print(numbers)
```

Output

```python
[1,2,3]
```

---

# Important Points

✅ Adds exactly one element.

✅ Adds at the end.

✅ Modifies the original list.

✅ Does not create a new list.

✅ Returns `None`.

---

# Common Mistakes

### Mistake 1

Expecting

```python
append()
```

to return the updated list.

Wrong

```python
new_list = numbers.append(5)
```

Correct

```python
numbers.append(5)
```

---

### Mistake 2

Thinking it inserts anywhere.

No.

It always inserts at the end.

---

### Mistake 3

Thinking

```python
append()
```

creates a new list.

It does not.

It modifies the same list.

---

# Interview Questions

## Q1. How many elements can `append()` add at one time?

Only **one** element.

---

## Q2. Where does `append()` insert the element?

Always at the end of the list.

---

## Q3. Does `append()` return the modified list?

No.

It returns

```python
None
```

---

## Q4. Does `append()` change the original list?

Yes.

It modifies the original list in place.

---

# Key Takeaways

- Methods belong to objects, while functions are called directly.
- Lists provide several built-in methods to manipulate data.
- `append()` is used to add a single element at the end of a list.
- `append()` modifies the original list and returns `None`.
- It is one of the most frequently used list methods in Python.

---
==============================================================================================================================================================

# Lecture 25 - Part 2
# `append()` (Deep Dive) & Introduction to `extend()`

# Table of Contents

- `append()` with Collections
- Appending a List vs Appending Elements
- Nested Lists
- Accessing Nested Elements
- Memory Diagram
- `append()` Rules
- Introduction to `extend()`
- Difference Between `append()` and `extend()`
- First `extend()` Example
- Dry Run
- Interview Questions
- Common Mistakes
- Key Takeaways

---

# `append()` with Collections

In Part 1, we learned that `append()` adds **one element** to the end of a list.

Now comes the most important question.

### What happens if the element itself is another list?

Consider

```python
animals = ["cat", "dog", "rabbit"]

wild_animals = ["tiger", "fox"]
```

If we execute

```python
animals.append(wild_animals)
```

Will Python insert

```text
tiger

fox
```

separately?

**No.**

Python treats the entire list as **one single object**.

---

# Example 2 — Appending a List

```python
animals = ["cat", "dog", "rabbit"]

wild_animals = ["tiger", "fox"]

animals.append(wild_animals)

print(animals)

print(len(animals))
```

Output

```python
['cat', 'dog', 'rabbit', ['tiger', 'fox']]

4
```

---

# Understanding the Output

Original list

```python
['cat','dog','rabbit']
```

Length

```text
3
```

Now execute

```python
append(wild_animals)
```

Python **does not open** the second list.

Instead,

it stores the **entire list** as one element.

Result

```python
[
'cat',
'dog',
'rabbit',
['tiger','fox']
]
```

Notice carefully.

The fourth element itself is another list.

---

# Memory Representation

Before

```text
animals

↓

+-------+-------+---------+

| cat | dog | rabbit |

+-------+-------+---------+
```

After

```text
animals

↓

+-------+-------+---------+------------------+

| cat | dog | rabbit | ['tiger','fox'] |

+-------+-------+---------+------------------+
```

The last box contains **one object**:

```python
['tiger','fox']
```

---

# Length Calculation

Many beginners expect

```python
5
```

because they see

```text
cat

dog

rabbit

tiger

fox
```

But Python returns

```python
4
```

Why?

Because the last element is

```python
['tiger','fox']
```

which counts as **one element**.

---

# Visual Representation

```text
Index

0 → cat

1 → dog

2 → rabbit

3 → ['tiger','fox']
```

Total elements

```text
4
```

---

# Nested Lists

A list inside another list is called a

## Nested List

Example

```python
[
1,
2,
[3,4],
5
]
```

Here

```python
[3,4]
```

is itself another list.

---

# Accessing Nested Elements

Suppose we execute

```python
print(animals[3][0])
```

Output

```python
tiger
```

---

# Why?

First

```python
animals[3]
```

returns

```python
['tiger','fox']
```

Now Python again applies indexing.

```python
['tiger','fox'][0]
```

returns

```python
tiger
```

---

# Step-by-Step Dry Run

Python executes

```python
animals[3]
```

Result

```python
['tiger','fox']
```

Now

```python
[0]
```

is applied.

Result

```python
'tiger'
```

---

# Memory Diagram

```text
animals

↓

0

↓

cat

----------------

1

↓

dog

----------------

2

↓

rabbit

----------------

3

↓

+---------+------+

| tiger | fox |

+---------+------+

      ↑

      animals[3]

             ↓

        animals[3][0]

             ↓

          tiger
```

---

# Important Rule

`append()` **never opens** a collection.

Whether you append

- another list
- a tuple
- a dictionary
- a set

Python stores the entire object as **one element**.

---

# Summary of `append()`

| Statement | Result |
|-----------|--------|
| `append(10)` | Adds one integer |
| `append("hello")` | Adds one string |
| `append([1,2])` | Adds one list |
| `append((1,2))` | Adds one tuple |

---

# Introduction to `extend()`

Suppose instead of creating

```python
[
'cat',
'dog',
'rabbit',
['tiger','fox']
]
```

you wanted

```python
[
'cat',
'dog',
'rabbit',
'tiger',
'fox'
]
```

Can `append()` do that?

No.

For this purpose,

Python provides another method

```python
extend()
```

---

# Purpose of `extend()`

`extend()` takes an iterable and adds **each individual element** to the end of the list.

Unlike `append()`,

it **opens** the iterable before adding the elements.

---

# Syntax

```python
list_name.extend(iterable)
```

---

# Example 3

```python
colors = ["red", "green"]

colors.extend(["blue", "yellow"])

print(colors)
```

Output

```python
['red', 'green', 'blue', 'yellow']
```

---

# Step-by-Step Dry Run

Initially

```python
colors

↓

['red','green']
```

Python executes

```python
extend(["blue","yellow"])
```

Instead of adding

```python
["blue","yellow"]
```

as one object,

Python takes

```text
blue

yellow
```

individually.

Final list

```python
[
'red',
'green',
'blue',
'yellow'
]
```

---

# Memory Representation

Before

```text
red

green
```

↓

Extend

```python
["blue","yellow"]
```

↓

Python inserts

```text
blue

yellow
```

individually.

Final Memory

```text
red

green

blue

yellow
```

---

# `append()` vs `extend()`

This is one of the most commonly asked interview questions.

| `append()` | `extend()` |
|------------|------------|
| Adds one object | Adds each element individually |
| Can create nested lists | Does not create nested lists (when extending with a list) |
| Accepts any object | Argument must be iterable |
| List grows by 1 | List grows by number of elements in iterable |

---

# Example Comparison

Using `append()`

```python
numbers = [1,2]

numbers.append([3,4])
```

Output

```python
[1,2,[3,4]]
```

---

Using `extend()`

```python
numbers = [1,2]

numbers.extend([3,4])
```

Output

```python
[1,2,3,4]
```

---

# Common Mistakes

### Mistake 1

Thinking

```python
append([3,4])
```

and

```python
extend([3,4])
```

do the same thing.

They do **not**.

---

### Mistake 2

Expecting

```python
append()
```

to insert every element of another list.

It never does.

---

### Mistake 3

Confusing a nested list with a normal list.

Remember

```python
[
1,
2,
[3,4]
]
```

contains **three** elements.

---

# Interview Questions

## Q1. What is a nested list?

A list that contains another list as one of its elements.

---

## Q2. What is the output?

```python
a=[1,2]

a.append([3,4])

print(len(a))
```

Answer

```python
3
```

---

## Q3. Which method creates nested lists?

```python
append()
```

---

## Q4. Which method adds individual elements from another list?

```python
extend()
```

---

## Q5. Why does

```python
append([1,2])
```

increase the length by only one?

Because the entire list

```python
[1,2]
```

is stored as a **single object**.

---

# Key Takeaways

- `append()` always adds one object, even if that object is another list.
- Appending a list creates a nested list.
- Nested elements are accessed using multiple indices such as `animals[3][0]`.
- `extend()` works differently—it unpacks an iterable and appends each element individually.
- Understanding the difference between `append()` and `extend()` is essential for coding interviews.

---

# End of Part 2

**➡️ Next Part:** `extend()` in detail—working with integers, why `extend(11)` throws a `TypeError`, fixing it with `[11]`, extending using strings (`"blue"` vs `["blue"]`), detailed dry runs, and interview questions.
=====================================================================================================================================================================================================================================

# Lecture 25 - Part 3
# `extend()` Method 


---

# Table of Contents

- Recap
- `extend()` Method
- Why `extend()` Needs an Iterable
- Example 1
- `extend(11)` Error
- Fixing the Error
- Extending Using Strings
- `"blue"` vs `["blue"]`
- Internal Working
- Memory Diagrams
- Comparison Table
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Recap

In the previous part, we learned the difference between

```python
append()
```

and

```python
extend()
```

Remember

```python
append()
```

adds **one object**.

```python
extend()
```

adds **each individual element** of an iterable.

---

# Why Does `extend()` Require an Iterable?

This is one of the most commonly misunderstood concepts.

Python internally processes `extend()` like this:

```text
Take the iterable

↓

Read one element

↓

Append it

↓

Read next element

↓

Append it

↓

Continue until iterable ends
```

Therefore,

Python **must** receive something that it can iterate over.

Examples of iterables are

- Lists
- Tuples
- Strings
- Sets
- Dictionaries (keys)
- Ranges

---

# Example 4 — Extending a List

```python
num_list = [1, 2, 3]

num_list.extend([11])

print(num_list)
```

Output

```python
[1, 2, 3, 11]
```

---

# Dry Run

Initially

```python
num_list

↓

[1,2,3]
```

Python receives

```python
[11]
```

It opens the iterable.

First element

```text
11
```

↓

Append

Final list

```python
[1,2,3,11]
```

---

# Memory Representation

Before

```text
+----+----+----+

|1 |2 |3 |

+----+----+----+
```

↓

Extend

```python
[11]
```

↓

After

```text
+----+----+----+----+

|1 |2 |3 |11 |

+----+----+----+----+
```

---

# Example 5 — Invalid Usage

Suppose we write

```python
num_list = [1,2,3]

num_list.extend(11)
```

Output

```text
TypeError:

'int' object is not iterable
```

---

# Why?

Python internally tries to do

```text
Read first element of 11
```

But

```python
11
```

is just one integer.

There is no

- first element
- second element
- third element

Therefore,

Python raises

```text
TypeError
```

---

# Internal Working

Python expects something like

```text
11

12

13
```

one after another.

But

```python
11
```

is just

```text
11
```

There is nothing to iterate.

---

# Correct Solution

Wrap the integer inside a list.

```python
num_list.extend([11])
```

Now Python sees

```text
List

↓

11
```

It can iterate successfully.

---

# Important Rule

`extend()`

accepts only

```text
Iterable Objects
```

Examples

✔ List

✔ Tuple

✔ String

✔ Range

✔ Set

❌ Integer

❌ Float

❌ Boolean (by itself)

---

# Extending Using Strings

One interesting feature of Python is

A string is also an iterable.

That means

Python can visit each character one by one.

---

# Example 6

```python
chars = ["red", "green"]

chars.extend("blue")

print(chars)
```

Output

```python
['red', 'green', 'b', 'l', 'u', 'e']
```

---

# Why Does This Happen?

Python treats

```python
"blue"
```

as

```text
b

↓

l

↓

u

↓

e
```

Each character is added separately.

---

# Dry Run

Initially

```python
[
'red',
'green'
]
```

Python reads

```python
"blue"
```

Character 1

```text
b
```

Append

↓

Character 2

```text
l
```

Append

↓

Character 3

```text
u
```

Append

↓

Character 4

```text
e
```

Append

Final list

```python
[
'red',
'green',
'b',
'l',
'u',
'e'
]
```

---

# Memory Diagram

Before

```text
red

green
```

↓

Python opens

```text
blue
```

↓

```text
b

l

u

e
```

↓

Final

```text
red

green

b

l

u

e
```

---

# Example 7 — Treat String as One Element

Suppose we want

```python
[
'red',
'green',
'blue'
]
```

instead of

```python
[
'red',
'green',
'b',
'l',
'u',
'e'
]
```

We simply wrap the string inside a list.

```python
more_chars = ["red", "green"]

more_chars.extend(["blue"])

print(more_chars)
```

Output

```python
['red', 'green', 'blue']
```

---

# Why?

Python receives

```python
["blue"]
```

The iterable contains only

```text
one element
```

namely

```python
"blue"
```

Therefore

only one string is appended.

---

# `"blue"` vs `["blue"]`

This is an extremely important interview question.

| Statement | Output |
|-----------|--------|
| `extend("blue")` | `['b','l','u','e']` |
| `extend(["blue"])` | `['blue']` |

---

# Visual Comparison

### Case 1

```python
extend("blue")
```

Python sees

```text
b

l

u

e
```

---

### Case 2

```python
extend(["blue"])
```

Python sees

```text
blue
```

as one element.

---

# `append()` vs `extend()` Revisited

Example

```python
numbers = [1,2]
```

### Using append

```python
numbers.append([3,4])
```

Output

```python
[1,2,[3,4]]
```

---

### Using extend

```python
numbers = [1,2]

numbers.extend([3,4])
```

Output

```python
[1,2,3,4]
```

---

# Summary Table

| Statement | Result |
|-----------|--------|
| `append(10)` | Adds one integer |
| `append([10])` | Adds one list |
| `extend([10])` | Adds integer 10 |
| `extend("abc")` | Adds `a`, `b`, `c` |
| `extend(["abc"])` | Adds `"abc"` as one element |
| `extend(10)` | ❌ TypeError |

---

# Common Mistakes

### Mistake 1

```python
numbers.extend(10)
```

❌ Invalid

---

### Mistake 2

Expecting

```python
extend("hello")
```

to add

```python
"hello"
```

It actually adds

```python
'h'

'e'

'l'

'l'

'o'
```

---

### Mistake 3

Using

```python
append([3,4])
```

when you really wanted

```python
extend([3,4])
```

---

# Interview Questions

## Q1. Why does `extend()` require an iterable?

Because Python processes the argument element by element.

---

## Q2. Why does

```python
extend(11)
```

fail?

Because an integer is **not iterable**.

---

## Q3. What is the output?

```python
a = []

a.extend("abc")

print(a)
```

Answer

```python
['a','b','c']
```

---

## Q4. What is the output?

```python
a=[]

a.extend(["abc"])

print(a)
```

Answer

```python
['abc']
```

---

## Q5. Which method is better for combining two lists?

Generally,

```python
extend()
```

because it appends each element individually instead of creating a nested list.

---

# Key Takeaways

- `extend()` requires an iterable.
- Integers cannot be passed directly to `extend()`.
- Wrapping a value inside a list makes it iterable.
- Strings are iterable character by character.
- `extend("blue")` and `extend(["blue"])` produce different results.
- Understanding the difference between `append()` and `extend()` is essential for Python interviews and writing clean code.

---

# End of Part 3

**➡️ Next Part:** Complete guide to the `insert()` method—syntax, inserting at a specific index, shifting elements, out-of-range positive indices, negative indices, detailed dry runs, and every classroom example from the lecture.
=================================================================================================================================================================================================================================================

# Lecture 26 - Part 4

# The `insert()` Method

## Table of Contents

- Introduction
- Why Do We Need `insert()`?
- Syntax
- How `insert()` Works
- Example 1
- Dry Run
- Memory Diagram
- Positive Out-of-Range Index
- Negative Out-of-Range Index
- Internal Working
- Comparison with `append()`
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

So far, we have learned two methods for adding elements to a list.

- `append()` → Adds an element at the **end** of the list.
- `extend()` → Adds **multiple elements** from an iterable to the end of the list.

But what if we want to insert an element at a **specific position**?

Example

Suppose we have

```python
numbers = [2, 3, 7, 9]
```

and we want to insert

```python
5
```

between

```text
3

and

7
```

Neither `append()` nor `extend()` can do this.

Python provides another method called

```python
insert()
```

---

# Purpose

The `insert()` method inserts an element at a **specified index**.

If elements already exist at that position,

Python shifts them one position to the right.

---

# Syntax

```python
list_name.insert(index, value)
```

where

- `index` → Position where the element should be inserted.
- `value` → Element to insert.

---

# How `insert()` Works

Suppose we have

```python
numbers = [2,3,7,9]
```

Python executes

```python
numbers.insert(2,5)
```

Python performs

```text
Locate index 2

↓

Shift all elements from index 2 onwards

↓

Create one empty position

↓

Store 5

↓

Increase list size
```

---

# Example 1

```python
nums = [2, 3, 7, 9]

nums.insert(2, 5)

print(nums)
```

Output

```python
[2, 3, 5, 7, 9]
```

---

# Step-by-Step Dry Run

Initially

```python
nums = [2,3,7,9]
```

Memory

```text
Index

0 → 2

1 → 3

2 → 7

3 → 9
```

Python executes

```python
nums.insert(2,5)
```

Current element at index

```text
2
```

is

```text
7
```

Python shifts

```text
7

↓

9
```

one position to the right.

Memory becomes

```text
0 → 2

1 → 3

2 → Empty

3 → 7

4 → 9
```

Now Python stores

```text
5
```

at index

```text
2
```

Final list

```python
[2,3,5,7,9]
```

---

# Visual Representation

Before

```text
+----+----+----+----+

|2 |3 |7 |9 |

+----+----+----+----+
```

↓

Insert

```python
5
```

at

```text
Index 2
```

↓

After

```text
+----+----+----+----+----+

|2 |3 |5 |7 |9 |

+----+----+----+----+----+
```

---

# Important Observation

Unlike

```python
append()
```

which always inserts at the end,

```python
insert()
```

can insert **anywhere**.

Beginning

```python
insert(0,value)
```

Middle

```python
insert(3,value)
```

End

```python
insert(len(list),value)
```

---

# Example 2 — Large Positive Index

The lecture demonstrates that `insert()` is very forgiving when the specified index is larger than the list length.

```python
nums = [2, 3, 5, 7, 9]

nums.insert(100, 12)

print(nums)
```

Output

```python
[2, 3, 5, 7, 9, 12]
```

---

# Why?

The list contains only

```text
5
```

elements.

Valid indices

```text
0

1

2

3

4
```

But we supplied

```text
100
```

Instead of generating an error,

Python automatically places the element at the **end**.

---

# Internal Working

Python interprets

```python
insert(100,12)
```

as

```text
Index is larger than list size

↓

Insert at last position
```

---

# Important Rule

Unlike normal indexing,

```python
insert()
```

does **not** raise

```text
IndexError
```

for a large positive index.

---

# Example 3 — Large Negative Index

```python
nums = [2, 3, 5, 7, 9, 12]

nums.insert(-50, 1)

print(nums)
```

Output

```python
[1, 2, 3, 5, 7, 9, 12]
```

---

# Why?

Normally,

negative indices count from the end.

Example

```text
-1

↓

Last element
```

But

```text
-50
```

is much smaller than the valid range.

Instead of generating an error,

Python inserts the element at the **beginning**.

---

# Memory Diagram

Before

```text
2

3

5

7

9

12
```

↓

Insert

```python
1
```

at

```text
-50
```

↓

After

```text
1

2

3

5

7

9

12
```

---

# Index Behavior Summary

| Index Passed | Result |
|--------------|--------|
| `0` | Insert at beginning |
| Valid index | Insert at that position |
| `len(list)` | Insert at end |
| Large positive index | Insert at end |
| Large negative index | Insert at beginning |

---

# `append()` vs `insert()`

| `append()` | `insert()` |
|------------|------------|
| Always adds at end | Adds at any position |
| One argument | Two arguments |
| Faster | Slightly slower because elements may need to shift |

---

# Time Complexity

### `append()`

Usually

```text
O(1)
```

because it adds at the end.

---

### `insert()`

Worst case

```text
O(n)
```

because many elements may need to shift to the right.

Example

```python
numbers.insert(0,100)
```

Every existing element shifts one position.

---

# Common Mistakes

### Mistake 1

Thinking

```python
insert()
```

replaces an element.

Wrong.

It inserts a new element and shifts existing elements.

---

### Mistake 2

Expecting

```python
insert(100,value)
```

to produce

```text
IndexError
```

It does not.

---

### Mistake 3

Confusing

```python
append()
```

and

```python
insert()
```

Remember

```python
append()
```

always works at the end.

---

### Mistake 4

Using

```python
insert()
```

when

```python
append()
```

is sufficient.

`append()` is generally faster.

---

# Interview Questions

## Q1. What is the syntax of `insert()`?

```python
list.insert(index, value)
```

---

## Q2. Does `insert()` replace an element?

No.

It inserts a new element and shifts the remaining elements.

---

## Q3. What happens if the index is larger than the list size?

Python appends the element at the end.

---

## Q4. What happens if the index is a very large negative number?

Python inserts the element at the beginning.

---

## Q5. Which is faster, `append()` or `insert()`?

Usually,

```python
append()
```

because it normally does not shift existing elements.

---

# Key Takeaways

- `insert()` inserts an element at a specific position.
- Existing elements shift to the right.
- Large positive indices insert at the end.
- Large negative indices insert at the beginning.
- `insert()` never raises an `IndexError` for out-of-range indices.
- `append()` is generally faster than `insert()`.

---

# End of Part 4

**➡️ Next Part:** `index()` and `count()` methods—searching for elements, handling duplicates, `ValueError`, case sensitivity, counting occurrences, complete dry runs, edge cases, and interview questions.
=======================================================================================================================================================================================================================

# Lecture 26 - Part 5

# Searching Elements in a List - `index()` and `count()`

## Table of Contents

- Introduction
- The `index()` Method
- Syntax
- Finding the First Occurrence
- Duplicate Elements
- Case Sensitivity
- Handling Missing Elements
- The `count()` Method
- Counting Frequency
- Difference Between `index()` and `count()`
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

Till now, we have learned how to **add elements** into a list using

- `append()`
- `extend()`
- `insert()`

Now let's learn how to **search** for elements inside a list.

Python provides two important methods for this purpose:

- `index()` → Finds the position of an element.
- `count()` → Counts how many times an element appears.

Although both methods search for values, they serve different purposes.

---

# The `index()` Method

## Purpose

The `index()` method searches for a value inside a list and returns the **index of its first occurrence**.

If the same value appears multiple times, only the first matching index is returned.

---

# Syntax

```python
list_name.index(value)
```

---

# Example 1

```python
fruits = ["apple", "banana", "cherry", "banana"]

print(fruits.index("cherry"))
```

Output

```python
2
```

---

# Dry Run

Initially

```python
fruits = [
"apple",
"banana",
"cherry",
"banana"
]
```

Python starts searching from the beginning.

```text
Index 0

↓

apple

Is it cherry?

No.
```

↓

```text
Index 1

↓

banana

Is it cherry?

No.
```

↓

```text
Index 2

↓

cherry

Match Found
```

Python immediately stops searching and returns

```python
2
```

---

# Memory Diagram

```text
Index

0 → apple

1 → banana

2 → cherry

3 → banana
```

Searching for

```python
"cherry"
```

↓

Result

```python
2
```

---

# Duplicate Elements

Consider

```python
fruits = ["apple", "banana", "cherry", "banana"]

print(fruits.index("banana"))
```

Output

```python
1
```

---

# Why Doesn't It Return 3?

The list contains

```text
banana
```

twice.

```text
Index 1

↓

banana
```

and

```text
Index 3

↓

banana
```

The `index()` method always returns the **first occurrence**.

As soon as Python finds the first match, it stops searching.

---

# Dry Run

Python checks

```text
Index 0

↓

apple

No
```

↓

```text
Index 1

↓

banana

Yes
```

Search ends immediately.

Returned value

```python
1
```

The element at index `3` is never checked because the required value has already been found.

---

# Important Rule

`index()` **never returns all matching indices**.

It returns **only the first occurrence**.

---

# Case Sensitivity

Strings in Python are **case-sensitive**.

Example

```python
fruits = ["apple", "banana", "cherry"]

print(fruits.index("Apple"))
```

Output

```text
ValueError:
'Apple' is not in list
```

---

# Why?

Python considers

```python
"apple"
```

and

```python
"Apple"
```

to be different strings.

Comparison

```text
apple == Apple
```

Result

```python
False
```

Therefore,

Python cannot find

```python
"Apple"
```

inside the list.

---

# Searching for a Missing Element

Suppose we write

```python
numbers = [10,20,30]

print(numbers.index(50))
```

Output

```text
ValueError:
50 is not in list
```

---

# Why Does This Error Occur?

Python searches every element.

```text
10

↓

20

↓

30
```

None of them match

```text
50
```

Since the element does not exist,

Python raises

```text
ValueError
```

---

# Internal Working of `index()`

```text
Start from index 0

↓

Compare value

↓

Match?

↓

Yes → Return index immediately

↓

No → Check next element

↓

End of list?

↓

Yes → Raise ValueError
```

---

# The `count()` Method

## Purpose

The `count()` method counts how many times a particular value appears in a list.

Unlike `index()`, it does **not stop** after finding the first occurrence.

It checks the **entire list**.

---

# Syntax

```python
list_name.count(value)
```

---

# Example

```python
letters = ["i", "e", "i", "j", "i"]

print(letters.count("i"))
```

Output

```python
3
```

---

# Dry Run

Initially

```python
[
'i',
'e',
'i',
'j',
'i'
]
```

Python checks every element.

```text
Index 0

↓

i

Count = 1
```

↓

```text
Index 1

↓

e

Count = 1
```

↓

```text
Index 2

↓

i

Count = 2
```

↓

```text
Index 3

↓

j

Count = 2
```

↓

```text
Index 4

↓

i

Count = 3
```

Search completes.

Final answer

```python
3
```

---

# Memory Diagram

```text
Index

0 → i ✓

1 → e

2 → i ✓

3 → j

4 → i ✓
```

Total matches

```python
3
```

---

# Searching for a Missing Element

```python
letters = ["i","e","i","j","i"]

print(letters.count("z"))
```

Output

```python
0
```

---

# Why No Error?

Unlike `index()`,

`count()` never raises an exception if the value is absent.

Instead,

it simply returns

```python
0
```

because there are zero matching elements.

---

# `index()` vs `count()`

| Feature | `index()` | `count()` |
|----------|-----------|-----------|
| Purpose | Finds the position | Counts occurrences |
| Return Type | Integer (index) | Integer (frequency) |
| Stops at First Match | ✅ Yes | ❌ No |
| Searches Entire List | ❌ No | ✅ Yes |
| Missing Value | Raises `ValueError` | Returns `0` |

---

# Example Comparison

```python
numbers = [5,2,5,7,5]
```

```python
numbers.index(5)
```

Output

```python
0
```

---

```python
numbers.count(5)
```

Output

```python
3
```

---

# Time Complexity

### `index()`

Worst Case

```text
O(n)
```

because Python may need to check every element.

---

### `count()`

Always

```text
O(n)
```

because it must scan the entire list to count all occurrences.

---

# Common Mistakes

## Mistake 1

Expecting

```python
index()
```

to return every matching position.

It returns only the **first occurrence**.

---

## Mistake 2

Using

```python
index()
```

without checking whether the value exists.

If the value is absent,

Python raises

```text
ValueError
```

---

## Mistake 3

Thinking

```python
count()
```

returns an index.

It returns the **frequency**, not the position.

---

## Mistake 4

Ignoring case sensitivity.

```python
"Apple"
```

and

```python
"apple"
```

are different strings.

---

# Interview Questions

## Q1. What does `index()` return?

The index of the **first occurrence** of the specified value.

---

## Q2. What happens if the value is not present?

`index()` raises a

```text
ValueError
```

---

## Q3. What does `count()` return?

The number of times the value appears in the list.

---

## Q4. What does

```python
["a","b","a"].count("c")
```

return?

```python
0
```

---

## Q5. Which method should be used to find duplicates?

```python
count()
```

because it counts occurrences.

---

# Key Takeaways

- `index()` returns the index of the first matching element.
- `index()` raises a `ValueError` if the element is absent.
- `count()` counts the total occurrences of a value.
- `count()` returns `0` when the value is not found.
- Both methods perform a linear search through the list.
- `index()` stops after the first match, whereas `count()` scans the entire list.

---

# End of Part 5

**➡️ Next Part:** `remove()`, `pop()`, and `clear()` methods—removing elements by value and by index, returned values, exceptions (`ValueError` and `IndexError`), detailed dry runs, comparison tables, and all classroom examples.
===============================================================================================================================================================================================================================================

# Lecture 26 - Part 6

# Removing Elements from a List - `remove()`, `pop()` and `clear()`

## Table of Contents

- Introduction
- The `remove()` Method
- Syntax
- Removing the First Occurrence
- Missing Element (`ValueError`)
- The `pop()` Method
- Removing by Index
- Default Behavior of `pop()`
- Missing Index (`IndexError`)
- The `clear()` Method
- Difference Between `remove()`, `pop()` and `clear()`
- Time Complexity
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

Until now, we have learned how to

- Add elements
- Search elements

The next important operation is **removing elements** from a list.

Python provides three important methods for deletion:

- `remove()` → Removes an element by **value**
- `pop()` → Removes an element by **index**
- `clear()` → Removes **all elements**

Although all three delete elements, they behave differently.

---

# The `remove()` Method

## Purpose

The `remove()` method removes the **first occurrence** of the specified value from the list.

If the same value appears multiple times, only the **first matching element** is removed.

---

# Syntax

```python
list_name.remove(value)
```

---

# Example 1

```python
items = ["physics", "math", "chemistry", "math"]

items.remove("math")

print(items)
```

Output

```python
['physics', 'chemistry', 'math']
```

---

# Step-by-Step Dry Run

Initially

```python
items = [
"physics",
"math",
"chemistry",
"math"
]
```

Python starts searching from index `0`.

```text
physics

↓

Not matched
```

↓

```text
math

↓

Matched
```

Python removes this element immediately.

The remaining elements shift one position to the left.

Final list

```python
[
'physics',
'chemistry',
'math'
]
```

Notice that the second `"math"` is **not removed**.

---

# Memory Diagram

Before

```text
Index

0 → physics

1 → math

2 → chemistry

3 → math
```

↓

Remove

```python
"math"
```

↓

After

```text
Index

0 → physics

1 → chemistry

2 → math
```

---

# Important Rule

`remove()` always deletes the **first occurrence** only.

Example

```python
numbers = [5,2,5,7,5]

numbers.remove(5)

print(numbers)
```

Output

```python
[2,5,7,5]
```

Only the first `5` is removed.

---

# Removing a Missing Element

```python
items = ["physics", "math"]

items.remove("maths")
```

Output

```text
ValueError

list.remove(x): x not in list
```

---

# Why?

Python searches the complete list.

Since

```python
"maths"
```

is not found,

Python raises

```text
ValueError
```

---

# Internal Working of `remove()`

```text
Start searching

↓

Match found?

↓

Yes

↓

Delete first occurrence

↓

Shift remaining elements

↓

Stop searching
```

---

# Return Value

Like many list methods,

```python
remove()
```

returns

```python
None
```

It modifies the original list directly.

---

# The `pop()` Method

## Purpose

The `pop()` method removes an element using its **index**.

Unlike `remove()`, it also **returns** the removed element.

---

# Syntax

```python
list_name.pop(index)
```

The index is optional.

---

# Example 2

```python
basket = ["apple", "banana", "cherry"]

popped_item = basket.pop(1)

print(popped_item)

print(basket)
```

Output

```python
banana

['apple', 'cherry']
```

---

# Dry Run

Initially

```python
basket = [
"apple",
"banana",
"cherry"
]
```

Python executes

```python
basket.pop(1)
```

Index `1`

↓

```text
banana
```

is removed.

The remaining elements shift left.

Returned value

```python
banana
```

Updated list

```python
[
'apple',
'cherry'
]
```

---

# Memory Diagram

Before

```text
0 → apple

1 → banana

2 → cherry
```

↓

Pop

```text
Index 1
```

↓

After

```text
0 → apple

1 → cherry
```

Returned

```text
banana
```

---

# Default Behavior of `pop()`

If no index is supplied,

Python automatically uses

```python
-1
```

which represents the last element.

---

# Example 3

```python
basket = ["apple", "banana", "cherry"]

last_item = basket.pop()

print(last_item)

print(basket)
```

Output

```python
cherry

['apple', 'banana']
```

---

# Why?

Internally,

Python executes

```python
basket.pop(-1)
```

Therefore,

the last element is removed.

---

# Invalid Index

```python
basket = ["apple", "banana"]

basket.pop(10)
```

Output

```text
IndexError

pop index out of range
```

---

# Why?

Valid indices are

```text
0

1
```

There is no element at index

```text
10
```

Therefore,

Python raises

```text
IndexError
```

---

# Internal Working of `pop()`

```text
Receive index

↓

Is index valid?

↓

Yes

↓

Remove element

↓

Shift remaining elements

↓

Return removed value
```

---

# The `clear()` Method

## Purpose

The `clear()` method removes **every element** from the list.

After calling `clear()`,

the list becomes empty.

---

# Syntax

```python
list_name.clear()
```

---

# Example

```python
data = [1,2,3]

data.clear()

print(data)
```

Output

```python
[]
```

---

# Important Observation

The list object is **not deleted**.

Only its contents are removed.

Example

```python
data = [1,2,3]

data.clear()

print(len(data))
```

Output

```python
0
```

The variable

```python
data
```

still exists.

It now refers to an empty list.

---

# Memory Diagram

Before

```text
data

↓

1

2

3
```

↓

Clear

↓

After

```text
data

↓

[]
```

---

# `remove()` vs `pop()` vs `clear()`

| Feature | `remove()` | `pop()` | `clear()` |
|----------|------------|----------|-----------|
| Removes By | Value | Index | Entire list |
| Returns Removed Value | ❌ No | ✅ Yes | ❌ No |
| Removes First Match | ✅ Yes | N/A | Removes all |
| Missing Value | `ValueError` | `IndexError` | No error |

---

# Time Complexity

| Method | Complexity |
|----------|-----------|
| `remove()` | O(n) |
| `pop()` (last element) | O(1) |
| `pop(index)` | O(n) |
| `clear()` | O(n) |

---

# Common Mistakes

## Mistake 1

Confusing

```python
remove()
```

with

```python
pop()
```

Remember

- `remove()` → value
- `pop()` → index

---

## Mistake 2

Expecting

```python
remove()
```

to remove every occurrence.

It removes only the **first occurrence**.

---

## Mistake 3

Using

```python
pop()
```

without checking whether the index exists.

This causes

```text
IndexError
```

---

## Mistake 4

Thinking

```python
clear()
```

deletes the variable.

It does not.

It only removes all elements.

---

# Interview Questions

## Q1. Which method removes an element using its value?

```python
remove()
```

---

## Q2. Which method returns the removed element?

```python
pop()
```

---

## Q3. What is the default index used by `pop()`?

```python
-1
```

---

## Q4. Which method removes all elements from a list?

```python
clear()
```

---

## Q5. Which error does `remove()` raise if the value is absent?

```text
ValueError
```

---

## Q6. Which error does `pop()` raise for an invalid index?

```text
IndexError
```

---

# Key Takeaways

- `remove()` deletes the first matching value.
- `pop()` deletes an element using its index and returns the removed element.
- `pop()` without arguments removes the last element.
- `clear()` removes every element but keeps the list object alive.
- `remove()` raises `ValueError` for a missing value.
- `pop()` raises `IndexError` for an invalid index.

---

# End of Part 6

**➡️ Next Part:** Complete comparison of `remove()`, `pop()`, and `del`, followed by `sort()` vs `sorted()`, `reverse=True`, `key=len`, mixed data type restrictions, and every classroom sorting example from the lecture.
========================================================================================================================================================================================================================================

# Lecture 26 - Part 7

# Sorting Lists - `sort()` and `sorted()`

## Table of Contents

- Introduction
- Why Sorting is Important
- The `sort()` Method
- The `sorted()` Function
- `sort()` vs `sorted()`
- Ascending Order
- Descending Order (`reverse=True`)
- Sorting Using `key`
- Sorting by String Length (`key=len`)
- Stable Sorting
- Mixed Data Type Restriction
- Time Complexity
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

One of the most common operations performed on a list is **sorting**.

Sorting arranges the elements in a particular order such as

- Ascending order
- Descending order
- Alphabetical order
- Based on string length
- Based on any custom rule

Python provides two different ways to sort data.

- `sort()` method
- `sorted()` function

Although both produce sorted data, they work differently.

---

# The `sort()` Method

## Purpose

The `sort()` method rearranges the **original list** into sorted order.

It modifies the existing list directly.

---

# Syntax

```python
list_name.sort()
```

---

# Example

```python
vowels = [4, 2, 6, 1]

vowels.sort()

print(vowels)
```

Output

```python
[1, 2, 4, 6]
```

---

# Dry Run

Initially

```python
[4,2,6,1]
```

Python rearranges the elements.

Smallest element

```text
1
```

↓

Next

```text
2
```

↓

Next

```text
4
```

↓

Largest

```text
6
```

Final list

```python
[1,2,4,6]
```

---

# Memory Diagram

Before

```text
4

2

6

1
```

↓

Sort

↓

After

```text
1

2

4

6
```

---

# Important Point

The original list itself changes.

Before

```python
[4,2,6,1]
```

After

```python
[1,2,4,6]
```

There is no separate copy.

---

# Return Value

A common mistake is expecting

```python
sort()
```

to return a sorted list.

Actually,

```python
sort()
```

returns

```python
None
```

Example

```python
numbers = [3,1,2]

result = numbers.sort()

print(result)
```

Output

```python
None
```

Correct usage

```python
numbers.sort()

print(numbers)
```

---

# The `sorted()` Function

Unlike `sort()`,

`sorted()` is a **built-in function**.

It creates a **new sorted list** while leaving the original list unchanged.

---

# Syntax

```python
sorted(iterable)
```

---

# Example

```python
vowels = [4,2,6,1]

new_vowels = sorted(vowels)

print(new_vowels)

print(vowels)
```

Output

```python
[1,2,4,6]

[4,2,6,1]
```

---

# Dry Run

Original list

```python
[4,2,6,1]
```

Python creates a copy.

Copy is sorted.

Original remains unchanged.

Result

```python
new_vowels

↓

[1,2,4,6]
```

Original

```python
vowels

↓

[4,2,6,1]
```

---

# Memory Diagram

```text
Original List

↓

[4,2,6,1]

↓

sorted()

↓

New List

↓

[1,2,4,6]
```

Notice that two different lists now exist.

---

# `sort()` vs `sorted()`

| Feature | `sort()` | `sorted()` |
|----------|----------|------------|
| Type | Method | Function |
| Original List | Modified | Unchanged |
| Returns | `None` | New sorted list |
| Memory | Uses same list | Creates new list |

---

# Ascending Order

Ascending order means

```text
Smallest

↓

Largest
```

Example

```python
numbers = [8,4,9,2]

numbers.sort()

print(numbers)
```

Output

```python
[2,4,8,9]
```

---

# Descending Order

Python provides the

```python
reverse=True
```

argument.

Example

```python
numbers = [8,4,9,2]

numbers.sort(reverse=True)

print(numbers)
```

Output

```python
[9,8,4,2]
```

---

# Internal Working

Python first sorts the list.

Then,

it reverses the sorted order.

Result

```text
Largest

↓

Smallest
```

---

# Sorting Using `key`

Sometimes we do not want alphabetical sorting.

Instead,

we want sorting based on another property.

For this,

Python provides

```python
key=
```

---

# Example - Sorting by String Length

```python
words = ["bee", "wasp", "moth", "ant"]

words.sort(key=len)

print(words)
```

Output

```python
['bee', 'ant', 'wasp', 'moth']
```

---

# Why?

Python does **not** compare the words.

Instead,

it compares their lengths.

| Word | Length |
|------|--------|
| bee | 3 |
| ant | 3 |
| wasp | 4 |
| moth | 4 |

Therefore

```python
[
'bee',
'ant',
'wasp',
'moth'
]
```

---

# Stable Sorting

Notice

```text
bee

↓

ant
```

Both have length

```text
3
```

Yet

```text
bee
```

appears first.

Why?

Because Python's sorting algorithm is **stable**.

If two elements have the same sorting key,

their original order is preserved.

---

# Descending Using `key`

```python
words = ["bee", "wasp", "moth", "ant"]

words.sort(key=len, reverse=True)

print(words)
```

Output

```python
['wasp', 'moth', 'bee', 'ant']
```

Longest words appear first.

---

# Mixed Data Type Restriction

The lecture highlights an important rule.

Python cannot compare unrelated data types.

Example

```python
data = [10, "apple", 5]

data.sort()
```

Output

```text
TypeError
```

---

# Why?

Python does not know whether

```text
10
```

is greater than

```text
apple
```

Therefore,

sorting fails.

---

# Boolean Exception

Booleans are special.

Internally,

Python treats

```python
False = 0

True = 1
```

Example

```python
data = [True, False, 2, 1]

data.sort()

print(data)
```

Output

```python
[False, True, 1, 2]
```

because

```text
False → 0

True → 1
```

---

# Time Complexity

Python uses **Timsort**, whose average and worst-case time complexity is

```text
O(n log n)
```

This makes Python's sorting highly efficient for real-world data.

---

# Common Mistakes

## Mistake 1

Writing

```python
new_list = numbers.sort()
```

`sort()` returns

```python
None
```

---

## Mistake 2

Using

```python
sort()
```

when you want to keep the original list unchanged.

Use

```python
sorted()
```

instead.

---

## Mistake 3

Trying to sort a list containing incompatible data types.

Example

```python
[1, "hello", 5]
```

This raises

```text
TypeError
```

---

## Mistake 4

Thinking

```python
reverse=True
```

sorts first.

Actually,

Python sorts normally and then reverses the result.

---

# Interview Questions

## Q1. What is the difference between `sort()` and `sorted()`?

`sort()` modifies the original list.

`sorted()` creates a new sorted list.

---

## Q2. What does `sort()` return?

```python
None
```

---

## Q3. Which argument is used for descending order?

```python
reverse=True
```

---

## Q4. Which argument allows custom sorting?

```python
key=
```

---

## Q5. Why does

```python
[10,"apple"].sort()
```

raise an error?

Because Python cannot compare integers and strings.

---

## Q6. Which sorting algorithm does Python use internally?

**Timsort**

---

# Key Takeaways

- `sort()` modifies the original list.
- `sorted()` returns a new sorted list.
- `reverse=True` sorts in descending order.
- `key=` allows custom sorting rules.
- `key=len` sorts strings by their length.
- Python sorting is stable.
- Mixed incompatible data types cannot be sorted together.
- Python uses the efficient **Timsort** algorithm.

---

# End of Part 7

**➡️ Next Part:** Classroom Exercise 1 (Extract digits from an alphanumeric string and calculate their sum) and Classroom Exercise 2 (Maintain a sorted list while accepting user input), with complete dry runs and explanations.
=============================================================================================================================================================================================================================================

# Lecture 26 - Part 8

# Classroom Exercise 1 - Extract Digits from a String and Find Their Sum

## Table of Contents

- Problem Statement
- Understanding the Problem
- Approach 1 - Using `in` Operator
- Complete Program
- Step-by-Step Dry Run
- Memory Diagram
- Time Complexity
- Approach 2 - Using `isdigit()`
- Complete Program
- Dry Run
- `isdigit()` Explained
- Comparison of Both Approaches
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Problem Statement

Write a program that accepts an **alphanumeric string** from the user.

The program should

- Extract every digit present in the string.
- Store those digits inside a list.
- Calculate the sum of all extracted digits.

---

## Example

Input

```text
ab12cd39x
```

Digits present

```text
1

2

3

9
```

List

```python
[1,2,3,9]
```

Sum

```text
15
```

---

# Approach 1 - Using the `in` Operator

The first solution checks whether each character belongs to the string

```python
"0123456789"
```

If it does,

it is converted into an integer and added to the list.

---

# Complete Program

```python
user_input = input("Enter alphanumeric values: ")

digits = []

for ch in user_input:

    if ch in "0123456789":

        digits.append(int(ch))

print("Extracted numeric list:", digits)

print("Total Sum of items:", sum(digits))
```

---

# Understanding the Logic

Suppose the input is

```text
ab12cd39x
```

Initially

```python
digits = []
```

Python starts reading the string one character at a time.

---

## Iteration 1

Character

```text
a
```

Check

```python
"a" in "0123456789"
```

Result

```python
False
```

Nothing is added.

---

## Iteration 2

Character

```text
b
```

Again

```python
False
```

---

## Iteration 3

Character

```text
1
```

Check

```python
"1" in "0123456789"
```

Result

```python
True
```

Convert

```python
int("1")
```

↓

```python
1
```

Append

```python
digits = [1]
```

---

## Iteration 4

Character

```text
2
```

Append

```python
digits = [1,2]
```

---

## Remaining Iterations

```text
c

↓

Ignored

d

↓

Ignored

3

↓

Append

9

↓

Append

x

↓

Ignored
```

Final list

```python
[1,2,3,9]
```

---

# Memory Diagram

Initially

```text
digits

↓

[]
```

↓

Read

```text
1
```

↓

```text
[1]
```

↓

Read

```text
2
```

↓

```text
[1,2]
```

↓

Read

```text
3
```

↓

```text
[1,2,3]
```

↓

Read

```text
9
```

↓

```text
[1,2,3,9]
```

---

# Calculating the Sum

Python executes

```python
sum(digits)
```

Internally

```text
1

+

2

+

3

+

9
```

↓

Answer

```text
15
```

---

# Time Complexity

Suppose the string contains

```text
n
```

characters.

Python checks each character exactly once.

Therefore

```text
Time Complexity

O(n)
```

---

# Approach 2 - Using `isdigit()`

Python strings provide a built-in method called

```python
isdigit()
```

Instead of checking

```python
"0123456789"
```

manually,

we can simply ask Python

"Is this character a digit?"

---

# Complete Program

```python
user_input = input("Enter alphanumeric values: ")

digits = []

for ch in user_input:

    if ch.isdigit():

        digits.append(int(ch))

print("Extracted numeric list:", digits)

print("Total Sum of items:", sum(digits))
```

---

# How `isdigit()` Works

Suppose

```python
ch = "5"
```

Python checks

```python
ch.isdigit()
```

Result

```python
True
```

Suppose

```python
ch = "A"
```

Result

```python
False
```

Suppose

```python
ch = "#"
```

Result

```python
False
```

Only numeric characters return

```python
True
```

---

# Dry Run

Input

```text
p7q4z
```

Initially

```python
digits = []
```

Read

```text
p
```

↓

```python
isdigit()

↓

False
```

Ignore

---

Read

```text
7
```

↓

```python
isdigit()

↓

True
```

Append

```python
7
```

---

Read

```text
q
```

Ignore

---

Read

```text
4
```

Append

---

Read

```text
z
```

Ignore

Final list

```python
[7,4]
```

Sum

```python
11
```

---

# `in` vs `isdigit()`

| Using `in` | Using `isdigit()` |
|------------|-------------------|
| Manual checking | Built-in method |
| Slightly longer | Cleaner and more readable |
| Checks against `"0123456789"` | Checks automatically |
| Beginner friendly | Preferred in real-world programs |

---

# Which Approach is Better?

Both approaches produce exactly the same output.

However,

```python
isdigit()
```

is generally preferred because

- It is easier to read.
- It clearly expresses the intention.
- It is less error-prone.
- It is a built-in Python method.

---

# Common Mistakes

## Mistake 1

Appending the character directly.

```python
digits.append(ch)
```

Result

```python
['1','2','3']
```

instead of

```python
[1,2,3]
```

Always convert using

```python
int(ch)
```

---

## Mistake 2

Trying

```python
sum(['1','2','3'])
```

This raises a

```text
TypeError
```

because `sum()` works with numbers, not strings.

---

## Mistake 3

Checking

```python
if ch == "0123456789"
```

This compares the entire string instead of checking membership.

---

## Mistake 4

Forgetting to initialize

```python
digits = []
```

before the loop.

---

# Interview Questions

## Q1. Why do we use `int(ch)` before appending?

Because input characters are strings, and we need integers for numerical calculations.

---

## Q2. Which method is preferred for checking digits?

```python
isdigit()
```

---

## Q3. What is the time complexity of this program?

```text
O(n)
```

where `n` is the length of the input string.

---

## Q4. What is the output?

```python
"A5B7".isdigit()
```

Answer

```python
False
```

because the complete string contains non-digit characters.

---

## Q5. What is the output?

```python
"7".isdigit()
```

Answer

```python
True
```

---

# Key Takeaways

- Iterate through the string one character at a time.
- Check whether each character is a digit.
- Convert digit characters to integers before storing them.
- Store extracted digits inside a list.
- Use `sum()` to calculate the total.
- `isdigit()` is the cleaner and more Pythonic solution.

---

# End of Part 8

**➡️ Next Part:** Classroom Exercise 2 – Maintain a sorted list while accepting five integers from the user using `insert()`, including complete algorithm, dry run, multiple examples, and interview questions.
=============================================================================================================================================================================================================================

# Lecture 26 - Part 9

# Classroom Exercise 2 - Maintain a Sorted List While Taking User Input

## Table of Contents

- Problem Statement
- Understanding the Problem
- Why Not Sort at the End?
- Algorithm
- Complete Program
- Step-by-Step Dry Run
- Memory Diagram
- Understanding the `inserted` Variable
- Time Complexity
- Alternative Approach
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Problem Statement

Write a Python program that accepts **5 integers** from the user.

After every input,

the number should be inserted into the correct position so that the list **always remains sorted**.

The list should **never become unsorted**.

---

## Example

Suppose the user enters

```text
30

10

40

20

50
```

The list should grow like this

```text
After 30

[30]
```

↓

```text
After 10

[10,30]
```

↓

```text
After 40

[10,30,40]
```

↓

```text
After 20

[10,20,30,40]
```

↓

```text
After 50

[10,20,30,40,50]
```

Notice that the list remains sorted **after every insertion**.

---

# Why Not Sort at the End?

One possible solution is

```python
Take all numbers

↓

Store them

↓

Call sort()
```

Although this works,

the objective of this exercise is different.

The goal is to **learn how to use the `insert()` method** effectively.

Each new number should immediately be placed at its correct position.

---

# Algorithm

For every number entered by the user:

1. Assume the number has **not** been inserted.
2. Compare it with every existing element.
3. If it is smaller than the current element:
   - Insert it before that element.
   - Mark it as inserted.
   - Stop checking further.
4. If no suitable position is found, append it at the end.

---

# Complete Program

```python
sorted_list = []

for i in range(5):

    num = int(input(f"Enter integer {i+1} of 5: "))

    inserted = False

    for index in range(len(sorted_list)):

        if num < sorted_list[index]:

            sorted_list.insert(index, num)

            inserted = True

            break

    if not inserted:

        sorted_list.append(num)

    print("Current sorted progression:", sorted_list)
```

---

# Understanding the Program

Initially

```python
sorted_list = []
```

The list is empty.

Therefore,

the first number entered will always be appended.

After that,

every new number is compared with the existing elements to find the correct position.

---

# Dry Run

## User enters

```text
30
```

Current list

```python
[]
```

There are no elements to compare.

So,

```python
append(30)
```

List becomes

```python
[30]
```

---

## User enters

```text
10
```

Current list

```python
[30]
```

Comparison

```text
10 < 30

↓

True
```

Insert at index `0`.

New list

```python
[10,30]
```

---

## User enters

```text
40
```

Current list

```python
[10,30]
```

Comparisons

```text
40 < 10

↓

False
```

↓

```text
40 < 30

↓

False
```

No suitable position found.

Append

```python
40
```

New list

```python
[10,30,40]
```

---

## User enters

```text
20
```

Current list

```python
[10,30,40]
```

Comparison

```text
20 < 10

↓

False
```

↓

```text
20 < 30

↓

True
```

Insert before

```text
30
```

New list

```python
[10,20,30,40]
```

---

## User enters

```text
50
```

Comparisons

```text
50 < 10

↓

False
```

↓

```text
50 < 20

↓

False
```

↓

```text
50 < 30

↓

False
```

↓

```text
50 < 40

↓

False
```

Append

```python
50
```

Final list

```python
[10,20,30,40,50]
```

---

# Memory Diagram

Initially

```text
[]
```

↓

Input

```text
30
```

↓

```text
[30]
```

↓

Input

```text
10
```

↓

```text
[10,30]
```

↓

Input

```text
40
```

↓

```text
[10,30,40]
```

↓

Input

```text
20
```

↓

```text
[10,20,30,40]
```

↓

Input

```text
50
```

↓

```text
[10,20,30,40,50]
```

---

# Understanding the `inserted` Variable

One of the most important parts of this program is

```python
inserted = False
```

Initially,

Python assumes that the new number has **not** been inserted.

If a suitable position is found,

```python
sorted_list.insert(index, num)

inserted = True
```

Now Python knows that the number is already in the list.

Therefore,

the final

```python
append()
```

statement is skipped.

---

# Why Do We Use `break`?

Consider

```python
20 < 30
```

The correct position has already been found.

There is no need to compare

```text
20

with

40

or

50
```

Therefore,

`break` immediately exits the loop.

This avoids unnecessary comparisons and improves efficiency.

---

# Time Complexity

Suppose the list currently contains

```text
n
```

elements.

In the worst case,

the program compares the new number with every existing element.

Therefore,

each insertion takes

```text
O(n)
```

Since we insert

```text
5
```

numbers,

the total complexity is approximately

```text
O(n²)
```

For only five numbers,

this is perfectly acceptable.

---

# Alternative Approach

Another solution is

```python
numbers = []

for i in range(5):

    num = int(input())

    numbers.append(num)

numbers.sort()

print(numbers)
```

Although this produces the same final output,

it does **not** satisfy the requirement of keeping the list sorted after **every insertion**.

Therefore,

the lecture solution using `insert()` is the correct approach.

---

# Common Mistakes

## Mistake 1

Forgetting

```python
inserted = False
```

Without this variable,

the program cannot determine whether to use `append()`.

---

## Mistake 2

Forgetting

```python
break
```

This may insert the same element multiple times or perform unnecessary comparisons.

---

## Mistake 3

Using

```python
append()
```

for every number.

The list will no longer remain sorted during insertion.

---

## Mistake 4

Calling

```python
sort()
```

after every input.

Although it works,

it is not the objective of this exercise.

The exercise is designed to practice the `insert()` method.

---

# Interview Questions

## Q1. Why is the variable `inserted` required?

It keeps track of whether the new number has already been inserted into the correct position.

---

## Q2. Why is `break` used after `insert()`?

Because once the correct position is found, no further comparisons are required.

---

## Q3. Which list method is the main focus of this exercise?

```python
insert()
```

---

## Q4. Can this program be written using `sort()`?

Yes, but it does not maintain the sorted order after every insertion.

---

## Q5. What is the worst-case time complexity of one insertion?

```text
O(n)
```

---

# Key Takeaways

- The objective is to keep the list sorted after every input.
- `insert()` is used to place the new element at the correct position.
- The `inserted` flag determines whether `append()` is required.
- `break` prevents unnecessary comparisons.
- This exercise demonstrates a practical use of the `insert()` method and linear searching.

---

# Lecture 26 Summary

In this lecture, we explored some of the most frequently used list methods in Python.

We learned how to:

- Add elements using `append()`, `extend()`, and `insert()`
- Search using `index()` and `count()`
- Remove elements using `remove()`, `pop()`, and `clear()`
- Sort lists using `sort()` and `sorted()`
- Customize sorting using `reverse=True` and `key`
- Apply these concepts through practical classroom exercises

These methods form the foundation of list manipulation and are used extensively in Python programming, coding interviews, and real-world applications.

---

# End of Lecture 26 ✅

# End of Part 1

**➡️ Next Part:** `append()` with nested lists, appending another list vs appending individual objects, accessing nested elements (`animals[3][0]`), and a complete introduction to the `extend()` method with every classroom example.
