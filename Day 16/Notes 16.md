# Python Programming Notes – Lecture 16

# Nested `if-else`, Single-Line `if`, `while` Loop, `break`, `while-else`

---

# Introduction

In the previous lecture, we studied various decision control statements such as `if`, `if-else`, `if-elif-else`, and Nested `if`.

One assignment given at the end of the lecture was:

> **Accept three distinct integers and print the greatest among them without using logical operators (`and`, `or`) or relational cascading (`a > b > c`).**

This lecture begins by solving that assignment and then introduces an entirely new concept—**Iterative Statements (Loops)**.

Unlike decision statements, which execute a block of code only once when a condition is satisfied, loops repeatedly execute a block of code until a specified condition becomes false. :contentReference[oaicite:0]{index=0}

---

# Topics Covered

- Nested `if-else` Optimization
- Finding Greatest of Three Numbers
- Single-Line `if` (Conditional Expression)
- Nested Conditional Expressions
- Iterative Statements
- `while` Loop
- `while-else`
- `break` Statement
- Homework Programs

---

# 1. Finding the Greatest of Three Numbers Using Nested `if`

## Problem Statement

Write a program to accept **three distinct integers** and print the greatest among them.

### Constraints

- Do **not** use `and`
- Do **not** use `or`
- Do **not** use relational cascading
- Use **Nested `if` statements** only

This problem forces us to think in the form of a **decision tree** instead of combining conditions.

---

# Logic

Suppose the numbers are

```
a
b
c
```

Instead of checking

```python
if a>b and a>c
```

(which is not allowed),

we compare step-by-step.

---

## Step 1

Compare

```python
a>b
```

If true,

then only compare

```python
a>c
```

If this is also true,

then

```
a is greatest
```

Otherwise,

```
c is greatest
```

---

## Step 2

If

```python
a>b
```

is false,

then because all numbers are unique,

```
b>a
```

must be true.

Now compare

```python
b>c
```

If true,

```
b is greatest
```

Otherwise,

```
c is greatest
```

---

# Decision Tree

```text
                a>b ?
              /       \
            Yes        No
           /            \
        a>c ?          b>c ?
       /    \         /     \
     Yes    No      Yes      No
      |      |       |        |
      a      c       b        c
```

---

# Complete Program

```python
a, b, c = input("Enter three unique numbers: ").split()

a = int(a)
b = int(b)
c = int(c)

if a > b:

    if a > c:
        print("Greatest number is {}".format(a))

    else:
        print("Greatest number is {}".format(c))

else:

    if b > c:
        print("Greatest number is {}".format(b))

    else:
        print("Greatest number is {}".format(c))
```

This is the same approach demonstrated in the lecture using nested decision blocks. :contentReference[oaicite:1]{index=1}

---

# Why is `split()` Used?

Instead of writing

```python
a = int(input())
b = int(input())
c = int(input())
```

Python allows

```python
a,b,c = input().split()
```

Example

Input

```
10 20 30
```

After splitting

```
a="10"

b="20"

c="30"
```

These are still strings.

Therefore,

```python
a=int(a)
b=int(b)
c=int(c)
```

is necessary.

---

# Dry Run – Example 1

Input

```
5

7

9
```

Comparison

```
5>7

False
```

Move to else

```
7>9

False
```

Output

```
Greatest number is 9
```

---

# Dry Run – Example 2

Input

```
15

7

9
```

Comparison

```
15>7

True
```

Now compare

```
15>9

True
```

Output

```
Greatest number is 15
```

---

# Why Use Nested `if`?

Without logical operators,

you cannot write

```python
if a>b and a>c
```

Therefore,

Nested `if` provides a structured way to compare numbers one step at a time.

---

# Advantages

- Easy to understand
- Avoids logical operators
- Reduces unnecessary comparisons
- Frequently asked in interviews and exams

---

# Common Mistakes

### Forgetting to convert to integers

Wrong

```python
a,b,c=input().split()
```

Comparison happens as strings.

Always convert

```python
a=int(a)
```

---

### Using logical operators

Wrong

```python
if a>b and a>c
```

The assignment specifically prohibits this.

---

### Assuming numbers are equal

The lecture assumes

```
All three numbers are unique.
```

Handling duplicate values requires additional conditions.

---

# Key Points

- Solve using Nested `if`.
- No `and` or `or`.
- No relational cascading.
- Compare numbers step by step.
- `split()` returns strings.
- Convert them using `int()` before comparison.

---

# Quick Revision

✔ `split()` separates input into multiple strings.

✔ Nested `if` builds a decision tree.

✔ Comparison is performed step by step.

✔ The lecture assumes all numbers are distinct.

---

**Next Part:** Python's Single-Line `if` (Conditional Expression), nested conditional expressions, introduction to loops, and the `while` loop.
==============================================================================================================================================================
# Part 2 – Python's Single-Line `if` (Conditional Expression)

In languages like **C, C++**, and **Java**, programmers often use the **Ternary Operator (`?:`)** to write simple decision-making statements in a single line.

Example in C/C++:

```cpp
(age >= 18) ? printf("Eligible") : printf("Not Eligible");
```

Python **does not provide the `?:` ternary operator**.

Instead, Python provides a much cleaner and more readable alternative known as the **Conditional Expression** or **Single-Line `if`**.

Although many programmers casually call it the *Python ternary operator*, technically it is a **Conditional Expression**.

---

# Why Use a Single-Line `if`?

Suppose we want to determine whether a number is even or odd.

Normally we write:

```python
num = int(input("Enter a number: "))

if num % 2 == 0:
    print("Number is Even")
else:
    print("Number is Odd")
```

This takes multiple lines.

For very small decisions, Python allows us to write the same logic in a single line.

---

# Syntax

```python
statement_if_true if condition else statement_if_false
```

General Syntax

```python
value_if_true if condition else value_if_false
```

### Working

Python first evaluates the condition.

- If the condition is **True**, the expression before `else` is executed.
- If the condition is **False**, the expression after `else` is executed.

---

# Example 1 – Even or Odd Number

```python
num = int(input("Enter a number: "))

print("Number is Even") if num % 2 == 0 else print("Number is Odd")
```

---

### Sample Output 1

```text
Enter a number:
8

Number is Even
```

---

### Sample Output 2

```text
Enter a number:
15

Number is Odd
```

This is the exact optimization shown in the lecture after discussing the normal `if-else` statement. :contentReference[oaicite:0]{index=0}

---

# Step-by-Step Working

Suppose

```text
Input

8
```

Python evaluates

```
8 % 2

↓

0
```

Now

```
0 == 0

↓

True
```

Therefore,

only this part executes

```python
print("Number is Even")
```

The `else` part is ignored.

---

Suppose

```text
Input

15
```

Python checks

```
15 % 2

↓

1
```

```
1 == 0

↓

False
```

Now

```python
print("Number is Odd")
```

executes.

---

# Important Rule

Unlike the normal `if` statement,

**a Single-Line `if` must always contain an `else` part.**

The following is **invalid**.

```python
print("Hello") if True
```

Output

```text
SyntaxError
```

Correct

```python
print("Hello") if True else print("Bye")
```

This rule is specifically emphasized in the lecture. :contentReference[oaicite:1]{index=1}

---

# Why is `else` Mandatory?

The conditional expression must always produce one complete result.

Python needs to know

- what to execute if the condition is True
- what to execute if the condition is False

Therefore,

`else` cannot be omitted.

---

# Assigning Values

Instead of printing directly,

we can assign the result to a variable.

Example

```python
num = 20

result = "Even" if num % 2 == 0 else "Odd"

print(result)
```

Output

```text
Even
```

---

# Nested Conditional Expressions

Python even allows one conditional expression inside another.

This is called **Nested Conditional Expressions**.

---

## Example

```python
age = 16

msg = "Kid" if age < 13 else ("Teenager" if age < 20 else "Adult")

print(msg)
```

Output

```text
Teenager
```

This example is demonstrated in the lecture to show that conditional expressions can handle more than two outcomes, although readability decreases. :contentReference[oaicite:2]{index=2}

---

# Step-by-Step Dry Run

Suppose

```text
age = 16
```

Python checks

```
age < 13

↓

False
```

Moves to

```
"Teenager" if age < 20 else "Adult"
```

Now

```
16 < 20

↓

True
```

Output

```text
Teenager
```

---

Suppose

```text
age = 25
```

First condition

```
25 < 13

↓

False
```

Second condition

```
25 < 20

↓

False
```

Output

```text
Adult
```

---

# Should We Use Nested Conditional Expressions?

They are perfectly valid,

but they become difficult to read as the number of conditions increases.

For simple decisions,

they improve readability.

For complex decision-making,

the normal `if-elif-else` statement is preferred.

---

# Comparison

## Normal `if-else`

```python
if age >= 18:
    print("Adult")
else:
    print("Minor")
```

---

## Single-Line `if`

```python
print("Adult") if age >= 18 else print("Minor")
```

---

# Advantages

- Short and concise.
- Easy for simple decisions.
- Improves readability when used appropriately.
- Useful for assigning values.

---

# Disadvantages

- Difficult to read for multiple nested conditions.
- Not suitable for long blocks of code.
- Can reduce code clarity if overused.

---

# Common Mistakes

### Omitting `else`

Wrong

```python
print("Hello") if True
```

Output

```text
SyntaxError
```

---

### Writing Complex Logic in One Line

Avoid writing large nested expressions.

Instead,

use normal `if-elif-else`.

---

# Key Points

- Python has **no `?:` operator**.
- It uses **Conditional Expressions** instead.
- `else` is mandatory.
- Conditional expressions return a value.
- Nested conditional expressions are allowed.
- Prefer normal `if-elif-else` for complex decisions.

---

# Quick Revision

✔ Python does not support the traditional ternary operator.

✔ Syntax:

```python
value_if_true if condition else value_if_false
```

✔ `else` is compulsory.

✔ Nested conditional expressions are possible.

✔ Use them only for small decision-making problems.

---

# Introduction to Iterative Statements (Loops)

So far, every statement in our programs has executed **only once**.

Consider the following code:

```python
print("Hello")
print("Hello")
print("Hello")
print("Hello")
print("Hello")
```

If we want to print `"Hello"` **100 times**, writing 100 `print()` statements is inefficient and difficult to maintain.

To solve this problem, programming languages provide **Loops**.

A **Loop** is a control structure that repeatedly executes a block of code until a specified condition becomes false.

Instead of writing the same statements again and again, we write them once inside the loop.

Python provides **only two looping statements**:

- `while`
- `for`

Unlike some other languages:

- Python **does not have a native `do-while` loop**.
- Python **does not have a `switch-case` statement** (older versions; pattern matching introduced later is different).

Loops are one of the most important concepts in programming because they eliminate repetitive code and make programs shorter, cleaner, and easier to maintain.

---

**Next Part:** The `while` loop, flow of execution, printing a name 10 times, counter variables, accumulator pattern, and summing the first `N` natural numbers.
===============================================================================================================================================================
# Part 3 – Iterative Statements (Loops)

Until now, we have studied **decision control statements** such as `if`, `if-else`, and `if-elif-else`.

These statements execute a block of code **only once** when the specified condition becomes `True`.

However, in real-world programming, we often need to execute the **same block of code repeatedly**.

For example:

- Printing numbers from **1 to 100**
- Printing a name **10 times**
- Finding the sum of the first **N natural numbers**
- Displaying multiplication tables
- Reading data until the user enters a specific value

Writing the same statements repeatedly is inefficient and makes the program longer.

To solve this problem, programming languages provide **loops**.

---

# What is a Loop?

A **loop** is a programming construct that repeatedly executes a block of code as long as a specified condition remains `True`.

When the condition becomes `False`, the loop terminates and control moves to the next statement after the loop.

---

# Why Do We Need Loops?

Without loops

```python
print("Sachin")
print("Sachin")
print("Sachin")
print("Sachin")
print("Sachin")
```

To print the same name **100 times**, we would need to write 100 `print()` statements.

Using a loop

```python
i = 1

while i <= 100:
    print("Sachin")
    i += 1
```

The code becomes much shorter and easier to maintain.

---

# Types of Loops in Python

Python provides only **two looping statements**.

1. `while`
2. `for`

Unlike C, C++, and Java,

Python **does not provide a native `do-while` loop**.

It also does not have the traditional **switch-case** statement (prior to structural pattern matching introduced in newer versions).

---

# The `while` Loop

The `while` loop is the simplest loop in Python.

It repeatedly executes a block of code **as long as the condition evaluates to `True`**.

After executing the loop body, Python **returns to the condition** and checks it again.

This process continues until the condition becomes `False`.

Unlike the `if` statement, which checks the condition only once, the `while` loop repeatedly checks the condition after every iteration. This behavior is highlighted during the lecture. :contentReference[oaicite:0]{index=0}

---

# Syntax

```python
while condition:
    statements
```

---

# Flow Diagram

```text
            Start
              │
              ▼
      Check Condition
              │
      ┌───────┴────────┐
    True            False
      │                 │
      ▼                 ▼
 Execute Loop       Exit Loop
      │
      ▼
 Update Variable
      │
      └──────────────► Back to Condition
```

---

# Components of a `while` Loop

A proper `while` loop generally contains three parts:

### 1. Initialization

```python
i = 1
```

Creates the control variable.

---

### 2. Condition

```python
i <= 10
```

Determines whether another iteration should occur.

---

### 3. Updation

```python
i += 1
```

Changes the control variable so the loop eventually stops.

Without the update statement, the loop may never terminate.

---

# Example 1 – Printing a Name 10 Times

This is the first `while` loop demonstrated in the lecture.

```python
i = 1

while i <= 10:
    print("Sachin")
    i += 1

print("Bye")
```

---

## Output

```text
Sachin
Sachin
Sachin
Sachin
Sachin
Sachin
Sachin
Sachin
Sachin
Sachin
Bye
```

The lecture explains that once `i` becomes **11**, the condition `i <= 10` becomes `False`, the loop terminates, and `"Bye"` is printed. :contentReference[oaicite:1]{index=1}

---

# Dry Run

Initial value

```
i = 1
```

Iteration 1

```
1 <= 10

↓

True

Print "Sachin"

i = 2
```

Iteration 2

```
2 <= 10

↓

True

Print "Sachin"

i = 3
```

...

Iteration 10

```
10 <= 10

↓

True

Print "Sachin"

i = 11
```

Now

```
11 <= 10

↓

False
```

The loop ends.

Python executes

```python
print("Bye")
```

---

# What Happens if We Forget the Update?

Example

```python
i = 1

while i <= 10:
    print(i)
```

Output

```text
1
1
1
1
1
...
```

The program never stops because `i` never changes.

This is called an **Infinite Loop**.

---

# Infinite Loop

An **Infinite Loop** is a loop whose condition never becomes `False`.

Example

```python
while True:
    print("Hello")
```

Output

```text
Hello
Hello
Hello
Hello
...
```

This loop continues forever unless interrupted manually or terminated using `break`.

---

# Counter Variable

The variable that controls the number of iterations is called the **Counter Variable** (or Loop Control Variable).

Example

```python
i = 1
```

Here,

`i` is the counter variable.

---

# Example 2 – Printing Numbers from 1 to 10

```python
i = 1

while i <= 10:
    print(i)
    i += 1
```

Output

```text
1
2
3
4
5
6
7
8
9
10
```

---

# Accumulator Pattern

One of the most common applications of loops is calculating totals.

To calculate a running total, we use an **Accumulator Variable**.

An accumulator is initialized before the loop and updated during each iteration.

---

# Example 3 – Sum of First N Natural Numbers

This is the second major program demonstrated in the lecture.

```python
num = int(input("Enter a number: "))

total_sum = 0
i = 1

while i <= num:
    total_sum += i
    i += 1

print("Sum is:", total_sum)
```

---

## Sample Output

```text
Enter a number:
5

Sum is: 15
```

---

# Dry Run

Input

```text
5
```

Initial values

```
total_sum = 0

i = 1
```

Iteration 1

```
total_sum = 0 + 1

↓

1
```

Iteration 2

```
1 + 2

↓

3
```

Iteration 3

```
3 + 3

↓

6
```

Iteration 4

```
6 + 4

↓

10
```

Iteration 5

```
10 + 5

↓

15
```

Loop ends.

Output

```text
15
```

---

# Counter vs Accumulator

| Counter | Accumulator |
|----------|-------------|
| Controls the number of iterations | Stores a running total |
| Usually increases by 1 | Changes according to the calculation |
| Example: `i` | Example: `total_sum` |

---

# Common Mistakes

### Forgetting Initialization

```python
while i <= 10:
```

Output

```text
NameError
```

---

### Forgetting Updation

```python
i = 1

while i <= 10:
    print(i)
```

Results in an infinite loop.

---

### Wrong Condition

```python
while i >= 10:
```

If `i` starts at 1, the loop never executes.

---

# Key Points

- Loops execute code repeatedly.
- Python provides `while` and `for`.
- `while` checks its condition before every iteration.
- Initialization, condition, and updation are essential.
- Forgetting the update often causes an infinite loop.
- The counter controls iterations.
- The accumulator stores cumulative results.

---

# Quick Revision

✔ `while` repeats until its condition becomes `False`.

✔ Initialization, condition, and updation are mandatory for most loops.

✔ A counter controls the loop.

✔ An accumulator stores totals.

✔ Infinite loops occur when the condition never becomes `False`.

---

**Next Part:** `while-else`, the `break` statement, natural loop termination vs forced termination, emulating a `do-while` loop using `while True`, and the homework assignments from the lecture.
============================================================================================================================================================================================================
# Part 4 – `break` Statement and `while-else`

Until now, we have learned how a `while` loop repeats execution until its condition becomes **False**.

However, there are situations where we may want to **terminate the loop immediately**, even though the loop condition is still `True`.

For such situations, Python provides the **`break` statement**.

This lecture also introduces one of Python's unique features—the **`else` block with loops**.

Unlike many other programming languages, Python allows an `else` block to be attached directly to a loop.

---

# The `break` Statement

The `break` statement immediately terminates the nearest loop.

As soon as Python encounters a `break` statement,

- the remaining statements inside the loop are skipped,
- the loop stops immediately,
- execution continues with the first statement after the loop.

---

# Syntax

```python
while condition:

    if condition2:
        break

    statements
```

---

# Flow Diagram

```text
             while Condition
                   │
           ┌───────┴────────┐
         True            False
           │                 │
           ▼                 ▼
      Execute Body      Exit Loop
           │
     break executed?
      │            │
    Yes           No
      │            │
 Exit Loop     Continue Loop
```

---

# Example – Using `break`

This is the primary example demonstrated in the lecture.

```python
i = 1

while i <= 10:

    if i == 5:
        break

    print(i)
    i += 1
```

---

## Output

```text
1
2
3
4
```

When

```python
i == 5
```

Python immediately executes

```python
break
```

The loop stops.

Numbers

```
5

6

7

8

9

10
```

are never printed.

This exact example is used in class to explain forced loop termination. :contentReference[oaicite:0]{index=0}

---

# Dry Run

Initial

```
i = 1
```

Iteration 1

```
1 == 5 ?

↓

False

Print 1

i = 2
```

Iteration 2

```
2 == 5 ?

↓

False

Print 2

i = 3
```

Iteration 3

```
Print 3
```

Iteration 4

```
Print 4
```

Iteration 5

```
5 == 5

↓

True

break
```

Loop terminates immediately.

---

# Why Use `break`?

Suppose we are searching for an element inside a list.

As soon as the element is found,

there is no need to continue searching.

Instead of checking the remaining elements,

we terminate the loop immediately.

This improves efficiency.

---

# Practical Uses

- Searching
- Menu-driven programs
- Password validation
- ATM systems
- Games
- Number guessing programs

---

# `while-else`

One of Python's unique features is that loops can have an **`else` block**.

Many beginners assume that the `else` block executes whenever the loop ends.

This is **not correct**.

---

# Rule

The `else` block executes **only if the loop terminates naturally**.

Natural termination means

```
Loop Condition

↓

False
```

---

# Syntax

```python
while condition:

    statements

else:

    statements
```

---

# Example – Natural Termination

```python
i = 1

while i <= 5:
    print(i)
    i += 1

else:
    print("Bye")
```

---

## Output

```text
1
2
3
4
5
Bye
```

Why?

Because

```
i

↓

6
```

Now

```
6 <= 5

↓

False
```

The loop ends normally.

Therefore,

Python executes the `else` block.

---

# Example – Using `break`

```python
i = 1

while i <= 10:

    if i == 5:
        break

    print(i)
    i += 1

else:
    print("Bye")
```

---

## Output

```text
1
2
3
4
```

Notice

```
Bye
```

is **not printed**.

Why?

Because the loop did **not** terminate naturally.

It terminated because of

```python
break
```

This behavior is emphasized in the lecture as the defining rule of `while-else`. :contentReference[oaicite:1]{index=1}

---

# Natural vs Forced Termination

| Natural Termination | Forced Termination |
|---------------------|-------------------|
| Condition becomes False | `break` statement executes |
| `else` block executes | `else` block is skipped |
| Normal loop exit | Immediate loop exit |

---

# Flow Diagram of `while-else`

```text
          while Condition
                │
        ┌───────┴────────┐
      True            False
        │                 │
        ▼                 ▼
 Execute Body       Execute else
        │
   break executed?
      │        │
    Yes       No
      │        │
 Exit Loop   Back to Condition
```

---

# Infinite Loop

Sometimes we intentionally create an infinite loop.

Example

```python
while True:
    print("Hello")
```

Output

```text
Hello
Hello
Hello
...
```

The condition

```python
True
```

never becomes false.

Therefore,

the loop runs forever.

---

# Why Would We Create an Infinite Loop?

Infinite loops are useful when

- displaying menus,
- continuously accepting user input,
- waiting for external events,
- creating servers,
- running games.

The loop continues until the programmer explicitly stops it using `break`.

---

# Emulating a `do-while` Loop

Unlike C and Java,

Python **does not have a native `do-while` loop**.

A `do-while` loop guarantees that the loop body executes **at least once** before checking the condition.

Python programmers commonly simulate this behavior using an infinite loop.

---

# Example

```python
i = 1

while True:

    print("Executed at least once")

    if i == 1:
        break
```

---

## Output

```text
Executed at least once
```

Why?

The loop starts with

```python
while True
```

which is always true.

Therefore,

the body executes immediately.

Only afterwards does Python encounter

```python
break
```

and terminate the loop.

This technique is presented in the lecture to mimic the behavior of a `do-while` loop. :contentReference[oaicite:2]{index=2}

---

# Common Mistakes

## Forgetting to Update

```python
while i <= 10:
    print(i)
```

Infinite loop.

---

## Assuming `else` Always Executes

Wrong.

If `break` executes,

the `else` block is skipped.

---

## Writing Code After `break`

Example

```python
if i == 5:
    break
    print(i)
```

The `print()` statement is **never executed** because `break` immediately exits the loop.

---

# Key Points

- `break` immediately terminates the nearest loop.
- Statements after `break` inside the same block are never executed.
- `while-else` is unique to Python.
- The `else` block executes only after **natural termination**.
- If the loop ends because of `break`, the `else` block is skipped.
- `while True` creates an infinite loop.
- Infinite loops are commonly stopped using `break`.
- `while True` can be used to simulate a `do-while` loop.

---

# Quick Revision

✔ `break` immediately exits the loop.

✔ `else` executes only after natural loop termination.

✔ `break` skips the `else` block.

✔ `while True` creates an infinite loop.

✔ Python has no native `do-while`.

✔ `while True` + `break` is the standard way to emulate a `do-while` loop.

---

**Next Part:** Homework assignments from the lecture (Leap Year Checker and Vowel Detection), additional practice programs, interview questions, quick revision, and complete lecture summary.
======================================================================================================================================================================================================
# Part 5 – Homework Assignments, Practice Programs & Lecture Summary

Towards the end of the lecture, the instructor discussed a few practice problems to strengthen the concepts of **decision control statements** and **loops**.

These assignments are designed to help students apply the concepts of:

- Nested `if`
- `while` loops
- Character processing
- String traversal
- Loop control

Instead of directly providing the complete solutions, the lecture explains the required logic and leaves the implementation as practice. :contentReference[oaicite:0]{index=0}

---

# Assignment 1 – Leap Year Checker

## Problem Statement

Write a Python program to accept a year from the user and determine whether it is a **Leap Year**.

---

## Important Note

Many beginners believe that

> **Every year divisible by 4 is a leap year.**

This is **incorrect**.

The lecture specifically reminds students that:

> **1900 is divisible by 4, but it is NOT a leap year.** :contentReference[oaicite:1]{index=1}

---

# Leap Year Rules

A year is a leap year if:

### Rule 1

It is divisible by **400**

OR

### Rule 2

It is divisible by **4**

AND

It is **not divisible by 100**

---

# Examples

| Year | Leap Year? |
|-------|------------|
| 2000 | ✅ Yes |
| 2024 | ✅ Yes |
| 1900 | ❌ No |
| 2100 | ❌ No |
| 2025 | ❌ No |

---

# Sample Input

```text
Enter Year:
2024
```

Output

```text
Leap Year
```

---

Another Example

```text
Enter Year:
1900
```

Output

```text
Not a Leap Year
```

---

# Logic

```text
Start

↓

Accept Year

↓

Year % 400 == 0 ?

↓

Yes → Leap Year

↓

No

↓

Year % 100 == 0 ?

↓

Yes → Not Leap Year

↓

No

↓

Year % 4 == 0 ?

↓

Yes → Leap Year

↓

Else

↓

Not Leap Year
```

---

# Assignment 2 – Vowel Detection Using `while`

The second homework assignment focuses on combining **loops** with **strings**.

---

## Problem Statement

Accept a string from the user and determine whether it contains any vowels.

The instructor provides a hint instead of the full solution.

---

# Hint Given in Class

Strings use

```
0-based indexing
```

Therefore,

start from

```python
i = 0
```

Continue until

```python
len(string)-1
```

During every iteration,

check whether

```python
string[i]
```

is a vowel.

This exact hint is provided during the lecture. :contentReference[oaicite:2]{index=2}

---

# Skeleton Program

```python
string_input = input("Enter a string: ")

i = 0

while i < len(string_input):

    # Check whether string_input[i]
    # is present inside
    # aeiouAEIOU

    i += 1
```

---

# Why Start from Zero?

Python stores strings using indexing.

Example

```text
Python
```

| Character | P | y | t | h | o | n |
|------------|---|---|---|---|---|---|
| Index | 0 | 1 | 2 | 3 | 4 | 5 |

Therefore,

the first character always begins at

```python
0
```

---

# Why Use `len()`?

Suppose

```python
name = "Python"
```

Then

```python
len(name)
```

returns

```text
6
```

The valid indices are

```
0

1

2

3

4

5
```

Therefore,

the loop should continue while

```python
i < len(name)
```

---

# General Algorithm

```text
Accept String

↓

i = 0

↓

Repeat until i reaches length

↓

Read Character

↓

Check whether vowel

↓

Move to next character

↓

End Loop
```

---

# Applications of This Logic

The same technique can later be used for

- Counting vowels
- Counting consonants
- Counting digits
- Counting spaces
- Reversing strings
- Finding uppercase letters
- Password validation

---

# Difference Between Decision Statements and Loops

| Decision Statements | Loops |
|---------------------|------|
| Execute once | Execute repeatedly |
| Example: `if` | Example: `while` |
| Used for making decisions | Used for repetition |

---

# Important Concepts Learned in Lecture 16

### Decision Making

- Nested `if`
- Decision tree
- Greatest of three numbers

---

### Conditional Expressions

- Python alternative to ternary operator
- Single-line `if`
- Nested conditional expressions

---

### Loops

- Need for loops
- `while`
- Counter variable
- Accumulator
- Infinite loop

---

### Loop Control

- `break`
- Natural termination
- Forced termination
- `while-else`

---

# Common Interview Questions

## 1. Does Python have a Ternary Operator (`?:`)?

No.

Python uses

```python
value_if_true if condition else value_if_false
```

---

## 2. Does Python have a `do-while` loop?

No.

Python programmers generally use

```python
while True:
```

with

```python
break
```

to achieve similar behavior.

---

## 3. When does the `else` block of a loop execute?

Only when the loop ends **naturally**.

If the loop ends because of

```python
break
```

the `else` block is skipped.

---

## 4. Difference Between Counter and Accumulator

Counter

```python
i = i + 1
```

Controls iterations.

Accumulator

```python
sum += i
```

Stores cumulative results.

---

## 5. What Does `break` Do?

Immediately terminates the nearest loop.

---

## 6. What Does `split()` Return?

It returns a **list of strings**.

Example

```python
a, b = input().split()
```

Both

```python
a

b
```

are strings until converted.

---

## 7. Why is `int()` Required After `split()`?

Because

```python
split()
```

always returns strings.

Mathematical comparisons require integers.

---

# Exam-Oriented Points

- `split()` returns strings.
- Nested `if` creates a decision tree.
- Python has no traditional ternary operator.
- `else` is mandatory in conditional expressions.
- Python provides only two loops:
  - `while`
  - `for`
- Python has no native `do-while`.
- `break` exits the nearest loop.
- `while-else` executes only after natural termination.
- Infinite loops commonly use `while True`.
- `len()` returns the number of characters in a string.

---

# Complete Lecture Summary

This lecture begins by solving the **Greatest of Three Numbers** assignment using **Nested `if-else`** without relying on logical operators or relational chaining. The solution is presented as a decision tree where comparisons are performed one step at a time.

The lecture then introduces Python's **Conditional Expression (Single-Line `if`)**, explaining how it serves as Python's readable alternative to the traditional ternary operator found in languages like C and Java. We also explore nested conditional expressions for handling multiple outcomes.

The second half of the lecture introduces **Iterative Statements**, focusing on the **`while` loop**. We study the three essential components of a loop—initialization, condition, and updation—and implement programs such as printing a name multiple times and finding the sum of the first `N` natural numbers using the accumulator pattern.

Finally, the lecture explains Python's **`break` statement** and the unique **`while-else`** construct, highlighting the important distinction between **natural loop termination** and **forced termination**. The lecture concludes with two practice assignments: **Leap Year Checker** and **Vowel Detection using a `while` loop**, preparing students for more advanced looping concepts in the upcoming lectures.

---

# Quick Revision

✅ Nested `if` is used when logical operators are restricted.

✅ `split()` returns strings.

✅ Convert values using `int()` before comparison.

✅ Python has no `?:` operator.

✅ Conditional Expression syntax:

```python
value_if_true if condition else value_if_false
```

✅ Python provides only two loops:

- `while`
- `for`

✅ `while` repeatedly executes while the condition is `True`.

✅ Counter controls the number of iterations.

✅ Accumulator stores cumulative results.

✅ `break` immediately terminates the loop.

✅ `while-else` executes only after natural termination.

✅ Python has no native `do-while`.

✅ `while True` + `break` is commonly used to simulate a `do-while`.

---

# Lecture 16 Completed ✅
=================================================================================================================================================================
