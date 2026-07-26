
# Lecture 26 - Part 1
Slide 29

# List Comprehension - Introduction

## Table of Contents

- Introduction
- What is Comprehension?
- Why Do We Need List Comprehension?
- Different Ways to Build a List
- Example Problem
- Solution Using `for` Loop
- Solution Using `lambda` and `map()`
- Solution Using List Comprehension
- Why List Comprehension is Better
- How List Comprehension Works
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

In the previous lectures, we learned how to

- Create lists
- Add elements
- Remove elements
- Search elements
- Sort lists

In this lecture, we will learn a powerful feature of Python called **List Comprehension**.

List Comprehension is one of the most frequently used Python features because it allows us to create new lists in a concise, readable, and efficient way. :contentReference[oaicite:0]{index=0}

---

# What is Comprehension?

A **comprehension** is a Python construct that allows one sequence to be built from another sequence.

In simple words,

List Comprehension means

> Creating a new list from an existing sequence using a single line of code.

The source sequence can be

- A list
- A tuple
- A string
- A range object
- Any iterable object

Instead of writing multiple lines using loops, Python allows us to write the same logic in a much shorter form. :contentReference[oaicite:1]{index=1}

---

# Why Do We Need List Comprehension?

Suppose you want to

- convert every character of a string to lowercase,
- find squares of numbers,
- filter odd numbers,
- convert words to uppercase,

Using a normal `for` loop requires several lines of code.

List Comprehension performs the same task in a single expression.

Advantages include

- Shorter code
- Easier to read
- Less boilerplate
- Faster execution

According to the lecture, List Comprehensions are approximately

- **35% faster than a `for` loop**
- **45% faster than using `map()`** for similar operations. :contentReference[oaicite:2]{index=2}

---

# Different Ways to Build a List

The lecture introduces three different approaches to solve the same problem.

1. Using a `for` loop
2. Using `lambda` with `map()`
3. Using List Comprehension

All three produce the same output.

Only the implementation changes.

---

# Example Problem

Suppose we have the string

```python
text = "BhOPal"
```

Task:

Store every character in a list after converting it to lowercase.

Expected Output

```python
['b', 'h', 'o', 'p', 'a', 'l']
```

---

# Solution 1 - Using `for` Loop

```python
text = "BhOPal"

myList = []

for ch in text:
    myList.append(ch.lower())

print(myList)
```

Output

```python
['b', 'h', 'o', 'p', 'a', 'l']
```

This is the traditional approach shown in the lecture. :contentReference[oaicite:3]{index=3}

---

# Understanding the Program

Initially

```python
text = "BhOPal"
```

Python starts reading one character at a time.

---

## Iteration 1

Current character

```text
B
```

Convert

```python
B.lower()
```

↓

```python
'b'
```

Append

```python
['b']
```

---

## Iteration 2

Character

```text
h
```

Lowercase

```python
'h'
```

Append

```python
['b', 'h']
```

---

## Remaining Iterations

```text
O

↓

o
```

↓

```text
P

↓

p
```

↓

```text
a

↓

a
```

↓

```text
l

↓

l
```

Final list

```python
['b', 'h', 'o', 'p', 'a', 'l']
```

---

# Memory Diagram

Initially

```text
myList

↓

[]
```

↓

Read

```text
B
```

↓

```text
['b']
```

↓

Read

```text
h
```

↓

```text
['b','h']
```

↓

Read

```text
O
```

↓

```text
['b','h','o']
```

↓

Continue...

↓

```text
['b','h','o','p','a','l']
```

---

# Solution 2 - Using `lambda` and `map()`

The lecture shows another solution using the `map()` function together with a lambda expression.

```python
text = "BhOPal"

myList = list(map(lambda ch: ch.lower(), text))

print(myList)
```

Output

```python
['b', 'h', 'o', 'p', 'a', 'l']
```

This approach is shorter than a `for` loop but may be less readable for beginners. :contentReference[oaicite:4]{index=4}

---

# How `map()` Works

Python reads the string one character at a time.

For each character,

the lambda function executes

```python
lambda ch: ch.lower()
```

Example

```text
B

↓

b
```

↓

```text
h

↓

h
```

↓

```text
O

↓

o
```

The resulting characters are collected into a list using

```python
list()
```

---

# Solution 3 - Using List Comprehension

The lecture finally introduces the simplest solution.

```python
text = "BhOPal"

myList = [ch.lower() for ch in text]

print(myList)
```

Output

```python
['b', 'h', 'o', 'p', 'a', 'l']
```

This is the preferred Pythonic solution. :contentReference[oaicite:5]{index=5}

---

# Breaking Down the Statement

```python
[ch.lower() for ch in text]
```

It consists of three parts.

### Part 1

```python
ch.lower()
```

This is the expression.

It tells Python what should be stored in the new list.

---

### Part 2

```python
for ch in text
```

This tells Python

"Read one character at a time from the string."

---

### Part 3

Python automatically creates a new list and stores each generated value.

No need to write

```python
append()
```

manually.

---

# Dry Run

String

```text
BhOPal
```

Initially

```python
new_list = []
```

Python reads

```text
B
```

↓

Expression

```python
B.lower()
```

↓

```python
'b'
```

↓

Automatically added

```python
['b']
```

Next

```text
h
```

↓

```python
['b','h']
```

Next

```text
O
```

↓

```python
['b','h','o']
```

The process continues until every character has been processed.

Final Output

```python
['b','h','o','p','a','l']
```

---

# Comparison of All Three Approaches

| Method | Lines of Code | Readability | Performance |
|---------|---------------|-------------|-------------|
| `for` Loop | More | Easy | Good |
| `map()` + `lambda` | Medium | Moderate | Better |
| List Comprehension | Least | Excellent | Best (among these) |

---

# Why is List Comprehension Faster?

With a normal loop,

Python repeatedly executes

- loop control,
- method calls,
- `append()` operations.

List Comprehension performs these operations internally in optimized C code, making it faster for many common tasks.

---

# Common Mistakes

## Mistake 1

Forgetting the brackets.

Incorrect

```python
ch.lower() for ch in text
```

Correct

```python
[ch.lower() for ch in text]
```

---

## Mistake 2

Writing the `for` part first.

Incorrect

```python
[for ch in text ch.lower()]
```

Correct

```python
[ch.lower() for ch in text]
```

---

## Mistake 3

Trying to use `append()` inside a List Comprehension.

Incorrect

```python
[myList.append(ch) for ch in text]
```

A List Comprehension already creates the list automatically.

---

# Interview Questions

## Q1. What is List Comprehension?

It is a concise way of creating a new list from an existing iterable.

---

## Q2. Which sequences can be used with List Comprehension?

- Lists
- Tuples
- Strings
- Range objects
- Any iterable

---

## Q3. Which is generally faster?

- `for` loop
- `map()`
- List Comprehension

**Answer:** List Comprehension.

---

## Q4. Does List Comprehension modify the original iterable?

No.

It creates a **new list**.

---

## Q5. Which method is considered the most Pythonic?

List Comprehension.

---

# Key Takeaways

- List Comprehension creates a new list from an existing iterable.
- It produces shorter and cleaner code.
- It automatically creates the new list.
- No explicit `append()` is required.
- It is generally faster than traditional loops and `map()` for similar operations.
- It is one of the most widely used Python features.

---

# End of Part 1

➡️ **Next Part:** Syntax of List Comprehension, execution flow, expression vs iterable, optional conditions, and the complete **Squares of Numbers (1–5)** exercise using both `for` loop and List Comprehension with detailed dry runs.
=================================================================================================================================================================================================================================================

# Lecture 29 - Part 2

# Syntax of List Comprehension and Squares Example

## Table of Contents

- General Syntax
- Understanding Each Part of the Syntax
- Execution Flow
- Comparison with `for` Loop
- Exercise - Squares of Numbers (1 to 5)
- Solution Using `for` Loop
- Solution Using List Comprehension
- Step-by-Step Dry Run
- Memory Diagram
- Time Complexity
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# General Syntax of List Comprehension

The lecture introduces the general syntax of List Comprehension as follows: :contentReference[oaicite:0]{index=0}

```python
list_variable = [expression for item in iterable]
```

If filtering is required,

an optional condition can also be added.

```python
list_variable = [expression for item in iterable if condition]
```

The `if condition` part is optional.

---

# Understanding Each Part

Consider

```python
[x**2 for x in range(1,6)]
```

This statement contains three important parts.

---

## Part 1 - Expression

```python
x**2
```

This tells Python

"What should be stored in the new list?"

Every value generated by this expression becomes an element of the new list.

---

## Part 2 - Iteration

```python
for x in range(1,6)
```

This tells Python

"Read one element at a time from the iterable."

Here,

the iterable is

```python
range(1,6)
```

which generates

```text
1

2

3

4

5
```

---

## Part 3 - Optional Condition

Sometimes we don't want every element.

Example

```python
[x for x in range(10) if x % 2 == 0]
```

Only values satisfying the condition are included.

We will study this in detail later in the lecture.

---

# How List Comprehension Executes

Suppose

```python
[x**2 for x in range(1,6)]
```

Python performs the following steps.

### Step 1

Generate

```text
1
```

↓

Evaluate

```python
1**2
```

↓

Store

```python
1
```

---

### Step 2

Generate

```text
2
```

↓

Evaluate

```python
2**2
```

↓

Store

```python
4
```

---

### Step 3

Generate

```text
3
```

↓

Evaluate

```python
3**2
```

↓

Store

```python
9
```

The same process continues until the iterable is exhausted.

---

# Internal Flow

```text
Start

↓

Read one element

↓

Evaluate expression

↓

Store result in new list

↓

Next element

↓

Repeat

↓

Return completed list
```

---

# Comparison with a `for` Loop

Normal `for` loop

```python
numbers = []

for x in range(1,6):
    numbers.append(x**2)
```

List Comprehension

```python
numbers = [x**2 for x in range(1,6)]
```

Notice that

- no empty list is created manually,
- no `append()` call is required,
- Python automatically creates and fills the list.

---

# Exercise

## Problem Statement

Write a program to generate the squares of numbers from **1 to 5**, store them in a list, and display the list. :contentReference[oaicite:1]{index=1}

Expected Output

```python
[1, 4, 9, 16, 25]
```

---

# Solution Using `for` Loop

```python
squaresList = []

for i in range(1,6):
    squaresList.append(i**2)

print(squaresList)
```

---

# Understanding the Program

Initially

```python
squaresList = []
```

Python starts reading numbers from

```python
range(1,6)
```

The generated values are

```text
1

2

3

4

5
```

Each number is squared and appended to the list.

---

# Dry Run

## Iteration 1

Current value

```text
1
```

Square

```python
1**2
```

↓

```python
1
```

Append

```python
[1]
```

---

## Iteration 2

Current value

```text
2
```

Square

```python
4
```

Append

```python
[1,4]
```

---

## Iteration 3

Current value

```text
3
```

Square

```python
9
```

Append

```python
[1,4,9]
```

---

## Iteration 4

Current value

```text
4
```

Square

```python
16
```

Append

```python
[1,4,9,16]
```

---

## Iteration 5

Current value

```text
5
```

Square

```python
25
```

Append

```python
[1,4,9,16,25]
```

Final Output

```python
[1,4,9,16,25]
```

---

# Memory Diagram

Initially

```text
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
[1,4]
```

↓

Read

```text
3
```

↓

```text
[1,4,9]
```

↓

Read

```text
4
```

↓

```text
[1,4,9,16]
```

↓

Read

```text
5
```

↓

```text
[1,4,9,16,25]
```

---

# Solution Using List Comprehension

The lecture provides the same solution using List Comprehension. :contentReference[oaicite:2]{index=2}

```python
squaresList = [x**2 for x in range(1,6)]

print(squaresList)
```

Output

```python
[1,4,9,16,25]
```

---

# Dry Run

Initially,

Python creates an empty list internally.

Generate

```text
1
```

↓

Evaluate

```python
1**2
```

↓

Store

```python
1
```

Current list

```python
[1]
```

---

Generate

```text
2
```

↓

Evaluate

```python
2**2
```

↓

Store

```python
4
```

Current list

```python
[1,4]
```

---

Generate

```text
3
```

↓

Store

```python
9
```

Current list

```python
[1,4,9]
```

---

Generate

```text
4
```

↓

Store

```python
16
```

Current list

```python
[1,4,9,16]
```

---

Generate

```text
5
```

↓

Store

```python
25
```

Final list

```python
[1,4,9,16,25]
```

---

# Why Is the List Created Automatically?

One of the biggest advantages of List Comprehension is that Python internally performs the work of

```python
append()
```

for every generated value.

So,

instead of writing

```python
numbers = []

for x in range(5):
    numbers.append(x)
```

Python automatically builds the list.

---

# Time Complexity

Suppose the iterable contains

```text
n
```

elements.

Each element is processed exactly once.

Therefore,

```text
Time Complexity = O(n)
```

Space required for the new list is also

```text
O(n)
```

---

# `for` Loop vs List Comprehension

| Feature | `for` Loop | List Comprehension |
|----------|------------|-------------------|
| Lines of Code | More | Less |
| `append()` Required | ✅ Yes | ❌ No |
| Readability | Good | Excellent |
| New List Created | Manual | Automatic |
| Performance | Good | Better |

---

# Common Mistakes

## Mistake 1

Using braces instead of square brackets.

Incorrect

```python
{x**2 for x in range(5)}
```

This creates a **set**, not a list.

---

## Mistake 2

Writing

```python
[x for range(5)]
```

The `for` keyword is mandatory.

Correct

```python
[x for x in range(5)]
```

---

## Mistake 3

Confusing the expression with the iterable.

Incorrect

```python
[range(5) for x]
```

Correct

```python
[x for x in range(5)]
```

---

## Mistake 4

Thinking List Comprehension modifies an existing list.

It always creates a **new list**.

---

# Interview Questions

## Q1. What is the general syntax of List Comprehension?

```python
[expression for item in iterable]
```

---

## Q2. Which part decides what gets stored in the new list?

The **expression**.

---

## Q3. Which part generates the values?

The iterable used in the `for` clause.

---

## Q4. Is the `if` condition compulsory?

No.

It is optional.

---

## Q5. Does List Comprehension require `append()`?

No.

Python handles it automatically.

---

# Key Takeaways

- List Comprehension follows the syntax `[expression for item in iterable]`.
- The expression decides what gets stored.
- The iterable provides the input values.
- Python automatically creates and fills the list.
- It eliminates the need for manual `append()` calls.
- It is concise, readable, and efficient.

---

# End of Part 2

➡️ **Next Part:** Convert every word of a sentence to uppercase using List Comprehension, accept multiple integers using `split()`, `int()`, `sum()`, and compare the `for` loop and List Comprehension solutions with detailed dry runs.
===================================================================================================================================================================================================================================================

# Lecture 26 - Part 3

# Practical Examples of List Comprehension

## Table of Contents

- Converting Words to Uppercase
- Understanding the `split()` Method
- How List Comprehension Executes
- Example - Convert Every Word to Uppercase
- Reading Multiple Integers in One Line
- Understanding `split()`
- Understanding `int()`
- Understanding `sum()`
- Complete Program
- Step-by-Step Dry Run
- Memory Diagram
- Time Complexity
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Example 1 - Convert Every Word of a Sentence to Uppercase

One of the most practical uses of List Comprehension is processing words in a sentence.

Suppose the user enters

```python
user_input = "I love India"
```

Our objective is to convert every word into uppercase.

Expected Output

```python
['I', 'LOVE', 'INDIA']
```

The lecture first converts the sentence into a list of words using the `split()` method and then applies List Comprehension. :contentReference[oaicite:0]{index=0}

---

# Program

```python
user_input = "I love India"

uppercase_words = [word.upper() for word in user_input.split()]

print(uppercase_words)
```

Output

```python
['I', 'LOVE', 'INDIA']
```

---

# Understanding the `split()` Method

Before List Comprehension starts,

Python executes

```python
user_input.split()
```

Input

```text
"I love India"
```

Output

```python
["I", "love", "India"]
```

Notice that

- spaces are removed,
- every word becomes an element of a new list.

---

# How the List Comprehension Executes

Python now receives

```python
["I", "love", "India"]
```

The comprehension is

```python
[word.upper() for word in user_input.split()]
```

Python processes one word at a time.

---

## Iteration 1

Current word

```text
I
```

Expression

```python
"I".upper()
```

Result

```text
I
```

New list

```python
['I']
```

---

## Iteration 2

Current word

```text
love
```

Expression

```python
"love".upper()
```

Result

```text
LOVE
```

New list

```python
['I', 'LOVE']
```

---

## Iteration 3

Current word

```text
India
```

Expression

```python
"India".upper()
```

Result

```text
INDIA
```

Final list

```python
['I', 'LOVE', 'INDIA']
```

---

# Memory Diagram

Initially

```text
[]
```

↓

Read

```text
I
```

↓

```text
['I']
```

↓

Read

```text
love
```

↓

```text
['I','LOVE']
```

↓

Read

```text
India
```

↓

```text
['I','LOVE','INDIA']
```

---

# Understanding `upper()`

The method

```python
upper()
```

returns a new string where all lowercase letters are converted into uppercase.

Example

```python
"python".upper()
```

Output

```python
'PYTHON'
```

The original string remains unchanged because strings are immutable.

---

# Example 2 - Reading Multiple Integers in One Line

Normally,

if we want five integers,

we write

```python
a = int(input())
b = int(input())
c = int(input())
...
```

This is lengthy.

The lecture demonstrates a much cleaner solution using List Comprehension. :contentReference[oaicite:1]{index=1}

---

# Program

```python
numbers = [int(ch) for ch in input("Enter 5 integers: ").split()]

print("List:", numbers)

print("Sum:", sum(numbers))
```

---

# Sample Input

```text
10 20 30 40 50
```

Output

```python
List: [10, 20, 30, 40, 50]

Sum: 150
```

---

# Breaking Down the Statement

```python
[int(ch) for ch in input().split()]
```

Let's understand it step by step.

---

## Step 1 - Read Input

Suppose the user types

```text
10 20 30 40 50
```

Everything entered is initially stored as a single string.

```text
"10 20 30 40 50"
```

---

## Step 2 - Apply `split()`

Python executes

```python
split()
```

Result

```python
['10', '20', '30', '40', '50']
```

Notice that these are still **strings**, not integers.

---

## Step 3 - Execute List Comprehension

Python now processes each string.

First element

```text
'10'
```

Expression

```python
int('10')
```

Result

```python
10
```

Current list

```python
[10]
```

---

Second element

```text
'20'
```

↓

```python
20
```

Current list

```python
[10,20]
```

---

Third element

```text
'30'
```

↓

```python
30
```

Current list

```python
[10,20,30]
```

---

Fourth element

```text
'40'
```

↓

```python
40
```

Current list

```python
[10,20,30,40]
```

---

Fifth element

```text
'50'
```

↓

```python
50
```

Final list

```python
[10,20,30,40,50]
```

---

# Memory Diagram

Input

```text
"10 20 30 40 50"
```

↓

After `split()`

```python
['10','20','30','40','50']
```

↓

After `int()`

```python
[10,20,30,40,50]
```

---

# Understanding `int()`

The function

```python
int()
```

converts a numeric string into an integer.

Example

```python
int("25")
```

Output

```python
25
```

Without `int()`,

our list would become

```python
['10','20','30']
```

instead of

```python
[10,20,30]
```

---

# Understanding `sum()`

Python provides the built-in function

```python
sum()
```

to calculate the total of all numeric elements.

Example

```python
numbers = [10,20,30]

sum(numbers)
```

Result

```python
60
```

Internally,

Python performs

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

# Time Complexity

Suppose the user enters

```text
n
```

numbers.

Each number is

- split once,
- converted once,
- stored once.

Therefore,

```text
Time Complexity = O(n)
```

Space Complexity is also

```text
O(n)
```

because a new list is created.

---

# Common Mistakes

## Mistake 1

Forgetting `int()`.

Incorrect

```python
[ch for ch in input().split()]
```

Result

```python
['10','20','30']
```

Strings are stored instead of integers.

---

## Mistake 2

Trying to calculate

```python
sum(['10','20'])
```

This raises

```text
TypeError
```

because `sum()` expects numeric values.

---

## Mistake 3

Using commas in input.

Input

```text
10,20,30
```

The program expects space-separated values.

Correct input

```text
10 20 30
```

---

## Mistake 4

Using `upper` without parentheses.

Incorrect

```python
word.upper
```

Correct

```python
word.upper()
```

---

# Interview Questions

## Q1. Why is `split()` required?

It converts a sentence into a list of words.

---

## Q2. What does `upper()` return?

A new string with all letters converted to uppercase.

---

## Q3. Why do we use `int()` inside the List Comprehension?

To convert string inputs into integers.

---

## Q4. What does `sum()` return?

The total of all numeric elements in a sequence.

---

## Q5. Can List Comprehension process strings?

Yes.

Strings are iterable, so each character (or each word after `split()`) can be processed.

---

# Key Takeaways

- `split()` converts a sentence into a list of words.
- `upper()` converts every word to uppercase.
- List Comprehension can transform every element of an iterable.
- `int()` converts numeric strings into integers.
- `sum()` calculates the total of all numbers in the list.
- Combining `split()`, `int()`, and List Comprehension is a common Python pattern for handling user input.

---

# End of Part 3

➡️ **Next Part:** Filtering elements using `if` in List Comprehension, extracting odd numbers, removing vowels from a string, multiple `if` conditions, and using the `or` operator with detailed dry runs and classroom examples.
======================================================================================================================================================================================================================================

# Lecture 26 - Part 4

# Filtering Elements Using `if` in List Comprehension

## Table of Contents

- Introduction
- Adding Conditions in List Comprehension
- General Syntax
- How Filtering Works
- Exercise 1 - Extract Odd Numbers
- Dry Run
- Memory Diagram
- Exercise 2 - Remove Vowels from a String
- Step-by-Step Explanation
- Multiple `if` Conditions
- Using the `or` Operator
- Comparison of Different Conditions
- Time Complexity
- Common Mistakes
- Interview Questions
- Key Takeaways

---

# Introduction

Until now, every element from the iterable was included in the new list.

For example,

```python
[x**2 for x in range(1,6)]
```

Every value produced by

```python
range(1,6)
```

was stored.

But what if we want **only some elements**?

Examples

- Only odd numbers
- Only even numbers
- Only positive numbers
- Only uppercase letters
- Remove vowels from a string

For such cases, Python allows us to add an **`if` condition** inside the List Comprehension. :contentReference[oaicite:0]{index=0}

---

# Adding Conditions in List Comprehension

The lecture explains that a condition can be added after the `for` clause.

Only those elements for which the condition evaluates to **True** are included in the new list. :contentReference[oaicite:1]{index=1}

General Syntax

```python
[expression for item in iterable if condition]
```

---

# Understanding the Syntax

Consider

```python
[x for x in range(1,11) if x % 2 != 0]
```

It has three parts.

---

## Expression

```python
x
```

This specifies what will be stored in the new list.

---

## Iteration

```python
for x in range(1,11)
```

Python reads numbers from 1 to 10.

---

## Condition

```python
if x % 2 != 0
```

Only odd numbers satisfy this condition.

Even numbers are skipped.

---

# Execution Flow

```text
Read an element

↓

Check the condition

↓

True?

↓

Yes

↓

Evaluate expression

↓

Store in new list

↓

No

↓

Ignore the element

↓

Move to the next element
```

---

# Exercise 1 - Extract Odd Numbers

### Problem Statement

Generate all odd numbers from **1 to 10** using List Comprehension.

Program

```python
odd_numbers = [x for x in range(1,11) if x % 2 != 0]

print(odd_numbers)
```

Output

```python
[1, 3, 5, 7, 9]
```

This is one of the examples demonstrated in the lecture. :contentReference[oaicite:2]{index=2}

---

# Dry Run

Numbers generated

```text
1 2 3 4 5 6 7 8 9 10
```

---

## Number = 1

Condition

```python
1 % 2 != 0
```

↓

True

Store

```python
[1]
```

---

## Number = 2

Condition

```python
2 % 2 != 0
```

↓

False

Skip

List remains

```python
[1]
```

---

## Number = 3

Condition

```python
3 % 2 != 0
```

↓

True

Store

```python
[1,3]
```

---

Python continues in the same way.

Final list

```python
[1,3,5,7,9]
```

---

# Memory Diagram

Initially

```text
[]
```

↓

Read

```text
1
```

↓

Condition True

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

Condition False

↓

```text
[1]
```

↓

Read

```text
3
```

↓

Condition True

↓

```text
[1,3]
```

↓

Continue...

↓

```text
[1,3,5,7,9]
```

---

# Exercise 2 - Remove Vowels from a String

The lecture demonstrates another useful application of filtering.

### Problem

Remove all vowels from a string.

Program

```python
def remove_vowels(text):

    return [ch for ch in text if ch.lower() not in "aeiou"]

result = remove_vowels("I live in India")

print(result)
```

Output

```python
[' ', 'l', 'v', ' ', 'n', ' ', 'n', 'd', '']
```

*(Depending on the implementation, spaces may also appear because they are not vowels.)* :contentReference[oaicite:3]{index=3}

---

# Understanding the Program

The List Comprehension is

```python
[ch for ch in text if ch.lower() not in "aeiou"]
```

Python processes one character at a time.

---

## Character

```text
I
```

Lowercase

```text
i
```

Check

```python
i not in "aeiou"
```

↓

False

Skip

---

## Character

```text
(space)
```

A space is **not** a vowel.

Condition

↓

True

Store

```text
' '
```

---

## Character

```text
l
```

Not a vowel

↓

Store

```text
'l'
```

---

## Character

```text
i
```

Vowel

↓

Skip

---

Python continues until every character has been checked.

---

# Memory Diagram

Input

```text
I live in India
```

↓

Characters examined

```text
I

↓

Skip
```

↓

```text
(space)

↓

Keep
```

↓

```text
l

↓

Keep
```

↓

```text
i

↓

Skip
```

↓

Continue...

---

# Multiple `if` Conditions

List Comprehension can also contain more than one condition.

Example

```python
squares = [

    x**2

    for x in range(1,21)

    if x % 2 == 0

    if x % 3 == 0

]
```

Output

```python
[36, 144, 324]
```

This includes only numbers divisible by **both 2 and 3**.

Divisible numbers

```text
6

12

18
```

Squares

```text
36

144

324
```

The lecture explains that multiple `if` statements behave like a logical **AND**. :contentReference[oaicite:4]{index=4}

---

# Dry Run

Numbers

```text
1

2

3

4

5

6
```

For

```text
6
```

Check

```python
6 % 2 == 0
```

↓

True

Next

```python
6 % 3 == 0
```

↓

True

Store

```python
36
```

---

For

```text
8
```

```python
8 % 2 == 0
```

↓

True

```python
8 % 3 == 0
```

↓

False

Skip

---

# Using the `or` Operator

Suppose we want numbers divisible by **2 OR 3**.

Program

```python
numbers = [

    x

    for x in range(1,11)

    if x % 2 == 0 or x % 3 == 0

]

print(numbers)
```

Output

```python
[2,3,4,6,8,9,10]
```

This example is also covered in the lecture. :contentReference[oaicite:5]{index=5}

---

# Difference Between Multiple `if` and `or`

### Multiple `if`

```python
if condition1

if condition2
```

Equivalent to

```python
condition1 AND condition2
```

Both conditions must be true.

---

### `or`

```python
if condition1 or condition2
```

Only one condition needs to be true.

---

# Comparison Table

| Syntax | Meaning |
|---------|---------|
| `if A if B` | A **AND** B |
| `if A and B` | Same as above |
| `if A or B` | A **OR** B |

---

# Time Complexity

If the iterable contains

```text
n
```

elements,

each element is checked once.

Therefore,

```text
Time Complexity = O(n)
```

Space Complexity

```text
O(n)
```

for the newly created list.

---

# Common Mistakes

## Mistake 1

Placing the `if` before the `for`.

Incorrect

```python
[x if x % 2 == 0 for x in range(10)]
```

Correct

```python
[x for x in range(10) if x % 2 == 0]
```

---

## Mistake 2

Using `=` instead of `==`.

Incorrect

```python
if x = 5
```

Correct

```python
if x == 5
```

---

## Mistake 3

Using `not in` incorrectly.

Correct

```python
ch.lower() not in "aeiou"
```

---

## Mistake 4

Assuming skipped elements become `None`.

They are simply **not added** to the new list.

---

# Interview Questions

## Q1. What is the syntax for filtering in List Comprehension?

```python
[expression for item in iterable if condition]
```

---

## Q2. When is an element added to the list?

Only when the condition evaluates to **True**.

---

## Q3. What is the difference between

```python
if A if B
```

and

```python
if A or B
```

The first behaves like **AND**.

The second behaves like **OR**.

---

## Q4. Can multiple `if` statements be used?

Yes.

Python evaluates all of them.

---

## Q5. Does filtering modify the original iterable?

No.

It creates a new list.

---

# Key Takeaways

- `if` conditions allow filtering while creating a list.
- Only elements satisfying the condition are stored.
- Multiple `if` statements behave like a logical **AND**.
- The `or` operator allows either condition to be satisfied.
- Filtering is one of the most powerful features of List Comprehension.
- List Comprehension combines iteration, transformation, and filtering into a single readable statement.

---

# End of Part 4

➡️ **Next Part:** Using the **ternary (`if-else`) operator** inside List Comprehension, followed by all classroom exercises:
- Filter integers from a mixed list
- Word lengths excluding `"the"`
- Extract uppercase consonants
- Complete lecture summary and interview questions.
===============================================================================================================================================================

# Lecture 26 - Part 5

# Ternary Operator and List Comprehension Exercises

## Table of Contents

- Introduction to `if-else` in List Comprehension
- Syntax
- How the Ternary Operator Works
- Example - Label Numbers as Even or Odd
- Exercise 1 - Extract Only Integers from a Mixed List
- Exercise 2 - Word Lengths Excluding "the"
- Exercise 3 - Extract Uppercase Consonants
- Comparison of Different List Comprehension Styles
- Time Complexity
- Common Mistakes
- Interview Questions
- Complete Lecture Summary
- Key Takeaways

---

# Introduction to `if-else` in List Comprehension

So far, we have used List Comprehension to

- transform data,
- filter data using `if`.

But sometimes we do **not** want to discard elements.

Instead,

we want to return **one value if the condition is true** and **another value if the condition is false**.

Python provides the **ternary operator** for this purpose.

This is the final variation of List Comprehension discussed in the lecture. :contentReference[oaicite:0]{index=0}

---

# Syntax

```python
[true_value if condition else false_value for item in iterable]
```

Notice the position of `if-else`.

Unlike filtering,

the `if-else` comes **before** the `for` loop.

---

# Comparing the Two Syntaxes

### Filtering

```python
[x for x in range(10) if x % 2 == 0]
```

Only matching elements are included.

---

### Conditional Transformation

```python
["Even" if x % 2 == 0 else "Odd" for x in range(10)]
```

Every element is included,

but its value depends on the condition.

---

# Example - Label Numbers as Even or Odd

Program

```python
labels = [

    "Even" if x % 2 == 0 else "Odd"

    for x in range(1,11)

]

print(labels)
```

Output

```python
['Odd', 'Even', 'Odd', 'Even', 'Odd',
 'Even', 'Odd', 'Even', 'Odd', 'Even']
```

This example is presented in the lecture to demonstrate the ternary operator inside List Comprehension. :contentReference[oaicite:1]{index=1}

---

# Dry Run

Numbers generated

```text
1 2 3 4 5 6 7 8 9 10
```

---

## Number = 1

Condition

```python
1 % 2 == 0
```

↓

False

Store

```text
"Odd"
```

---

## Number = 2

Condition

```python
2 % 2 == 0
```

↓

True

Store

```text
"Even"
```

---

## Number = 3

↓

False

↓

```text
"Odd"
```

Python continues until all numbers are processed.

Final Output

```python
[
'Odd',
'Even',
'Odd',
'Even',
'Odd',
'Even',
'Odd',
'Even',
'Odd',
'Even'
]
```

---

# Memory Diagram

Initially

```text
[]
```

↓

Read

```text
1
```

↓

Store

```text
Odd
```

↓

```text
['Odd']
```

↓

Read

```text
2
```

↓

Store

```text
Even
```

↓

```text
['Odd','Even']
```

↓

Continue...

---

# Exercise 1 - Filter Numbers from a Mixed List

## Problem Statement

Write a function

```python
get_numbers(data)
```

that receives a list containing different data types.

Return a new list containing **only integers**.

Example Input

```python
mixed_list = [

    "Hello",

    25,

    "@",

    7,

    12,

    "Bye"

]
```

Expected Output

```python
[25, 7, 12]
```

---

# Program

```python
def get_numbers(data):

    return [

        x

        for x in data

        if type(x) == int

    ]

mixed_list = ["Hello", 25, "@", 7, 12, "Bye"]

filtered = get_numbers(mixed_list)

print(filtered)
```

This is one of the lecture exercises. :contentReference[oaicite:2]{index=2}

---

# Dry Run

Element

```text
"Hello"
```

Check

```python
type("Hello") == int
```

↓

False

Skip

---

Element

```text
25
```

↓

True

↓

Store

```python
[25]
```

---

Element

```text
@
```

↓

False

↓

Skip

---

Element

```text
7
```

↓

True

↓

```python
[25,7]
```

---

Element

```text
12
```

↓

True

↓

```python
[25,7,12]
```

Final Output

```python
[25,7,12]
```

---

# Exercise 2 - Word Lengths Excluding `"the"`

## Problem Statement

Return the length of every word in a sentence,

except the word

```text
the
```

(case-insensitive).

---

# Program

```python
def get_lengths(sentence):

    return [

        len(word)

        for word in sentence.split()

        if word.lower() != "the"

    ]

text = "Welcome to the world of Python"

lengths = get_lengths(text)

print(lengths)
```

Output

```python
[7,2,5,2,6]
```

---

# Understanding the Program

Sentence

```text
Welcome to the world of Python
```

After

```python
split()
```

↓

```python
[
'Welcome',
'to',
'the',
'world',
'of',
'Python'
]
```

Python checks every word.

Word

```text
the
```

Condition

```python
word.lower() != "the"
```

↓

False

Skipped

Remaining words contribute their lengths.

Result

```python
[7,2,5,2,6]
```

This example demonstrates combining **transformation** (`len(word)`) with **filtering** (`if`). :contentReference[oaicite:3]{index=3}

---

# Exercise 3 - Extract Uppercase Consonants

## Problem Statement

Extract only uppercase consonants from a string.

Ignore

- lowercase letters,
- vowels,
- spaces.

---

# Program

```python
def get_upper_consonants(text):

    return [

        ch

        for ch in text

        if ch.isupper()

        and ch.lower() not in "aeiou"

    ]

sample = "I Live In Bhopal"

result = get_upper_consonants(sample)

print(result)
```

Output

```python
['L','B']
```

This is the final exercise discussed in the lecture. :contentReference[oaicite:4]{index=4}

---

# Dry Run

Characters

```text
I
```

Uppercase

↓

Yes

Vowel

↓

Yes

Skip

---

Character

```text
L
```

Uppercase

↓

Yes

Consonant

↓

Yes

Store

```python
['L']
```

---

Character

```text
B
```

↓

Uppercase

↓

Consonant

↓

Store

```python
['L','B']
```

Remaining characters are skipped.

Final Output

```python
['L','B']
```

---

# Comparison of Different List Comprehension Styles

| Purpose | Syntax |
|---------|--------|
| Basic | `[expr for x in iterable]` |
| Filtering | `[expr for x in iterable if condition]` |
| Conditional (`if-else`) | `[a if condition else b for x in iterable]` |

---

# Time Complexity

Each example processes every element exactly once.

Therefore,

```text
Time Complexity = O(n)
```

Space Complexity

```text
O(n)
```

because a new list is created.

---

# Common Mistakes

## Mistake 1

Writing

```python
[x for x in iterable if else]
```

Incorrect syntax.

---

## Mistake 2

Placing `else` after the `for`.

Incorrect

```python
[x for x in range(5) if condition else value]
```

Correct

```python
[value1 if condition else value2 for x in range(5)]
```

---

## Mistake 3

Using

```python
type(x) = int
```

Use

```python
type(x) == int
```

---

## Mistake 4

Forgetting

```python
lower()
```

when comparing

```text
"The"

THE

the
```

Without `lower()`, case-insensitive comparisons will fail.

---

# Interview Questions

## Q1. What is the syntax of `if-else` in List Comprehension?

```python
[true_value if condition else false_value for item in iterable]
```

---

## Q2. Where is the `if-else` written?

Before the `for` loop.

---

## Q3. What is the difference between filtering and `if-else`?

Filtering removes elements.

`if-else` keeps every element but changes its value.

---

## Q4. Can transformation and filtering be used together?

Yes.

Example

```python
[len(word) for word in sentence.split() if word != "the"]
```

---

## Q5. Why is List Comprehension popular?

Because it is

- concise,
- readable,
- efficient,
- expressive.

---

# Lecture 26 Summary

In this lecture, we learned one of Python's most powerful features — **List Comprehension**.

We covered:

- What List Comprehension is
- Why it is preferred over traditional loops
- Basic syntax
- Creating new lists from existing iterables
- Transforming values
- Filtering elements with `if`
- Using multiple conditions
- Using `or`
- Using the ternary (`if-else`) operator
- Solving practical classroom exercises
- Processing strings, lists, and user input efficiently

List Comprehension is widely used in real-world Python programs because it combines **iteration**, **transformation**, and **filtering** into a concise and readable form.

---

# Key Takeaways

- List Comprehension creates new lists in a concise way.
- It can transform, filter, or conditionally modify elements.
- Filtering uses `if` after the `for`.
- Ternary expressions use `if-else` before the `for`.
- It often replaces lengthy `for` loops with cleaner code.
- It is considered one of the most Pythonic features.

---

# End of Lecture 26 ✅
