# Python Dictionaries — More on Dictionary
## Lecture 30: Updating and Removing Dictionary Data


> **Part 1:** Updating a Dictionary + Removing Data from a Dictionary

---

## Table of Contents

1. [Updating a Dictionary](#1-updating-a-dictionary)
   - [Using Assignment Operator](#11-using-assignment-operator)
   - [Example: Updating an Existing Key](#12-example-updating-an-existing-key)
   - [Example: Adding a New Key](#13-example-adding-a-new-key)
   - [Using `update()`](#14-using-update)
   - [Example: `update()` with Two Dictionaries](#15-example-update-with-two-dictionaries)
   - [Bank Account Exercise](#16-bank-account-exercise)
2. [Removing Data from a Dictionary](#2-removing-data-from-a-dictionary)
   - [`pop()`](#21-pop)
   - [Example: `pop()`](#22-example-pop)
   - [`del`](#23-del)
   - [Example: `del`](#24-example-del)
   - [`clear()`](#25-clear)
   - [Example: `clear()`](#26-example-clear)
3. [Quick Revision](#3-quick-revision)

---

# 1. Updating a Dictionary

A dictionary is **mutable**, so its contents can be changed after creation.

According to the lecture, there are two ways to add new items or change the value of an existing item:

1. **Assignment operator**
2. **`update()` method**

---

## 1.1 Using Assignment Operator

### Syntax

```python
dict_var[key] = value
```

### How it works

When we use the assignment operator:

- Python searches for the specified `key`.
- If the key **already exists**, its value is replaced.
- If the key **does not exist**, a new key-value pair is created.

### Basic idea

```text
Existing key    → value gets replaced
New key         → new key-value pair is created
```

---

## 1.2 Example: Updating an Existing Key

### Program

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print("Before updating:")
print(student_data)

student_data[2] = 'Brajendra'

print("After updating:")
print(student_data)
```

### Output

```text
Before updating:
{1: 'Amit', 2: 'Brajesh', 3: 'Chetan', 4: 'Deepak', 5: 'Neeraj'}

After updating:
{1: 'Amit', 2: 'Brajendra', 3: 'Chetan', 4: 'Deepak', 5: 'Neeraj'}
```

### What happened?

The key `2` was already present.

```python
student_data[2] = 'Brajendra'
```

Therefore:

```text
2 : 'Brajesh'
```

became:

```text
2 : 'Brajendra'
```

The key `2` was **not added again**.

---

## 1.3 Example: Adding a New Key

### Program

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

print("Before updating:")
print(student_data)

student_data[8] = 'Ankit'

print("After updating:")
print(student_data)
```

### Output

```text
Before updating:
{1: 'Amit', 2: 'Brajesh', 3: 'Chetan', 4: 'Deepak', 5: 'Neeraj'}

After updating:
{1: 'Amit', 2: 'Brajesh', 3: 'Chetan', 4: 'Deepak', 5: 'Neeraj', 8: 'Ankit'}
```

### Important

Key `8` did not previously exist, so Python creates a new key-value pair:

```python
8: 'Ankit'
```

---

# 1.4 Using `update()`

The `update()` method is used to merge the keys and values of one dictionary/iterable into another.

### Syntax

```python
dict_var.update(dict_var2)
```

### Main rule

If the same key exists in both dictionaries:

```text
value from dict_var2 replaces
the old value in dict_var
```

If the key does not exist:

```text
new key-value pair is added
```

---

## 1.5 Example: `update()` with Two Dictionaries

### Program

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}

student_data2 = {
    2: 'Brajendra',
    8: 'Ankit'
}

print("Before updating:")
print(student_data)

student_data.update(student_data2)

print("After updating:")
print(student_data)
```

### Output

```text
Before updating:
{1: 'Amit', 2: 'Brajesh', 3: 'Chetan', 4: 'Deepak', 5: 'Neeraj'}

After updating:
{1: 'Amit', 2: 'Brajendra', 3: 'Chetan', 4: 'Deepak', 5: 'Neeraj', 8: 'Ankit'}
```

### Understand the result

Before:

```python
student_data = {
    1: 'Amit',
    2: 'Brajesh',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj'
}
```

Second dictionary:

```python
student_data2 = {
    2: 'Brajendra',
    8: 'Ankit'
}
```

There are two cases:

| Key | Present in original? | Result |
|---|---|---|
| `2` | Yes | `'Brajesh'` becomes `'Brajendra'` |
| `8` | No | `8: 'Ankit'` is added |

So the final dictionary is:

```python
{
    1: 'Amit',
    2: 'Brajendra',
    3: 'Chetan',
    4: 'Deepak',
    5: 'Neeraj',
    8: 'Ankit'
}
```

---

# 1.6 Bank Account Exercise

## Problem

Create a dictionary named `accounts` containing account IDs and balances.

Initialize it with:

```text
101 → 50000
102 → 45000
103 → 55000
```

Then:

1. Ask the user for an account ID.
2. Ask the user for an amount.
3. If the account ID is already present:
   - update the balance by adding the amount.
4. Otherwise:
   - create a new account with the given amount as its balance.
5. Finally, print all account details.

---

## Sample Case 1 — Existing Account

Input:

```text
Enter account id: 101
Enter amount: 4000
```

The existing balance is:

```text
50000
```

New balance:

```text
50000 + 4000 = 54000
```

Sample output shown in the lecture:

```text
Current Accounts Present
{101: 50000, 102: 45000, 103: 55000}

Enter account id:101
Enter amount:4000
Account updated
Account Details:
{101: 54000, 102: 45000, 103: 55000}
```

---

## Sample Case 2 — New Account

Input:

```text
Enter account id: 104
Enter amount: 60000
```

Since `104` does not exist, a new entry is created.

Sample output shown in the lecture:

```text
Current Accounts Present
{101: 50000, 102: 45000, 103: 55000}

Enter account id:104
Enter amount:60000
New Account Created
Account Details:
{101: 50000, 102: 45000, 103: 55000, 104: 60000}
```

---

## Solution

```python
accounts = {
    101: 50000,
    102: 45000,
    103: 55000
}

print("Current Accounts Present")
print(accounts)

id = int(input("Enter account id:"))
amt = int(input("Enter amount:"))

balance = accounts.get(id)

if balance is None:
    accounts[id] = amt
    print("New Account Created")
else:
    newbalance = balance + amt
    accounts[id] = newbalance
    print("Account updated")

print("Account Details:")
print(accounts)
```

### Important idea: `get()` + `is None`

```python
balance = accounts.get(id)
```

The `get()` method is used to obtain the balance for the specified account ID.

Then:

```python
if balance is None:
```

checks whether no value was obtained.

If no existing account is found:

```python
accounts[id] = amt
```

creates a new account.

Otherwise:

```python
newbalance = balance + amt
accounts[id] = newbalance
```

updates the existing account.

---

# 2. Removing Data from a Dictionary

Since dictionaries are mutable, items can also be removed.

The lecture introduces three ways:

1. `pop(key)`
2. `del`
3. `clear()`

---

# 2.1 `pop()`

The `pop()` method removes the entry with the specified key and returns its value.

### Syntax

```python
dict_var.pop(key, [default])
```

`pop()` can take two parameters:

### 1. `key`

The key that should be searched for and removed.

### 2. `default` — optional

The value returned if the key is not present.

---

## Return behavior of `pop()`

### Case 1: Key exists

The key is removed and its value is returned.

```python
d = {'a': 10, 'b': 20}

x = d.pop('a')

print(x)
print(d)
```

Result:

```text
10
{'b': 20}
```

### Case 2: Key does not exist + default is provided

The default value is returned.

```python
d.pop('x', -1)
```

Result:

```text
-1
```

### Case 3: Key does not exist + default is not provided

Python raises:

```text
KeyError
```

---

# 2.2 Example: `pop()`

The lecture uses a dictionary containing the number of days in six months.

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    "May": 31,
    "Jun": 30
}

print(sixMonths)

print(sixMonths.pop("Jun"))

print(sixMonths)

print(sixMonths.pop("Jul", -1))

print(sixMonths.pop("Jul", "Not found"))

print(sixMonths.pop("Jul"))
```

### Output

```text
{'Jan': 31, 'Feb': 28, 'Mar': 31, 'Apr': 30, 'May': 31, 'Jun': 30}

30

{'Jan': 31, 'Feb': 28, 'Mar': 31, 'Apr': 30, 'May': 31}

-1

Not found

Traceback (most recent call last):
    ...
KeyError: 'Jul'
```

### Step-by-step

First:

```python
sixMonths.pop("Jun")
```

removes:

```python
"Jun": 30
```

and returns:

```text
30
```

Then:

```python
sixMonths.pop("Jul", -1)
```

Since `"Jul"` is not present, `-1` is returned.

Next:

```python
sixMonths.pop("Jul", "Not found")
```

again `"Jul"` is absent, so:

```text
Not found
```

is returned.

Finally:

```python
sixMonths.pop("Jul")
```

has no default value, so Python raises:

```text
KeyError: 'Jul'
```

---

# 2.3 `del`

`del` is a Python keyword/operator that can be used to remove an item from a dictionary.

### Syntax

```python
del dict_var[key]
```

It removes the entry whose key is supplied.

### If the key is not found

A `KeyError` is raised.

### `del` can also delete the entire dictionary object

```python
del dict_var
```

After this, the variable no longer refers to the dictionary.

---

# 2.4 Example: Deleting the Entire Dictionary

### Program

```python
threeMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31
}

print(threeMonths)

del threeMonths

print(threeMonths)
```

### Output

```text
{'Jan': 31, 'Feb': 28, 'Mar': 31}

Traceback (most recent call last):
    ...
NameError: name 'threeMonths' is not defined
```

### Why?

This statement:

```python
del threeMonths
```

deletes the dictionary variable itself.

Therefore, when Python reaches:

```python
print(threeMonths)
```

the name `threeMonths` is no longer defined.

---

# 2.5 `clear()`

The `clear()` method removes **all items** from a dictionary.

### Syntax

```python
dict_var.clear()
```

### Important points from the lecture

- `clear()` does not take an argument.
- It removes all items from the dictionary.
- The dictionary itself remains available.
- The dedicated `clear()` slide states that the method returns `None`.

---

# 2.6 Example: `clear()`

### Program

```python
threeMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31
}

print(threeMonths)

threeMonths.clear()

print(threeMonths)
```

### Output

```text
{'Jan': 31, 'Feb': 28, 'Mar': 31}
{}
```

### Difference between `del` and `clear()`

```python
del threeMonths
```

removes the variable/object reference entirely.

Whereas:

```python
threeMonths.clear()
```

removes all items but leaves:

```python
threeMonths
```

available as an empty dictionary.

---

# 3. Quick Revision

## Updating

### Assignment

```python
dict_var[key] = value
```

- Existing key → value is replaced.
- New key → new key-value pair is added.

### `update()`

```python
dict1.update(dict2)
```

- Merges data from `dict2` into `dict1`.
- Same key → value is overwritten.
- New key → added.

---

## Removing

| Method | What it does | Returns |
|---|---|---|
| `pop(key)` | Removes one key-value pair | Removed value |
| `pop(key, default)` | Removes pair; uses default if key is absent | Removed value or default |
| `del dict[key]` | Removes one pair | No returned value |
| `del dict` | Deletes the dictionary variable | No returned value |
| `clear()` | Removes all items | `None` |

---

## ⭐ Exam-Oriented Points

### 1. What happens if the key already exists?

```python
d[key] = value
```

The old value is replaced.

### 2. What happens if the key does not exist?

```python
d[key] = value
```

A new key-value pair is created.

### 3. What happens with `update()` and duplicate keys?

The value from the updating dictionary replaces the existing value.

### 4. What does `pop()` return?

The value associated with the removed key.

### 5. What happens if `pop()` cannot find the key?

- With a default → returns the default.
- Without a default → raises `KeyError`.

### 6. What does `del dictionary` do?

It deletes the dictionary variable.

### 7. What does `clear()` do?

It removes all entries and leaves an empty dictionary.

---

## 🧠 One-Line Memory Trick

```text
Assignment → Add / Replace
update()   → Merge
pop()      → Remove + Return Value
del        → Delete
clear()    → Empty Dictionary
```

---
==============================================================================================================================================================
# Python Dictionaries — Functions, `*args` and `**kwargs`
More on Dictionary — Part 2


> **Part 2:** Dictionary Functions + Variable-Length Arguments

---

## Table of Contents

1. [Functions Used With Dictionary](#1-functions-used-with-dictionary)
2. [`len()` Function](#2-len-function)
3. [`max()` Function](#3-max-function)
4. [Highest Score Exercise](#4-highest-score-exercise)
5. [Finding the Player With the Highest Score](#5-finding-the-player-with-the-highest-score)
6. [`min()` Function](#6-min-function)
7. [`any()` Function](#7-any-function)
8. [`all()` Function](#8-all-function)
9. [`sorted()` Function](#9-sorted-function)
10. [Variable-Length Arguments](#10-variable-length-arguments)
11. [`*args`](#11-args)
12. [`**kwargs`](#12-kwargs)
13. [`*args` vs `**kwargs`](#13-args-vs-kwargs)
14. [Quick Revision](#14-quick-revision)

---

# 1. Functions Used With Dictionary

Python allows several built-in functions to be used with dictionary objects.

The lecture covers:

```text
len()
max()
min()
any()
all()
sorted()
```

> **Important:** Several of these functions operate on the **keys** when a dictionary is passed directly.

The functions are introduced in Lecture 37 pages/slides 19–19. fileciteturn3file0L10-L20

---

# 2. `len()` Function

## Definition

`len()` returns the **number of items** in the dictionary.

Since every item consists of a key-value pair:

```text
len(dictionary)
```

returns the number of key-value pairs.

## Syntax

```python
len(dictionary)
```

## Example from the lecture

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    "May": 31,
    "Jun": 30
}

print(len(sixMonths))
```

## Output

```text
6
```

There are six key-value pairs in the dictionary. fileciteturn3file0L22-L29

---

# 3. `max()` Function

## Definition

When a dictionary is passed directly to `max()`, it returns the **greatest key** present in the dictionary.

```python
max(dictionary)
```

does **not** search for the greatest value.

### Remember

```text
max(dict)        → maximum key
max(dict.values()) → maximum value
```

---

## 3.1 Example: String Keys

### Program

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    "May": 31,
    "Jun": 30
}

print(max(sixMonths))
```

## Output

```text
May
```

The dictionary keys are compared, so the greatest key alphabetically is `"May"`. fileciteturn3file0L31-L37

---

## 3.2 Guess the Output — Mixed Key Types

### Program from the slide

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    3: 31,
    "Apr": 30,
    5: 31,
    6: 30
}

print(max(sixMonths))
```

### Result

This produces a **`TypeError`** because the dictionary contains keys of incompatible types:

```text
str
int
```

Python cannot directly compare strings and integers using the ordering required by `max()`.

The lecture presents this as a **Guess The Output** example. fileciteturn3file0L38-L42

---

## 3.3 Example: Integer Keys

### Program

```python
sixMonths = {
    1: 31,
    2: 28,
    3: 31,
    4: 30,
    5: 31,
    6: 30
}

print(max(sixMonths))
```

## Output

```text
6
```

The greatest key is `6`. fileciteturn3file0L43-L48

---

## 3.4 Example: Boolean Keys

### Program

```python
data = {
    False: 10,
    True: 5
}

print(max(data))
```

## Output

```text
True
```

In Python's Boolean ordering:

```text
False < True
```

Therefore, `True` is the maximum key in this example. fileciteturn3file0L49-L54

---

## 3.5 Guess the Output — `None` as a Key

### Program from the slide

```python
data = {
    False: 0,
    True: 1,
    None: 2
}

print(max(data))
```

### Result

This raises a **`TypeError`** because `None` cannot be ordered against the Boolean/integer key values in the way required by `max()`.

The slide presents this as another **Guess The Output** question. fileciteturn3file0L55-L59

---

# 4. Highest Score Exercise

## Problem

Write a program to:

1. Create a dictionary called `players`.
2. Accept the names of **5 players**.
3. Accept the runs scored by each player.
4. Find the **highest score**.

The lecture specifically uses the dictionary's **values** to find the highest score. fileciteturn3file0L60-L63

---

## Solution from the Lecture

```python
players = {}

i = 1

while i <= 5:
    name = input("Enter player name:")
    runs = int(input("Enter runs:"))

    players[name] = runs

    i = i + 1

print(players)

runs = max(players.values())

print("Highest runs are :", runs)
```

### Key concept

Suppose:

```python
players = {
    "A": 50,
    "B": 90,
    "C": 40
}
```

If we write:

```python
max(players)
```

Python searches the **keys**.

But we want the highest runs, so we use:

```python
max(players.values())
```

This searches the **values**.

The lecture solution uses exactly this approach. fileciteturn3file0L67-L77

---

# 5. Finding the Player With the Highest Score

## Problem

Modify the previous program so that it finds:

1. The highest score.
2. The **name of the player** who scored that highest score.

The lecture introduces this as a modification of the previous exercise. fileciteturn3file0L78-L81

---

## Solution from the Lecture

```python
players = {}

i = 1

while i <= 5:
    name = input("Enter player name:")
    runs = int(input("Enter runs:"))

    players[name] = runs

    i = i + 1

print(players)

max = 0
pl = ""

for name, runs in players.items():
    if runs > max:
        max = runs
        pl = name

print("Player with top score is", pl, "with score of", max)
```

### How the logic works

Initially:

```python
max = 0
pl = ""
```

Then the program goes through every key-value pair:

```python
for name, runs in players.items():
```

For each player:

```python
if runs > max:
```

If the current player's runs are greater than the previous maximum:

```python
max = runs
pl = name
```

So:

```text
max → highest runs found so far
pl  → name of player with that score
```

Finally:

```python
print("Player with top score is", pl, "with score of", max)
```

prints both the player name and score. fileciteturn3file0L85-L100

> **Note:** The lecture uses `max` as a variable name in this example. In normal Python programming, avoid using `max` as a variable because `max()` is also a built-in function.

---

# 6. `min()` Function

## Definition

When a dictionary is passed directly to `min()`, it returns the **least key** present in the dictionary.

## Syntax

```python
min(dictionary)
```

---

## Example from the Lecture

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    "May": 31,
    "Jun": 30
}

print(min(sixMonths))
```

## Output

```text
Apr
```

The dictionary keys are compared, and `"Apr"` is the least key alphabetically. fileciteturn3file0L101-L108

### Remember

```python
min(dict)           # minimum key
min(dict.values())  # minimum value
```

---

# 7. `any()` Function

## Definition

The `any()` function accepts a dictionary and checks the **keys**.

It returns:

```text
True  → if at least one key is truthy
False → if no key is truthy
```

For an empty dictionary:

```python
any({})
```

returns:

```text
False
```

The lecture explains `any()` in terms of whether at least one dictionary element/key is `True`. fileciteturn3file0L109-L117

---

## 7.1 Example

### Program

```python
data = {
    1: 31,
    2: 28,
    3: 30
}

print(any(data))
```

### Output

```text
True
```

Why?

The keys are:

```text
1, 2, 3
```

All three are truthy, so at least one key is truthy.

Therefore:

```text
True
```

---

## 7.2 Guess the Output

### Program

```python
data = {
    0: 1,
    False: 2,
    '': 3
}

print(any(data))
```

### Output

```text
False
```

The keys are falsy:

```text
0
False
''
```

Therefore, there is no truthy key.

> **Important:** `0` and `False` are considered equal as dictionary keys, so Python does not store them as two separate keys. The important point for `any()` is still that the stored keys here are falsy. fileciteturn3file0L118-L122

---

## 7.3 Guess the Output

### Program

```python
data = {
    '0': 1,
    False: 2,
    '': 3
}

print(any(data))
```

### Output

```text
True
```

Why?

The string:

```python
'0'
```

is **non-empty**, so it is truthy.

Therefore, at least one key is truthy.

```text
any(data) → True
```

The lecture uses this example to demonstrate the difference between:

```python
0
```

and:

```python
'0'
```

The integer `0` is falsy, while the non-empty string `'0'` is truthy. fileciteturn3file0L123-L127

---

## 7.4 Empty Dictionary

### Program

```python
data = {}

print(any(data))
```

### Output

```text
False
```

An empty dictionary contains no keys, so there is no truthy key. fileciteturn3file0L128-L132

---

# 8. `all()` Function

## Definition

The `all()` function accepts a dictionary and checks its **keys**.

It returns:

```text
True  → if all keys are truthy
False → if at least one key is falsy
```

An important special case:

```python
all({})
```

returns:

```text
True
```

The lecture describes this as `True` when all dictionary keys are true or when the dictionary/list is empty. fileciteturn3file0L133-L141

---

## 8.1 Example With a Falsy Key

### Program

```python
data = {
    1: 31,
    2: 28,
    3: 30,
    0: 10
}

print(all(data))
```

### Output

```text
False
```

Why?

The keys are:

```text
1, 2, 3, 0
```

The key:

```text
0
```

is falsy.

Since **all** keys must be truthy for `all()` to return `True`:

```text
all(data) → False
```

---

## 8.2 Example

### Program

```python
data = {
    1: 31,
    2: 28,
    3: 30
}

print(all(data))
```

### Output

```text
True
```

All keys:

```text
1, 2, 3
```

are truthy.

Therefore:

```text
all(data) → True
```

The lecture uses this example as a Guess The Output question. fileciteturn3file0L142-L146

---

## 8.3 Example With Strings and Boolean

### Program

```python
data = {
    '0': 1,
    True: 2,
    ' ': 3
}

print(all(data))
```

### Output

```text
True
```

The keys are:

```python
'0'
True
' '
```

All are truthy:

- `'0'` → non-empty string → truthy
- `True` → truthy
- `' '` → non-empty string → truthy

Therefore:

```text
True
```

The lecture uses this example to demonstrate truthiness of non-empty strings. fileciteturn3file0L147-L151

---

## 8.4 Empty Dictionary

### Program

```python
data = {}

print(all(data))
```

### Output

```text
True
```

This is an important special case:

```python
all({})
```

returns `True`. fileciteturn3file0L152-L156

---

# 9. `sorted()` Function

## Definition

When a dictionary is passed to `sorted()`:

- The **keys** are sorted.
- Sorting is in **ascending order** by default.
- A new **list of keys** is returned.
- The original dictionary is **not modified**.

## Syntax

```python
sorted(dictionary)
```

The lecture specifically states that `sorted()` returns a sorted list containing only the dictionary keys. fileciteturn3file0L157-L162

---

## 9.1 Example: Sorting Dictionary Keys

### Program

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    "May": 31,
    "Jun": 30
}

print(sorted(sixMonths))
print(sixMonths)
```

### Output

```text
['Apr', 'Feb', 'Jan', 'Jun', 'Mar', 'May']

{'Jan': 31, 'Feb': 28, 'Mar': 31, 'Apr': 30, 'May': 31, 'Jun': 30}
```

### Important observation

The first line is a **list**:

```python
['Apr', 'Feb', 'Jan', 'Jun', 'Mar', 'May']
```

The original dictionary remains unchanged.

This demonstrates:

```text
sorted(dict) → sorted list of keys
```

and **does not modify the original dictionary**. fileciteturn3file0L163-L169

---

## 9.2 Mixed Key Types

### Program

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    4: 31,
    5: 30
}

print(sorted(sixMonths))
```

### Result

This raises a **`TypeError`** because the dictionary contains both:

```text
str
int
```

keys.

Python cannot sort incompatible key types using the normal ordering operation.

The lecture presents this as a Guess The Output question. fileciteturn3file0L170-L174

---

## 9.3 Reverse Sorting

The `sorted()` function supports:

```python
reverse=True
```

to sort in descending order.

### Program

```python
sixMonths = {
    "Jan": 31,
    "Feb": 28,
    "Mar": 31,
    "Apr": 30,
    "May": 31,
    "Jun": 30
}

print(sorted(sixMonths, reverse=True))
```

### Output

```text
['May', 'Mar', 'Jun', 'Jan', 'Feb', 'Apr']
```

The keys are returned in reverse/descending order.

The original dictionary is still not modified. fileciteturn3file0L175-L180

---

# 10. Variable-Length Arguments

The second major topic in the remaining Lecture 37 slides is **variable-length arguments**.

The lecture first demonstrates why a normal function with a fixed number of parameters cannot accept an arbitrary number of arguments.

---

## 10.1 Fixed Number of Arguments

### Example from the lecture

```python
def addnos(x, y, z):
    print("sum:", x + y + z)

addnos(10, 20, 30)
addnos(10, 20, 30, 40, 50)
```

The first function call provides exactly three arguments:

```python
addnos(10, 20, 30)
```

so it can work.

The second call provides five arguments:

```python
addnos(10, 20, 30, 40, 50)
```

but the function has only three parameters:

```python
x, y, z
```

Therefore, the second call results in a **`TypeError`** because too many positional arguments were supplied.

This example motivates the need for variable-length arguments. fileciteturn3file0L181-L190

---

# 11. `*args`

Python provides a mechanism for accepting a variable number of **positional arguments**.

The parameter is prefixed with a single asterisk:

```python
*args
```

The lecture explains that the variable-length arguments received inside the function are stored as a **tuple**. fileciteturn3file0L191-L198

---

## 11.1 Syntax

```python
def function_name(*args):
    ...
```

The name `args` is conventional. The important part is:

```python
*
```

---

## 11.2 Example From the Lecture

```python
def addnos(*args):
    sum = 0

    for x in args:
        sum = sum + x

    print("sum:", sum)

addnos(10, 20, 30)
addnos(10, 20, 30, 40, 50)
```

### Output

```text
sum: 60
sum: 150
```

### How it works

For:

```python
addnos(10, 20, 30)
```

inside the function:

```python
args
```

contains the values as a tuple:

```python
(10, 20, 30)
```

Then:

```python
for x in args:
```

iterates over each value.

The sum becomes:

```text
10 + 20 + 30 = 60
```

For:

```python
addnos(10, 20, 30, 40, 50)
```

the tuple contains:

```python
(10, 20, 30, 40, 50)
```

and:

```text
10 + 20 + 30 + 40 + 50 = 150
```

The complete example is shown in Lecture 37's `*args` section. fileciteturn3file0L199-L209

---

# 12. `**kwargs`

`*args` handles variable-length **positional arguments**.

But sometimes we want to pass variable-length **keyword arguments**, such as:

```python
name="Sachin"
age=38
city="Bhopal"
```

For this purpose Python provides:

```python
**kwargs
```

The lecture introduces `**kwargs` as the solution for variable-length keyword arguments and notes that `*args` cannot be used to pass keyword arguments. fileciteturn3file0L210-L216

---

## 12.1 What Are Keyword Arguments?

Consider:

```python
show(name="Sachin", age=38)
```

Here:

```text
name → keyword
Sachin → actual data/value

age → keyword
38 → actual data/value
```

With `**kwargs`:

```text
keywords become dictionary keys
actual data becomes dictionary values
```

The lecture explicitly describes this mapping. fileciteturn3file0L217-L225

---

## 12.2 Syntax

```python
def function_name(**data):
    ...
```

The double asterisk:

```python
**
```

before the parameter name indicates variable-length keyword arguments.

Inside the function, the arguments are received as a **dictionary**.

---

## 12.3 Example From the Lecture

```python
def show_details(**data):
    print("\nData type of argument:", type(data))

    for key, value in data.items():
        print("{} is {}".format(key, value))


show_details(
    Firstname="Sachin",
    Lastname="Kapoor",
    Age=38,
    Phone=9826012345
)

show_details(
    Firstname="Amit",
    Lastname="Sharma",
    Email="amit@gmail.com",
    Country="India",
    Age=25,
    Phone=9893198931
)
```

The lecture uses this example to demonstrate that `**data` receives the keyword arguments as a dictionary and then iterates over its key-value pairs. fileciteturn3file0L226-L237

---

## 12.4 Understanding the First Call

```python
show_details(
    Firstname="Sachin",
    Lastname="Kapoor",
    Age=38,
    Phone=9826012345
)
```

Inside the function, `data` is conceptually:

```python
{
    "Firstname": "Sachin",
    "Lastname": "Kapoor",
    "Age": 38,
    "Phone": 9826012345
}
```

Therefore:

```python
type(data)
```

is:

```text
<class 'dict'>
```

The loop:

```python
for key, value in data.items():
```

extracts each key-value pair.

The output follows the form:

```text
Firstname is Sachin
Lastname is Kapoor
Age is 38
Phone is 9826012345
```

---

## 12.5 Understanding the Second Call

```python
show_details(
    Firstname="Amit",
    Lastname="Sharma",
    Email="amit@gmail.com",
    Country="India",
    Age=25,
    Phone=9893198931
)
```

Inside the function, `data` contains the supplied keyword arguments as a dictionary:

```python
{
    "Firstname": "Amit",
    "Lastname": "Sharma",
    "Email": "amit@gmail.com",
    "Country": "India",
    "Age": 25,
    "Phone": 9893198931
}
```

Again:

```python
type(data)
```

is:

```text
<class 'dict'>
```

The loop prints each key and value.

---

# 13. `*args` vs `**kwargs`

This distinction is extremely important.

| Feature | `*args` | `**kwargs` |
|---|---|---|
| Argument type | Positional | Keyword |
| Symbol | `*` | `**` |
| Inside function | Tuple | Dictionary |
| Example | `addnos(10, 20, 30)` | `show(name="Amit")` |
| Access | Iterate through tuple | `.items()`, keys, values, etc. |

### `*args`

```python
def addnos(*args):
    print(args)
```

Call:

```python
addnos(10, 20, 30)
```

Conceptually:

```python
args = (10, 20, 30)
```

### `**kwargs`

```python
def show(**data):
    print(data)
```

Call:

```python
show(name="Amit", age=25)
```

Conceptually:

```python
data = {
    "name": "Amit",
    "age": 25
}
```

---

# 14. Quick Revision

## Dictionary Functions

```python
len(d)
```

→ number of key-value pairs.

```python
max(d)
```

→ greatest key.

```python
min(d)
```

→ least key.

```python
any(d)
```

→ `True` if at least one key is truthy.

```python
all(d)
```

→ `True` if all keys are truthy.

```python
sorted(d)
```

→ sorted list of keys.

---

## `sorted()` Important Point

```python
sorted(d)
```

does **not** modify `d`.

It returns a new list.

---

## `max()` / `min()` Important Point

If you want to find the maximum/minimum **value**:

```python
max(d.values())
min(d.values())
```

Do not use:

```python
max(d)
min(d)
```

because those operate on the keys.

---

## `any()` and `all()` Important Point

For a dictionary passed directly:

```python
any(d)
all(d)
```

the **keys are evaluated**, not the values.

---

## Empty Dictionary

```python
any({})
```

→ `False`

```python
all({})
```

→ `True`

---

## Variable-Length Arguments

### `*args`

```python
def function(*args):
    ...
```

- Accepts variable number of positional arguments.
- Arguments are received as a tuple.

### `**kwargs`

```python
def function(**kwargs):
    ...
```

- Accepts variable number of keyword arguments.
- Arguments are received as a dictionary.
- Keywords become keys.
- Supplied data becomes values.

---

# ⭐ Final Memory Table

| Concept | Remember |
|---|---|
| `len(d)` | Number of dictionary items |
| `max(d)` | Greatest key |
| `min(d)` | Least key |
| `max(d.values())` | Greatest value |
| `min(d.values())` | Least value |
| `any(d)` | At least one truthy key |
| `all(d)` | Every key is truthy |
| `any({})` | `False` |
| `all({})` | `True` |
| `sorted(d)` | Sorted list of keys |
| `sorted(d, reverse=True)` | Reverse-sorted list of keys |
| `*args` | Variable positional arguments → tuple |
| `**kwargs` | Variable keyword arguments → dictionary |

---

## 🧠 Easy Way to Remember

```text
Dictionary directly
        ↓
   keys are used
        ↓
len → count
max → greatest
min → smallest
any → at least one True
all → everything True
sorted → sorted keys
```

And:

```text
*args
   ↓
positional arguments
   ↓
tuple

**kwargs
   ↓
keyword arguments
   ↓
dictionary
```

---
==============================================================================================================================================================
# Python Dictionaries — Dictionary Methods & Comprehension

## Part 3

This part covers:

- Dictionary methods
- `copy()`
- `copy()` vs `=`
- `in` and `not in`
- Dictionary comprehension
- Dictionary comprehension syntax
- Copying a dictionary using comprehension
- Transforming dictionary values
- Transforming dictionary keys
- Character frequency counting
- Adding conditions to dictionary comprehension
- Multiple conditions
- Conditional expressions inside dictionary comprehension

---

# 1. Dictionary Methods

Python provides several built-in methods to work with dictionary objects.

The important dictionary methods are:

```text
clear()
copy()
get()
items()
keys()
pop()
update()
values()
```

Some of these methods were already covered earlier. In this part, we focus especially on `copy()` and then move to dictionary comprehension.

---

# 2. The `copy()` Method

The `copy()` method returns a **shallow copy** of a dictionary.

## Syntax

```python
dict.copy()
```

## Example

```python
original = {1: 'one', 2: 'two'}

new = original.copy()

print('new: ', new)
print('original: ', original)
```

## Output

```text
new:  {1: 'one', 2: 'two'}
original:  {1: 'one', 2: 'two'}
```

### What happens?

```python
new = original.copy()
```

creates a **new dictionary** containing the same key-value data.

Therefore:

```python
new
```

and:

```python
original
```

are separate dictionary objects.

---

# 3. `copy()` vs `=`

There is an important difference between:

```python
new = original.copy()
```

and:

```python
new = original
```

## Using `copy()`

When `copy()` is used:

```python
new = original.copy()
```

a new dictionary is created and filled with a copy of the data from the original dictionary.

Conceptually:

```text
original
   ↓
{1: 'one', 2: 'two'}

        copy()

new
   ↓
{1: 'one', 2: 'two'}
```

The two dictionary objects are separate.

---

## Using `=`

When the assignment operator is used:

```python
new = original
```

a new **reference** to the original dictionary is created.

There is still only one dictionary object.

Conceptually:

```text
original ──┐
           ├──→ {1: 'one', 2: 'two'}
new ───────┘
```

Both variables refer to the same dictionary.

---

# 4. Guess the Output — `=` vs `copy()`

Consider the following two programs.

## Case 1 — Using `=`

```python
original = {1: 'one', 2: 'two'}

new = original

new.clear()

print('new: ', new)
print('original: ', original)
```

### Output

```text
new:  {}
original:  {}
```

### Why?

Because:

```python
new = original
```

does not create another dictionary.

Both variables refer to the same object.

So:

```python
new.clear()
```

clears the dictionary that both variables refer to.

---

## Case 2 — Using `copy()`

```python
original = {1: 'one', 2: 'two'}

new = original.copy()

new.clear()

print('new: ', new)
print('original: ', original)
```

### Output

```text
new:  {}
original:  {1: 'one', 2: 'two'}
```

### Why?

Here:

```python
new = original.copy()
```

creates a separate dictionary.

Therefore:

```python
new.clear()
```

only clears `new`.

`original` remains unchanged.

---

## ⭐ Remember

```text
new = original
        ↓
Same dictionary object

new = original.copy()
        ↓
New dictionary object
```

---

# 5. Using `in` and `not in` With Dictionary

The `in` and `not in` operators can be used with dictionaries to check whether a particular **key** is present.

## `in`

If the key is present:

```python
key in dictionary
```

returns:

```text
True
```

If the key is not present:

```text
False
```

---

## `not in`

If the key is not present:

```python
key not in dictionary
```

returns:

```text
True
```

If the key is present:

```text
False
```

### Important

When used directly with a dictionary:

```python
in
not in
```

check the **keys**, not the values.

---

# 6. Guess the Output — `in` and `not in`

## Program

```python
cars = {
    "Maruti": "Ciaz",
    "Hyundai": "Verna",
    "Honda": "Amaze"
}

print(cars)

print("Hyundai is present:", "Hyundai" in cars)

print("Audi is present:", "Audi" in cars)

print("Renault not present:", "Renault" not in cars)
```

## Output

```text
{'Maruti': 'Ciaz', 'Hyundai': 'Verna', 'Honda': 'Amaze'}
Hyundai is present: True
Audi is present: False
Renault not present: True
```

### Explanation

`"Hyundai"` is a key:

```python
"Hyundai" in cars
```

therefore:

```text
True
```

`"Audi"` is not a key:

```python
"Audi" in cars
```

therefore:

```text
False
```

`"Renault"` is not a key:

```python
"Renault" not in cars
```

therefore:

```text
True
```

---

# 7. Dictionary Comprehension

Just as Python provides **list comprehension**, it also provides **dictionary comprehension**.

Dictionary comprehension is a mechanism for transforming one dictionary into another dictionary.

During this transformation:

- Items from the original dictionary can be included conditionally.
- Keys can be transformed.
- Values can be transformed.
- Conditions can be applied.

---

## Basic Idea

Suppose we have:

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3
}
```

Dictionary comprehension can create another dictionary from it:

```python
dict2 = {k: v for k, v in dict1.items()}
```

---

# 8. Syntax for Dictionary Comprehension

## Syntax

```python
dict_variable = {key: value for (key, value) in iterable}
```

### Parts of the syntax

#### `dict_variable`

The name of the new dictionary.

Example:

```python
newdict
```

#### `key:value`

The key-value expression that will be assigned to the new dictionary.

Example:

```python
k:v
```

#### `for (key,value)`

The tuple:

```python
(key, value)
```

receives key-value pairs one at a time.

#### `in iterable`

The iterable can be any object on which iteration is possible.

For dictionaries, a common iterable is:

```python
dictionary.items()
```

---

## Breaking the syntax down

```python
newdict = {k: v for (k, v) in olddict.items()}
```

means:

```text
Take each key-value pair from olddict
            ↓
Put the key in k
Put the value in v
            ↓
Create k:v in newdict
```

---

# 9. Exercise — Copy a Dictionary Using Comprehension

## Problem

Produce a copy of the following dictionary using dictionary comprehension:

```python
cars = {
    "Maruti": "Ciaz",
    "Hyundai": "Verna",
    "Honda": "Amaze"
}
```

## Solution

```python
cars = {
    "Maruti": "Ciaz",
    "Hyundai": "Verna",
    "Honda": "Amaze"
}

newcars = {k: v for (k, v) in cars.items()}

print(newcars)
```

## Output

```text
{'Maruti': 'Ciaz', 'Hyundai': 'Verna', 'Honda': 'Amaze'}
```

### Explanation

```python
cars.items()
```

provides the key-value pairs.

For every pair:

```python
k
```

receives the key and:

```python
v
```

receives the value.

Then:

```python
k: v
```

creates the corresponding entry in `newcars`.

---

# 10. Exercise — Double the Values

## Problem

Create a new dictionary from:

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}
```

The value associated with each key should be doubled.

## Program

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}

double_dict1 = {k: v * 2 for (k, v) in dict1.items()}

print(double_dict1)
```

## Output

```text
{'a': 2, 'b': 4, 'c': 6, 'd': 8, 'e': 10}
```

### What changed?

Original:

```text
a → 1
b → 2
c → 3
d → 4
e → 5
```

New:

```text
a → 2
b → 4
c → 6
d → 8
e → 10
```

Only the **values** are transformed.

The keys remain unchanged.

---

# 11. Exercise — Double the Keys

## Problem

Create a new dictionary where the keys are doubled.

Given:

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}
```

## Program

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}

double_dict1 = {k * 2: v for (k, v) in dict1.items()}

print(double_dict1)
```

## Output

```text
{'aa': 1, 'bb': 2, 'cc': 3, 'dd': 4, 'ee': 5}
```

### What changed?

The keys:

```text
a → aa
b → bb
c → cc
d → dd
e → ee
```

The values remain unchanged.

This is possible because the keys are strings, and:

```python
'a' * 2
```

produces:

```text
'aa'
```

---

# 12. Exercise — Frequency Count of Characters

## Problem

Accept a string from the user and print the frequency count of its letters.

In other words:

> Find how many times each letter occurs in the string.

---

## Solution

```python
str = input("Type a string:")

mydict = {
    ch: str.count(ch)
    for ch in str
}

for k, v in mydict.items():
    print(k, ":", v)
```

### How it works

Suppose the user enters:

```text
India
```

The comprehension processes each character:

```text
I
n
d
i
a
```

For each character:

```python
str.count(ch)
```

counts how many times that character occurs.

The resulting dictionary is:

```python
{
    'I': 1,
    'n': 1,
    'd': 1,
    'i': 1,
    'a': 1
}
```

Output:

```text
I : 1
n : 1
d : 1
i : 1
a : 1
```

### Important observation

If a character occurs more than once, the dictionary still contains only one key for that character.

For example:

```text
India
```

has five distinct characters, so five entries are produced.

For:

```text
banana
```

the repeated characters use the same dictionary key, so the final dictionary contains:

```python
{
    'b': 1,
    'a': 3,
    'n': 2
}
```

---

# 13. Adding Conditions to Dictionary Comprehension

Dictionary comprehension can also contain conditions.

Only those key-value pairs that satisfy the condition are included in the new dictionary.

## Basic syntax

```python
dict_variable = {
    key: value
    for (key, value) in iterable
    if condition
}
```

The condition works like the condition used in list comprehension.

---

## General Structure

```python
new_dict = {
    key_expression: value_expression
    for key, value in old_dict.items()
    if condition
}
```

The process is:

```text
Take an item
     ↓
Check condition
     ↓
Condition True?
   ↙       ↘
 Yes        No
 ↓           ↓
Include     Ignore
```

---

# 14. Exercise — Values Greater Than 2 and Store Their Doubles

## Problem

Create a new dictionary from:

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}
```

Requirements:

1. Select values greater than `2`.
2. Store their doubled values.

## Program

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}

dict2 = {
    k: v * 2
    for (k, v) in dict1.items()
    if v > 2
}

print(dict2)
```

## Output

```text
{'c': 6, 'd': 8, 'e': 10}
```

### Step-by-step

Original:

```text
a → 1
b → 2
c → 3
d → 4
e → 5
```

Condition:

```python
v > 2
```

So:

```text
1 → rejected
2 → rejected
3 → accepted
4 → accepted
5 → accepted
```

Then the accepted values are doubled:

```text
3 → 6
4 → 8
5 → 10
```

Final:

```python
{
    'c': 6,
    'd': 8,
    'e': 10
}
```

---

# 15. Exercise — Two Conditions

## Problem

Create a new dictionary where:

1. The original value is greater than `2`.
2. The original value is also a multiple of `2`.
3. Store the double of the selected value.

Given:

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}
```

## Program

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}

dict2 = {
    k: v * 2
    for (k, v) in dict1.items()
    if v > 2
    if v % 2 == 0
}

print(dict2)
```

## Output

```text
{'d': 8}
```

### Why?

Check each value:

| Key | Value | `v > 2` | `v % 2 == 0` | Included? |
|---|---:|---|---|---|
| `a` | 1 | No | — | No |
| `b` | 2 | No | Yes | No |
| `c` | 3 | Yes | No | No |
| `d` | 4 | Yes | Yes | Yes |
| `e` | 5 | Yes | No | No |

Only:

```text
d → 4
```

satisfies both conditions.

Its value is doubled:

```text
4 × 2 = 8
```

Therefore:

```python
{'d': 8}
```

---

# 16. Exercise — EVEN or ODD

## Problem

Create a new dictionary from:

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}
```

For every value:

- If the value is even, store `"even"`.
- If the value is odd, store `"odd"`.

---

## Program

```python
dict1 = {
    'a': 1,
    'b': 2,
    'c': 3,
    'd': 4,
    'e': 5
}

dict2 = {
    k: 'even' if v % 2 == 0 else 'odd'
    for (k, v) in dict1.items()
}

print(dict2)
```

## Output

```text
{'a': 'odd', 'b': 'even', 'c': 'odd', 'd': 'even', 'e': 'odd'}
```

### How it works

The expression:

```python
'even' if v % 2 == 0 else 'odd'
```

is a conditional expression.

For each value:

```text
1 → odd
2 → even
3 → odd
4 → even
5 → odd
```

The keys remain unchanged.

---

# ⭐ Dictionary Comprehension Patterns

## 1. Copy

```python
new = {
    k: v
    for k, v in old.items()
}
```

---

## 2. Transform Values

```python
new = {
    k: v * 2
    for k, v in old.items()
}
```

---

## 3. Transform Keys

```python
new = {
    k * 2: v
    for k, v in old.items()
}
```

---

## 4. Filter Using a Condition

```python
new = {
    k: v
    for k, v in old.items()
    if v > 2
}
```

---

## 5. Filter Using Multiple Conditions

```python
new = {
    k: v * 2
    for k, v in old.items()
    if v > 2
    if v % 2 == 0
}
```

---

## 6. Conditional Value

```python
new = {
    k: 'even' if v % 2 == 0 else 'odd'
    for k, v in old.items()
}
```

---

# 🧠 Easy Way to Remember Dictionary Comprehension

Think:

```text
{ WHAT : WHAT
  for EACH ITEM
  in WHERE
  if CONDITION }
```

Example:

```python
{k: v * 2 for k, v in data.items() if v > 2}
```

Read it as:

> For every key-value pair in `data`, if the value is greater than 2, put the same key with double the value into the new dictionary.

---

# Quick Revision

| Concept | Syntax |
|---|---|
| Copy dictionary | `new = old.copy()` |
| Same reference | `new = old` |
| Check key exists | `key in dict` |
| Check key absent | `key not in dict` |
| Dictionary comprehension | `{k:v for k,v in dict.items()}` |
| Transform value | `{k:v*2 for k,v in dict.items()}` |
| Transform key | `{k*2:v for k,v in dict.items()}` |
| Add condition | `{k:v for k,v in dict.items() if condition}` |
| Conditional value | `{k:'even' if condition else 'odd' for k,v in dict.items()}` |

---

# ⭐ Most Important Points

### `copy()` vs `=`

```python
new = old
```

→ Both variables refer to the same dictionary.

```python
new = old.copy()
```

→ A separate dictionary is created.

---

### `in` and `not in`

With a dictionary:

```python
key in dict
```

checks the **key**.

```python
key not in dict
```

checks whether the **key is absent**.

---

### Dictionary Comprehension

Used to:

- Copy dictionaries
- Transform keys
- Transform values
- Filter entries
- Apply multiple conditions
- Generate values using conditional expressions

---

## One-Line Memory Trick

```text
copy()       → Separate dictionary
=            → Same dictionary reference

in           → Key exists?
not in       → Key doesn't exist?

Comprehension
     ↓
Transform + Filter + Create
```
===============================================================================================================================================================
# Python Dictionaries — Part 4
## Restrictions on Dictionary Keys and Values

---

## Table of Contents

1. [Restrictions on Dictionary Keys](#1-restrictions-on-dictionary-keys)
2. [Almost Any Type Can Be a Key](#2-almost-any-type-can-be-a-key)
3. [Class Names as Dictionary Keys](#3-class-names-as-dictionary-keys)
4. [Duplicate Keys](#4-duplicate-keys)
5. [Duplicate Keys During Dictionary Creation](#5-duplicate-keys-during-dictionary-creation)
6. [Dictionary Keys Must Be Immutable](#6-dictionary-keys-must-be-immutable)
7. [Lists and Dictionaries Cannot Be Keys](#7-lists-and-dictionaries-cannot-be-keys)
8. [Restrictions on Dictionary Values](#8-restrictions-on-dictionary-values)
9. [Quick Revision](#9-quick-revision)

---

# 1. Restrictions on Dictionary Keys

Dictionary keys have some important rules.

The main idea is:

> **Dictionary keys must be hashable, which in the examples here means using immutable objects.**

Python allows many different types to be used as dictionary keys.

Common examples include:

- `int`
- `float`
- `bool`
- `str`
- `tuple` (when it is immutable)

But mutable objects such as:

- `list`
- `dict`

cannot be used as dictionary keys.

---

# 2. Almost Any Type Can Be a Key

Almost any type of value can be used as a dictionary key, such as:

- integers
- floating-point numbers
- Boolean values
- strings
- and other suitable immutable objects

### Example

```python
d = {65: "A", 3.14: "pi", True: 1}

print(d)
```

### Explanation

Here, the keys are:

```text
65
3.14
True
```

All three are valid dictionary keys.

The corresponding values are:

```text
"A"
"pi"
1
```

A dictionary does not require all keys to have the same data type.

For example, this dictionary contains an integer, a float, and a Boolean key.

---

# 3. Class Names as Dictionary Keys

Class names can also be used as dictionary keys.

### Example

```python
d = {int: 1, float: 2, bool: 3}

print(d)
print(d[float])
```

### Explanation

Here:

```python
int
float
bool
```

are being used as dictionary keys.

The dictionary associates:

| Key | Value |
|---|---:|
| `int` | `1` |
| `float` | `2` |
| `bool` | `3` |

The expression:

```python
d[float]
```

accesses the value associated with the `float` key.

So it gives:

```text
2
```

### Important Point

A dictionary key does not have to be a normal string or number. Suitable objects, including class objects, can also be used as keys.

---

# 4. Duplicate Keys

### Rule

**Duplicate keys are not allowed as separate entries in a dictionary.**

If we assign a value to an already existing key:

- Python does not create another copy of that key.
- The existing value is replaced.

### Example

```python
d = {
    "MP": "Indore",
    "UP": "Lucknow",
    "RAJ": "Jaipur"
}

print(d)

d["MP"] = "Bhopal"

print(d)
```

### Before updating

```text
{'MP': 'Indore', 'UP': 'Lucknow', 'RAJ': 'Jaipur'}
```

Then:

```python
d["MP"] = "Bhopal"
```

changes the value associated with `"MP"`.

### After updating

```text
{'MP': 'Bhopal', 'UP': 'Lucknow', 'RAJ': 'Jaipur'}
```

### What happened?

The key:

```text
"MP"
```

already existed.

Therefore, Python **replaced its old value**:

```text
"Indore"
```

with:

```text
"Bhopal"
```

It did **not** create another `"MP"` entry.

### Remember

```python
d["MP"] = "Bhopal"
```

means:

> If `"MP"` already exists, update its value.

---

# 5. Duplicate Keys During Dictionary Creation

Duplicate keys can also appear while initially creating a dictionary.

If the same key is specified more than once, the later occurrence overrides the earlier one.

### Example

```python
d = {
    "MP": "Indore",
    "UP": "Lucknow",
    "RAJ": "Jaipur",
    "MP": "Bhopal"
}

print(d)
```

Here `"MP"` appears twice:

```python
"MP": "Indore"
```

and later:

```python
"MP": "Bhopal"
```

The later value replaces the earlier one.

### Result

```text
{'MP': 'Bhopal', 'UP': 'Lucknow', 'RAJ': 'Jaipur'}
```

### Important Exam Point

When duplicate keys occur during dictionary creation:

> **The last value assigned to that key is retained.**

So:

```python
{"A": 10, "A": 20}
```

results in:

```python
{"A": 20}
```

---

# 6. Dictionary Keys Must Be Immutable

A dictionary key must be of a type that is **immutable**.

Examples of suitable immutable types include:

- `int`
- `float`
- `str`
- `bool`
- `tuple`

### Why?

Dictionary keys need to remain stable so Python can reliably locate the corresponding dictionary entry.

Therefore, mutable objects such as lists and dictionaries cannot normally be used as keys.

---

## Tuple as a Dictionary Key

A tuple can be used as a dictionary key because tuples are immutable.

### Example

```python
d = {
    (1, 1): "a",
    (1, 2): "b",
    (2, 1): "c",
    (2, 2): "d"
}

print(d)
print(d[(1, 2)])
```

### Dictionary

```text
{
    (1, 1): 'a',
    (1, 2): 'b',
    (2, 1): 'c',
    (2, 2): 'd'
}
```

The expression:

```python
d[(1, 2)]
```

accesses the value stored for the tuple key:

```text
(1, 2)
```

So the result is:

```text
b
```

### Key Idea

```python
(1, 2)
```

is a tuple.

Because the tuple is immutable, it can be used as a dictionary key.

---

# 7. Lists and Dictionaries Cannot Be Keys

A list cannot be used as a dictionary key because a list is mutable.

Similarly, another dictionary cannot be used as a dictionary key because dictionaries are mutable.

### Example

```python
d = {
    [1, 1]: "a",
    [1, 2]: "b",
    [2, 1]: "c",
    [2, 2]: "d"
}

print(d)
```

This is invalid.

The keys here are lists:

```python
[1, 1]
[1, 2]
[2, 1]
[2, 2]
```

Lists are mutable, so they cannot be used as dictionary keys.

Python will raise an error because the list is unhashable.

### Remember

| Object | Mutable? | Can be a dictionary key? |
|---|---|---|
| `int` | No | ✅ Yes |
| `float` | No | ✅ Yes |
| `str` | No | ✅ Yes |
| `bool` | No | ✅ Yes |
| `tuple` | No | ✅ Yes |
| `list` | Yes | ❌ No |
| `dict` | Yes | ❌ No |

### Easy Memory Trick

> **Immutable → suitable for keys**  
> **Mutable → not suitable for keys**

---

# 8. Restrictions on Dictionary Values

The rules for dictionary **values** are much less restrictive.

There are **no restrictions on dictionary values** in the sense that a value can be any type of object Python supports.

A dictionary value can be:

- integer
- float
- string
- Boolean
- list
- dictionary
- tuple
- user-defined object
- and other Python objects

This is different from dictionary keys.

---

## Example: Multiple Entries Can Have the Same Value

There is no restriction against a particular value appearing multiple times in a dictionary.

For example:

```python
d = {
    "A": 10,
    "B": 10,
    "C": 20
}
```

The value:

```text
10
```

appears more than once.

This is completely valid.

### Important Difference

Duplicate **keys** are not retained as separate entries.

Duplicate **values** are allowed.

So this is valid:

```python
{
    "A": 10,
    "B": 10,
    "C": 10
}
```

because the keys are different even though the values are the same.

---

## Values Can Be Mutable

Unlike keys, dictionary values can be mutable objects.

For example, a list can be a value:

```python
d = {
    "numbers": [1, 2, 3]
}

print(d)
```

A dictionary can also be a value:

```python
d = {
    "student": {
        "name": "Rahul",
        "age": 20
    }
}

print(d)
```

So:

> **Keys have restrictions; values can be much more flexible.**

---

# 9. Quick Revision

## Dictionary Key Rules

### ✅ Valid key types from these examples

```text
int
float
bool
str
tuple
class names / class objects
```

### ❌ Invalid key types from these examples

```text
list
dict
```

The important distinction is **immutability/hashability**.

---

## Duplicate Key Rule

If a key appears more than once:

```python
d = {"A": 10, "A": 20}
```

the later value wins:

```python
{"A": 20}
```

Similarly:

```python
d["A"] = 30
```

updates the existing value instead of creating another `"A"` key.

---

## Duplicate Value Rule

Duplicate values are completely allowed:

```python
d = {
    "A": 10,
    "B": 10,
    "C": 10
}
```

This is valid because the keys are different.

---

## Key vs Value — Most Important Comparison

| Feature | Dictionary Key | Dictionary Value |
|---|---|---|
| Must be unique? | ✅ Yes | ❌ No |
| Can be mutable? | ❌ No | ✅ Yes |
| Can be a list? | ❌ No | ✅ Yes |
| Can be a dictionary? | ❌ No | ✅ Yes |
| Can be a tuple? | ✅ Yes | ✅ Yes |
| Can be a string? | ✅ Yes | ✅ Yes |
| Can be an integer? | ✅ Yes | ✅ Yes |

---

## 🧠 One-Line Memory Trick

> **KEY = Immutable + Unique**  
> **VALUE = Any Python object + Duplicates allowed**

---

## Exam-Oriented Questions

### Q1. Can a list be used as a dictionary key?

**Answer:** No. A list is mutable and therefore cannot be used as a dictionary key.

### Q2. Can a tuple be used as a dictionary key?

**Answer:** Yes. A tuple is immutable.

### Q3. What happens if a key is repeated?

**Answer:** The later value replaces/overrides the earlier value.

### Q4. Can two dictionary keys have the same value?

**Answer:** Yes. Duplicate values are allowed.

### Q5. Can a dictionary be a dictionary value?

**Answer:** Yes. Dictionary values can be mutable objects, including other dictionaries.

### Q6. Can a dictionary be used as a dictionary key?

**Answer:** No. A dictionary is mutable and therefore cannot be used as a key.

---



**Covered:**

- Restrictions on dictionary keys
- Different types that can be dictionary keys
- Class names as keys
- Duplicate keys
- Duplicate keys during creation
- Immutable keys
- Tuple keys
- Why lists cannot be keys
- Why dictionaries cannot be keys
- Restrictions on values
- Duplicate values
- Mutable values
- Key vs value comparison
- Exam-oriented revision
=============================================================================================================================================================
# Python Dictionaries — Part 5
## Country Management Application

---

## Table of Contents

1. [Country Management App — Exercise](#1-country-management-app--exercise)
2. [Initial Country Data](#2-initial-country-data)
3. [Required Operations](#3-required-operations)
4. [Program Menu](#4-program-menu)
5. [Displaying Country Names](#5-displaying-country-names)
6. [Adding a Country](#6-adding-a-country)
7. [Deleting a Country](#7-deleting-a-country)
8. [Main Program](#8-main-program)
9. [Complete Country Management App](#9-complete-country-management-app)
10. [Modified Country Management App — Exercise](#10-modified-country-management-app--exercise)
11. [Three Values for Each Country](#11-three-values-for-each-country)
12. [Quick Revision](#12-quick-revision)

---

# 1. Country Management App — Exercise

The exercise is to create a complete **Country Management App** using a Python dictionary.

The dictionary stores:

```text
COUNTRY CODE → COUNTRY NAME
```

For example:

```text
IN → India
US → America
```

The application should allow the user to perform operations on the dictionary.

---

# 2. Initial Country Data

The program starts with the following country data:

| Country Code | Country Name |
|---|---|
| `IN` | India |
| `US` | America |
| `AU` | Australia |
| `CA` | Canada |

The dictionary is:

```python
countries = {
    "IN": "India",
    "US": "America",
    "AU": "Australia",
    "CA": "Canada"
}
```

Here:

- `IN`, `US`, `AU`, `CA` are the **keys**
- `India`, `America`, `Australia`, `Canada` are the **values**

---

# 3. Required Operations

The application provides these operations:

### 1. View

Display the country names stored in the dictionary.

### 2. Add

Add a new country and its country code.

### 3. Delete

Delete a country from the dictionary.

### 4. Exit

Terminate the program.

The user selects an operation from the menu.

---

# 4. Program Menu

The program displays:

```text
SELECT AN OPTION:
view: View country names
add: Add a country
del: Delete a country
exit- Exit the program
```

The user then enters their choice.

Example:

```text
Your choice: view
```

The program performs the corresponding operation.

---

# 5. Displaying Country Names

A separate function is used to handle the **view** operation.

```python
def view_country(countries):
    ...
```

The dictionary is passed to the function.

The purpose of this function is to display the countries stored in the dictionary.

### Function idea

```text
countries dictionary
        ↓
view_country()
        ↓
display country information
```

Using a separate function keeps the program organized.

---

# 6. Adding a Country

A separate function handles adding a country:

```python
def add_country(countries):
    ...
```

The function receives the dictionary and adds a new country.

The basic dictionary operation used for adding is:

```python
countries[key] = value
```

For example:

```python
countries["UK"] = "United Kingdom"
```

This adds a new key-value pair.

---

# 7. Deleting a Country

A separate function handles deletion:

```python
def del_country(countries):
    ...
```

A country can be removed from the dictionary using dictionary deletion operations.

For example:

```python
del countries["UK"]
```

This removes the key `"UK"` and its associated value.

---

# 8. Main Program

After defining the functions, the dictionary is initialized:

```python
countries = {
    "IN": "India",
    "US": "America",
    "AU": "Australia",
    "CA": "Canada"
}
```

The program then repeatedly displays the menu and asks the user for a choice.

The main loop is:

```python
while True:
    show_menu()

    choice = input("Your choice:")

    if choice == "view":
        view_country(countries)

    elif choice == "add":
        add_country(countries)

    elif choice == "del":
        del_country(countries)

    elif choice == "exit":
        break

    else:
        print("Wrong choice ! Try again!")
```

---

## Understanding the Main Loop

### `while True`

```python
while True:
```

creates an infinite loop.

The application keeps running until the user chooses:

```text
exit
```

---

### Display the menu

```python
show_menu()
```

The menu is shown to the user.

---

### Take user input

```python
choice = input("Your choice:")
```

The user enters one of the available commands.

---

### View option

```python
if choice == "view":
    view_country(countries)
```

If the user enters:

```text
view
```

the `view_country()` function is called.

---

### Add option

```python
elif choice == "add":
    add_country(countries)
```

If the user enters:

```text
add
```

the `add_country()` function is called.

---

### Delete option

```python
elif choice == "del":
    del_country(countries)
```

If the user enters:

```text
del
```

the `del_country()` function is called.

---

### Exit option

```python
elif choice == "exit":
    break
```

The `break` statement terminates the `while` loop.

Therefore, the application exits.

---

### Invalid option

```python
else:
    print("Wrong choice ! Try again!")
```

If the user enters anything other than:

```text
view
add
del
exit
```

the program displays:

```text
Wrong choice ! Try again!
```

and the loop continues.

---

# 9. Complete Country Management App

The application is organized using separate functions.

## Menu Function

```python
def show_menu():
    print("SELECT AN OPTION:")
    print("view: View country names")
    print("add: Add a country")
    print("del: Delete a country")
    print("exit- Exit the program")
    print()
```

## Country Functions

The application defines functions for the three dictionary operations:

```python
def view_country(countries):
    # View country information
    pass

def add_country(countries):
    # Add a country
    pass

def del_country(countries):
    # Delete a country
    pass
```

The function names are:

```text
view_country()
add_country()
del_country()
```

---

## Main Program Structure

```python
countries = {
    "IN": "India",
    "US": "America",
    "AU": "Australia",
    "CA": "Canada"
}

while True:
    show_menu()

    choice = input("Your choice:")

    if choice == "view":
        view_country(countries)

    elif choice == "add":
        add_country(countries)

    elif choice == "del":
        del_country(countries)

    elif choice == "exit":
        break

    else:
        print("Wrong choice ! Try again!")
```

### Program Flow

```text
Start
  ↓
Initialize countries dictionary
  ↓
Display menu
  ↓
Take user choice
  ↓
 ┌────────┬────────┬────────┬────────┐
 ↓        ↓        ↓        ↓
view     add      del      exit
 ↓        ↓        ↓        ↓
View     Add     Delete    Stop
country  country country   program
  ↓        ↓        ↓
  └────────┴────────┘
          ↓
      Show menu again
```

---

# 10. Modified Country Management App — Exercise

The next exercise modifies the previous application.

Instead of storing only:

```text
COUNTRY CODE → COUNTRY NAME
```

the program must store **three values for each key**.

The three values are:

1. Country Name
2. Capital City
3. Population

The same options should still be provided to the user.

---

# 11. Three Values for Each Country

The starting data is:

| Country Code | Country Name | Capital City | Population |
|---|---|---|---:|
| `IN` | India | Delhi | 1,400,000,000 |
| `US` | America | Washington | 320,000,000 |
| `AU` | Australia | Canberra | 24,000,000 |
| `CA` | Canada | Ottawa | 940,000 |

The given country information is:

```text
IN → India, Delhi, 1400000000
US → America, Washington, 320000000
AU → Australia, Canberra, 24000000
CA → Canada, Ottawa, 940000
```

---

## Representing Multiple Values

A dictionary normally stores:

```python
key: value
```

When multiple pieces of information are required for one key, the value can contain multiple pieces of data.

For example, a country's value could be represented using a list or tuple:

```python
countries = {
    "IN": ["India", "Delhi", 1400000000],
    "US": ["America", "Washington", 320000000],
    "AU": ["Australia", "Canberra", 24000000],
    "CA": ["Canada", "Ottawa", 940000]
}
```

Here:

```text
Key → Multiple values
```

For example:

```text
IN → ["India", "Delhi", 1400000000]
```

contains:

```text
Country Name → India
Capital      → Delhi
Population   → 1400000000
```

---

## Same User Options

The modified application should still provide the same operations:

```text
view
add
del
exit
```

So the basic application structure remains the same.

The difference is that each country now stores **three pieces of information instead of one**.

---

# 12. Quick Revision

## Original Application

The dictionary stores:

```text
COUNTRY CODE → COUNTRY NAME
```

Example:

```python
countries = {
    "IN": "India",
    "US": "America"
}
```

---

## Modified Application

The dictionary stores:

```text
COUNTRY CODE → COUNTRY NAME + CAPITAL + POPULATION
```

Example:

```python
countries = {
    "IN": ["India", "Delhi", 1400000000]
}
```

---

## Important Functions

```python
show_menu()
view_country()
add_country()
del_country()
```

---

## Main Loop

```python
while True:
```

keeps the application running.

The loop ends when:

```python
break
```

is executed after the user selects:

```text
exit
```

---

## Important Dictionary Operations Used

### Add / Update

```python
countries[key] = value
```

### Delete

```python
del countries[key]
```

### Access

```python
countries[key]
```

---

# 🧠 Final Memory Map

```text
COUNTRY MANAGEMENT APP
        │
        ├── Dictionary
        │      │
        │      └── Country Code → Country Data
        │
        ├── Menu
        │      ├── view
        │      ├── add
        │      ├── del
        │      └── exit
        │
        ├── Functions
        │      ├── show_menu()
        │      ├── view_country()
        │      ├── add_country()
        │      └── del_country()
        │
        └── while True
               │
               ├── view → View data
               ├── add  → Add data
               ├── del  → Delete data
               └── exit → break
```

---

# Part 5 Complete

This completes the remaining material on:

- Country Management App
- Country code and country name dictionary
- View operation
- Add operation
- Delete operation
- Exit operation
- Menu function
- Main program loop
- Modified application
- Storing country name, capital city and population
- Initial data for all four countries
