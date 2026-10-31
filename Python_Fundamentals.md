# Python Fundamentals – Quick Cheatsheet

## 1. Print, Variables & Data Types

```python
print("Hello World")
print(10, 20, 30, sep="-")  # 10-20-30
print(10, end=" ")          # Prevents new line
```

| Function | Purpose | Example |
|---|---|---|
| `print()` | Display output | `print("Hello")` |
| `type()` | Check datatype | `type(10)` |
| `input()` | Take user input | `input("Enter: ")` |

### Data Types

| Type | Example |
|---|---|
| `int` | `10`, `-20` |
| `float` | `10.5`, `3.14` |
| `str` | `"Hello"` |
| `bool` | `True`, `False` |
| `NoneType` | `None` |

### Variable Naming Rules

- Must start with a letter (`a-z`, `A-Z`) or underscore (`_`).
- Cannot start with a number.
- Cannot contain spaces or special characters.
- Variable names are case-sensitive (`name` != `Name`).
- Python keywords cannot be used as variable names.

---

## 2. Type Casting

Converting one datatype into another.

| Function | Purpose | Example |
|---|---|---|
| `int()` | Convert to integer | `int("123")` |
| `float()` | Convert to float | `float("12.5")` |
| `str()` | Convert to string | `str(123)` |
| `bool()` | Convert to Boolean | `bool(0)` |

### Examples

```python
int("123")           # 123
int(3.99)            # 3
int(-7.8)            # -7
int(True)            # 1
int(False)           # 0

float("12.5")        # 12.5
float(10)            # 10.0

str(123)             # "123"
str(True)            # "True"

int(float("3.99"))   # 3
```

### Truthy and Falsy Values

**Falsy values:**
```python
False
0
0.0
0j
""
[]
()
{}
set()
None
```

Everything else is generally truthy.

```python
bool(0)          # False
bool(0.0)        # False
bool("")         # False
bool(" ")        # True
bool("0")        # True
bool("False")    # True
bool(100)        # True
```

**Important:** `int("3.99")` raises `ValueError`. Use `int(float("3.99"))`.

---

## 3. User Input

`input()` always returns a string.

```python
name = input("Enter name: ")
age = int(input("Enter age: "))
salary = float(input("Enter salary: "))
```

### Addition of Two Numbers

```python
a = int(input("Enter first number: "))
b = int(input("Enter second number: "))

print("Addition =", a + b)
```

**Important:**

```python
"10" + "20"       # "1020" (String concatenation)
10 + 20           # 30 (Mathematical addition)
```

---

## 4. Print Parameters: sep and end

| Parameter | Purpose | Default |
|---|---|---|
| `sep` | Separates multiple values | Space `" "` |
| `end` | Defines what appears at the end | Newline `"\n"` |

```python
print(1, 2, 3, sep="-")       # 1-2-3
print(1, 2, 3, sep="@")       # 1@2@3
print(1, 2, 3, sep="\n")      # Each value on new line

print(1, end=" ")
print(2, end=" ")
print(3)                      # 1 2 3
```

---

## 5. Operators

### Arithmetic Operators

| Operator | Meaning | Example | Output |
|---|---|---|---|
| `+` | Addition | `5 + 2` | `7` |
| `-` | Subtraction | `5 - 2` | `3` |
| `*` | Multiplication | `5 * 2` | `10` |
| `/` | Division | `5 / 2` | `2.5` |
| `%` | Modulus (remainder) | `5 % 2` | `1` |
| `//` | Floor division | `5 // 2` | `2` |
| `**` | Exponentiation | `2 ** 3` | `8` |

**Important Points:**

- String + String = Concatenation.
- String * Integer = String repetition.
- `/` always returns a float.
- `//` rounds towards negative infinity.
- `%` returns the remainder.

```python
"Hi" * 3        # HiHiHi

8 / 2           # 4.0
8 // 3          # 2

-10 // 3        # -4
int(-3.9)       # -3

5 % 2           # 1
2 ** 3          # 8
2 ** 0.5        # 1.414...
```

### Comparison Operators

Comparison operators return `True` or `False`.

| Operator | Meaning | Example |
|---|---|---|
| `==` | Equal to | `5 == 5` |
| `!=` | Not equal to | `5 != 3` |
| `>` | Greater than | `5 > 3` |
| `<` | Less than | `3 < 5` |
| `>=` | Greater than or equal | `5 >= 5` |
| `<=` | Less than or equal | `3 <= 5` |

```python
2 == 2.0       # True
2 == "2"       # False
10 < 15 < 20   # True
20 > 10 < 12   # True
```

**Remember:**
- `=` means assignment.
- `==` means comparison.

### Assignment Operators

| Operator | Equivalent |
|---|---|
| `a += 5` | `a = a + 5` |
| `a -= 5` | `a = a - 5` |
| `a *= 5` | `a = a * 5` |
| `a /= 5` | `a = a / 5` |
| `a //= 5` | `a = a // 5` |
| `a %= 5` | `a = a % 5` |
| `a **= 2` | `a = a ** 2` |

---

## 6. Logical Operators

| Operator | Meaning |
|---|---|
| `and` | Both conditions must be True |
| `or` | At least one condition must be True |
| `not` | Reverses the Boolean result |

### Truth Table

| A | B | A and B | A or B |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

### Examples

```python
True and True       # True
True and False      # False

True or False       # True
False or False      # False

not True            # False
not False           # True
```

### Important: Python's and/or Behaviour

`and` returns the first falsy value; otherwise, the last value.

`or` returns the first truthy value; otherwise, the last value.

```python
10 and 20           # 20
0 and 20            # 0
1 and 2 and 3       # 3

4 or 5              # 4
0 or 5              # 5
45 or 60 or 100     # 45
```

`not` always returns a Boolean.

---

## 7. Operator Precedence

Higher priority to lower priority:

| Priority | Operators |
|---|---|
| 1 | `()` |
| 2 | `**` |
| 3 | Unary `+`, `-` |
| 4 | `*`, `/`, `//`, `%` |
| 5 | `+`, `-` |
| 6 | `<`, `>`, `<=`, `>=`, `==`, `!=` |
| 7 | `not` |
| 8 | `and` |
| 9 | `or` |

```python
print(10 + 2 * 5)      # 20
print((10 + 2) * 5)    # 60
```

Parentheses can be used to control evaluation order.

---

## 8. Conditional Statements

Conditional statements execute code based on conditions.

### if

```python
if condition:
    statement
```

### if-else

```python
if condition:
    statement1
else:
    statement2
```

### if-elif-else

```python
if condition1:
    statement1
elif condition2:
    statement2
else:
    statement3
```

### Nested if

An `if` statement inside another `if` statement.

```python
if condition1:
    if condition2:
        print("Both conditions satisfied")
```

**Important:** Indentation defines the code block.

### Example: Grade Calculator

```python
marks = int(input("Enter marks: "))

if 90 < marks <= 100:
    print("Grade A")
elif 80 < marks <= 90:
    print("Grade B")
elif 70 < marks <= 80:
    print("Grade C")
elif 0 < marks <= 70:
    print("Grade D")
else:
    print("Invalid marks")
```

---

## 9. Common Problem Patterns

### Even or Odd

```python
if n % 2 == 0:
    print("Even")
else:
    print("Odd")
```

### Positive, Negative or Zero

```python
if n > 0:
    print("Positive")
elif n < 0:
    print("Negative")
else:
    print("Zero")
```

### FizzBuzz

- Divisible by 3 and 5 → FizzBuzz
- Divisible by 3 only → Fizz
- Divisible by 5 only → Buzz

```python
n = int(input("Enter number: "))

if n % 3 == 0 and n % 5 == 0:
    print("FizzBuzz")
elif n % 3 == 0:
    print("Fizz")
elif n % 5 == 0:
    print("Buzz")
else:
    print("Neither")
```

---

## 10. Common Python Errors

| Error | Meaning |
|---|---|
| `SyntaxError` | Incorrect Python syntax |
| `TypeError` | Incompatible data types |
| `ValueError` | Invalid value for conversion |
| `NameError` | Variable not defined |
| `ZeroDivisionError` | Division by zero |
| `IndentationError` | Incorrect indentation |

---

