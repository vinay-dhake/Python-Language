# Python OOP — Inheritance, Single Inheritance, Constructors & `super()`

## 1. Inheritance

Inheritance is an important feature of Object-Oriented Programming (OOP).

It allows us to define a **new class from an existing class**.

The existing class is called the **base class**, **parent class**, or **superclass**.

The new class is called the **derived class**, **child class**, or **subclass**.

```text
Parent / Base Class
        │
        ▼
Child / Derived Class
```

A child class can reuse functionality already written in its parent class.

---

## 2. Real-Life Examples

### Bank accounts

A general `Account` class can contain common operations:

```text
Account
├── deposit()
└── withdraw()
```

Then classes such as:

```text
SavingAccount
CheckingAccount
```

can inherit those operations.

### Animal hierarchy

```text
                 Animal
                /      \
            Mammal     Reptile
            /   \         \
       Elephant Tiger   Crocodile
```

For example:

- `Elephant` is an `Animal`.
- `Tiger` is an `Animal`.
- `Crocodile` is an `Animal`.

Inheritance represents such real-world relationships naturally.

---

## 3. Benefits of Inheritance

### 3.1 Represents real-world relationships

Inheritance makes relationships such as:

```text
Animal → Mammal → Elephant
```

easy to model.

### 3.2 Code reusability

Common code can be written once in the parent and reused by child classes.

### 3.3 Adding features without modifying the parent

A child can add new methods and attributes while keeping the parent class unchanged.

```python
class Animal:

    def eat(self):
        print("It eats.")


class Bird(Animal):

    def fly(self):
        print("It flies in the sky.")
```

`Bird` gets `eat()` from `Animal` and adds `fly()`.

---

# 4. Types of Inheritance

The material identifies these forms of inheritance:

1. Single inheritance
2. Multiple inheritance
3. Multi-level inheritance
4. Hierarchical inheritance
5. Hybrid inheritance

This part focuses mainly on single inheritance and constructor behavior.

---

# 5. Single Inheritance

In **single inheritance**, one derived class inherits from one base class.

```text
Base Class
    │
    ▼
Derived Class
```

### Syntax

```python
class BaseClass:
    # body of base class
    pass


class DerivedClass(BaseClass):
    # body of derived class
    pass
```

Example:

```python
class Account:
    pass


class SavingAccount(Account):
    pass
```

Here:

- `Account` → parent/base class
- `SavingAccount` → child/derived class

---

# 6. Single Inheritance Example

```python
class Animal:

    def eat(self):
        print("It eats.")

    def sleep(self):
        print("It sleeps.")


class Bird(Animal):

    def set_type(self, type):
        self.type = type

    def fly(self):
        print("It flies in the sky.")

    def __str__(self):
        return "This is a " + self.type


duck = Bird()

duck.set_type("Duck")

print(duck)
duck.eat()
duck.sleep()
duck.fly()
```

### Output

```text
This is a Duck
It eats.
It sleeps.
It flies in the sky.
```

`Bird` does not define `eat()` or `sleep()`, but its object can call them because `Bird` inherits from `Animal`.

---

# 7. Using `super()`

Python provides `super()` to access members of a parent class from a child class.

It is especially useful for:

1. Calling the parent constructor.
2. Calling an overridden parent method.

Common syntax:

```python
super().__init__(...)
```

and:

```python
super().method_name(...)
```

---

# 8. How Constructors Behave in Inheritance

When a child object is created, Python looks for `__init__()` in the child class.

There are two important cases.

## Case 1: Child has no `__init__()`

```python
class A:

    def __init__(self):
        print("Instantiating A...")


class B(A):
    pass


b = B()
```

### Output

```text
Instantiating A...
```

Because `B` has no constructor of its own, the inherited constructor from `A` is used.

---

## Case 2: Child has its own `__init__()`

```python
class A:

    def __init__(self):
        print("Instantiating A...")


class B(A):

    def __init__(self):
        print("Instantiating B...")


b = B()
```

### Output

```text
Instantiating B...
```

The parent constructor is **not automatically called** when the child defines its own constructor.

This is an important Python rule.

---

# 9. Why Parent Constructor May Be Needed

Suppose the parent constructor creates important instance variables:

```python
class Rectangle:

    def __init__(self):
        self.l = 10
        self.b = 20
```

Now:

```python
class Cuboid(Rectangle):

    def __init__(self):
        self.h = 30

    def volume(self):
        print("Volume of cuboid is", self.l * self.b * self.h)
```

If we execute:

```python
obj = Cuboid()
obj.volume()
```

the parent constructor has not run, so `self.l` and `self.b` were never created.

This causes an `AttributeError`.

The problem is therefore not inheritance itself. The problem is that the initialization performed by the parent constructor did not happen.

---

# 10. Calling Parent Constructor Explicitly

There are two approaches:

1. Use the parent class name.
2. Use `super()`.

### Using the parent class name

```python
class Rectangle:

    def __init__(self):
        self.l = 10
        self.b = 20


class Cuboid(Rectangle):

    def __init__(self):
        Rectangle.__init__(self)
        self.h = 30

    def volume(self):
        print("Volume of cuboid is", self.l * self.b * self.h)


obj = Cuboid()
obj.volume()
```

### Output

```text
Volume of cuboid is 6000
```

Notice:

```python
Rectangle.__init__(self)
```

requires explicit `self`.

---

# 11. Calling Parent Constructor Using `super()`

The same example can be written as:

```python
class Rectangle:

    def __init__(self):
        self.l = 10
        self.b = 20


class Cuboid(Rectangle):

    def __init__(self):
        super().__init__()
        self.h = 30

    def volume(self):
        print("Volume of cuboid is", self.l * self.b * self.h)


obj = Cuboid()
obj.volume()
```

### Output

```text
Volume of cuboid is 6000
```

With:

```python
super().__init__()
```

we do not explicitly pass `self`.

---

# 12. What Is `super()`?

`super()` provides a special proxy object through which parent-side methods can be accessed.

For example:

```python
super().__init__()
```

accesses the appropriate parent constructor.

Similarly:

```python
super().display()
```

can access the corresponding parent implementation of `display()`.

---

# 13. Benefits of `super()`

Important advantages include:

- No need to explicitly pass `self`.
- Useful for calling parent constructors.
- Useful for calling overridden parent methods.
- Avoids unnecessarily hard-coding the parent class name.
- Helpful in multiple inheritance.

For example:

```python
Parent.__init__(self)
```

can become:

```python
super().__init__()
```

---

# 14. `super()` Does Not Have to Be the First Statement

Python does not require `super().__init__()` to be the first statement in a child constructor.

### Parent first

```python
class Vehicle:

    def __init__(self):
        print("Vehicle Created")


class Car(Vehicle):

    def __init__(self):
        super().__init__()
        print("Car Created")


c = Car()
```

Output:

```text
Vehicle Created
Car Created
```

### Child statement first

```python
class Car(Vehicle):

    def __init__(self):
        print("Car Created")
        super().__init__()
```

Output:

```text
Car Created
Vehicle Created
```

The execution order follows the order of statements in the constructor.

---

# 15. Constructor Summary

```text
Create child object
       │
       ▼
Does child define __init__()?
       │
   ┌───┴────┐
   │        │
  No       Yes
   │        │
   ▼        ▼
Use       Execute child
inherited constructor
constructor │
            ▼
       Parent constructor
       is NOT automatic
            │
            ▼
       use super().__init__()
       when parent initialization
       is required
```

---

# 16. Important Exam Points

- Inheritance provides code reuse.
- A parent is also called a base class.
- A child is also called a derived class.
- If a child has no `__init__()`, Python can use the inherited parent constructor.
- If a child defines its own `__init__()`, the parent constructor is not automatically called.
- `super().__init__()` can explicitly invoke parent initialization.
- `super()` does not require explicit `self`.
- `super()` can also be used for overridden methods.

# Python OOP — Method Overriding and `super()` in Overridden Methods

## 1. Method Overriding

**Method overriding** occurs when a derived class defines a method with the same name as a method already defined in its base class.

Example:

```python
class Parent:

    def display(self):
        print("Parent display")


class Child(Parent):

    def display(self):
        print("Child display")
```

Now:

```python
obj = Child()
obj.display()
```

Output:

```text
Child display
```

The child implementation is selected.

---

# 2. Why Method Overriding Is Used

A child class may need different behavior for a method that already exists in the parent.

For example:

```text
Circle.area()
    → πr²

Cylinder.area()
    → 2πr² + 2πrh
```

Both operations are called `area()`, but their behavior is different.

The child therefore overrides the parent method.

---

# 3. `Person` and `Employee` Example

```python
class Person:

    def __init__(self, age, name):
        self.age = age
        self.name = name

    def __str__(self):
        return f"Age: {self.age}, Name: {self.name}"


class Employee(Person):

    def __init__(self, age, name, emp_id, salary):
        super().__init__(age, name)
        self.emp_id = emp_id
        self.salary = salary


emp = Employee(24, "Nitin", 101, 50000)
print(emp)
```

Output:

```text
Age: 24, Name: Nitin
```

`Employee` does not define `__str__()`, so Python finds the inherited `Person.__str__()`.

---

# 4. Overriding `__str__()`

If we want all employee information:

```python
class Person:

    def __init__(self, age, name):
        self.age = age
        self.name = name

    def __str__(self):
        return f"Age:{self.age},Name:{self.name}"


class Employee(Person):

    def __init__(self, age, name, emp_id, salary):
        super().__init__(age, name)
        self.emp_id = emp_id
        self.salary = salary

    def __str__(self):
        return (
            f"Age:{self.age},Name:{self.name},"
            f"Id:{self.emp_id},Salary:{self.salary}"
        )


emp = Employee(24, "Nitin", 101, 45000)
print(emp)
```

Output:

```text
Age:24,Name:Nitin,Id:101,Salary:45000
```

Here:

```python
Employee.__str__()
```

overrides:

```python
Person.__str__()
```

---

# 5. Calling the Parent Version of an Overridden Method

Sometimes the child wants to keep the parent's behavior and then add its own behavior.

Use:

```python
super().method_name(...)
```

Example:

```python
class Parent:

    def display(self):
        print("Parent")


class Child(Parent):

    def display(self):
        print("Child")
        super().display()


obj = Child()
obj.display()
```

Output:

```text
Child
Parent
```

The child implementation runs first and explicitly calls the parent implementation.

---

# 6. `super()` Inside `__str__()`

Instead of rewriting the parent's formatting logic, the child can reuse it:

```python
class Person:

    def __init__(self, age, name):
        self.age = age
        self.name = name

    def __str__(self):
        return f"Age:{self.age},Name:{self.name}"


class Employee(Person):

    def __init__(self, age, name, emp_id, salary):
        super().__init__(age, name)
        self.emp_id = emp_id
        self.salary = salary

    def __str__(self):
        parent_string = super().__str__()
        return f"{parent_string},Id:{self.emp_id},Salary:{self.salary}"


emp = Employee(24, "Nitin", 101, 45000)
print(emp)
```

Output:

```text
Age:24,Name:Nitin,Id:101,Salary:45000
```

The parent handles:

```text
Age
Name
```

and the child adds:

```text
ID
Salary
```

---

# 7. Circle and Cylinder — Complete Example

This example demonstrates inheritance, constructor chaining, overriding, and `super()`.

```python
import math


class Circle:

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * math.pow(self.radius, 2)


class Cylinder(Circle):

    def __init__(self, radius, height):
        super().__init__(radius)
        self.height = height

    def area(self):
        return (
            2 * super().area()
            + 2 * math.pi * self.radius * self.height
        )

    def volume(self):
        return super().area() * self.height


obj = Cylinder(5, 10)

print("Area of Cylinder:", obj.area())
print("Volume of Cylinder:", obj.volume())
```

Output:

```text
Area of Cylinder: 471.23889803846897
Volume of Cylinder: 785.3981633974483
```

---

# 8. Understanding `Cylinder.__init__()`

```python
def __init__(self, radius, height):
    super().__init__(radius)
    self.height = height
```

The parent constructor creates:

```python
self.radius
```

The child creates:

```python
self.height
```

Therefore the final object contains both values.

---

# 9. Understanding the Overridden `area()`

Circle area:

```text
πr²
```

Cylinder total surface area:

```text
2πr² + 2πrh
```

The child reuses the parent's circle-area calculation:

```python
super().area()
```

Therefore:

```python
2 * super().area() + 2 * math.pi * self.radius * self.height
```

is equivalent to:

```text
2πr² + 2πrh
```

---

# 10. Understanding `volume()`

Cylinder volume:

```text
πr²h
```

The parent method returns:

```text
πr²
```

Therefore:

```python
return super().area() * self.height
```

calculates:

```text
πr² × h = πr²h
```

---

# 11. Calling the Parent Method Directly

Suppose:

```python
obj = Cylinder(5, 10)
```

Then:

```python
obj.area()
```

calls the overridden `Cylinder.area()`.

But:

```python
Circle.area(obj)
```

directly invokes the parent implementation.

This is a useful distinction.

```text
obj.area()
     ↓
Cylinder.area()

Circle.area(obj)
     ↓
Circle.area()
```

---

# 12. Guess-the-Output Example

```python
class Person:

    def __init__(self, age, name):
        self.age = age
        self.name = name

    def __str__(self):
        return f"Age:{self.age},Name:{self.name}"


class Emp(Person):

    def __init__(self, age, name, emp_id, salary):
        super().__init__(age, name)
        self.emp_id = emp_id
        self.salary = salary


e = Emp(24, "Nitin", 101, 45000)
print(e)
```

Output:

```text
Age:24,Name:Nitin
```

### Reason

`Emp` does not override `__str__()`.

Python searches the inheritance chain and finds:

```python
Person.__str__()
```

Therefore only `age` and `name` are displayed.

---

# 13. Modified Version

Now redefine `__str__()`:

```python
class Emp(Person):

    def __init__(self, age, name, emp_id, salary):
        super().__init__(age, name)
        self.emp_id = emp_id
        self.salary = salary

    def __str__(self):
        return (
            f"Age:{self.age},Name:{self.name},"
            f"Id:{self.emp_id},Salary:{self.salary}"
        )
```

Output:

```text
Age:24,Name:Nitin,Id:101,Salary:45000
```

This is method overriding.

---

# 14. Important Distinction

### Overriding

Child defines the same method:

```python
def display(self):
```

This gives the child its own implementation.

### `super()`

Used when the child wants to access the parent implementation:

```python
super().display()
```

Therefore:

```text
Overriding
    ↓
Child provides its own implementation

super()
    ↓
Child can reuse parent implementation
```

---

# 15. Direct Parent Call vs `super()`

### Direct call

```python
Circle.area(obj)
```

or:

```python
Rectangle.__init__(self)
```

The parent class name is explicitly written.

### `super()`

```python
super().area()
```

or:

```python
super().__init__()
```

The inheritance relationship is used without explicitly naming the parent.

---

# 16. Exam Points

- Method overriding occurs when a child redefines an inherited method.
- When called through a child object, the child implementation is normally selected.
- `super()` can be used to access the parent implementation.
- `super().__init__()` is useful for constructor chaining.
- `super().method()` is useful inside overridden methods.
- `BaseClass.method(derived_object)` can directly call a base implementation from outside the child class.
- `__str__()` is inherited like other methods and can be overridden.

---

# Quick Revision

```text
Parent method
     ↓
Child defines same method
     ↓
Method overriding
     ↓
Child version executes
     ↓
Need parent version?
     ↓
super().method()
```

# Python OOP — Multi-Level Inheritance, Hierarchical Inheritance, `issubclass()` and `isinstance()`

## 1. Multi-Level Inheritance

In **multi-level inheritance**, a class inherits from another class which itself inherits from another class.

```text
Class A
   │
   ▼
Class B
   │
   ▼
Class C
```

This can be written as:

```text
A → B → C
```

Here:

- `A` is the top-level parent.
- `B` is a child of `A`.
- `B` is also the direct parent of `C`.
- `C` is the final derived class in this chain.

---

# 2. Example: Manager → Reviewer → Developer

```python
class Manager:

    def final_review(self):
        print("Final Review Done by Manager")


class Reviewer(Manager):

    def review(self):
        print("Reviewing Done by Reviewer")


class Developer(Reviewer):

    def write_code(self):
        print("Code Written by Developer")


dev = Developer()

dev.write_code()
dev.review()
dev.final_review()
```

### Output

```text
Code Written by Developer
Reviewing Done by Reviewer
Final Review Done by Manager
```

The `Developer` object can use:

```python
write_code()
```

from its own class,

```python
review()
```

from `Reviewer`, and

```python
final_review()
```

from `Manager`.

The inheritance chain is:

```text
Developer
    ↓
Reviewer
    ↓
Manager
```

---

# 3. Multi-Level Method Overriding with `super()`

Different levels of the hierarchy can override the same method.

```python
class Manager:

    def review(self):
        print("Final Review Done by Manager")


class Reviewer(Manager):

    def review(self):
        print("Reviewing Done by Reviewer")
        super().review()


class Developer(Reviewer):

    def review(self):
        print("Code Reviewing by Developer")
        super().review()


dev = Developer()
dev.review()
```

### Output

```text
Code Reviewing by Developer
Reviewing Done by Reviewer
Final Review Done by Manager
```

---

# 4. Understanding the `super()` Chain

Execution starts with:

```python
dev.review()
```

Python selects:

```python
Developer.review()
```

Inside it:

```python
super().review()
```

continues to the next implementation:

```python
Reviewer.review()
```

Then `Reviewer` executes:

```python
super().review()
```

which reaches:

```python
Manager.review()
```

So the chain is:

```text
Developer.review()
        ↓
Reviewer.review()
        ↓
Manager.review()
```

This is one reason `super()` is especially useful in inheritance chains.

---

# 5. Three-Level Employee Hierarchy

A useful multi-level structure is:

```text
Person
   ↓
Employee
   ↓
Manager
```

### `Person`

Contains:

- `name`
- `age`
- `__init__()`
- `__str__()`

### `Employee`

Adds:

- `emp_id`
- `salary`
- `income()`
- `__init__()`
- `__str__()`

### `Manager`

Adds:

- `bonus`
- `income()`
- `__init__()`
- `__str__()`

---

# 6. Complete Example

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Name: {self.name}, Age: {self.age}"


class Employee(Person):

    def __init__(self, name, age, emp_id, salary):
        super().__init__(name, age)
        self.emp_id = emp_id
        self.salary = salary

    def income(self):
        return self.salary

    def __str__(self):
        return (
            f"{super().__str__()}, "
            f"ID: {self.emp_id}, Salary: {self.salary}"
        )


class Manager(Employee):

    def __init__(self, name, age, emp_id, salary, bonus):
        super().__init__(name, age, emp_id, salary)
        self.bonus = bonus

    def income(self):
        return self.salary + self.bonus

    def __str__(self):
        return f"{super().__str__()}, Bonus: {self.bonus}"


mgr = Manager("Rahul", 35, 1001, 80000, 20000)

print("Full Details:", mgr)
print("Salary:", mgr.salary)
print("Total Income:", mgr.income())
```

### Output

```text
Full Details: Name: Rahul, Age: 35, ID: 1001, Salary: 80000, Bonus: 20000
Salary: 80000
Total Income: 100000
```

---

# 7. Constructor Chain in the Example

When this runs:

```python
mgr = Manager("Rahul", 35, 1001, 80000, 20000)
```

`Manager.__init__()` executes.

It calls:

```python
super().__init__(name, age, emp_id, salary)
```

which calls `Employee.__init__()`.

`Employee.__init__()` then calls:

```python
super().__init__(name, age)
```

which calls `Person.__init__()`.

The initialization chain is therefore:

```text
Manager.__init__()
       ↓
Employee.__init__()
       ↓
Person.__init__()
```

The attributes are created step by step:

```text
Person:
    name
    age

Employee:
    emp_id
    salary

Manager:
    bonus
```

The final object contains all five attributes.

---

# 8. Method Overriding in the Employee Example

`Employee` defines:

```python
def income(self):
    return self.salary
```

`Manager` defines:

```python
def income(self):
    return self.salary + self.bonus
```

The `Manager` version overrides the `Employee` version.

For:

```text
salary = 80000
bonus = 20000
```

the manager's income is:

```text
80000 + 20000 = 100000
```

---

# 9. Hierarchical Inheritance

In **hierarchical inheritance**, multiple child classes inherit from one common parent.

```text
             Parent
             /    \
            /      \
        Child 1   Child 2
```

Common attributes and methods are placed in the shared parent.

---

# 10. Polygon → Rectangle / Triangle

The example hierarchy is:

```text
             Polygon
             /     \
            /       \
     Rectangle     Triangle
```

`Polygon` stores common dimensions.

`Rectangle` and `Triangle` provide their own `area()` implementations.

---

# 11. Complete Hierarchical Example

```python
class Polygon:

    def __init__(self, dim1, dim2):
        self.dim1 = dim1
        self.dim2 = dim2

    def __str__(self):
        return f"Dim1: {self.dim1}, Dim2: {self.dim2}"


class Rectangle(Polygon):

    def area(self):
        return self.dim1 * self.dim2


class Triangle(Polygon):

    def area(self):
        return 0.5 * self.dim1 * self.dim2


r = Rectangle(10, 20)
t = Triangle(5, 7)

print("Rectangle Dimensions:", r)
print("Rectangle Area:", r.area())

print("Triangle Dimensions:", t)
print("Triangle Area:", t.area())
```

### Output

```text
Rectangle Dimensions: Dim1: 10, Dim2: 20
Rectangle Area: 200
Triangle Dimensions: Dim1: 5, Dim2: 7
Triangle Area: 17.5
```

Both children inherit:

```python
__init__()
__str__()
```

from `Polygon`.

But each child supplies its own:

```python
area()
```

implementation.

---

# 12. Multi-Level vs Hierarchical Inheritance

| Feature | Multi-Level | Hierarchical |
|---|---|---|
| Structure | A → B → C | A → B and A → C |
| Main idea | Inheritance chain | Multiple children share a parent |
| Example | Person → Employee → Manager | Polygon → Rectangle/Triangle |
| Shape | Chain | Branch/tree |

### Memory trick

```text
Multi-Level = chain

A
↓
B
↓
C
```

```text
Hierarchical = branches

   A
  / \
 B   C
```

---

# 13. `issubclass()`

Python provides the built-in function:

```python
issubclass()
```

to check whether one class is a subclass of another class.

### Syntax

```python
issubclass(DerivedClass, BaseClass)
```

It returns:

```text
True
```

or:

```text
False
```

---

# 14. `issubclass()` Example

```python
class MyBase:
    pass


class MyDerived(MyBase):
    pass


print(issubclass(MyDerived, MyBase))
```

Output:

```text
True
```

because:

```text
MyDerived
    ↓
MyBase
```

---

# 15. Direct and Indirect Inheritance

Consider:

```python
class MyBase:
    pass


class MyDerived(MyBase):
    pass
```

### Direct inheritance

```python
issubclass(MyDerived, MyBase)
```

returns:

```text
True
```

### Inheritance from `object`

Python classes ultimately inherit from `object`.

Therefore:

```python
issubclass(MyBase, object)
```

returns:

```text
True
```

and:

```python
issubclass(MyDerived, object)
```

also returns:

```text
True
```

because:

```text
MyDerived
    ↓
MyBase
    ↓
object
```

But:

```python
issubclass(MyBase, MyDerived)
```

returns:

```text
False
```

because the parent is not a subclass of its child.

### Complete example

```python
class MyBase:
    pass


class MyDerived(MyBase):
    pass


print(issubclass(MyDerived, MyBase))
print(issubclass(MyBase, object))
print(issubclass(MyDerived, object))
print(issubclass(MyBase, MyDerived))
```

Output:

```text
True
True
True
False
```

---

# 16. `isinstance()`

`isinstance()` checks whether an object is an instance of a specified class or one of its parent classes.

### Syntax

```python
isinstance(object, ClassName)
```

It returns:

```text
True
```

or:

```text
False
```

---

# 17. `isinstance()` Example

```python
class MyBase:
    pass


class MyDerived(MyBase):
    pass


d = MyDerived()
b = MyBase()

print(isinstance(d, MyBase))
print(isinstance(d, MyDerived))
print(isinstance(d, object))
print(isinstance(b, MyBase))
print(isinstance(b, MyDerived))
print(isinstance(b, object))
```

### Output

```text
True
True
True
True
False
True
```

---

# 18. Why Is `isinstance(d, MyBase)` True?

We created:

```python
d = MyDerived()
```

So `d` is directly an instance of `MyDerived`.

But:

```text
MyDerived
    ↓
MyBase
```

Therefore the object is also considered an instance of `MyBase`.

And because:

```text
MyBase
    ↓
object
```

it is also an instance of `object`.

Therefore:

```python
isinstance(d, MyDerived)  # True
isinstance(d, MyBase)     # True
isinstance(d, object)     # True
```

---

# 19. Why Is `isinstance(b, MyDerived)` False?

Here:

```python
b = MyBase()
```

The object belongs to the parent class.

It is not automatically an instance of the child class.

Therefore:

```python
isinstance(b, MyDerived)
```

returns:

```text
False
```

An object of a child class can also be considered an object of its parent class, but the reverse is not true.

---

# 20. `issubclass()` vs `isinstance()`

This is an important distinction.

| Function | Checks | Example |
|---|---|---|
| `issubclass()` | Class-to-class relationship | `issubclass(MyDerived, MyBase)` |
| `isinstance()` | Object-to-class relationship | `isinstance(d, MyBase)` |

### Easy memory trick

```text
issubclass()
     ↓
class ↔ class
```

```text
isinstance()
     ↓
object ↔ class
```

---

# 21. Common Exam Traps

### Trap 1

Do not confuse:

```python
issubclass()
```

with:

```python
isinstance()
```

Use:

```python
issubclass(Child, Parent)
```

for a class relationship.

Use:

```python
isinstance(obj, Parent)
```

for an object relationship.

### Trap 2

A parent object is not automatically a child object.

```python
b = MyBase()

isinstance(b, MyDerived)
```

is:

```text
False
```

### Trap 3

A child object can satisfy an `isinstance()` test for its parent:

```python
d = MyDerived()

isinstance(d, MyBase)
```

is:

```text
True
```

# Python OOP — Circle/Cylinder Exercise, Solutions & Final Revision

## 1. Circle and Cylinder Exercise

Create a class called `Circle`.

It should contain an instance member:

```python
radius
```

and these methods:

### `__init__()`

Accept a radius and initialize the instance variable.

### `area()`

Calculate:

```text
πr²
```

Then create a derived class:

```text
Circle
   ↓
Cylinder
```

`Cylinder` should contain:

```python
height
```

and provide:

### `__init__()`

Initialize both:

```text
radius
height
```

### `area()`

Override `Circle.area()` and calculate:

```text
2πr² + 2πrh
```

### `volume()`

Calculate:

```text
πr²h
```

---

# 2. Solution

```python
import math


class Circle:

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * math.pow(self.radius, 2)


class Cylinder(Circle):

    def __init__(self, radius, height):
        super().__init__(radius)
        self.height = height

    def area(self):
        return (
            2 * super().area()
            + 2 * math.pi * self.radius * self.height
        )

    def volume(self):
        return super().area() * self.height


obj = Cylinder(10, 20)

print("Area of cylinder is", obj.area())
print("Volume of cylinder is", obj.volume())
```

### Output

```text
Area of cylinder is 1884.9555921538758
Volume of cylinder is 6283.185307179587
```

---

# 3. Step-by-Step Execution

When:

```python
obj = Cylinder(10, 20)
```

is executed, `Cylinder.__init__()` runs.

Inside it:

```python
super().__init__(10)
```

calls the parent constructor:

```python
Circle.__init__(10)
```

which creates:

```python
self.radius = 10
```

Then the child constructor creates:

```python
self.height = 20
```

The final object contains:

```text
radius = 10
height = 20
```

---

# 4. Calculating Cylinder Area

The formula is:

```text
2πr² + 2πrh
```

The parent method already calculates:

```text
πr²
```

Therefore:

```python
2 * super().area() + 2 * math.pi * self.radius * self.height
```

provides the required formula.

For:

```text
r = 10
h = 20
```

the result is:

```text
600π
```

which is approximately:

```text
1884.9555921538758
```

---

# 5. Calculating Cylinder Volume

The formula is:

```text
πr²h
```

The parent method gives:

```text
πr²
```

Therefore:

```python
super().area() * self.height
```

gives:

```text
πr²h
```

For:

```text
r = 10
h = 20
```

the result is:

```text
2000π
```

which is approximately:

```text
6283.185307179587
```

---

# 6. Calling the Parent Version from Outside the Child

Suppose:

```python
obj = Cylinder(10, 20)
```

Then:

```python
obj.area()
```

calls the overridden method:

```python
Cylinder.area()
```

If we specifically want the parent implementation:

```python
Circle.area(obj)
```

can be used.

### Syntax

```python
BaseClass.method_name(derived_object)
```

Example:

```python
print("Area of Circle:", Circle.area(obj))
```

This directly invokes `Circle.area()` using `obj` as the instance.

---

# 7. Complete Example

```python
import math


class Circle:

    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return math.pi * math.pow(self.radius, 2)


class Cylinder(Circle):

    def __init__(self, radius, height):
        super().__init__(radius)
        self.height = height

    def area(self):
        return (
            2 * super().area()
            + 2 * math.pi * self.radius * self.height
        )

    def volume(self):
        return super().area() * self.height


obj = Cylinder(10, 20)

print("Area of cylinder is", obj.area())
print("Volume of cylinder is", obj.volume())
print("Area of Circle:", Circle.area(obj))
```

The calls mean:

```python
obj.area()
```

→ `Cylinder.area()`

```python
obj.volume()
```

→ `Cylinder.volume()`

```python
Circle.area(obj)
```

→ `Circle.area()` directly

---

# 8. Important Concepts at a Glance

## Inheritance

Creating a new class from an existing class.

```python
class Child(Parent):
    pass
```

## Base / Parent Class

The class whose functionality is inherited.

## Derived / Child Class

The class that inherits from another class.

## Single Inheritance

```text
A
↓
B
```

## Multi-Level Inheritance

```text
A
↓
B
↓
C
```

## Hierarchical Inheritance

```text
    A
   / \
  B   C
```

## Method Overriding

A child defines a method with the same name as an inherited parent method.

## `super()`

Used to access the appropriate parent-side implementation.

```python
super().__init__()
```

or:

```python
super().method()
```

## `issubclass()`

Checks a class-to-class relationship:

```python
issubclass(Child, Parent)
```

## `isinstance()`

Checks an object-to-class relationship:

```python
isinstance(obj, Parent)
```

---

# 9. Parent Class Name vs `super()`

### Direct parent call

```python
Parent.__init__(self)
```

or:

```python
Parent.method(self)
```

The parent class name is explicitly written.

### `super()`

```python
super().__init__()
```

or:

```python
super().method()
```

No explicit `self` is required.

`super()` is especially useful when inheritance relationships become more complex.

---

# 10. Constructor Behavior

### Child has no constructor

```python
class A:

    def __init__(self):
        print("A")


class B(A):
    pass


B()
```

Output:

```text
A
```

### Child has its own constructor

```python
class A:

    def __init__(self):
        print("A")


class B(A):

    def __init__(self):
        print("B")


B()
```

Output:

```text
B
```

### Child explicitly calls parent

```python
class B(A):

    def __init__(self):
        super().__init__()
        print("B")
```

Output:

```text
A
B
```

---

# 11. Method Overriding

```python
class A:

    def display(self):
        print("A")


class B(A):

    def display(self):
        print("B")


B().display()
```

Output:

```text
B
```

The child implementation is selected.

To call the parent version:

```python
class B(A):

    def display(self):
        print("B")
        super().display()
```

Output:

```text
B
A
```

---

# 12. Multi-Level `super()` Chain

```text
Developer
    ↓
Reviewer
    ↓
Manager
```

If all three override `review()` and each calls:

```python
super().review()
```

the call can proceed:

```text
Developer.review()
        ↓
Reviewer.review()
        ↓
Manager.review()
```

This is an important pattern in inheritance.

---

# 13. `issubclass()` Quick Examples

```python
class A:
    pass


class B(A):
    pass
```

Then:

```python
issubclass(B, A)
```

→ `True`

```python
issubclass(A, B)
```

→ `False`

```python
issubclass(B, object)
```

→ `True`

because the chain is:

```text
B → A → object
```

---

# 14. `isinstance()` Quick Examples

```python
a = A()
b = B()
```

Then:

```python
isinstance(b, B)
```

→ `True`

```python
isinstance(b, A)
```

→ `True`

```python
isinstance(b, object)
```

→ `True`

But:

```python
isinstance(a, B)
```

→ `False`

because an object of the parent class is not automatically an object of the child class.

---

# 15. Common Exam Questions

## Theory

1. What is inheritance?
2. Explain the benefits of inheritance.
3. What is a base class?
4. What is a derived class?
5. Explain single inheritance.
6. Explain multi-level inheritance.
7. Explain hierarchical inheritance.
8. What is method overriding?
9. What is `super()`?
10. Why is `super()` used?
11. Explain constructor behavior in inheritance.
12. What happens when a child class does not define `__init__()`?
13. What happens when a child class defines `__init__()`?
14. What is `issubclass()`?
15. What is `isinstance()`?
16. Differentiate `issubclass()` and `isinstance()`.

---

# 16. Programming Questions

### Question 1

Create:

```text
Animal
   ↓
Bird
```

Put `eat()` and `sleep()` in `Animal` and `fly()` in `Bird`.

Demonstrate inherited and child methods.

### Question 2

Create:

```text
Person
   ↓
Employee
```

Use `super()` for initialization and override `__str__()`.

### Question 3

Create:

```text
Person
   ↓
Employee
   ↓
Manager
```

Add salary and bonus and override `income()`.

### Question 4

Create:

```text
Polygon
   /    \
Rectangle Triangle
```

Implement `area()` differently in the two child classes.

### Question 5

Create:

```text
Circle
   ↓
Cylinder
```

Implement `area()` and `volume()` using `super()`.

---

# 17. Final Memory Map

```text
                         INHERITANCE
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
      Single               Multi-Level          Hierarchical
        │                     │                     │
       A → B                A → B → C             A → B
                                                   A → C
        │
        ▼
   Constructor
        │
   ┌────┴─────┐
   │          │
No child    Child has
__init__    __init__
   │          │
   ▼          ▼
Inherited   Parent constructor
constructor not automatic
              │
              ▼
       super().__init__()
```

```text
                   METHOD OVERRIDING
                          │
               Child defines same method
                          │
                          ▼
                  Child implementation
                          │
                  Need parent version?
                          │
                          ▼
                  super().method()
```

```text
                    TYPE CHECKING
                         │
              ┌──────────┴──────────┐
              │                     │
         issubclass()          isinstance()
              │                     │
          class/class           object/class
```

---

# 18. Final Revision Table

| Concept | Main Idea | Typical Syntax |
|---|---|---|
| Inheritance | Reuse functionality from another class | `class B(A):` |
| Base class | Parent class | `class A:` |
| Derived class | Child class | `class B(A):` |
| Single inheritance | One parent → one child | `A → B` |
| Multi-level inheritance | Multiple inheritance levels | `A → B → C` |
| Hierarchical inheritance | One parent → multiple children | `A → B`, `A → C` |
| Constructor inheritance | Child uses inherited constructor | `class B(A): pass` |
| `super()` | Access parent-side implementation | `super().method()` |
| Constructor chaining | Parent and child initialization | `super().__init__()` |
| Method overriding | Child redefines inherited method | Same method name |
| Parent overridden method | Reuse parent implementation | `super().method()` |
| Direct parent call | Call base implementation directly | `A.method(obj)` |
| `issubclass()` | Tests class relationship | `issubclass(B, A)` |
| `isinstance()` | Tests object relationship | `isinstance(obj, A)` |

---

# 19. Final Key Points

1. Inheritance promotes code reuse.
2. Parent and base class refer to the class being inherited from.
3. Child and derived class refer to the class that inherits.
4. If the child has no `__init__()`, the inherited constructor can be used.
5. If the child defines `__init__()`, the parent constructor is not automatically executed.
6. `super().__init__()` can explicitly call parent initialization.
7. `super()` does not require explicit `self`.
8. `super().method()` can access the parent implementation of an overridden method.
9. Method overriding means redefining an inherited method in the child.
10. Multi-level inheritance forms a chain.
11. Hierarchical inheritance forms branches from a common parent.
12. `issubclass()` checks a class relationship.
13. `isinstance()` checks an object relationship.
14. A child object can be considered an instance of its parent class.
15. A parent object is not automatically an instance of its child class.
16. `BaseClass.method(derived_object)` can directly invoke a base-class implementation from outside the derived class.
