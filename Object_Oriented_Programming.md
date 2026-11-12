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


## 2. Class and Object

-   **Class:** A blueprint that describes the attributes and methods its
    objects can have. A class is blueprint or template to create objects.
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


student1 = Student("Raj")
student2 = Student("Rahul")

student1.display()
student2.display()
```

**Output**

```text
Raj
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


student1 = Student("Jyothish", 23)
student1.display()
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


# Part 2: The Four Pillars of OOP

## 7. Encapsulation

Pillar 1: Encapsulation
Definition: Wrapping data and methods together inside a single unit (class), while controlling access to the data.

Real-life example: ATM machine.


You can:
- Check your balance.
- Withdraw money.
- Deposit money.
But you cannot directly access the internal banking system.



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

Important points:
- __balance uses name mangling to discourage direct access.
- We access the balance through methods.
- This helps protect the object's internal state.
### Property -- controlled attribute access



## 8. Inheritance

**Meaning:** Inheritance allows one class to acquire properties and methods from another class.

Real-life example:
- Animal → Parent class.
- Dog → Child class.
- Cat → Child class.

 ```python
class Animal:

    def eat(self):
        print("Animal is eating")


class Dog(Animal):

    def bark(self):
        print("Dog is barking")


dog = Dog()

dog.eat()
dog.bark()
```

```

Here:
- Animal is the parent class.
- Dog is the child class.
- Dog inherits the eat() method.
Remember: Inheritance = Code reusability.

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


## 9. Polymorphism

Pillar 3: Polymorphism
Poly = Many
Morphism = Forms

Definition: The same interface or method name can have different behaviours depending on the object.

Real-life example:

A person can:
- Drive a car.
- Ride a bike.
- Fly an aircraft.
The action is transportation, but the implementation differs.

```python
class Dog:

    def sound(self):
        print("Bark")


class Cat:

    def sound(self):
        print("Meow")


class Cow:

    def sound(self):
        print("Moo")


animals = [Dog(), Cat(), Cow()]

for animal in animals:
    animal.sound()
```
polymorphism = Same interface, different behaviour.

## 10. Abstraction

Imagine you're driving a car.

You have:
- Accelerator
- Brake
- Steering wheel
You know WHAT these controls do, but you don't need to know HOW the engine, braking system or steering mechanism works internally.

Hiding implementation details and exposing only essential functionality.

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

"Python provides a module called abc, which stands for Abstract Base Classes. 

We import two things:
1. ABC – To create an abstract class.
2. abstractmethod – To define a method that child classes must implement."

->Payment is abstract class that we have created 
->There is an abstract method called pay(), which accepting an amount.
-> Pass is just a placeholder currently no implementation  

->UpiPayment inherits from the Payment class. -
This demonstrates abstraction because we define what operation should be performed without exposing the implementation details to the user."


**Output:** `Paid 500 using UPI.`

ABC allows us to create abstract base classes.
@abstractmethod declares a method that concrete subclasses must implement.

A class with unimplemented abstract methods cannot be instantiated. A
concrete child class must implement them.


Difference Between Encapsulation and Abstraction 

Abstraction -> Hide complexity
Encapsulation -> Protect internal data

------------------------------------------------------------------------

# Part 3: Other Useful OOP Concepts


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



## 13. Quick OOP Relationship Guide

| Concept | Key idea | Example relationship |
| :--- | :--- | :--- |
| Encapsulation | Bundle data and control access | Account manages its balance |
| Inheritance | Reuse/extend a parent class | Developer is an Employee |
| Polymorphism | Same operation, different behaviour | Dog and Cat both have `sound()` |
| Abstraction | Define required behaviour, hide details | Payment requires `pay()` |
| Composition | Build a class using other objects | Car has an Engine |

------------------------------------------------------------------------

