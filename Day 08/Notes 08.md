# 📘 Python Lecture 8 - More on Strings

> These notes are based on my learning journey in Python. This chapter covers advanced string operations such as concatenation, slicing, useful string methods, string comparison, and type conversion.

---

# 📚 Topics Covered

* String Concatenation
* String Slicing
* Step Value in Slicing
* Useful String Methods
* Comparing Strings
* Type Conversion

---

# 🔗 String Concatenation

## What is String Concatenation?

**Concatenation** means joining two or more strings together.

In Python, the `+` operator joins strings.

> **Note:**
>
> * For numbers, `+` performs **addition**.
> * For strings, `+` performs **concatenation** (joining).

---

## Syntax

```python
string1 + string2
```

---

## Example 1

```python
s1 = "Good"
s2 = "Morning"

s3 = s1 + s2

print(s3)
```

### Output

```
GoodMorning
```

---

## Example 2

```python
s1 = "Good"
s2 = "Morning"

s3 = s1 + " " + s2

print(s3)
```

### Output

```
Good Morning
```

---

## More Examples

### Joining Three Strings

```python
first = "Python"
second = "is"
third = "Awesome"

print(first + " " + second + " " + third)
```

Output

```
Python is Awesome
```

---

### Concatenating Empty String

```python
print("Hello" + "")
```

Output

```
Hello
```

---

### Using Variables

```python
name = "Vinay"

print("Hello " + name)
```

Output

```
Hello Vinay
```

---

## ❌ Common Mistake

```python
age = 20

print("Age = " + age)
```

Output

```
TypeError
```

### ✔ Correct Way

```python
age = 20

print("Age = " + str(age))
```

Output

```
Age = 20
```

---

# ✂️ String Slicing

## What is Slicing?

Slicing is the process of extracting a portion (substring) from a string.

Example:

```
Industry
```

Extract

```
dust
```

using slicing.

---

## Syntax

```python
string[start:end]
```

* `start` → Starting index (inclusive)
* `end` → Ending index (exclusive)

Python stops at **end - 1**.

---

## Example

```python
s = "Industry"

print(s[2:6])
```

Output

```
dust
```

Explanation

```
Index

I n d u s t r y
0 1 2 3 4 5 6 7

2 -> d
3 -> u
4 -> s
5 -> t

Stops before index 6
```

---

## Example

```python
s = "Welcome"

print(s[3:6])
```

Output

```
com
```

---

## Example

```python
s = "Mumbai"

print(s[0:3])
```

Output

```
Mum
```

---

## Example

```python
s = "Mumbai"

print(s[0:10])
```

Output

```
Mumbai
```

Python safely stops at the end of the string even if the ending index is larger than the string length.

---

## Example

```python
s = "Python"

print(s[2:2])
```

Output

```
```

Because the starting index and ending index are the same, nothing is extracted.

---

## Example

```python
s = "Python"

print(s[6:10])
```

Output

```
```

Index `6` is already at the end of the string.

---

## Omitting the Start Index

```python
s = "welcome"

print(s[:3])
```

Output

```
wel
```

Equivalent to

```python
print(s[0:3])
```

---

## Omitting the End Index

```python
s = "welcome"

print(s[1:])
```

Output

```
elcome
```

Equivalent to

```python
print(s[1:len(s)])
```

---

## Copy Entire String

```python
s = "welcome"

print(s[:])
```

Output

```
welcome
```

---

## Invalid Syntax

```python
print(s[])
```

Output

```
SyntaxError
```

---

# 🔄 Negative Indexing

Python also supports negative indices.

```
welcome

-7 -6 -5 -4 -3 -2 -1
 w  e  l  c  o  m  e
```

---

## Example

```python
s = "welcome"

print(s[-4:-1])
```

Output

```
com
```

---

## Example

```python
s = "welcome"

print(s[-1:-4])
```

Output

```
```

Because slicing moves from left to right by default, the start index must be smaller than the end index.

---

# 📌 Key Points

* Strings are immutable.
* Slicing never modifies the original string.
* Ending index is excluded.
* Out-of-range ending indices are safe.
* Empty slices return an empty string.
* Negative indices count from the end.

---

# 📖 Summary

| Concept                  | Example                | Output                         |
| ------------------------ | ---------------------- | ------------------------------ |
| Concatenation            | `"Hi" + "There"`       | `HiThere`                      |
| Concatenation with Space | `"Hi" + " " + "There"` | `Hi There`                     |
| Slice                    | `"Python"[1:4]`        | `yth`                          |
| Entire String            | `s[:]`                 | Copy of string                 |
| From Start               | `s[:5]`                | First five characters          |
| Till End                 | `s[3:]`                | Characters from index 3 onward |
| Negative Slice           | `s[-4:-1]`             | Last few characters            |

---

# 🎯 What I Learned

* How to join multiple strings using the `+` operator.
* Difference between numeric addition and string concatenation.
* How Python slicing works.
* Why the ending index is excluded.
* How to use omitted indices.
* How negative indexing makes extracting characters from the end easier.
* Common slicing mistakes and how to avoid them.
