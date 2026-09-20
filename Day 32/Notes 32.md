# Lecture 32: Methods in Python — Part 1

> **Topic:** More on Object-Oriented Programming  
> **Focus:** Methods in a class, types of methods, instance methods, `self`, accessing instance variables, `__dict__`, and the employee salary-increment practical.

---

## 1. Introduction

Once a class has been created, the next step is to provide **methods** inside the class.

A **method** is a function defined inside a class. Methods define the behavior of objects.

Python provides three types of methods in a class:

1. **Instance Methods**
2. **Class Methods**
3. **Static Methods**

---

# 2. Types of Methods in Python

| Type | Usually called using | Main purpose |
|---|---|---|
| **Instance Method** | Object | Works with instance/object data |
| **Class Method** | Class name | Works with class-level data |
| **Static Method** | Class name | Utility operation without automatic object/class reference |

Memory trick:

```text
Instance Method → Object
Class Method    → Class
Static Method   → Utility
```

---

# 3. Instance Methods

## Definition

**Instance methods** are the most common type of methods in Python classes.

They are called instance methods because they can access the **instance members** of an object.

An instance method:

- belongs to an object/instance
- can access instance variables
- can access other instance methods
- can modify the state of the current object
- normally takes `self` as its first parameter

---

## 3.1 Why is `self` used?

An instance method needs to know **which object** is calling it.

The first parameter is normally named `self`.

`self` points to the **current object** for which the method is being called.

Example:

```python
class Emp:
    def show(self):
        print("Employee details")
```

When we write:

```python
e1 = Emp()
e1.show()
```

Python conceptually passes `e1` to `show()`:

```python
Emp.show(e1)
```

Therefore, inside that call:

```python
self
```

refers to `e1`.

---

# 4. What Can an Instance Method Access?

Through `self`, an instance method can access:

- instance variables
- other instance methods
- the state of the current object

Example:

```python
class Emp:
    def __init__(self, age, name, salary):
        self.age = age
        self.name = name
        self.salary = salary

    def show(self):
        print("Age:", self.age, "Name:", self.name, "Salary:", self.salary)
```

Here:

```python
self.age
self.name
self.salary
```

are instance variables of the current object.

---

# 5. Complete Instance Method Example

```python
class Emp:
    def __init__(self, age, name, salary):
        self.age = age
        self.name = name
        self.salary = salary

    def show(self):
        print("Age:", self.age, "Name:", self.name, "Salary:", self.salary)


e = Emp(25, "Rahul", 30000.0)
f = Emp(31, "Varun", 45000.0)

e.show()
f.show()
```

### Output

```text
Age: 25 Name: Rahul Salary: 30000.0
Age: 31 Name: Varun Salary: 45000.0
```

## Step-by-step

### First object

```python
e = Emp(25, "Rahul", 30000.0)
```

`e` gets:

```text
age = 25
name = Rahul
salary = 30000.0
```

### Second object

```python
f = Emp(31, "Varun", 45000.0)
```

`f` gets:

```text
age = 31
name = Varun
salary = 45000.0
```

### Calling the method

```python
e.show()
```

Here `self` refers to `e`.

```python
f.show()
```

Here `self` refers to `f`.

Thus the same `show()` method works with different objects.

---

# 6. Instance Methods Can Modify Object State

Instance methods can also modify an object's instance variables.

```python
class EMP:
    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary

    def display(self):
        print(f"Name: {self.name}, Age: {self.age}, Salary: {self.salary}")

    def apply_raise(self, percentage):
        self.salary += self.salary * (percentage / 100)


e1 = EMP("Aman", 25, 50000)
e2 = EMP("Rahul", 28, 60000)

e1.display()
e1.apply_raise(10)
e1.display()
```

### Output

```text
Name: Aman, Age: 25, Salary: 50000
Name: Aman, Age: 25, Salary: 55000.0
```

`apply_raise()` modifies:

```python
self.salary
```

for the object on which it is called.

---

# 7. Important Rule: Instance Variables Must Be Accessed Through `self`

Consider:

```python
class Emp:
    def __init__(self):
        self.name = "Amit"
        self.age = 24
        self.sal = 50000.0

    def show(self):
        print(age, name, sal)


e1 = Emp()
e1.show()
```

This gives a `NameError` because:

```python
age
name
sal
```

are being treated as ordinary names, not as instance attributes.

The output shown in the material is:

```text
NameError: name 'age' is not defined
```

### Correct code

```python
class Emp:
    def __init__(self):
        self.name = "Amit"
        self.age = 24
        self.sal = 50000.0

    def show(self):
        print(self.age, self.name, self.sal)


e1 = Emp()
e1.show()
```

### Output

```text
24 Amit 50000.0
```

---

# 8. Constructor Parameters vs Instance Variables

Consider:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

    def show(self):
        print(age, name, sal)


e1 = Emp("amit", 34, 50000.0)
e1.show()
```

The parameters:

```python
name
age
sal
```

are local to `__init__()`.

They are not automatically available inside `show()`.

The values are stored in the object through:

```python
self.name = name
self.age = age
self.sal = sal
```

Therefore the correct `show()` method is:

```python
def show(self):
    print(self.age, self.name, self.sal)
```

The incorrect version produces:

```text
NameError: name 'age' is not defined
```

### Key distinction

```text
name       → local parameter
self.name  → instance variable
```

---

# 9. Obtaining Details of Instance Variables Using `__dict__`

Every normal Python object with an instance dictionary has an attribute called:

```python
__dict__
```

It contains the object's instance attributes and their values in dictionary form.

Example:

```python
class Emp:
    def __init__(self):
        self.name = "Amit"
        self.age = 24
        self.sal = 50000.0


e1 = Emp()
print(e1.__dict__)
```

### Output

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
```

The dictionary maps:

```text
attribute name → value
```

So:

| Attribute | Value |
|---|---|
| `name` | `"Amit"` |
| `age` | `24` |
| `sal` | `50000.0` |

---

# 10. Creating Instance Variables Using `__dict__`

Because `__dict__` is a dictionary, it can also be manipulated to add an instance variable.

```python
class Emp:
    def __init__(self):
        self.name = "Amit"
        self.age = 24
        self.sal = 50000.0

    def show(self):
        print(self.name, self.age, self.sal, self.department)


e1 = Emp()

print(e1.__dict__)
e1.__dict__['department'] = 'IT'
print(e1.__dict__)
e1.show()
```

### Output

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
{'name': 'Amit', 'age': 24, 'sal': 50000.0, 'department': 'IT'}
Amit 24 50000.0 IT
```

The important statement is:

```python
e1.__dict__['department'] = 'IT'
```

which adds an instance attribute called `department` to `e1`.

---

# 11. Four Ways to Create Instance Variables

The material identifies four ways to create instance variables.

## 1. Inside `__init__()` using `self`

```python
class Emp:
    def __init__(self):
        self.name = "Amit"
        self.age = 24
```

## 2. Inside any instance method using `self`

```python
class Emp:
    def setDept(self, department):
        self.department = department
```

## 3. Outside the class using the object reference

```python
class Emp:
    def __init__(self):
        self.name = "Amit"


e1 = Emp()
e1.salary = 50000.0
```

## 4. Using `__dict__`

```python
e1.__dict__['department'] = 'IT'
```

### Summary

```text
1. __init__()       → self.variable
2. Instance method  → self.variable
3. Outside class    → object.variable
4. __dict__         → object.__dict__['variable']
```

---

# 12. Instance Variables Can Differ Between Objects

Consider:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

    def setDept(self, department):
        self.department = department

    def setProject(self, project):
        self.project = project

    def setBonus(self, bonus):
        self.bonus = bonus


e1 = Emp("Amit", 24, 30000.0)
e2 = Emp("Sumit", 34, 45000.0)

e1.setDept("Finance")
e1.setProject("Banking Info System")
e1.setBonus(20000.0)

e2.setDept("Production")

print(e1.__dict__)
print()
print(e2.__dict__)
```

### Output

```text
{'name': 'Amit', 'age': 24, 'sal': 30000.0, 'department': 'Finance', 'project': 'Banking Info System', 'bonus': 20000.0}

{'name': 'Sumit', 'age': 34, 'sal': 45000.0, 'department': 'Production'}
```

### Important observation

`e1` and `e2` belong to the same class, but they do not have exactly the same instance variables.

`e1` has:

```text
name, age, sal, department, project, bonus
```

`e2` has:

```text
name, age, sal, department
```

The material highlights that Python is dynamically typed, so objects of the same class can have different numbers of instance variables.

---

# 13. Class Methods

A **class method** is bound to the class rather than to an individual object.

It is used to access or modify class-level data.

A class method is created using:

```python
@classmethod
```

Its first parameter is conventionally named:

```python
cls
```

where `cls` refers to the class.

### General syntax

```python
class ClassName:

    @classmethod
    def method_name(cls):
        pass
```

A class method can be called using:

```python
ClassName.method_name()
```

---

# 14. Class Method Example

```python
class EMP:
    company = "TechCorp"

    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary

    @classmethod
    def set_company(cls, new_name):
        cls.company = new_name

    @classmethod
    def get_company(cls):
        return cls.company

    def display(self):
        print(f"Name: {self.name}, Company: {EMP.company}")


print(EMP.get_company())

EMP.set_company("Amazon")

e1 = EMP("Aman", 25, 50000)
e1.display()
```

### Output

```text
TechCorp
Name: Aman, Company: Amazon
```

### Explanation

Initially:

```python
company = "TechCorp"
```

Calling:

```python
EMP.set_company("Amazon")
```

changes the class-level value to:

```text
Amazon
```

---

# 15. `self` vs `cls`

| `self` | `cls` |
|---|---|
| Refers to current object | Refers to current class |
| Used in instance methods | Used in class methods |
| Accesses instance variables | Accesses class variables |
| Example: `self.name` | Example: `cls.company` |

Memory trick:

```text
self → instance/object
cls  → class
```

---

# 16. Static Methods

A **static method** does not automatically receive:

- `self`
- `cls`

It is generally used for a utility operation that is logically related to the class but does not need instance or class state.

A static method uses:

```python
@staticmethod
```

General form:

```python
class ClassName:

    @staticmethod
    def method_name():
        pass
```

It is normally called as:

```python
ClassName.method_name()
```

### Important comparison

```text
Instance Method → self
Class Method    → cls
Static Method   → no automatic self/cls
```

---

# 17. Circle Exercise

## Problem Statement

Create a class called `Circle` having an instance member called `radius`.

Provide the following methods:

### `__init__()`

Initialize `radius` using the parameter passed to the constructor.

### `cal_area()`

Calculate and print the area of the circle.

### `cal_circumference()`

Calculate and print the circumference of the circle.

Finally, in the main script:

1. Take radius from the user.
2. Create a `Circle` object.
3. Calculate the area.
4. Calculate the circumference.
5. Display both results.

---

# 18. Circle — Complete Solution

```python
import math

class Circle:
    def __init__(self, radius):
        self.radius = radius

    def cal_area(self):
        area = math.pi * math.pow(self.radius, 2)
        print("Area of circle is", area)

    def cal_circumference(self):
        circumf = math.tau * self.radius
        print("Circumference of circle is", circumf)


radius = int(input("Enter radius:"))
cobj = Circle(radius)
cobj.cal_area()
cobj.cal_circumference()
```

### Example output from the material

For radius `10`:

```text
Enter radius:10
Area of circle is 314.1592653589793
Circumference of circle is 62.83185307179586
```

### Formula used

Area:

```text
πr²
```

Circumference:

```text
2πr
```

In the code, circumference is calculated using:

```python
math.tau * self.radius
```

where `math.tau` represents `2π`.

---

# 19. Homework / Practical Exercise — Employee Salary Increment

Create an `EMP` class to manage employee details and calculate salary increments based on a raise percentage supplied at runtime.

## Requirements

### Instance attributes

```text
name
age
salary
```

### Class attribute

```python
raise_amount
```

### Methods

1. `__init__()` — initialize employee details.
2. `set_raise_amount(cls, amount)` — set the raise percentage using a class method.
3. `increase_sal(self)` — apply the raise to the current employee's salary.
4. `display(self)` — display employee details.

---

# 20. Complete Employee Salary Increment Program

```python
class EMP:
    raise_amount = 0

    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self.salary = salary

    @classmethod
    def set_raise_amount(cls, amount):
        cls.raise_amount = amount

    def increase_sal(self):
        self.salary += self.salary * (EMP.raise_amount / 100)

    def display(self):
        print(
            f"Name: {self.name} | "
            f"Age: {self.age} | "
            f"Salary: {self.salary:.2f}"
        )


if __name__ == "__main__":

    user_raise = float(
        input("Enter company raise percentage (e.g., 10 for 10%): ")
    )

    EMP.set_raise_amount(user_raise)

    emp1 = EMP("Rahul", 26, 50000)
    emp2 = EMP("Priya", 24, 70000)

    print("\n--- Before Increment ---")
    emp1.display()
    emp2.display()

    emp1.increase_sal()
    emp2.increase_sal()

    print("\n--- After Increment ---")
    emp1.display()
    emp2.display()
```

---

# 21. Understanding the Employee Program

## Step 1 — Class variable

```python
raise_amount = 0
```

This is a class variable shared at the class level.

## Step 2 — Constructor

```python
def __init__(self, name, age, salary):
    self.name = name
    self.age = age
    self.salary = salary
```

Each employee object gets its own name, age, and salary.

## Step 3 — Set raise percentage

```python
@classmethod
def set_raise_amount(cls, amount):
    cls.raise_amount = amount
```

If the user enters `10`, then the class-level raise percentage becomes `10`.

## Step 4 — Increase salary

```python
def increase_sal(self):
    self.salary += self.salary * (EMP.raise_amount / 100)
```

For a salary of `50000` and a raise of `10%`:

```text
Increase = 50000 × 10 / 100
         = 5000

New salary = 55000
```

For `70000`:

```text
Increase = 70000 × 10 / 100
         = 7000

New salary = 77000
```

## Step 5 — Display

```python
def display(self):
    print(
        f"Name: {self.name} | "
        f"Age: {self.age} | "
        f"Salary: {self.salary:.2f}"
    )
```

This is an instance method because it uses `self` to access employee-specific data.

---

# 22. Quick Comparison of Method Types

| Feature | Instance Method | Class Method | Static Method |
|---|---|---|---|
| Decorator | None required | `@classmethod` | `@staticmethod` |
| First automatic parameter | `self` | `cls` | None |
| Main data | Instance/object data | Class data | Neither automatically |
| Typical call | `obj.method()` | `Class.method()` | `Class.method()` |
| Example | `e1.display()` | `EMP.set_company()` | `Class.utility()` |

---

# 23. Important Exam Questions

### Q1. What is an instance method?

An instance method is a method that operates on the data/state of an individual object and normally takes `self` as its first parameter.

### Q2. Why is `self` used?

`self` refers to the current object and allows the method to access that object's instance variables and other methods.

### Q3. How do you access an instance variable inside an instance method?

Using:

```python
self.variable_name
```

Example:

```python
self.salary
```

### Q4. Can an instance method modify instance variables?

Yes.

```python
self.salary += 5000
```

### Q5. What is `__dict__`?

`__dict__` contains the object's instance attributes and their values in dictionary form.

### Q6. What is a class method?

A class method is bound to the class and is normally used to access or modify class-level data.

### Q7. Which decorator creates a class method?

```python
@classmethod
```

### Q8. What is the first parameter of a class method?

Conventionally:

```python
cls
```

### Q9. Which decorator creates a static method?

```python
@staticmethod
```

### Q10. Does a static method automatically receive `self`?

No.

---

# 24. Common Mistakes

## Mistake 1 — Forgetting `self`

Wrong:

```python
class Emp:
    def show():
        print("Hello")
```

Correct:

```python
class Emp:
    def show(self):
        print("Hello")
```

## Mistake 2 — Accessing instance variables without `self`

Wrong:

```python
def show(self):
    print(name)
```

Correct:

```python
def show(self):
    print(self.name)
```

## Mistake 3 — Confusing local variables and instance variables

```python
def __init__(self, name):
    self.name = name
```

Here:

```text
name      → local parameter
self.name → instance variable
```

## Mistake 4 — Confusing `self` and `cls`

```text
self → current object
cls  → current class
```

---

# 25. Memory Map

```text
                    METHODS IN PYTHON
                           |
          +----------------+----------------+
          |                |                |
      INSTANCE           CLASS           STATIC
       METHOD            METHOD           METHOD
          |                |                |
        self              cls          no automatic
          |                |             self/cls
          |                |
     object data       class data
          |                |
     self.name         cls.company
```

---

# 26. One-Line Revision

```text
Method = function inside a class

Instance Method → works with object → self
Class Method    → works with class  → cls
Static Method   → utility method    → no automatic self/cls

self.variable → instance variable

obj.__dict__ → dictionary containing object's instance attributes

Instance variables can be created:
1. inside __init__() using self
2. inside another instance method using self
3. outside class using object reference
4. using __dict__
```

---

# 27. Part 1 Coverage Checklist

- [x] Introduction to methods in a class
- [x] Three types of methods
- [x] Instance methods
- [x] `self`
- [x] Accessing instance variables through `self`
- [x] Employee instance-method example
- [x] Modifying object state using an instance method
- [x] Error caused by accessing instance variables without `self`
- [x] Constructor parameters vs instance variables
- [x] `__dict__`
- [x] Creating instance variables using instance methods
- [x] Different objects having different instance variables
- [x] Four ways to create instance variables
- [x] Class methods
- [x] `@classmethod`
- [x] `cls`
- [x] Class-method employee example
- [x] Static-method definition
- [x] Circle exercise and complete solution
- [x] Employee salary-increment practical
- [x] Exam-oriented points
- [x] Common mistakes
- [x] Quick revision map

---

**End of Part 1**
 Part 2

> **Focus of Part 2:** Deleting instance variables, `del`, deleting attributes through methods and object references, deleting an object reference, `del self`, and detailed output-based examples.

---

# 1. Deleting Instance Variables

Just as instance variables can be created dynamically, they can also be **deleted**.

Python provides the `del` statement for removing an instance variable.

There are **two ways** to delete an instance variable:

1. From inside the class using:
   ```python
   del self.variable_name
   ```

2. From outside the class using:
   ```python
   del object_reference.variable_name
   ```

---

# 2. Deleting an Instance Variable from Inside the Class

Suppose we have:

```python
class Boy:
    def __init__(self, name, girlfriend):
        self.name = name
        self.girlfriend = girlfriend

    def breakup(self):
        del self.girlfriend
```

The method:

```python
def breakup(self):
    del self.girlfriend
```

removes the `girlfriend` instance variable from the current object.

Before calling `breakup()`:

```python
self.girlfriend
```

exists.

After calling:

```python
del self.girlfriend
```

it no longer exists.

---

# 3. Guess the Output — Deleting an Instance Variable Inside a Method

Consider:

```python
class Boy:
    def __init__(self, name, girlfriend):
        self.name = name
        self.girlfriend = girlfriend

    def breakup(self):
        del self.girlfriend


b1 = Boy("Deepak", "Jyoti")

print(b1.__dict__)

b1.breakup()

print(b1.girlfriend)
```

## Step 1: Object creation

```python
b1 = Boy("Deepak", "Jyoti")
```

The object contains:

```python
{
    'name': 'Deepak',
    'girlfriend': 'Jyoti'
}
```

Therefore:

```python
print(b1.__dict__)
```

prints:

```text
{'name': 'Deepak', 'girlfriend': 'Jyoti'}
```

---

## Step 2: Call `breakup()`

```python
b1.breakup()
```

Inside the method:

```python
del self.girlfriend
```

Since:

```text
self → b1
```

this effectively removes:

```python
b1.girlfriend
```

from the object.

---

## Step 3: Try to access the deleted variable

```python
print(b1.girlfriend)
```

The attribute no longer exists.

Therefore Python raises an:

```text
AttributeError
```

The output shown in the lecture is:

```text
{'name': 'Deepak', 'girlfriend': 'Jyoti'}

Traceback (most recent call last):
    ...
AttributeError: 'Boy' object has no attribute 'girlfriend'
```

### Important

Deleting an instance variable does **not** delete the entire object.

Only that particular attribute is removed.

---

# 4. Effect of Deletion on `__dict__`

Because instance variables are represented in the object's `__dict__`, deleting an instance variable also removes its entry from `__dict__`.

For example:

```python
class Engineer:
    def __init__(self, girlfriend, job):
        self.girlfriend = girlfriend
        self.job = job

    def fired(self):
        del self.job
```

Initially:

```python
{
    'girlfriend': 'Rani',
    'job': 'Software Engineer'
}
```

After:

```python
e1.fired()
```

the `job` attribute is removed.

The object then contains only:

```python
{
    'girlfriend': 'Rani'
}
```

---

# 5. Deleting an Instance Variable from Outside the Class

An instance variable can also be deleted directly using its object reference.

Syntax:

```python
del object_reference.variable_name
```

Example:

```python
class Engineer:
    def __init__(self, girlfriend, job):
        self.girlfriend = girlfriend
        self.job = job

    def fired(self):
        del self.job


e1 = Engineer("Rani", "Software Engineer")

print(e1.__dict__)

e1.fired()

del e1.girlfriend

print(e1.__dict__)
```

### Output

```text
{'girlfriend': 'Rani', 'job': 'Software Engineer'}
{}
```

### What happened?

Initially:

```text
girlfriend → Rani
job        → Software Engineer
```

After:

```python
e1.fired()
```

the following was removed:

```python
job
```

So:

```text
girlfriend → Rani
```

remained.

Then:

```python
del e1.girlfriend
```

removed the remaining instance variable.

Therefore:

```python
e1.__dict__
```

became:

```python
{}
```

---

# 6. Two Ways to Delete Instance Variables — Revision

| Where? | Syntax | Example |
|---|---|---|
| Inside class / instance method | `del self.var` | `del self.job` |
| Outside class | `del obj.var` | `del e1.girlfriend` |

Memory trick:

```text
Inside method → self
Outside class → object reference
```

---

# 7. Deleting the Object Reference

Deleting an instance variable is different from deleting the object reference.

Consider:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal


e1 = Emp("Amit", 24, 50000.0)

print(e1.__dict__)

del e1

print(e1.__dict__)
```

The important statement is:

```python
del e1
```

Here, `e1` is a reference variable.

`del e1` removes the reference named `e1`.

It does not mean:

```python
del e1.name
del e1.age
del e1.sal
```

It removes the variable/reference `e1`.

---

# 8. Guess the Output — `del e1`

Code:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal


e1 = Emp("Amit", 24, 50000.0)

print(e1.__dict__)

del e1

print(e1.__dict__)
```

Before deleting the reference:

```python
print(e1.__dict__)
```

produces:

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
```

Then:

```python
del e1
```

removes the name `e1`.

Therefore the next statement:

```python
print(e1.__dict__)
```

tries to use a name that no longer exists.

The lecture shows:

```text
NameError: name 'e1' is not defined
```

---

# 9. `del object.variable` vs `del object`

These two statements are very different.

## Delete one instance variable

```python
del e1.sal
```

Only:

```python
e1.sal
```

is removed.

The object and its other attributes continue to exist.

---

## Delete the reference

```python
del e1
```

The reference named `e1` is removed.

After this:

```python
e1
```

cannot be used.

### Easy comparison

```text
del e1.sal
    ↓
Delete one attribute

del e1
    ↓
Delete the reference named e1
```

---

# 10. `del self` Inside an Instance Method

A particularly important example is:

```python
def remove(self):
    del self
```

At first, it may look as though:

```python
del self
```

will delete the object.

But that is **not what happens** in the example.

`self` is itself a local reference inside the method.

Deleting `self` removes that local reference.

If another reference is still pointing to the same object, the object continues to exist.

---

# 11. Guess the Output — `del self`

Consider:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

    def remove(self):
        del self


e1 = Emp("Amit", 24, 50000.0)

print(e1.__dict__)

e1.remove()

print(e1.__dict__)
```

The lecture shows the output as:

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
```

---

# 12. Why Doesn't `del self` Delete the Object?

Suppose:

```python
e1 = Emp("Amit", 24, 50000.0)
```

Conceptually:

```text
e1 ───────────────► Emp object
```

When:

```python
e1.remove()
```

is called, Python passes the object reference into `self`.

Inside the method:

```text
e1 ───────────────► object
self ─────────────► object
```

There are two references pointing to the same object.

Now:

```python
del self
```

removes only the local reference:

```text
self ─────────────► object    ← removed
```

But:

```text
e1 ───────────────► object
```

still exists.

Therefore the object can still be accessed through:

```python
e1
```

and:

```python
e1.__dict__
```

still works.

### Main idea

```text
del self
    ↓
removes the local reference self
    ↓
does NOT remove the object while e1 still refers to it
```

---

# 13. Instance Variables Belong Separately to Each Object

Every object gets its own copy of its instance variables.

Consider:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal


e1 = Emp("Amit", 24, 50000.0)
e2 = Emp("Sumit", 25, 45000.0)
```

The two objects have separate instance data.

Conceptually:

```text
e1
 ├── name = Amit
 ├── age  = 24
 └── sal  = 50000.0

e2
 ├── name = Sumit
 ├── age  = 25
 └── sal  = 45000.0
```

Therefore deleting an instance variable from `e1` does not delete the corresponding variable from `e2`.

---

# 14. Guess the Output — Deleting Variables from Different Objects

Consider:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal


e1 = Emp("Amit", 24, 50000.0)
e2 = Emp("Sumit", 25, 45000.0)

print(e1.__dict__)
print(e2.__dict__)

del e1.sal
del e2.age

print()

print(e1.__dict__)
print(e2.__dict__)
```

### Before deletion

```text
e1:
{'name': 'Amit', 'age': 24, 'sal': 50000.0}

e2:
{'name': 'Sumit', 'age': 25, 'sal': 45000.0}
```

Then:

```python
del e1.sal
```

removes `sal` only from `e1`.

And:

```python
del e2.age
```

removes `age` only from `e2`.

### Output shown in the lecture

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
{'name': 'Sumit', 'age': 25, 'sal': 45000.0}

{'name': 'Amit', 'age': 24}
{'name': 'Sumit', 'sal': 45000.0}
```

---

# 15. Why Doesn't Deleting an Instance Variable Affect Another Object?

Because instance variables belong to individual objects.

For:

```python
e1 = Emp("Amit", 24, 50000.0)
e2 = Emp("Sumit", 25, 45000.0)
```

the objects have separate instance dictionaries.

Conceptually:

```text
e1.__dict__  → its own attributes

e2.__dict__  → its own attributes
```

Therefore:

```python
del e1.sal
```

does not affect:

```python
e2.sal
```

Similarly:

```python
del e2.age
```

does not affect:

```python
e1.age
```

---

# 16. Complete Deletion Summary

Python allows us to delete:

### A. An instance variable

```python
del e1.sal
```

### B. An instance variable from inside a method

```python
del self.sal
```

### C. An object reference

```python
del e1
```

### D. The local `self` reference

```python
del self
```

These operations are **not equivalent**.

---

# 17. Comparison Table

| Statement | What is removed? | Can the object still be accessed through another reference? |
|---|---|---|
| `del e1.sal` | `sal` attribute of `e1` | Yes |
| `del self.sal` | Current object's `sal` attribute | Yes |
| `del e1` | Name/reference `e1` | Yes, if another reference exists |
| `del self` | Local reference `self` | Yes, if another reference exists |

---

# 18. Important `__dict__` Connection

The lecture repeatedly uses:

```python
object.__dict__
```

to observe changes to instance variables.

For example:

```python
e1.__dict__
```

might initially be:

```python
{
    'name': 'Amit',
    'age': 24,
    'sal': 50000.0
}
```

After:

```python
del e1.sal
```

it becomes:

```python
{
    'name': 'Amit',
    'age': 24
}
```

This makes `__dict__` very useful for understanding:

- which instance variables currently exist
- when a variable is added
- when a variable is deleted
- whether two objects have the same instance variables

---

# 19. Full Concept Flow

The lecture's OOP progression can be remembered as:

```text
Create Object
     ↓
Create Instance Variables
     ↓
Access Instance Variables
     ↓
Modify Instance Variables
     ↓
Add More Instance Variables
     ↓
Inspect Using __dict__
     ↓
Delete Instance Variables
     ↓
Delete Object References
```

---

# 20. Exam-Oriented Questions

## Q1. How can an instance variable be deleted from inside a class?

Using:

```python
del self.variable_name
```

Example:

```python
def remove_salary(self):
    del self.salary
```

---

## Q2. How can an instance variable be deleted from outside the class?

Using:

```python
del object_reference.variable_name
```

Example:

```python
del e1.salary
```

---

## Q3. What happens after deleting an instance variable?

The attribute no longer exists for that object.

Trying to access it can result in:

```text
AttributeError
```

---

## Q4. What is the difference between `del e1.sal` and `del e1`?

```python
del e1.sal
```

removes only the `sal` attribute.

```python
del e1
```

removes the reference named `e1`.

---

## Q5. Does `del self` delete the object?

Not necessarily.

In the lecture's example, `del self` removes the local reference `self`, while the object remains accessible through `e1`.

---

## Q6. Why does `del self` not remove the object in the example?

Because another reference:

```python
e1
```

still points to the same object.

---

## Q7. Do all objects of the same class necessarily have exactly the same instance variables?

Not necessarily.

The lecture demonstrates that Python objects of the same class can have different numbers of instance variables because instance variables can be added dynamically.

For example:

```python
e1.setProject("Banking Info System")
```

adds `project` to `e1`, but if the same method is not called for `e2`, `e2` does not get that variable.

---

# 21. Important Output-Based Patterns

### Pattern 1 — Missing `self`

```python
print(age)
```

when `age` is an instance variable gives a `NameError`.

Correct:

```python
print(self.age)
```

---

### Pattern 2 — Deleted attribute

```python
del e1.salary
print(e1.salary)
```

The attribute no longer exists, so accessing it produces an `AttributeError`.

---

### Pattern 3 — Deleted reference

```python
del e1
print(e1)
```

The name `e1` is no longer defined, so using it produces a `NameError`.

---

### Pattern 4 — `del self`

```python
def remove(self):
    del self
```

This removes the local reference `self`; another reference such as `e1` can still access the object.

---

# 22. Quick Revision Table

| Concept | Syntax | Meaning |
|---|---|---|
| Access instance variable | `self.name` | Access current object's attribute |
| Add instance variable | `self.department = "IT"` | Create attribute |
| Add outside class | `e1.salary = 50000` | Create attribute through object |
| Add through dictionary | `e1.__dict__['department'] = 'IT'` | Add attribute through `__dict__` |
| Delete inside method | `del self.salary` | Remove current object's attribute |
| Delete outside class | `del e1.salary` | Remove object's attribute |
| Delete reference | `del e1` | Remove the name/reference |
| Delete local self reference | `del self` | Remove local `self` reference |

---

# 23. Final Memory Map

```text
                 INSTANCE VARIABLES
                         |
        +----------------+----------------+
        |                |                |
      CREATE           ACCESS           DELETE
        |                |                |
        |             self.x              |
        |                                 |
        +----------------+----------------+
        |                |                |
   __init__()       instance method   del self.x
   self.x = ...     self.x            del obj.x
   obj.x = ...                       __dict__
   obj.__dict__
```

And for references:

```text
del obj
  ↓
removes object reference/name

del self
  ↓
removes local self reference

Neither statement should be confused with:

del obj.variable
  ↓
removes one instance variable
```

---

# 24. Part 2 Coverage Checklist

- [x] Deleting instance variables
- [x] `del self.variable`
- [x] `del object.variable`
- [x] Boy / breakup example
- [x] `AttributeError` after deleting an attribute
- [x] Engineer / fired example
- [x] Deleting attributes from outside the class
- [x] `del e1`
- [x] `NameError` after deleting an object reference
- [x] Difference between deleting an attribute and deleting a reference
- [x] `del self`
- [x] Why `del self` does not remove the object in the demonstrated example
- [x] Separate instance variables for separate objects
- [x] Deleting `e1.sal` and `e2.age`
- [x] Effect of deletion on `__dict__`
- [x] Output-based questions
- [x] Exam questions
- [x] Quick revision table
- [x] Memory map

---

**End of Part 2**
# Lecture 32: Methods in Python — Part 3

> **Focus of Part 3:** Circle exercise and solution, complete integration of the lecture concepts, output-based revision, and exam-oriented practice.

---

# 1. Circle Class — Practical Exercise

The lecture gives an exercise to create a class named `Circle`.

The class should contain an instance variable:

```python
radius
```

and the following instance methods:

```text
__init__()
cal_area()
cal_circumference()
```

---

# 2. Requirements of the Circle Program

## `__init__()`

The constructor should initialize `radius` using the parameter passed during object creation.

Example:

```python
def __init__(self, radius):
    self.radius = radius
```

Here:

```text
radius       → parameter/local variable
self.radius  → instance variable
```

---

## `cal_area()`

This instance method should calculate and print the area of the circle.

Formula:

```text
Area = π × r²
```

In Python, the lecture uses:

```python
math.pi
```

and:

```python
math.pow(self.radius, 2)
```

---

## `cal_circumference()`

This instance method should calculate and print the circumference.

Formula:

```text
Circumference = 2πr
```

The lecture uses:

```python
math.tau * self.radius
```

where `math.tau` represents `2π`.

---

# 3. Complete Circle Solution

```python
import math

class Circle:

    def __init__(self, radius):
        self.radius = radius

    def cal_area(self):
        area = math.pi * math.pow(self.radius, 2)
        print("Area of circle is", area)

    def cal_circumference(self):
        circumf = math.tau * self.radius
        print("Circumference of circle is", circumf)


radius = int(input("Enter radius:"))

cobj = Circle(radius)

cobj.cal_area()
cobj.cal_circumference()
```

---

# 4. Understanding the Circle Program

## Step 1 — Import `math`

```python
import math
```

The program uses mathematical constants/functions from Python's `math` module.

---

## Step 2 — Create the class

```python
class Circle:
```

A class named `Circle` is created.

---

## Step 3 — Create the instance variable

```python
def __init__(self, radius):
    self.radius = radius
```

The value passed while creating the object is stored in:

```python
self.radius
```

So `radius` becomes an instance variable of the Circle object.

---

## Step 4 — Calculate area

```python
def cal_area(self):
    area = math.pi * math.pow(self.radius, 2)
    print("Area of circle is", area)
```

The formula used is:

```text
π × r²
```

For radius `10`:

```text
Area = π × 10²
     = π × 100
     ≈ 314.1592653589793
```

---

## Step 5 — Calculate circumference

```python
def cal_circumference(self):
    circumf = math.tau * self.radius
    print("Circumference of circle is", circumf)
```

Since:

```text
math.tau = 2π
```

the formula becomes:

```text
2πr
```

For radius `10`:

```text
Circumference = 2π × 10
              ≈ 62.83185307179586
```

---

## Step 6 — Take user input

```python
radius = int(input("Enter radius:"))
```

The user enters the radius.

---

## Step 7 — Create the object

```python
cobj = Circle(radius)
```

The entered radius is passed to:

```python
__init__()
```

and stored as:

```python
self.radius
```

---

## Step 8 — Call the methods

```python
cobj.cal_area()
cobj.cal_circumference()
```

The two instance methods calculate and display the results.

---

# 5. Circle Program Output

For:

```text
Enter radius:10
```

the lecture shows:

```text
Area of circle is 314.1592653589793
Circumference of circle is 62.83185307179586
```

---

# 6. Important Concept in the Circle Example

Notice that the input is taken **outside the class**:

```python
radius = int(input("Enter radius:"))
```

and then passed to the class:

```python
cobj = Circle(radius)
```

The class receives the value through:

```python
__init__(self, radius)
```

and stores it using:

```python
self.radius = radius
```

This clearly demonstrates the flow:

```text
User Input
    ↓
radius
    ↓
Circle(radius)
    ↓
__init__(self, radius)
    ↓
self.radius
    ↓
cal_area() / cal_circumference()
```

---

# 7. Complete Lecture Concept Map

The lecture connects several important OOP concepts.

```text
                         CLASS
                           |
             +-------------+-------------+
             |             |             |
           Data          Methods      __dict__
             |             |
     Instance Variables   |
             |             |
             |       +-----+-----+
             |       |     |     |
             |    Instance Class Static
             |     Method Method Method
             |       |     |     |
             |      self   cls   no automatic
             |                    self/cls
             |
       +-----+----------------------+
       |                            |
    Creation                     Deletion
       |                            |
  +----+----+                 +-----+------+
  |    |    |                 |            |
__init__ method obj ref    del self.x   del obj.x
       |                     |
     __dict__              delete attribute
```

---

# 8. Most Important `self` Concepts

`self` is central to the instance-method examples.

## `self` represents the current object

If:

```python
e1.show()
```

is called, then inside `show()`:

```python
self
```

refers to `e1`.

If:

```python
e2.show()
```

is called, then:

```python
self
```

refers to `e2`.

---

## `self` allows access to instance variables

```python
self.name
self.age
self.salary
```

Without `self`, Python does not automatically assume that:

```python
name
age
salary
```

are instance variables.

---

# 9. Most Important `__dict__` Concepts

`__dict__` provides a dictionary representation of the object's instance attributes.

Example:

```python
e1.__dict__
```

may produce:

```python
{
    'name': 'Amit',
    'age': 24,
    'sal': 50000.0
}
```

If an attribute is added:

```python
e1.department = "IT"
```

then:

```python
e1.__dict__
```

contains:

```python
{
    'name': 'Amit',
    'age': 24,
    'sal': 50000.0,
    'department': 'IT'
}
```

If it is deleted:

```python
del e1.department
```

the entry is removed.

---

# 10. Adding an Attribute Through `__dict__`

The lecture also demonstrates direct manipulation of the dictionary.

```python
e1.__dict__['department'] = 'IT'
```

After this:

```python
e1.department
```

can be accessed.

For example:

```python
class Emp:
    def __init__(self):
        self.name = "Amit"
        self.age = 24
        self.sal = 50000.0

    def show(self):
        print(self.name, self.age, self.sal, self.department)


e1 = Emp()

print(e1.__dict__)

e1.__dict__['department'] = 'IT'

print(e1.__dict__)

e1.show()
```

Output:

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
{'name': 'Amit', 'age': 24, 'sal': 50000.0, 'department': 'IT'}
Amit 24 50000.0 IT
```

---

# 11. Dynamic Instance Variables

One important observation from the lecture is that an object can acquire additional instance variables after it has already been created.

For example:

```python
e1 = Emp("Amit", 24, 30000.0)
```

may initially have:

```python
name
age
sal
```

Then:

```python
e1.setDept("Finance")
```

adds:

```python
department
```

Then:

```python
e1.setProject("Banking Info System")
```

adds:

```python
project
```

Then:

```python
e1.setBonus(20000.0)
```

adds:

```python
bonus
```

So the object's instance data can grow dynamically.

---

# 12. Same Class, Different Instance Variables

The lecture's employee example demonstrates:

```python
e1 = Emp("Amit", 24, 30000.0)
e2 = Emp("Sumit", 34, 45000.0)
```

Then:

```python
e1.setDept("Finance")
e1.setProject("Banking Info System")
e1.setBonus(20000.0)

e2.setDept("Production")
```

Therefore:

```text
e1 → name, age, sal, department, project, bonus

e2 → name, age, sal, department
```

The two objects belong to the same class but do not have exactly the same set of instance variables.

---

# 13. Output-Based Question — Predict the Dictionaries

Given:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

    def setDept(self, department):
        self.department = department

    def setProject(self, project):
        self.project = project

    def setBonus(self, bonus):
        self.bonus = bonus


e1 = Emp("Amit", 24, 30000.0)
e2 = Emp("Sumit", 34, 45000.0)

e1.setDept("Finance")
e1.setProject("Banking Info System")
e1.setBonus(20000.0)

e2.setDept("Production")

print(e1.__dict__)
print()
print(e2.__dict__)
```

### Answer

```text
{'name': 'Amit', 'age': 24, 'sal': 30000.0, 'department': 'Finance', 'project': 'Banking Info System', 'bonus': 20000.0}

{'name': 'Sumit', 'age': 34, 'sal': 45000.0, 'department': 'Production'}
```

### Key observation

`project` and `bonus` are not present in `e2`.

They were created only for `e1`.

---

# 14. Output-Based Question — Attribute Deletion

Given:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal


e1 = Emp("Amit", 24, 50000.0)
e2 = Emp("Sumit", 25, 45000.0)

print(e1.__dict__)
print(e2.__dict__)

del e1.sal
del e2.age

print()

print(e1.__dict__)
print(e2.__dict__)
```

### Answer

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
{'name': 'Sumit', 'age': 25, 'sal': 45000.0}

{'name': 'Amit', 'age': 24}
{'name': 'Sumit', 'sal': 45000.0}
```

### Why?

Because:

```python
del e1.sal
```

only changes `e1`.

And:

```python
del e2.age
```

only changes `e2`.

---

# 15. Output-Based Question — `del self`

Given:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

    def remove(self):
        del self


e1 = Emp("Amit", 24, 50000.0)

print(e1.__dict__)

e1.remove()

print(e1.__dict__)
```

### Answer

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
```

The local reference `self` is removed, but `e1` still refers to the object.

---

# 16. Output-Based Question — `del e1`

Given:

```python
class Emp:
    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal


e1 = Emp("Amit", 24, 50000.0)

print(e1.__dict__)

del e1

print(e1.__dict__)
```

### Answer

First:

```text
{'name': 'Amit', 'age': 24, 'sal': 50000.0}
```

Then:

```python
del e1
```

removes the reference `e1`.

The next use of `e1` produces:

```text
NameError: name 'e1' is not defined
```

---

# 17. Output-Based Question — Deleted Attribute

Given:

```python
class Boy:
    def __init__(self, name, girlfriend):
        self.name = name
        self.girlfriend = girlfriend

    def breakup(self):
        del self.girlfriend


b1 = Boy("Deepak", "Jyoti")

print(b1.__dict__)

b1.breakup()

print(b1.girlfriend)
```

### Answer

Initially:

```text
{'name': 'Deepak', 'girlfriend': 'Jyoti'}
```

After:

```python
b1.breakup()
```

the attribute:

```python
girlfriend
```

is removed.

Therefore:

```python
print(b1.girlfriend)
```

produces an:

```text
AttributeError
```

---

# 18. Three Important Errors to Remember

## `NameError`

Occurs when a name/reference does not exist.

Example:

```python
del e1
print(e1)
```

Result:

```text
NameError
```

---

## `AttributeError`

Occurs when an object does not have the requested attribute.

Example:

```python
del e1.salary
print(e1.salary)
```

Result:

```text
AttributeError
```

---

## Important distinction

```text
NameError
   ↓
Name/reference itself is unavailable

AttributeError
   ↓
Object exists, but requested attribute does not
```

---

# 19. Instance Method vs Class Method vs Static Method

The lecture identifies three method types.

## Instance Method

```python
class Emp:
    def show(self):
        pass
```

- Uses `self`
- Called using an object
- Works with instance data

Example:

```python
e1.show()
```

---

## Class Method

```python
class Emp:
    @classmethod
    def change_company(cls):
        pass
```

- Uses `cls`
- Decorated with `@classmethod`
- Called using the class name
- Works with class-level data

Example:

```python
Emp.change_company()
```

---

## Static Method

```python
class Emp:
    @staticmethod
    def utility():
        pass
```

- No automatic `self`
- No automatic `cls`
- Called using the class name
- Used for utility-style operations

Example:

```python
Emp.utility()
```

---

# 20. Final Comparison

| Concept | Instance Method | Class Method | Static Method |
|---|---|---|---|
| Main receiver | Object | Class | None |
| First automatic parameter | `self` | `cls` | None |
| Decorator | Not required | `@classmethod` | `@staticmethod` |
| Called using | Object | Class | Class |
| Main data | Instance data | Class data | Independent logic |
| Example | `e1.show()` | `Emp.set_company()` | `Emp.utility()` |

---

# 21. Most Important Exam Questions from the Lecture

### Q1. What are the three types of methods in Python?

1. Instance methods
2. Class methods
3. Static methods

---

### Q2. What is an instance method?

A method that can access and operate on the instance members of an object.

---

### Q3. What is the purpose of `self`?

`self` refers to the current object and is used to access its instance variables and methods.

---

### Q4. What is `__dict__`?

It is the dictionary associated with an object that stores its instance attributes and their values.

---

### Q5. How many ways are shown in the lecture to create instance variables?

Four:

1. Inside `__init__()` using `self`
2. Inside another instance method using `self`
3. Outside the class using the object reference
4. Using the instance's `__dict__`

---

### Q6. How can an instance variable be deleted?

Using either:

```python
del self.variable
```

inside an instance method, or:

```python
del object.variable
```

outside the class.

---

### Q7. What happens when `del object.variable` is executed?

That particular instance variable is removed from the object.

---

### Q8. What happens when `del object` is executed?

The reference/name is removed.

---

### Q9. Does `del self` necessarily delete the object?

No. In the demonstrated example, another reference (`e1`) still points to the object.

---

### Q10. Why can two objects of the same class have different instance variables?

Because instance variables can be created dynamically for individual objects.

---

# 22. Quick Revision Sheet

```text
METHOD
  ↓
Function defined inside a class

3 TYPES
  ↓
Instance → self
Class    → cls
Static   → no automatic self/cls

INSTANCE VARIABLE
  ↓
self.x

ACCESS
  ↓
self.x
obj.x

CREATE
  ↓
1. __init__() using self
2. Any instance method using self
3. Outside class using obj
4. Using obj.__dict__

VIEW
  ↓
obj.__dict__

DELETE ATTRIBUTE
  ↓
del self.x
del obj.x

DELETE REFERENCE
  ↓
del obj

DELETE LOCAL self REFERENCE
  ↓
del self

ERRORS
  ↓
NameError     → name/reference unavailable
AttributeError → attribute unavailable
```

---

# 23. Final Lecture Revision Map

```text
                         PYTHON OOP METHODS
                                  |
          +-----------------------+-----------------------+
          |                       |                       |
       INSTANCE                CLASS                  STATIC
        METHOD                 METHOD                 METHOD
          |                       |                       |
         self                    cls                no automatic
          |                       |                   self/cls
          |                       |
   object data              class data
          |
    +-----+-----------------------------+
    |                                   |
  ACCESS                              MODIFY
    |                                   |
 self.name                        self.salary = ...
 self.age
 self.sal
    |
    +----------------+
    |                |
 __dict__          methods
    |                |
 inspect data      setDept()
    |              setProject()
    |              setBonus()
    |
    +----------------+
    |
  DELETE
    |
 +--+----------------------+
 |                         |
del self.x              del obj.x
 |
delete attribute

del obj
 |
delete reference/name

del self
 |
delete local self reference
```

---

# 24. Complete Coverage Checklist

- [x] Types of methods
- [x] Instance methods
- [x] `self`
- [x] Accessing instance variables through `self`
- [x] Instance method employee example
- [x] Circle exercise
- [x] Circle solution
- [x] Circle output
- [x] `__dict__`
- [x] Adding instance variables through instance methods
- [x] Adding instance variables through object reference
- [x] Adding instance variables through `__dict__`
- [x] Different objects having different instance variables
- [x] Class methods
- [x] `cls`
- [x] Static methods
- [x] Deleting instance variables
- [x] `del self.variable`
- [x] `del object.variable`
- [x] Boy / `breakup()` example
- [x] Engineer / `fired()` example
- [x] `del e1`
- [x] `del self`
- [x] Deleting variables from different objects
- [x] `NameError`
- [x] `AttributeError`
- [x] Output-based revision
- [x] Exam questions
- [x] Final memory map

---

# 25. Final Takeaway

The most important ideas to remember from this lecture are:

```text
Instance Method
      ↓
uses self
      ↓
works with current object's data

__dict__
      ↓
shows object's instance attributes

Instance Variables
      ↓
can be created dynamically

Instance Variables
      ↓
can be deleted dynamically

del obj.variable
      ↓
deletes one attribute

del obj
      ↓
deletes the reference/name

del self
      ↓
deletes the local self reference,
not necessarily the object itself
```

**End of Part 3**
