# Python OOP Cheatsheet

## 1. Classes & Objects

```python
class Dog:
    species = "Canis familiaris"        # class attribute (shared)

    def __init__(self, name, age):      # constructor / initializer
        self.name = name                # instance attribute
        self.age = age

    def bark(self):                     # instance method
        return f"{self.name} says woof!"

d = Dog("Rex", 3)
print(d.bark())          # Rex says woof!
print(d.species)         # Canis familiaris
```

- `self` = the current instance (first parameter of instance methods)
- `__init__` runs automatically when an object is created
- Class attributes are shared by all instances; instance attributes belong to one object

---

## 2. Method Types

```python
class Demo:
    count = 0

    def instance_method(self):          # needs an instance
        return "instance"

    @classmethod
    def class_method(cls):              # gets the class, not instance
        cls.count += 1
        return cls.count

    @staticmethod
    def static_method(x, y):            # no self / cls, utility function
        return x + y
```

| Type | First arg | Access instance data | Access class data |
|---|---|---|---|
| Instance method | `self` | Yes | Yes |
| `@classmethod` | `cls` | No | Yes |
| `@staticmethod` | none | No | No |

**Alternative constructor with classmethod:**

```python
class Person:
    def __init__(self, name, age):
        self.name, self.age = name, age

    @classmethod
    def from_birth_year(cls, name, year):
        return cls(name, 2026 - year)
```

---

## 3. The Four Pillars

### Encapsulation
Bundling data and methods, and restricting direct access.

```python
class Account:
    def __init__(self, balance):
        self.public = "anyone"
        self._protected = "convention: internal use"
        self.__private = balance          # name-mangled -> _Account__private

    def get_balance(self):
        return self.__private
```

- `name` → public
- `_name` → protected (by convention only)
- `__name` → private (name mangling, not truly hidden)

### Inheritance
```python
class Animal:
    def __init__(self, name):
        self.name = name
    def speak(self):
        return "..."

class Cat(Animal):
    def __init__(self, name, indoor):
        super().__init__(name)            # call parent constructor
        self.indoor = indoor
    def speak(self):                      # override
        return "Meow"
```

### Polymorphism
Same interface, different behavior.

```python
for a in [Cat("Tom", True), Animal("Generic")]:
    print(a.speak())
```

### Abstraction
Hide implementation, expose only what's needed (see ABCs below).

---

## 4. Inheritance Details

```python
class A: pass
class B(A): pass                  # single
class C(A, B): pass               # multiple (order matters)

isinstance(obj, A)                # is obj an instance of A (or subclass)?
issubclass(B, A)                  # True
C.__mro__                         # Method Resolution Order (C3 linearization)
```

- `super()` follows the MRO, not just "the parent"
- Prefer composition over deep inheritance when possible

---

## 5. Abstract Base Classes

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14159 * self.r ** 2

# Shape()  -> TypeError: can't instantiate abstract class
```

---

## 6. Properties (getters / setters)

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius

    @property
    def celsius(self):                    # getter
        return self._celsius

    @celsius.setter
    def celsius(self, value):             # setter with validation
        if value < -273.15:
            raise ValueError("Below absolute zero")
        self._celsius = value

    @property
    def fahrenheit(self):                 # read-only computed property
        return self._celsius * 9 / 5 + 32

t = Temperature(25)
t.celsius = 30                            # calls setter
print(t.fahrenheit)                       # 86.0
```

---

## 7. Dunder (Magic) Methods

| Method | Triggered by | Purpose |
|---|---|---|
| `__init__(self, ...)` | `Cls(...)` | Initialize object |
| `__new__(cls, ...)` | before `__init__` | Create object |
| `__str__(self)` | `str(obj)`, `print(obj)` | Readable string |
| `__repr__(self)` | `repr(obj)`, debugging | Unambiguous string |
| `__len__(self)` | `len(obj)` | Length |
| `__getitem__(self, k)` | `obj[k]` | Indexing |
| `__setitem__(self, k, v)` | `obj[k] = v` | Item assignment |
| `__iter__` / `__next__` | `for x in obj` | Iteration |
| `__contains__(self, x)` | `x in obj` | Membership |
| `__call__(self, ...)` | `obj(...)` | Make callable |
| `__eq__`, `__lt__`, `__gt__` | `==`, `<`, `>` | Comparison |
| `__add__`, `__sub__`, `__mul__` | `+`, `-`, `*` | Operator overloading |
| `__enter__` / `__exit__` | `with obj:` | Context manager |
| `__del__` | garbage collection | Destructor |
| `__hash__` | `hash(obj)` | Hashing (dict keys / sets) |
| `__bool__` | `bool(obj)` | Truthiness |

```python
class Vector:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __eq__(self, other):
        return (self.x, self.y) == (other.x, other.y)

print(Vector(1, 2) + Vector(3, 4))        # Vector(4, 6)
```

> `__str__` is for users, `__repr__` is for developers. If only `__repr__` is defined, `print()` uses it too.

---

## 8. Dataclasses

```python
from dataclasses import dataclass, field

@dataclass
class Student:
    name: str
    marks: int = 0
    subjects: list = field(default_factory=list)   # mutable default

s = Student("Asha", 90)
print(s)          # Student(name='Asha', marks=90, subjects=[])
```

Options: `@dataclass(frozen=True)` (immutable), `order=True` (comparisons), `slots=True` (less memory).
Auto-generates `__init__`, `__repr__`, `__eq__`.

---

## 9. `__slots__`

```python
class Point:
    __slots__ = ("x", "y")        # no __dict__, saves memory, blocks new attributes
    def __init__(self, x, y):
        self.x, self.y = x, y
```

---

## 10. Composition vs Inheritance

```python
class Engine:
    def start(self): return "Engine on"

class Car:                                # "has-a" relationship
    def __init__(self):
        self.engine = Engine()
    def start(self):
        return self.engine.start()
```

- **Inheritance** = "is-a" (Dog is an Animal)
- **Composition** = "has-a" (Car has an Engine)

---

## 11. Context Managers (class-based)

```python
class FileManager:
    def __init__(self, path, mode):
        self.path, self.mode = path, mode
    def __enter__(self):
        self.f = open(self.path, self.mode)
        return self.f
    def __exit__(self, exc_type, exc, tb):
        self.f.close()
        return False                      # don't suppress exceptions

with FileManager("a.txt", "w") as f:
    f.write("hello")
```

---

## 12. Iterators (class-based)

```python
class Countdown:
    def __init__(self, n): self.n = n
    def __iter__(self): return self
    def __next__(self):
        if self.n <= 0:
            raise StopIteration
        self.n -= 1
        return self.n + 1

print(list(Countdown(3)))                 # [3, 2, 1]
```

---

## 13. Introspection Helpers

```python
type(obj)                  # class of obj
isinstance(obj, Cls)       # instance check
issubclass(Sub, Base)      # subclass check
hasattr(obj, "x")          # attribute exists?
getattr(obj, "x", None)    # get with default
setattr(obj, "x", 10)      # set dynamically
delattr(obj, "x")          # delete attribute
vars(obj)                  # obj.__dict__
dir(obj)                   # list attributes & methods
callable(obj)              # can it be called?
```

---

## 14. Class Decorators & Metaclass (quick note)

```python
class Meta(type):
    def __new__(mcs, name, bases, ns):
        return super().__new__(mcs, name, bases, ns)

class MyClass(metaclass=Meta): ...
```

Metaclasses customize **class creation**. Rarely needed; classes are objects whose class is `type`.

---

## 15. Common Pitfalls

- **Mutable default arguments:** use `None` and create inside the method

  ```python
  def __init__(self, items=None):
      self.items = items if items is not None else []
  ```
- **Forgetting `self`:** `TypeError: takes 1 positional argument but 2 were given`
- **Forgetting `super().__init__()`** in subclasses
- **Class attribute mutation:** `self.shared_list.append(x)` changes it for all instances
- **Defining `__eq__` without `__hash__`:** makes objects unhashable
- **`__private` isn't truly private,** just name-mangled

---

