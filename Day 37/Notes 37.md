# Python Exception Handling — Part 1

## 1. Introduction

Exception handling is a Python mechanism for responding to abnormal situations during program execution. It helps a program provide a useful response instead of stopping unexpectedly.

It is particularly important in programs that accept user input, perform calculations, read files, or communicate with APIs and external services.

## 2. What Is an Exception?

An **exception** is an abnormal condition detected while a program is running that interrupts its normal flow.

```python
a = 10 / 0
```

This raises `ZeroDivisionError` because division by zero is not permitted.

Another example:

```python
number = int("2a")
```

This raises `ValueError` because `"2a"` cannot be converted to an integer.

## 3. Syntax Errors vs. Runtime Exceptions

### Syntax errors

A syntax error occurs when code violates Python's grammar and is detected while the code is parsed.

```python
if True
    print("Hello")
```

The colon after `if True` is missing. Other examples include unclosed quotes, unmatched parentheses, missing colons, and incorrect indentation (`IndentationError`).

### Runtime exceptions

A runtime exception occurs while validly parsed code is executing.

```python
a = 10
b = 0
result = a / b
```

The syntax is valid, but the division raises `ZeroDivisionError`.

| Syntax error | Runtime exception |
|---|---|
| Invalid Python grammar | An operation fails during execution |
| Usually detected before the program starts running | Detected when the relevant statement executes |
| Example: missing colon | Example: division by zero |
| A syntax error in the current file normally prevents it from running | Can be handled with `try` and `except` |

## 4. What Happens When an Exception Is Unhandled?

When an unhandled exception occurs, Python stops the normal execution path at the failing statement and displays a traceback with a technical error message.

Consider:

```python
a = int(input("Enter first no:"))
b = int(input("Enter second no:"))

c = a / b
print("Div is", c)

d = a + b
print("Sum is", d)
```

### Valid input

Input:

```text
Enter first no: 10
Enter second no: 5
```

Output:

```text
Div is 2.0
Sum is 15
```

### Zero denominator

Input:

```text
Enter first no: 10
Enter second no: 0
```

The division raises `ZeroDivisionError: division by zero`. The later division output and sum statements are not reached, even though `10 + 0` is a valid calculation.

## 5. Invalid Integer Input

In the same program, suppose the second input is `2a`. This statement fails:

```python
b = int(input("Enter second no:"))
```

Python raises a `ValueError`, with a message similar to:

```text
ValueError: invalid literal for int() with base 10: '2a'
```

The input is text, but its contents are not a valid integer representation. A user-friendly message such as `Please enter an integer` is easier to understand.

## 6. What Is Exception Handling?

**Exception handling** allows a program to respond to runtime errors in a controlled way rather than ending abruptly.

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Denominator should not be 0")
```

Output:

```text
Denominator should not be 0
```

The invalid division still raises an exception, but the handler responds to it.

## 7. Why Exception Handling Matters

It can:
- Provide understandable error messages.
- Handle invalid user input.
- Let suitable code after a handled error continue.
- Improve reliability when using files, APIs, and external resources.

Exception handling does not guarantee that a program must continue after every error. The program needs an appropriate handler, and some failures may still require termination.

## 8. Useful Foundation Topics

Exception handling is an important foundation for:
- **File handling:** reading and saving information.
- **API calling:** sending and receiving requests.
- **External services:** responding to unavailable resources, invalid responses, or timeouts.

## 9. Quick Revision

- An exception is an abnormal condition during execution.
- `10 / 0` raises `ZeroDivisionError`.
- `int("2a")` raises `ValueError`.
- An unhandled exception interrupts normal execution and displays a traceback.
- Exception handling provides a controlled response to runtime errors.
===============================================================================================================================================================
# Python Exception Handling — Part 2

## 1. Exception-Handling Keywords

Python provides five keywords used in exception handling:

| Keyword | Purpose |
|---|---|
| `try` | Contains code that may raise an exception |
| `except` | Handles a matching exception |
| `else` | Runs if the `try` block finishes without an exception |
| `raise` | Explicitly raises an exception |
| `finally` | Runs during cleanup flow whether or not an exception occurred |

## 2. Basic `try` and `except`

```python
try:
    # Code that may fail
    risky_operation()
except SomeException:
    # Handling code
    print("A problem occurred")
```

Put potentially failing statements inside `try`. Name the exception class after `except`. If the named exception occurs, its handler runs; if it does not occur, that handler is skipped.

### Division example

```python
a = int(input("Enter first no:"))
b = int(input("Enter second no:"))

try:
    c = a / b
    print("Div is", c)
except ZeroDivisionError:
    print("Denominator should not be 0")

d = a + b
print("Sum is", d)
```

If the user enters `10` and `0`, output is:

```text
Denominator should not be 0
Sum is 10
```

The matching handler runs, then execution continues after the `try`/`except` structure. With inputs `10` and `3`, the program prints the division result and `Sum is 13`.

## 3. Statements After an Exception in `try`

When an exception occurs, the remaining statements in that `try` block are skipped.

```python
try:
    print("Statement 1")
    result = 10 / 0
    print("Statement 2")
except ZeroDivisionError:
    print("Exception handled")
```

Output:

```text
Statement 1
Exception handled
```

`Statement 2` is not printed because execution leaves the `try` block when the division fails.

## 4. The `else` Block

The optional `else` block runs only if the `try` block completes without an exception.

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print("Result:", result)
```

Output:

```text
Result: 5.0
```

General syntax:

```python
try:
    # Operations that may fail
except ExceptionType1:
    # Handle the first exception type
except ExceptionType2:
    # Handle the second exception type
else:
    # Runs only when try succeeds
```

The names after `except` must be actual exception classes such as `ValueError` or `ZeroDivisionError`.

## 5. Python Exception Hierarchy

Python's built-in exceptions are organized into classes. `BaseException` is the top-level base class, while `Exception` is the common base for most application errors that programs normally handle.

```text
BaseException
└── Exception
    ├── ArithmeticError
    │   ├── FloatingPointError
    │   ├── OverflowError
    │   └── ZeroDivisionError
    ├── LookupError
    │   ├── IndexError
    │   └── KeyError
    ├── NameError
    │   └── UnboundLocalError
    ├── TypeError
    ├── ValueError
    ├── AttributeError
    ├── OSError
    │   ├── FileNotFoundError
    │   ├── FileExistsError
    │   └── PermissionError
    ├── RuntimeError
    ├── ImportError
    │   └── ModuleNotFoundError
    └── SyntaxError
        └── IndentationError
```

This is a simplified hierarchy, not the full tree. `SystemExit`, `KeyboardInterrupt`, and `GeneratorExit` derive directly from `BaseException`, rather than `Exception`.

## 6. Important Exception Classes

- **`Exception`** — common base class for most application-level exceptions.
- **`ArithmeticError`** — base class for arithmetic-related failures.
- **`FloatingPointError`** — associated with floating-point calculation failures; uncommon in ordinary Python code.
- **`ZeroDivisionError`** — division or modulo by zero.
  ```python
  result = 10 / 0
  ```
- **`OverflowError`** — an arithmetic result is too large for the relevant representation.
  ```python
  import math
  result = math.exp(20000)
  ```
  On typical Python builds, this raises `OverflowError`.
- **`LookupError`** — base class for lookup failures.
- **`IndexError`** — sequence index is outside the valid range.
  ```python
  my_list = [10, 20, 30]
  print(my_list[5])
  ```
- **`KeyError`** — dictionary key is missing.
  ```python
  student = {"name": "Rahul", "age": 21}
  print(student["marks"])
  ```
- **`NameError`** — identifier cannot be found.
  ```python
  print(total_score)
  ```
- **`UnboundLocalError`** — a local variable is read before assignment.
  ```python
  count = 10

  def update_counter():
      print(count)
      count = count + 1

  update_counter()
  ```
  Since `count` is assigned inside the function, Python treats it as local there, so the earlier access raises `UnboundLocalError`.
- **`TypeError`** — operation applied to an inappropriate type.
  ```python
  x = 10
  y = "Hello"
  z = x + y
  ```
- **`ValueError`** — correct general type, but invalid value.
  ```python
  value = int("abc")
  ```
- **`AttributeError`** — requested object attribute does not exist.
- **`OSError`** — operating-system-related failure.
- **`FileNotFoundError`** — required file cannot be found.
- **`FileExistsError`** — target already exists when an operation expects to create it.
- **`PermissionError`** — operation lacks required permissions.
- **`ImportError`** — import operation fails.
- **`ModuleNotFoundError`** — requested module cannot be found.
- **`SyntaxError`** — invalid Python syntax.
- **`IndentationError`** — invalid indentation; a subclass of `SyntaxError`.
- **`RuntimeError`** — a runtime problem not described more specifically by another exception class.

## 7. Reference Table

| Exception | Typical cause |
|---|---|
| `ArithmeticError` | Arithmetic-related failure |
| `FloatingPointError` | Floating-point calculation failure |
| `ZeroDivisionError` | Division or modulo by zero |
| `OverflowError` | Arithmetic result exceeds supported range |
| `LookupError` | Lookup failure |
| `IndexError` | Sequence index out of range |
| `KeyError` | Dictionary key missing |
| `NameError` | Identifier not found |
| `UnboundLocalError` | Local variable read before assignment |
| `TypeError` | Inappropriate type |
| `ValueError` | Invalid value |
| `AttributeError` | Attribute does not exist |
| `OSError` | Operating-system failure |
| `FileNotFoundError` | File missing |
| `FileExistsError` | Target already exists |
| `PermissionError` | Insufficient permission |
| `ImportError` | Import failure |
| `ModuleNotFoundError` | Module missing |
| `SyntaxError` | Invalid syntax |
| `IndentationError` | Invalid indentation |
| `RuntimeError` | Other runtime failure |

## 8. Key Points

- `try` contains code that may fail.
- `except` handles a matching exception.
- `else` runs only when `try` succeeds.
- Exception classes have parent-child relationships.
- `ZeroDivisionError` is a subclass of `ArithmeticError`.
- `IndexError` and `KeyError` are subclasses of `LookupError`.
- `UnboundLocalError` is a subclass of `NameError`.
===============================================================================================================================================================
# Python Exception Handling — Part 3

## 1. Handling Multiple Exceptions

A `try` statement may contain more than one `except` clause. Each clause can handle a different exception type.

```python
try:
    # Code that may fail
    ...
except ExceptionType1:
    # Handle the first exception
    ...
except ExceptionType2:
    # Handle the second exception
    ...
```

For one exception occurrence, at most one matching `except` clause executes. Once Python selects a handler, it does not continue through the other sibling handlers.

## 2. Parent and Child Exception Classes

Some exceptions inherit from other exceptions:

```text
ArithmeticError
└── ZeroDivisionError
```

Because `ZeroDivisionError` is a subclass of `ArithmeticError`, an `except ArithmeticError` clause can also catch `ZeroDivisionError`.

### Correct order: child before parent

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
except ArithmeticError:
    print("Numeric calculation failed!")
```

Output:

```text
Division by 0 exception occurred!
```

### Incorrect order: parent before child

```python
try:
    result = 10 / 0
except ArithmeticError:
    print("Numeric calculation failed!")
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
```

Output:

```text
Numeric calculation failed!
```

The parent handler matches the child exception first, so the later child handler is not selected.

**Rule:** If both parent and child exceptions have separate handlers, place the child handler before the parent handler.

## 3. Output Question 1 — Successful Calculations

```python
import math

try:
    x = 10 / 5
    print(x)

    ans = math.exp(3)
    print(ans)

except ZeroDivisionError:
    print("Division by 0 exception occurred!")
except ArithmeticError:
    print("Numeric calculation failed!")
```

Output:

```text
2.0
20.085536923187668
```

Explanation:
1. `10 / 5` evaluates to `2.0`.
2. `math.exp(3)` calculates approximately \(e^3 = 20.085536923187668\).
3. No exception occurs, so neither handler executes.

## 4. Output Question 2 — Division by Zero First

```python
import math

try:
    x = 10 / 0
    print(x)

    ans = math.exp(20000)
    print(ans)

except ZeroDivisionError:
    print("Division by 0 exception occurred!")
except ArithmeticError:
    print("Numeric calculation failed!")
```

Output:

```text
Division by 0 exception occurred!
```

The first division immediately raises `ZeroDivisionError`. The following `print(x)` and `math.exp(20000)` statements are not reached.

## 5. Output Question 3 — Exponential Overflow

```python
import math

try:
    x = 10 / 5
    print(x)

    ans = math.exp(20000)
    print(ans)

except ZeroDivisionError:
    print("Division by 0 exception occurred!")
except ArithmeticError:
    print("Numeric calculation failed!")
```

Output:

```text
2.0
Numeric calculation failed!
```

Explanation:
1. The first calculation prints `2.0`.
2. On typical Python builds, `math.exp(20000)` raises `OverflowError`.
3. `OverflowError` is a subclass of `ArithmeticError`.
4. The `ArithmeticError` handler runs.
5. `print(ans)` is skipped because the assignment did not complete.

## 6. Output Question 4 — Parent Handler First

```python
import math

try:
    x = 10 / 5
    print(x)

    ans = math.exp(20000)
    print(ans)

except ArithmeticError:
    print("Numeric calculation failed!")
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
```

Output:

```text
2.0
Numeric calculation failed!
```

The exponential calculation raises an arithmetic exception, which the first handler catches.

## 7. Output Question 5 — Division by Zero with Parent First

```python
import math

try:
    x = 10 / 0
    print(x)

    ans = math.exp(20000)
    print(ans)

except ArithmeticError:
    print("Numeric calculation failed!")
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
```

Output:

```text
Numeric calculation failed!
```

The first operation raises `ZeroDivisionError`, which is also an `ArithmeticError`. Since the parent handler appears first, it runs.

## 8. Quick Revision

| Situation | Result |
|---|---|
| No exception occurs | `except` blocks are skipped |
| An exception occurs | A matching handler runs |
| Exception occurs partway through `try` | Remaining statements in that `try` block are skipped |
| Several `except` clauses exist | At most one matching handler runs |
| Parent and child handlers both exist | Put child first |
| `OverflowError` occurs | An `ArithmeticError` handler can catch it |
===================================================================================================================================================================
# Python Exception Handling — Part 4

## 1. Exercise: Ask Until Valid Input Is Entered

Write a program that:
1. Asks for two integers.
2. Calculates and displays their division.
3. If the user enters a non-integer value, asks again for valid integer input.
4. If the denominator is zero, asks for a non-zero denominator.
5. Repeats until valid input is supplied.
6. Displays the result and terminates after success.

## 2. Solution with Separate Exception Handlers

```python
while True:
    try:
        a = int(input("Input first no:"))
        b = int(input("Input second no:"))

        c = a / b
        print("Div is", c)

        break

    except ValueError:
        print("Please input integers only! Try again")

    except ZeroDivisionError:
        print("Please input non-zero denominator")
```

### How it works

- `while True` repeats the process.
- `int(input(...))` converts the input text into an integer.
- Invalid integer text raises `ValueError`.
- Dividing by zero raises `ZeroDivisionError`.
- The relevant handler prints a useful message; the loop then repeats.
- When division succeeds, the result is printed and `break` terminates the loop.

### Sample interaction

```text
Input first no: 10
Input second no: 0
Please input non-zero denominator

Input first no: a
Please input integers only! Try again

Input first no: 10
Input second no: a
Please input integers only! Try again

Input first no: 4
Input second no: 5
Div is 0.8
```

## 3. One `except` Clause for Multiple Exceptions

When several exception types need the same response, place their names inside a tuple after `except`.

```python
while True:
    try:
        a = int(input("Input first no:"))
        b = int(input("Input second no:"))

        c = a / b
        print("Div is", c)

        break

    except (ValueError, ZeroDivisionError):
        print("Either input is incorrect or denominator is 0. Try again!")
```

The handler catches either `ValueError` or `ZeroDivisionError`.

### Sample interaction

```text
Input first no: 4
Input second no: 0
Either input is incorrect or denominator is 0. Try again!

Input first no: 10
Input second no: bhopal
Either input is incorrect or denominator is 0. Try again!

Input first no: 10
Input second no: 4
Div is 2.5
```

### Separate vs. combined handlers

- Use separate handlers when each error needs a different message.
- Use a combined handler when the same response is appropriate for all listed exception types.

## 4. Handling All Exceptions with Bare `except`

Python permits an `except` clause without an exception class:

```python
try:
    # Code that may raise an exception
    ...
except:
    print("Some problem occurred. Try again!")
```

Example:

```python
while True:
    try:
        a = int(input("Input first no:"))
        b = int(input("Input second no:"))

        c = a / b
        print("Div is", c)

        break

    except:
        print("Some problem occurred. Try again!")
```

Sample interaction:

```text
Input first no: 10
Input second no: 0
Some problem occurred. Try again!

Input first no: 10
Input second no: a
Some problem occurred. Try again!

Input first no: 10
Input second no: 4
Div is 2.5
```

### Limitation of bare `except`

The handler does not name the exception type. A zero denominator and invalid input can produce the same message, so the program does not explain which problem occurred.

In production code, specific handlers are usually preferable. A bare `except:` can also catch exceptions such as `KeyboardInterrupt`, which are often better allowed to propagate. When a broad handler is genuinely needed, `except Exception:` is often safer.

## 5. Comparison of Exception-Handling Approaches

| Approach | Syntax | When useful |
|---|---|---|
| Separate handlers | `except ValueError:` and `except ZeroDivisionError:` | Different errors need different responses |
| Combined handler | `except (ValueError, ZeroDivisionError):` | Several errors share a response |
| Bare handler | `except:` | Broad handling, but exception type is not specified |

## 6. The `else` Keyword

`else` runs only when the `try` block completes without raising an exception.

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print("Result:", result)
```

Output:

```text
Result: 5.0
```

## 7. The `raise` Keyword

`raise` explicitly raises an exception when the program detects a condition it wants to report as an error.

```python
age = -2

if age < 0:
    raise ValueError("Age cannot be negative")
```

The code raises `ValueError` because a negative age is invalid for this example.

## 8. The `finally` Keyword

`finally` runs during normal cleanup flow whether or not an exception occurred. It is commonly used for cleanup actions.

```python
try:
    file = open("data.txt", "r", encoding="utf-8")
    content = file.read()
except FileNotFoundError:
    print("The requested file could not be found.")
else:
    print(content)
    print("File read successfully!")
finally:
    print("Executing cleanup operations")
```

If `data.txt` is missing, the error handler runs and `finally` still executes. If the file opens, this example should also close it; using `with` is a safer common pattern because it closes the file automatically:

```python
try:
    with open("data.txt", "r", encoding="utf-8") as file:
        content = file.read()
except FileNotFoundError:
    print("The requested file could not be found.")
else:
    print(content)
    print("File read successfully!")
finally:
    print("File-reading attempt completed.")
```

## 9. Exam-Oriented Questions

### Theory
1. Define exception handling.
2. Differentiate syntax errors and runtime exceptions.
3. Explain `try`, `except`, `else`, `raise`, and `finally`.
4. What happens when an exception is unhandled?
5. Explain `ValueError` and `ZeroDivisionError`.
6. What is exception hierarchy?
7. Why should child exception handlers appear before parent handlers?
8. How can one handler catch multiple exception types?
9. What is the limitation of a bare `except`?

### Programming
1. Write a program to divide two integers and handle a zero denominator.
2. Keep asking for input until valid integers are entered.
3. Handle `ValueError` and `ZeroDivisionError` separately.
4. Handle both exceptions with a single `except` clause.
5. Write a program using bare `except` and explain its limitation.
6. Predict the output when `ArithmeticError` is listed before `ZeroDivisionError`.

## 10. Final Memory Map

```text
Exception handling
├── try       risky code
├── except    handle an exception
├── else      runs when try succeeds
├── raise     raise an exception explicitly
└── finally   cleanup flow

Multiple exception handling
├── separate handlers
├── except (A, B)
└── bare except

Important rules
├── exception interrupts the try block
├── at most one matching handler runs
├── child handler before parent handler
└── while True + break can repeat input until success
```

## 11. Final Quick Revision

- Use `try` for statements that may fail.
- Use `except` to handle known exceptions.
- Use `else` for code that should run only after successful execution.
- Use `raise` to report an invalid condition as an exception.
- Use `finally` for cleanup code.
- `ValueError` commonly occurs when integer conversion receives invalid text.
- `ZeroDivisionError` occurs when the denominator is zero.
- `except (A, B)` catches either of two named exception types.
- A bare `except:` does not reveal which exception occurred.
- Put child exception handlers before parent exception handlers.
