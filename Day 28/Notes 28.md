# 📚 Python – Tuples Continued & Strings

This lecture covers the continuation of **Tuples** and an introduction to **Strings in Python**. It explains tuple methods and operations, string creation, indexing, traversal, slicing, and string operators.

---

## 📌 1. Tuple Methods

Tuples are **immutable**, which means their elements cannot be changed after the tuple is created.

Because of this, tuples do not provide methods that modify their contents, such as:

* `append()`
* `insert()`
* `remove()`
* `pop()`
* `sort()`
* `reverse()`

Tuples mainly provide two important methods:

1. `index()`
2. `count()`

### 🔹 `index()` Method

The `index()` method returns the **first index** at which a specified element occurs in a tuple.

### Syntax

```python
tuple_name.index(value)
```

### Example

```python
primes = (2, 3, 5, 7, 11)

print(primes.index(5))
```

**Output:**

```text
2
```

Here, `5` is present at index `2`.

If the element does not exist, Python raises a `ValueError`.

```python
primes = (2, 3, 5, 7, 11)

print(primes.index(60))
```

**Output:**

```text
ValueError
```

---

### 🔹 `count()` Method

The `count()` method returns the number of times a particular element occurs in a tuple.

### Syntax

```python
tuple_name.count(value)
```

### Example

```python
t = ('i', 'n', 'd', 'i', 'a')

print(t.count('i'))
```

**Output:**

```text
2
```

The character `'i'` occurs **two times** in the tuple.

If the element is not present, `count()` returns `0`.

```python
print(t.count('z'))
```

**Output:**

```text
0
```

> **Remember:** `index()` gives the position, while `count()` gives the number of occurrences.

---

## 📌 2. Operations on Tuples

Tuples support several standard operations.

### 🔹 Membership Operators

The membership operators are:

* `in`
* `not in`

They are used to check whether an element exists in a tuple.

```python
my_tuple = ('A', 'B', 'C', 'D')

print('A' in my_tuple)
print('G' not in my_tuple)
```

**Output:**

```text
True
True
```

* `in` → checks whether an element is present.
* `not in` → checks whether an element is absent.

---

### 🔹 Tuple Concatenation (`+`)

The `+` operator is used to join two tuples.

```python
odd = (1, 3, 5)
even = (2, 4, 6)

print(odd + even)
```

**Output:**

```text
(1, 3, 5, 2, 4, 6)
```

The original tuples are not modified. A **new tuple** is created.

Tuples can also contain different types of data:

```python
numbers = (1, 2, 3)
words = ('one', 'two')

print(numbers + words)
```

**Output:**

```text
(1, 2, 3, 'one', 'two')
```

> **Important:** A tuple can only be concatenated with another tuple.

---

### 🔹 Tuple Repetition (`*`)

The `*` operator can be used to repeat a tuple.

```python
t = (10, 20, 30)

print(t * 3)
```

**Output:**

```text
(10, 20, 30, 10, 20, 30, 10, 20, 30)
```

The repetition value must be an **integer**.

```python
(1, 2) * 3
```

is valid, but:

```python
(1, 2) * 3.0
```

causes an error because `3.0` is a float.

---

## 📌 3. Introduction to Strings

A **string** is a sequence of **zero or more characters**.

Strings are **immutable data structures**. This means that we can access the characters inside a string, but we cannot directly change the contents of the existing string.

Examples of strings:

```python
"Hello"
"Python"
"12345"
"Hello World"
"@#$%"
""
```

An empty string is also a valid string:

```python
s = ""
```

---

## 📌 4. Creating a String

Python provides **three ways** to create a string:

1. Using single quotes
2. Using double quotes
3. Using triple quotes

The PDF introduces these three methods on page 4.

### 🔹 Using Single Quotes

```python
my_string = 'Hello'

print(my_string)
```

**Output:**

```text
Hello
```

### 🔹 Using Double Quotes

```python
my_string = "Hello"

print(my_string)
```

**Output:**

```text
Hello
```

### 🔹 Using Triple Quotes

Triple quotes can be written using either:

```python
'''Hello'''
```

or:

```python
"""Hello"""
```

They are generally used for **multiline strings**.

### Example from the PDF

```python
my_string = '''Hello'''

print(my_string)
```

**Output:**

```text
Hello
```

### Multiline String Example

```python
my_string = """Hello, welcome to
the world of Python"""

print(my_string)
```

**Output:**

```text
Hello, welcome to
the world of Python
```

These examples are shown on page 5 of the PDF.

---

## 📌 5. Accessing Strings

Python provides three ways to access a string:

1. **Print the complete string**
2. **Access individual characters using indexing**
3. **Access multiple characters using slicing**

The PDF introduces these three approaches on page 6.

---

## 📌 6. Printing the Whole String

A complete string can be directly passed to the `print()` function.

### Example

```python
city = "Bhopal"

print(city)
```

**Output:**

```text
Bhopal
```

This example is given on page 7 of the PDF.

---

## 📌 7. Accessing Individual Characters

Every character in a string has an **index**.

Consider:

```python
city = "Bhopal"
```

The string contains 6 characters.

### Forward Indexing

```text
Character:   B    h    o    p    a    l
Index:       0    1    2    3    4    5
```

### Backward Indexing

```text
Character:   B    h    o    p    a    l
Index:      -6   -5   -4   -3   -2   -1
```

Therefore:

* First character → `city[0]`
* Second character → `city[1]`
* Last character → `city[-1]`
* Second-last character → `city[-2]`

The indexing diagram is shown on page 9 of the PDF.

---

## 📌 8. String Indexing Example

```python
city = "Bhopal"

print(city[0])
print(city[1])
print(city[-1])
print(city[-2])
```

**Output:**

```text
B
h
l
a
```

This example is given on page 10 of the PDF.

### Explanation

```text
city[0]  → B
city[1]  → h
city[-1] → l
city[-2] → a
```

---

## 📌 9. Index Out of Range

Consider:

```python
city = "Bhopal"

print(city[6])
```

The valid positive indexes are:

```text
0  1  2  3  4  5
```

There is no index `6`.

Therefore Python raises:

```text
IndexError: String index out of range
```

This example is given on page 11 of the PDF.

> **Remember:** For a string of length `n`, positive indexes range from `0` to `n - 1`.

---

## 📌 10. String Index Must Be an Integer

Consider:

```python
city = "Bhopal"

print(city[1.5])
```

This produces:

```text
TypeError: String indices must be integers
```

The example is shown on page 12 of the PDF.

String indexes must be integers.

Valid:

```python
city[0]
city[1]
city[-1]
```

Invalid:

```python
city[1.5]
```

---

## 📌 11. Accessing String Elements Using a `while` Loop

A string can be traversed using a `while` loop.

### Example

```python
city = "Bhopal"

i = 0

while i < len(city):
    print(city[i])
    i = i + 1
```

**Output:**

```text
B
h
o
p
a
l
```

This example is given on page 13 of the PDF.

### How It Works

`len(city)` returns:

```text
6
```

Therefore the loop runs while:

```python
i < 6
```

The values of `i` are:

```text
0
1
2
3
4
5
```

So Python accesses:

```python
city[0]
city[1]
city[2]
city[3]
city[4]
city[5]
```

The `len()` function works with strings and returns the number of characters in the string.

---

## 📌 12. Accessing String Elements Using a `for` Loop

Since a string is a **sequence type**, a `for` loop can directly iterate through its characters.

### Example

```python
city = "Bhopal"

for ch in city:
    print(ch)
```

**Output:**

```text
B
h
o
p
a
l
```

This example is given on page 14 of the PDF.

### `while` vs `for`

Using `while`:

```python
i = 0

while i < len(city):
    print(city[i])
    i = i + 1
```

Using `for`:

```python
for ch in city:
    print(ch)
```

The `for` loop is simpler when we only need each character.

---

## 📌 13. Reverse Traversal of a String

The PDF contains an exercise asking us to traverse a string in reverse order using only a `for` loop and **without using the slice operator**.

### Solution

```python
city = "Bhopal"

for i in range(len(city) - 1, -1, -1):
    print(city[i])
```

**Output:**

```text
l
a
p
o
h
B
```

The solution is given on page 16.

### Understanding the `range()`

Since:

```python
len(city)
```

is `6`, the range becomes:

```python
range(5, -1, -1)
```

which generates:

```text
5, 4, 3, 2, 1, 0
```

Therefore the characters are accessed from the last character to the first.

---

## 📌 14. String Slicing

Just like lists and tuples, strings also support the **slice operator**.

### Syntax

```python
string[start:end]
```

* `start` → starting index
* `end` → ending index
* The `end` index is **not included**

This is explained on page 17 of the PDF.

For example:

```python
city = "Bhopal"
```

```text
Index:       0    1    2    3    4    5
Character:   B    h    o    p    a    l
```

---

## 📌 15. Slicing Examples

### Example 1

```python
city = "Bhopal"

print(city[1:4])
```

**Output:**

```text
hop
```

Indexes `1`, `2`, and `3` are included.

Index `4` is excluded.

---

### Example 2

```python
city = "Bhopal"

print(city[3:5])
```

**Output:**

```text
pa
```

Indexes `3` and `4` are included, while index `5` is excluded.

---

## 📌 16. Slicing from the Beginning

```python
city = "Bhopal"

print(city[0:4])
```

**Output:**

```text
Bhop
```

This takes characters from index `0` up to, but not including, index `4`.

---

### End Index Can Be Larger Than the String

```python
city = "Bhopal"

print(city[0:10])
```

**Output:**

```text
Bhopal
```

Even though `10` is beyond the length of the string, slicing simply returns the available characters.

---

## 📌 17. Omitting Start or End

### Omitting the Start

```python
city = "Bhopal"

print(city[:4])
```

**Output:**

```text
Bhop
```

`city[:4]` means:

```text
Start from the beginning
Stop before index 4
```

---

### Omitting the End

```python
city = "Bhopal"

print(city[1:])
```

**Output:**

```text
hopal
```

`city[1:]` means:

```text
Start from index 1
Continue until the end
```

These examples appear on page 20 of the PDF.

---

## 📌 18. Negative Index Slicing

Negative indexes can also be used while slicing.

```text
Character:   B    h    o    p    a    l
Index:      -6   -5   -4   -3   -2   -1
```

### Example

```python
city = "Bhopal"

print(city[:-2])
```

**Output:**

```text
Bhop
```

The slice starts from the beginning and stops before `-2`.

### Example

```python
city = "Bhopal"

print(city[-2:])
```

**Output:**

```text
al
```

This takes the last two characters.

---

## 📌 19. Step Value in String Slicing

The complete syntax of slicing is:

```python
string[start:end:step]
```

The third parameter is called the **step value**.

The step determines how many positions Python moves after retrieving a character.

The default step value is:

```text
1
```

This is explained on page 22 of the PDF.

---

### Positive Step

If the step is positive:

* Movement is **left to right**
* Default start is `0`
* Default end is `len(string)`

### Negative Step

If the step is negative:

* Movement is **right to left**
* It is used for backward/reverse traversal

---

## 📌 20. Step Value Example

```python
city = "Bhopal"

print(city[1:4:2])
```

**Output:**

```text
hp
```

Why?

```text
Index:       0    1    2    3    4    5
Character:   B    h    o    p    a    l
```

Start at index `1`:

```text
h
```

Move by `2`:

```text
1 → 3
```

So:

```text
1 → h
3 → p
```

Result:

```text
hp
```

---

## 📌 21. Step Value Cannot Be Zero

The step value cannot be `0`.

```python
city = "Bhopal"

print(city[1:4:0])
```

**Output:**

```text
ValueError: Slice step cannot be 0
```

### Remember

```text
Positive step → Forward
Negative step → Backward
Zero step     → ValueError
```

---

## 📌 22. Positive Step vs Negative Step

Consider:

```python
city = "Bhopal"
```

### Positive Step

```python
print(city[4:1:1])
```

Here, the starting index is `4`, but the step is positive.

Python tries to move forward:

```text
4 → 5 → ...
```

while the end is `1`.

Therefore, there are no characters to return and the result is an **empty string**.

### Negative Step

```python
print(city[4:1:-1])
```

**Output:**

```text
apo
```

Python moves backward:

```text
4 → 3 → 2
```

which gives:

```text
a → p → o
```

Therefore:

```text
apo
```

---

## 📌 23. Empty Start and End in Slicing

```python
city = "Bhopal"

print(city[::])
```

**Output:**

```text
Bhopal
```

When start, end, and step are omitted, the default values are used.

---

## 📌 24. Reversing a String Using Slicing

One of the most important string-slicing techniques is:

```python
city = "Bhopal"

print(city[::-1])
```

**Output:**

```text
lapohB
```

The `-1` step tells Python to move from right to left.

### ⭐ Remember This

```python
string[::-1]
```

is the standard slicing technique for reversing a string.

Example:

```python
word = "Python"

print(word[::-1])
```

**Output:**

```text
nohtyP
```

---

# 🧠 Quick Revision

### String

A string is a **sequence of zero or more characters** and is **immutable**.

### Creating Strings

```python
'Hello'
"Hello"
'''Hello'''
"""Hello"""
```

### Positive Indexing

```text
0 → first character
1 → second character
...
```

### Negative Indexing

```text
-1 → last character
-2 → second-last character
...
```

### Indexing

```python
s[index]
```

Returns one character.

### Slicing

```python
s[start:end]
```

Returns multiple characters.

### Full Slicing

```python
s[start:end:step]
```

### Reverse

```python
s[::-1]
```

### Traversing with `for`

```python
for ch in s:
    print(ch)
```

### Traversing Backwards

```python
for i in range(len(s) - 1, -1, -1):
    print(s[i])
```

### Important Errors

```text
Invalid index       → IndexError
Non-integer index   → TypeError
Step = 0            → ValueError
```

---

# 📚 Python – Tuples Continued & Strings

This lecture covers the continuation of **Tuples** and an introduction to **Strings in Python**. It explains tuple methods, tuple operations, string creation, indexing, slicing, operators, and string formatting.

---

## 📌 Tuple Methods

Tuples are **immutable**, which means their elements cannot be changed after the tuple is created.

Because tuples are immutable, they do not support methods that modify the tuple, such as:

- `append()`
- `insert()`
- `remove()`
- `pop()`
- `sort()`
- `reverse()`

Tuples mainly provide two methods:

1. `index()`
2. `count()`

### 🔹 `index()` Method

The `index()` method returns the **first index** of a specified element in a tuple.

### Example

```python
primes = (2, 3, 5, 7, 11)

print(primes.index(5))
