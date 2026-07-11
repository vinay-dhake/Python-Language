# Python Programming Notes – Lecture 17

# Control Statements (`break`, `continue`, `pass`) & Introduction to the `for` Loop

> **Topics Covered**
>
> - Revisiting the Vowel Checking Program
> - `while-else` with `break`
> - Case Sensitivity
> - `.lower()` Method
> - Number Guessing Game
> - `random.randint()`
> - `continue` Statement
> - Difference between `break` and `continue`
> - Infinite Loop using `continue`
> - `pass` Statement
> - Introduction to Python `for` Loop
> - Iterating over Strings
> - Iterating over Lists
> - Rewriting previous programs using `for`
> - Sequence and Iterable
>
> **Note:** These notes cover only the **first lecture** from the uploaded PDF. The **`range()` function and topics after it are intentionally excluded.**

---

# Introduction

In the previous lecture, we learned about the `while` loop, the `break` statement, and the unique `while-else` construct in Python.

This lecture begins by solving the assignment given in the previous class and then introduces two important loop control statements—`continue` and `pass`. Finally, it introduces Python's **iterator-based `for` loop**, which is significantly different from the traditional `for` loops found in languages like C, C++, and Java.

---

# 1. Checking Whether a String Contains a Vowel

## Problem Statement

Write a program to accept a string from the user and determine whether it contains **at least one vowel**.

If a vowel is found:

- Print **"String contains vowel"**
- Stop searching immediately.

If no vowel exists:

- Print **"String doesn't contain any vowel"**

---

## Algorithm

1. Accept a string from the user.
2. Start checking from index `0`.
3. Compare each character with the vowels (`a`, `e`, `i`, `o`, `u`).
4. If a vowel is found, print the message and terminate the loop using `break`.
5. If the loop finishes naturally, execute the `else` block.

---

## Program

```python
string_input = input("Enter a string: ")

i = 0
length = len(string_input)

while i < length:

    if string_input[i] in "aeiou":
        print("String contains vowel")
        break

    i += 1

else:
    print("String doesn't contain any vowel")
```

---

## How the Program Works

The loop starts from the first character of the string and checks each character one by one.

Whenever a vowel is encountered, the `break` statement immediately terminates the loop.

If no vowel is found after checking every character, the loop terminates naturally and the `else` block executes.

---

## Dry Run – Example 1

**Input**

```text
Python
```

| Index | Character | Is Vowel? |
|------:|-----------|-----------|
| 0 | P | ❌ |
| 1 | y | ❌ |
| 2 | t | ❌ |
| 3 | h | ❌ |
| 4 | o | ✅ |

At index `4`, the character `o` is found inside `"aeiou"`.

Therefore,

```python
break
```

executes immediately.

**Output**

```text
String contains vowel
```

---

## Dry Run – Example 2

**Input**

```text
cry
```

Execution

```text
c
↓

r
↓

y
↓

Loop Ends

↓

else Executes
```

**Output**

```text
String doesn't contain any vowel
```

---

# Understanding `while-else`

Many beginners think the `else` belongs to the `if` statement.

In reality, the `else` here belongs to the **`while` loop**.

The `else` block executes **only if the loop terminates naturally**.

If the loop is terminated using `break`, the `else` block is skipped completely.

This makes `while-else` useful for searching problems like this one.

---

# 2. Case Sensitivity Problem

The previous solution works only for lowercase letters.

Consider the input:

```text
BHOPAL
```

The program compares

```text
B
H
O
P
A
L
```

with

```text
aeiou
```

Since Python is **case-sensitive**,

```text
O ≠ o
A ≠ a
```

the program incorrectly reports that there are no vowels.

---

# Solution 1 – Check Both Cases

```python
if string_input[i] in "aeiouAEIOU":
```

Now both uppercase and lowercase vowels are accepted.

Examples

```text
A ✓
E ✓
I ✓
O ✓
U ✓

a ✓
e ✓
i ✓
o ✓
u ✓
```

---

# Solution 2 – Convert Everything to Lowercase (Recommended)

A cleaner solution is to convert the complete string into lowercase before processing it.

```python
string_input = input("Enter a string: ").lower()
```

Example

```text
Input

BHOPAL

↓

After lower()

bhopal
```

Now the original condition works perfectly.

```python
if string_input[i] in "aeiou":
```

---

## Why is `.lower()` Better?

Instead of checking

```python
if ch in "aeiouAEIOU":
```

we write

```python
string_input = string_input.lower()
```

and then simply write

```python
if ch in "aeiou":
```

Advantages:

- Cleaner code
- Easier to read
- Fewer comparisons
- More maintainable
==============================================================================================================================================================
# 3. Number Guessing Game (Assignment)

After discussing the vowel checking program, the instructor introduced a real-world practice problem to strengthen the understanding of loops, decision-making, and loop control statements.

Unlike previous programs, this assignment requires the program to repeatedly interact with the user until the correct answer is entered or the user decides to quit.

---

## Problem Statement

Create a **Number Guessing Game**.

### Requirements

- The computer should generate a random number.
- The user should repeatedly guess the number.
- If the guessed number is greater than the secret number, display:

```text
Guess is too large. Try Again.
```

- If the guessed number is smaller than the secret number, display:

```text
Guess is too small. Try Again.
```

- If the guessed number matches the secret number, display:

```text
Congratulations! You guessed it correctly.
```

and terminate the program.

---

## Exit Condition

If the user enters

```text
0
```

or

```text
Any Negative Number
```

the game should terminate immediately.

Display a farewell message before exiting.

Example

```text
Thank You

Game Ended
```

---

# Generating Random Numbers

To make the game interesting, the secret number should not be fixed.

Python provides a built-in module named

```python
random
```

for generating random values.

Import the module

```python
import random
```

---

## randint()

The function used in the lecture is

```python
random.randint(a, b)
```

Syntax

```python
random.randint(start, end)
```

Example

```python
import random

secret_number = random.randint(1, 25)

print(secret_number)
```

---

## Important Property

Both limits are included.

```
random.randint(1,25)
```

may generate

```text
1

7

13

25
```

Notice that

- 1 is possible
- 25 is also possible

Hence,

`randint()` generates numbers in the **inclusive range** `[start, end]`.

---

## Expected Execution

Suppose the computer secretly generated

```text
17
```

Program execution

```text
Guess Number : 25

Guess is too large.
Try Again.

Guess Number : 10

Guess is too small.
Try Again.

Guess Number : 15

Guess is too small.
Try Again.

Guess Number : 17

Congratulations!
You guessed it correctly.
```

---

## Example – User Quits

Suppose the user enters

```text
Guess Number : 0
```

Output

```text
Thank You

Game Ended
```

---

## Concepts Practiced

This single assignment combines multiple concepts studied so far.

- `while` loop
- `if-elif-else`
- `break`
- User Input
- Random Number Generation

---

## Real-Life Applications

The same concept is used in

- Quiz Games
- Lottery Simulators
- Password Guessing Games
- Puzzle Games
- Interactive Console Applications

---

# 4. The `continue` Statement

In the previous lecture, we learned about the **`break` statement**.

The `break` statement immediately terminates the loop.

Sometimes, however, we don't want to terminate the entire loop.

Instead,

we simply want to **skip the remaining statements of the current iteration** and move directly to the next iteration.

For such situations, Python provides the

```python
continue
```

statement.

---

## Difference Between `break` and `continue`

| `break` | `continue` |
|----------|------------|
| Terminates the loop immediately | Skips only the current iteration |
| Remaining loop iterations never execute | Remaining iterations continue normally |
| Control moves outside the loop | Control moves back to the loop condition |

---

## Flow of `continue`

```text
Loop Starts

↓

Condition True

↓

Execute Statements

↓

continue encountered?

↓

Yes

↓

Skip Remaining Statements

↓

Go Back to Loop Condition
```

Unlike `break`,

the loop itself is **not terminated**.

Only the current iteration ends.

---

# Example – Printing Only Even Numbers

The instructor discussed this example as a dry-run exercise.

```python
i = 0

while i < 10:

    i += 1

    if i % 2 != 0:
        continue

    print(i)
```

---

## Dry Run

Initial

```text
i = 0
```

### First Iteration

```
i = 1

1 is odd

continue
```

`print()` is skipped.

---

### Second Iteration

```
i = 2

2 is even

print(2)
```

---

### Third Iteration

```
i = 3

continue
```

---

### Fourth Iteration

```
i = 4

print(4)
```

This process continues until

```
10
```

---

## Output

```text
2
4
6
8
10
```

Only even numbers are printed because every odd number immediately executes

```python
continue
```

which skips the `print()` statement.

---

## Key Observation

Notice that

```python
i += 1
```

is written **before**

```python
continue
```

This becomes extremely important in the next example.
=================================================================================================================================================================
# 5. Using `continue` to Skip Vowels

After understanding how the `continue` statement works, the instructor demonstrated a practical example.

### Problem Statement

Accept a string from the user and print **only the consonants**, skipping all vowels.

For example,

**Input**

```text
sachin
```

**Output**

```text
s
c
h
n
```

Each consonant should be printed on a separate line.

---

# Incorrect Approach (Infinite Loop)

Many beginners write the program like this:

```python
string_input = input("Enter a string: ")

i = 0

while i < len(string_input):

    if string_input[i] in "aeiou":
        continue

    print(string_input[i])

    i += 1
```

---

## What is the Problem?

Suppose the input is

```text
sachin
```

Execution

### Iteration 1

```
i = 0

Character = s

Not vowel

Print s

i = 1
```

---

### Iteration 2

```
i = 1

Character = a

'a' is vowel

continue executes
```

Now observe carefully.

The statement

```python
i += 1
```

never executes because

```python
continue
```

skips all remaining statements of the current iteration.

Therefore,

```
i remains 1
```

Again

```
Character = a

↓

continue

↓

i still 1

↓

continue

↓

i still 1
```

This process repeats forever.

---

# Result

The program never reaches the next character.

It gets stuck on

```text
a
```

creating an **Infinite Loop**.

---

# Why Does This Happen?

Remember

`continue`

does **not** terminate the loop.

It only skips the remaining statements of the current iteration.

Since

```python
i += 1
```

comes **after**

```python
continue
```

the counter never changes.

---

# Correct Approach

To solve this problem,

increment the counter **before** executing `continue`.

The instructor uses a temporary variable to make the program cleaner.

```python
string_input = input("Enter a string: ")

i = 0
length = len(string_input)

while i < length:

    ch = string_input[i]

    i += 1

    if ch in "aeiouAEIOU":
        continue

    print(ch)
```

---

# Why Does This Work?

Notice the order carefully.

```python
ch = string_input[i]

i += 1

if ch in "aeiouAEIOU":
    continue
```

Even if

```python
continue
```

executes,

the counter has already increased.

Therefore,

the loop safely moves to the next character.

---

# Dry Run

Input

```text
sachin
```

| Character | Vowel? | Printed |
|-----------|--------|----------|
| s | ❌ | ✅ |
| a | ✅ | ❌ |
| c | ❌ | ✅ |
| h | ❌ | ✅ |
| i | ✅ | ❌ |
| n | ❌ | ✅ |

---

## Output

```text
s
c
h
n
```

---

# Important Observation

This example teaches an important rule.

Whenever you use

```python
continue
```

make sure that the loop control variable has already been updated.

Otherwise,

the loop may never terminate.

---

# Common Mistake

Wrong

```python
if condition:
    continue

i += 1
```

Correct

```python
i += 1

if condition:
    continue
```

---

# Practice Assignments

To strengthen your understanding of loops and loop control statements, the instructor assigned two practice problems.

---

## Assignment 1 – Sum Until User Enters Zero

### Problem Statement

Accept integers continuously from the user.

Keep adding them to the total.

Stop taking input when the user enters

```text
0
```

Finally,

display the sum of all previously entered numbers.

---

### Example

**Input**

```text
5
2
7
10
0
```

Output

```text
Sum = 24
```

---

## Algorithm

```text
Start

↓

Sum = 0

↓

Accept Number

↓

Number == 0 ?

↓

Yes

↓

Stop Loop

↓

Print Sum

↓

End

↓

Otherwise

↓

Add Number

↓

Repeat
```

---

## Concepts Used

- `while`
- `break`
- Accumulator
- User Input

---

# Assignment 2 – Ignore Negative Numbers

This assignment is a modification of the previous problem.

### Problem Statement

Accept integers continuously.

- If the user enters a **negative number**, ignore it.
- Do **not** add it to the sum.
- Continue accepting input.
- Stop only when the user enters

```text
0
```

---

### Example

**Input**

```text
5

2

-6

11

0
```

Calculation

```text
5 + 2 + 11
```

Output

```text
18
```

Notice

```
-6
```

is ignored completely.

This problem is intended to encourage the use of the **`continue` statement** inside a loop.
=============================================================================================================================================================
# 6. The `pass` Statement

So far, we have studied two loop control statements:

- `break`
- `continue`

Python provides one more special statement called **`pass`**.

Unlike `break` and `continue`, the `pass` statement **does absolutely nothing**.

It is simply a placeholder that tells Python:

> **"There is no code to execute here right now."**

---

# Why Do We Need `pass`?

Python uses **indentation** to define code blocks.

Unlike C, C++, or Java, Python does not allow empty code blocks.

For example,

```python
if True:

else:
    print("Hello")
```

This program produces an error because the `if` block is empty.

Output

```text
IndentationError
```

Python expects at least one statement inside every block.

To satisfy this requirement, we use

```python
pass
```

---

# Syntax

```python
if condition:
    pass
```

---

# How Does `pass` Work?

When Python encounters

```python
pass
```

it simply ignores it and continues executing the remaining program.

No output is produced.

No action is performed.

---

# Example

```python
num = int(input("Enter an integer: "))

if num % 2 == 0:
    pass
else:
    print("Number is odd")
```

---

## Output 1

Input

```text
8
```

Output

```text
```

Nothing is printed because the even-number block contains only

```python
pass
```

---

## Output 2

Input

```text
7
```

Output

```text
Number is odd
```

---

# Step-by-Step Execution

Suppose

```text
num = 8
```

Python checks

```python
8 % 2 == 0
```

↓

True

Python executes

```python
pass
```

↓

Nothing happens.

Program ends.

---

Suppose

```text
num = 7
```

Python checks

```python
7 % 2 == 0
```

↓

False

Python enters the

```python
else
```

block.

Output

```text
Number is odd
```

---

# Does `pass` Skip the Loop?

No.

Many beginners confuse

```python
pass
```

with

```python
continue
```

or

```python
break
```

It does **not**

- terminate the loop
- skip the iteration
- exit the function

It simply performs **no operation**.

---

# Difference Between `break`, `continue` and `pass`

| Statement | Purpose |
|-----------|---------|
| `break` | Terminates the loop immediately |
| `continue` | Skips the current iteration and moves to the next iteration |
| `pass` | Performs no action; acts as a placeholder |

---

# When is `pass` Used?

Although it looks useless initially, it becomes extremely useful while developing large applications.

Common uses include

- Empty `if` blocks
- Empty loops
- Empty functions
- Empty classes
- Writing code incrementally
- Designing program structure before implementation

Example

```python
def login():

    pass
```

The function is syntactically complete.

The implementation can be added later.

---

# Another Example

```python
class Student:

    pass
```

The class currently has no members,

but Python accepts it because of

```python
pass
```

---

# Example with Loop

```python
for i in range(5):

    pass

print("Done")
```

Output

```text
Done
```

The loop runs,

but nothing happens inside it.

---

# Important Points

- `pass` is a placeholder statement.
- It performs absolutely no operation.
- It is used only to satisfy Python's syntax rules.
- It is commonly used during software development when code is yet to be written.

---

# Common Mistakes

### Mistake 1

Thinking `pass` skips iterations.

Wrong.

Only

```python
continue
```

does that.

---

### Mistake 2

Thinking `pass` exits loops.

Wrong.

Only

```python
break
```

terminates a loop.

---

### Mistake 3

Thinking `pass` produces output.

Wrong.

It performs no operation.

---

# Quick Comparison

| Statement | Loop Ends? | Current Iteration Skipped? | Performs Nothing? |
|-----------|------------|----------------------------|-------------------|
| `break` | ✅ | ❌ | ❌ |
| `continue` | ❌ | ✅ | ❌ |
| `pass` | ❌ | ❌ | ✅ |

---

# 7. Introduction to the Python `for` Loop

Until now, every repetitive task has been solved using the

```python
while
```

loop.

Although `while` is very powerful, it requires the programmer to manually handle

- Initialization
- Condition
- Counter Update

For example,

```python
i = 0

while i < 5:

    print(i)

    i += 1
```

Notice that we have to manually

- create `i`
- increment `i`
- stop the loop

Python provides another looping statement called the **`for` loop** that automatically handles iteration over collections.

Unlike C, C++, or Java,

Python's `for` loop is **not** based on initialization, condition, and increment.

Instead, it is an **Iterator-Based Loop**.

This is one of the biggest differences between Python and many other programming languages.

In the next section, we will learn how Python's `for` loop works and how it iterates over sequences such as **strings** and **lists** without requiring any counter variable.
=======================================================================================================================================================================================
# 8. Python `for` Loop

The **`for` loop** is the second looping statement provided by Python.

Unlike the `while` loop, where the programmer is responsible for managing the loop control variable, the `for` loop automatically retrieves one element at a time from a collection and executes the loop body.

This makes the `for` loop simpler, cleaner, and less error-prone.

---

# How Python's `for` Loop is Different

Many programming languages use a traditional `for` loop.

For example, in C/C++:

```cpp
for(int i = 0; i < 5; i++)
```

This contains three parts:

- Initialization
- Condition
- Increment/Decrement

Similarly, Java follows the same style.

Some languages such as PL/SQL use syntax similar to

```text
FOR i = 1 TO 100
```

Python is completely different.

Python's `for` loop is **Iterator-Based**.

Instead of working with numbers directly, it works with **iterable objects**.

---

# Iterator-Based `for` Loop

Python automatically takes one element from a sequence, stores it in the loop variable, executes the loop body, and then moves to the next element.

The programmer does not need to:

- Initialize a counter
- Increment the counter
- Check the stopping condition

Python handles everything internally.

---

# Syntax

```python
for variable in sequence:
    statements
```

General Form

```python
for item in iterable:
    statements
```

where

- **item** → Temporary variable
- **iterable** → Object containing multiple values

---

# Flow of Execution

```text
Sequence

↓

Take First Element

↓

Store in Variable

↓

Execute Loop Body

↓

Take Next Element

↓

Execute Loop Body

↓

...

↓

No More Elements

↓

Loop Ends
```

Unlike the `while` loop,

there is **no manual condition checking** and **no counter update**.

---

# Example 1 – Iterating Over a String

One of the first demonstrations in the lecture was iterating through a string.

```python
word = "sachin"

for ch in word:
    print(ch)
```

---

## Output

```text
s
a
c
h
i
n
```

---

# Step-by-Step Working

Initially,

```text
word = "sachin"
```

Python automatically performs

```
ch = 's'

↓

print(s)

↓

ch = 'a'

↓

print(a)

↓

ch = 'c'

↓

print(c)

↓

...

↓

Loop Ends
```

Notice that

- No index variable is created.
- No `i += 1` is written.
- No `len()` function is required.

Everything is managed internally by Python.

---

# Advantages over `while`

Using `while`

```python
word = "sachin"

i = 0

while i < len(word):

    print(word[i])

    i += 1
```

Using `for`

```python
word = "sachin"

for ch in word:
    print(ch)
```

The second program is

- Shorter
- Easier to read
- Less prone to mistakes
- No risk of forgetting `i += 1`

---

# Example 2 – Iterating Over a List

The lecture also demonstrated that the `for` loop works with lists.

```python
fruits = ["apple", "banana", "cherry", "date"]

for fruit in fruits:
    print(fruit)
```

---

## Output

```text
apple
banana
cherry
date
```

---

# Step-by-Step Execution

Initially

```text
fruits
```

contains four elements.

Python performs

```
fruit = "apple"

↓

Print apple

↓

fruit = "banana"

↓

Print banana

↓

fruit = "cherry"

↓

Print cherry

↓

fruit = "date"

↓

Print date

↓

Loop Ends
```

Again,

notice that there is

- no index
- no counter
- no increment

---

# Why is the `for` Loop Safer?

The biggest advantage of a `for` loop is that it completely eliminates common mistakes that occur in `while` loops.

For example,

in a `while` loop,

forgetting

```python
i += 1
```

creates an infinite loop.

This problem cannot occur in a `for` loop because Python automatically moves to the next element.

---

# Rewriting the Previous Vowel Removal Program Using `for`

In the previous section, we solved the problem using a `while` loop.

```python
string_input = input("Enter a string: ")

i = 0

while i < len(string_input):

    ch = string_input[i]

    i += 1

    if ch in "aeiouAEIOU":
        continue

    print(ch)
```

Using a `for` loop, the same program becomes much shorter.

```python
string_input = input("Enter a string: ")

for ch in string_input:

    if ch in "aeiouAEIOU":
        continue

    print(ch)
```

---

## Output

Input

```text
sachin
```

Output

```text
s
c
h
n
```

---

# Why is the `for` Version Better?

Compared to the `while` version,

we no longer need

- `i`
- `len()`
- Indexing
- `i += 1`

Therefore,

the code becomes

- shorter
- cleaner
- easier to understand
- less error-prone

---

# Sequence

A **Sequence** is an ordered collection of elements.

Examples include

- String
- List
- Tuple

Example

```python
"Python"

[10,20,30]

("A","B","C")
```

Each element has a specific position.

---

# Iterable

An **Iterable** is any object whose elements can be accessed one by one during iteration.

Python's `for` loop works only with iterable objects.

Examples of iterables

- Strings
- Lists
- Tuples
- Sets
- Dictionaries

---

# Difference Between Sequence and Iterable

| Sequence | Iterable |
|-----------|----------|
| Ordered collection of elements | Any object that can be iterated |
| Supports indexing | Can be traversed using `for` |
| Example: String, List | Example: String, List, Tuple, Set, Dictionary |

Every sequence is iterable, but not every iterable necessarily behaves like a sequence.

---

# Common Mistakes

### Mistake 1

Trying to manually increment the loop variable.

Wrong

```python
for ch in word:

    ch += 1
```

The loop variable automatically changes during each iteration.

---

### Mistake 2

Using indexing unnecessarily.

Wrong

```python
for ch in word:

    print(word[ch])
```

Here,

`ch` is already the character.

Correct

```python
print(ch)
```

---

# Interview Points

- Python's `for` loop is **Iterator-Based**.
- It is different from C/C++/Java `for` loops.
- No initialization, condition, or increment is required.
- Works with iterable objects.
- Automatically moves to the next element.
- Reduces the chances of infinite loops.
- Makes programs shorter and easier to read.

---

# Quick Revision

- Python provides two loops:
  - `while`
  - `for`
- `for` is an **Iterator-Based Loop**.
- It works with iterable objects.
- No counter variable is required.
- No `len()` or indexing is needed for simple iteration.
- Strings and lists are iterable.
- `for` loops are generally preferred over `while` loops whenever we need to traverse a collection.

---

# Lecture 17 Summary

In this lecture, we first completed the vowel checking assignment using a combination of **`while`**, **`break`**, and **`while-else`**. We then discussed the issue of **case sensitivity** and learned two solutions: checking both uppercase and lowercase vowels, and the cleaner approach of converting the input using `.lower()`.

Next, we explored the **Number Guessing Game**, where the `random` module and `random.randint()` function were introduced to generate random integers.

The lecture then introduced the **`continue` statement**, highlighting how it differs from `break`, and demonstrated both correct and incorrect usages, including an example that leads to an infinite loop if the loop control variable is not updated before `continue`.

We also studied the **`pass` statement**, understanding that it serves as a placeholder and performs no operation while satisfying Python's syntax requirements.

Finally, the lecture introduced Python's **iterator-based `for` loop**, showing how it differs from traditional `for` loops in other languages. We learned to iterate over **strings** and **lists**, rewrote the previous vowel filtering program using `for`, and understood the concepts of **Sequence** and **Iterable**.

> **Lecture 17 Completed (Up to Introduction of `for` Loop — `range()` function not included.)**
==============================================================================================================================================================================================================================================================================================================================================================
