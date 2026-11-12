OOPs in Python 
1. Introduction to OOPs (2 minutes)

"Suppose we want to build a student management system. We have 1,000 students. How would we store their information?"

One approach is using variables:
student1_name = "Rahul"student1_age = 22student2_name = "Amit"student2_age = 23


Imagine doing this for 1,000 students!

This becomes difficult to maintain.

Instead, we use OOPs.
What is OOPs?
OOPs stands for Object-Oriented Programming System.

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
- 
Important distinction:
Class	Object
Blueprint	Instance
Logical definition	Actual entity
Defines attributes and methods	Has its own state


3. Attributes and Constructor (2 minutes)
Objects need data.

For example, every student has a different name and age.

We use a constructor to initialise that data.
Constructor: __init__()
class Student:    def __init__(self, name, age):        self.name = name        self.age = age    def display(self):        print(self.name, self.age)student1 = Student("Rahul", 22)student2 = Student("Amit", 23)student1.display()student2.display()


Output:
Rahul 22
Amit 23

Explain these three things:
1. __init__() is automatically called when an object is created.
2. self refers to the current object.
3. self.name and self.age are instance attributes.
Remember: Each object has its own instance attributes.
4. Four Pillars of OOPs (5 minutes)
This is the most important part of your session.

OOPs has four major pillars.
Pillar 1: Encapsulation
Definition: Wrapping data and methods together inside a single unit (class), while controlling access to the data.

Real-life example: ATM machine.

You can:
- Check your balance.
- Withdraw money.
- Deposit money.
But you cannot directly access the internal banking system.

Python example:
class BankAccount:    def __init__(self, balance):        self.__balance = balance    def deposit(self, amount):        if amount > 0:            self.__balance += amount    def get_balance(self):        return self.__balanceaccount = BankAccount(1000)account.deposit(500)print(account.get_balance())


Output:
1500

Important points:
- __balance uses name mangling to discourage direct access.
- We access the balance through methods.
- This helps protect the object's internal state.
Remember: Encapsulation = Data protection + controlled access.
Pillar 2: Inheritance
Definition: Inheritance allows one class to acquire properties and methods from another class.

Real-life example:
- Animal → Parent class.
- Dog → Child class.
- Cat → Child class.
Python example:
class Animal:    def eat(self):        print("Animal is eating")class Dog(Animal):    def bark(self):        print("Dog is barking")dog = Dog()dog.eat()dog.bark()


Output:
Animal is eating
Dog is barking

Here:
- Animal is the parent class.
- Dog is the child class.
- Dog inherits the eat() method.
Remember: Inheritance = Code reusability.
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

Python example:
class Dog:    def sound(self):        print("Bark")class Cat:    def sound(self):        print("Meow")class Cow:    def sound(self):        print("Moo")animals = [Dog(), Cat(), Cow()]for animal in animals:    animal.sound()


Output:
Bark
Meow
Moo

Notice:

We are calling the same method sound().

But the output changes depending on the object.

Remember: Polymorphism = Same interface, different behaviour.
Pillar 4: Abstraction
Definition: Hiding implementation details and exposing only essential functionality.

Real-life example:

When you drive a car:
- You use the steering wheel.
- You press the accelerator.
- You apply the brakes.
You don't need to understand the entire internal engine mechanism.

Python example:
from abc import ABC, abstractmethodclass Vehicle(ABC):    @abstractmethod    def start(self):        passclass Car(Vehicle):    def start(self):        print("Car is starting")class Bike(Vehicle):    def start(self):        print("Bike is starting")car = Car()bike = Bike()car.start()bike.start()


Output:
Car is starting
Bike is starting

Important points:
- ABC allows us to create abstract base classes.
- @abstractmethod declares a method that concrete subclasses must implement.
- We cannot directly instantiate Vehicle while it has an unimplemented abstract method.
Remember: Abstraction = Hiding implementation details, exposing essential behaviour.
5. Why do we need OOPs? (1 minute)
Ask your classmates:

"What happens when our application becomes bigger?"

Without OOPs:
- Code becomes difficult to maintain.
- Code duplication increases.
- Managing related data becomes difficult.
- Changes become harder to manage.
With OOPs:
- Code reusability.
- Better organisation.
- Easier maintenance.
- Better modularity.
- Easier testing.
This is also where SOLID principles come into the picture.

OOPs helps organise code. SOLID helps us design that code better.
6. Quick Revision (2 minutes)
End your session by asking these questions.
Question	Answer
What is OOPs?	Object-Oriented Programming
What is a class?	Blueprint for creating objects
What is an object?	Instance of a class
What is __init__()?	Initialises a newly created object
What is self?	Reference to the current instance
What is encapsulation?	Bundling data and methods with controlled access
What is inheritance?	Acquiring functionality from another class
What is polymorphism?	Same interface, different behaviour
What is abstraction?	Hiding implementation details
