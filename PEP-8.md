# Python PEP 8 Cheatsheet

## 1. What is PEP 8?

PEP stands for **Python Enhancement Proposal**.

PEP 8 is the official Python style guide. It provides coding conventions to make Python code:
- Readable
- Consistent
- Maintainable
- Easy to understand

**Remember:** PEP 8 does not change how Python code works. It defines how Python code should be written.

---

## 2. Indentation

- Use 4 spaces for each indentation level.
- Do not mix tabs and spaces.
- Avoid unnecessary indentation.

Correct:

```python
def calculate_sum(a, b):
    result = a + b
    return result
```

Incorrect:

```python
def calculate_sum(a, b):
  result = a + b
    return result
```

---

## 3. Maximum Line Length

- Maximum recommended line length for code: 79 characters.
- Maximum recommended line length for comments and docstrings: 72 characters.
- Break long statements into multiple lines.

Correct:

```python
total_population = (
    population_of_india
    + population_of_china
    + population_of_usa
)
```

Another example:

```python
def calculate_average(
    total_marks,
    number_of_students
):
    return total_marks / number_of_students
```

---

## 4. Blank Lines

Use blank lines to separate different parts of your code.

PEP 8 recommendations:

- Two blank lines between top-level functions and classes.
- One blank line between methods inside a class.
- Use blank lines inside functions when they improve readability.

Example:

```python
import math


def calculate_area(radius):
    return math.pi * radius ** 2


def calculate_perimeter(radius):
    return 2 * math.pi * radius


class Circle:
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return calculate_area(self.radius)
```

---

## 5. Naming Conventions

Naming conventions are extremely important in Python.

| Element | Convention | Example |
|---|---|---|
| Variables | snake_case | `total_marks` |
| Functions | snake_case | `calculate_area()` |
| Methods | snake_case | `get_name()` |
| Classes | PascalCase | `StudentDetails` |
| Constants | UPPER_CASE | `MAX_VALUE` |
| Modules | lowercase | `calculator.py` |
| Packages | lowercase | `analytics` |
| Private attributes | Leading underscore | `_salary` |

### Variables

Correct:

```python
student_name = "Varad"
total_marks = 450
```

Incorrect:

```python
studentName = "Varad"
TotalMarks = 450
```

### Functions

Correct:

```python
def calculate_total():
    pass
```

Incorrect:

```python
def CalculateTotal():
    pass
```

### Classes

Correct:

```python
class StudentDetails:
    pass
```

Incorrect:

```python
class student_details:
    pass
```

### Constants

```python
MAX_RETRIES = 5
PI = 3.14159
DATABASE_NAME = "students"
```

---

## 6. Spaces Around Operators

Use spaces around operators.

Correct:

```python
total = a + b
average = total / count
is_valid = age >= 18
```

Incorrect:

```python
total=a+b
average=total/count
is_valid=age>=18
```

### Important exception: Keyword arguments and default values

Do not put spaces around `=` when assigning default parameter values or passing keyword arguments.

Correct:

```python
def calculate_total(price=100):
    pass


calculate_total(price=200)
```

Incorrect:

```python
def calculate_total(price = 100):
    pass


calculate_total(price = 200)
```

---

## 7. Spaces After Commas

Always use one space after commas.

Correct:

```python
numbers = [10, 20, 30, 40]

student = {
    "name": "Varad",
    "age": 25
}
```

Incorrect:

```python
numbers = [10,20,30,40]
```

---

## 8. Avoid Unnecessary Spaces

Do not put unnecessary spaces inside brackets, parentheses or braces.

Correct:

```python
numbers = [1, 2, 3]
student = {"name": "Varad"}
result = calculate_sum(10, 20)
```

Incorrect:

```python
numbers = [ 1, 2, 3 ]
student = { "name": "Varad" }
result = calculate_sum( 10, 20 )
```

---

## 9. Import Statements

- Imports should generally be placed at the top of the file.
- Use separate lines for separate imports.
- Group imports in the following order:
  1. Standard library imports
  2. Third-party imports
  3. Local application imports

Correct:

```python
import csv
import os

import matplotlib.pyplot as plt
import numpy as np

from my_project.calculations import calculate_average
```

Incorrect:

```python
import csv, os, numpy, matplotlib
```

### Avoid wildcard imports

Correct:

```python
from math import sqrt
```

Incorrect:

```python
from math import *
```

---

## 10. Comments

Comments should explain why something is happening, not simply repeat the code.

Correct:

```python
# Ignore matches without a valid winner.
if not winner:
    continue
```

Incorrect:

```python
# Check winner
if not winner:
    continue
```

### Inline comments

Use at least two spaces before an inline comment.

```python
total = 100  # Initial total
```

Avoid unnecessary comments.

---

## 11. Docstrings

Docstrings explain what a function, class or module does.

Use triple double quotes.

Example:

```python
def calculate_average(total_marks, number_of_students):
    """
    Calculate the average marks of students.

    Args:
        total_marks: Sum of all students' marks.
        number_of_students: Total number of students.

    Returns:
        Average marks.
    """
    return total_marks / number_of_students
```

Use docstrings for:
- Modules
- Functions
- Classes
- Methods

---

## 12. Boolean Comparisons

Avoid comparing boolean values unnecessarily.

Correct:

```python
if is_valid:
    print("Valid")
```

Incorrect:

```python
if is_valid == True:
    print("Valid")
```

For checking `None`, use `is` or `is not`.

Correct:

```python
if result is None:
    print("No result")
```

Incorrect:

```python
if result == None:
    print("No result")
```

---

## 13. String Formatting

Prefer f-strings for readable string formatting.

Correct:

```python
name = "Varad"
age = 25

print(f"My name is {name} and I am {age} years old.")
```

Another option:

```python
print("My name is {}.".format(name))
```

Avoid unnecessary string concatenation:

```python
message = "Hello " + name
```

Prefer:

```python
message = f"Hello {name}"
```

---

## 14. Avoid Multiple Statements on One Line

Correct:

```python
x = 10
y = 20

print(x + y)
```

Incorrect:

```python
x = 10; y = 20; print(x + y)
```

Keep one statement per line for readability.

---

## 15. List Comprehensions

List comprehensions are useful for creating lists concisely.

Correct:

```python
squares = [number ** 2 for number in range(10)]
```

With a condition:

```python
even_numbers = [
    number
    for number in range(20)
    if number % 2 == 0
]
```

Avoid excessively complicated comprehensions. Use a normal loop when it improves readability.

---

## 16. Exception Handling

Use specific exceptions instead of catching every exception.

Correct:

```python
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("Please enter a valid integer.")
```

Incorrect:

```python
try:
    number = int(input("Enter a number: "))
except:
    print("Something went wrong.")
```

Avoid bare `except` unless there is a specific reason.

---

## 17. File Handling

Use context managers (`with`) when working with files.

Correct:

```python
with open("data.csv", "r", encoding="utf-8") as file:
    data = file.read()
```

Incorrect:

```python
file = open("data.csv", "r")
data = file.read()
file.close()
```

The `with` statement automatically closes the file.

---

## 18. Return Statements

Avoid unnecessary `else` after a return statement.

Correct:

```python
def check_age(age):
    if age >= 18:
        return "Adult"

    return "Minor"
```

Less readable:

```python
def check_age(age):
    if age >= 18:
        return "Adult"
    else:
        return "Minor"
```

---

## 19. Don't Use Mutable Default Arguments

Avoid using lists or dictionaries as default function arguments.

Incorrect:

```python
def add_student(name, students=[]):
    students.append(name)
    return students
```

Correct:

```python
def add_student(name, students=None):
    if students is None:
        students = []

    students.append(name)
    return students
```

Mutable default arguments are created once when the function is defined, not every time it is called.

---

## 20. File and Module Naming

- Use lowercase module names.
- Use short and descriptive names.
- Use underscores when necessary.
- Avoid spaces in filenames.

Correct:

```text
main.py
data_analysis.py
student_details.py
```

Incorrect:

```text
MainFile.py
Data Analysis.py
StudentDetailsFile.py
```

---

## 21. PEP 8 Tools

You can use automated tools to identify and fix style issues.

### Flake8

Checks Python code against style and quality rules.

Install:

```bash
pip install flake8
```

Check a file:

```bash
flake8 main.py
```

Check an entire project:

```bash
flake8 .
```

Set maximum line length:

```bash
flake8 --max-line-length=79 .
```

### Ruff

A fast Python linter and formatter.

Install:

```bash
pip install ruff
```

Check code:

```bash
ruff check .
```

Automatically fix supported issues:

```bash
ruff check --fix .
```

Format code:

```bash
ruff format .
```

### Black

An opinionated Python code formatter.

Install:

```bash
pip install black
```

Format a file:

```bash
black main.py
```

Format an entire project:

```bash
black .
```

---

## 22. VS Code PEP 8 Setup

Recommended extensions:

- Python
- Pylance
- Ruff

Useful settings in `settings.json`:

```json
{
    "editor.formatOnSave": true,
    "editor.rulers": [79],
    "editor.tabSize": 4,
    "editor.insertSpaces": true,
    "files.trimTrailingWhitespace": true,
    "[python]": {
        "editor.defaultFormatter": "charliermarsh.ruff"
    }
}
```

This helps maintain consistent formatting while coding.

---

## 23. Quick Revision Table

| Rule | Recommendation |
|---|---|
| Indentation | 4 spaces |
| Maximum code line length | 79 characters |
| Comment/docstring line length | 72 characters |
| Functions | snake_case |
| Variables | snake_case |
| Classes | PascalCase |
| Constants | UPPER_CASE |
| Modules | lowercase |
| Imports | At the top of the file |
| Blank lines | 2 between top-level definitions |
| Operators | Spaces around operators |
| Commas | One space after commas |
| Strings | Prefer f-strings |
| File handling | Use `with` |
| None comparison | Use `is None` |
| Boolean comparison | Use `if condition:` |
| Exceptions | Catch specific exceptions |
| Mutable defaults | Use `None` instead |

---
