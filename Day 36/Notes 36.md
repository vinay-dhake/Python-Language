# Python Exception Handling --- Part 1

## 1. Introduction

Exception handling is used to manage abnormal situations that occur
while a Python program is running. Without handling, an exception can
stop normal execution and display a technical traceback.

Exception handling is especially important in programs that accept user
input or interact with files, APIs, servers, or external data.

The material identifies Exception Handling, File Handling, and API
Calling as important Python building blocks for larger applications.

## 2. What Is an Exception?

An **exception** is an abnormal condition or error that occurs during
program execution.

For example:

``` python
a = 10
b = 0
c = a / b
```

This produces `ZeroDivisionError` because division by zero cannot be
performed.

Another example:

``` python
data = "abc"
number = int(data)
```

This produces `ValueError` because the string cannot be converted to an
integer.

## 3. What Happens When an Exception Occurs?

If an exception is not handled, Python stops normal execution at the
point of failure and displays information about the exception.

Consider:

``` python
a = int(input("Enter first no:"))
b = int(input("Enter second no:"))
c = a / b
print("Div is", c)
d = a + b
print("Sum is", d)
```

With input `10` and `5`:

``` text
Div is 2.0
Sum is 15
```

With input `10` and `0`, `c = a / b` raises `ZeroDivisionError`. The
later addition is not reached, even though `10 + 0` is valid.

A typical unhandled traceback is:

``` text
Traceback (most recent call last):
  File "except1.py", line 3, in <module>
    c = a / b
ZeroDivisionError: division by zero
```

The traceback is useful for a programmer, but a user-friendly
application may instead show a simple message such as:

``` text
Denominator should not be 0
```

## 4. Invalid Integer Input

The same sample program can fail earlier if the user enters a
non-integer value.

``` python
a = int(input("Enter first no:"))
b = int(input("Enter second no:"))
c = a / b
print("Div is", c)
d = a + b
print("Sum is", d)
```

If the second input is `2a`, conversion fails:

``` text
ValueError: invalid literal for int() with base 10: '2a'
```

The program stops before the division and addition.

## 5. Exception Handling

**Exception handling** is a mechanism that allows errors to be handled
gracefully while the program is running instead of allowing execution to
end abruptly.

The basic idea is:

``` text
Risky operation
      ↓
Exception occurs
      ↓
Matching handler
      ↓
Controlled response
```

For example:

``` python
try:
    c = 10 / 0
except ZeroDivisionError:
    print("Denominator should not be 0")
```

Output:

``` text
Denominator should not be 0
```

## 6. Why Exception Handling Is Needed

Without exception handling:

``` text
Invalid operation → exception → program stops
```

With exception handling:

``` text
Invalid operation → exception → handler → user-friendly response
```

Exception handling does not make an invalid operation valid. It gives
the program a controlled way to respond to the failure.

## 7. Syntax Error vs Runtime Exception

A **syntax error** occurs when Python code violates the language's
syntax rules.

Example:

``` python
print("Hello')
```

The string is not closed correctly.

A **runtime exception** occurs while syntactically valid code is
executing.

Example:

``` python
a = 10
b = 0
result = a / b
```

Here the syntax is valid, but execution raises `ZeroDivisionError`.

### Comparison

  -----------------------------------------------------------------------
  Syntax Error                        Runtime Exception
  ----------------------------------- -----------------------------------
  Code does not follow Python syntax  Syntax is valid but an operation
                                      fails during execution

  Detected while parsing              Occurs while executing

  Example: invalid quotation or       Example: division by zero
  indentation                         

  Prevents normal execution           Can be handled with
                                      exception-handling constructs
  -----------------------------------------------------------------------

## 8. Key Points

-   An exception is an abnormal condition during execution.
-   `10 / 0` raises `ZeroDivisionError`.
-   `int("2a")` raises `ValueError`.
-   An unhandled exception interrupts normal execution.
-   Statements after the point of failure are not executed.
-   Python displays a traceback for an unhandled exception.
-   Exception handling lets a program respond gracefully.
-   User-friendly messages can replace technical traceback messages.
=================================================================================================================================================================
# Python Exception Handling --- Part 2

## 1. Exception Handling Keywords

The material introduces five Python keywords associated with exception
handling:

``` text
try
except
else
raise
finally
```

The examples in this material mainly demonstrate `try`, `except`, and
`else`.

## 2. `try`

The `try` block contains operations that may generate an exception.

``` python
try:
    c = a / b
```

If an exception occurs, Python searches for an appropriate `except`
handler.

## 3. `except`

The `except` block handles a specified exception.

``` python
try:
    c = a / b
except ZeroDivisionError:
    print("Denominator should not be 0")
```

The name after `except` is an exception class.

## 4. `else`

The `else` block executes when the `try` block completes without an
exception.

``` python
try:
    # code that may fail
except SomeException:
    # runs if SomeException occurs
else:
    # runs if no exception occurs
```

The flow is:

``` text
Exception → except
No exception → else
```

## 5. Detailed `try-except-else` Syntax

``` python
try:
    # operations that may raise an exception
    ...

except ExceptionI:
    # handles ExceptionI
    ...

except ExceptionII:
    # handles ExceptionII
    ...

else:
    # executes when no exception occurs
    ...
```

`ExceptionI` and `ExceptionII` represent actual exception classes such
as `ValueError` or `ZeroDivisionError`.

## 6. Example --- Handling `ZeroDivisionError`

``` python
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

Input:

``` text
Enter first no:10
Enter second no:0
```

Output:

``` text
Denominator should not be 0
Sum is 10
```

With `10` and `3`:

``` text
Div is 3.3333333333333335
Sum is 13
```

When the exception occurs, the remaining statements in that `try` block
are skipped. Code after the complete `try-except` structure can execute.

## 7. Exception Hierarchy

Python exceptions are organized as classes. A simplified hierarchy
represented in the material is:

``` text
BaseException
    │
    └── Exception
         ├── ArithmeticError
         │    └── ZeroDivisionError
         ├── LookupError
         │    ├── IndexError
         │    └── KeyError
         ├── NameError
         │    └── UnboundLocalError
         ├── TypeError
         ├── ValueError
         ├── OSError
         │    ├── FileNotFoundError
         │    └── PermissionError
         └── SyntaxError
              └── IndentationError
```

The hierarchy diagram in the source also shows `RuntimeError` under
`Exception` and `FileNotFoundError`/`PermissionError` under `OSError`.

## 8. Important Exception Classes

### `Exception`

General base class for application-level exceptions.

### `ArithmeticError`

Base class for errors associated with numeric calculations.

### `FloatingPointError`

Associated with floating-point calculation failures.

### `ZeroDivisionError`

Raised when division or modulo by zero is attempted.

``` python
x = 10 / 0
```

### `OverflowError`

Associated with an arithmetic result that is too large to be represented
in the relevant numeric form.

### `LookupError`

Base class for lookup-related errors.

### `IndexError`

Raised when a sequence index is outside the valid range.

``` python
numbers = [10, 20, 30]
print(numbers[5])
```

### `KeyError`

Raised when a dictionary key is not present.

``` python
student = {"name": "Alice", "age": 21}
print(student["course"])
```

### `NameError`

Raised when an identifier cannot be found.

``` python
print(total_score)
```

Python is case-sensitive, so this also fails:

``` python
Print("Hello World")
```

### `UnboundLocalError`

A specialized `NameError` associated with using a local variable before
it has been assigned.

``` python
count = 10

def update_counter():
    print(count)
    count = count + 1

update_counter()
```

The assignment inside the function makes `count` local to that function,
so the earlier access produces `UnboundLocalError`.

### `TypeError`

Occurs when an operation or function is used with an inappropriate type.

``` python
a = 10
b = "20"
result = a + b
```

### `ValueError`

Occurs when an argument has an appropriate type but an invalid value.

``` python
data = "abc"
number = int(data)
```

### `AttributeError`

Raised when a non-existent attribute is referenced.

### `OSError`

Represents operating-system-related errors.

### `FileNotFoundError`

Raised when a required file is not present.

### `FileExistsError`

Raised when an operation tries to create something that already exists.

### `PermissionError`

Raised when an operation is attempted without the required access
rights.

### `SyntaxError`

Raised for invalid Python syntax.

### `IndentationError`

Raised when indentation is not specified correctly.

## 9. Exception Reference Table

  Exception              Main idea
  ---------------------- ------------------------------------------------
  `Exception`            General base class for application exceptions
  `ArithmeticError`      Numeric calculation-related errors
  `FloatingPointError`   Floating-point calculation failure
  `ZeroDivisionError`    Division or modulo by zero
  `OverflowError`        Arithmetic result too large for representation
  `LookupError`          Lookup-related failure
  `IndexError`           Sequence index out of range
  `KeyError`             Dictionary key not found
  `NameError`            Identifier not found
  `UnboundLocalError`    Local variable used before assignment
  `TypeError`            Inappropriate type for an operation/function
  `ValueError`           Appropriate type but invalid value
  `AttributeError`       Non-existent attribute referenced
  `OSError`              Operating-system-related error
  `FileNotFoundError`    Required file is missing
  `FileExistsError`      Target already exists
  `PermissionError`      Required access rights are missing
  `SyntaxError`          Invalid Python syntax
  `IndentationError`     Incorrect indentation

## 10. Important Hierarchy Rule

Exception classes can have parent-child relationships. For example:

``` text
ArithmeticError
       ↑
ZeroDivisionError
```

This relationship becomes important when multiple `except` clauses are
used. A parent handler can also match a child exception, so specific
child handlers must be considered before broader parent handlers.
===============================================================================================================================================================
# Python Exception Handling --- Part 3

## 1. Handling Multiple Exceptions

A `try` statement may have more than one `except` clause for different
exception types.

``` python
try:
    # risky code
except ExceptionType1:
    # handle first type
except ExceptionType2:
    # handle second type
```

For a particular exception occurrence, only one matching `except` clause
is executed.

## 2. Parent and Child Exception Classes

Exception classes are related through inheritance. For example:

``` text
ArithmeticError
       ↑
ZeroDivisionError
```

`ZeroDivisionError` is a child of `ArithmeticError`.

Therefore this can also match a division-by-zero exception:

``` python
except ArithmeticError:
    ...
```

## 3. Correct Order: Child Before Parent

When both child and parent exceptions are handled separately, put the
child first:

``` python
try:
    x = 10 / 0

except ZeroDivisionError:
    print("Division by 0 exception occurred!")

except ArithmeticError:
    print("Numeric calculation failed!")
```

The specific `ZeroDivisionError` handler gets the opportunity to run
first.

## 4. Incorrect Order: Parent Before Child

``` python
try:
    x = 10 / 0

except ArithmeticError:
    print("Numeric calculation failed!")

except ZeroDivisionError:
    print("Division by 0 exception occurred!")
```

`ZeroDivisionError` is also an `ArithmeticError`, so the first handler
already matches it. The later `ZeroDivisionError` handler does not get a
chance to run for that occurrence.

### Rule

``` text
Specific child exception
          ↓
Broader parent exception
```

## 5. Guess the Output --- Example 1

``` python
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

``` text
2.0
20.085536923187668
```

No exception occurs, so neither `except` block executes.

## 6. Guess the Output --- Example 2

``` python
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

``` text
Division by 0 exception occurred!
```

The first operation raises `ZeroDivisionError`. The remaining statements
in the `try` block are skipped, so `math.exp(20000)` is never reached.

## 7. Guess the Output --- Example 3

``` python
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

``` text
2.0
Numeric calculation failed!
```

The division succeeds and prints `2.0`. The large exponential
calculation produces an arithmetic overflow condition, so the
`ArithmeticError` handler runs. The later `print(ans)` is not executed.

## 8. Guess the Output --- Example 4

``` python
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

``` text
2.0
Numeric calculation failed!
```

The arithmetic overflow is matched by `ArithmeticError`.

## 9. Guess the Output --- Example 5

``` python
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

``` text
Numeric calculation failed!
```

The actual exception is `ZeroDivisionError`, but it is also an
`ArithmeticError`. Since the broader parent handler appears first, it
catches the exception before the specific handler gets a chance.

## 10. Execution Flow Inside `try`

If an exception occurs partway through a `try` block, the remaining
statements in that `try` block are skipped.

``` python
try:
    print("Statement 1")
    x = 10 / 0
    print("Statement 2")
except ZeroDivisionError:
    print("Exception handled")
```

Output:

``` text
Statement 1
Exception handled
```

`Statement 2` is never reached.

## 11. Multiple-Exception Handling: Key Rules

-   A `try` can have multiple `except` clauses.
-   Each clause may handle a different exception class.
-   For one exception occurrence, only one matching handler executes.
-   A parent exception can match a child exception.
-   Therefore, put specific child exceptions before broader parent
    exceptions.
-   Once an exception occurs, later statements in that `try` block are
    skipped.

## 12. Quick Revision Table

  -----------------------------------------------------------------------
  Situation                           Result
  ----------------------------------- -----------------------------------
  No exception in `try`               `except` blocks are skipped

  Exception occurs                    Matching `except` executes

  Exception occurs midway through     Remaining `try` statements are
  `try`                               skipped

  Several matching handlers           One appropriate handler executes

  Parent + child handlers             Put child before parent

  `ZeroDivisionError` with parent     Parent handler can catch it
  first                               
  -----------------------------------------------------------------------
==============================================================================================================================================================
# Python Exception Handling --- Part 4

## 1. Exercise --- Repeatedly Ask for Correct Input

Write a program that asks the user for two integers and calculates their
division.

The required behavior is:

-   If the user enters a non-integer value, ask for integers again.
-   If the denominator is zero, ask for a non-zero denominator.
-   Repeat until correct input is given.
-   Display the division only after valid input is supplied.
-   Terminate after successful input.

## 2. Logic of the Exercise

``` text
Ask for two values
       ↓
Convert to integers
       ↓
Conversion successful?
   No ───────→ ValueError handler → ask again
   Yes
       ↓
Is denominator zero?
   Yes ──────→ ZeroDivisionError handler → ask again
   No
       ↓
Calculate division
       ↓
Print result
       ↓
break
       ↓
Stop
```

## 3. Solution Using Separate Exception Handlers

``` python
while True:
    try:
        a = int(input("Input first no:"))
        b = int(input("Input second no:"))
        c = a / b
        print("Div is ", c)
        break

    except ValueError:
        print("Please input integers only! Try again")

    except ZeroDivisionError:
        print("Please input non-zero denominator")
```

## 4. Understanding `while True`

``` python
while True:
```

creates a loop that continues indefinitely until `break` is executed.

This is useful here because invalid input should cause the program to
ask again.

## 5. Understanding `int(input(...))`

``` python
a = int(input("Input first no:"))
```

`input()` returns text. `int()` attempts to convert that text to an
integer.

For example:

``` text
10 → valid integer
```

but:

``` text
a → ValueError
```

The same applies to the second input.

## 6. Handling `ValueError`

``` python
except ValueError:
    print("Please input integers only! Try again")
```

This runs when an input cannot be converted to an integer.

Example:

``` text
Input first no: a
Please input integers only! Try again
```

The loop then starts another iteration.

## 7. Handling `ZeroDivisionError`

``` python
except ZeroDivisionError:
    print("Please input non-zero denominator")
```

If the user enters:

``` text
Input first no: 10
Input second no: 0
```

`a / b` raises `ZeroDivisionError` and the message is displayed.

## 8. Successful Input

For:

``` text
Input first no: 4
Input second no: 5
```

the result is:

``` text
Div is  0.8
```

Then:

``` python
break
```

terminates the loop.

## 9. Sample Interaction

``` text
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
Div is  0.8
```

## 10. One `except` for Multiple Exceptions

When several exception types require the same response, their names can
be placed inside parentheses and separated by commas.

Syntax:

``` python
except (ExceptionType1, ExceptionType2):
    # common handling code
```

Example:

``` python
while True:
    try:
        a = int(input("Input first no:"))
        b = int(input("Input second no:"))
        c = a / b
        print("Div is ", c)
        break

    except (ValueError, ZeroDivisionError):
        print("Either input is incorrect or denominator is 0. Try again!")
```

## 11. How the Combined Handler Works

### Zero denominator

``` text
Input first no: 4
Input second no: 0
Either input is incorrect or denominator is 0. Try again!
```

### Invalid input

``` text
Input first no: 10
Input second no: bhopal
Either input is incorrect or denominator is 0. Try again!
```

### Correct input

``` text
Input first no: 10
Input second no: 4
Div is 2.5
```

## 12. Handling All Exceptions

An `except` clause can be written without an exception class name:

``` python
try:
    # operations
except:
    # handling code
```

The material describes this as a way to make the handler run for an
exception without specifying its type.

## 13. Example of Bare `except`

``` python
while True:
    try:
        a = int(input("Input first no:"))
        b = int(input("Input second no:"))
        c = a / b
        print("Div is ", c)
        break

    except:
        print("Some problem occurred. Try again!")
```

### Sample interaction

``` text
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

## 14. Limitation of Bare `except`

The material emphasizes that when the exception class is omitted, the
handler does not tell us which type of exception occurred.

For example, both `ValueError` and `ZeroDivisionError` can reach the
same handler:

``` python
except:
    print("Some problem occurred. Try again!")
```

The message is generic rather than identifying the actual exception.

Specific handlers are therefore useful when different errors need
different responses.

## 15. Specific vs Combined vs Bare Handling

### Separate handlers

``` python
except ValueError:
    print("Please input integers only!")

except ZeroDivisionError:
    print("Please input non-zero denominator")
```

Different exceptions receive different responses.

### One handler for several named exceptions

``` python
except (ValueError, ZeroDivisionError):
    print("Invalid input or zero denominator")
```

Several known exception types share one response.

### Bare handler

``` python
except:
    print("Some problem occurred")
```

The exception class is not specified.

## 16. Comparison Table

  -------------------------------------------------------------------------------------------
  Approach                Syntax                                      Main characteristic
  ----------------------- ------------------------------------------- -----------------------
  Separate handlers       `except ValueError:`                        Different exceptions
                                                                      can receive different
                                                                      responses

  Multiple types in one   `except (ValueError, ZeroDivisionError):`   Several named
  handler                                                             exceptions share one
                                                                      response

  Bare handler            `except:`                                   Exception class is not
                                                                      specified
  -------------------------------------------------------------------------------------------

## 17. Important Output Questions

### Question 1

``` python
try:
    x = 10 / 0
    print(x)
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
except ArithmeticError:
    print("Numeric calculation failed!")
```

Output:

``` text
Division by 0 exception occurred!
```

### Question 2

``` python
try:
    x = 10 / 0
    print(x)
except ArithmeticError:
    print("Numeric calculation failed!")
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
```

Output:

``` text
Numeric calculation failed!
```

The parent handler appears first and matches `ZeroDivisionError`.

### Question 3

``` python
try:
    x = 10 / 5
    print(x)
except ZeroDivisionError:
    print("Division by 0 exception occurred!")
except ArithmeticError:
    print("Numeric calculation failed!")
```

Output:

``` text
2.0
```

No exception occurs.

## 18. Exam-Oriented Questions

### Theory

1.  What is exception handling?
2.  What is an exception?
3.  What happens when an unhandled exception occurs?
4.  Explain `try`, `except`, and `else`.
5.  Name the five exception-handling keywords introduced in the
    material.
6.  Explain exception hierarchy.
7.  What is `ZeroDivisionError`?
8.  What is `ValueError`?
9.  What is `TypeError`?
10. What is `IndexError`?
11. What is `KeyError`?
12. What is `NameError`?
13. What is `UnboundLocalError`?
14. What is multiple-exception handling?
15. Why should child exceptions appear before parent exceptions?
16. How can multiple exception types be handled by one `except` clause?
17. What is a bare `except`?
18. What is the limitation of a bare `except`?

### Programming

1.  Write a program to divide two user-provided integers and handle
    `ZeroDivisionError`.
2.  Keep asking for input until two valid integers are entered.
3.  Handle `ValueError` and `ZeroDivisionError` separately.
4.  Handle both using one `except` clause.
5.  Write a program using a bare `except`.
6.  Predict output when `ArithmeticError` appears before
    `ZeroDivisionError`.
7.  Predict output when `ZeroDivisionError` appears before
    `ArithmeticError`.

## 19. Final Memory Map

``` text
                    EXCEPTION HANDLING
                           │
          ┌────────────────┼────────────────┐
          │                │                │
         try             except            else
          │                │                │
     risky code       handle error      no exception
                           │
             ┌─────────────┼──────────────┐
             │             │              │
        specific       multiple       all exceptions
        exception      exceptions        except:
             │             │
             │        (A, B, C)
             │
             ▼
      exception hierarchy
             │
       ┌─────┴─────┐
       │           │
 ArithmeticError  LookupError
       │           │
 ZeroDivision   IndexError
               KeyError
```

## 20. Final Quick Revision

``` text
Exception
    ↓
Abnormal condition during execution

try
    ↓
Code that may generate an exception

except
    ↓
Handles an exception

else
    ↓
Runs when no exception occurs

Multiple except
    ↓
Different handlers for different exceptions

Child exception
    ↓
Place before parent exception

Single handler for multiple exceptions
    ↓
except (A, B)

All-exception handler
    ↓
except:

Repeated input
    ↓
while True + try/except + break
```

## 21. Most Important Rules

1.  Put potentially failing code inside `try`.
2.  Handle the appropriate exception using `except`.
3.  If no exception occurs, an `else` block can execute.
4.  Once an exception occurs inside a `try` block, the remaining
    statements in that block are skipped.
5.  Multiple `except` clauses can be used.
6.  Only one matching `except` handler executes for a particular
    exception occurrence.
7.  When parent and child exception classes are both handled separately,
    put the child before the parent.
8.  Multiple exception types can be handled with
    `except (ValueError, ZeroDivisionError)`.
9.  A bare handler can be written as `except:`.
10. A bare handler does not identify the exception type in its handler.
11. A `while True` loop can repeatedly request valid input.
12. `break` can terminate that loop after successful input.
