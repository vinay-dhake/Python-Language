# Python OOP — Multiple Inheritance

## 1. Multiple Inheritance

**Multiple inheritance** occurs when one child class inherits from more than one parent class.

```text
Parent Class A       Parent Class B
       \                   /
        \                 /
         \               /
          Child Class C
```

The basic syntax is:

```python
class A:
    # properties and methods
    pass

class B:
    # properties and methods
    pass

class C(A, B):
    # members of C
    pass
```

Here `C` inherits from both `A` and `B`.

---

## 2. Features of Multiple Inheritance

In multiple inheritance, the derived class can use functionality provided by all its base classes.

```text
A        B
 \      /
  \    /
    C
```

The order in:

```python
class C(A, B):
```

is important because Python uses that order while determining the **Method Resolution Order (MRO)**.

---

## 3. Real-World Example — Smartphone

A smartphone can combine capabilities associated with a phone and a computer.

```text
        Phone              Computer
          \                   /
           \                 /
            \               /
             Smartphone
```

A phone can provide:

- Making calls
- Sending messages

A computer can provide:

- Running applications
- Internet browsing

A smartphone can additionally provide its own features, such as taking pictures.

---

## 4. Smartphone Example

```python
class Phone:

    def make_call(self):
        print("Making a call")


class Computer:

    def browse_internet(self):
        print("Surfing the internet")


class SmartPhone(Phone, Computer):

    def take_pic(self):
        print("Taking pic using camera")


apple = SmartPhone()

apple.make_call()
apple.browse_internet()
apple.take_pic()
```

### Output

```text
Making a call
Surfing the internet
Taking pic using camera
```

### Explanation

```python
apple.make_call()
```

comes from `Phone`.

```python
apple.browse_internet()
```

comes from `Computer`.

```python
apple.take_pic()
```

is defined directly inside `SmartPhone`.

---

# 5. Multiple Inheritance with Constructors

Consider two independent parent classes.

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def getname(self):
        return self.name

    def getage(self):
        return self.age
```

Another class:

```python
class Student:

    def __init__(self, roll, per):
        self.roll = roll
        self.per = per

    def getroll(self):
        return self.roll

    def getper(self):
        return self.per
```

Now a child can inherit from both:

```python
class ScienceStudent(Person, Student):
    pass
```

---

# 6. Complete `ScienceStudent` Example

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def getname(self):
        return self.name

    def getage(self):
        return self.age


class Student:

    def __init__(self, roll, per):
        self.roll = roll
        self.per = per

    def getroll(self):
        return self.roll

    def getper(self):
        return self.per


class ScienceStudent(Person, Student):

    def __init__(self, name, age, roll, per, stream):
        Person.__init__(self, name, age)
        Student.__init__(self, roll, per)
        self.stream = stream

    def getstream(self):
        return self.stream


ms = ScienceStudent("Suresh", 19, 203, 89.4, "maths")

print("Name:", ms.getname())
print("Age:", ms.getage())
print("Roll:", ms.getroll())
print("Per:", ms.getper())
print("Stream:", ms.getstream())
```

### Output

```text
Name: Suresh
Age: 19
Roll: 203
Per: 89.4
Stream: maths
```

---

# 7. Constructor Execution

When this executes:

```python
ms = ScienceStudent("Suresh", 19, 203, 89.4, "maths")
```

the child constructor performs three kinds of initialization.

### Person initialization

```python
Person.__init__(self, name, age)
```

creates:

```python
self.name
self.age
```

### Student initialization

```python
Student.__init__(self, roll, per)
```

creates:

```python
self.roll
self.per
```

### ScienceStudent initialization

```python
self.stream = stream
```

creates:

```python
self.stream
```

So the object contains:

```text
name
age
roll
per
stream
```

---

# 8. Accessing Members from Both Parents

The object:

```python
ms = ScienceStudent(...)
```

can use:

```python
ms.getname()
ms.getage()
```

from `Person`.

It can use:

```python
ms.getroll()
ms.getper()
```

from `Student`.

It can use:

```python
ms.getstream()
```

from `ScienceStudent`.

Conceptually:

```text
ScienceStudent
│
├── Person
│   ├── getname()
│   └── getage()
│
├── Student
│   ├── getroll()
│   └── getper()
│
└── own method
    └── getstream()
```

---

# 9. Why Parent Constructors Are Explicitly Called

Both parent classes have their own initialization logic.

Therefore the child constructor explicitly calls:

```python
Person.__init__(self, name, age)
```

and:

```python
Student.__init__(self, roll, per)
```

This initializes the state supplied by both parent classes.

---

# 10. Guess the Output

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(A, B):
    pass


obj = C()
obj.m()
```

### Output

```text
m of A called
```

Both parents contain `m()`.

Python therefore needs a rule to decide which implementation to use.

That rule is called **Method Resolution Order (MRO)**.

For:

```python
class C(A, B):
```

the relevant order starts with:

```text
C → A → B
```

So `A.m()` is found first.
=================================================================================================================================================================
# Python OOP — Method Resolution Order (MRO)

## 1. What Is MRO?

**MRO** stands for **Method Resolution Order**.

In multiple inheritance, MRO defines the order in which Python searches classes when looking for a method or attribute.

It becomes important when more than one parent class contains a member with the same name.

---

## 2. Why MRO Is Needed

Consider:

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(A, B):
    pass
```

Both `A` and `B` define:

```python
m()
```

Now:

```python
obj = C()
obj.m()
```

Which implementation should execute?

Python uses MRO to determine the answer.

---

## 3. Basic MRO Rule

For multiple inheritance, Python:

1. Searches the current class first.
2. If the member is not found, it searches the parent classes according to the MRO.
3. Parent order matters.
4. A class is not unnecessarily searched more than once.
5. The common base `object` appears at the end of the normal MRO.

For a simple declaration:

```python
class C(A, B):
    pass
```

the order is conceptually:

```text
C → A → B → object
```

---

## 4. Seeing MRO with `mro()`

Python provides:

```python
ClassName.mro()
```

to inspect a class's method resolution order.

Example:

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(A, B):
    pass


print(C.mro())
```

The result is conceptually:

```text
[
    C,
    A,
    B,
    object
]
```

The actual interactive Python representation contains class objects such as:

```text
<class '__main__.C'>
<class '__main__.A'>
<class '__main__.B'>
<class 'object'>
```

`mro()` returns the MRO as a **list**.

---

## 5. Seeing MRO with `__mro__`

Python also provides:

```python
ClassName.__mro__
```

Example:

```python
class A:
    pass


class B:
    pass


class C(A, B):
    pass


print(C.__mro__)
```

The result is conceptually:

```text
(
    C,
    A,
    B,
    object
)
```

`__mro__` returns the MRO as a **tuple**.

---

## 6. `mro()` vs `__mro__`

| Feature | `mro()` | `__mro__` |
|---|---|---|
| Syntax | `C.mro()` | `C.__mro__` |
| Result | List | Tuple |
| Purpose | Display MRO | Display MRO |
| Order | Same | Same |

Both show the same method-resolution sequence.

---

## 7. Complete MRO Example

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(A, B):
    pass


obj = C()

obj.m()

print(C.mro())
print(C.__mro__)
```

### Method output

```text
m of A called
```

because the search begins:

```text
C → A → B → object
```

and `A` contains `m()`.

---

## 8. Changing the Parent Order

Now change:

```python
class C(A, B):
```

to:

```python
class C(B, A):
```

Example:

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(B, A):
    pass


obj = C()
obj.m()
```

### Output

```text
m of B called
```

The MRO now begins:

```text
C → B → A → object
```

Therefore `B.m()` is found first.

---

## 9. Why Parent Order Matters

Compare:

```python
class C(A, B):
    pass
```

with:

```python
class C(B, A):
    pass
```

### First

```text
C → A → B → object
```

Result:

```text
m of A called
```

### Second

```text
C → B → A → object
```

Result:

```text
m of B called
```

Therefore the order of parent classes affects method lookup.

---

## 10. Current Class Is Searched First

Consider:

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(A, B):

    def m(self):
        print("m of C called")


obj = C()
obj.m()
```

### Output

```text
m of C called
```

Python starts with:

```text
C
```

Since `C` already defines `m()`, the search stops there.

---

## 11. MRO and Attribute Lookup

MRO is also relevant when Python searches for attributes.

```python
class A:
    x = 10


class B:
    x = 20


class C(A, B):
    pass


obj = C()

print(obj.x)
```

The relevant order is:

```text
C → A → B → object
```

`C` does not define `x`.

`A` defines `x` first.

Therefore:

```text
10
```

is printed.

---

## 12. MRO Search Visualization

For:

```python
class C(A, B):
    pass
```

think of method lookup as:

```text
          obj.m()
             │
             ▼
             C
             │
        Does C have m?
          /               Yes        No
         │          │
         ▼          ▼
      Execute       A
                    │
               Does A have m?
                 /                      Yes        No
                │          │
                ▼          ▼
             Execute       B
```

The search continues until the required member is found.

---

## 13. MRO and `super()`

`super()` is closely related to MRO.

It should not simply be understood as:

> "Call the class written immediately above."

Instead, `super()` continues method lookup through the appropriate inheritance resolution order.

Example:

```python
class A:

    def show(self):
        print("A")


class B(A):

    def show(self):
        print("B")
        super().show()


class C(B):

    def show(self):
        print("C")
        super().show()


obj = C()
obj.show()
```

### Output

```text
C
B
A
```

The calls continue through the inheritance chain.

---

## 14. Why MRO Is Important

Without a defined method-search order, multiple inheritance could create uncertainty.

For example:

```text
       A       B
        \     /
         \   /
           C
```

If both `A` and `B` define:

```python
show()
```

Python needs a deterministic way to choose an implementation.

MRO supplies that order.

```text
Multiple Inheritance
        ↓
Possible name conflict
        ↓
MRO
        ↓
Deterministic lookup
```

---

## 15. Important MRO Points

- MRO means **Method Resolution Order**.
- It determines the class-search order for methods and attributes.
- The current class is searched first.
- Parent order matters.
- `Class.mro()` displays the MRO as a list.
- `Class.__mro__` displays the MRO as a tuple.
- `object` appears at the end of the normal MRO.
- MRO prevents ambiguous method lookup by defining a consistent search sequence.
===============================================================================================================================================================
# Python OOP — Hybrid Inheritance

## 1. Hybrid Inheritance

**Hybrid inheritance** is a combination of more than one form of inheritance.

A common structure combines:

- Hierarchical inheritance
- Multiple inheritance

```text
             A
            / \
           /   \
          B     C
           \   /
            \ /
             D
```

Here:

```text
A → B
A → C
B, C → D
```

So `B` and `C` form a hierarchical structure with `A`, while `D` demonstrates multiple inheritance.

---

## 2. Understanding the Structure

```text
        Class A
        /     \
       ↓       ↓
   Class B   Class C
       \       /
        ↓     ↓
         Class D
```

Relationships:

- `B` inherits from `A`.
- `C` inherits from `A`.
- `D` inherits from both `B` and `C`.

This is a hybrid inheritance structure.

---

## 3. Real-World Example — Employee Hierarchy

Consider:

```text
              Employee
              /      \
             /        \
        Manager      Engineer
            \          /
             \        /
              TechLead
```

Here:

- `Employee` is the common base.
- `Manager` inherits from `Employee`.
- `Engineer` inherits from `Employee`.
- `TechLead` inherits from both `Manager` and `Engineer`.

The `TechLead` class combines two inheritance paths.

---

## 4. Basic Hybrid Example

```python
class A:

    def m1(self):
        print("m1 of A called")


class B(A):

    def m2(self):
        print("m2 of B called")


class C(A):

    def m3(self):
        print("m3 of C called")


class D(B, C):
    pass
```

The hierarchy is:

```text
        A
       / \
      B   C
       \ /
        D
```

---

## 5. Using the Hybrid-Inheritance Classes

```python
obj = D()

obj.m1()
obj.m2()
obj.m3()
```

### Output

```text
m1 of A called
m2 of B called
m3 of C called
```

### Explanation

`m1()` is defined in `A`.

Because both `B` and `C` inherit from `A`, `D` can eventually access it.

`m2()` is defined in `B`.

`m3()` is defined in `C`.

Therefore `D` can access all three methods.

---

# 6. The Diamond Problem

The **Diamond Problem** is an ambiguity that can arise in hybrid inheritance.

The basic structure is:

```text
        A
       / \
      B   C
       \ /
        D
```

Suppose:

- `A` defines `m()`.
- `B` inherits from `A` and overrides `m()`.
- `C` inherits from `A` and overrides `m()`.
- `D` inherits from both `B` and `C`.

Now `D` has two possible inherited implementations:

```text
B.m()
C.m()
```

The question is:

> Which version of `m()` should `D` use?

This situation is called the **Diamond Problem**.

---

## 7. Why It Is Called the Diamond Problem

The inheritance diagram resembles a diamond:

```text
        A
       / \
      B   C
       \ /
        D
```

The common base is `A`.

The two intermediate classes are `B` and `C`.

The final derived class is `D`.

---

# 8. Diamond Problem Example

```python
class A:

    def m(self):
        print("m of A called")


class B(A):

    def m(self):
        print("m of B called")


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass


obj = D()
obj.m()
```

### Output

```text
m of B called
```

Why?

The class declaration is:

```python
class D(B, C):
```

The relevant MRO is:

```text
D → B → C → A → object
```

Python searches:

1. `D`
2. `B`
3. `C`
4. `A`
5. `object`

`D` does not define `m()`.

`B` defines `m()`.

Therefore Python executes:

```python
B.m()
```

---

# 9. Reverse the Parent Order

Now write:

```python
class D(C, B):
    pass
```

The complete example is:

```python
class A:

    def m(self):
        print("m of A called")


class B(A):

    def m(self):
        print("m of B called")


class C(A):

    def m(self):
        print("m of C called")


class D(C, B):
    pass


obj = D()
obj.m()
```

### Output

```text
m of C called
```

The MRO now begins:

```text
D → C → B → A → object
```

`C.m()` is therefore found first.

---

# 10. Child Class Overrides the Method

Suppose `D` itself defines `m()`:

```python
class D(B, C):

    def m(self):
        print("m of D called")
```

Then:

```python
obj = D()
obj.m()
```

produces:

```text
m of D called
```

The current class is always considered first.

So the search stops at:

```text
D
```

---

# 11. One Intermediate Class Does Not Override

Consider:

```python
class A:

    def m(self):
        print("m of A called")


class B(A):
    pass


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass


obj = D()
obj.m()
```

### Output

```text
m of C called
```

The MRO is:

```text
D → B → C → A → object
```

Search:

```text
D → m not found
B → m not directly defined
C → m found
```

Therefore `C.m()` executes.

---

# 12. Important Observation

A child class such as `B` may inherit a method from `A`, but Python's MRO is still followed.

For:

```text
D → B → C → A → object
```

if `B` does not directly define `m()` and `C` does, `C.m()` is found before the search reaches `A`.

Therefore:

```text
B inherits m from A
```

does not mean that Python immediately chooses `A.m()` simply because `B` appears before `C`.

The actual MRO determines the lookup sequence.

---

# 13. MRO Solves the Diamond Problem

Python uses MRO to give method lookup a deterministic order.

For:

```text
        A
       / \
      B   C
       \ /
        D
```

with:

```python
class D(B, C):
```

the search follows the appropriate resolution order.

If `B` defines the method, `B`'s version is selected before `C`'s version.

If `B` does not define it but `C` does, Python can find `C`'s implementation before reaching `A`.

Thus Python can resolve the diamond structure using its method-resolution mechanism.

---

# 14. Real-World Analogy — Amphibious Vehicle

A similar hybrid structure can be imagined as:

```text
             Vehicle
             /     \
            /       \
          Car       Boat
            \       /
             \     /
        AmphibiousCar
```

`Vehicle` is the common parent.

`Car` and `Boat` inherit from it.

`AmphibiousCar` inherits from both.

If both `Car` and `Boat` define a method such as:

```python
move()
```

then the final class needs a defined method-selection rule.

MRO provides that rule.

---

# 15. Hybrid Inheritance + MRO

The relationship can be summarized as:

```text
Hybrid Inheritance
        ↓
Multiple inheritance paths
        ↓
Possible method-name conflicts
        ↓
MRO determines search order
        ↓
First applicable implementation is selected
```

---

# 16. Key Points

- Hybrid inheritance combines more than one inheritance form.
- A common structure combines hierarchical and multiple inheritance.
- The diamond structure is a common hybrid-inheritance pattern.
- The Diamond Problem concerns method ambiguity created by a shared base and two intermediate classes.
- Python uses MRO to determine method lookup order.
- The current class is searched first.
- Parent order matters.
- `D(B, C)` and `D(C, B)` can produce different results.
- If `D` defines the method itself, `D`'s method is selected.
- A specific parent implementation can be explicitly invoked when required.
==============================================================================================================================================================
# Python OOP — Final MRO Revision, Output Questions & Summary

## 1. Manual Method Call

Sometimes we want to call a particular parent's implementation directly instead of allowing normal MRO lookup to choose it.

Suppose:

```python
class A:

    def m(self):
        print("m of A called")


class B(A):

    def m(self):
        print("m of B called")


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass
```

Create an object:

```python
obj = D()
```

Normal call:

```python
obj.m()
```

follows the MRO:

```text
D → B → C → A → object
```

and therefore prints:

```text
m of B called
```

But we can explicitly call:

```python
C.m(obj)
```

which prints:

```text
m of C called
```

---

## 2. `obj.m()` vs `C.m(obj)`

### Normal method call

```python
obj.m()
```

Python performs normal method lookup using the MRO.

```text
obj.m()
   ↓
MRO lookup
   ↓
D → B → C → A → object
```

### Explicit parent implementation

```python
C.m(obj)
```

The method from `C` is explicitly selected.

```text
C.m(obj)
   ↓
Directly execute C.m()
```

This distinction is useful when solving output questions.

---

# 3. Complete Diamond Example

```python
class A:

    def m(self):
        print("m of A called")


class B(A):

    def m(self):
        print("m of B called")


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass


obj = D()

obj.m()
```

### Output

```text
m of B called
```

### MRO

```text
D → B → C → A → object
```

`D` does not contain `m()`.

`B` contains `m()`.

Therefore `B.m()` is selected.

---

# 4. Reverse Parent Order

```python
class D(C, B):
    pass
```

### MRO

```text
D → C → B → A → object
```

### Output

```text
m of C called
```

This demonstrates why parent order matters.

---

# 5. Child Overrides the Method

```python
class D(B, C):

    def m(self):
        print("m of D called")
```

Now:

```python
obj = D()
obj.m()
```

### Output

```text
m of D called
```

The search begins with `D`, and `D` already contains `m()`.

---

# 6. No Override in `B`

```python
class A:

    def m(self):
        print("m of A called")


class B(A):
    pass


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass


obj = D()
obj.m()
```

### Output

```text
m of C called
```

### MRO

```text
D → B → C → A → object
```

Search:

```text
D → not found
B → no direct m()
C → found
```

Therefore:

```text
m of C called
```

---

# 7. Guess-the-Output Questions

## Question 1

```python
class A:

    def m(self):
        print("m of A called")


class B:

    def m(self):
        print("m of B called")


class C(A, B):
    pass


obj = C()
obj.m()
```

### Answer

```text
m of A called
```

Reason:

```text
C → A → B → object
```

---

## Question 2

Change:

```python
class C(A, B):
```

to:

```python
class C(B, A):
```

### Answer

```text
m of B called
```

Reason:

```text
C → B → A → object
```

---

## Question 3

```python
class A:

    def m(self):
        print("m of A called")


class B(A):

    def m(self):
        print("m of B called")


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass


obj = D()
obj.m()
```

### Answer

```text
m of B called
```

Reason:

```text
D → B → C → A → object
```

---

## Question 4

Change:

```python
class D(B, C):
```

to:

```python
class D(C, B):
```

### Answer

```text
m of C called
```

---

## Question 5

```python
class D(B, C):

    def m(self):
        print("m of D called")
```

### Answer

```text
m of D called
```

The current class is checked first.

---

## Question 6

```python
class A:

    def m(self):
        print("m of A called")


class B(A):
    pass


class C(A):

    def m(self):
        print("m of C called")


class D(B, C):
    pass


D().m()
```

### Answer

```text
m of C called
```

The MRO is:

```text
D → B → C → A → object
```

`B` does not directly define `m()`, so the search continues to `C`.

---

# 8. How to Solve MRO Output Questions

When you see multiple or hybrid inheritance, use this method.

### Step 1 — Draw the hierarchy

For example:

```text
        A
       /       B   C
       \ /
        D
```

### Step 2 — Look at the child declaration

```python
class D(B, C):
```

The parent order is:

```text
B first
C second
```

### Step 3 — Check the child

Does `D` define the required method?

If yes, execute `D`'s method.

If not, continue.

### Step 4 — Follow the MRO

For the simple diamond:

```text
D → B → C → A → object
```

### Step 5 — Find the first applicable implementation

Stop when the required method is found.

---

# 9. Final Concept Map

```text
                         INHERITANCE
                              │
                ┌─────────────┴─────────────┐
                │                           │
        Multiple Inheritance        Hybrid Inheritance
                │                           │
        A + B → C                  Combination of forms
                │                           │
                ▼                           ▼
        Possible conflict             Diamond structure
                │                           │
                └─────────────┬─────────────┘
                              ▼
                             MRO
                              │
              ┌───────────────┼───────────────┐
              │               │               │
        Current class     Parent order      object
          searched          matters         at end
              │
              ▼
       First applicable method
```

---

# 10. Multiple Inheritance vs Hybrid Inheritance

| Topic | Multiple Inheritance | Hybrid Inheritance |
|---|---|---|
| Meaning | One child inherits from multiple parents | Combination of multiple inheritance forms |
| Simple structure | `A + B → C` | `A → B`, `A → C`, `B + C → D` |
| Example | `SmartPhone(Phone, Computer)` | `D(B, C)` where both `B` and `C` inherit from `A` |
| Main topic | Multiple parent classes | Combined inheritance structures |
| MRO relevance | Important | Very important |
| Diamond structure | Not required | Common example |

---

# 11. MRO Quick Reference

```python
class C(A, B):
    pass
```

Typical simple order:

```text
C → A → B → object
```

Reverse:

```python
class C(B, A):
    pass
```

Typical simple order:

```text
C → B → A → object
```

For a diamond:

```python
class B(A):
    pass

class C(A):
    pass

class D(B, C):
    pass
```

the conceptual order is:

```text
D → B → C → A → object
```

---

# 12. Important Differences

## `mro()`

```python
C.mro()
```

- Used to inspect MRO.
- Returns a list.

## `__mro__`

```python
C.__mro__
```

- Used to inspect MRO.
- Returns a tuple.

## `obj.method()`

```python
obj.m()
```

- Uses normal method lookup.
- Follows MRO.

## `Parent.method(obj)`

```python
C.m(obj)
```

- Explicitly selects the specified class's method.
- Does not rely on normal MRO selection to choose between `B` and `C`.

---

# 13. Exam-Oriented Questions

## Theory Questions

1. What is multiple inheritance?
2. Write the syntax for multiple inheritance.
3. What are the advantages of multiple inheritance?
4. What is MRO?
5. Why is MRO required?
6. Explain the MRO search rule.
7. How can MRO be viewed in Python?
8. What is the difference between `mro()` and `__mro__`?
9. What is hybrid inheritance?
10. Explain the diamond problem.
11. How does Python resolve the diamond problem?
12. Why does changing parent order change the output?
13. What happens if the child class itself overrides the method?
14. How can a specific parent's method be called directly?

---

# 14. Programming Questions

### Question 1

Create:

```text
Phone
Computer
   \ /
SmartPhone
```

Implement:

- `make_call()`
- `browse_internet()`
- `take_pic()`

Demonstrate multiple inheritance.

### Question 2

Create:

```text
Person
Student
    \ /
ScienceStudent
```

Initialize all attributes and display them.

### Question 3

Create:

```text
A
/ B  C
\ /
 D
```

Give `A`, `B`, and `C` the same method and predict which implementation `D` uses.

### Question 4

Change:

```python
class D(B, C):
```

to:

```python
class D(C, B):
```

and explain the output difference.

### Question 5

Display the MRO using both:

```python
D.mro()
```

and:

```python
D.__mro__
```

### Question 6

Explicitly call `C`'s implementation using:

```python
C.method(obj)
```

---

# 15. Final Revision Table

| Concept | Main Idea | Typical Syntax |
|---|---|---|
| Multiple inheritance | One child has multiple parents | `class C(A, B)` |
| MRO | Method search order | `C.mro()` |
| `mro()` | Displays MRO as a list | `C.mro()` |
| `__mro__` | Displays MRO as a tuple | `C.__mro__` |
| Parent order | Affects lookup | `C(A, B)` |
| Hybrid inheritance | Combination of inheritance types | `D(B, C)` |
| Diamond Problem | Shared base creates method-selection ambiguity | `A → B,C → D` |
| Current class | Searched first | `D().m()` |
| Explicit method call | Select a specific class implementation | `C.m(obj)` |

---

# 16. Final Key Points to Remember

1. Multiple inheritance allows a class to inherit from more than one base class.
2. Syntax:

```python
class Child(Parent1, Parent2):
```

3. The order of parent classes matters.
4. MRO means **Method Resolution Order**.
5. Python checks the current class first.
6. If a method is not found, Python follows the MRO.
7. `Class.mro()` returns MRO information as a list.
8. `Class.__mro__` returns MRO information as a tuple.
9. `object` normally appears at the end of the MRO.
10. Hybrid inheritance combines more than one inheritance form.
11. The diamond structure is a common hybrid-inheritance structure.
12. The Diamond Problem concerns which implementation should be used when two intermediate classes provide competing implementations.
13. Python uses MRO to determine a consistent lookup order.
14. `D(B, C)` and `D(C, B)` can produce different results.
15. If `D` defines the method itself, `D`'s implementation is selected first.
16. If `B` does not directly define a method but `C` does, the MRO can reach `C` before `A`.
17. A specific implementation can be directly called using:

```python
ParentClass.method(obj)
```

18. For output questions, first determine the MRO and then find the first class in that order that defines the required method.
