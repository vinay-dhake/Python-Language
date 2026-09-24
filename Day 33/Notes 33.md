# Lecture 33: OOP in Python — Class Methods, Inheritance & `super()`

## Part 1 — Class Methods and Employee Exercise

This part covers class methods, `@classmethod`, `cls`, accessing class methods, and the complete `Emp` salary-increment exercise.

---

# 1. Lecture Overview

This lecture continues Object-Oriented Programming in Python.

The major ideas are:

1. Class methods
2. Creating class methods
3. Accessing class methods
4. The `@classmethod` decorator
5. The `cls` reference
6. Class variables and class-level data
7. Employee salary-increment exercise
8. Complete implementation using a class method

The later part of the lecture covers static methods, while the accompanying text also covers inheritance and `super()`.

---

# 2. Class Methods

Python allows classes to contain **class methods**, just as they can contain class variables.

A class method is a method that works on the **class as a whole**, rather than specifically on one object.

For example, if an `Emp` class contains:

```python
class Emp:
    raise_amount = 0
```

and we want a method to initialize or change `raise_amount`, a class method is appropriate.

---

# 3. Instance Method vs Class Method

## Instance Method

An instance method works with an individual object.

```python
class Emp:
    def display(self):
        print("Employee details")
```

The first parameter is conventionally:

```python
self
```

`self` represents the current object.

It can access:

```python
self.name
self.age
self.sal
```

## Class Method

A class method works with the class itself.

```python
class Emp:
    @classmethod
    def set_raise_amount(cls):
        pass
```

Here:

```text
self → current object
cls  → current class
```

---

# 4. Creating a Class Method

To create a class method, use:

```python
@classmethod
```

This is a **decorator** and is written immediately above the method definition.

### Syntax

```python
class <class_name>:

    @classmethod
    def <method_name>(cls):
        # class-specific code
        pass
```

Example:

```python
class Emp:

    @classmethod
    def show_class_info(cls):
        print("This is a class method")
```

---

# 5. What Does `@classmethod` Do?

The decorator tells Python that the method is a class method.

Python automatically supplies the class object as the first argument.

Therefore:

```python
@classmethod
def method_name(cls):
    ...
```

receives the class through:

```python
cls
```

This is similar to how Python supplies the current object as `self` to an instance method.

```text
Instance method → self → object
Class method    → cls  → class
```

---

# 6. Understanding `cls`

Python creates a special **class object** for every class.

For a class method, `cls` refers to that class object.

Example:

```python
class Emp:

    @classmethod
    def show(cls):
        print(cls)

Emp.show()
```

Here `cls` refers to the `Emp` class object.

---

# 7. Is `cls` a Keyword?

No.

`cls` is only a **convention**.

Another parameter name can technically be used:

```python
class Emp:

    @classmethod
    def show(x):
        print(x)
```

Python still passes the class reference to `x`.

However, the standard convention is:

```python
cls
```

Similarly:

```text
self → conventional instance reference
cls  → conventional class reference
```

---

# 8. Important Rules About Class Methods

### Rule 1 — Use `@classmethod`

```python
@classmethod
def method(cls):
    pass
```

### Rule 2 — First parameter receives the class

```python
cls
```

is automatically supplied by Python.

### Rule 3 — Class methods operate at class level

They are intended for operations involving class-level data.

For example:

```python
cls.raise_amount
```

can access a class variable.

### Rule 4 — They are not intended for one particular object's state

A class method is not meant to operate on:

```python
self.name
self.age
self.sal
```

for one particular employee.

---

# 9. Accessing a Class Method

The preferred way to call a class method is using the class name:

```python
ClassName.method_name()
```

Example:

```python
Emp.set_raise_amount()
```

The class name is followed by the dot operator.

---

# 10. Calling a Class Method Through an Object

Python also permits a class method to be called through an object:

```python
e1.set_raise_amount()
```

However, the lecture recommends **not doing this**.

The reason is that class methods operate on the class rather than on an individual object.

Therefore, prefer:

```python
Emp.set_raise_amount()
```

because it clearly communicates that the operation is class-level.

---

# 11. `self` vs `cls`

| Feature | `self` | `cls` |
|---|---|---|
| Used with | Instance method | Class method |
| Represents | Current object | Class object |
| Main data | Instance data | Class-level data |
| Automatically supplied | Yes | Yes |
| Conventional name | `self` | `cls` |

### Memory trick

```text
self → object
cls  → class
```

---

# 12. Employee Exercise

The lecture gives an employee exercise.

Create:

```python
class Emp:
    ...
```

The class must contain:

### Instance variables

```text
name
age
sal
```

### Class variable

```python
raise_amount
```

`raise_amount` stores the percentage increment to be applied to employee salaries.

---

# 13. Required Methods

The exercise requires:

### `__init__()`

Initializes:

```text
name
age
sal
```

using the parameters supplied while creating an object.

### `increase_sal()`

Calculates the salary increment and adds it to `sal`.

### `display()`

Displays the employee's:

```text
name
age
sal
```

The solution also uses:

### `set_raise_amount()`

A class method that obtains the raise percentage and stores it in the class variable.

---

# 14. Employee Class Variable

Start with:

```python
class Emp:
    raise_amount = 0
```

`raise_amount` is a **class variable**.

It represents the salary increment percentage at class level.

---

# 15. Creating `set_raise_amount()`

The solution defines:

```python
@classmethod
def set_raise_amount(cls):
    cls.raise_amount = float(
        input("Enter raise percentage:")
    )
```

### Breakdown

```python
@classmethod
```

Makes the method a class method.

```python
cls
```

Receives the class reference.

```python
input("Enter raise percentage:")
```

Gets the value from the user.

```python
float(...)
```

Converts the input to a floating-point number.

```python
cls.raise_amount = ...
```

stores the value in the class variable.

---

# 16. Employee Constructor

```python
def __init__(self, name, age, sal):
    self.name = name
    self.age = age
    self.sal = sal
```

The parameters:

```text
name
age
sal
```

are stored as instance variables:

```python
self.name
self.age
self.sal
```

Each employee object therefore has its own employee details.

---

# 17. `increase_sal()` Method

The solution uses:

```python
def increase_sal(self):
    self.sal = self.sal + (
        self.sal * Emp.raise_amount / 100
    )
```

The formula is:

```text
increment = current salary × raise percentage / 100

new salary = current salary + increment
```

---

# 18. Salary Calculation Example

Suppose:

```text
Salary = 50000
Raise = 8.5%
```

Then:

```text
Increment = 50000 × 8.5 / 100
          = 4250
```

Therefore:

```text
New salary = 50000 + 4250
           = 54250
```

For:

```text
Salary = 45000
Raise = 8.5%
```

we get:

```text
Increment = 45000 × 8.5 / 100
          = 3825

New salary = 45000 + 3825
           = 48825
```

---

# 19. `display()` Method

```python
def display(self):
    print(self.name, self.age, self.sal)
```

This is an **instance method** because it uses:

```python
self.name
self.age
self.sal
```

These values belong to the individual employee object.

---

# 20. Complete Employee Program

```python
class Emp:

    raise_amount = 0

    @classmethod
    def set_raise_amount(cls):
        cls.raise_amount = float(
            input("Enter raise percentage:")
        )

    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

    def increase_sal(self):
        self.sal = self.sal + (
            self.sal * Emp.raise_amount / 100
        )

    def display(self):
        print(self.name, self.age, self.sal)


Emp.set_raise_amount()

e1 = Emp("Amit", 24, 50000.0)
e2 = Emp("Sumit", 26, 45000.0)

print("Before incrementing:")
print("_____________________")

e1.display()
e2.display()

e1.increase_sal()
e2.increase_sal()

print()

print(
    "After incrementing by",
    Emp.raise_amount,
    "percent:"
)

print("__________________________________")

e1.display()
e2.display()
```

---

# 21. Program Execution Flow

```text
Start
  ↓
Create Emp class
  ↓
raise_amount = 0
  ↓
Emp.set_raise_amount()
  ↓
User enters percentage
  ↓
Class variable updated
  ↓
Create e1
  ↓
Create e2
  ↓
Display original salaries
  ↓
Increase e1 salary
  ↓
Increase e2 salary
  ↓
Display updated salaries
```

---

# 22. Sample Output

The lecture shows an example with an `8.5` percent raise:

```text
Enter raise percentage: 8.5

Before incrementing:

Amit 24 50000.0
Sumit 26 45000.0

After incrementing by 8.5 percent:

Amit 24 54250.0
Sumit 26 48825.0
```

---

# 23. Why Is `set_raise_amount()` a Class Method?

The method changes:

```python
raise_amount
```

which is a class variable.

The value represents the salary increment percentage at the class level.

Therefore the operation logically belongs to the **class**, rather than one particular employee object.

This is why:

```python
@classmethod
def set_raise_amount(cls):
```

is used.

---

# 24. Class Variable vs Instance Variables

The `Emp` example contains both.

### Class variable

```python
raise_amount = 0
```

### Instance variables

```python
self.name
self.age
self.sal
```

Conceptually:

```text
                  Emp Class
                     |
             raise_amount = 8.5
                     |
          +----------+----------+
          |                     |
         e1                    e2
          |                     |
   name = Amit            name = Sumit
   age  = 24              age  = 26
   sal  = 54250.0         sal  = 48825.0
```

---

# 25. `cls.raise_amount` vs `Emp.raise_amount`

Inside a class method, the class variable can be accessed through:

```python
cls.raise_amount
```

The solution also accesses it from another method using:

```python
Emp.raise_amount
```

Example:

```python
def increase_sal(self):
    self.sal = self.sal + (
        self.sal * Emp.raise_amount / 100
    )
```

Both expressions refer to the class-level raise percentage in their respective contexts.

---

# 26. Important Exam Questions

### Q1. What is a class method?

A method that works on the class as a whole rather than specifically on one object.

### Q2. Which decorator creates a class method?

```python
@classmethod
```

### Q3. What is the first parameter of a class method?

Conventionally:

```python
cls
```

### Q4. What does `cls` represent?

The class object.

### Q5. Is `cls` a keyword?

No. It is a convention.

### Q6. Can a class method be called using an object?

Yes, but the lecture recommends using the class name.

### Q7. Why is `set_raise_amount()` a class method?

Because it modifies the class-level variable:

```python
raise_amount
```

### Q8. Difference between `self` and `cls`?

```text
self → current object
cls  → current class
```

---

# 27. Quick Revision Table

| Feature | Instance Method | Class Method |
|---|---|---|
| First parameter | `self` | `cls` |
| Represents | Current object | Class object |
| Main purpose | Object-specific behavior | Class-level operation |
| Decorator | Not required | `@classmethod` |
| Instance data | Can access | Not directly |
| Class data | Can access | Can access |
| Preferred call | Object | Class |
| Example | `e1.display()` | `Emp.set_raise_amount()` |

---

# 28. Memory Map

```text
                 CLASS METHOD
                      |
                @classmethod
                      |
                     cls
                      |
              class object reference
                      |
              +-------+-------+
              |               |
       class variable     class operation
              |
       raise_amount
              |
     set_raise_amount()
              |
       Emp.set_raise_amount()
```

---

# 29. Part 1 Coverage Checklist

- [x] Class methods
- [x] Class-level operations
- [x] Creating class methods
- [x] `@classmethod`
- [x] Decorator concept
- [x] `cls`
- [x] Class object
- [x] `cls` as a convention
- [x] Accessing class methods
- [x] Calling using class name
- [x] Calling using object reference
- [x] Why class name is preferred
- [x] Employee exercise
- [x] `raise_amount`
- [x] `name`, `age`, `sal`
- [x] `__init__()`
- [x] `set_raise_amount()`
- [x] `increase_sal()`
- [x] `display()`
- [x] Salary formula
- [x] Complete program
- [x] Sample output
- [x] `self` vs `cls`
- [x] Exam questions
- [x] Quick revision
- [x] Memory map

---
 OOP in Python — Static Methods

## 1. Static Methods

Static methods are the third type of method that a Python class can contain.

The three major method types are:

1. Instance methods
2. Class methods
3. Static methods

A static method is associated with a class, but it does not receive an object reference or a class reference automatically.

---

## 2. Main Characteristics of Static Methods

A static method:

- Is defined inside a class.
- Is created using the `@staticmethod` decorator.
- Does not automatically receive `self`.
- Does not automatically receive `cls`.
- Does not require an object to be called.
- Can be called using the class name.
- Generally performs a self-contained operation based on the arguments supplied to it.

Example:

```python
class MyMath:

    @staticmethod
    def add_nos(a, b):
        return a + b
```

Calling it:

```python
MyMath.add_nos(10, 20)
```

No object is required.

---

# 3. Class Method vs Static Method

The important difference is what Python automatically provides to the method.

## Class Method

A class method receives:

```python
cls
```

automatically.

Example:

```python
class Emp:

    @classmethod
    def show(cls):
        print(cls)
```

Here `cls` refers to the class object.

---

## Static Method

A static method receives **no implicit reference**.

Example:

```python
class MyMath:

    @staticmethod
    def add_nos(a, b):
        return a + b
```

Python does not automatically add:

```text
self
```

or:

```text
cls
```

The method works only with the arguments explicitly passed to it.

---

# 4. Key Difference

```text
Class Method
     ↓
@classmethod
     ↓
cls is automatically passed
     ↓
Works with class-level information


Static Method
     ↓
@staticmethod
     ↓
No self or cls is automatically passed
     ↓
Works with explicitly supplied arguments
```

---

# 5. Creating a Static Method

To create a static method, use:

```python
@staticmethod
```

above the method definition.

### Syntax

```python
class <class_name>:

    @staticmethod
    def <method_name>(<arg_list>):
        # argument-specific code
        pass
```

Example:

```python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b
```

---

# 6. Why Is `@staticmethod` Called a Decorator?

`@staticmethod` tells Python that the method should behave as a static method.

It prevents Python from automatically passing:

```text
self
```

when the method is accessed through an object.

It also means that the method does not automatically receive:

```text
cls
```

when called using the class.

Therefore:

```python
@staticmethod
def add(a, b):
```

means the method expects exactly the explicitly supplied arguments:

```python
a
b
```

---

# 7. Example — `MyMath`

The lecture provides a mathematical utility class.

```python
class MyMath:

    @staticmethod
    def add_nos(a, b):
        c = a + b
        return c

    @staticmethod
    def mult_nos(a, b):
        c = a * b
        return c

print("Sum of 10 and 20 is", MyMath.add_nos(10, 20))
print("Product of 10 and 20 is", MyMath.mult_nos(10, 20))
```

---

# 8. Understanding `add_nos()`

The method is:

```python
@staticmethod
def add_nos(a, b):
    c = a + b
    return c
```

There is no:

```python
self
```

and no:

```python
cls
```

The method receives only:

```python
a
b
```

because those are the arguments explicitly supplied by the caller.

The call is:

```python
MyMath.add_nos(10, 20)
```

Therefore:

```text
a = 10
b = 20
```

and:

```python
c = a + b
```

becomes:

```python
c = 10 + 20
```

So the result is:

```text
30
```

---

# 9. Understanding `mult_nos()`

The second method is:

```python
@staticmethod
def mult_nos(a, b):
    c = a * b
    return c
```

Calling:

```python
MyMath.mult_nos(10, 20)
```

gives:

```text
a = 10
b = 20
```

Therefore:

```text
c = 10 × 20
c = 200
```

---

# 10. Output of the `MyMath` Example

The program:

```python
class MyMath:

    @staticmethod
    def add_nos(a, b):
        c = a + b
        return c

    @staticmethod
    def mult_nos(a, b):
        c = a * b
        return c


print("Sum of 10 and 20 is", MyMath.add_nos(10, 20))
print("Product of 10 and 20 is", MyMath.mult_nos(10, 20))
```

produces:

```text
Sum of 10 and 20 is 30
Product of 10 and 20 is 200
```

---

# 11. Static Method Does Not Automatically Receive `cls`

Consider:

```python
class MyMath:

    @staticmethod
    def add(a, b):
        return a + b
```

There is no:

```python
cls
```

parameter.

Therefore the method does not automatically know about the class.

It simply receives:

```python
a
b
```

and performs its operation.

---

# 12. Can a Static Method Access Class Data?

The lecture points out an important detail:

A static method can access class data **using the class name**.

For example:

```python
class Emp:

    raise_amount = 0

    @staticmethod
    def set_raise_amount():
        Emp.raise_amount = float(
            input("Enter raise percentage:")
        )
```

Notice that the method does not have:

```python
cls
```

So it cannot use:

```python
cls.raise_amount
```

Instead, it uses:

```python
Emp.raise_amount
```

through the class name.

---

# 13. Static Version of `set_raise_amount()`

The employee method can therefore be written as:

```python
class Emp:

    raise_amount = 0

    @staticmethod
    def set_raise_amount():
        Emp.raise_amount = float(
            input("Enter raise percentage:")
        )
```

Calling:

```python
Emp.set_raise_amount()
```

executes the method.

The user enters the percentage, and the value is stored in:

```python
Emp.raise_amount
```

---

# 14. Why Doesn't the Static Method Use `cls`?

Because a static method does not automatically receive the class object.

For example:

```python
@staticmethod
def set_raise_amount():
```

has no:

```python
cls
```

parameter.

Therefore, to access the class variable, the method explicitly uses:

```python
Emp.raise_amount
```

This is an important difference between class methods and static methods.

---

# 15. Class Method vs Static Method — Employee Example

## Class method version

```python
class Emp:

    raise_amount = 0

    @classmethod
    def set_raise_amount(cls):
        cls.raise_amount = float(
            input("Enter raise percentage:")
        )
```

Here:

```python
cls.raise_amount
```

can be used because Python automatically provides the class reference.

---

## Static method version

```python
class Emp:

    raise_amount = 0

    @staticmethod
    def set_raise_amount():
        Emp.raise_amount = float(
            input("Enter raise percentage:")
        )
```

Here:

```python
Emp.raise_amount
```

is used because Python does not provide `cls`.

---

# 16. Important Point About Omitting `@staticmethod`

The lecture presents an important behavior concerning a method written without:

```python
@staticmethod
```

Consider:

```python
class Demo:

    def display():
        print("Inside display")
```

There is no:

```python
self
```

parameter.

What happens depends on how the method is called.

---

# 17. Case 1 — Calling Without `@staticmethod` Using an Object

Consider:

```python
class Demo:

    def display():
        print("Inside display")


d = Demo()
d.display()
```

At first glance, it may look as though:

```python
display()
```

does not need any argument.

However, because `display` was not declared with:

```python
@staticmethod
```

and it is called using:

```python
d.display()
```

Python treats it as an instance method.

Python automatically passes the object reference as the first argument.

Conceptually:

```text
d.display()
     ↓
display(d)
```

But the method definition is:

```python
def display():
```

which accepts zero arguments.

Python therefore passes one argument while the method accepts zero.

---

# 18. Output of Case 1

Code:

```python
class Demo:

    def display():
        print("Inside display")


d = Demo()
d.display()
```

The lecture shows a `TypeError` similar to:

```text
TypeError: display() takes 0 positional arguments but 1 was given
```

### Why?

Because:

```text
Method expects → 0 arguments
Python passes  → 1 argument
```

The automatically supplied argument is the object reference.

---

# 19. Case 2 — Calling the Same Method Using the Class Name

Consider:

```python
class Demo:

    def display():
        print("Inside display")


Demo.display()
```

Here the method is accessed using the class name.

The lecture shows:

```text
Inside display
```

### Why does it work?

Because calling:

```python
Demo.display()
```

does not automatically provide an object as the first argument.

Therefore the method:

```python
def display():
```

receives zero arguments, exactly as it expects.

---

# 20. Important Observation

Without explicitly using:

```python
@staticmethod
```

the same method can behave differently depending on how it is accessed.

### Through an object

```python
d.display()
```

Python treats it as an instance-method-style call and supplies the object.

### Through the class

```python
Demo.display()
```

No object is supplied automatically.

This explains the two different results.

---

# 21. Case 3 — `display(self)` Called Through the Class

Now consider:

```python
class Demo:

    def display(self):
        print("Inside display")


Demo.display()
```

The method is written with one required parameter:

```python
self
```

but the call:

```python
Demo.display()
```

does not provide an argument.

Therefore Python raises a `TypeError`.

The lecture's output is:

```text
TypeError: display() missing 1 required positional argument: 'self'
```

---

# 22. Why Does This Happen?

When using the class name directly:

```python
Demo.display()
```

Python does not automatically supply an object as `self`.

Therefore:

```python
def display(self):
```

is waiting for one argument.

But:

```python
Demo.display()
```

supplies none.

So:

```text
Required → 1 argument (`self`)
Provided → 0 arguments
```

Result:

```text
TypeError
```

---

# 23. Case 4 — Manually Supplying the Argument

Consider:

```python
class Demo:

    def display(self):
        print(self)


Demo.display("Inside display")
```

Here the string:

```python
"Inside display"
```

is explicitly supplied as the first argument.

Therefore Python binds:

```python
self = "Inside display"
```

Then:

```python
print(self)
```

prints:

```text
Inside display
```

The lecture uses this example to demonstrate that when the class name is used directly, a method can be called like an ordinary function by explicitly supplying its arguments.

---

# 24. Why Is This Called Static-Method-Like Behavior?

The lecture explains that when:

```python
Demo.display(...)
```

is used, Python does not automatically pass an object.

Therefore the method can be supplied with the required argument manually.

However, this should not be confused with the proper declaration of a static method.

The proper and clear way to declare a static method is:

```python
@staticmethod
def display(...):
```

---

# 25. Case 5 — Calling a Normal Instance Method Through an Object

Consider:

```python
class Demo:

    def display(self):
        print("Inside display")


D = Demo()
D.display()
```

Here the call is made through an object:

```python
D.display()
```

Python automatically passes the object reference as the first argument.

Conceptually:

```text
D.display()
     ↓
display(D)
```

Therefore:

```python
self
```

receives the address/reference of `D`.

The method executes successfully.

Output:

```text
Inside display
```

---

# 26. Important Comparison of the Four `Demo` Examples

## Example 1

```python
class Demo:
    def display():
        print("Inside display")

d = Demo()
d.display()
```

Result:

```text
TypeError
```

Reason:

```text
Python automatically passes d,
but display() accepts no parameter.
```

---

## Example 2

```python
class Demo:
    def display():
        print("Inside display")

Demo.display()
```

Result:

```text
Inside display
```

Reason:

```text
No object is automatically passed.
```

---

## Example 3

```python
class Demo:
    def display(self):
        print("Inside display")

Demo.display()
```

Result:

```text
TypeError
```

Reason:

```text
self is required,
but no argument was supplied.
```

---

## Example 4

```python
class Demo:
    def display(self):
        print(self)

Demo.display("Inside display")
```

Result:

```text
Inside display
```

Reason:

```text
The argument was supplied manually,
so self receives "Inside display".
```

---

## Example 5

```python
class Demo:
    def display(self):
        print("Inside display")

D = Demo()
D.display()
```

Result:

```text
Inside display
```

Reason:

```text
Python automatically passes D as self.
```

---

# 27. Why Use `@staticmethod` Instead of Relying on This Behavior?

Although a method without `@staticmethod` can be called through the class, explicitly using:

```python
@staticmethod
```

makes the programmer's intention clear.

Example:

```python
class MyMath:

    @staticmethod
    def add(a, b):
        return a + b
```

Now it is immediately clear that:

- no object is required
- no `self` is required
- no `cls` is required
- the method operates on its supplied arguments

---

# 28. When Should Each Type of Method Be Used?

Choosing the method type depends on what the method needs to work with.

---

## Instance Methods

Instance methods are the **most common** type.

Use an instance method when the operation needs data or properties belonging to a particular object.

Example:

```python
class Emp:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print(self.name, self.salary)
```

Call:

```python
e1.display()
```

The method operates on `e1`.

### Main idea

```text
Need object-specific data?
        ↓
Use instance method
```

---

# 29. Class Methods

Use a class method when the operation needs to work with class-level information.

Example:

```python
class Emp:

    raise_amount = 0

    @classmethod
    def set_raise_amount(cls, amount):
        cls.raise_amount = amount
```

Call:

```python
Emp.set_raise_amount(10)
```

### Main idea

```text
Need class-level data or class-level operation?
        ↓
Use class method
```

---

# 30. Static Methods

Use a static method when the operation is self-contained and does not need automatic access to either:

```text
self
```

or:

```text
cls
```

Example:

```python
class MyMath:

    @staticmethod
    def add(a, b):
        return a + b
```

Call:

```python
MyMath.add(10, 20)
```

### Main idea

```text
Need neither object nor class reference?
        ↓
Use static method
```

---

# 31. Method Selection Memory Trick

```text
INSTANCE METHOD
      ↓
Need object?
      ↓
Use self


CLASS METHOD
      ↓
Need class?
      ↓
Use cls


STATIC METHOD
      ↓
Need neither?
      ↓
Use explicit arguments only
```

---

# 32. Complete Comparison

| Feature | Instance Method | Class Method | Static Method |
|---|---|---|---|
| Uses `self` | Yes | No | No |
| Uses `cls` | No | Yes | No |
| Access instance variables | Yes | No | No |
| Access class variables | Yes | Yes | Yes, using class name |
| Automatic object reference | Yes | No | No |
| Automatic class reference | No | Yes | No |
| Decorator required | No | `@classmethod` | `@staticmethod` |
| Main purpose | Object behavior | Class-level operations | Utility functions |
| Preferred call | Object | Class | Class |
| Example | `e1.display()` | `Emp.set_raise_amount()` | `MyMath.add_nos(10, 20)` |

---

# 33. Important Difference: Static Method and Class Data

A static method does not automatically receive the class.

Therefore:

```python
@staticmethod
def method():
    print(cls)
```

will not work because `cls` is not automatically defined.

But the method can explicitly use the class name:

```python
@staticmethod
def method():
    print(Emp.raise_amount)
```

So:

```text
Static method
     ↓
No automatic cls
     ↓
Use ClassName.attribute if class data is required
```

---

# 34. Important Difference: Static Method and Instance Data

Similarly, a static method does not automatically receive:

```python
self
```

Therefore it cannot directly do:

```python
self.name
```

unless an object is explicitly passed as an argument.

For example:

```python
class Demo:

    @staticmethod
    def show(obj):
        print(obj.name)
```

Here `obj` is explicitly supplied by the caller.

```python
d = Demo()
d.name = "Amit"

Demo.show(d)
```

The method can then access:

```python
obj.name
```

because the object was explicitly passed.

---

# 35. Exam-Oriented Questions

## Q1. What is a static method?

A static method is a method declared using `@staticmethod` that does not automatically receive an object or class reference.

---

## Q2. Which decorator is used for static methods?

```python
@staticmethod
```

---

## Q3. Does a static method receive `self` automatically?

No.

---

## Q4. Does a static method receive `cls` automatically?

No.

---

## Q5. How is a static method called?

Usually through the class name:

```python
ClassName.method()
```

---

## Q6. Can a static method access class variables?

Yes, using the class name.

Example:

```python
Emp.raise_amount
```

---

## Q7. What happens when a method without `@staticmethod` is called through an object?

Python treats the access as an instance-method-style call and automatically supplies the object as the first argument.

---

## Q8. What happens if the method does not have a parameter to receive that object?

A `TypeError` occurs.

---

## Q9. What happens when a method with no parameters is called using the class name?

No object is automatically supplied, so the method can execute if it requires no arguments.

---

## Q10. Why should `@staticmethod` be used?

It clearly declares that the method is independent of automatic instance/class binding.

---

# 36. Quick Revision

```text
@staticmethod
      ↓
Static method
      ↓
No automatic self
      ↓
No automatic cls
      ↓
Works with explicit arguments
      ↓
Can be called using class name
```

---

# 37. Final Method Map

```text
                    METHODS
                       |
        +--------------+--------------+
        |              |              |
    INSTANCE         CLASS          STATIC
      METHOD         METHOD          METHOD
        |              |              |
      self            cls          no automatic
        |              |             reference
        |              |
   object data     class data
        |              |
   e1.display()   Emp.set_raise_amount()
                       |
                @classmethod

Static example:
MyMath.add_nos(10, 20)
        |
   @staticmethod
        |
   explicit arguments
```

---

# 38. Final Takeaways

Remember these three rules:

### Rule 1

```python
def method(self):
```

is used for an instance method when the method needs the current object.

### Rule 2

```python
@classmethod
def method(cls):
```

is used when the method needs the class.

### Rule 3

```python
@staticmethod
def method(args):
```

is used when the method does not need an automatically supplied object or class reference.

The simplest memory rule is:

```text
Object → self
Class  → cls
Neither → static method
```

---

# 39. Part 2 Coverage Checklist

- [x] Static methods
- [x] Purpose of static methods
- [x] `@staticmethod`
- [x] Static-method syntax
- [x] Difference between class and static methods
- [x] No automatic `self`
- [x] No automatic `cls`
- [x] `MyMath` example
- [x] `add_nos()`
- [x] `mult_nos()`
- [x] Output of the mathematical example
- [x] Static method accessing class data through class name
- [x] Static version of `set_raise_amount()`
- [x] Why `cls` is not available automatically in a static method
- [x] Behavior when `@staticmethod` is omitted
- [x] `Demo.display()` examples
- [x] Object-call `TypeError` example
- [x] Class-call example
- [x] Missing `self` example
- [x] Manually supplying the first argument
- [x] Normal instance-method call
- [x] When to use instance methods
- [x] When to use class methods
- [x] When to use static methods
- [x] Complete comparison table
- [x] Exam questions
- [x] Quick revision
- [x] Final method map

OOP in Python — Inheritance and `super()`

# 1. Inheritance

**Inheritance** is an OOP mechanism in which a new class is created from an existing class.

The existing class is commonly called the:

- Parent class
- Base class
- Superclass

The new class is commonly called the:

- Child class
- Derived class
- Subclass

The child class can use the members inherited from the parent class and can also define its own additional members.

---

# 2. Parent Class and Child Class

Consider:

```python
class Rectangle:
    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth
```

Here:

```text
Rectangle
```

is the parent/base class.

Now create:

```python
class Cuboid(Rectangle):
    ...
```

Here:

```text
Cuboid
```

is the child/derived class.

The relationship can be represented as:

```text
Rectangle
    |
    | inheritance
    ↓
Cuboid
```

The `Cuboid` class inherits the members provided by `Rectangle`.

---

# 3. Why Is Inheritance Useful?

Inheritance allows a child class to reuse functionality already defined in a parent class.

For example:

```text
Rectangle
 ├── length
 └── breadth

Cuboid
 ├── inherited length
 ├── inherited breadth
 └── height
```

A cuboid can therefore use the length and breadth initialized by the parent class while adding its own `height`.

This avoids unnecessarily repeating the same initialization code.

---

# 4. Constructor Chaining

When a child class defines its own `__init__()` method, the parent class constructor does not automatically have to be called by simply defining the child constructor.

If the child needs the parent class's initialization logic, it should explicitly invoke the parent constructor.

This is called **constructor chaining**.

Consider:

```python
class Rectangle:
    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth
```

The child class adds:

```python
height
```

Therefore its constructor needs to initialize:

```text
length
breadth
height
```

The parent class already contains the logic for:

```text
length
breadth
```

So the child can delegate that work to the parent constructor.

---

# 5. Calling the Parent Constructor Using the Parent Class Name

One way to call the parent constructor is:

```python
ParentClass.__init__(self, ...)
```

For the `Rectangle` and `Cuboid` example:

```python
class Rectangle:
    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):
    def __init__(self, length, breadth, height):
        Rectangle.__init__(self, length, breadth)
        self.height = height
```

The statement:

```python
Rectangle.__init__(self, length, breadth)
```

explicitly calls the parent class's constructor.

---

# 6. Why Must `self` Be Passed Explicitly?

Notice:

```python
Rectangle.__init__(self, length, breadth)
```

The first argument is:

```python
self
```

This is required because we are directly calling the parent class method through the class name.

The parent constructor is defined as:

```python
def __init__(self, length, breadth):
```

When invoked directly in this way, the current child object must be explicitly supplied as the first argument.

Conceptually:

```text
Current Cuboid object
        ↓
       self
        ↓
Rectangle.__init__(self, length, breadth)
```

The parent constructor then initializes:

```python
self.length
self.breadth
```

on the same `Cuboid` object.

---

# 7. Complete `Rectangle` and `Cuboid` Example

```python
class Rectangle:
    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):
    def __init__(self, length, breadth, height):
        Rectangle.__init__(self, length, breadth)
        self.height = height

    def volume(self):
        return self.length * self.breadth * self.height


c1 = Cuboid(10, 5, 4)

print("Cuboid Volume:", c1.volume())
```

---

# 8. Understanding the Example Step by Step

## Step 1 — Create the `Cuboid` object

```python
c1 = Cuboid(10, 5, 4)
```

The arguments are:

```text
length = 10
breadth = 5
height = 4
```

---

## Step 2 — Child constructor executes

The child constructor is:

```python
def __init__(self, length, breadth, height):
```

It receives:

```text
10
5
4
```

---

## Step 3 — Parent constructor is called

```python
Rectangle.__init__(self, length, breadth)
```

This initializes:

```python
self.length = 10
self.breadth = 5
```

---

## Step 4 — Child-specific data is initialized

The child constructor then executes:

```python
self.height = height
```

Therefore the object contains:

```text
length  = 10
breadth = 5
height  = 4
```

---

## Step 5 — Calculate volume

The method:

```python
def volume(self):
    return self.length * self.breadth * self.height
```

calculates:

```text
10 × 5 × 4
= 200
```

Output:

```text
Cuboid Volume: 200
```

---

# 9. Problem with Direct Parent-Class Calls

Calling the parent constructor using:

```python
Rectangle.__init__(self, length, breadth)
```

works, but it has some disadvantages.

---

## Disadvantage 1 — `self` Must Be Passed Manually

The child must explicitly write:

```python
self
```

Example:

```python
Rectangle.__init__(self, length, breadth)
```

If `self` is omitted:

```python
Rectangle.__init__(length, breadth)
```

the arguments no longer match what the parent constructor expects.

This results in a `TypeError`.

### Correct

```python
Rectangle.__init__(self, length, breadth)
```

### Incorrect

```python
Rectangle.__init__(length, breadth)
```

---

# 10. Disadvantage 2 — Tight Coupling to the Parent Class Name

Suppose the parent class is:

```python
class Rectangle:
```

and the child contains:

```python
Rectangle.__init__(self, length, breadth)
```

The child code directly depends on the name:

```text
Rectangle
```

If the parent class is renamed, the direct references inside child classes also have to be changed.

For example, if:

```python
Rectangle
```

is renamed to:

```python
Shape
```

then:

```python
Rectangle.__init__(self, length, breadth)
```

would also need to be changed.

This creates tighter coupling between the child and the specific parent class name.

---

# 11. `super()`

Python provides:

```python
super()
```

to delegate operations to the parent class according to Python's inheritance mechanism.

Instead of writing:

```python
Rectangle.__init__(self, length, breadth)
```

we can write:

```python
super().__init__(length, breadth)
```

This is the preferred approach for the parent-constructor example.

---

# 12. Calling the Parent Constructor Using `super()`

The same example can be written as:

```python
class Rectangle:
    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):
    def __init__(self, length, breadth, height):
        super().__init__(length, breadth)
        self.height = height

    def volume(self):
        return self.length * self.breadth * self.height


c2 = Cuboid(12, 6, 3)

print("Cuboid Volume:", c2.volume())
```

---

# 13. Understanding `super().__init__()`

The statement:

```python
super().__init__(length, breadth)
```

calls the appropriate parent implementation of `__init__()`.

Unlike:

```python
Rectangle.__init__(self, length, breadth)
```

the current object does not have to be supplied explicitly.

The object reference is handled automatically.

Therefore:

```text
Direct parent call:
Rectangle.__init__(self, length, breadth)

Using super():
super().__init__(length, breadth)
```

---

# 14. Step-by-Step `super()` Example

Consider:

```python
class Rectangle:
    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):
    def __init__(self, length, breadth, height):
        super().__init__(length, breadth)
        self.height = height
```

Now:

```python
c2 = Cuboid(12, 6, 3)
```

### Step 1

Child constructor receives:

```text
length = 12
breadth = 6
height = 3
```

### Step 2

This executes:

```python
super().__init__(length, breadth)
```

The parent constructor initializes:

```python
self.length = 12
self.breadth = 6
```

### Step 3

The child constructor initializes:

```python
self.height = 3
```

The final object contains:

```text
length  = 12
breadth = 6
height  = 3
```

### Step 4

Volume:

```text
12 × 6 × 3
= 216
```

Output:

```text
Cuboid Volume: 216
```

---

# 15. Direct Parent Call vs `super()`

| Feature | Parent class name | `super()` |
|---|---|---|
| Example | `Rectangle.__init__(self, ...)` | `super().__init__(...)` |
| Pass `self` explicitly | Yes | No |
| Parent class name written directly | Yes | No |
| Parent delegation | Explicit | Through inheritance mechanism |
| Coupling to specific parent name | Higher | Lower |
| Useful with multiple inheritance | More difficult to manage manually | Designed to work with MRO |

---

# 16. `super()` and Multiple Inheritance

One important advantage of `super()` is that it works with Python's **Method Resolution Order (MRO)**.

In simple single inheritance:

```text
Rectangle
    ↓
Cuboid
```

the behavior is straightforward.

With multiple inheritance, a child can inherit from more than one parent:

```python
class A:
    ...

class B:
    ...

class C(A, B):
    ...
```

Python determines the order in which methods are searched using the **Method Resolution Order**.

`super()` follows that inheritance order.

This makes it much more suitable for cooperative multiple-inheritance designs than manually naming one particular parent class.

---

# 17. Why `super()` Is Preferred

The main reasons are:

### 1. No explicit `self`

Instead of:

```python
Rectangle.__init__(self, length, breadth)
```

write:

```python
super().__init__(length, breadth)
```

### 2. Less dependence on a specific parent name

The child does not directly write:

```python
Rectangle
```

in the constructor delegation statement.

### 3. Works with Python's MRO

`super()` participates in the Method Resolution Order, which is particularly important in multiple inheritance.

---

# 18. `super()` Does Not Mean "Always Call the Direct Parent"

A useful way to understand:

```python
super()
```

is that it follows Python's inheritance/MRO mechanism rather than simply meaning "hard-code the immediate parent class."

In a simple hierarchy:

```text
Rectangle → Cuboid
```

it results in the expected parent constructor call.

In more complex inheritance structures, `super()` follows the appropriate next class in the MRO.

---

# 19. Does `super()` Have to Be the First Statement?

A common question is whether:

```python
super().__init__()
```

must always be the first statement inside a Python constructor.

### Python

Python does **not** impose a rule that `super().__init__()` must be the first statement.

For example:

```python
class Cuboid(Rectangle):

    def __init__(self, length, breadth, height):

        if length <= 0:
            raise ValueError("Invalid length")

        print("Creating Cuboid")

        super().__init__(length, breadth)

        self.height = height
```

Here:

```python
super().__init__(length, breadth)
```

comes after:

```python
if length <= 0:
    ...
```

and:

```python
print("Creating Cuboid")
```

This is allowed in Python.

---

# 20. Java vs Python

The lecture contrasts the constructor rules in Java and Python.

## Java

In Java, a call to:

```java
super()
```

in a constructor must follow Java's constructor-invocation rules and must be the first statement.

## Python

Python does not impose the same "must be first statement" restriction on:

```python
super().__init__()
```

It can appear later in the child constructor.

For example:

```python
class Cuboid(Rectangle):

    def __init__(self, length, breadth, height):

        print("Checking parameters")

        if length <= 0:
            raise ValueError("Invalid length")

        super().__init__(length, breadth)

        self.height = height
```

The parent constructor is called after the checks.

---

# 21. Why Might We Place `super().__init__()` Later?

Because the child constructor may need to perform some work before initializing the parent portion.

Examples include:

- checking parameters
- transforming values
- logging information
- performing child-specific validation

For example:

```python
class Cuboid(Rectangle):

    def __init__(self, length, breadth, height):

        length = abs(length)
        breadth = abs(breadth)

        super().__init__(length, breadth)

        self.height = abs(height)
```

The values are transformed before they are sent to the parent constructor.

---

# 22. Important `super()` Syntax

The common syntax is:

```python
super().__init__(...)
```

For example:

```python
class Child(Parent):

    def __init__(self, value):
        super().__init__(value)
```

The child can then add its own initialization:

```python
self.child_value = ...
```

---

# 23. Complete Example — Parent and Child Data

```python
class Rectangle:

    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):

    def __init__(self, length, breadth, height):
        super().__init__(length, breadth)
        self.height = height

    def volume(self):
        return self.length * self.breadth * self.height


c = Cuboid(10, 5, 4)

print("Length:", c.length)
print("Breadth:", c.breadth)
print("Height:", c.height)
print("Volume:", c.volume())
```

Output:

```text
Length: 10
Breadth: 5
Height: 4
Volume: 200
```

The values `length` and `breadth` are initialized by the parent constructor, while `height` is initialized by the child constructor.

---

# 24. Guess the Output — Direct Parent Constructor

```python
class Rectangle:

    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):

    def __init__(self, length, breadth, height):
        Rectangle.__init__(self, length, breadth)
        self.height = height

    def volume(self):
        return self.length * self.breadth * self.height


c = Cuboid(10, 5, 4)

print(c.length)
print(c.breadth)
print(c.height)
print(c.volume())
```

Output:

```text
10
5
4
200
```

---

# 25. Guess the Output — `super()`

```python
class Rectangle:

    def __init__(self, length, breadth):
        self.length = length
        self.breadth = breadth


class Cuboid(Rectangle):

    def __init__(self, length, breadth, height):
        super().__init__(length, breadth)
        self.height = height

    def volume(self):
        return self.length * self.breadth * self.height


c = Cuboid(12, 6, 3)

print(c.length)
print(c.breadth)
print(c.height)
print(c.volume())
```

Output:

```text
12
6
3
216
```

---

# 26. Common Mistake — Forgetting `self` in Direct Parent Call

Incorrect:

```python
Rectangle.__init__(length, breadth)
```

Correct:

```python
Rectangle.__init__(self, length, breadth)
```

When directly invoking the parent constructor through its class name, the current object must be supplied explicitly.

With `super()`, this is unnecessary:

```python
super().__init__(length, breadth)
```

---

# 27. Common Mistake — Confusing `super()` with an Object

`super()` is not the child object itself.

For example:

```python
super().__init__(length, breadth)
```

means that the initialization is delegated according to the inheritance relationship and MRO.

It is not equivalent to simply writing:

```python
self.__init__(length, breadth)
```

The latter would call the current object's constructor and can lead to incorrect recursive behavior.

---

# 28. Parent and Child Constructor Flow

For:

```python
c = Cuboid(10, 5, 4)
```

the flow can be visualized as:

```text
Cuboid object created
        |
        ↓
Cuboid.__init__()
        |
        ↓
super().__init__(10, 5)
        |
        ↓
Rectangle.__init__()
        |
        +── self.length = 10
        |
        +── self.breadth = 5
        |
        ↓
return to Cuboid.__init__()
        |
        +── self.height = 4
        |
        ↓
Cuboid object initialized
```

---

# 29. Key Terms

| Term | Meaning |
|---|---|
| Parent class | Existing/base class |
| Child class | Class derived from another class |
| Inheritance | Mechanism for deriving a class from another class |
| Constructor | `__init__()` method used for initialization |
| Constructor chaining | Calling parent initialization from a child constructor |
| `super()` | Mechanism for delegating to the next class in the inheritance hierarchy/MRO |
| MRO | Method Resolution Order used to determine method lookup order |

---

# 30. Important Exam Questions

## Q1. What is inheritance?

Inheritance is an OOP mechanism in which a child class derives functionality from a parent class.

---

## Q2. What is a parent class?

A parent class is the existing/base class from which another class inherits.

---

## Q3. What is a child class?

A child class is a derived class that inherits from a parent class.

---

## Q4. Why does a child constructor call the parent constructor?

To reuse the parent's initialization logic and initialize inherited attributes.

---

## Q5. How can a parent constructor be called directly?

Using:

```python
ParentClass.__init__(self, arguments)
```

---

## Q6. Why is `self` required in a direct parent-constructor call?

Because the parent method is being invoked directly through the class name, so the current object must be supplied explicitly.

---

## Q7. How can a parent constructor be called using `super()`?

```python
super().__init__(arguments)
```

---

## Q8. What is an advantage of `super()`?

It avoids explicitly passing `self` and works with Python's inheritance/MRO mechanism.

---

## Q9. What is MRO?

MRO stands for **Method Resolution Order**. It determines the order in which Python searches classes for methods and attributes.

---

## Q10. Must `super().__init__()` be the first statement in a Python constructor?

No. Python does not impose that restriction.

---

# 31. Quick Revision

```text
Inheritance
    ↓
Parent + Child classes
    ↓
Child can reuse parent functionality
    ↓
Constructor chaining
    ↓
Parent initialization from child
    |
    +------------------------------+
    |                              |
Direct parent call             super()
    |                              |
Parent.__init__(self, ...)     super().__init__(...)
    |                              |
self required explicitly       self handled automatically
    |                              |
More direct coupling          Uses inheritance/MRO
```

---

# 32. Direct Parent Call vs `super()` — Memory Trick

```text
ParentClass.__init__(self, ...)
        ↓
"Call this specific parent explicitly"

super().__init__(...)
        ↓
"Delegate through the inheritance hierarchy"
```

For simple inheritance both can reach the parent constructor, but `super()` is designed to cooperate with Python's inheritance and MRO system.

---

# 33. Final Takeaways

Remember these points:

```text
Inheritance
→ allows a child class to derive from a parent class

Constructor chaining
→ child constructor invokes parent initialization

ParentClass.__init__(self, ...)
→ direct parent constructor call
→ self must be passed explicitly

super().__init__(...)
→ parent/delegated constructor call
→ self is handled automatically

super()
→ follows Python's inheritance/MRO mechanism

Python
→ does not require super().__init__() to be the first statement
```

---

# 34. Part 3 Coverage Checklist

- [x] Inheritance
- [x] Parent/base class
- [x] Child/derived class
- [x] Constructor chaining
- [x] Rectangle parent class
- [x] Cuboid child class
- [x] Parent constructor using class name
- [x] Explicit `self` in parent constructor call
- [x] Complete Cuboid volume example
- [x] Drawbacks of direct parent constructor calls
- [x] `super()`
- [x] Calling parent constructor using `super()`
- [x] Complete `super()` example
- [x] Direct call vs `super()` comparison
- [x] Multiple inheritance and MRO
- [x] Why `super()` is useful
- [x] `super()` placement inside Python constructors
- [x] Java vs Python constructor rule
- [x] Parameter validation/transformation before `super()`
- [x] Output-based examples
- [x] Common mistakes
- [x] Exam questions
- [x] Revision map

---
