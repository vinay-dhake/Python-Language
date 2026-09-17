# Lecture 31 — Introduction to Object-Oriented Programming (OOP) in Python
## Part 1 — POP vs OOP, Objects, Classes, and Creating Objects

> **Coverage:** Introduction through creation of classes and objects.

---

# 1. Introduction to Object-Oriented Programming

**Object-Oriented Programming (OOP)** is a programming paradigm used to design programs around **objects**.

Before OOP, the programs covered so far were mainly written using **Procedure-Oriented Programming (POP)**.

---

# 2. Procedure-Oriented Programming (POP)

## What is POP?

**POP = Procedure-Oriented Programming.**

In POP, a program is designed around **functions/procedures**. These functions are blocks of statements that manipulate data.

For example, a calculator can be divided into functions:

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

def multiply(a, b):
    return a * b

def divide(a, b):
    return a / b
```

The program is therefore organized around functions.

```text
POP
 ↓
Functions / Procedures
 ↓
Functions manipulate data
```

---

# 3. Advantages of POP

## 3.1 Code Reusability

The same code can be reused at different places without copying it.

```python
def add(a, b):
    return a + b

print(add(10, 20))
print(add(5, 7))
```

The `add()` function is written once and can be used multiple times.

## 3.2 Easy to Implement

POP is easy to implement, especially for small programs.

## 3.3 Easy to Track Program Flow for Small Programs

For small programs, it is easier to follow which function is called and when.

---

# 4. Disadvantages of POP

The lecture discusses three major problems.

## 4.1 Difficult to Relate With Real-World Objects

Real-world entities such as:

- Cars
- Humans
- Dogs
- Mobile phones
- Accounts
- Students
- Employees

have both data and behaviours.

For example, a car has:

```text
Attributes:
    Color
    Mileage
    Maximum Speed
    Model
    Year

Behaviours:
    Start
    Stop
    Drive
    Brake
```

Representing such entities naturally using only independent functions is difficult.

## 4.2 Data is Exposed to the Whole Program

Data may be accessible to different functions throughout the program. This gives less control over how data is accessed or modified.

## 4.3 Difficult to Create New Data Types

Built-in types such as `int`, `float`, `str`, `list`, etc. cannot directly describe every real-world entity.

For example, an employee may need:

```text
Age
Name
Salary
```

OOP allows us to create a structure representing such an entity.

---

# 5. Solution: Object-Oriented Programming

The solution to these problems is **Object-Oriented Programming (OOP)**.

OOP allows us to represent real-world entities directly in our programs.

The roots of OOP go back to the **1960s**. The lecture identifies **Simula** as the first programming language to use objects.

---

# 6. What is OOP?

> **OOP is a programming paradigm (way of developing programs) in which real-world objects can be represented in code.**

Examples include:

```text
Car
Animal
Person
Account
Student
Employee
```

OOP allows us to combine:

```text
Data + Functionality
```

and wrap them inside an **object**.

---

# 7. What is an Object?

In programming, a real-world entity having specific **attributes/features** can be represented as an object.

### Simple definition

> **An object is something that possesses characteristics and can perform certain functions.**

An object therefore has two major aspects:

```text
Object
│
├── Attributes → Characteristics / Data
│
└── Behaviours → Functions / Actions
```

### Easy memory trick

```text
WHAT DOES IT HAVE? → Attributes
WHAT CAN IT DO?    → Behaviours
```

---

# 8. Example: Car as an Object

A **car** is an example of an object.

### Behaviours of a Car

A car can:

```text
Start
Stop
Drive
Brake
```

These are the functions/behaviours of the car.

### Attributes of a Car

A car can have:

```text
Color
Mileage
Maximum Speed
Model
Year
```

So:

```text
CAR
│
├── Attributes
│   ├── Color
│   ├── Mileage
│   ├── Maximum Speed
│   ├── Model
│   └── Year
│
└── Behaviours
    ├── Start
    ├── Stop
    ├── Drive
    └── Brake
```

---

# 9. Are Humans Objects?

Yes.

Humans can also be represented as objects because they have attributes and behaviours.

### Attributes

```text
Name
Height
Age
```

### Behaviours

```text
Walking
Talking
Running
Eating
```

Therefore:

```text
Human
│
├── Attributes
│   ├── Name
│   ├── Height
│   └── Age
│
└── Behaviours
    ├── Walking
    ├── Talking
    ├── Running
    └── Eating
```

---

# 10. What is a Class?

To create/represent objects, we first write their attributes and behaviours under a **single group**.

This group is called a **class**.

> **A class is an architecture, blueprint, or template of an object.**

A class is a proper description of the:

- Attributes
- Methods/behaviours

of an object.

---

# 11. Class as a Blueprint

The easiest analogy is a blueprint/design.

Suppose a particular type of car has a design. The design describes what the car will have and what it can do.

That design is like a **class**.

Using the same class, we can create many objects.

```text
             CLASS
        (Blueprint/Design)
               │
       ┌───────┼───────┐
       ↓       ↓       ↓
     Object  Object  Object
       1       2       3
```

### Remember

```text
CLASS  → Blueprint / Template
OBJECT → Instance created from the class
```

---

# 12. Car Class Example

The lecture illustrates a car class using a common design from which many cars can be created.

Possible attributes include:

```text
Car Colour
Model Year
Max Speed
Engine Capacity
Mileage
```

Possible methods include:

```text
Start
Stop
Brake
Accelerate
Drive
```

The important idea is:

> One class can be used to create many objects of the same general type.

---

# 13. Dog Class Example

A **Dog** class is another example.

The class contains attributes:

```text
Breed
Size
Age
Color
```

and behaviours:

```text
Eat()
Sleep()
Sit()
Run()
```

So:

```text
DOG CLASS
│
├── Attributes
│   ├── Breed
│   ├── Size
│   ├── Age
│   └── Color
│
└── Behaviours
    ├── Eat()
    ├── Sleep()
    ├── Sit()
    └── Run()
```

The lecture's diagram shows three different dog objects created from this common class:

### Dog 1

```text
Breed = Neapolitan Mastiff
Size  = Large
Age   = 5 years
Color = Black
```

### Dog 2

```text
Breed = Maltese
Size  = Small
Age   = 2 years
Color = White
```

### Dog 3

```text
Breed = Chow Chow
Size  = Medium
Age   = 3 years
Color = Brown
```

The class gives the common structure, while each object has its own actual values.

---

# 14. Student Class Example

A **Student** can also be represented using a class.

Possible attributes shown/discussed include:

```text
Name
Age
Gender
Roll Number
```

Possible behaviours include:

```text
Eating
Drinking
Running
```

Multiple student objects can be created from the same Student class.

For example:

```text
Student 1
Name = Amit
Age = 20
Roll No = 101

Student 2
Name = Rahul
Age = 21
Roll No = 102
```

The class defines the structure; individual objects contain the particular values.

---

# 15. Other Real-World OOP Examples

## College Management System

Possible objects:

```text
Student
Faculty
Department
Library
Canteen
```

### Student

Attributes:

```text
Roll Number
Name
Gender
Percentage
```

Behaviours:

```text
Take Admission
Attend Classes
Appear for Exams
```

---

## Car

Attributes:

```text
Color
Brand
Price
Top Speed
```

Behaviours:

```text
Start
Stop
Accelerate
Reverse
```

---

## Dog

Attributes:

```text
Breed
Size
Age
Color
```

Behaviours:

```text
Eat
Sleep
Sit
Bark
Run
```

---

## Citizen / Aadhaar System

A possible class is:

```text
Citizen
```

One important property is:

```text
Aadhaar Number
```

Each Citizen object can hold its own Aadhaar number.

```text
Citizen Class
      │
 ┌────┼────┐
 ↓    ↓    ↓
 C1   C2   C3
 │    │    │
Different Aadhaar numbers
```

---

# 16. Creating a Class in Python

Python uses the **`class` keyword** to define a class.

A class can contain **class members**, such as:

- Attributes
- Methods

The basic structure is:

```python
class ClassName:
    # class members
```

---

# 17. Syntax of Creating a Class

```python
class <class_name>:
    # class members
```

### Components

```text
class
 ↓
Keyword used to define a class

<class_name>
 ↓
Name of the class

:
 ↓
Beginning of the class body

class members
 ↓
Attributes and methods
```

---

# 18. Example: Empty Class

An empty class can be written using `pass`.

```python
class Emp:
    pass
```

Here:

- `class` is the Python keyword.
- `Emp` is the class name.
- `pass` keeps the class body empty.

`pass` is useful when a syntactically valid block is required but no statement needs to be written yet.

---

# 19. Creating Objects

After defining a class, we create an object to use it.

Creating an object is called:

> **Instantiating a class**

An object is also called an:

> **Instance of the class**

Therefore:

```text
Creating object
      =
Instantiating class
      =
Creating an instance
```

---

# 20. Syntax of Creating an Object

```python
var_name = class_name()
```

Example:

```python
e = Emp()
```

Here:

```text
Emp
 ↓
Class name

()
 ↓
Creates an instance

e
 ↓
Reference variable
```

---

# 21. Basic Class and Object Example

```python
class Emp:
    pass

e = Emp()
```

Explanation:

- `Emp` is the class.
- `Emp()` creates an object/instance.
- `e` refers to that object.

Conceptually:

```text
Emp class
   │
   │ Emp()
   ↓
Emp object
   ↑
   │
   e
```

---

# 22. Complete Example: `type()` and Object Representation

The lecture gives this complete program:

```python
class Emp:
    pass

e = Emp()

print(type(e))
print(e)
```

### `print(type(e))`

This tells us the type/class of `e`.

The output has the form:

```text
<class '__main__.Emp'>
```

This means that `e` is an object of class `Emp`.

### `print(e)`

The object is displayed in a form similar to:

```text
<__main__.Emp object at 0x...>
```

The exact hexadecimal value depends on the particular execution.

It identifies the object using a representation containing its class and a memory-related address.

---

# 23. Understanding `__main__`

When the Python file is executed directly, its module name is:

```python
__main__
```

Therefore:

```text
<class '__main__.Emp'>
```

can be understood as:

```text
Module  → __main__
Class   → Emp
Object  → e
```

---

# 24. Class vs Object

| Class | Object |
|---|---|
| Blueprint/template | Instance |
| Describes structure | Represents an actual instance |
| Contains definitions of attributes/methods | Has actual data associated with the instance |
| Used to create objects | Created from a class |
| Example: `Emp` | Example: `e = Emp()` |

### Most important line

```text
CLASS  = Blueprint
OBJECT = Instance
```

---

# 25. Quick Revision

## POP

```text
Procedure-Oriented Programming
        ↓
Program organized around functions
```

Advantages:

- Reusability
- Easy implementation
- Easy to track small-program flow

Problems:

- Difficult to relate with real-world objects
- Data is exposed to the whole program
- Difficult to create new data types

---

## OOP

```text
Object-Oriented Programming
        ↓
Program organized around objects
        ↓
Real-world entities can be represented
        ↓
Data + Functionality
```

---

## Object

```text
Object
│
├── Attributes → Data / Characteristics
└── Behaviours → Functions / Actions
```

---

## Class

```text
Class
│
└── Blueprint / Template
        ↓
     Objects
```

---

## Python Syntax

### Class

```python
class Emp:
    pass
```

### Object

```python
e = Emp()
```

---

# 26. Important Exam Questions

### Q1. What is POP?

**Answer:** POP stands for Procedure-Oriented Programming. It is a programming paradigm in which programs are designed around functions/procedures that manipulate data.

### Q2. State the advantages of POP.

1. Code can be reused.
2. It is easy to implement.
3. Program flow is easier to track for small programs.

### Q3. State the disadvantages of POP.

1. Difficult to relate with real-world objects.
2. Data is exposed to the whole program.
3. Difficult to create new data types.

### Q4. What is OOP?

**Answer:** OOP is a programming paradigm that allows programs to be designed around objects and allows real-world entities to be represented in code.

### Q5. What is an object?

**Answer:** An object is a real-world entity represented in programming that possesses attributes/characteristics and can perform functions/behaviours.

### Q6. What is a class?

**Answer:** A class is a blueprint, template, architecture, or proper description of the attributes and methods of an object.

### Q7. What is instantiation?

**Answer:** Instantiation means creating an object/instance of a class.

### Q8. How do you create a class in Python?

```python
class Emp:
    pass
```

### Q9. How do you create an object?

```python
e = Emp()
```

### Q10. What does `type(e)` tell us?

It tells us the class/type of the object referenced by `e`.

---

# 27. One-Minute Memory Map

```text
                     OOP
                      │
          ┌───────────┴───────────┐
          ↓                       ↓
        CLASS                   OBJECT
          │                       │
    Blueprint/Template          Instance
          │                       │
          └───────────┬───────────┘
                      ↓
             Attributes + Behaviours
                      │
               ┌──────┴──────┐
               ↓             ↓
              Data        Methods
```

Basic Python example:

```python
class Emp:
    pass

e = Emp()

print(type(e))
print(e)
```

Remember:

```text
class Emp   → Defines a class
Emp()       → Creates an object
e           → Reference to the object
type(e)     → Gives the object's type
```

---

## End of Part 1
===============================================================================================================================================================
## Part 2 — Data Members, Instance Variables, `__init__()`, and `self`

> **Coverage:** Adding data members → types of variables → instance variables → comparison with C++/Java → Python `__init__()` → automatic execution → `self` → why `self` is required.

---

# 1. Adding Data Members / Attributes

After defining a class, the next step is to provide it with **data members/variables**.

These variables are used to hold values related to the objects.

For example, an employee object may need data such as:

```text
Age
Name
Salary
```

These values can be stored as attributes of the employee object.

---

# 2. Types of Variables in a Python Class

The lecture introduces **three types of variables**:

1. **Instance Variables**
2. **Local Variables**
3. **Class Variables**

```text
Variables in a class
│
├── Instance Variables
│   └── Created on an instance/object basis
│
├── Local Variables
│   └── Created inside a method
│
└── Class Variables
    └── Created inside the class and shared by objects
```

---

## 2.1 Instance Variables

Instance variables are created **for each individual object/instance**.

Each object gets its own copy.

Example idea:

```text
Object 1 → age, name, salary
Object 2 → age, name, salary
Object 3 → age, name, salary
```

Even though the variables have the same names, their values can be different for different objects.

---

## 2.2 Local Variables

A local variable is created **inside a method**.

Its lifetime is limited to the execution of that method.

Conceptually:

```text
Method starts
     ↓
Local variable is created
     ↓
Method executes
     ↓
Method finishes
     ↓
Local variable is destroyed
```

Example:

```python
class Emp:
    def show(self):
        age = 25
        print(age)
```

Here:

```python
age = 25
```

is a local variable of the `show()` method.

It is not automatically an attribute of the object.

---

## 2.3 Class Variables

Class variables are created **inside the class** and are shared by the objects of that class.

They are sometimes also called **static variables**.

Conceptually:

```text
              Class Variable
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
       Object 1  Object 2  Object 3
          │         │         │
          └──── Shared ──────┘
```

The detailed use of class variables comes later; for now, remember that they are associated with the class and are shared.

---

# 3. What is an Instance Variable?

The lecture defines an instance variable as an **object variable**.

> **Instance variables are created by Python for each individual object of the class.**

The most important property is:

> **Each object has its own copy of an instance variable.**

They are not shared between different objects.

---

## Example Concept

Suppose we have:

```text
Employee object e
Employee object f
```

Both objects may have an attribute called:

```text
age
```

But:

```text
e.age
```

and

```text
f.age
```

belong to different objects.

For example:

```python
e.age = 25
f.age = 30
```

Then:

```text
e.age → 25
f.age → 30
```

Changing `e.age` does not automatically change `f.age`.

---

# 4. Instance Variables vs Shared Variables

This distinction is important.

### Instance variable

```text
Object-specific
```

Each object gets its own copy.

### Class variable

```text
Class-level
```

The same class variable can be shared by objects.

So remember:

```text
Instance Variable → One copy per object
Class Variable    → Shared by objects
```

---

# 5. Creating Instance Variables in Python

Creating instance variables in Python is different from languages such as **C++ and Java**.

The lecture compares the three languages to explain this difference.

---

# 6. Creating Instance Variables in C++

In C++, data members can be declared directly inside the class.

Example:

```cpp
class Emp
{
    int age;
    char name[20];
    double salary;
    ........
    ........
};
```

Here:

```text
age
name
salary
```

are instance variables/data members of the class.

To use the class, the lecture shows:

```cpp
Emp obj;
```

Creating an object allocates space for the object in memory.

The object contains the data members:

```text
age
name
salary
```

The lecture also explains that a special method called a **constructor** is automatically called for initializing the object.

---

# 7. Creating Instance Variables in Java

Java also allows data members to be declared inside the class.

Example:

```java
class Emp
{
    int age;
    String name;
    double salary;
    ........
    ........
}
```

Here:

```text
age
name
salary
```

are instance variables.

To create an object:

```java
Emp obj = new Emp();
```

This creates an object in the **heap** containing the data members.

The reference variable points to that object.

Conceptually:

```text
Reference
    │
    ↓
┌─────────────────────┐
│       Object        │
│                     │
│ age                 │
│ name                │
│ salary              │
└─────────────────────┘
```

The lecture also explains that the special method called a **constructor** is called automatically to initialize the object.

---

# 8. C++/Java vs Python

The important difference is:

```text
C++ / Java
    ↓
Declare data members inside the class
    ↓
Object creation allocates the corresponding object data
```

Python handles instance-variable creation differently.

In Python, the lecture introduces the special method:

```python
__init__()
```

---

# 9. `__init__()` in Python

Python uses a special method called:

```python
__init__()
```

to create and initialize an object's initial attributes by giving them their default values.

The lecture compares it with the constructor concept in C++/Java.

### Important points

- `__init__()` is a special method.
- Python calls it automatically when an object is created.
- It is used to initialize the object's initial attributes.
- It behaves similarly to a constructor in C++ or Java.

---

# 10. Why is `__init__()` Called Automatically?

Consider:

```python
class Emp:
    def __init__(self):
        print("Object created. . .")
```

Now create an object:

```python
e = Emp()
```

We did **not** explicitly write:

```python
e.__init__()
```

Nevertheless, Python automatically invokes `__init__()` during object creation.

Therefore the output is:

```text
Object created. . .
```

This demonstrates the automatic execution of `__init__()`.

---

# 11. Full Code — Automatic `__init__()` Execution

The example from the lecture is:

```python
class Emp:
    def __init__(self):
        print("Object created. . .")

e = Emp()
```

### Output

```text
Object created. . .
```

### Execution flow

```text
class Emp
    ↓
Define __init__()
    ↓
e = Emp()
    ↓
Object is created
    ↓
Python automatically calls __init__()
    ↓
print() executes
    ↓
Object created. . .
```

### Key point

> As soon as the object of the `Emp` class is created, Python automatically calls `__init__()`.

---

# 12. Another Example — Multiple Objects

Now consider:

```python
class Emp:
    def __init__(self):
        print("Object created. . .")

e = Emp()
f = Emp()
g = Emp()
```

There are **three object creations**:

```python
e = Emp()
f = Emp()
g = Emp()
```

Therefore `__init__()` is automatically called **three times**.

### Output

```text
Object created. . .
Object created. . .
Object created. . .
```

### Execution flow

```text
e = Emp()
   ↓
__init__()
   ↓
Object created. . .

f = Emp()
   ↓
__init__()
   ↓
Object created. . .

g = Emp()
   ↓
__init__()
   ↓
Object created. . .
```

This example clearly proves that `__init__()` executes automatically **for each object created**.

---

# 13. The `self` Argument

In the examples above, you may have noticed:

```python
def __init__(self):
```

There is an argument called:

```python
self
```

This leads to two important questions:

1. **What is `self`?**
2. **Why is `self` required?**

These are fundamental questions in Python OOP.

---

# 14. What is `self`?

Whenever we create an object, Python automatically calls the `__init__()` method.

While calling `__init__()`, Python also passes the **address/reference of the object** for which `__init__()` is being called as the **first argument**.

Therefore, when defining `__init__()`, we need at least one formal parameter to receive this object reference.

By convention, this parameter is named:

```python
self
```

### In simple words

> **`self` refers to the current object.**

It allows the method to know **which object** is being initialized or operated on.

---

# 15. Understanding `self` With an Object

Suppose:

```python
e = Emp()
```

Python internally needs to associate the call to `__init__()` with object `e`.

Conceptually:

```text
e = Emp()
   │
   ↓
Object created
   │
   ↓
__init__(e)
   │
   ↓
self receives the object reference
```

So inside `__init__()`:

```python
self
```

refers to the object currently being initialized.

---

# 16. Why is `self` Needed?

Suppose we create multiple objects:

```python
e = Emp()
f = Emp()
g = Emp()
```

Each object is different.

Python therefore needs a way for a method to identify the object on which it is operating.

Conceptually:

```text
e = Emp()
   ↓
__init__(self = e)

f = Emp()
   ↓
__init__(self = f)

g = Emp()
   ↓
__init__(self = g)
```

This is why the first parameter is required in an instance method.

The parameter is conventionally called:

```python
self
```

---

# 17. Important: `self` Is a Parameter

Consider:

```python
class Emp:
    def __init__(self):
        print("Object created. . .")
```

The method definition contains:

```python
self
```

So:

```python
def __init__(self):
```

has one parameter.

When Python automatically calls the method, the current object's reference is supplied to that parameter.

The object creation:

```python
e = Emp()
```

can be understood conceptually as Python arranging a call equivalent to:

```python
__init__(e)
```

The exact internal mechanics are more detailed, but for learning OOP, the important point is:

```text
Current object reference
          ↓
        self
```

---

# 18. What If We Don't Create `self`?

The lecture next demonstrates what happens if `self` is not provided.

Incorrect code:

```python
class Emp:
    def __init__():
        print("Object created. . .")

e = Emp()
```

Notice that:

```python
def __init__():
```

does **not** contain `self`.

But Python still passes the current object reference when calling the instance method.

Therefore, the method's parameter list does not match the arguments supplied by Python.

This results in an error.

The important lesson is:

> **An instance method must have a parameter to receive the current object reference. By convention, that parameter is named `self`.**

---

# 19. Correct vs Incorrect `__init__()`

## Correct

```python
class Emp:
    def __init__(self):
        print("Object created. . .")

e = Emp()
```

## Incorrect

```python
class Emp:
    def __init__():
        print("Object created. . .")

e = Emp()
```

### Difference

```text
Correct:
__init__(self)
          ↑
Receives current object reference

Incorrect:
__init__()
          ↑
No parameter to receive the object reference
```

---

# 20. Key Relationship: Object Creation → `__init__()` → `self`

Keep this sequence in mind:

```text
e = Emp()
     │
     ↓
Object of Emp is created
     │
     ↓
Python automatically calls __init__()
     │
     ↓
Current object's reference is passed
     │
     ↓
self receives that reference
```

This sequence becomes extremely important when we start creating instance variables.

---

# 21. Quick Revision Table

| Concept | Meaning |
|---|---|
| Instance variable | Variable created separately for each object |
| Local variable | Variable created inside a method |
| Class variable | Variable created inside class and shared by objects |
| `__init__()` | Special method automatically called when object is created |
| `self` | Parameter that receives the current object's reference |
| Instantiation | Creation of an object/instance |
| Constructor comparison | `__init__()` is used similarly to a constructor for initialization |

---

# 22. Important Examples to Remember

## Example 1 — One Object

```python
class Emp:
    def __init__(self):
        print("Object created. . .")

e = Emp()
```

Output:

```text
Object created. . .
```

---

## Example 2 — Three Objects

```python
class Emp:
    def __init__(self):
        print("Object created. . .")

e = Emp()
f = Emp()
g = Emp()
```

Output:

```text
Object created. . .
Object created. . .
Object created. . .
```

Reason:

```text
3 objects created
       ↓
__init__() called 3 times
```

---

## Example 3 — Missing `self`

```python
class Emp:
    def __init__():
        print("Object created. . .")

e = Emp()
```

This is incorrect because `__init__()` has no parameter to receive the current object's reference.

---

# 23. Exam-Oriented Questions

### Q1. What are the three types of variables in a Python class?

**Answer:**

1. Instance variables
2. Local variables
3. Class variables

---

### Q2. What is an instance variable?

**Answer:**

An instance variable is a variable created for an individual object of a class. Each object has its own copy of the instance variable.

---

### Q3. What is a local variable?

**Answer:**

A local variable is created inside a method and exists during the execution of that method.

---

### Q4. What is a class variable?

**Answer:**

A class variable is created inside a class and is shared by the objects of that class.

---

### Q5. What is `__init__()`?

**Answer:**

`__init__()` is a special Python method that is automatically called when an object is created. It is used to initialize the object's initial attributes.

---

### Q6. Why is `__init__()` compared with a constructor?

Because it is automatically invoked during object creation and is used for initialization, similar to constructors in C++ and Java.

---

### Q7. What is `self`?

**Answer:**

`self` is the conventional first parameter of an instance method. It receives the reference to the current object when the method is called.

---

### Q8. Why is `self` required?

**Answer:**

When Python calls an instance method, it passes the current object's reference as the first argument. A parameter is required to receive that reference; by convention, that parameter is named `self`.

---

### Q9. What happens when three objects are created?

For:

```python
e = Emp()
f = Emp()
g = Emp()
```

the `__init__()` method is automatically called once for each object.

Therefore:

```text
__init__() → 3 calls
```

---

# 24. One-Minute Memory Map

```text
                 CLASS
                   │
                   ↓
             Create Object
                   │
                   ↓
              Emp()
                   │
                   ↓
           __init__() called
                   │
                   ↓
        Current object reference
                   │
                   ↓
                 self
                   │
                   ↓
       Initialize object attributes
```

And remember the three variable types:

```text
Python Class Variables
│
├── Instance Variable
│      └── One copy per object
│
├── Local Variable
│      └── Inside method
│
└── Class Variable
       └── Shared by objects
```

---

## End of Part 2
============================================================================================================================================================
## Part 3 — `self`, Instance Variables, Passing Parameters to `__init__()`, and Default Arguments

> **Coverage:** The role of `self` → dynamically creating instance members → hardcoded instance variables → adding attributes outside `__init__()` → passing parameters to `__init__()` → local parameters vs instance variables → using different data for different objects → default arguments → multiple `__init__()` definitions.

---

# 1. More About `self`

The `self` argument is one of the most important concepts in Python OOP.

The lecture explains that:

> **`self` always points to the address/reference of the current object.**

It can be thought of as similar to:

- `this` reference in Java
- `this` pointer in C++

The exact syntax differs between languages, but the purpose is similar: it identifies the current object.

---

# 2. `self` Is Used With Instance Methods

Python passes the address/reference of the current object to an instance method when that method is called.

This applies not only to:

```python
__init__()
```

but also to other instance methods.

Therefore, an instance method normally has at least one parameter to receive the current object reference.

By convention, that parameter is named:

```python
self
```

Example:

```python
class Emp:
    def show(self):
        print("Employee details")
```

Here:

```python
self
```

represents the object on which `show()` is operating.

---

# 3. Can We Give Some Other Name to `self`?

Yes.

The word `self` is a **convention**, not a special keyword that must literally be used as the parameter name.

The lecture demonstrates:

```python
class Emp:
    def __init__(myself):
        print("Object created. . .")

e = Emp()
```

### Output

```text
Object created. . .
```

The parameter is named:

```python
myself
```

instead of:

```python
self
```

and the program still works.

---

## Important Point

Although another name can be used, using:

```python
self
```

is strongly preferred because it is the standard Python convention and makes the code easier for other programmers to understand.

So:

```python
def __init__(self):
```

is preferred over:

```python
def __init__(myself):
```

---

# 4. The Most Important Role of `self`

The lecture introduces a very important use of `self`:

> We can use `self` to dynamically add instance members to the current object.

The basic syntax is:

```python
class <class_name>:
    def __init__(self):
        self.<var_name> = value
```

For example:

```python
class Emp:
    def __init__(self):
        self.age = 25
        self.name = "Rahul"
        self.salary = 30000.0
```

Here:

```python
self.age
self.name
self.salary
```

are instance variables/instance members.

They belong to the object currently represented by `self`.

---

# 5. `self.variable` Creates an Instance Variable

Consider:

```python
self.age = 25
```

The left-hand side:

```python
self.age
```

means:

> Create/store the attribute `age` in the current object.

The right-hand side:

```python
25
```

is the value assigned to that attribute.

Similarly:

```python
self.name = "Rahul"
```

stores the name in the current object.

And:

```python
self.salary = 30000.0
```

stores the salary in the current object.

---

# 6. Example — Hardcoded Instance Variables

The lecture gives this example:

```python
class Emp:
    def __init__(self):
        self.age = 25
        self.name = "Rahul"
        self.salary = 30000.0

e = Emp()

print("Age:", e.age, "Name:", e.name, "Salary:", e.salary)
```

### Output

```text
Age: 25 Name: Rahul Salary: 30000.0
```

### Explanation

When:

```python
e = Emp()
```

is executed:

1. An `Emp` object is created.
2. Python automatically calls `__init__()`.
3. `self` refers to the newly created object.
4. The following instance variables are created:

```python
self.age = 25
self.name = "Rahul"
self.salary = 30000.0
```

Therefore:

```python
e.age
e.name
e.salary
```

can be accessed after object creation.

---

# 7. Object Representation of the Above Example

Conceptually:

```text
Emp Class
   │
   ↓
e = Emp()
   │
   ↓
┌──────────────────────────┐
│       Emp Object         │
│                          │
│ age    = 25              │
│ name   = "Rahul"         │
│ salary = 30000.0         │
└──────────────────────────┘
```

The attributes are attached to the individual object.

---

# 8. What Happens With Multiple Objects?

Consider:

```python
class Emp:
    def __init__(self):
        self.age = 25
        self.name = "Rahul"
        self.salary = 30000.0

e = Emp()
f = Emp()
```

The `__init__()` method executes separately for each object.

So both objects receive their own instance variables:

```text
e
├── age = 25
├── name = "Rahul"
└── salary = 30000.0

f
├── age = 25
├── name = "Rahul"
└── salary = 30000.0
```

The variables have the same initial values here because the values are hardcoded.

---

# 9. Problem With Hardcoded Values

Suppose we want two employees:

```text
Employee 1:
Age = 25
Name = Rahul
Salary = 30000

Employee 2:
Age = 31
Name = Varun
Salary = 45000
```

The hardcoded version cannot conveniently provide different values because:

```python
self.age = 25
self.name = "Rahul"
self.salary = 30000.0
```

always assigns the same values whenever `__init__()` executes.

Therefore, we need a way to pass different values while creating different objects.

This leads to:

> **Passing parameters to `__init__()`**

---

# 10. Can We Add an Instance Variable Outside `__init__()`?

Yes.

Python allows an instance attribute to be added directly to an object.

The lecture gives this example:

```python
class Emp:
    def __init__(self):
        self.age = 25
        self.name = "Rahul"

e = Emp()

e.salary = 30000.0

print("Age:", e.age, "Name:", e.name, "Salary:", e.salary)
```

### Important observation

`salary` was not created inside `__init__()`.

Instead, it was added after the object was created:

```python
e.salary = 30000.0
```

Because it is written using the object reference:

```python
e.salary
```

Python adds `salary` to that particular object.

---

# 11. Understanding Dynamic Addition of Attributes

Consider:

```python
e = Emp()
e.salary = 30000.0
```

Conceptually:

```text
Step 1

e = Emp()

e object
├── age
└── name


Step 2

e.salary = 30000.0

e object
├── age
├── name
└── salary
```

The attribute is dynamically added to that object.

This demonstrates the important role of `self` and object references in Python.

---

# 12. `self` and the Dot Operator

The general form is:

```python
self.variable = value
```

The dot operator:

```python
.
```

is used to access/create an attribute belonging to the object.

Examples:

```python
self.age = 25
self.name = "Rahul"
self.salary = 30000.0
```

Later, outside the class, we use the object reference:

```python
e.age
e.name
e.salary
```

So:

```text
Inside class:
self.age

Outside class:
e.age
```

Both refer to the `age` attribute of the relevant object.

---

# 13. Passing Parameters to `__init__()`

The lecture asks:

> Since `__init__()` is also a method, can we pass arguments to it?

**Yes.**

Since `__init__()` is a method, it can receive parameters.

However, there are two important things to remember.

### Rule 1 — Arguments are passed during object creation

Because Python calls `__init__()` automatically when an object is created, the values need to be supplied while creating the object.

Example:

```python
e = Emp(25, "Rahul", 30000.0)
```

### Rule 2 — Parameters must be defined in `__init__()`

The method must contain parameters to receive those values.

Example:

```python
def __init__(self, age, name, salary):
```

---

# 14. Parameterized `__init__()`

The basic structure is:

```python
class Emp:
    def __init__(self, age, name, salary):
        self.age = age
        self.name = name
        self.salary = salary
```

Now the object can be created using:

```python
e = Emp(25, "Rahul", 30000.0)
```

The values are passed to `__init__()`.

---

# 15. Understanding `self.age = age`

This line is extremely important:

```python
self.age = age
```

There are **two different `age` variables** here.

### Left side

```python
self.age
```

This is the **instance variable/attribute** belonging to the current object.

### Right side

```python
age
```

This is the **parameter/local variable** received by `__init__()`.

So:

```text
self.age = age
    ↑       ↑
object     parameter
attribute
```

Similarly:

```python
self.name = name
```

and:

```python
self.salary = salary
```

copy the parameter values into the object's instance variables.

---

# 16. Parameterized `__init__()` — Complete Example

The lecture gives:

```python
class Emp:
    def __init__(self, age, name, salary):
        self.age = age
        self.name = name
        self.salary = salary

e = Emp(25, "Rahul", 30000.0)

print("Age:", e.age, "Name:", e.name, "Salary:", e.salary)

f = Emp(31, "Varun", 45000.0)

print("Age:", f.age, "Name:", f.name, "Salary:", f.salary)
```

### Output

```text
Age: 25 Name: Rahul Salary: 30000.0
Age: 31 Name: Varun Salary: 45000.0
```

---

# 17. Step-by-Step Execution of the Parameterized Example

## First object

```python
e = Emp(25, "Rahul", 30000.0)
```

Python creates an `Emp` object and calls:

```python
__init__(self, 25, "Rahul", 30000.0)
```

Conceptually:

```text
self    → e object
age     → 25
name    → "Rahul"
salary  → 30000.0
```

Then:

```python
self.age = age
self.name = name
self.salary = salary
```

produces:

```text
e.age    = 25
e.name   = "Rahul"
e.salary = 30000.0
```

---

## Second object

```python
f = Emp(31, "Varun", 45000.0)
```

Python creates another object.

Conceptually:

```text
self    → f object
age     → 31
name    → "Varun"
salary  → 45000.0
```

Therefore:

```text
f.age    = 31
f.name   = "Varun"
f.salary = 45000.0
```

---

# 18. Why Do We Need `self`?

Without `self`, the values would only exist as local parameters during method execution.

For example:

```python
def __init__(self, age, name, salary):
```

The variables:

```python
age
name
salary
```

are parameters/local variables.

They are available while `__init__()` is executing.

To store those values inside the object, we write:

```python
self.age = age
self.name = name
self.salary = salary
```

So:

```text
Parameter/local variable
          ↓
     self.variable
          ↓
Instance variable of object
```

---

# 19. Lifetime of Parameters vs Instance Variables

The lecture makes an important distinction.

### Parameters/local variables

For:

```python
def __init__(self, age, name, salary):
```

the variables:

```python
age
name
salary
```

are parameters/local variables.

They exist while the method is executing.

After the method finishes, these local parameters are destroyed.

### Instance variables

Variables such as:

```python
self.age
self.name
self.salary
```

belong to the object.

They remain available as long as the object exists.

Therefore:

```text
age
name
salary
   ↓
temporary method parameters

self.age
self.name
self.salary
   ↓
object's instance attributes
```

---

# 20. Important Point: `self` Must Be First

The lecture emphasizes:

> The argument `self` should always be the first argument because Python passes the address/reference of the current object as the first argument.

Therefore:

```python
def __init__(self, age, name, salary):
```

is the expected structure.

Not:

```python
def __init__(age, self, name, salary):
```

The first parameter is used for the current object reference.

---

# 21. Parameter Name and Instance Variable Name Can Be Different

They do not have to use the same names.

The lecture also demonstrates:

```python
class Emp:
    def __init__(self, x, y, z):
        self.age = x
        self.name = y
        self.salary = z

e = Emp(25, "Rahul", 30000.0)

print("Age:", e.age, "Name:", e.name, "Salary:", e.salary)

f = Emp(31, "Varun", 45000.0)

print("Age:", f.age, "Name:", f.name, "Salary:", f.salary)
```

### Mapping

For:

```python
e = Emp(25, "Rahul", 30000.0)
```

the parameters receive:

```text
x = 25
y = "Rahul"
z = 30000.0
```

Then:

```python
self.age = x
self.name = y
self.salary = z
```

creates:

```text
e.age    = 25
e.name   = "Rahul"
e.salary = 30000.0
```

For:

```python
f = Emp(31, "Varun", 45000.0)
```

the result is:

```text
f.age    = 31
f.name   = "Varun"
f.salary = 45000.0
```

### Output

```text
Age: 25 Name: Rahul Salary: 30000.0
Age: 31 Name: Varun Salary: 45000.0
```

---

# 22. Why `self.age = age` Is So Common

Using the same name on both sides is a common Python style:

```python
self.age = age
```

It can initially look confusing.

Remember:

```text
self.age
   ↓
Object's attribute

age
   ↓
Method parameter
```

Therefore:

```python
self.age = age
```

means:

> Store the value received in the `age` parameter inside the current object's `age` attribute.

---

# 23. Passing Different Values to Different Objects

This is the major advantage of a parameterized `__init__()`.

Example:

```python
e = Emp(25, "Rahul", 30000.0)
f = Emp(31, "Varun", 45000.0)
```

Both objects use the same class:

```text
Emp
```

but contain different values:

```text
e
├── age = 25
├── name = Rahul
└── salary = 30000

f
├── age = 31
├── name = Varun
└── salary = 45000
```

Therefore:

> **One class can create many objects, each with its own instance data.**

---

# 24. Can We Pass Different Numbers of Arguments?

The lecture asks whether we can make the program work with different numbers of arguments while creating `Emp` objects.

For example, something like:

```python
Emp("amit")
```

and:

```python
Emp("sumit", 23)
```

and:

```python
Emp("deepak", 34, 50000)
```

The answer given is:

> **Yes — use default arguments.**

---

# 25. Default Arguments in `__init__()`

A parameter can be given a default value.

Example:

```python
class Emp:
    def __init__(self, name, age=0, sal=0.0):
        self.name = name
        self.age = age
        self.sal = sal
```

Here:

```text
name → required
age  → default value 0
sal  → default value 0.0
```

Therefore, we can create objects with different numbers of supplied arguments.

---

# 26. Default Argument Example

The lecture's solution is:

```python
class Emp:
    def __init__(self, name, age=0, sal=0.0):
        self.name = name
        self.age = age
        self.sal = sal

e1 = Emp("amit")
e2 = Emp("sumit", 23)
e3 = Emp("deepak", 34, 50000)

print(e1.name)
print(e2.name, e2.age)
print(e3.name, e3.age, e3.sal)
```

### How it works

## Object 1

```python
e1 = Emp("amit")
```

Only `name` is supplied.

Therefore:

```text
name = "amit"
age  = 0
sal  = 0.0
```

---

## Object 2

```python
e2 = Emp("sumit", 23)
```

`name` and `age` are supplied.

Therefore:

```text
name = "sumit"
age  = 23
sal  = 0.0
```

---

## Object 3

```python
e3 = Emp("deepak", 34, 50000)
```

All three values are supplied.

Therefore:

```text
name = "deepak"
age  = 34
sal  = 50000
```

---

# 27. Default Arguments — Memory Diagram

```text
__init__(self, name, age=0, sal=0.0)
                    │       │
                    │       └── default = 0.0
                    └────────── default = 0
```

### Calls

```python
Emp("amit")
```

uses:

```text
age = 0
sal = 0.0
```

```python
Emp("sumit", 23)
```

uses:

```text
age = 23
sal = 0.0
```

```python
Emp("deepak", 34, 50000)
```

uses:

```text
age = 34
sal = 50000
```

---

# 28. Important Guess-the-Output: Multiple `__init__()` Definitions

The lecture contains an important output question:

```python
class Emp:
    def __init__(self, name):
        self.name = name

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __init__(self, name, age, sal):
        self.name = name
        self.age = age
        self.sal = sal

e1 = Emp("amit")
e2 = Emp("sumit", 23)
e3 = Emp("deepak", 34, 50000.0)

print(e1.name)
print(e2.name, e2.age)
print(e3.name, e3.age, e3.sal)
```

### Important concept

Python does **not** select between these three `__init__()` methods based on the number of arguments.

The later definition replaces the earlier definition.

Therefore, the effective `__init__()` is:

```python
def __init__(self, name, age, sal):
    self.name = name
    self.age = age
    self.sal = sal
```

As a result:

```python
e1 = Emp("amit")
```

does not match the final method because `age` and `sal` are missing.

So the program raises a `TypeError` when `e1` is created.

### Key lesson

> Defining multiple methods with the same name in a Python class does not create traditional method overloading. The later definition replaces the previous definition.

---

# 29. Why Default Arguments Solve the Problem

Instead of writing:

```python
def __init__(self, name):
    ...

def __init__(self, name, age):
    ...

def __init__(self, name, age, sal):
    ...
```

we can use one method:

```python
def __init__(self, name, age=0, sal=0.0):
    self.name = name
    self.age = age
    self.sal = sal
```

Now all of these are possible:

```python
Emp("amit")
Emp("sumit", 23)
Emp("deepak", 34, 50000)
```

This is the approach demonstrated in the lecture.

---

# 30. Complete Concept Flow

```text
                 Object Creation
                       │
                       ↓
                    Emp(...)
                       │
                       ↓
               __init__() called
                       │
                       ↓
             Current object → self
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
       Parameters             Instance data
       age/name/salary        self.age/name/salary
             │                   │
             ↓                   ↓
       Temporary values      Stored in object
```

---

# 31. `self` — Complete Summary

Remember these points:

### `self` refers to:

```text
Current object
```

### `self` is used to:

```text
Access instance attributes
Create instance attributes
Access the current object's data
```

### Syntax

```python
self.variable = value
```

### Example

```python
class Emp:
    def __init__(self, age, name, salary):
        self.age = age
        self.name = name
        self.salary = salary
```

---

# 32. Instance Variable Creation — Complete Summary

### Hardcoded

```python
class Emp:
    def __init__(self):
        self.age = 25
        self.name = "Rahul"
        self.salary = 30000.0
```

Problem:

```text
Every object receives the same values.
```

### Parameterized

```python
class Emp:
    def __init__(self, age, name, salary):
        self.age = age
        self.name = name
        self.salary = salary
```

Advantage:

```text
Different objects can receive different values.
```

### Default arguments

```python
class Emp:
    def __init__(self, name, age=0, sal=0.0):
        self.name = name
        self.age = age
        self.sal = sal
```

Advantage:

```text
Objects can be created with different numbers of supplied arguments.
```

---

# 33. Important Exam Questions

## Q1. What is the most important role of `self`?

`self` allows us to refer to the current object and dynamically create/access instance members.

---

## Q2. Can `self` be given another name?

Yes. The name `self` is a convention. Another parameter name can work, but `self` is the standard and recommended convention.

Example:

```python
class Emp:
    def __init__(myself):
        print("Object created. . .")
```

---

## Q3. Why must `self` be the first parameter?

Python passes the current object's reference as the first argument to an instance method.

---

## Q4. What is the difference between `age` and `self.age`?

```text
age
 ↓
Parameter/local variable

self.age
 ↓
Instance variable belonging to the current object
```

---

## Q5. What does this statement mean?

```python
self.age = age
```

It stores the value received by the `age` parameter in the `age` attribute of the current object.

---

## Q6. Why use a parameterized `__init__()`?

To initialize different objects with different instance data.

---

## Q7. Why use default arguments?

To allow objects to be created while supplying different numbers of arguments.

---

## Q8. What happens if multiple `__init__()` methods are defined?

The later definition replaces the earlier one; Python does not perform traditional constructor overloading based on argument count.

---

# 34. Quick Revision Table

| Concept | Meaning |
|---|---|
| `self` | Current object reference |
| `self.age` | `age` attribute of current object |
| `age` in `__init__(self, age)` | Local parameter |
| `__init__()` | Automatically called during object creation |
| Hardcoded attributes | Same initial values for every object |
| Parameterized `__init__()` | Allows different values for different objects |
| Default argument | Supplies a value when an argument is omitted |
| Multiple same-named `__init__()` | Later definition replaces earlier definition |

---

# 35. One-Minute Memory Map

```text
                     Emp(...)
                        │
                        ↓
                  __init__(...)
                        │
                        ↓
                      self
                        │
              ┌─────────┴─────────┐
              ↓                   ↓
          Parameters          Instance variables
       age/name/salary       self.age/self.name/...
              │                   │
              ↓                   ↓
       Temporary values      Stored in object
```

### Remember:

```python
self.age = age
```

means:

```text
object's age ← parameter age
```

And:

```python
Emp(25, "Rahul", 30000.0)
```

means:

```text
Create an Emp object
        ↓
Call __init__()
        ↓
Pass values
        ↓
Store them using self
```

---

## End of Part 3
==============================================================================================================================================================
