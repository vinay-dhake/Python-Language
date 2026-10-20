# Python Programming Series — Lecture 39
## Advanced File Handling, Resource Management & Exception Handling

> **Topics covered:** Safe file closing, `locals()`, `None`, file-reading methods, line-by-line processing, and filtering integers from a text file.

---

## Table of Contents

1. [Robust Resource Management](#1-robust-resource-management)
   - [Method A: Check `locals()`](#method-a-check-locals)
   - [Method B: Initialize with `None`](#method-b-initialize-with-none-recommended)
2. [Reading Data from Files](#2-reading-data-from-files)
   - [`read()`](#a-read-the-entire-file-with-read)
   - [Write Multiple Lines](#b-write-multiple-lines-until-blank-input)
   - [`readline()`](#c-read-one-line-at-a-time-with-readline)
   - [`readlines()`](#d-read-all-lines-into-a-list-with-readlines)
3. [Case Study: Extract Integers from a File](#3-case-study-extract-integers-from-a-file)
4. [Method Summary](#4-method-summary)
5. [Best Practices](#5-best-practices)

---

## 1. Robust Resource Management

When working with files, we should close an opened file after completing the operation. A common approach is to call `f.close()` in a `finally` block.

However, consider this situation:

```python
try:
    f = open("G:/message.txt", "w")
except OSError as ex:
    print("Could not open the file:", ex)
finally:
    f.close()
```

If `open()` fails, the assignment to `f` never completes. If `f` was not defined earlier, `f.close()` raises a `NameError`.

We need to check whether a file object was successfully created before trying to close it.

### Method A: Check `locals()`

`locals()` returns a dictionary representing the current local namespace. We can check whether `'f'` is a key in that dictionary.

```python
try:
    f = open("G:/message.txt", "w")
    text = input("Type something: ")
    f.write(text)

except FileNotFoundError as ex:
    print("Cannot create the file:", ex)
except OSError as ex:
    print("Cannot write the data:", ex)

finally:
    if 'f' in locals():
        f.close()

    print("Execution completed.")
```

**Important points:**
- Dictionary keys are strings, so use `'f'`, not `f`.
- `locals()` checks the current local namespace.
- This can work, but it is less straightforward than initializing the variable explicitly.

### Method B: Initialize with `None` (Recommended)

Set `f = None` before entering the `try` block. If opening the file fails, `f` remains `None`. If opening succeeds, `f` refers to a file object.

```python
f = None

try:
    f = open("D:/message.txt", "w")
    text = input("Type something: ")
    f.write(text + "\n")
    print("File saved successfully.")

except FileNotFoundError as ex:
    print("Cannot create the file:", ex)
except OSError as ex:
    print("Cannot write the data:", ex)

finally:
    if f is not None:
        f.close()
        print("File closed successfully.")
```

**Why does this work?**

| Situation | Value of `f` | Action in `finally` |
|---|---|---|
| Opening the file fails | `None` | Does not call `close()` |
| Opening succeeds | File object | Calls `close()` |

> **Best practice:** For simple examples using `try`/`finally`, initialize the file variable to `None` and check it before closing.

### An Even Simpler Approach: `with open(...)`

Python's context manager automatically closes the file when the `with` block exits, including when an exception occurs.

```python
try:
    with open("message.txt", "w", encoding="utf-8") as f:
        text = input("Type something: ")
        f.write(text + "\n")
        print("File saved successfully.")

except OSError as ex:
    print("File operation failed:", ex)
```

For most everyday file operations, **`with open(...)` is the recommended approach** because it handles cleanup automatically.

---

## 2. Reading Data from Files

Python provides three commonly used file-reading methods.

### A. Read the Entire File with `read()`

The `read()` method reads the remaining file content and returns it as a single string.

```python
try:
    with open("message.txt", "r", encoding="utf-8") as f:
        text = f.read()
        print(text)

except FileNotFoundError:
    print("File not found.")
except OSError as ex:
    print("Could not read the file:", ex)
```

**Use it when:** The file is small enough to comfortably fit in memory and you need its entire content.

### B. Write Multiple Lines Until Blank Input

This program keeps accepting input until the user presses `Enter` on an empty line.

```python
lines_count = 0

try:
    with open("message.txt", "w", encoding="utf-8") as f:
        print("Type your text. Press Enter on a blank line to stop.")

        while True:
            text = input()

            if text == "":
                break

            f.write(text + "\n")
            lines_count += 1

    print(f"Total lines saved: {lines_count}")

except OSError as ex:
    print("Could not write the file:", ex)
```

**How it works:**
1. Opens the file in write mode (`"w"`).
2. Reads one line of input at a time.
3. Stops when the input is an empty string.
4. Writes each non-empty line followed by `\n`.
5. Counts the number of lines written.

> **Note:** Write mode (`"w"`) creates a file if it does not exist and overwrites its existing contents if it does.

### C. Read One Line at a Time with `readline()`

`readline()` reads one line per call. When the end of the file is reached, it returns an empty string (`""`).

```python
lines_read = 0

try:
    with open("message.txt", "r", encoding="utf-8") as f:
        while True:
            text = f.readline()

            if text == "":
                break

            print(text.strip())
            lines_read += 1

    print(f"Total lines read: {lines_read}")

except FileNotFoundError:
    print("File not found.")
except OSError as ex:
    print("Could not read the file:", ex)
```

**Important:**
- `readline()` includes the line-ending character when one is present.
- `strip()` removes leading and trailing whitespace, including newline characters.
- Checking `text == ""` detects the end of the file. A blank line in a file normally contains a newline (`"\n"`), so it is not the same as the end-of-file result.

#### Alternative: Use `end=""`

Instead of stripping whitespace, preserve the original line content and avoid an extra newline when printing:

```python
with open("message.txt", "r", encoding="utf-8") as f:
    while True:
        text = f.readline()

        if text == "":
            break

        print(text, end="")
```

### D. Read All Lines into a List with `readlines()`

`readlines()` reads all remaining lines and returns a **list of strings**. Each string usually retains its line-ending character.

```python
try:
    with open("message.txt", "r", encoding="utf-8") as f:
        my_list = f.readlines()

    for line in my_list:
        print(line.strip())

    print(f"Total lines read: {len(my_list)}")

except FileNotFoundError:
    print("File not found.")
except OSError as ex:
    print("Could not read the file:", ex)
```

For example, if `message.txt` contains:

```text
Hello
Python
World
```

Then `readlines()` returns a list similar to:

```python
["Hello\n", "Python\n", "World\n"]
```

**Use it when:** You specifically need a list of all lines. Remember that reading all lines at once can use a lot of memory for large files.

---

## 3. Case Study: Extract Integers from a File

### Problem Statement

Suppose `data.txt` contains a mixture of words and numbers:

```text
10
hello
25
Python
-5
3.14
100
```

Write a program that:

1. Opens and reads the file.
2. Converts valid integer strings into integers.
3. Skips values that are not valid integers.
4. Stores valid integers in a list.
5. Calculates and displays their sum and average.
6. Handles errors such as missing files and files with no valid integers.

### Solution

```python
def read_and_process_numbers(file_name):
    numbers = []

    try:
        with open(file_name, "r", encoding="utf-8") as f:
            lines = f.readlines()

        if not lines:
            raise ValueError("The file is empty.")

        for value in lines:
            cleaned_value = value.strip()

            try:
                number = int(cleaned_value)
                numbers.append(number)

            except ValueError:
                print(f"Skipping non-integer value: {cleaned_value}")

        if not numbers:
            raise ValueError("No valid integer values found.")

        print("\n--- Valid Integers Extracted ---")
        for number in numbers:
            print(number)

        total_sum = sum(numbers)
        average = total_sum / len(numbers)

        print(f"\nNumbers: {numbers}")
        print(f"Sum: {total_sum}")
        print(f"Average: {average:.2f}")

    except FileNotFoundError as ex:
        print("File not found:", ex)
    except ValueError as ex:
        print("Value error:", ex)
    except OSError as ex:
        print("File or operating-system error:", ex)


read_and_process_numbers("data.txt")
```

### Sample Output

For the sample file above, the output will be similar to:

```text
Skipping non-integer value: hello
Skipping non-integer value: Python
Skipping non-integer value: 3.14

--- Valid Integers Extracted ---
10
25
-5
100

Numbers: [10, 25, -5, 100]
Sum: 130
Average: 32.50
```

### Explanation

**Step 1: Read the file**

```python
with open(file_name, "r", encoding="utf-8") as f:
    lines = f.readlines()
```

Reads the file into a list of lines. The `with` statement closes the file automatically.

**Step 2: Remove surrounding whitespace**

```python
cleaned_value = value.strip()
```

Removes leading and trailing whitespace, including newline characters.

**Step 3: Convert the string to an integer**

```python
number = int(cleaned_value)
```

- `"25"` becomes the integer `25`.
- `"-5"` becomes the integer `-5`.
- `"hello"` raises `ValueError`.
- `"3.14"` raises `ValueError` because it is not an integer string.

**Step 4: Skip invalid values**

```python
try:
    number = int(cleaned_value)
    numbers.append(number)
except ValueError:
    print(f"Skipping non-integer value: {cleaned_value}")
```

The inner `try`/`except` handles conversion errors for individual lines, allowing the program to continue processing later lines.

**Step 5: Calculate the sum and average**

```python
total_sum = sum(numbers)
average = total_sum / len(numbers)
```

The program checks that `numbers` is not empty before dividing, preventing division by zero.

**Exception-handling note:** An empty file is detected with `if not lines`. A file containing only words is handled by the later `if not numbers` check. The broad `except Exception` is intentionally omitted because specific exceptions make errors easier to understand and debug.

---

## 4. Method Summary

| Method / Function | Purpose | Return value |
|---|---|---|
| `f.read()` | Reads all remaining content | String |
| `f.readline()` | Reads one line | String |
| `f.readlines()` | Reads all remaining lines | List of strings |
| `f.close()` | Closes the file | `None` |
| `locals()` | Returns the current local namespace dictionary | Dictionary |
| `globals()` | Returns the global namespace dictionary | Dictionary |
| `str.strip()` | Removes surrounding whitespace | String |
| `int(value)` | Converts a valid integer string | Integer |
| `sum(numbers)` | Adds numeric values | Number |
| `len(numbers)` | Counts items | Integer |

### `read()`, `readline()`, and `readlines()` at a Glance

| Feature | `read()` | `readline()` | `readlines()` |
|---|---|---|---|
| Reads | Entire remaining content | One line per call | All remaining lines |
| Returns | String | String | List of strings |
| Typical use | Process complete text | Process sequentially | Work with a list of lines |
| Memory use | Can be high for large files | Low per call | Can be high for large files |

---

## 5. Best Practices

- Prefer `with open(...) as f` because Python closes the file automatically.
- If using `try`/`finally` manually, initialize the file variable to `None` and check `if f is not None` before closing it.
- Use a specific exception such as `FileNotFoundError`, `ValueError`, or `OSError` when appropriate.
- Use `encoding="utf-8"` for predictable text-file encoding.
- Use `"r"` to read, `"w"` to overwrite or create, and `"a"` to append to a file.
- Use `strip()` when you want to remove surrounding whitespace; avoid it when that whitespace is meaningful.
- Check that a list contains values before calculating an average.
- Avoid catching every exception with `except Exception` unless you have a clear reason to do so.
- For very large files, consider iterating directly over the file instead of loading every line into memory.

---

## Quick Revision

1. Why can `f.close()` raise `NameError`?  
   Because the file variable may never have been assigned if opening the file failed.

2. Why initialize `f = None`?  
   It gives the variable a known value before the file-opening operation.

3. Which method returns a list of lines?  
   `readlines()`.

4. What does `readline()` return at end-of-file?  
   An empty string (`""`).

5. What does `strip()` do?  
   Removes leading and trailing whitespace, including newline characters.

6. Why use an inner `try`/`except ValueError` in the case study?  
   To skip invalid integer strings without stopping the processing of the remaining lines.

7. What is the recommended way to manage file resources?  
   Use `with open(...) as f` whenever possible.

---

**End of Lecture 39 — Advanced File Handling, Resource Management & Exception Handling**
