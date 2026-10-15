# Python Exception Handling — Part 2
## Part 1: Exception Objects, Error Details, and Raising Exceptions

## 1. Accessing an Exception Object

When an exception occurs, Python creates an exception object containing information about the error. Inside an `except` block, assign that object to a variable using `as`.

```python
try:
    risky_operation()
except SomeException as error:
    print(error)
```

- `SomeException` is the exception type you want to catch.
- `as error` stores the exception object in `error`.
- `print(error)` displays the exception message.

The variable name is your choice. Common names include `e`, `error`, and `exc`.

### Example: division with input validation

```python
while True:
    try:
        a = int(input("Input first number: "))
        b = int(input("Input second number: "))

        result = a / b
        print("Division is", result)
        break

    except (ValueError, ZeroDivisionError) as e:
        print(e)
```

How it works:

1. `while True` repeats until `break` is reached.
2. `int(...)` converts input to an integer. Text such as `"abc"` raises `ValueError`.
3. `a / b` raises `ZeroDivisionError` if `b` is zero.
4. The `except` clause catches either listed exception and stores the exception object in `e`.
5. `print(e)` displays the error message.
6. If an exception occurs, the loop retries. If the inputs are valid and the denominator is nonzero, the result is printed and the loop ends.

Example interaction:

```text
Input first number: 10
Input second number: 0
division by zero
Input first number: 10
Input second number: abc
invalid literal for int() with base 10: 'abc'
Input first number: 10
Input second number: 5
Division is 2.0
```

Exact exception-message wording can vary slightly between Python versions.

### Catching multiple exception types

```python
except (ValueError, ZeroDivisionError) as e:
    print(e)
```

Use a tuple when the same response is suitable for each error. If different errors need different responses, use separate handlers:

```python
try:
    number = int(input("Enter a number: "))
    result = 100 / number
except ValueError:
    print("Please enter an integer.")
except ZeroDivisionError:
    print("The number must not be zero.")
```

---

## 2. Obtaining Full Exception Details with `traceback`

An exception message alone may not be enough when debugging. Python's built-in `traceback` module can format details similar to the traceback displayed when a program fails.

A traceback can include:

- The file in which the exception occurred.
- The line number associated with the failure.
- The code location that raised the exception.
- The exception class, such as `ValueError` or `ZeroDivisionError`.
- The exception message.

### `traceback.format_exc()`

`traceback.format_exc()` returns the current exception's formatted traceback as a string. It is commonly called inside an exception handler.

```python
import traceback

try:
    value = 10 / 0
except:
    print(traceback.format_exc())
```

The traceback includes the `ZeroDivisionError` and its message. The filename, line number, and exact formatting depend on where the code runs.

### Full input example

```python
import traceback

while True:
    try:
        a = int(input("Input first number: "))
        b = int(input("Input second number: "))

        result = a / b
        print("Division is", result)
        break

    except:
        print(traceback.format_exc())
```

If the denominator is zero, the traceback explains that division by zero occurred. If the user enters text that cannot be converted to an integer, it identifies the `ValueError` and the conversion line.

### Prefer catching expected exceptions

A bare `except:` catches almost every exception, including errors you may not intend to suppress. For input validation, explicit exception types are usually preferable:

```python
import traceback

while True:
    try:
        a = int(input("Input first number: "))
        b = int(input("Input second number: "))
        result = a / b
        print("Division is", result)
        break

    except (ValueError, ZeroDivisionError):
        print(traceback.format_exc())
```

This catches the two expected errors. Other exceptions are allowed to propagate.

### `print(e)` versus `traceback.format_exc()`

| Approach | What it provides | Typical use |
|---|---|---|
| `print(e)` | The exception message | Showing a short error |
| `traceback.format_exc()` | Formatted traceback details | Debugging and locating an error |

For user-facing applications, avoid exposing internal paths or implementation details unnecessarily. Detailed tracebacks are usually more appropriate for development logs.

---

## 3. Raising an Exception with `raise`

Python raises exceptions automatically when an operation fails. You can also deliberately raise an exception when your program detects a condition that should not be allowed.

### Syntax

```python
raise ExceptionClassName
```

Or provide a message:

```python
raise ExceptionClassName("Helpful error message")
```

Examples:

```python
raise ValueError
```

```python
raise ValueError("Age cannot be negative.")
```

The second form includes a message that explains the problem.

### Example: reject a negative age

```python
age = int(input("Enter age: "))

if age < 0:
    raise ValueError("Age cannot be negative.")

print("Age:", age)
```

If the user enters a negative number, Python raises `ValueError`. Because this example does not catch the exception, the program stops and displays a traceback.

### Raising and handling an exception together

```python
try:
    age = int(input("Enter age: "))

    if age < 0:
        raise ValueError("Age cannot be negative.")

    print("Age:", age)

except ValueError as e:
    print("Invalid input:", e)
```

If the user enters `-5`, the output is:

```text
Invalid input: Age cannot be negative.
```

If the user enters text instead of an integer, `int(...)` also raises `ValueError`, and the same handler catches it. If these situations need different messages, handle conversion and range validation separately.

---

## 4. Exercise: Validate Two Integers Before Division

### Requirements

Write a program that repeatedly asks for a numerator and denominator. It should:

1. Ask for two integers.
2. If either input is not an integer, ask for integers only.
3. If the denominator is zero, ask for a non-zero denominator.
4. If either number is negative, or the numerator is zero, display a message that negative numbers are not allowed. The exercise treats a zero numerator as invalid too.
5. Repeat until valid inputs are provided.
6. Print the division result and stop once the inputs are valid.

### Solution using `raise`

```python
while True:
    try:
        a = int(input("Input first number: "))
        b = int(input("Input second number: "))

        if a <= 0 or b < 0:
            raise Exception("Negative numbers not allowed! Try again")

        result = a / b
        print("Division is", result)
        break

    except ValueError:
        print("Please input integers only! Try again")

    except ZeroDivisionError:
        print("Please input a non-zero denominator")

    except Exception as e:
        print(e)
```

### Explanation

- `while True` repeats the input process.
- `int(input(...))` converts each input to an integer.
- `a <= 0 or b < 0` rejects a numerator less than or equal to zero and a negative denominator.
- `raise Exception(...)` deliberately raises an exception when the validation rule fails.
- `except ValueError` handles inputs that cannot be converted to integers.
- `except ZeroDivisionError` handles division by zero.
- `except Exception as e` catches the deliberately raised general exception and prints its message.
- `break` ends the loop only after division succeeds.

### Example interaction

```text
Input first number: 10
Input second number: -4
Negative numbers not allowed! Try again
Input first number: 10
Input second number: 0
Please input a non-zero denominator
Input first number: -1
Input second number: 4
Negative numbers not allowed! Try again
Input first number: 10
Input second number: bhopal
Please input integers only! Try again
Input first number: 20
Input second number: 5
Division is 4.0
```

### A useful refinement

The example uses `Exception` for a validation rule. In larger programs, a more specific built-in exception such as `ValueError` or a custom exception can communicate intent more clearly.

---

## 5. Quick Revision

- Use `except ExceptionType as e` to access the exception object.
- `print(e)` displays the exception message.
- `traceback.format_exc()` returns formatted traceback details as a string.
- Use `raise` to deliberately generate an exception when a rule is violated.
- Use separate `except` blocks when different errors need different messages.
- Use a loop to keep asking for input until the required conditions are met.
# Python Exception Handling — Part 2
## Part 2: Bank Accounts, the `finally` Block, and Output Tracing

## 6. Exercise: Build a `BankAccount` Class

This exercise combines object-oriented programming with exception handling.

### Requirements

Create a `BankAccount` class that supports:
- An initial balance.
- Depositing money.
- Withdrawing money.
- Raising an exception if the requested withdrawal is greater than the available balance.

### Solution

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance

    def deposit(self, amount):
        self.balance += amount
        print(f"Deposited: {amount}")
        print(f"New balance: {self.balance}")

    def withdraw(self, amount):
        if amount > self.balance:
            raise ValueError("Insufficient funds!")

        self.balance -= amount
        print(f"Withdrawn: {amount}")
        print(f"Remaining balance: {self.balance}")


try:
    account = BankAccount(5000)
    account.deposit(2000)
    account.withdraw(8000)

except ValueError as e:
    print("Error:", e)
```

### Output

```text
Deposited: 2000
New balance: 7000
Error: Insufficient funds!
```

### Explanation

#### Constructor

```python
def __init__(self, balance):
    self.balance = balance
```

The constructor runs when a `BankAccount` object is created. `self.balance` stores the balance as an instance attribute. `BankAccount(5000)` starts with a balance of `5000`.

#### Deposit method

```python
self.balance += amount
```

This adds the deposit to the current balance. A deposit of `2000` changes the balance from `5000` to `7000`.

#### Withdrawal method

```python
if amount > self.balance:
    raise ValueError("Insufficient funds!")
```

The method checks the withdrawal amount before changing the balance. If the amount exceeds the available balance, it raises `ValueError`. The remaining statements in `withdraw()` are skipped after the exception is raised.

If the amount is valid, `self.balance -= amount` subtracts it and the method prints the withdrawal and remaining balance.

#### Handling the exception

```python
except ValueError as e:
    print("Error:", e)
```

The exception is caught outside the class. The class detects the invalid operation, while the calling code decides how to report it.

### Try a successful withdrawal

Replace:

```python
account.withdraw(8000)
```

with:

```python
account.withdraw(3000)
```

The balance after the deposit is `7000`, so the withdrawal succeeds and the remaining balance becomes `4000`.

### Practical improvements

The exercise focuses on exception handling. A real account class should also validate that deposits and withdrawals are positive numbers and should consider how to handle invalid data types.

---

## 7. The `finally` Block

The `finally` block contains code that should run whether an exception occurs or not. It is especially useful for cleanup operations.

Common cleanup tasks include:
- Closing a file.
- Releasing a resource.
- Disconnecting from a database.
- Logging out a user.
- Returning an ATM card after a transaction.

### Syntax with `except` and `finally`

```python
try:
    # Code that might raise an exception
    risky_operation()

except SomeException:
    # Handle the selected exception
    handle_error()

finally:
    # Cleanup code
    cleanup()
```

### Syntax with `finally` but no `except`

```python
try:
    # Code that might raise an exception
    risky_operation()
finally:
    # Code to run as the try statement exits
    cleanup()
```

The `except` block is optional when a `try` statement has a `finally` block. In the second form, an exception is not handled by an `except` clause. The `finally` block runs, and then the exception continues propagating.

### How the blocks work together

- `try`: contains operations that may fail.
- `except`: handles exception types that match the error raised.
- `finally`: performs cleanup when execution leaves the `try` statement, whether normally or through an exception.

A `finally` block is not a replacement for `except`. It is primarily for cleanup code that should run on the way out.

---

## 8. File Cleanup with `finally`

Files should be closed after use. If an error occurs while processing a file, cleanup should still be attempted.

```python
file = None

try:
    file = open("data.txt", "r")
    content = file.read()
    print("Data processed successfully.")

except FileNotFoundError:
    print("Error: The requested file could not be found.")

except Exception as e:
    print(f"An unexpected error occurred: {e}")

finally:
    if file is not None:
        file.close()
        print("File handle closed safely in finally block.")
```

### Explanation

1. `file = None` establishes an initial value. This matters because opening the file might fail before a file object is assigned.
2. `open("data.txt", "r")` attempts to open the file for reading.
3. `file.read()` reads its content.
4. `FileNotFoundError` handles the case in which the file does not exist.
5. `except Exception as e` catches other ordinary exceptions and displays their messages.
6. `finally` runs as the `try` statement exits.
7. `if file is not None` ensures `close()` is called only if opening succeeded.

If the file cannot be opened, `file` remains `None`, so the cleanup condition is false. If opening succeeds, the file is closed when execution reaches `finally`.

### Modern alternative: `with`

Python's context manager syntax automatically closes a file when the `with` block exits:

```python
try:
    with open("data.txt", "r") as file:
        content = file.read()
        print("Data processed successfully.")

except FileNotFoundError:
    print("Error: The requested file could not be found.")
```

Both approaches are useful to understand. The explicit `finally` example demonstrates cleanup logic; `with open(...)` is generally preferred for ordinary file handling.

---

## 9. Guess the Output: No Exception

```python
try:
    print("A")
    result = 10 / 2
    print("B")

except ZeroDivisionError:
    print("C")

finally:
    print("D")
```

### Execution trace

1. `print("A")` runs.
2. `10 / 2` succeeds and assigns `5.0` to `result`.
3. `print("B")` runs.
4. There is no exception, so the `except` block is skipped.
5. The `finally` block prints `D`.

### Output

```text
A
B
D
```

**Key rule:** `finally` runs even when the `try` block completes successfully.

---

## 10. Guess the Output: Exception Is Handled

```python
try:
    print("A")
    result = 10 / 0
    print("B")

except ZeroDivisionError:
    print("C")

finally:
    print("D")
```

### Execution trace

1. `print("A")` runs.
2. `10 / 0` raises `ZeroDivisionError`.
3. The remaining statements in `try` are skipped, so `print("B")` does not run.
4. The matching `except ZeroDivisionError` block prints `C`.
5. The `finally` block prints `D`.

### Output

```text
A
C
D
```

**Key rule:** When an exception occurs, Python skips the remaining statements in the `try` block and looks for a matching handler.

---

## 11. Guess the Output: Exception Is Not Handled

```python
try:
    print("A")
    result = int("abc")
    print("B")

except ZeroDivisionError:
    print("C")

finally:
    print("D")
```

### Execution trace

1. `print("A")` runs.
2. `int("abc")` raises `ValueError`, because `"abc"` is not a valid integer representation.
3. The handler only catches `ZeroDivisionError`, so it does not match.
4. `print("B")` is skipped.
5. The `finally` block prints `D`.
6. After `finally` completes, the unhandled `ValueError` propagates and Python reports a traceback.

### Output pattern

```text
A
D
Traceback (most recent call last):
    ...
ValueError: invalid literal for int() with base 10: 'abc'
```

The traceback's filename and line numbers depend on where the program runs.

**Key rule:** `finally` still runs when an exception is unhandled. It does not automatically catch or suppress that exception.

---

## 12. `finally` Inside an Input Loop: Guess the Output

```python
while True:
    try:
        a = int(input("Input first number: "))
        b = int(input("Input second number: "))

        result = a / b
        print("Division is", result)
        break

    except ZeroDivisionError:
        print("Denominator should not be zero")

    finally:
        print("Thank you for using the app!")
```

### Case A: Denominator is zero

Input:

```text
Input first number: 10
Input second number: 0
```

- Division raises `ZeroDivisionError`.
- The `except` block prints the denominator error.
- The `finally` block prints the thank-you message.
- The loop continues because no `break` was reached.

Output for this attempt:

```text
Denominator should not be zero
Thank you for using the app!
```

### Case B: Valid division

Input:

```text
Input first number: 10
Input second number: 5
```

- Division succeeds.
- The result `2.0` is printed.
- `break` requests that the loop end.
- The `finally` block prints its message as the `try` statement exits.

Output for this attempt:

```text
Division is 2.0
Thank you for using the app!
```

### Case C: Input is not an integer

Input:

```text
Input first number: 10
Input second number: a
```

- `int("a")` raises `ValueError`.
- The only `except` block catches `ZeroDivisionError`, so the `ValueError` is not handled.
- The `finally` block prints the thank-you message.
- The unhandled `ValueError` then terminates normal execution and produces a traceback.

Output pattern:

```text
Thank you for using the app!
Traceback (most recent call last):
    ...
ValueError: invalid literal for int() with base 10: 'a'
```

### Important observation

The `finally` block runs before control leaves the `try` statement, including when `break` or an unhandled exception is involved. In this example, the thank-you message appears after each attempt, not just once at the very end.

To handle non-integer input gracefully, add an `except ValueError` block.

# Python Exception Handling — Part 2
## Part 3: ATM Exercise, User-Defined Exceptions, and Revision

## 13. Exercise: An OOP-Based ATM Withdrawal System

This exercise combines a class, an instance method, exception handling, and a `finally` block.

### Requirements

Create an ATM simulation that:
1. Defines an `ATM` class.
2. Has an instance method named `withdraw()`.
3. Starts with a balance of ₹10,000.
4. Raises an exception if a requested withdrawal exceeds ₹5,000.
5. Raises an exception if the withdrawal exceeds the available balance.
6. Uses `try`, `except`, and `finally`.
7. Prints a suitable success or failure message.
8. Always prints a message indicating that the card is returned.

### Complete example

```python
class ATM:
    def __init__(self, card_number):
        self.card_number = card_number
        self.balance = 10000

    def withdraw(self):
        try:
            print(f"Card inserted: {self.card_number}")
            print("Processing transaction...")

            amount = int(input("Enter amount to withdraw: "))

            if amount > 5000:
                raise ValueError(
                    "Amount exceeds ATM withdrawal limit of ₹5000!"
                )

            if amount > self.balance:
                raise ValueError("Insufficient balance!")

            self.balance -= amount
            print(f"Please collect your cash: ₹{amount}")
            print(f"Remaining balance: ₹{self.balance}")

        except ValueError as e:
            print("Transaction failed:", e)

        finally:
            print("Card returned")


atm = ATM("1234-5678-9999")
atm.withdraw()
```

### Explanation

#### Constructor

```python
def __init__(self, card_number):
    self.card_number = card_number
    self.balance = 10000
```

- `self.card_number` stores the card identifier for this object.
- `self.balance` initializes the account balance to ₹10,000.

The card number is sample data for an educational simulation. A real banking system must not expose or handle card details in this simplistic way.

#### Read the withdrawal amount

```python
amount = int(input("Enter amount to withdraw: "))
```

The user must enter an integer. If the input is text such as `hello`, `int(...)` raises `ValueError`, which is caught by the handler.

#### Enforce the ATM limit

```python
if amount > 5000:
    raise ValueError("Amount exceeds ATM withdrawal limit of ₹5000!")
```

A withdrawal above ₹5,000 is rejected by deliberately raising `ValueError`.

#### Check the balance

```python
if amount > self.balance:
    raise ValueError("Insufficient balance!")
```

This checks that the account has enough funds. The amount is not deducted if either validation raises an exception.

#### Update the balance

```python
self.balance -= amount
```

This statement executes only after both checks pass.

#### Handle failure

```python
except ValueError as e:
    print("Transaction failed:", e)
```

The exception object is assigned to `e`, and its message is included in the failure output.

#### Return the card in `finally`

```python
finally:
    print("Card returned")
```

This runs after a successful transaction or after a handled `ValueError`. It also runs before an unhandled exception propagates out of the `try` statement.

### Example: successful withdrawal

If the user enters `2000`, the output is:

```text
Card inserted: 1234-5678-9999
Processing transaction...
Enter amount to withdraw: 2000
Please collect your cash: ₹2000
Remaining balance: ₹8000
Card returned
```

### Example: amount exceeds the limit

If the user enters `6000`, the output is:

```text
Card inserted: 1234-5678-9999
Processing transaction...
Enter amount to withdraw: 6000
Transaction failed: Amount exceeds ATM withdrawal limit of ₹5000!
Card returned
```

### Example: invalid input

If the user enters `abc`, converting the input to an integer raises `ValueError`. The `except` block prints a transaction-failed message, and the `finally` block still prints `Card returned`.

### Further validation

The exercise focuses on the upper withdrawal limit and available balance. A more complete implementation should also reject zero and negative withdrawal amounts:

```python
if amount <= 0:
    raise ValueError("Withdrawal amount must be positive.")
```

This prevents nonsensical withdrawal requests.

---

## 14. Creating User-Defined Exceptions

Python has many built-in exception classes, including `ValueError`, `TypeError`, `ZeroDivisionError`, and `FileNotFoundError`.

Sometimes an application has a specific rule that is easier to communicate with its own exception type. Such an exception is called a **user-defined exception** or **custom exception**.

### Why create a custom exception?

A custom exception can:
- Give a domain-specific name to an error.
- Make validation code easier to understand.
- Allow a handler to catch one particular application error without catching unrelated errors.
- Separate an application's rules from Python's general built-in errors.

For example, an application could define `NegativeNumberException` for a rule that rejects negative values.

### Defining a custom exception

A custom exception is created by defining a class that inherits, directly or indirectly, from Python's `Exception` class.

```python
class NegativeNumberException(Exception):
    pass
```

- `class NegativeNumberException(Exception):` declares a new exception class.
- Inheriting from `Exception` makes it part of Python's normal exception hierarchy.
- `pass` means the class body contains no additional implementation. The inherited exception behavior is enough for this example.

### Raising the custom exception

```python
raise NegativeNumberException("Negative numbers are not allowed.")
```

This creates and raises an instance of `NegativeNumberException`, with the supplied message.

### Catching the custom exception

```python
try:
    number = int(input("Enter a positive number: "))

    if number < 0:
        raise NegativeNumberException("Negative numbers are not allowed.")

    print("Number:", number)

except ValueError:
    print("Please enter an integer.")

except NegativeNumberException as e:
    print(e)
```

If the user enters `-4`, the custom exception is raised and caught by its dedicated handler. If the user enters text, `int(...)` raises the built-in `ValueError`, which is handled separately.

---

## 15. Complete Example: Division Using a Custom Exception

This program combines a custom exception with input conversion errors, division by zero, and a retry loop.

```python
class NegativeNumberException(Exception):
    pass


while True:
    try:
        a = int(input("Input first number: "))
        b = int(input("Input second number: "))

        if a <= 0 or b < 0:
            raise NegativeNumberException(
                "Negative numbers are not allowed! Try again"
            )

        result = a / b
        print("Division is", result)
        break

    except ValueError:
        print("Please input integers only! Try again")

    except ZeroDivisionError:
        print("Please input a non-zero denominator")

    except NegativeNumberException as e:
        print(e)
```

### How it works

1. The custom exception class is defined before the loop.
2. The loop requests two integer inputs.
3. `ValueError` handles text that cannot be converted to an integer.
4. The condition `a <= 0 or b < 0` checks the validation rule used in this example.
5. If the rule is violated, `NegativeNumberException` is raised.
6. `ZeroDivisionError` handles division by zero.
7. The custom exception handler prints its message.
8. If an attempt fails, the loop continues.
9. When the inputs pass the checks and division succeeds, the result is printed and `break` ends the loop.

### Example interaction

```text
Input first number: 10
Input second number: -3
Negative numbers are not allowed! Try again
Input first number: 10
Input second number: 0
Please input a non-zero denominator
Input first number: 10
Input second number: a
Please input integers only! Try again
Input first number: 10
Input second number: 5
Division is 2.0
```

### Note about the validation condition

The code uses:

```python
if a <= 0 or b < 0:
```

This rejects a numerator of zero or below and a negative denominator. A denominator of zero is not rejected by this condition; instead, division raises `ZeroDivisionError`, which is handled separately. The wording of the custom error message follows the exercise's intended rule, although a more precise message could say that the numerator must be positive and the denominator must be non-negative.

If the goal is to require both numbers to be strictly positive, use:

```python
if a <= 0 or b <= 0:
    raise NegativeNumberException("Both numbers must be positive.")
```

Then a zero denominator is caught by the custom validation first, rather than by division. Choose the condition that matches the required exercise specification.

---

## 16. Built-In Exceptions vs. User-Defined Exceptions

| Built-in exception | Typical meaning |
|---|---|
| `ValueError` | A value has an inappropriate format or value for an operation |
| `TypeError` | An operation or function receives an unsuitable type |
| `ZeroDivisionError` | A division or modulo operation uses zero as the divisor |
| `FileNotFoundError` | An attempt to access a file fails because it cannot be found |

| User-defined exception | Typical purpose |
|---|---|
| `NegativeNumberException` | Represent an application's rule against negative values |
| `InsufficientFundsError` | Represent an account operation that exceeds available funds |
| `WithdrawalLimitError` | Represent a withdrawal that exceeds a configured limit |

The names in the second table are examples of possible application-specific exception classes; they are not Python built-ins.

---

## 17. Quick Comparison: `raise`, `except`, and `finally`

| Keyword or block | Purpose | Example |
|---|---|---|
| `raise` | Deliberately raises an exception | `raise ValueError("Invalid age")` |
| `except` | Catches a matching exception | `except ValueError as e:` |
| `finally` | Runs cleanup as the `try` statement exits | `finally: print("Cleanup")` |

These constructs do different jobs: `raise` signals a problem, `except` handles a matching problem, and `finally` performs final actions.

---

## 18. Important Rules to Remember

1. **Capture an exception object with `as`.**

   ```python
   except ValueError as e:
       print(e)
   ```

2. **`traceback.format_exc()` returns formatted traceback details.** It is useful for debugging and should normally be called while handling an exception.

3. **`raise` can generate an exception deliberately.**

   ```python
   raise ValueError("Invalid value")
   ```

4. **Catch specific exception types when possible.** This makes it clear which failures the program expects.

5. **The `finally` block runs whether the `try` block succeeds or raises an exception.** If an exception is not caught, it normally continues propagating after `finally` finishes.

6. **A custom exception should inherit from `Exception`**, directly or indirectly.

7. **A retry loop needs a clear success exit.** In these examples, `break` ends the loop after valid input and successful computation.

8. **Validate before changing state.** In the account and ATM examples, the withdrawal amount is checked before the balance is reduced.

---

## 19. Practice Questions

Try to answer these before looking at the solutions.

### Question 1: What is printed?

```python
try:
    print("Start")
    value = 8 / 2
except ZeroDivisionError:
    print("Error")
finally:
    print("End")
```

**Answer:**

```text
Start
End
```

The division succeeds, so the `except` block is skipped. The `finally` block runs.

### Question 2: What is printed before the exception is reported?

```python
try:
    print("A")
    int("hello")
except ZeroDivisionError:
    print("B")
finally:
    print("C")
```

**Answer pattern:**

```text
A
C
Traceback (most recent call last):
    ...
ValueError: invalid literal for int() with base 10: 'hello'
```

`ValueError` does not match the `ZeroDivisionError` handler. The `finally` block runs before the unhandled exception propagates.

### Question 3: Write a custom exception

Define `InvalidAgeError` and raise it when an age is negative.

**One possible solution:**

```python
class InvalidAgeError(Exception):
    pass


try:
    age = int(input("Enter age: "))

    if age < 0:
        raise InvalidAgeError("Age cannot be negative.")

    print("Age accepted.")

except ValueError:
    print("Please enter an integer.")

except InvalidAgeError as e:
    print(e)
```

### Question 4: Why is `finally` useful in the ATM exercise?

**Answer:** It ensures the card-return message is printed after a successful transaction or after a handled transaction error, instead of placing the cleanup message in multiple branches.

### Question 5: Why check the balance before subtracting a withdrawal?

**Answer:** If the requested amount is too large, the program raises an exception before changing the account balance. This prevents an invalid operation from updating the object's state.

---

## 20. Final Cheat Sheet

- **Exception object:** `except SomeError as e`
- **Print the error message:** `print(e)`
- **Formatted traceback:** `traceback.format_exc()`
- **Raise a built-in exception:** `raise ValueError("message")`
- **Define a custom exception:** `class MyError(Exception): pass`
- **Catch a custom exception:** `except MyError as e:`
- **Cleanup block:** `finally:`
- **Common cleanup tasks:** close files, release resources, return cards, disconnect sessions.
- **Reliable validation pattern:** validate inputs, raise a suitable exception if a rule is violated, catch expected errors, and repeat until successful input is received.
