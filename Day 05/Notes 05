# 🐍 Comprehensive Guide to Python Built-in Functions, Standard Library Modules & Error Handling

This document covers Python's built-in functions, standard library modules, console output customization, and the difference between syntax errors and runtime exceptions.

---

# 1️⃣ Character Comparison Using `max()` and `min()`

Python compares characters based on their underlying **ASCII/Unicode values**.

## ASCII Values

| Character Type            | ASCII Range |
| ------------------------- | ----------- |
| Uppercase Letters (`A-Z`) | 65 - 90     |
| Lowercase Letters (`a-z`) | 97 - 122    |
| 0 to 9                    | 48 - 57     |

Since lowercase letters have higher ASCII values than uppercase letters, they are considered larger during comparisons.

---

## Example

```python
max('A', 'b', 'C')
```

### Output

```python
'b'
```

### Explanation

| Character | ASCII Value |
| --------- | ----------- |
| A         | 65          |
| C         | 67          |
| b         | 98          |

Since `98` is the highest value, Python returns:

```python
'b'
```

---

# 2️⃣ Using Standard Library Modules

Python ships with a rich Standard Library that provides functionality for mathematics, system information, calendars, networking, file handling, and much more.

---

## A. The `math` Module

The `math` module provides mathematical functions and constants.

### Factorial Example

```python
import math

result = math.factorial(5)

print(result)
```

### Output

```python
120
```

### Explanation

```text
5! = 5 × 4 × 3 × 2 × 1
   = 120
```

---

## B. The `platform` Module

The `platform` module provides information about the system and operating environment.

### Example

```python
import platform

print("OS Architecture:", platform.architecture())
print("Machine Type:", platform.machine())
print("Operating System:", platform.system())
print("Python Version:", platform.python_version())
```

### Sample Output

```text
OS Architecture: ('64bit', 'WindowsPE')
Machine Type: AMD64
Operating System: Windows
Python Version: 3.13.0
```

---

## C. The `calendar` Module

The `calendar` module helps generate month and year calendars.

### Display a Specific Month

```python
import calendar

print(calendar.month(2026, 6))
```

### Display an Entire Year

```python
import calendar

print(calendar.calendar(2026))
```

---

## D. Discovering Available Modules

Python's help system can display all installed and built-in modules.

### Example

```python
help("modules")
```

This command lists all modules available in the current Python environment.

---

# 3️⃣ Controlling Console Output with `print()`

By default, `print()` automatically adds a newline after printing.

Internally:

```python
print(value, end="\n")
```

---

## Example

```python
print("Data Processing Started...", end=" ")
print("Success!")
```

### Output

```text
Data Processing Started... Success!
```

---

## Common `end` Values

| Value   | Effect             |
| ------- | ------------------ |
| `"\n"`  | New line (default) |
| `" "`   | Space              |
| `""`    | No separator       |
| `"---"` | Custom delimiter   |

### Example

```python
print("A", end="---")
print("B")
```

Output:

```text
A---B
```

---

# 4️⃣ Error Handling: Syntax Errors vs Runtime Exceptions

Understanding Python errors is essential for debugging.

---

## Syntax Error vs Runtime Exception

| Feature           | Syntax Error          | Runtime Exception                  |
| ----------------- | --------------------- | ---------------------------------- |
| Detection Time    | Compilation Phase     | Execution Phase                    |
| Cause             | Invalid Python syntax | Valid syntax but invalid operation |
| Execution         | Program never starts  | Program crashes during execution   |
| Lines Above Error | Not executed          | Executed successfully              |
| Lines Below Error | Not executed          | Not executed after crash           |

---

# A. Syntax Errors

A Syntax Error occurs when Python cannot understand the structure of the code.

---

## Example

```python
print("Line 1")
print("Line 2")

if True
    print("Line 3")
```

### Problem

The colon (`:`) is missing after the `if` statement.

---

### Result

```text
SyntaxError
```

### Important Observation

Even though the first two print statements appear before the error:

```python
print("Line 1")
print("Line 2")
```

Nothing executes.

Python first compiles the entire file before running any line.

---

## Execution Flow

```text
Compile Entire File
        │
        ▼
Syntax Error Found
        │
        ▼
Execution Aborted
```

---

# B. Runtime Exceptions

Runtime Exceptions occur when syntax is correct, but an operation fails while the program is running.

---

## Example

```python
print("Monday")
print("Tuesday")

print(10 / 0)

print("Wednesday")
```

---

### Output

```text
Monday
Tuesday

Traceback (most recent call last):
  File "script.py", line 4, in <module>
    print(10 / 0)

ZeroDivisionError: division by zero
```

---

## Step-by-Step Analysis

### Step 1

```python
print("Monday")
```

Output:

```text
Monday
```

---

### Step 2

```python
print("Tuesday")
```

Output:

```text
Tuesday
```

---

### Step 3

```python
print(10 / 0)
```

Python encounters:

```python
10 / 0
```

which is mathematically impossible.

This raises:

```python
ZeroDivisionError
```

---

### Step 4

```python
print("Wednesday")
```

This statement never executes because the program has already terminated.

---

## Runtime Execution Flow

```text
Execute Line 1
       │
       ▼
Execute Line 2
       │
       ▼
Exception Occurs
       │
       ▼
Program Stops
```

---

# 🎯 Key Takeaways

* `max()` and `min()` compare characters using ASCII/Unicode values.
* Lowercase letters have higher ASCII values than uppercase letters.
* The `math` module provides mathematical functions such as `factorial()`.
* The `platform` module provides system information.
* The `calendar` module generates monthly and yearly calendars.
* `help("modules")` lists available Python modules.
* The `print()` function uses `end="\n"` by default.
* Syntax Errors are detected before execution begins.
* Runtime Exceptions occur while the program is running.
* Statements before a Runtime Exception execute successfully.
* Statements after a Runtime Exception never execute.
