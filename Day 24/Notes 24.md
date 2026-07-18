
# Python Programming 🐍

# Lecture 25: List Operations, Modification & Global Functions

> **Topics Covered**
>
> - List Modification
> - Slice Assignment
> - Deleting Elements
> - List Operators (`+`, `*`)
> - Membership Operators (`in`, `not in`)
> - Practical Exercise
> - Global Functions on Lists
> - Important Interview Questions
> - Common Mistakes
> - Summary

---

# Introduction

In the previous lecture, we learned:

- What is a List?
- Creating Lists
- Accessing List Elements
- Traversing Lists
- List Slicing

In this lecture, we will learn how to **modify**, **delete**, **combine**, and **perform operations** on lists using Python's built-in operators and global functions.

Since Python lists are **mutable**, their contents can be changed even after the list has been created.

This makes lists one of the most powerful data structures in Python.

---

# Why are Lists Mutable?

Unlike

- Integer
- Float
- String
- Tuple

a list allows its elements to be changed.

Example

```python
numbers = [10,20,30]
```

Later we can change

```python
numbers[1] = 50
```

Now

```python
numbers
```

becomes

```python
[10,50,30]
```

The original list object is modified instead of creating a new one.

---

# Learning Objectives

After completing this lecture you will be able to

- Modify existing list elements
- Replace multiple elements using slicing
- Insert elements using slicing
- Delete elements
- Delete multiple elements
- Concatenate lists
- Replicate lists
- Perform membership testing
- Solve duplicate checking problems
- Use Python global functions on lists

---

# 1. List Modification

One of the biggest advantages of Python lists is that they are **mutable**.

Mutable means

> The contents of a list can be changed after it is created.

Example

```python
fruits = ["Apple","Mango","Banana"]
```

Original list

```python
['Apple', 'Mango', 'Banana']
```

We can modify any element.

---

# Modifying Elements using Index

General Syntax

```python
list_name[index] = new_value
```

Python replaces the old value stored at that index.

---

## Example 1

```python
sports = ['cricket', 'football', 'tennis']

print(sports)

sports[1] = 'volleyball'

print(sports)
```

Output

```python
['cricket', 'football', 'tennis']

['cricket', 'volleyball', 'tennis']
```

---

## Step-by-Step Explanation

Initially

```text
Index

0           1           2

↓

cricket   football   tennis
```

Python executes

```python
sports[1] = 'volleyball'
```

It locates

```text
Index = 1
```

Current value

```text
football
```

replaces it with

```text
volleyball
```

Now memory becomes

```text
0              1             2

↓

cricket    volleyball    tennis
```

Only one element changes.

The size of the list remains the same.

---

# Important Observation

The assignment

```python
sports[1] = "volleyball"
```

does **NOT**

- create another list
- increase the size
- shift elements

Instead,

Python simply replaces the existing element.

---

# Can We Assign Beyond the Last Index?

No.

Python only allows assignment to an index that already exists.

Suppose

```python
sports = ['cricket','football','tennis']
```

Length

```python
3
```

Valid indices

```text
0

1

2
```

Trying

```python
sports[3] = "volleyball"
```

produces an error.

---

# Example 2

```python
sports = ['cricket','football','tennis']

sports[3] = 'volleyball'
```

Output

```text
IndexError:
list assignment index out of range
```

---

## Why?

Python searches for

```text
Index 3
```

But the list contains only

```text
0

1

2
```

Hence

```text
IndexError
```

is raised.

---

# Important Difference

Appending

```python
sports.append("volleyball")
```

✔ Valid

because append() creates a new position.

Assignment

```python
sports[3] = "volleyball"
```

❌ Invalid

because Python expects index 3 to already exist.

---

# Interview Question

### Q1. Can we increase the size of a list using index assignment?

No.

```python
numbers = [10,20,30]

numbers[3] = 40
```

raises

```text
IndexError
```

To increase the size, use

```python
append()

insert()

extend()

slice assignment
```

---

# Memory Representation

Before modification

```text
sports

│

▼

+---------+-----------+---------+

|cricket|football|tennis|

+---------+-----------+---------+
```

After

```python
sports[1]="volleyball"
```

```text
sports

│

▼

+---------+--------------+---------+

|cricket|volleyball|tennis|

+---------+--------------+---------+
```

Only the second element changes.

---

# Key Points

- Lists are mutable.
- Existing elements can be overwritten.
- Index assignment replaces data.
- List size remains unchanged.
- Assigning beyond the last index raises `IndexError`.

---

# Common Mistakes

### Mistake 1

```python
numbers=[10,20,30]

numbers[3]=40
```

Wrong expectation

```python
[10,20,30,40]
```

Actual result

```text
IndexError
```

---

### Mistake 2

Thinking assignment inserts data.

```python
numbers[1]=100
```

It **replaces** the element instead of inserting a new one.

---

# Quick Revision

✔ Lists are mutable.

✔ Existing elements can be modified.

✔ Index assignment replaces elements.

✔ Out-of-range assignment raises `IndexError`.

---

# End of Part 1
**➡️ Next Part:** Deleting Elements from Lists using `del`, deleting slices, clearing lists, deleting the entire list variable, and all classroom examples with detailed explanations.End of Part 1

==================================================================================================================================================================

# Flexible Slice Assignment (Mutating Lists Using Slicing)

In the previous section, we learned how to modify **a single element** using indexing.

Python provides an even more powerful feature called **Slice Assignment**, which allows us to replace **multiple elements at once**.

Unlike normal indexing, slice assignment can:

- Replace multiple elements
- Increase the size of a list
- Decrease the size of a list
- Insert new elements without deleting existing ones

This is one of the unique features of Python lists and is discussed in detail in the lecture. :contentReference[oaicite:0]{index=0}

---

# What is Slice Assignment?

General Syntax

```python
list_name[start:end] = iterable
```

Unlike normal assignment,

```python
list_name[index] = value
```

slice assignment works on **multiple positions simultaneously**.

---

# Example 3 — Replacing Equal Number of Elements

```python
sports = ['cricket', 'football', 'tennis']

sports[1:3] = ['volleyball', 'snooker']

print(sports)
```

Output

```python
['cricket', 'volleyball', 'snooker']
```

---

## Dry Run

Original List

```text
Index

0          1          2

↓

cricket   football   tennis
```

Slice

```python
sports[1:3]
```

contains

```text
football

tennis
```

Python removes these two elements and inserts

```text
volleyball

snooker
```

Final List

```text
cricket

volleyball

snooker
```

Notice

- 2 elements removed
- 2 elements inserted

The size of the list remains unchanged.

---

# Memory Representation

Before

```text
+----------+-----------+---------+

|cricket|football|tennis|

+----------+-----------+---------+
```

After

```text
+----------+--------------+----------+

|cricket|volleyball|snooker|

+----------+--------------+----------+
```

---

# Example 4 — Replacing Fewer Elements with More Elements

Python allows the replacement list to contain **more elements** than the slice being replaced.

```python
sports = ['cricket', 'football', 'tennis']

sports[1:3] = [
    'volleyball',
    'snooker',
    'badminton',
    'rugby'
]

print(sports)

print(len(sports))
```

Output

```python
['cricket',
 'volleyball',
 'snooker',
 'badminton',
 'rugby']

5
```

---

## What Happened?

Original Slice

```text
football

tennis
```

Only **2 elements** were removed.

But Python inserted

```text
volleyball

snooker

badminton

rugby
```

Total inserted

```text
4 elements
```

The list automatically grows.

---

# Visual Representation

Before

```text
cricket

football

tennis
```

↓

Remove

```text
football

tennis
```

↓

Insert

```text
volleyball

snooker

badminton

rugby
```

↓

Final List

```text
cricket

volleyball

snooker

badminton

rugby
```

Length

```text
5
```

---

# Important Observation

Unlike index assignment,

slice assignment **can increase the size of a list**.

This is because Python shifts existing elements as needed.

---

# Example 5 — Zero-Deletion Insertion

This is one of the most interesting examples from the lecture.

```python
sports = ['cricket', 'football', 'tennis']

sports[1:1] = [
    'volleyball',
    'snooker',
    'badminton',
    'rugby'
]

print(sports)
```

Output

```python
[
'cricket',
'volleyball',
'snooker',
'badminton',
'rugby',
'football',
'tennis'
]
```

---

# Why Does This Work?

Look carefully at the slice.

```python
sports[1:1]
```

Start

```text
1
```

Stop

```text
1
```

The slice contains

```text
Nothing
```

Python therefore deletes

```text
0 elements
```

and inserts the new sequence at that position.

This is often called **Zero-Deletion Insertion**.

---

# Step-by-Step Dry Run

Original List

```text
cricket

football

tennis
```

Cursor Position

```text
cricket | football
```

Insert

```text
volleyball

snooker

badminton

rugby
```

Everything after index `1` shifts to the right.

Final List

```text
cricket

volleyball

snooker

badminton

rugby

football

tennis
```

---

# Visual Representation

Before

```text
Index

0          1          2

↓

cricket   football   tennis
```

Insertion Point

```text
Index 1
```

After

```text
0

1

2

3

4

5

6

↓

cricket

volleyball

snooker

badminton

rugby

football

tennis
```

Notice

No element was removed.

Existing elements simply shifted to the right.

---

# Why is Slice Assignment Powerful?

Slice assignment allows us to:

✔ Replace existing elements

✔ Remove elements

✔ Insert new elements

✔ Expand a list

✔ Shrink a list

using the **same syntax**.

---

# Comparison

| Operation | Result |
|-----------|--------|
| `sports[1] = "volleyball"` | Replaces one element |
| `sports[1:3] = [...]` | Replaces multiple elements |
| `sports[1:1] = [...]` | Inserts elements without deleting |
| `sports[1:3] = []` | Deletes elements (covered next) |

---

# Common Mistakes

### Mistake 1

Thinking

```python
sports[1:1]
```

is an error.

It is perfectly valid.

The slice is empty, so Python simply inserts the new sequence.

---

### Mistake 2

Expecting the replacement list to have the same length.

Not required.

Python allows

- shorter replacement
- longer replacement
- empty replacement

---

### Mistake 3

Using a non-iterable on the right-hand side.

Wrong

```python
sports[1:3] = 100
```

❌ Error

Correct

```python
sports[1:3] = [100]
```

---

# Interview Questions

### Q1. Can slice assignment increase the size of a list?

Yes.

Example

```python
numbers=[1,2,3]

numbers[1:2]=[10,20,30]
```

---

### Q2. Can slice assignment decrease the size of a list?

Yes.

Replacing a larger slice with a smaller iterable reduces the list size.

---

### Q3. What happens in

```python
sports[1:1]=["A","B"]
```

No elements are deleted.

The new elements are inserted at index `1`.

---

### Q4. Why is the right-hand side of slice assignment usually a list?

Because slice assignment expects an **iterable**. Lists are the most common iterable used for replacing slices.

---

# Key Takeaways

- Slice assignment modifies multiple elements simultaneously.
- The replacement iterable can be smaller, equal, or larger than the slice.
- `start == end` creates an empty slice, allowing insertion without deletion.
- Slice assignment is more flexible than index assignment.
- Python automatically shifts elements when expanding or inserting.

---

# End of Part 2
==================================================================================================================================================================

# Deleting Elements from a List

Until now, we have learned how to

- Modify list elements
- Replace slices
- Insert new elements

Now we will learn how to **delete** elements from a list.

Since Python lists are **mutable**, elements can be removed at any time.

Python provides two common ways to delete data:

1. Using the `del` keyword
2. Using slice assignment with an empty list

Both methods permanently modify the original list.

---

# Using the `del` Keyword

General Syntax

```python
del list_name[index]
```

The `del` keyword removes the element stored at the given index.

After deletion,

- the element disappears
- all remaining elements shift one position to the left
- the list size decreases by one

---

# Example 6 — Delete One Element

```python
sports = ['cricket', 'football', 'tennis']

del sports[1]

print(sports)
```

Output

```python
['cricket', 'tennis']
```

---

# Dry Run

Original List

```text
Index

0          1          2

↓

cricket   football   tennis
```

Python executes

```python
del sports[1]
```

Deleted element

```text
football
```

Remaining elements shift left.

Final List

```text
Index

0          1

↓

cricket   tennis
```

---

# Memory Representation

Before

```text
+----------+-----------+---------+

|cricket|football|tennis|

+----------+-----------+---------+
```

Delete

```text
football
```

After

```text
+----------+---------+

|cricket|tennis|

+----------+---------+
```

Notice

- List length becomes smaller.
- Python automatically adjusts the indices.

---

# Important Observation

Deleting an element does **not** leave an empty space.

Python shifts every element after the deleted position.

---

# Example 7 — Deleting an Invalid Index

```python
sports = ['cricket', 'football', 'tennis']

del sports[3]
```

Output

```text
IndexError:
list assignment index out of range
```

---

# Why?

Valid indices

```text
0

1

2
```

There is no

```text
Index 3
```

Hence Python raises

```text
IndexError
```

---

# Deleting Multiple Elements

Instead of deleting one element at a time,

Python allows deleting an entire slice.

There are two methods.

---

# Method 1 — Slice Assignment with Empty List

General Syntax

```python
list_name[start:end] = []
```

Python removes every element inside the slice.

---

# Example 8

```python
sports = [
    'cricket',
    'football',
    'tennis',
    'hockey',
    'badminton'
]

sports[1:3] = []

print(sports)
```

Output

```python
['cricket', 'hockey', 'badminton']
```

---

# Dry Run

Original List

```text
cricket

football

tennis

hockey

badminton
```

Slice

```python
sports[1:3]
```

contains

```text
football

tennis
```

Python replaces this slice with

```python
[]
```

Result

```text
cricket

hockey

badminton
```

---

# Visual Representation

Before

```text
0

1

2

3

4

↓

cricket

football

tennis

hockey

badminton
```

Delete

```text
football

tennis
```

After

```text
0

1

2

↓

cricket

hockey

badminton
```

---

# Method 2 — Using `del` with a Slice

General Syntax

```python
del list_name[start:end]
```

This produces the same result as assigning an empty list.

---

# Example 9

```python
sports = [
    'cricket',
    'football',
    'tennis',
    'hockey',
    'badminton'
]

del sports[1:3]

print(sports)
```

Output

```python
['cricket', 'hockey', 'badminton']
```

---

# Explanation

Python removes

```text
football

tennis
```

The remaining elements shift left automatically.

---

# Which Method is Better?

Both

```python
sports[1:3] = []
```

and

```python
del sports[1:3]
```

produce the same result.

However,

```python
del
```

is usually preferred because it clearly indicates deletion.

---

# Example 10 — Out-of-Bounds Slice Deletion

```python
sports = [
    'cricket',
    'football',
    'tennis',
    'hockey',
    'badminton'
]

del sports[1:10]

print(sports)
```

Output

```python
['cricket']
```

---

# Why Doesn't This Produce an Error?

Python slices are forgiving.

Requested slice

```text
1:10
```

Actual list ends at

```text
Index 4
```

Python simply deletes everything from

```text
Index 1
```

to the end of the list.

No exception is raised.

---

# Example 11 — Delete Entire List Contents

```python
sports = [
    'cricket',
    'football',
    'tennis',
    'hockey',
    'badminton'
]

sports[0:10] = []

print(sports)
```

Output

```python
[]
```

---

# Explanation

Slice

```python
0:10
```

covers the complete list.

Replacing it with

```python
[]
```

removes every element.

The list still exists, but it becomes empty.

---

# Empty List vs Deleted List

Empty List

```python
sports = []
```

or

```python
sports[0:10] = []
```

Result

```python
[]
```

The variable still exists.

You can still do

```python
sports.append("football")
```

Successfully.

---

# Example 12 — Deleting the Entire List Variable

```python
sports = ['cricket', 'football', 'tennis']

del sports
```

Now

```python
print(sports)
```

Output

```text
NameError:
name 'sports' is not defined
```

---

# Why?

This time,

Python removes the **variable itself**, not just its contents.

Memory

Before

```text
sports

↓

List Object
```

After

```text
sports

❌ Does not exist
```

Trying to access it produces

```text
NameError
```

---

# Difference Between Empty List and Deleted Variable

| Empty List | Deleted Variable |
|------------|------------------|
| `sports = []` | `del sports` |
| Variable exists | Variable removed |
| Can append new elements | Cannot access variable |
| Prints `[]` | Raises `NameError` |

---

# Common Mistakes

### Mistake 1

```python
del sports[100]
```

❌ Raises

```text
IndexError
```

---

### Mistake 2

Confusing

```python
del sports
```

with

```python
sports.clear()
```

`del sports`

removes the variable completely.

`clear()` removes only the contents.

---

### Mistake 3

Thinking

```python
del sports[1:100]
```

raises an error.

It does **not**.

Python silently truncates the slice to the available range.

---

# Interview Questions

### Q1. Does deleting an element leave an empty position?

No.

Python shifts all remaining elements to the left.

---

### Q2. Which is better?

```python
sports[1:3] = []
```

or

```python
del sports[1:3]
```

Both are correct.

`del` is generally more readable for deletion.

---

### Q3. What is the difference between

```python
sports = []
```

and

```python
del sports
```

- `sports = []` creates an empty list.
- `del sports` removes the variable itself.

---

### Q4. Does deleting an out-of-range slice raise an error?

No.

Slice deletion is safe even if the stop index exceeds the list length.

---

# Key Takeaways

- `del list[index]` removes one element.
- `del list[start:end]` removes multiple elements.
- Slice assignment with `[]` also deletes elements.
- Out-of-range slices are handled safely.
- `del list_name` removes the entire variable, causing a `NameError` if accessed later.

---

# End of Part 3
**➡️ Next Part:** List Operators (`+` and `*`) — Concatenation, Replication, TypeErrors, `list()` with strings, Boolean multiplication, and all classroom examples with detailed explanations.
================================================================================================================================================================================================

# List Operators (`+` and `*`)

Python provides several operators that can directly work with lists.

The two most commonly used operators are:

- `+` → Concatenation Operator
- `*` → Replication Operator

These operators make it easy to combine lists or repeat their contents without writing loops.

---

# 1. Concatenation Operator (`+`)

The `+` operator joins two lists together.

General Syntax

```python
new_list = list1 + list2
```

The result is a **new list** containing all the elements of the first list followed by all the elements of the second list.

The original lists remain unchanged.

---

# Example 14 — Concatenating Two Lists

```python
indoor = ['carrom', 'ludo', 'chess']
outdoor = ['cricket', 'football']

all_sports = indoor + outdoor

print(all_sports)
```

Output

```python
['carrom', 'ludo', 'chess', 'cricket', 'football']
```

---

# Dry Run

List 1

```text
carrom

ludo

chess
```

+

List 2

```text
cricket

football
```

↓

Python creates

```text
carrom

ludo

chess

cricket

football
```

Notice

Neither `indoor` nor `outdoor` changes.

Instead, Python creates a **new list**.

---

# Memory Representation

Before

```text
indoor

↓

['carrom','ludo','chess']


outdoor

↓

['cricket','football']
```

After

```text
all_sports

↓

[
'carrom',
'ludo',
'chess',
'cricket',
'football'
]
```

---

# Important Rule

The `+` operator works only when **both operands are lists**.

---

# Example 15 — Invalid Concatenation

```python
indoor = ['carrom', 'ludo', 'chess']

indoor = indoor + "table tennis"
```

Output

```text
TypeError:
can only concatenate list (not "str") to list
```

---

# Why?

Left side

```python
List
```

Right side

```python
String
```

Python cannot combine different data types using the list concatenation operator.

---

# Example 16 — Correct Way

```python
indoor = ['carrom', 'ludo', 'chess']

indoor = indoor + ["table tennis"]

print(indoor)
```

Output

```python
['carrom', 'ludo', 'chess', 'table tennis']
```

---

# Why Does This Work?

Because

```python
["table tennis"]
```

is itself a **list**.

Now both operands are lists.

```text
List

+

List
```

Therefore,

concatenation succeeds.

---

# Example 17 — Invalid Integer Concatenation

```python
nums = [10,20,30,40]

nums = nums + 60
```

Output

```text
TypeError:
can only concatenate list (not "int") to list
```

---

# Explanation

Python sees

```python
List

+

Integer
```

which is not allowed.

---

# Example 18 — Correct Way

```python
nums = [10,20,30,40]

nums = nums + [60]

print(nums)
```

Output

```python
[10,20,30,40,60]
```

---

# Important Rule

Whenever you want to add **one element** using `+`,

wrap it inside a list.

Wrong

```python
nums + 60
```

Correct

```python
nums + [60]
```

---

# Using the `list()` Function with `+`

The lecture also demonstrates an interesting use of the `list()` constructor.

Remember

```python
list()
```

expects an **iterable**.

Strings are iterable.

Integers are not.

---

# Example 19 — Invalid

```python
list(60)
```

Output

```text
TypeError:
'int' object is not iterable
```

---

# Why?

An integer cannot be traversed character by character.

Therefore,

```python
list(60)
```

is invalid.

---

# Example 20 — String to List

```python
names = ['amit', 'sumit']

names = names + list('deepak')

print(names)
```

Output

```python
['amit',
 'sumit',
 'd',
 'e',
 'e',
 'p',
 'a',
 'k']
```

---

# Dry Run

Original List

```text
amit

sumit
```

Python executes

```python
list("deepak")
```

Result

```python
['d','e','e','p','a','k']
```

Now

```python
names + ['d','e','e','p','a','k']
```

produces

```python
[
'amit',
'sumit',
'd',
'e',
'e',
'p',
'a',
'k'
]
```

---

# Important Observation

Many beginners expect

```python
['amit','sumit','deepak']
```

But Python actually converts

```python
"deepak"
```

into

```python
['d','e','e','p','a','k']
```

because strings are sequences of characters.

---

# 2. Replication Operator (`*`)

The `*` operator repeats the contents of a list multiple times.

General Syntax

```python
list_name * n
```

where

```text
n
```

is an integer.

---

# Example 22

```python
names = ['amit', 'sumit']

names = names * 2

print(names)
```

Output

```python
['amit', 'sumit', 'amit', 'sumit']
```

---

# Dry Run

Original List

```text
amit

sumit
```

Replication

```python
* 2
```

Python copies the complete list twice.

Final List

```text
amit

sumit

amit

sumit
```

---

# Memory Representation

Before

```text
['amit','sumit']
```

↓

Replication

```python
*2
```

↓

After

```text
[
'amit',
'sumit',
'amit',
'sumit'
]
```

---

# Example 23 — Invalid Replication

```python
names = ['amit', 'sumit']

names = names * 2.5
```

Output

```text
TypeError
```

---

# Why?

The replication operator accepts only an **integer**.

Float values are not allowed.

---

# Boolean Replication

In Python

```python
True
```

behaves like

```python
1
```

and

```python
False
```

behaves like

```python
0
```

---

# Example 24

```python
names = ['amit', 'sumit']

print(names * True)
```

Output

```python
['amit', 'sumit']
```

---

# Explanation

Python interprets

```python
True
```

as

```python
1
```

Therefore

```python
names * 1
```

returns the original list.

---

# Example 25

```python
names = ['amit', 'sumit']

print(names * False)
```

Output

```python
[]
```

---

# Why?

Python converts

```python
False
```

to

```python
0
```

Hence

```python
names * 0
```

returns an empty list.

---

# Summary Table

| Expression | Result |
|------------|--------|
| `list1 + list2` | Concatenates two lists |
| `list + "abc"` | ❌ TypeError |
| `list + [100]` | Adds one element (wrapped in a list) |
| `list * 3` | Repeats the list three times |
| `list * 0` | Returns `[]` |
| `list * True` | Returns original list |
| `list * False` | Returns empty list |
| `list(60)` | ❌ TypeError |
| `list("abc")` | `['a', 'b', 'c']` |

---

# Common Mistakes

### Mistake 1

```python
numbers + 50
```

❌ Invalid

Correct

```python
numbers + [50]
```

---

### Mistake 2

Thinking

```python
list("python")
```

returns

```python
["python"]
```

Correct Output

```python
['p','y','t','h','o','n']
```

---

### Mistake 3

Using a float with `*`

```python
numbers * 2.5
```

❌ Invalid

---

# Interview Questions

### Q1. Does `+` modify the original lists?

No.

It creates a **new list**.

---

### Q2. Can we concatenate a list and a string?

No.

Both operands must be lists.

---

### Q3. What is the difference between

```python
["deepak"]
```

and

```python
list("deepak")
```

```python
["deepak"]
```

contains **one string element**.

```python
list("deepak")
```

contains **six character elements**.

---

### Q4. Why does

```python
names * False
```

return an empty list?

Because

```python
False == 0
```

and repeating a list zero times produces `[]`.

---

# Key Takeaways

- `+` joins two lists and returns a new list.
- Both operands of `+` must be lists.
- `*` repeats the list a specified number of times.
- Replication requires an integer multiplier.
- Strings passed to `list()` are broken into individual characters.
- `True` behaves like `1` and `False` behaves like `0` during replication.

---

# End of Part 4

**➡️ Next Part:** Membership Operators (`in`, `not in`), classroom exercise on accepting **5 unique integers**, detailed dry run, duplicate detection using `continue`, and interview questions.
===================================================================================================================================================================================================

# Membership Operators (`in` and `not in`)

In many real-world programs, we often need to check whether an element is already present in a list.

For example,

- Is a username already registered?
- Is a roll number already stored?
- Has a product already been added to the cart?
- Is a duplicate value entered by the user?

Python provides **Membership Operators** for such situations.

The two membership operators are:

- `in`
- `not in`

These operators return a Boolean value (`True` or `False`).

---

# 1. `in` Operator

The `in` operator checks whether an element exists inside a list.

## General Syntax

```python
element in list_name
```

If the element exists,

Python returns

```python
True
```

Otherwise,

```python
False
```

---

# Example 26

```python
names = ['amit', 'sumit']

print('sumit' in names)

print('Sumit' in names)
```

Output

```python
True

False
```

---

# Dry Run

List

```text
Index

0

1

↓

amit

sumit
```

Python checks

```python
'sumit' in names
```

Comparison

```text
amit == sumit

False
```

↓

```text
sumit == sumit

True
```

Python immediately returns

```python
True
```

---

Now Python checks

```python
'Sumit' in names
```

Comparison

```text
"Sumit"

≠

"sumit"
```

Since uppercase **S** and lowercase **s** are different,

Python returns

```python
False
```

---

# Important Observation

Membership testing is **case-sensitive**.

Example

```python
"Amit"

!=

"amit"
```

Similarly,

```python
"Python"

!=

"python"
```

---

# Visual Representation

```text
names

↓

+--------+---------+

| amit | sumit |

+--------+---------+
```

Searching

```python
"sumit"
```

↓

Found

```python
True
```

Searching

```python
"Sumit"
```

↓

Not Found

```python
False
```

---

# Time Complexity

The `in` operator searches one element at a time.

Worst Case

```text
O(n)
```

where

```text
n
```

is the number of elements in the list.

---

# 2. `not in` Operator

The `not in` operator performs the opposite operation.

It checks whether an element **does not exist** inside the list.

---

## General Syntax

```python
element not in list_name
```

Returns

```python
True
```

if the element is absent.

Otherwise

```python
False
```

---

## Example

```python
names = ['amit', 'sumit']

print('deepak' not in names)

print('amit' not in names)
```

Output

```python
True

False
```

---

# Practical Classroom Exercise

## Problem Statement

Write a Python program to

- Accept **5 unique integers** from the user.
- If the user enters a duplicate value,
- display

```text
item already present
```

and ask again.

The program should stop only after collecting **five unique integers**.

This exercise demonstrates the practical use of the membership operator. :contentReference[oaicite:0]{index=0}

---

# Example 27

```python
my_ints = []

print("Enter 5 unique integers:")

while True:

    num = int(input("Enter integer: "))

    if num in my_ints:
        print("item already present")
        continue

    my_ints.append(num)

    if len(my_ints) == 5:
        break

print("Five unique values:", my_ints)
```

---

# Complete Dry Run

Initially

```python
my_ints = []
```

User enters

```text
10
```

Check

```python
10 in []
```

Result

```python
False
```

Append

```python
[10]
```

---

User enters

```text
20
```

Check

```python
20 in [10]
```

False

Append

```python
[10,20]
```

---

User enters

```text
10
```

Check

```python
10 in [10,20]
```

True

Output

```text
item already present
```

Python executes

```python
continue
```

So,

- nothing is appended
- loop starts again

List remains

```python
[10,20]
```

---

User enters

```text
30
```

List

```python
[10,20,30]
```

---

User enters

```text
40
```

List

```python
[10,20,30,40]
```

---

User enters

```text
50
```

List

```python
[10,20,30,40,50]
```

Now

```python
len(my_ints)
```

becomes

```python
5
```

Hence

```python
break
```

executes.

Final Output

```python
Five unique values:

[10,20,30,40,50]
```

---

# Why Use `continue`?

When a duplicate is found,

Python executes

```python
continue
```

This skips the remaining statements inside the loop.

Without

```python
continue
```

the duplicate would also be appended.

---

# Flow Diagram

```text
Start

↓

Read Number

↓

Already Present?

↓

Yes

↓

Print

"item already present"

↓

continue

↓

Read Again

------------------

No

↓

Append

↓

Length == 5 ?

↓

Yes

↓

Stop

↓

Print List
```

---

# Alternative Using `not in`

The same logic can be written as

```python
if num not in my_ints:

    my_ints.append(num)

else:

    print("item already present")
```

Both programs are correct.

---

# Common Mistakes

### Mistake 1

Using

```python
=
```

instead of

```python
in
```

Wrong

```python
if num = my_ints
```

Correct

```python
if num in my_ints
```

---

### Mistake 2

Ignoring case sensitivity

```python
"Amit"

!=

"amit"
```

---

### Mistake 3

Forgetting

```python
continue
```

Without `continue`, duplicate values may still be processed.

---

### Mistake 4

Using

```python
if len(my_ints) > 5
```

Correct

```python
if len(my_ints) == 5
```

---

# Interview Questions

### Q1. What does the `in` operator return?

A Boolean value:

- `True`
- `False`

---

### Q2. Is membership testing case-sensitive?

Yes.

```python
"Python"

!=

"python"
```

---

### Q3. Which operator checks for absence?

```python
not in
```

---

### Q4. Why is `continue` used in the duplicate-checking program?

It skips the remaining statements of the current iteration and immediately starts the next iteration, preventing duplicate values from being added.

---

### Q5. What is the time complexity of `in` on a list?

Worst-case complexity:

```text
O(n)
```

because Python may need to check every element.

---

# Key Takeaways

- `in` checks whether an element exists in a list.
- `not in` checks whether an element is absent.
- Membership testing returns `True` or `False`.
- Membership testing is case-sensitive.
- The `continue` statement is useful when rejecting duplicate input.
- A common application of membership operators is enforcing unique values in a list.

---

# End of Part 5

**➡️ Next Part:** Built-in Global Functions on Lists — `len()`, `max()`, `min()`, `sum()`, `sorted()`, `list()`, `any()`, `all()`, including every lecture example, edge cases, interview questions, and detailed explanations.
==================================================================================================================================================================

# Built-in Global Functions on Lists

Python provides many **built-in global functions** that work directly with lists.

These functions help us perform common operations such as

- finding the length
- finding the maximum element
- finding the minimum element
- calculating the sum
- sorting
- converting iterables into lists
- checking truth values

Unlike list methods (`append()`, `insert()`, etc.), these are **global functions**, meaning they are called by passing the list as an argument.

Example

```python
len(my_list)
```

instead of

```python
my_list.len()
```

---

# 1. `len()` Function

The `len()` function returns the total number of elements present in a list.

## Syntax

```python
len(list_name)
```

Return Type

```python
int
```

---

## Example 28

```python
print(len([1, 2, 3, 4]))
```

Output

```python
4
```

---

## Dry Run

List

```python
[1,2,3,4]
```

Python counts

```text
1

2

3

4
```

Total

```text
4
```

Hence

```python
len(...)
```

returns

```python
4
```

---

# Important Notes

An empty list

```python
[]
```

has length

```python
0
```

Example

```python
print(len([]))
```

Output

```python
0
```

---

# 2. `max()` Function

The `max()` function returns the largest element in a list.

The elements must be **comparable**.

---

## Example 29

```python
print(max([2, 11, 5, 9]))
```

Output

```python
11
```

---

## Explanation

Python compares

```text
2

11

5

9
```

Largest

```text
11
```

---

# Strings with `max()`

Python compares strings **lexicographically** (dictionary order), based on Unicode/ASCII values.

---

## Example 30

```python
print(max(['january', 'december', 'march']))
```

Output

```python
'march'
```

---

## Why?

Python compares the first differing characters.

```text
j

d

m
```

Since

```text
m
```

comes after

```text
j

and

d
```

the result is

```python
'march'
```

---

# Boolean Values

Booleans behave like integers.

```text
False = 0

True = 1
```

---

## Example 31

```python
print(max([False, True]))
```

Output

```python
True
```

---

## Why?

Internally

```text
False

↓

0

---------------

True

↓

1
```

Largest

```text
1
```

Hence

```python
True
```

---

# Invalid Comparisons

Python cannot compare incompatible data types.

---

## Example 32

```python
print(max([10, "hello"]))
```

Output

```text
TypeError
```

---

## Example 33

```python
print(max(["orange", None]))
```

Output

```text
TypeError
```

---

# Why?

Python cannot determine whether

```text
10

>

"hello"
```

or

```text
"orange"

>

None
```

Different data types cannot be compared directly.

---

# 3. `min()` Function

The `min()` function returns the smallest element.

Its rules are exactly opposite to `max()`.

---

## Example

```python
print(min([2,11,5,9]))
```

Output

```python
2
```

---

## String Example

```python
print(min(['january','december','march']))
```

Output

```python
'december'
```

because

```text
d

<

j

<

m
```

---

# 4. `sum()` Function

The `sum()` function adds all numeric elements of a list.

It works with

- Integers
- Floats
- Booleans

It does **not** work with strings.

---

## Example 34

```python
print(sum([10,20,30]))
```

Output

```python
60
```

---

## Dry Run

```text
10

+

20

+

30

=

60
```

---

## Example 35

```python
print(sum([2.5,3.5,4.5]))
```

Output

```python
10.5
```

---

# Boolean Example

```python
print(sum([True, False, True]))
```

Output

```python
2
```

Explanation

```text
True

↓

1

False

↓

0

True

↓

1
```

Total

```text
2
```

---

# Invalid Example

```python
print(sum([1,'2','3']))
```

Output

```text
TypeError
```

---

# Why?

Python cannot add

```text
Integer

+

String
```

---

# 5. `sorted()` Function

The `sorted()` function returns a **new sorted list**.

The original list remains unchanged.

---

## Example 36

```python
nums = [7,4,9,1]

sorted_nums = sorted(nums)

print(sorted_nums)

print(nums)
```

Output

```python
[1,4,7,9]

[7,4,9,1]
```

---

# Important Observation

Original list

```python
nums
```

does **not** change.

Only

```python
sorted_nums
```

contains the sorted values.

---

# Descending Order

Use

```python
reverse=True
```

---

## Example 37

```python
print(sorted([2,5,1,3], reverse=True))
```

Output

```python
[5,3,2,1]
```

---

# Difference Between `sorted()` and `sort()`

| `sorted()` | `sort()` |
|------------|----------|
| Global function | List method |
| Returns a new list | Modifies original list |
| Works with any iterable | Works only on lists |

---

# 6. `list()` Function

The `list()` constructor converts an iterable into a list.

---

## Example 38

```python
print(list("Bhopal"))
```

Output

```python
['B','h','o','p','a','l']
```

---

## Explanation

A string is iterable.

Each character becomes a separate list element.

---

## Example 39

```python
print(list((10,20,30)))
```

Output

```python
[10,20,30]
```

---

# Explanation

Tuple

```python
(10,20,30)
```

↓

Converted into

```python
[10,20,30]
```

---

# 7. `any()` Function

The `any()` function behaves like the logical **OR** operator.

It returns

```python
True
```

if **at least one** element is truthy.

---

## Example 40

```python
print(any([0, False, 5]))
```

Output

```python
True
```

---

## Why?

Values

```text
0

↓

False

False

↓

False

5

↓

True
```

At least one value is

```text
True
```

Hence

```python
True
```

---

## Example 41

```python
print(any([0, False]))
```

Output

```python
False
```

---

## Example 42

```python
print(any([]))
```

Output

```python
False
```

---

# 8. `all()` Function

The `all()` function behaves like logical **AND**.

It returns

```python
True
```

only when **every element** is truthy.

---

## Example 43

```python
print(all([1,2,3,0]))
```

Output

```python
False
```

---

## Why?

The value

```text
0
```

is falsy.

Hence

```python
False
```

---

## Example 44

```python
print(all([1,2,3,4]))
```

Output

```python
True
```

---

## Example 45

```python
print(all([]))
```

Output

```python
True
```

---

# Why Does `all([])` Return `True`?

This is a special edge case in Python.

An empty collection contains **no false values**.

Therefore,

```python
all([])
```

returns

```python
True
```

This concept is known as **vacuous truth** in logic.

---

# Summary Table

| Function | Purpose | Example | Output |
|----------|---------|---------|--------|
| `len()` | Number of elements | `len([1,2,3])` | `3` |
| `max()` | Largest element | `max([2,5,1])` | `5` |
| `min()` | Smallest element | `min([2,5,1])` | `1` |
| `sum()` | Adds numeric values | `sum([10,20])` | `30` |
| `sorted()` | Returns sorted copy | `sorted([3,1])` | `[1,3]` |
| `list()` | Converts iterable to list | `list("abc")` | `['a','b','c']` |
| `any()` | Logical OR | `any([0,1])` | `True` |
| `all()` | Logical AND | `all([1,2])` | `True` |

---

# Common Interview Questions

### Q1. Does `sorted()` modify the original list?

No.

It returns a **new sorted list**.

---

### Q2. What is the difference between `max()` and `sum()`?

- `max()` returns the largest element.
- `sum()` adds all numeric elements.

---

### Q3. Why does `sum()` fail on strings?

Because strings cannot be added numerically.

---

### Q4. Why does `any([])` return `False`?

An empty iterable contains **no truthy elements**.

---

### Q5. Why does `all([])` return `True`?

An empty iterable contains **no falsy elements**, so the condition "all elements are truthy" is considered satisfied.

---

# Key Takeaways

- `len()` counts elements.
- `max()` and `min()` require comparable values.
- `sum()` works only with numeric data types.
- `sorted()` returns a new sorted list without modifying the original.
- `list()` converts any iterable into a list.
- `any()` behaves like logical **OR**.
- `all()` behaves like logical **AND**.
- Understanding the edge cases of `any([])` and `all([])` is important for interviews.

---

# End of Part 6

**➡️ Next Part (Final):** Complete Lecture 25 revision, comparison tables, frequently asked interview questions, common errors, best practices, and a comprehensive summary of all topics covered in the lecture.
==================================================================================================================================================================

# Lecture 24 - Complete Revision & Interview Notes

Congratulations! 🎉

You have completed **Lecture 24**.

This lecture focused on **modifying lists**, **deleting elements**, **list operators**, **membership testing**, and **Python's built-in global functions**. It also included practical classroom exercises and important edge cases. :contentReference[oaicite:0]{index=0}

---

# Complete Lecture Summary

This lecture can be divided into six major sections.

## 1. List Modification

We learned that Python lists are **mutable**, which means their elements can be changed after creation.

### Single Element Modification

Syntax

```python
list_name[index] = new_value
```

Example

```python
sports = ['cricket', 'football', 'tennis']

sports[1] = 'volleyball'
```

Output

```python
['cricket', 'volleyball', 'tennis']
```

### Important Points

- Replaces the existing element.
- List length remains unchanged.
- Index must already exist.

---

## 2. Slice Assignment

General Syntax

```python
list_name[start:end] = iterable
```

Unlike normal assignment,

slice assignment can

- replace elements
- insert elements
- delete elements
- expand a list
- shrink a list

### Examples

```python
sports[1:3] = ['volleyball', 'snooker']
```

Replace two elements.

---

```python
sports[1:3] = [
    'volleyball',
    'snooker',
    'badminton',
    'rugby'
]
```

List expands automatically.

---

```python
sports[1:1] = [
    'volleyball',
    'snooker'
]
```

Nothing is deleted.

Python inserts the new elements.

---

# 3. Deleting Elements

Three methods were discussed.

---

### Delete Single Element

```python
del sports[1]
```

Deletes one element.

Remaining elements shift left.

---

### Delete Multiple Elements

```python
del sports[1:3]
```

Deletes the complete slice.

---

### Delete Using Empty Slice Assignment

```python
sports[1:3] = []
```

Produces the same result.

---

### Delete Entire List

```python
del sports
```

Variable disappears completely.

Accessing it later raises

```text
NameError
```

---

# 4. List Operators

## Concatenation (`+`)

```python
list1 + list2
```

Creates a new list.

---

Example

```python
[1,2] + [3,4]
```

Output

```python
[1,2,3,4]
```

---

### Rules

✔ Both operands must be lists.

Wrong

```python
list + 10
```

Correct

```python
list + [10]
```

---

## Replication (`*`)

```python
list * n
```

Repeats the list.

Example

```python
['A','B'] * 3
```

Output

```python
['A','B','A','B','A','B']
```

---

### Boolean Multiplication

```python
True == 1

False == 0
```

Therefore

```python
list * True
```

returns the original list.

```python
list * False
```

returns

```python
[]
```

---

# 5. Membership Operators

Two operators

```python
in

not in
```

---

Example

```python
"amit" in names
```

Returns

```python
True
```

---

Example

```python
"Rahul" not in names
```

Returns

```python
True
```

---

### Important Notes

Membership checking

- returns Boolean values
- is case-sensitive
- performs linear search on lists

---

# Classroom Exercise

Accept

```text
5 unique integers
```

If duplicate entered

```text
item already present
```

Continue asking until

```text
5
```

unique numbers are stored.

---

# 6. Global Functions

The lecture concluded with Python's built-in sequence functions.

---

## `len()`

Counts elements.

```python
len([10,20,30])
```

Output

```python
3
```

---

## `max()`

Largest element.

```python
max([2,5,9])
```

Output

```python
9
```

---

## `min()`

Smallest element.

```python
min([2,5,9])
```

Output

```python
2
```

---

## `sum()`

Adds numeric values.

```python
sum([10,20,30])
```

Output

```python
60
```

---

## `sorted()`

Returns a sorted copy.

Original list remains unchanged.

---

## `list()`

Converts iterables into lists.

```python
list("Python")
```

Output

```python
['P','y','t','h','o','n']
```

---

## `any()`

Behaves like logical **OR**.

Returns

```python
True
```

if at least one value is truthy.

---

## `all()`

Behaves like logical **AND**.

Returns

```python
True
```

only if every value is truthy.

---

# Complete Comparison Table

| Operation | Syntax | Changes Original List |
|-----------|--------|-----------------------|
| Modify Element | `list[i] = value` | ✅ Yes |
| Slice Assignment | `list[a:b] = [...]` | ✅ Yes |
| Delete Element | `del list[i]` | ✅ Yes |
| Delete Slice | `del list[a:b]` | ✅ Yes |
| Concatenate | `list1 + list2` | ❌ No |
| Replicate | `list * n` | ❌ No (returns new list) |
| Membership | `x in list` | ❌ No |
| `sorted()` | `sorted(list)` | ❌ No |
| `len()` | `len(list)` | ❌ No |
| `sum()` | `sum(list)` | ❌ No |

---

# Common Errors

## 1.

```python
numbers[3] = 40
```

Error

```text
IndexError
```

---

## 2.

```python
numbers + 40
```

Error

```text
TypeError
```

Correct

```python
numbers + [40]
```

---

## 3.

```python
numbers * 2.5
```

Error

```text
TypeError
```

---

## 4.

```python
sum([10,"20"])
```

Error

```text
TypeError
```

---

## 5.

```python
max([10,"hello"])
```

Error

```text
TypeError
```

---

## 6.

```python
list(50)
```

Error

```text
TypeError
```

---

# Frequently Asked Interview Questions

## Q1. Why are lists called mutable?

Because their contents can be modified after creation.

---

## Q2. Difference between

```python
append()
```

and

```python
+
```

| append() | + |
|-----------|---|
| Adds element to existing list | Creates a new list |
| Modifies original list | Original lists remain unchanged |

---

## Q3. Difference between

```python
del list
```

and

```python
list = []
```

| `list=[]` | `del list` |
|------------|------------|
| Creates an empty list | Deletes the variable |
| Variable still exists | Variable removed |

---

## Q4. Difference between

```python
sorted()
```

and

```python
sort()
```

| sorted() | sort() |
|-----------|---------|
| Returns new list | Modifies original list |
| Global function | List method |

---

## Q5. Why does

```python
any([])
```

return

```python
False
```

Because there are no truthy values.

---

## Q6. Why does

```python
all([])
```

return

```python
True
```

Because there are no falsy values.

---

## Q7. Which operator checks duplicate values in a list?

```python
in
```

---

## Q8. Which operator joins two lists?

```python
+
```

---

## Q9. Which operator repeats a list?

```python
*
```

---

## Q10. Can slice assignment increase the size of a list?

Yes.

Python automatically shifts elements when required.

---

# Memory Tricks for Exams

### Remember

**Index Assignment**

```text
Replace
```

---

**Slice Assignment**

```text
Replace

Insert

Delete

Expand

Shrink
```

---

**+**

```text
Join Lists
```

---

**\***

```text
Repeat Lists
```

---

**in**

```text
Search
```

---

**len()**

```text
Count
```

---

**sum()**

```text
Add
```

---

**sorted()**

```text
Sort without changing original
```

---

**any()**

```text
OR
```

---

**all()**

```text
AND
```

---

# Final Key Takeaways

- Python lists are mutable.
- Elements can be modified using indexing.
- Slice assignment is extremely flexible and supports replacement, insertion, deletion, expansion, and shrinking.
- The `del` keyword removes elements or even the entire list variable.
- The `+` operator concatenates lists, while `*` replicates them.
- Membership operators (`in`, `not in`) are commonly used for searching and duplicate detection.
- Global functions like `len()`, `max()`, `min()`, `sum()`, `sorted()`, `list()`, `any()`, and `all()` simplify common list operations.
- Understanding edge cases (`any([])`, `all([])`, out-of-range slices, and type compatibility) is important for interviews and exams.

---

# End of Lecture 24 🎉


**➡️ Next Lecture (Lecture 26):** Python **List Methods** such as `.append()`, `.extend()`, `.insert()`, `.remove()`, `.pop()`, `.clear()`, `.copy()`, `.count()`, `.index()`, `.sort()`, `.reverse()`, and more, depending on your course sequence.
