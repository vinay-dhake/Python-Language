# 🐍 Python — String Methods

> **Topic:** String Methods  
> **Lecture:** String Methods  
> **Language:** Python

---

## 📚 Table of Contents

1. [Introduction to String Methods](#-introduction-to-string-methods)
2. [Categories of String Methods](#-categories-of-string-methods)
3. [String Conversion Methods](#-string-conversion-methods)
   - [`capitalize()`](#1-capitalize)
   - [`lower()`](#2-lower)
   - [`upper()`](#3-upper)
   - [`swapcase()`](#4-swapcase)
   - [`title()`](#5-title)
   - [`islower()`](#6-islower)
   - [`isupper()`](#7-isupper)
   - [`istitle()`](#8-istitle)
   - [`isalpha()`](#9-isalpha)
   - [`isdigit()`](#10-isdigit)
   - [`isalnum()`](#11-isalnum)
   - [`isspace()`](#12-isspace)
4. [String Comparison Methods](#-string-comparison-methods)
   - [`startswith()`](#1-startswith)
   - [`endswith()`](#2-endswith)
5. [String Searching Methods](#-string-searching-methods)
   - [`index()`](#1-index)
   - [`find()`](#2-find)
   - [`count()`](#3-count)
6. [String Replacement Methods](#-string-replacement-methods)
   - [`replace()`](#1-replace)
   - [`strip()`](#2-strip)
   - [`split()`](#3-split)
   - [`join()`](#4-join)
7. [Practice Exercise](#-practice-exercise)
8. [Quick Revision](#-quick-revision)

---

# 🔹 Introduction to String Methods

A Python **string object** has a number of methods, also called **member functions**.

These methods allow us to perform different operations on strings.

According to the lecture, string methods can be grouped into different categories depending on the type of operation they perform.

---

# 🔹 Categories of String Methods

The lecture divides string methods into the following categories:

1. **String Conversion Methods**
2. **String Comparison Methods**
3. **String Searching Methods**
4. **String Replacement Methods**

### Overview

| Category | Purpose | Examples |
|---|---|---|
| Conversion | Change or test the form/case/content of a string | `capitalize()`, `lower()`, `upper()`, `title()` |
| Comparison | Check the beginning or ending of a string | `startswith()`, `endswith()` |
| Searching | Search for substrings or count occurrences | `index()`, `find()`, `count()` |
| Replacement | Replace, split, join, or remove surrounding characters | `replace()`, `strip()`, `split()`, `join()` |

---

# 🟦 1. STRING CONVERSION METHODS

String conversion methods are used to convert a string into another form or check characteristics of the string.

---

## 1. `capitalize()`

### Definition

The `capitalize()` method returns a copy of the string with:

- The **first character** capitalized.
- All remaining characters converted to **lowercase**.

### Syntax

```python
string.capitalize()
```

### Example 1

```python
name = "guido van rossum"

newname = name.capitalize()

print(f"Original name is {name}")
print(f"Capitalized name is {newname}")
```

### Output

```text
Original name is guido van rossum
Capitalized name is Guido van rossum
```

### Important Point

`capitalize()` does **not** capitalize the first letter of every word.

For example:

```python
name = "sachin kapoor"

print(name.capitalize())
```

Output:

```text
Sachin kapoor
```

It does **not** produce:

```text
Sachin Kapoor
```

For capitalizing every word, `title()` is used.

---

## Example 2

```python
name = "Guido Van Rossum"

newname = name.capitalize()

print(f"Original name is {name}")
print(f"Capitalized name is {newname}")
```

The original string remains unchanged.

This is because string methods return a new string rather than modifying the original string.

---

## Example 3

```python
text = "python is awesome. java rocks"

newtext = text.capitalize()

print(f"Original text is {text}")
print(f"Capitalized text is {newtext}")
```

Output conceptually:

```text
Original text is python is awesome. java rocks
Capitalized text is Python is awesome. java rocks
```

### Observation

Only the first character of the complete string is capitalized.

---

# 2. `lower()`

### Definition

The `lower()` method returns a copy of the string with all alphabetic characters converted to lowercase.

### Syntax

```python
string.lower()
```

### Example

```python
name = "Sachin Kapoor"

lc = name.lower()

print(f"Original name is {name}")
print(f"Lower name is {lc}")
```

Output:

```text
Original name is Sachin Kapoor
Lower name is sachin kapoor
```

---

# 3. `upper()`

### Definition

The `upper()` method returns a copy of the string with all alphabetic characters converted to uppercase.

### Syntax

```python
string.upper()
```

### Example

```python
name = "Sachin Kapoor"

uc = name.upper()

print(f"Original name is {name}")
print(f"Upper name is {uc}")
```

Output:

```text
Original name is Sachin Kapoor
Upper name is SACHIN KAPOOR
```

---

## `lower()` vs `upper()`

```python
name = "Sachin Kapoor"

print(name.lower())
print(name.upper())
```

Output:

```text
sachin kapoor
SACHIN KAPOOR
```

---

# 4. `swapcase()`

### Definition

The `swapcase()` method returns a copy of the string with the case of every character swapped.

That means:

```text
lowercase → UPPERCASE
UPPERCASE → lowercase
```

### Syntax

```python
string.swapcase()
```

### Example

```python
name = "Sachin Kapoor"

newname = name.swapcase()

print(f"Original name is {name}")
print(f"Swapped name is {newname}")
```

Output:

```text
Original name is Sachin Kapoor
Swapped name is sACHIN kAPOOR
```

### Example

```python
text = "PyThOn"

print(text.swapcase())
```

Output:

```text
pYtHoN
```

---

# 5. `title()`

### Definition

The `title()` method returns a copy of the string converted into **title case** or **proper case**.

In title case:

- The beginning of each word is converted to uppercase.
- The remaining letters are converted to lowercase.

### Syntax

```python
string.title()
```

### Example

```python
text = "we got independence in 1947"

newtext = text.title()

print(f"Original text is {text}")
print(f"Title text is {newtext}")
```

Output:

```text
Original text is we got independence in 1947
Title text is We Got Independence In 1947
```

---

## More `title()` Examples

### Example 1

```python
text = "i lOVe pYTHoN"

print(text.title())
```

Output:

```text
I Love Python
```

---

### Example 2

```python
text = "physics,chemistry,maths"

print(text.title())
```

Output:

```text
Physics,Chemistry,Maths
```

---

### Example 3

```python
text = "physics_chemistry_maths"

print(text.title())
```

Output:

```text
Physics_Chemistry_Maths
```

---

### Example 4

```python
text = "physics1chemistry2maths"

print(text.title())
```

Output:

```text
Physics1Chemistry2Maths
```

---

### Example 5

```python
text = "He's an engineer, isn't he?"

print(text.title())
```

The example demonstrates how `title()` handles words containing punctuation and apostrophes.

---

# 6. `islower()`

### Definition

The `islower()` method returns:

- `True` if all alphabets in the string are lowercase.
- `False` otherwise.

### Syntax

```python
string.islower()
```

### Example

```python
s = "this is good"
print(s.islower())

s = "th!s is a1so g00d"
print(s.islower())

s = "this is Not good"
print(s.islower())
```

Output:

```text
True
True
False
```

### Important Observation

Characters that are **not alphabets**, such as:

- numbers
- spaces
- punctuation

do not prevent `islower()` from returning `True`, as long as the alphabetic characters present are lowercase.

---

# 7. `isupper()`

### Definition

The `isupper()` method returns:

- `True` if all alphabets in the string are uppercase.
- `False` otherwise.

### Syntax

```python
string.isupper()
```

### Example

```python
s = "THIS IS GOOD!"
print(s.isupper())

s = "THIS IS ALSO G00D!"
print(s.isupper())

s = "THIS IS not GOOD!"
print(s.isupper())
```

Output:

```text
True
True
False
```

---

# 8. `istitle()`

### Definition

The `istitle()` method returns `True` if the string is in title case.

Otherwise, it returns `False`.

### Syntax

```python
string.istitle()
```

### Examples

```python
s = "Python Is Good."
print(s.istitle())

s = "Python is good"
print(s.istitle())

s = "This Is @ Symbol."
print(s.istitle())

s = "99 Is A Number"
print(s.istitle())

s = "PYTHON"
print(s.istitle())
```

Output from the lecture:

```text
True
True
True
False
False
```

### Important Observation

`istitle()` checks whether the alphabetic words follow title-case rules.

---

# 9. `isalpha()`

### Definition

The `isalpha()` method returns `True` if the string contains **only alphabets**.

Otherwise, it returns `False`.

For an empty string, it also returns `False`.

### Syntax

```python
string.isalpha()
```

### Example

```python
name = "Monalisa"
print(name.isalpha())

name = "M0nalisa"
print(name.isalpha())

name = "Monalisa Shah"
print(name.isalpha())
```

### Output shown in the lecture

```text
False
False
True
```

> **Note:** The PDF's displayed output appears inconsistent with the stated definition for `"Monalisa"` and `"Monalisa Shah"` because spaces are normally not alphabetic characters. For your GitHub notes, retain the lecture example but verify the result by running the code in your Python environment.

---

# 10. `isdigit()`

### Definition

The `isdigit()` method returns `True` if the string contains only digits.

Otherwise, it returns `False`.

### Syntax

```python
string.isdigit()
```

### Examples

```python
text = "12345"
print(text.isdigit())

text = "012345"
print(text.isdigit())

text = "12345 6"
print(text.isdigit())

text = "a12345"
print(text.isdigit())
```

Output:

```text
True
True
False
False
```

### Why?

```text
"12345"   → only digits → True
"012345"  → only digits → True
"12345 6" → contains space → False
"a12345"  → contains alphabet → False
```

---

# 11. `isalnum()`

### Definition

The `isalnum()` method returns `True` if the string contains only **alphanumeric characters**.

Alphanumeric means:

```text
A-Z
a-z
0-9
```

Otherwise, it returns `False`.

### Syntax

```python
string.isalnum()
```

### Examples

```python
name = "M234onalisa"
print(name.isalnum())

name = "M3ona Shah "
print(name.isalnum())

name = "Mo3nalisaSha22ah"
print(name.isalnum())

name = "133"
print(name.isalnum())
```

The lecture displays:

```text
True
True
True
False
```

> **Note:** The displayed PDF output appears inconsistent with Python's actual `isalnum()` behavior for `"M3ona Shah "` and `"133"`. The important concept stated by the lecture is that spaces and other non-alphanumeric characters cause `isalnum()` to return `False`.

---

# 12. `isspace()`

### Definition

The `isspace()` method returns `True` if the string contains only whitespace characters.

Otherwise, it returns `False`.

An empty string returns `False`.

---

## What is Whitespace?

Whitespace includes:

### Space

```text
" "
```

### Tab

```text
\t
```

### Newline

```text
\n
```

### Carriage Return

```text
\r
```

---

## Examples

```python
s = ' \t'
print(s.isspace())

s = ' a '
print(s.isspace())

s = ' '
print(s.isspace())

s = ''
print(s.isspace())
```

Output:

```text
True
False
True
False
```

### Explanation

```text
" \t" → only whitespace → True
" a " → contains 'a' → False
" "   → only whitespace → True
""    → empty string → False
```

---

# 🟩 2. STRING COMPARISON METHODS

The lecture introduces two important string comparison methods:

1. `startswith()`
2. `endswith()`

These methods return Boolean values:

```python
True
```

or

```python
False
```

---

# 1. `startswith()`

### Definition

The `startswith()` method checks whether a string starts with a specified prefix.

It returns:

```text
True
```

if the string starts with the specified prefix.

Otherwise:

```text
False
```

### Syntax

```python
string.startswith(prefix)
```

It can take a maximum of three parameters:

```python
string.startswith(prefix, start, end)
```

### Parameters

#### `prefix`

The string with which the comparison is performed.

#### `start` — optional

The position from where checking begins.

#### `end` — optional

The position up to which checking is performed.

---

## Example

```python
text = "Python is easy to learn."

result = text.startswith('is easy')
print(result)

result = text.startswith('Python is ')
print(result)

result = text.startswith('Python is easy to learn.')
print(result)

result = text.startswith('is easy', 7)
print(result)
```

Output:

```text
False
True
True
True
```

### Explanation

The string is:

```text
Python is easy to learn.
```

The first test:

```python
text.startswith('is easy')
```

returns `False` because the complete string starts with:

```text
Python
```

The last example:

```python
text.startswith('is easy', 7)
```

starts checking from index `7`, where `"is easy"` begins.

---

# 2. `endswith()`

### Definition

The `endswith()` method checks whether a string ends with a specified suffix.

It returns:

```text
True
```

if the string ends with the specified suffix.

Otherwise:

```text
False
```

### Syntax

```python
string.endswith(suffix)
```

It can take up to three parameters:

```python
string.endswith(suffix, start, end)
```

### Parameters

#### `suffix`

The string to be checked.

#### `start` — optional

Beginning position where the suffix is checked.

#### `end` — optional

Ending position where the suffix is checked.

---

## Example

```python
text = "Python is easy to learn."

result = text.endswith('to learn')
print(result)

result = text.endswith('to learn.')
print(result)

result = text.endswith('learn.', 7)
print(result)

result = text.endswith('is', 7, 13)
print(result)
```

Output:

```text
False
True
True
False
```

### Important

Notice the difference:

```python
'to learn'
```

does not include the final period.

While:

```python
'to learn.'
```

includes the period.

Therefore:

```python
text.endswith('to learn')
```

returns:

```text
False
```

while:

```python
text.endswith('to learn.')
```

returns:

```text
True
```

---

## More `endswith()` Examples

```python
text = "Python is easy to learn."

result = text.endswith('easy', 7, 13)
print(result)

result = text.endswith('easy', 7, 14)
print(result)
```

Output:

```text
False
True
```

This example demonstrates the importance of the `start` and `end` positions.

---

# 🟨 3. STRING SEARCHING METHODS

The lecture covers three major searching methods:

1. `index()`
2. `find()`
3. `count()`

---

# 1. `index()`

### Definition

The `index()` method returns the index of the **first occurrence** of a substring inside a string.

If the substring is found:

```text
index is returned
```

If the substring is not found:

```text
an exception is raised
```

Specifically:

```text
ValueError
```

### Syntax

```python
string.index(sub)
```

or:

```python
string.index(sub, start, end)
```

### Parameters

#### `sub`

The substring to search for.

#### `start` — optional

Beginning position for the search.

#### `end` — optional

Ending position for the search.

---

## Example

```python
text = "Sunday is a fun day"

result = text.index('is a fun')
print(result)

result = text.index('day')
print(result)

result = text.index('day', 7)
print(result)

result = text.index('night')
print(result)
```

Output:

```text
7
3
16
ValueError
```

### Why?

The string:

```text
Sunday is a fun day
```

has:

```text
day
```

appearing more than once.

`index()` returns the index of the first matching occurrence unless a starting position changes the search.

---

# 2. `find()`

### Definition

The `find()` method returns the index of the first occurrence of a substring.

If the substring is not found, it returns:

```text
-1
```

This is the major difference between `find()` and `index()`.

### Syntax

```python
string.find(sub)
```

or:

```python
string.find(sub, start, end)
```

---

## Example

```python
text = "Sunday is a fun day"

result = text.find('is a fun')
print(result)

result = text.find('day')
print(result)

result = text.find('day', 7)
print(result)

result = text.find('night')
print(result)
```

Output:

```text
7
3
16
-1
```

---

# 🔥 `index()` vs `find()`

This is an important exam concept.

| Feature | `index()` | `find()` |
|---|---|---|
| Finds substring | Yes | Yes |
| Returns first occurrence | Yes | Yes |
| If substring exists | Returns index | Returns index |
| If substring does not exist | Raises `ValueError` | Returns `-1` |

### Example

```python
text = "Python"
```

Using `index()`:

```python
print(text.index("Java"))
```

Result:

```text
ValueError
```

Using `find()`:

```python
print(text.find("Java"))
```

Result:

```text
-1
```

---

# 3. `count()`

### Definition

The `count()` method returns the number of occurrences of a substring in a given string.

If the substring is not found, it returns:

```text
0
```

### Syntax

```python
string.count(sub)
```

or:

```python
string.count(sub, start, end)
```

### Parameters

- `sub` → substring to search
- `start` → optional starting position
- `end` → optional ending position

---

## Example

```python
text = "Python is awesome, isn't it?"

substring = "is"
count = text.count(substring)
print(count)

substring = "i"
count = text.count(substring, 8, 25)
print(count)

substring = "ton"
count = text.count(substring)
print(count)
```

Output:

```text
2
1
0
```

### Explanation

The substring:

```text
"is"
```

occurs twice in the given string.

The substring:

```text
"ton"
```

does not occur, so:

```text
0
```

is returned.

---

# 🟥 4. STRING REPLACEMENT METHODS

The lecture covers:

1. `replace()`
2. `strip()`
3. `split()`
4. `join()`

---

# 1. `replace()`

### Definition

The `replace()` method returns a copy of a string in which occurrences of an old substring are replaced by a new substring.

### Syntax

```python
string.replace(old, new)
```

or:

```python
string.replace(old, new, count)
```

### Parameters

#### `old`

The substring that we want to replace.

#### `new`

The substring that replaces the old substring.

#### `count` — optional

The number of times the replacement should be performed.

---

## Important Point

`replace()` does **not change the original string**.

It returns a new string.

If the old substring is not found, a copy of the original string is returned.

---

## Example

The lecture demonstrates replacing `"ue"` with `"ack"`.

```python
text = "Blue Blue Blue"

newtext = text.replace("ue", "ack")
print(newtext)
```

Result:

```text
Black Black Black
```

---

## Using `count`

```python
text = "Blue Blue Blue"

newtext = text.replace("ue", "ack", 2)
print(newtext)
```

Only two occurrences are replaced.

Result:

```text
Black Black Blue
```

---

## Substring Not Found

```python
text = "Blue Blue Blue"

newtext = text.replace("eu", "ack")
print(newtext)
```

Since `"eu"` does not occur in the string, the original content remains unchanged:

```text
Blue Blue Blue
```

---

# 2. `strip()`

### Definition

The `strip()` method returns a copy of the string with leading and trailing characters removed.

By default, it removes leading and trailing whitespace.

### Syntax

```python
string.strip()
```

It can also accept an optional character set:

```python
string.strip(chars)
```

### Parameter

#### `chars` — optional

A string specifying the set of characters to remove from the beginning and end.

If `chars` is not supplied, leading and trailing whitespace is removed.

---

## Example

```python
text = " Good Morning "

newtext = text.strip()

print("Original text:[" + text + "]")
print("New text:[" + newtext + "]")
```

Output:

```text
Original text:[ Good Morning ]
New text:[Good Morning]
```

### Important

`strip()` removes characters from the **beginning and end**.

It does not remove spaces between words.

For example:

```text
" Good Morning "
```

becomes:

```text
"Good Morning"
```

The space between:

```text
Good Morning
```

remains.

---

# 🟪 5. `split()`

### Definition

The `split()` method breaks a string at a specified separator and returns a **list of strings**.

### Syntax

```python
string.split()
```

or:

```python
string.split(separator)
```

or:

```python
string.split(separator, maxsplit)
```

---

## Parameters

### `separator` — optional

The delimiter at which the string should be split.

If no separator is specified, whitespace is used as the separator.

Whitespace includes characters such as:

- space
- newline
- tab

### `maxsplit` — optional

Specifies the maximum number of splits.

The default value is:

```text
-1
```

which means there is no limit on the number of splits.

---

# Example 1 — Default `split()`

```python
text = "Live and let live"

print(text.split())
```

Output:

```text
['Live', 'and', 'let', 'live']
```

The spaces are used as separators.

---

# Example 2 — Using a Separator

```python
grocery = "Milk, Butter, Bread"

print(grocery.split(', '))
```

Output:

```text
['Milk', 'Butter', 'Bread']
```

Here:

```python
', '
```

is the separator.

---

# Example 3 — Separator Not Present

```python
grocery = "Milk, Butter, Bread"

print(grocery.split(':'))
```

Since `:` is not present in the string, the complete string remains as one list element.

Output:

```text
['Milk, Butter, Bread']
```

---

# 🟧 6. `join()`

### Definition

The `join()` method returns a string formed by concatenating the elements of an iterable.

The iterable should contain **only strings**.

### Syntax

```python
separator.join(iterable)
```

---

# Example 1

```python
mylist = ["C", "C++", "Java", "Python"]

s = "->"

print(s.join(mylist))
```

Output:

```text
C->C++->Java->Python
```

The separator:

```python
"->"
```

is placed between every element.

---

# Example 2

```python
letters = "PYTHON"

letters_spaced = " ".join(letters)

print(letters_spaced)
```

Output:

```text
P Y T H O N
```

### Explanation

A string is itself an iterable.

Therefore:

```python
"PYTHON"
```

is processed character by character:

```text
P
Y
T
H
O
N
```

The space separator is inserted between each character.

---

# 🔥 `split()` vs `join()`

These methods are commonly used together.

### `split()`

Converts a string into a list:

```python
text = "Python Java C++"

words = text.split()

print(words)
```

Output:

```text
['Python', 'Java', 'C++']
```

### `join()`

Converts an iterable of strings into a single string:

```python
words = ["Python", "Java", "C++"]

text = " -> ".join(words)

print(text)
```

Output:

```text
Python -> Java -> C++
```

---

# 📝 Practice Exercise — User Registration System

The lecture provides a programming exercise to simulate a **user registration process**.

The program should perform the following tasks.

---

## Requirement 1 — Accept Full Name

First, ask the user to enter their full name.

If the user does not enter a valid full name:

- Display an error message.
- Ask again for the full name.
- Repeat until a valid full name is entered.

### Definition of Full Name

According to the exercise:

> A full name means a string containing at least **2 words separated by a space**.

---

## Requirement 2 — Accept Password

After obtaining the full name, ask the user to enter a password.

The password must:

1. Contain at least **8 characters**.
2. Contain at least **1 digit**.
3. Contain at least **1 uppercase letter**.

If the password is invalid:

- Ask the user again.
- Continue until the user enters a valid password.

---

## Requirement 3 — Display First Name

Finally:

1. Extract the user's first name.
2. Display a `THANK YOU` message.

---

## Required Functions

The lecture asks for separate functions for:

```python
get_full_name()
```

```python
get_password()
```

```python
get_first_name(fullname)
```

The basic structure shown in the lecture is:

```python
def get_full_name():
    pass


def get_password():
    pass


def get_first_name(fullname):
    pass


fullname = get_full_name()

pwd = get_password()

firstname = get_first_name(fullname)

print("Hello", firstname, "\nThank you for joining us!")
```

### Important String Methods Used in This Exercise

This exercise can make use of concepts such as:

```python
split()
```

```python
isdigit()
```

```python
isupper()
```

```python
len()
```

and string indexing.

---

# 🧠 Important String Methods — One-Page Revision

| Method | Purpose |
|---|---|
| `capitalize()` | First character uppercase, remaining characters lowercase |
| `lower()` | Converts letters to lowercase |
| `upper()` | Converts letters to uppercase |
| `swapcase()` | Swaps uppercase and lowercase |
| `title()` | Converts words to title case |
| `islower()` | Checks whether alphabetic characters are lowercase |
| `isupper()` | Checks whether alphabetic characters are uppercase |
| `istitle()` | Checks whether string is title case |
| `isalpha()` | Checks whether string contains only alphabets |
| `isdigit()` | Checks whether string contains only digits |
| `isalnum()` | Checks whether string contains only alphanumeric characters |
| `isspace()` | Checks whether string contains only whitespace |
| `startswith()` | Checks whether string begins with specified prefix |
| `endswith()` | Checks whether string ends with specified suffix |
| `index()` | Returns first index; raises `ValueError` if not found |
| `find()` | Returns first index; returns `-1` if not found |
| `count()` | Counts occurrences of substring |
| `replace()` | Replaces occurrences of substring |
| `strip()` | Removes leading/trailing characters |
| `split()` | Splits string into a list |
| `join()` | Joins iterable elements into a string |

---

# ⭐ Important Differences for Exams

## `capitalize()` vs `title()`

### `capitalize()`

```python
"hello world".capitalize()
```

Result:

```text
Hello world
```

### `title()`

```python
"hello world".title()
```

Result:

```text
Hello World
```

---

## `index()` vs `find()`

### `index()`

If substring is not found:

```text
ValueError
```

### `find()`

If substring is not found:

```text
-1
```

---

## `split()` vs `join()`

### `split()`

```text
String → List
```

### `join()`

```text
Iterable/List of strings → String
```

---

## `lower()` vs `upper()`

```text
lower() → lowercase
upper() → uppercase
```

---

## `startswith()` vs `endswith()`

```text
startswith() → checks beginning
endswith()   → checks ending
```

---

# 📌 Important Concept: String Methods Return a Copy

Many string methods do not modify the original string.

For example:

```python
name = "sachin"

newname = name.capitalize()

print(name)
print(newname)
```

Output:

```text
sachin
Sachin
```

The original:

```python
name
```

remains unchanged.

This is related to the fact that Python strings are immutable.

---

# 🎯 Final Revision

The four major groups covered in the lecture are:

```text
                    STRING METHODS
                          |
        +-----------------+-----------------+
        |                 |                 |
   CONVERSION         COMPARISON        SEARCHING
        |                 |                 |
 capitalize()       startswith()        index()
 lower()            endswith()          find()
 upper()                                count()
 swapcase()
 title()
 islower()
 isupper()
 istitle()
 isalpha()
 isdigit()
 isalnum()
 isspace()

                          |
                     REPLACEMENT
                          |
                    replace()
                    strip()
                    split()
                    join()
```

---

# ✅ Key Takeaways

1. Python provides many built-in methods for string manipulation.
2. String methods are grouped according to their purpose.
3. `capitalize()` affects only the first character of the complete string.
4. `title()` capitalizes the beginning of words.
5. `lower()` converts letters to lowercase.
6. `upper()` converts letters to uppercase.
7. `swapcase()` reverses character case.
8. `isalpha()`, `isdigit()`, `isalnum()`, and `isspace()` are useful for validation.
9. `startswith()` checks the beginning of a string.
10. `endswith()` checks the ending of a string.
11. `index()` raises an exception when the substring is absent.
12. `find()` returns `-1` when the substring is absent.
13. `count()` counts substring occurrences.
14. `replace()` creates a modified copy of the string.
15. `strip()` removes leading and trailing characters.
16. `split()` converts a string into a list.
17. `join()` combines strings into a single string.
18. String methods generally return a new string rather than modifying the original string.

---

# 📚 End of String Methods Notes


# 🐍 Python — Introduction to Dictionary

> **Topic:** Dictionary - I  
> **Lecture:** Introduction to Dictionary  
> **Language:** Python

---

## 📚 Table of Contents

1. [Today's Agenda](#-todays-agenda)
2. [What Is a Dictionary?](#-what-is-a-dictionary)
3. [What Is a Key-Value Pair?](#-what-is-a-key-value-pair)
4. [Creating a Dictionary](#-creating-a-dictionary)
5. [General Syntax](#-general-syntax-of-creating-a-dictionary)
6. [Dictionary Examples](#-dictionary-examples)
7. [Important Characteristics](#-important-characteristics-of-dictionaries)
8. [Other Ways of Creating a Dictionary](#-other-ways-of-creating-a-dictionary)
9. [Printing a Dictionary](#-printing-a-dictionary)
10. [Accessing Individual Elements](#-accessing-individual-elements)
11. [`[]` vs `get()`](#-difference-between--and-get)
12. [Traversing a Dictionary](#-traversing-a-dictionary)
13. [Iterating Only on Keys](#-iterating-only-on-keys)
14. [Getting Values Using Keys](#-getting-values-using-keys)
15. [Performance Issue](#-performance-issue)
16. [`items()` Method](#-items-method)
17. [Iterating Over Values](#-iterating-only-on-values)
18. [Important Point — Dictionary Ordering](#-important-point--dictionary-ordering)
19. [Python 3.6 and Python 3.7](#-python-36-and-python-37)
20. [Quick Revision](#-quick-revision)

---

# 📌 Today's Agenda

The lecture covers:

- Dictionary-I
- What is a Dictionary?
- What is a Key-Value Pair?
- Creating a Dictionary
- Important Characteristics of a Dictionary
- Different Ways to Access a Dictionary
- An Important Point about Dictionary Ordering

---

# 🔹 What Is a Dictionary?

A **Python dictionary** is a collection used to store data in the form of:

```text
key : value
```

A dictionary associates one piece of information with another.

For example:

```text
Roll Number → Student Name
```

or:

```text
Customer Name → Mobile Number
```

---

## 🔹 Dictionary vs List / Tuple / String

The lecture compares dictionaries with the collections studied previously.

### List, Tuple and String

These are:

- Ordered collections.
- Capable of storing multiple elements.
- Elements are accessed using their positions/indexes.

For example:

```python
mylist = ["Amit", "Brajesh", "Chetan"]
```

An element can be accessed using its index:

```python
mylist[0]
```

---

### Dictionary

A dictionary stores data as:

```text
key : value
```

Instead of accessing a value through an index, we use its corresponding **key**.

For example:

```python
student_data = {
    1: "Amit",
    2: "Brajesh",
    3: "Chetan"
}
```

Here:

```text
1 → Amit
2 → Brajesh
3 → Chetan
```

The number is the **key**, while the student's name is the **value**.

---

# 🔹 What Is a Key-Value Pair?

Sometimes we need to store data in such a way that **one piece of information is connected to another piece of information**.

Examples:

```text
Roll Number → Student Name
```

```text
Customer Name → Mobile Number
```

In:

```text
RollNo → Student Name
```

the:

```text
RollNo
```

is called the **key**.

The associated:

```text
Student Name
```

is called the **value**.

Therefore:

```text
Key → Value
```

is called a **key-value pair**.

Python provides the **dictionary** data type to store such paired data.

---

# 🔹 Creating a Dictionary

Creating a dictionary is done using **curly braces**:

```python
{ }
```

Dictionary elements are separated using commas.

Each element is represented as:

```python
key: value
```

---

## 🔹 Important Rules for Dictionary Keys and Values

### Values

Values:

- Can be of any data type.
- Can be repeated.

For example:

```python
{
    1: "Amit",
    2: "Amit"
}
```

Both keys have the same value.

That is allowed.

---

### Keys

Keys:

- Must be of an immutable type.
- Must be unique.

Examples of commonly used immutable key types include:

```text
int
str
tuple
```

A dictionary cannot have duplicate keys as separate entries.

---

# 🔹 General Syntax of Creating a Dictionary

The general syntax is:

```python
d = {
    <key>: <value>,
    <key>: <value>,
    ...
    <key>: <value>
}
```

For example:

```python
student_data = {
    1: "Amit",
    2: "Brajesh",
    3: "Chetan"
}
```

Here:

```text
1 → Amit
2 → Brajesh
3 → Chetan
```

---

# 🔹 Dictionary Examples

## Example 1 — Empty Dictionary

An empty dictionary can be created using:

```python
my_dict = {}
```

Here:

```python
my_dict
```

contains no key-value pairs.

---

## Example 2 — Dictionary with Integer Keys

```python
my_dict = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan'
}
```

Here:

| Key | Value |
|---:|---|
| `1` | `'Amit'` |
| `2` | `'Brajesh'` |
| `3` | `'Chetan'` |

---

## Example 3 — Dictionary with Mixed Keys

A dictionary can contain keys of different immutable types.

```python
my_dict = {
    1: 'John',
    'a': 'vowel'
}
```

Here:

```text
1 → John
a → vowel
```

The keys are of different types:

```python
1
```

is an integer, while:

```python
'a'
```

is a string.

---

## Example 4 — Dictionary with Lists as Values

Values can themselves be lists.

```python
my_dict = {
    'Rahul': ['C', 'C++'],
    'Ajay': ['Java', 'C', 'Python'],
    'Neeraj': ['Oracle', 'Python']
}
```

The dictionary associates a person's name with a list of programming languages.

Conceptually:

```text
Rahul  → C, C++
Ajay   → Java, C, Python
Neeraj → Oracle, Python
```

Notice that the **values are lists**.

---

# 🔹 Important Characteristics of Dictionaries

The lecture identifies the following characteristics of Python dictionaries:

1. They can be **nested**.
2. They are **mutable**.
3. They are **dynamic**.
4. They are described in the lecture as **unordered**.
5. Dictionary items are accessed using their **corresponding keys**, not indexes.

---

## 1. Dictionaries Can Be Nested

A dictionary can contain another dictionary as a value.

Conceptually:

```python
my_dict = {
    "student": {
        "name": "Amit",
        "roll": 1
    }
}
```

This is called a **nested dictionary**.

---

## 2. Dictionaries Are Mutable

Mutable means that dictionary contents can be changed after the dictionary has been created.

For example, values can be changed.

```python
student = {
    1: "Amit"
}

student[1] = "Rahul"
```

Now the value associated with key `1` is:

```text
Rahul
```

---

## 3. Dictionaries Are Dynamic

A dictionary can grow or shrink during program execution.

New key-value pairs can be added and existing entries can be removed.

---

## 4. Dictionary Items Are Accessed Using Keys

Unlike a list:

```python
mylist[0]
```

we do not normally use an index to access dictionary data.

Instead, we use the key:

```python
my_dict[key]
```

For example:

```python
student_data = {
    1: "Amit",
    2: "Brajesh",
    3: "Chetan"
}

print(student_data[2])
```

The key:

```python
2
```

is used to obtain:

```text
Brajesh
```

---

# 🔹 Other Ways of Creating a Dictionary

Python also provides the built-in:

```python
dict()
```

function for creating dictionaries.

---

## Example 1 — Empty Dictionary Using `dict()`

```python
my_dict = dict()
```

This creates an empty dictionary.

It is equivalent to:

```python
my_dict = {}
```

---

## Example 2 — Using `dict()` with a Dictionary

```python
my_dict = dict({
    1: 'apple',
    2: 'ball'
})
```

The result is a dictionary containing:

```text
1 → apple
2 → ball
```

---

## Example 3 — Using Another Sequence

A dictionary can also be created from a sequence of key-value pairs.

```python
my_dict = dict([
    (1, 'apple'),
    (2, 'ball')
])
```

Here:

```python
(1, 'apple')
```

represents one key-value pair.

Similarly:

```python
(2, 'ball')
```

represents another key-value pair.

The resulting dictionary is:

```python
{
    1: 'apple',
    2: 'ball'
}
```

---

# 🔹 Printing a Dictionary

The lecture presents four ways to work with or print dictionary data:

1. Directly pass the dictionary to `print()`.
2. Access individual values using keys and the subscript operator `[]`.
3. Access individual values using `get()`.
4. Traverse the dictionary using loops.

---

# 1. Printing the Entire Dictionary

Consider:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print(student_data)
```

The dictionary itself can be passed directly to:

```python
print()
```

The output contains the dictionary's key-value pairs.

---

# 🔹 Accessing Individual Elements

Keys are used to retrieve their corresponding values.

Python provides two important ways to access a dictionary value using a key:

### Method 1

Subscript operator:

```python
[]
```

### Method 2

Dictionary method:

```python
get()
```

---

# 🔹 Accessing Using `[]`

Consider:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print(student_data[3])
```

Here:

```python
3
```

is the key.

Therefore, Python returns its associated value:

```text
Chetan
```

---

# 🔹 Accessing Using `get()`

The same value can be obtained using:

```python
student_data.get(3)
```

Example:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print(student_data.get(3))
```

Output:

```text
Chetan
```

---

# 🔥 Difference Between `[]` and `get()`

This is one of the most important concepts in the lecture.

Both:

```python
student_data[key]
```

and:

```python
student_data.get(key)
```

can be used to access a dictionary value.

However, they behave differently when the key **does not exist**.

---

## Case 1 — Using `[]`

Suppose:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}
```

Now try:

```python
print(student_data[6])
```

There is no key:

```python
6
```

Therefore, the subscript operator raises:

```text
KeyError
```

---

## Case 2 — Using `get()`

Now try:

```python
print(student_data.get(6))
```

The key does not exist.

Instead of raising a `KeyError`, `get()` returns:

```python
None
```

---

# 🔥 Example from the Lecture

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print("Name of student with roll no 6:", student_data.get(6))

print("Name of student with roll no 6:", student_data[6])
```

The first statement returns:

```text
None
```

because key `6` does not exist.

The second statement raises:

```text
KeyError
```

because key `6` is missing.

---

# 📊 `[]` vs `get()`

| Feature | `dict[key]` | `dict.get(key)` |
|---|---|---|
| Used to access value | ✅ | ✅ |
| Existing key | Returns value | Returns value |
| Missing key | Raises `KeyError` | Returns `None` |
| Exception generated for missing key | Yes | No |

### Easy way to remember

```text
[] + missing key → KeyError
get() + missing key → None
```

---

# 🔄 Traversing a Dictionary

**Traversing** means visiting the elements of a dictionary one by one.

Python allows three ways to traverse a dictionary:

1. Iterate only over **keys**.
2. Iterate over **keys and values**.
3. Iterate only over **values**.

---

# 🟦 1. Iterate Only on Keys

When:

```python
for ... in
```

is used directly on a dictionary, the loop iterates over the dictionary's **keys by default**.

It does not directly iterate over the values or key-value pairs.

---

## Example

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

for roll in student_data:
    print("Roll:", roll)
```

Here:

```python
roll
```

receives each key.

Conceptually:

```text
1
2
3
4
5
```

Therefore the loop prints the roll numbers.

---

# 🔹 Why Does the Loop Give Keys?

When Python sees:

```python
for roll in student_data:
```

it interprets the dictionary as an iterable of its keys.

So:

```python
for roll in student_data:
```

is effectively traversing the keys.

---

# 🟦 Another Way to Iterate Only on Keys

Python provides:

```python
keys()
```

The `keys()` method provides the dictionary's keys in an iterable form.

---

## Example

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

for roll in student_data.keys():
    print("Roll:", roll)
```

The loop explicitly tells Python:

> Iterate over the dictionary's keys.

---

# 🔹 `keys()` Method

Conceptually:

```python
student_data.keys()
```

provides the dictionary's keys.

These keys can then be traversed using a `for` loop.

Example:

```python
for roll in student_data.keys():
    print(roll)
```

---

# 🟨 Getting Values Using Keys

Once we have a key, we can obtain its associated value.

For example:

```python
student_data[roll]
```

or:

```python
student_data.get(roll)
```

can be used.

---

## Example from the Lecture

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

for roll in student_data:
    print("Roll:", roll, "Name:", student_data[roll])
```

### How it works

During each iteration:

```python
roll
```

contains a key.

Then:

```python
student_data[roll]
```

retrieves the corresponding value.

Conceptually:

```text
roll = 1 → Amit
roll = 2 → Brajesh
roll = 3 → Chetan
roll = 4 → Deepak
roll = 5 → Neeraj
```

---

# ⚠️ Performance Issue

The above solution works correctly, but the lecture points out a performance issue.

Consider:

```python
for roll in student_data:
    print("Roll:", roll, "Name:", student_data[roll])
```

The process is:

```text
1. Get a key
       ↓
2. Search for its associated value
       ↓
3. Print the key and value
       ↓
4. Repeat
```

The program is repeatedly accessing the dictionary to obtain the value corresponding to each key.

The lecture describes this as an inefficient solution.

---

# 💡 Much Better Solution — `items()`

Python provides the:

```python
items()
```

method.

The `items()` method returns a `dict_items` object containing the dictionary's:

```text
(key, value)
```

pairs.

Each key-value pair is represented as a tuple.

---

# 🔹 `items()` Method

Consider:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}
```

Calling:

```python
student_data.items()
```

provides the dictionary's key-value pairs.

Conceptually:

```text
(1, 'Amit')
(2, 'Brajesh')
(3, 'Chetan')
(4, 'Deepak')
(5, 'Neeraj')
```

---

# 🔹 Syntax of Using `items()`

The lecture gives the general syntax:

```python
for <var1, var2> in <dict_var>.items():
    # var1 will hold key
    # var2 will hold value
```

For example:

```python
for roll, name in student_data.items():
    print("Roll:", roll, "Name:", name)
```

---

# 🔍 How `items()` Works

Python automatically assigns:

```text
First variable → key
Second variable → value
```

So:

```python
for roll, name in student_data.items():
```

means:

```text
roll → key
name → corresponding value
```

For example:

```text
roll = 1
name = Amit
```

then:

```text
roll = 2
name = Brajesh
```

and so on.

---

# 🔹 Example from the Lecture

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

for roll, name in student_data.items():
    print("Roll:", roll, "Name:", name)
```

This directly provides both the key and its corresponding value.

---

# ⭐ Why `items()` Is Better

Compare the two approaches.

### Approach 1

```python
for roll in student_data:
    print("Roll:", roll, "Name:", student_data[roll])
```

Here:

```text
Get key
   ↓
Access dictionary again
   ↓
Get value
```

### Approach 2

```python
for roll, name in student_data.items():
    print("Roll:", roll, "Name:", name)
```

Here:

```text
Get key + value together
```

Therefore, `items()` provides a cleaner and more direct approach when both keys and values are required.

---

# 🟩 2. Iterate Only on Values

Sometimes we don't need the keys.

We only need the values.

Python provides:

```python
values()
```

for this purpose.

---

# 🔹 `values()` Method

The `values()` method provides the dictionary's values in an iterable form.

---

## Example

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

for name in student_data.values():
    print("Name:", name)
```

Here:

```python
name
```

receives only the values.

Conceptually:

```text
Amit
Brajesh
Chetan
Deepak
Neeraj
```

The keys are not used.

---

# 📊 Dictionary Traversal Methods

| Requirement | Method / Syntax |
|---|---|
| Iterate over keys | `for key in dictionary:` |
| Iterate over keys explicitly | `for key in dictionary.keys():` |
| Iterate over keys and values | `for key, value in dictionary.items():` |
| Iterate over values | `for value in dictionary.values():` |

---

# 🔥 Complete Traversal Example

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}
```

### Only Keys

```python
for roll in student_data:
    print("Roll:", roll)
```

---

### Only Keys Using `keys()`

```python
for roll in student_data.keys():
    print("Roll:", roll)
```

---

### Keys + Values

```python
for roll, name in student_data.items():
    print("Roll:", roll, "Name:", name)
```

---

### Only Values

```python
for name in student_data.values():
    print("Name:", name)
```

---

# ⚠️ Very Important Point — Dictionary Ordering

The lecture discusses an important point regarding the term:

```text
unordered
```

The lecture initially describes a Python dictionary as an **unordered collection**.

The term "unordered" traditionally meant that:

> The order in which elements are inserted into a dictionary and the order in which they are retrieved might be different.

---

# 🔹 Example of the Meaning of "Unordered"

Suppose elements are inserted as:

```text
1 → Amit
2 → Brajesh
3 → Chetan
4 → Deepak
5 → Neeraj
```

Historically, one could not rely on the retrieval order being the same as the insertion order.

Therefore, dictionaries were traditionally described as:

```text
unordered
```

---

# 🔹 But What Do We Observe in Modern Python?

Consider:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print(student_data)
```

The output appears in the same order in which the data was inserted.

For example:

```text
{
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}
```

This raises an important question:

> Why does the dictionary appear to preserve insertion order?

---

# 🧠 Python 3.6 and Python 3.7

The lecture explains the evolution of dictionary ordering.

---

## Python 3.6

As of Python **3.6**, the **CPython implementation** of Python dictionaries remembers the order in which items were inserted.

However, this was considered an:

```text
implementation detail
```

rather than a language guarantee.

---

## Python 3.7

As of Python **3.7**, insertion ordering became a:

```text
language feature
```

This means dictionary insertion order became part of the Python language specification.

---

# 🔹 `OrderedDict`

The lecture also explains that in Python 3.6, if insertion ordering needed to be guaranteed across different Python implementations, one could use:

```python
OrderedDict
```

The important historical distinction is:

```text
Python 3.6
→ CPython dictionaries preserve insertion order as an implementation detail.

Python 3.7+
→ Insertion ordering is a language feature.
```

---

# 📌 Historical Understanding

The terminology can therefore be understood as follows:

```text
Older Python
     ↓
Dictionary described as unordered
     ↓
Python 3.6
     ↓
CPython preserves insertion order
(as implementation detail)
     ↓
Python 3.7
     ↓
Insertion order becomes a language feature
```

---

# 📊 Dictionary — Complete Concept Summary

| Concept | Explanation |
|---|---|
| Dictionary | Collection of key-value pairs |
| Key | Identifies/accesses a value |
| Value | Data associated with a key |
| Keys | Must be unique and immutable |
| Values | Can be of any data type and can repeat |
| `{}` | Creates an empty dictionary |
| `dict()` | Built-in function for creating dictionaries |
| `[]` | Access value using key |
| `get()` | Access value safely |
| `keys()` | Provides dictionary keys |
| `values()` | Provides dictionary values |
| `items()` | Provides key-value pairs |
| Mutable | Dictionary contents can be changed |
| Dynamic | Dictionary can grow/shrink |
| Nested | Dictionary can contain dictionaries |
| Insertion order | Guaranteed as a language feature from Python 3.7 |

---

# 🔥 Most Important Examples

## Example 1 — Creating a Dictionary

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan'
}
```

---

## Example 2 — Accessing a Value

```python
print(student_data[2])
```

Output:

```text
Brajesh
```

---

## Example 3 — Using `get()`

```python
print(student_data.get(2))
```

Output:

```text
Brajesh
```

---

## Example 4 — Missing Key

```python
print(student_data.get(6))
```

Output:

```text
None
```

But:

```python
print(student_data[6])
```

raises:

```text
KeyError
```

---

## Example 5 — Iterate Keys

```python
for roll in student_data:
    print(roll)
```

---

## Example 6 — Iterate Keys Using `keys()`

```python
for roll in student_data.keys():
    print(roll)
```

---

## Example 7 — Iterate Keys and Values

```python
for roll, name in student_data.items():
    print(roll, name)
```

---

## Example 8 — Iterate Values

```python
for name in student_data.values():
    print(name)
```

---

# 🧠 Easy Way to Remember Dictionary Methods

Think of a dictionary as:

```text
KEY ─────────→ VALUE
```

Then:

```python
dictionary.keys()
```

means:

```text
Give me the keys
```

```python
dictionary.values()
```

means:

```text
Give me the values
```

```python
dictionary.items()
```

means:

```text
Give me KEY + VALUE together
```

---

# 🎯 Exam-Oriented Questions

## Q1. What is a dictionary?

A dictionary is a Python collection that stores data as **key-value pairs**.

---

## Q2. What is a key-value pair?

A key-value pair associates one piece of information, called the **key**, with another piece of information, called the **value**.

Example:

```python
1: "Amit"
```

Here:

```text
1 → key
Amit → value
```

---

## Q3. What are the characteristics of dictionaries?

According to the lecture:

- Dictionaries can be nested.
- Dictionaries are mutable.
- Dictionaries are dynamic.
- They were traditionally described as unordered.
- Dictionary values are accessed using keys rather than indexes.

---

## Q4. What is the difference between `[]` and `get()`?

```text
dict[key]
```

raises `KeyError` when the key does not exist.

```text
dict.get(key)
```

returns `None` when the key does not exist.

---

## Q5. What does `keys()` do?

It provides the keys of a dictionary in an iterable form.

Example:

```python
for key in student_data.keys():
    print(key)
```

---

## Q6. What does `values()` do?

It provides the values of a dictionary in an iterable form.

Example:

```python
for value in student_data.values():
    print(value)
```

---

## Q7. What does `items()` do?

It provides dictionary key-value pairs.

Example:

```python
for key, value in student_data.items():
    print(key, value)
```

---

## Q8. Why is `items()` useful?

When both the key and value are required, `items()` provides them together.

Instead of:

```python
for roll in student_data:
    print(roll, student_data[roll])
```

we can use:

```python
for roll, name in student_data.items():
    print(roll, name)
```

---

# ⭐ Quick Revision

### Create Empty Dictionary

```python
my_dict = {}
```

or:

```python
my_dict = dict()
```

---

### Create Dictionary

```python
my_dict = {
    1: "Amit",
    2: "Brajesh"
}
```

---

### Access Value

```python
my_dict[1]
```

---

### Safe Access

```python
my_dict.get(1)
```

---

### Get Keys

```python
my_dict.keys()
```

---

### Get Values

```python
my_dict.values()
```

---

### Get Key-Value Pairs

```python
my_dict.items()
```

---

### Traverse Keys

```python
for key in my_dict:
    print(key)
```

---

### Traverse Keys + Values

```python
for key, value in my_dict.items():
    print(key, value)
```

---

### Traverse Values

```python
for value in my_dict.values():
    print(value)
```

---

# 🏆 Final Memory Trick

Remember:

```text
             DICTIONARY
                 |
          KEY : VALUE
          /      |      \
       keys()  items()  values()
          |       |        |
        Keys   Both      Values
```

And remember the most important access difference:

```text
dictionary[key]
       ↓
Missing key
       ↓
KeyError
```

while:

```text
dictionary.get(key)
       ↓
Missing key
       ↓
None
```

---

# 📚 End of Dictionary Notes
