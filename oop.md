# Python OOP & SOLID -- Cheat Sheet

A practical beginner-to-intermediate reference with **what it is, why it
is useful, and small examples**. Examples use Python 3.

------------------------------------------------------------------------

# Part 1: Object-Oriented Programming (OOP)

## 1. What is OOP?

**Object-Oriented Programming** is a way of organizing a program around
objects that contain data and behaviour.

-   **Data** is represented by attributes (variables).
-   **Behaviour** is represented by methods (functions inside a class).

**Why use OOP?** It helps group related code, reuse behaviour, represent
real-world concepts, and maintain larger programs.

Example: A `BankAccount` has data such as account holder and balance,
and behaviour such as deposit and withdraw. 

It is a programming paradigm in which we organise code around objects rather than just functions.

An object contains:
- Data (Attributes)
- Behaviour (Methods)
For example:

A student has:
- Name
- Age
- Roll number
And can perform actions:
- Study
- Attend class
- Submit assignments
That's the basic idea of OOPs.
2. Classes and Objects (3 minutes)
These are the most fundamental concepts of OOPs.
What is a Class?
A class is a blueprint or template used to create objects.

Example:

Think about a house blueprint.

A blueprint describes:
- Number of rooms
- Doors
- Windows
- Structure
But the blueprint itself isn't a physical house.

Similarly, a class defines the structure and behaviour of objects.
What is an Object?
An object is an instance of a class.

Let's see this in Python.
class Student:    def study(self):        print("Student is studying")student1 = Student()student2 = Student()student1.study()student2.study()


Output:
Student is studying
Student is studying

Explanation:
- class Student → Defines a class.
- student1 → First object.
- student2 → Second object.
- study() → Method.
- self → Refers to the current object.

## 2. Class and Object

-   **Class:** A blueprint that describes the attributes and methods its
    objects can have.
-   **Object:** A particular instance created from a class.

```python
class Car:
    def start(self):
        print("Car started")


car1 = Car()
car2 = Car()

car1.start()
car2.start()
```

**Output**

```text
Car started
Car started
```

**Why?** One class can be used to create many independent objects.

## 3. `self`

`self` refers to the current object. It lets an instance method read or
update the data belonging to the object on which it was called.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(self.name)


student1 = Student("Jyothish")
student2 = Student("Rahul")

student1.display()
student2.display()
```

**Output**

```text
Jyothish
Rahul
```

When `student1.display()` is called, Python passes `student1` as the
first argument automatically. `self` is a convention, not a reserved
keyword, but use that name.

**Java comparison:** Python `self` is similar to Java `this`, but Python
requires it to be written explicitly in the method definition.

## 4. `__init__()` -- Object initialization

`__init__()` runs automatically after a new object is created. It
initializes that object's starting data.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(f"{self.name}, {self.age}")


student = Student("Jyothish", 23)
student.display()
```

**Output**

```text
Jyothish, 23
```

**Why use it?** It puts an object into a useful starting state at
creation time. Without it, you would have to assign attributes
separately and could forget required data.

**Important:** `__init__()` initializes an object; `__new__()` is
responsible for creating it. In everyday application code, you usually
write `__init__()`.

## 5. Instance Variables and Class Variables

### Instance variables

Belong to an individual object. Different objects can store different
values.

### Class variables

Declared in the class body and shared through the class by its
instances.

```python
class Employee:
    company = "MountBlue"  # class variable

    def __init__(self, name, salary):
        self.name = name       # instance variable
        self.salary = salary   # instance variable


first = Employee("Jyothish", 30000)
second = Employee("Rahul", 40000)

print(first.name, first.salary, first.company)
print(second.name, second.salary, second.company)
```

**Output**

```text
Jyothish 30000 MountBlue
Rahul 40000 MountBlue
```

Changing `Employee.company` changes the class value seen by instances
that have not shadowed it. Assigning `first.company = "Google"`
creates/updates an instance attribute for `first`; it does not change
the class variable.

**Use:** Instance variables store object-specific information. Class
variables store information common to the class.

## 6. Three Types of Methods

All three are useful, but they serve different purposes.

### A. Instance method -- acts on one object

-   First parameter is conventionally `self`.
-   Can access and modify instance data.
-   Can also access class data.

**Scenario:** Increase the salary of one employee.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def increase_salary(self, amount):
        self.salary += amount


employee = Employee("Jyothish", 30000)
employee.increase_salary(5000)
print(employee.salary)
```

**Output:** `35000`

**Why?** The method needs to know which employee's salary should change.

### B. Class method -- acts on the class

-   Uses the `@classmethod` decorator.
-   First parameter is conventionally `cls`, referring to the class.
-   Can read or update class-level data.
-   Often used for alternative constructors.

**Scenario:** Change the company name for the class.

```python
class Employee:
    company = "MountBlue"

    @classmethod
    def change_company(cls, new_name):
        cls.company = new_name


Employee.change_company("Google")
print(Employee.company)
```

**Output:** `Google`

**Why?** Changing a shared class setting should not require a particular
employee object.

Alternative constructor example:

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @classmethod
    def from_text(cls, text):
        name, salary = text.split(",")
        return cls(name, int(salary))


employee = Employee.from_text("Jyothish,30000")
print(employee.name, employee.salary)
```

**Output:** `Jyothish 30000`

### C. Static method -- related utility, no automatic object/class argument

-   Uses the `@staticmethod` decorator.
-   Does not receive `self` or `cls` automatically.
-   Useful for a helper operation related to the class.

**Scenario:** Validate a salary value.

```python
class Employee:
    @staticmethod
    def is_valid_salary(salary):
        return salary > 0


print(Employee.is_valid_salary(30000))
print(Employee.is_valid_salary(-500))
```

**Output**

```text
True
False
```

**Why?** Validation only needs the supplied value; it does not need an
employee object or class state.

### Method comparison

| Method | First parameter | Best used when |
| :--- | :--- | :--- |
| Instance | `self` | Working with one object's data |
| Class | `cls` | Working with class-level data or creating objects another way |
| Static | None automatically | A related helper does not need object/class data |

A normal instance method can technically read class variables too.
Choose the method type based on what the operation needs and make that
intention clear.

------------------------------------------------------------------------

# Part 2: The Four Pillars of OOP

## 7. Encapsulation

**Meaning:** Keep related data and the methods that operate on it
together, and control how important data is changed.

Python does not enforce Java-style access modifiers. It uses naming
conventions:

-   `name` -- public; normal access.
-   `_balance` -- non-public by convention; intended for internal use.
-   `__balance` -- name-mangled by Python to reduce accidental
    access/name clashes. It is not truly private.

**Scenario:** Prevent a bank balance from being reduced through an
invalid withdrawal.

```python
class BankAccount:
    def __init__(self, balance):
        self._balance = balance

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self._balance:
            self._balance -= amount

    def get_balance(self):
        return self._balance


account = BankAccount(1000)
account.withdraw(300)
print(account.get_balance())
```

**Output:** `700`

**Why?** The class provides controlled operations instead of asking
outside code to change the balance directly.

### Property -- controlled attribute access

`@property` lets a method be accessed like an attribute. It is commonly
used for validation.

```python
class Product:
    def __init__(self, price):
        self.price = price

    @property
    def price(self):
        return self._price

    @price.setter
    def price(self, value):
        if value < 0:
            raise ValueError("Price cannot be negative")
        self._price = value


product = Product(500)
product.price = 750
print(product.price)
```

**Output:** `750`

## 8. Inheritance

**Meaning:** A child class reuses or extends the attributes and methods of a parent class.

**Why?** Avoid repeating common behaviour and represent an "is-a" relationship.

### Common inheritance patterns
| Type | Meaning |
| :--- | :--- |
| Single | One child inherits from one parent |
| Multiple | One child inherits from multiple parents |
| Multilevel | A class inherits from a child class, forming a chain |
| Hierarchical | Multiple child classes inherit from one parent |
| Hybrid | Combination of inheritance patterns |

### 1. Single Inheritance
One child inherits from one parent.

```python
class Employee:
    def work(self):
        print("Employee is working")

class Developer(Employee):
    def code(self):
        print("Developer is coding")

developer = Developer()
developer.work()
developer.code()
```

### 2. Multiple Inheritance
One child inherits from two or more parents.

```python
class Camera:
    def take_photo(self):
        print("Photo captured")

class Phone:
    def make_call(self):
        print("Calling...")

class SmartPhone(Camera, Phone):
    pass

device = SmartPhone()
device.take_photo()
device.make_call()
```

### 3. Multilevel Inheritance
A child class inherits from another child class, forming a grandfather-father-child chain.

```python
class Animal:
    def breathe(self):
        print("Breathing...")

class Dog(Animal):
    def bark(self):
        print("Barking...")

class Puppy(Dog):
    def weep(self):
        print("Weeping...")

puppy = Puppy()
puppy.breathe() # From Animal
puppy.bark()    # From Dog
puppy.weep()    # From Puppy
```

### 4. Hierarchical Inheritance
Multiple child classes inherit from a single parent class.

```python
class Shape:
    def draw(self):
        print("Drawing a shape")

class Circle(Shape):
    def draw_circle(self):
        print("Drawing a circle")

class Square(Shape):
    def draw_square(self):
        print("Drawing a square")

circle = Circle()
square = Square()
circle.draw() # Both share the parent method
square.draw()
```

### 5. Hybrid Inheritance
A combination of two or more types of inheritance (e.g., Hierarchical + Multiple).

```python
class Vehicle:
    def move(self):
        print("Vehicle is moving")

class Car(Vehicle):
    def drive(self):
        print("Driving on road")

class Boat(Vehicle):
    def sail(self):
        print("Sailing on water")

class AmphibiousVehicle(Car, Boat):
    def hybrid_action(self):
        print("Can go on land and water")

amphibian = AmphibiousVehicle()
amphibian.move() # Inherited from the top-level Vehicle class
```

### `super()`
Use `super()` to call the next implementation in the method resolution order (MRO), commonly a parent implementation.

```python
class Employee:
    def __init__(self, name):
        self.name = name

class Developer(Employee):
    def __init__(self, name, language):
        super().__init__(name)
        self.language = language

developer = Developer("Jyothish", "Python")
print(developer.name, developer.language)
```

### MRO — Method Resolution Order
MRO is the order Python follows to find a method, especially with multiple inheritance. Python uses a consistent order (C3 linearization). You can check it using `ClassName.mro()`.

## 9. Polymorphism

**Meaning:** The same operation or method name can behave differently depending on the object.

**Why?** Code can work with different object types through a common operation.

### Compile-time vs. Run-time Polymorphism in Python

**Compile-Time Polymorphism (Method Overloading)**
*   **What it is:** In languages like Java or C++, you can write multiple methods with the *exact same name* but different numbers of parameters. The computer decides which one to use when the code is compiled.
*   **Does Python have it?** **No, not natively.** Because Python is dynamically typed, if you write two methods with the same name, the second one simply overwrites the first.
*   **The Python workaround:** We achieve the same result using default arguments or `*args`.
    ```python
    class Calculator:
        def add(self, a, b, c=0):
            return a + b + c

    calc = Calculator()
    print(calc.add(2, 3))    # Output: 5
    print(calc.add(2, 3, 4)) # Output: 9
    ```

**Run-Time Polymorphism (Method Overriding & Duck Typing)**
*   **What it is:** The computer decides which method to run while the program is actually running (at run-time) based on the specific object being used.
*   **Does Python have it?** **Yes, absolutely.** This is Python's default behavior.

### Method Overriding (Run-Time Polymorphism)
A child class provides its own implementation of an inherited method.

```python
class Dog:
    def sound(self):
        print("Bark")

class Cat:
    def sound(self):
        print("Meow")

for animal in [Dog(), Cat()]:
    animal.sound() # Python decides at run-time which sound() to call
```

### Duck Typing (Run-Time Polymorphism)
Python often focuses on whether an object supports the required behaviour, rather than caring about its exact parent class. (If it walks like a duck and quacks like a duck, it's a duck).

```python
class PDFReport:
    def export(self):
        print("Exporting PDF")

class ExcelReport:
    def export(self):
        print("Exporting Excel")

def export_report(report):
    report.export() # Works as long as the object has an export() method

export_report(PDFReport())
export_report(ExcelReport())
```

## 10. Abstraction

**Meaning:** Expose what an object should do while hiding the details of
how it does it.

**Why?** Define a common contract and let each implementation provide
its own details.

Python supports abstract base classes through the `abc` module.

```python
from abc import ABC, abstractmethod


class Payment(ABC):
    @abstractmethod
    def pay(self, amount):
        pass


class UpiPayment(Payment):
    def pay(self, amount):
        print(f"Paid {amount} using UPI")


payment = UpiPayment()
payment.pay(500)
```

**Output:** `Paid 500 using UPI`

A class with unimplemented abstract methods cannot be instantiated. A
concrete child class must implement them.

------------------------------------------------------------------------

# Part 3: Other Useful OOP Concepts

## 11. Composition

**Meaning:** One class contains an object of another class. This
represents a "has-a" relationship.

**Why?** Build complex behaviour by combining smaller classes.
Composition is often more flexible than deep inheritance.

```python
class Engine:
    def start(self):
        print("Engine started")


class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
        print("Car is ready")


car = Car()
car.start()
```

**Output**

```text
Engine started
Car is ready
```

A car **has an** engine. It is not a type of engine.

## 12. Magic (Dunder) Methods

Special methods with double underscores let objects work with Python
operations such as printing, comparison and built-in functions.

| Method | Purpose |
| :--- | :--- |
| `__init__()` | Initialize an object |
| `__str__()` | Human-readable string for `str()` and `print()` |
| `__repr__()` | Developer-oriented representation |
| `__len__()` | Behaviour for `len()` |
| `__eq__()` | Behaviour for `==` |
| `__add__()` | Behaviour for `+` |

Example:

```python
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return self.title


book = Book("Python Basics")
print(book)
```

**Output:** `Python Basics`

## 13. Quick OOP Relationship Guide

| Concept | Key idea | Example relationship |
| :--- | :--- | :--- |
| Encapsulation | Bundle data and control access | Account manages its balance |
| Inheritance | Reuse/extend a parent class | Developer is an Employee |
| Polymorphism | Same operation, different behaviour | Dog and Cat both have `sound()` |
| Abstraction | Define required behaviour, hide details | Payment requires `pay()` |
| Composition | Build a class using other objects | Car has an Engine |

------------------------------------------------------------------------

# Part 4: SOLID Principles

SOLID is a set of five design principles that help make object-oriented
code easier to maintain, extend and test. They are guidelines, not
strict syntax rules.

## S -- Single Responsibility Principle (SRP)

**Meaning:** A class should have one clear responsibility and one main
reason to change.

**Why?** When unrelated tasks are placed in one class, a change to one
task can affect the others.

**Avoid:** One `Report` class that calculates data, formats the report
and saves files.

**Better:** Separate responsibilities.

```python
class Report:
    def generate(self):
        return "Monthly report"


class ReportPrinter:
    def print_report(self, report):
        print(report)


class ReportSaver:
    def save(self, report):
        print("Report saved")
```

Each class has a focused job.

## O -- Open/Closed Principle (OCP)

**Meaning:** Software should be open for extension but closed for
modification.

**Why?** Adding a new behaviour should not require repeatedly changing
stable existing code.

```python
class EmailNotification:
    def send(self, message):
        print(f"Email: {message}")


class SMSNotification:
    def send(self, message):
        print(f"SMS: {message}")


def notify(notification, message):
    notification.send(message)


notify(EmailNotification(), "Welcome")
notify(SMSNotification(), "Welcome")
```

A new notification type can be added by creating another class with
`send()`, without changing `notify()`.

## L -- Liskov Substitution Principle (LSP)

**Meaning:** An object of a child class should be usable wherever its
parent class is expected, without breaking the program's expected
behaviour.

**Why?** Inheritance should preserve the promises made by the parent
class.

**Example:** If code expects every `Bird` to fly, making `Penguin`
inherit that behaviour and then fail when `fly()` is called breaks the
expectation.

A better design separates flying behaviour:

```python
class Bird:
    def eat(self):
        print("Bird is eating")


class FlyingBird(Bird):
    def fly(self):
        print("Bird is flying")


class Sparrow(FlyingBird):
    pass


class Penguin(Bird):
    def swim(self):
        print("Penguin is swimming")
```

Now code that requires `fly()` can work with `FlyingBird` objects,
rather than assuming every bird can fly.

## I -- Interface Segregation Principle (ISP)

**Meaning:** Do not force a class to implement methods it does not need.
Prefer smaller, focused interfaces.

**Why?** Large interfaces create unnecessary methods and empty
implementations.

Python example using abstract base classes:

```python
from abc import ABC, abstractmethod


class Printable(ABC):
    @abstractmethod
    def print_document(self):
        pass


class Scannable(ABC):
    @abstractmethod
    def scan_document(self):
        pass


class SimplePrinter(Printable):
    def print_document(self):
        print("Printing document")


class MultiFunctionPrinter(Printable, Scannable):
    def print_document(self):
        print("Printing document")

    def scan_document(self):
        print("Scanning document")
```

A simple printer is not forced to implement scanning.

## D -- Dependency Inversion Principle (DIP)

**Meaning:** High-level code should depend on abstractions (expected
behaviour), not on a specific low-level implementation.

**Why?** It becomes easier to replace implementations and test code.

```python
class EmailSender:
    def send(self, message):
        print(f"Email sent: {message}")


class NotificationService:
    def __init__(self, sender):
        self.sender = sender

    def notify(self, message):
        self.sender.send(message)


email_sender = EmailSender()
service = NotificationService(email_sender)
service.notify("Welcome")
```

`NotificationService` depends on an object that provides `send()`,
rather than creating an email sender internally. Another sender can be
supplied without changing the service.

------------------------------------------------------------------------

# Part 5: Final Revision

## OOP keywords and syntax

| Topic | Python syntax |
| :--- | :--- |
| Class | `class Student:` |
| Create object | `student = Student()` |
| Initialize object | `def __init__(self):` |
| Current object | `self` |
| Class method | `@classmethod` |
| Static method | `@staticmethod` |
| Inheritance | `class Child(Parent):` |
| Parent implementation | `super()` |
| Property | `@property` |
| Abstract class | `class A(ABC):` |
| Abstract method | `@abstractmethod` |
| Override method | Define the same method in child |
| Check MRO | `ClassName.mro()` |

## Four pillars in one line

1.  **Encapsulation:** Bundle data and methods; control how data is
    accessed or changed.
2.  **Inheritance:** Reuse and extend an existing class.
3.  **Polymorphism:** Use a common operation with different
    implementations.
4.  **Abstraction:** Define what must be done while hiding
    implementation details.

## SOLID in one line

1.  **S -- Single Responsibility:** One focused responsibility per
    class.
2.  **O -- Open/Closed:** Extend behaviour without repeatedly modifying
    stable code.
3.  **L -- Liskov Substitution:** Child objects should honour the
    parent's expected behaviour.
4.  **I -- Interface Segregation:** Prefer small, focused interfaces.
5.  **D -- Dependency Inversion:** Depend on abstractions, not concrete
    implementations.

## Practical advice

-   Use instance methods when working with an object's data.
-   Use class methods for class-level operations and alternative
    constructors.
-   Use static methods for related utility logic that needs neither
    `self` nor `cls`.
-   Prefer composition when a "has-a" relationship fits better than
    inheritance.
-   Keep classes focused and avoid unnecessary abstraction.
-   Follow PEP 8 naming conventions: `PascalCase` for classes and
    `snake_case` for methods and variables.

------------------------------------------------------------------------

**End of cheat sheet**
