# Python SOLID Principles Cheatsheet

| Letter | Principle | One-liner |
|---|---|---|
| **S** | Single Responsibility | A class should have only one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subclasses must be usable wherever the parent is |
| **I** | Interface Segregation | Prefer small, focused interfaces over big ones |
| **D** | Dependency Inversion | Depend on abstractions, not concrete classes |

---# Python SOLID Principles Cheatsheet

| Letter | Principle | One-liner |
|---|---|---|
| **S** | Single Responsibility | A class should have only one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subclasses must be usable wherever the parent is |
| **I** | Interface Segregation | Prefer small, focused interfaces over big ones |
| **D** | Dependency Inversion | Depend on abstractions, not concrete classes |

---

## 1. S: Single Responsibility Principle (SRP)

> One class = one job = one reason to change.

### Bad
```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        return f"Report: {self.data}"

    def save_to_file(self, path):          # persistence mixed in
        with open(path, "w") as f:
            f.write(self.generate())

    def send_email(self, to):              # delivery mixed in
        print(f"Emailing to {to}")
```

### Good
```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        return f"Report: {self.data}"

class FileSaver:
    def save(self, content, path):
        with open(path, "w") as f:
            f.write(content)

class EmailSender:
    def send(self, content, to):
        print(f"Emailing to {to}")
```

**Smell:** a class name with "And" or "Manager", or methods unrelated to each other.

---

## 2. O: Open/Closed Principle (OCP)

> Add new behavior by adding new code, not by editing existing code.

### Bad
```python
class AreaCalculator:
    def area(self, shape):
        if shape["type"] == "circle":
            return 3.14159 * shape["r"] ** 2
        elif shape["type"] == "square":
            return shape["side"] ** 2
        # every new shape = edit this function
```

### Good
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14159 * self.r ** 2

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2

def total_area(shapes: list[Shape]):
    return sum(s.area() for s in shapes)    # never changes when adding shapes
```

**Smell:** long `if/elif` chains on type or a string flag.

---

## 3. L: Liskov Substitution Principle (LSP)

> If `B` is a subclass of `A`, you should be able to use `B` anywhere `A` is expected without breaking behavior.

### Bad (classic Rectangle/Square)
```python
class Rectangle:
    def __init__(self, w, h):
        self.w, self.h = w, h
    def set_width(self, w):  self.w = w
    def set_height(self, h): self.h = h
    def area(self): return self.w * self.h

class Square(Rectangle):
    def set_width(self, w):
        self.w = self.h = w              # surprises callers
    def set_height(self, h):
        self.w = self.h = h

def resize(rect: Rectangle):
    rect.set_width(5)
    rect.set_height(10)
    assert rect.area() == 50             # fails for Square
```

### Good
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Rectangle(Shape):
    def __init__(self, w, h): self.w, self.h = w, h
    def area(self): return self.w * self.h

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2
```

### LSP rules of thumb
- Don't strengthen preconditions (accept less than the parent did)
- Don't weaken postconditions (return less than the parent promised)
- Don't raise new unexpected exceptions
- Keep the same return types and behavior contract
- If a subclass overrides a method to `raise NotImplementedError`, it probably violates LSP

---

## 4. I: Interface Segregation Principle (ISP)

> Don't force classes to implement methods they don't use.

### Bad
```python
from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self): ...
    @abstractmethod
    def eat(self): ...

class Robot(Worker):
    def work(self): print("Working")
    def eat(self): raise NotImplementedError   # robots don't eat
```

### Good
```python
from abc import ABC, abstractmethod

class Workable(ABC):
    @abstractmethod
    def work(self): ...

class Eatable(ABC):
    @abstractmethod
    def eat(self): ...

class Human(Workable, Eatable):
    def work(self): print("Working")
    def eat(self): print("Eating")

class Robot(Workable):
    def work(self): print("Working")
```

### Pythonic alternative: `typing.Protocol` (structural typing)
```python
from typing import Protocol

class Workable(Protocol):
    def work(self) -> None: ...

def run(w: Workable):
    w.work()          # any object with .work() fits, no inheritance needed
```

---

## 5. D: Dependency Inversion Principle (DIP)

> High-level modules shouldn't depend on low-level modules. Both should depend on abstractions.

### Bad
```python
class MySQLDatabase:
    def save(self, data): print("Saving to MySQL")

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()        # hard-coded dependency

    def create_user(self, user):
        self.db.save(user)
```

### Good (dependency injection)
```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def save(self, data): ...

class MySQLDatabase(Database):
    def save(self, data): print("Saving to MySQL")

class MongoDatabase(Database):
    def save(self, data): print("Saving to MongoDB")

class UserService:
    def __init__(self, db: Database):    # injected abstraction
        self.db = db

    def create_user(self, user):
        self.db.save(user)

service = UserService(MySQLDatabase())   # swap freely
service = UserService(MongoDatabase())
```

**Bonus:** makes testing easy, since you can inject a fake:

```python
class FakeDB(Database):
    def __init__(self): self.saved = []
    def save(self, data): self.saved.append(data)

fake = FakeDB()
UserService(fake).create_user("asha")
assert fake.saved == ["asha"]
```

> **DIP vs DI:** DIP is the principle (depend on abstractions). Dependency Injection is a technique for achieving it (pass dependencies in from outside).

---

## 6. Quick Smell Detector

| Symptom | Likely violation |
|---|---|
| Class does I/O, logic, and formatting | SRP |
| Adding a feature means editing old `if/elif` chains | OCP |
| Subclass raises `NotImplementedError` or changes expected behavior | LSP |
| Empty or `pass` methods just to satisfy an interface | ISP |
| `self.x = ConcreteClass()` inside `__init__` | DIP |

---

## 7. Python-Specific Tips

- Python's duck typing and `Protocol` often replace heavy interface hierarchies
- Use `abc.ABC` + `@abstractmethod` when you want enforcement at instantiation
- Use `Protocol` when you want flexible, structural contracts
- Functions are first-class: passing a callable can satisfy OCP/DIP without any classes
- Don't over-engineer: apply SOLID where change is likely, not everywhere

```python
# DIP/OCP with plain functions
def process(data, formatter):          # formatter is any callable
    return formatter(data)

process("hi", str.upper)
process("hi", lambda s: s[::-1])
```

---

## 8. Interview One-Liners

- **SRP:** "A class should have one, and only one, reason to change."
- **OCP:** "Extend behavior without modifying existing code."
- **LSP:** "Subtypes must be substitutable for their base types."
- **ISP:** "Many specific interfaces beat one general-purpose interface."
- **DIP:** "Depend on abstractions, not concretions."

## 1. S: Single Responsibility Principle (SRP)

> One class = one job = one reason to change.

### Bad
```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        return f"Report: {self.data}"

    def save_to_file(self, path):          # persistence mixed in
        with open(path, "w") as f:
            f.write(self.generate())

    def send_email(self, to):              # delivery mixed in
        print(f"Emailing to {to}")
```

### Good
```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        return f"Report: {self.data}"

class FileSaver:
    def save(self, content, path):
        with open(path, "w") as f:
            f.write(content)

class EmailSender:
    def send(self, content, to):
        print(f"Emailing to {to}")
```

**Smell:** a class name with "And" or "Manager", or methods unrelated to each other.

---

## 2. O: Open/Closed Principle (OCP)

> Add new behavior by adding new code, not by editing existing code.

### Bad
```python
class AreaCalculator:
    def area(self, shape):
        if shape["type"] == "circle":
            return 3.14159 * shape["r"] ** 2
        elif shape["type"] == "square":
            return shape["side"] ** 2
        # every new shape = edit this function
```

### Good
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14159 * self.r ** 2

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2

def total_area(shapes: list[Shape]):
    return sum(s.area() for s in shapes)    # never changes when adding shapes
```

**Smell:** long `if/elif` chains on type or a string flag.

---

## 3. L: Liskov Substitution Principle (LSP)

> If `B` is a subclass of `A`, you should be able to use `B` anywhere `A` is expected without breaking behavior.

### Bad (classic Rectangle/Square)
```python
class Rectangle:
    def __init__(self, w, h):
        self.w, self.h = w, h
    def set_width(self, w):  self.w = w
    def set_height(self, h): self.h = h
    def area(self): return self.w * self.h

class Square(Rectangle):
    def set_width(self, w):
        self.w = self.h = w              # surprises callers
    def set_height(self, h):
        self.w = self.h = h

def resize(rect: Rectangle):
    rect.set_width(5)
    rect.set_height(10)
    assert rect.area() == 50             # fails for Square
```

### Good
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Rectangle(Shape):
    def __init__(self, w, h): self.w, self.h = w, h
    def area(self): return self.w * self.h

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2
```

### LSP rules of thumb
- Don't strengthen preconditions (accept less than the parent did)
- Don't weaken postconditions (return less than the parent promised)
- Don't raise new unexpected exceptions
- Keep the same return types and behavior contract
- If a subclass overrides a method to `raise NotImplementedError`, it probably violates LSP

---

## 4. I: Interface Segregation Principle (ISP)

> Don't force classes to implement methods they don't use.

### Bad
```python
from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self): ...
    @abstractmethod
    def eat(self): ...

class Robot(Worker):
    def work(self): print("Working")
    def eat(self): raise NotImplementedError   # robots don't eat
```

### Good
```python
from abc import ABC, abstractmethod

class Workable(ABC):
    @abstractmethod
    def work(self): ...

class Eatable(ABC):
    @abstractmethod
    def eat(self): ...

class Human(Workable, Eatable):
    def work(self): print("Working")
    def eat(self): print("Eating")

class Robot(Workable):
    def work(self): print("Working")
```

### Pythonic alternative: `typing.Protocol` (structural typing)
```python
from typing import Protocol

class Workable(Protocol):
    def work(self) -> None: ...

def run(w: Workable):
    w.work()          # any object with .work() fits, no inheritance needed
```

---

## 5. D: Dependency Inversion Principle (DIP)

> High-level modules shouldn't depend on low-level modules. Both should depend on abstractions.

### Bad
```python
class MySQLDatabase:
    def save(self, data): print("Saving to MySQL")

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()        # hard-coded dependency

    def create_user(self, user):
        self.db.save(user)
```

### Good (dependency injection)
```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def save(self, data): ...

class MySQLDatabase(Database):
    def save(self, data): print("Saving to MySQL")

class MongoDatabase(Database):
    def save(self, data): print("Saving to MongoDB")

class UserService:
    def __init__(self, db: Database):    # injected abstraction
        self.db = db

    def create_user(self, user):
        self.db.save(user)

service = UserService(MySQLDatabase())   # swap freely
service = UserService(MongoDatabase())
```

**Bonus:** makes testing easy, since you can i# Python SOLID Principles Cheatsheet

| Letter | Principle | One-liner |
|---|---|---|
| **S** | Single Responsibility | A class should have only one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | Subclasses must be usable wherever the parent is |
| **I** | Interface Segregation | Prefer small, focused interfaces over big ones |
| **D** | Dependency Inversion | Depend on abstractions, not concrete classes |

---

## 1. S: Single Responsibility Principle (SRP)

> One class = one job = one reason to change.

### Bad
```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        return f"Report: {self.data}"

    def save_to_file(self, path):          # persistence mixed in
        with open(path, "w") as f:
            f.write(self.generate())

    def send_email(self, to):              # delivery mixed in
        print(f"Emailing to {to}")
```

### Good
```python
class Report:
    def __init__(self, data):
        self.data = data

    def generate(self):
        return f"Report: {self.data}"

class FileSaver:
    def save(self, content, path):
        with open(path, "w") as f:
            f.write(content)

class EmailSender:
    def send(self, content, to):
        print(f"Emailing to {to}")
```

**Smell:** a class name with "And" or "Manager", or methods unrelated to each other.

---

## 2. O: Open/Closed Principle (OCP)

> Add new behavior by adding new code, not by editing existing code.

### Bad
```python
class AreaCalculator:
    def area(self, shape):
        if shape["type"] == "circle":
            return 3.14159 * shape["r"] ** 2
        elif shape["type"] == "square":
            return shape["side"] ** 2
        # every new shape = edit this function
```

### Good
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Circle(Shape):
    def __init__(self, r): self.r = r
    def area(self): return 3.14159 * self.r ** 2

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2

def total_area(shapes: list[Shape]):
    return sum(s.area() for s in shapes)    # never changes when adding shapes
```

**Smell:** long `if/elif` chains on type or a string flag.

---

## 3. L: Liskov Substitution Principle (LSP)

> If `B` is a subclass of `A`, you should be able to use `B` anywhere `A` is expected without breaking behavior.

### Bad (classic Rectangle/Square)
```python
class Rectangle:
    def __init__(self, w, h):
        self.w, self.h = w, h
    def set_width(self, w):  self.w = w
    def set_height(self, h): self.h = h
    def area(self): return self.w * self.h

class Square(Rectangle):
    def set_width(self, w):
        self.w = self.h = w              # surprises callers
    def set_height(self, h):
        self.w = self.h = h

def resize(rect: Rectangle):
    rect.set_width(5)
    rect.set_height(10)
    assert rect.area() == 50             # fails for Square
```

### Good
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self): ...

class Rectangle(Shape):
    def __init__(self, w, h): self.w, self.h = w, h
    def area(self): return self.w * self.h

class Square(Shape):
    def __init__(self, side): self.side = side
    def area(self): return self.side ** 2
```

### LSP rules of thumb
- Don't strengthen preconditions (accept less than the parent did)
- Don't weaken postconditions (return less than the parent promised)
- Don't raise new unexpected exceptions
- Keep the same return types and behavior contract
- If a subclass overrides a method to `raise NotImplementedError`, it probably violates LSP

---

## 4. I: Interface Segregation Principle (ISP)

> Don't force classes to implement methods they don't use.

### Bad
```python
from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self): ...
    @abstractmethod
    def eat(self): ...

class Robot(Worker):
    def work(self): print("Working")
    def eat(self): raise NotImplementedError   # robots don't eat
```

### Good
```python
from abc import ABC, abstractmethod

class Workable(ABC):
    @abstractmethod
    def work(self): ...

class Eatable(ABC):
    @abstractmethod
    def eat(self): ...

class Human(Workable, Eatable):
    def work(self): print("Working")
    def eat(self): print("Eating")

class Robot(Workable):
    def work(self): print("Working")
```

### Pythonic alternative: `typing.Protocol` (structural typing)
```python
from typing import Protocol

class Workable(Protocol):
    def work(self) -> None: ...

def run(w: Workable):
    w.work()          # any object with .work() fits, no inheritance needed
```

---

## 5. D: Dependency Inversion Principle (DIP)

> High-level modules shouldn't depend on low-level modules. Both should depend on abstractions.

### Bad
```python
class MySQLDatabase:
    def save(self, data): print("Saving to MySQL")

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()        # hard-coded dependency

    def create_user(self, user):
        self.db.save(user)
```

### Good (dependency injection)
```python
from abc import ABC, abstractmethod

class Database(ABC):
    @abstractmethod
    def save(self, data): ...

class MySQLDatabase(Database):
    def save(self, data): print("Saving to MySQL")

class MongoDatabase(Database):
    def save(self, data): print("Saving to MongoDB")

class UserService:
    def __init__(self, db: Database):    # injected abstraction
        self.db = db

    def create_user(self, user):
        self.db.save(user)

service = UserService(MySQLDatabase())   # swap freely
service = UserService(MongoDatabase())
```

**Bonus:** makes testing easy, since you can inject a fake:

```python
class FakeDB(Database):
    def __init__(self): self.saved = []
    def save(self, data): self.saved.append(data)

fake = FakeDB()
UserService(fake).create_user("asha")
assert fake.saved == ["asha"]
```

> **DIP vs DI:** DIP is the principle (depend on abstractions). Dependency Injection is a technique for achieving it (pass dependencies in from outside).

---

## 6. Quick Smell Detector

| Symptom | Likely violation |
|---|---|
| Class does I/O, logic, and formatting | SRP |
| Adding a feature means editing old `if/elif` chains | OCP |
| Subclass raises `NotImplementedError` or changes expected behavior | LSP |
| Empty or `pass` methods just to satisfy an interface | ISP |
| `self.x = ConcreteClass()` inside `__init__` | DIP |

---

## 7. Python-Specific Tips

- Python's duck typing and `Protocol` often replace heavy interface hierarchies
- Use `abc.ABC` + `@abstractmethod` when you want enforcement at instantiation
- Use `Protocol` when you want flexible, structural contracts
- Functions are first-class: passing a callable can satisfy OCP/DIP without any classes
- Don't over-engineer: apply SOLID where change is likely, not everywhere

```python
# DIP/OCP with plain functions
def process(data, formatter):          # formatter is any callable
    return formatter(data)

process("hi", str.upper)
process("hi", lambda s: s[::-1])
```

---

## 8. Interview One-Liners

- **SRP:** "A class should have one, and only one, reason to change."
- **OCP:** "Extend behavior without modifying existing code."
- **LSP:** "Subtypes must be substitutable for their base types."
- **ISP:** "Many specific interfaces beat one general-purpose interface."
- **DIP:** "Depend on abstractions, not concretions."nject a fake:

```python
class FakeDB(Database):
    def __init__(self): self.saved = []
    def save(self, data): self.saved.append(data)

fake = FakeDB()
UserService(fake).create_user("asha")
assert fake.saved == ["asha"]
```

> **DIP vs DI:** DIP is the principle (depend on abstractions). Dependency Injection is a technique for achieving it (pass dependencies in from outside).

---

## 6. Quick Smell Detector

| Symptom | Likely violation |
|---|---|
| Class does I/O, logic, and formatting | SRP |
| Adding a feature means editing old `if/elif` chains | OCP |
| Subclass raises `NotImplementedError` or changes expected behavior | LSP |
| Empty or `pass` methods just to satisfy an interface | ISP |
| `self.x = ConcreteClass()` inside `__init__` | DIP |

---

## 7. Python-Specific Tips

- Python's duck typing and `Protocol` often replace heavy interface hierarchies
- Use `abc.ABC` + `@abstractmethod` when you want enforcement at instantiation
- Use `Protocol` when you want flexible, structural contracts
- Functions are first-class: passing a callable can satisfy OCP/DIP without any classes
- Don't over-engineer: apply SOLID where change is likely, not everywhere

```python
# DIP/OCP with plain functions
def process(data, formatter):          # formatter is any callable
    return formatter(data)

process("hi", str.upper)
process("hi", lambda s: s[::-1])
```

---

