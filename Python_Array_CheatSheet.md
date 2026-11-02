# Python Arrays & Lists

## 1. Lists

A list is used to store multiple values in a single variable.

- Ordered (maintains insertion order).
- Mutable (we can modify elements).
- Allows duplicate values.
- Can store different data types.

```python
numbers = [10, 20, 30, 40, 50]

# Empty list
my_list = []

# Different data types
data = [10, "Python", 3.14, True]
```

### Accessing elements

Python uses zero-based indexing.

```python
numbers = [10, 20, 30, 40, 50]

numbers[0]     # 10
numbers[2]     # 30
numbers[-1]    # 50 (last element)
numbers[-2]    # 40
```

### Slicing

Syntax: `list[start:end:step]`

```python
numbers = [10, 20, 30, 40, 50, 60]

numbers[0:3]    # [10, 20, 30]
numbers[:3]     # First 3 elements
numbers[2:]     # From index 2 till end
numbers[::2]    # Every second element
numbers[::-1]   # Reverse the list
numbers[-3:]    # Last 3 elements
```

## 2. Adding elements

```python
numbers = [10, 20, 30]

numbers.append(40)           # Adds one element
numbers.extend([50, 60])     # Adds multiple elements
numbers.insert(1, 15)        # Adds at a particular index
```

### append() vs extend()

```python
numbers = [1, 2, 3]

numbers.append([4, 5])
# [1, 2, 3, [4, 5]]

numbers = [1, 2, 3]

numbers.extend([4, 5])
# [1, 2, 3, 4, 5]
```

Remember:
- append() adds the entire object as one element.
- extend() adds elements individually.

## 3. Removing elements

```python
numbers = [10, 20, 30, 40, 50]

numbers.remove(30)    # Removes by value
numbers.pop(1)        # Removes element at index 1
numbers.pop()         # Removes last element

del numbers[0]        # Deletes element at index 0
del numbers[0:2]      # Deletes a range

numbers.clear()       # Removes all elements
```

| Method | Use |
|---|---|
| remove() | Remove an element by value |
| pop() | Remove and return an element |
| del | Delete element or range |
| clear() | Empty the entire list |

## 4. Searching in lists

```python
numbers = [10, 20, 30, 40, 20]

20 in numbers           # True
100 not in numbers      # True

numbers.index(30)       # Returns index: 2
numbers.count(20)       # Returns count: 2
```

## 5. Sorting and reversing

```python
numbers = [40, 10, 50, 20, 30]

numbers.sort()                    # Ascending order
numbers.sort(reverse=True)        # Descending order

numbers.reverse()                 # Reverses existing list

new_list = sorted(numbers)        # Creates a sorted copy
```

Difference:

- sort() changes the original list.
- sorted() returns a new sorted list.

## 6. Some useful built-in functions

```python
numbers = [10, 20, 30, 40, 50]

len(numbers)       # Number of elements
sum(numbers)       # Sum of elements
min(numbers)       # Smallest element
max(numbers)       # Largest element

average = sum(numbers) / len(numbers)

all([True, True])       # True if all are True
any([False, True])      # True if at least one is True
```

## 7. Looping through lists

```python
numbers = [10, 20, 30, 40]

# Normal iteration
for number in numbers:
    print(number)

# Using index
for index in range(len(numbers)):
    print(numbers[index])

# Using enumerate
for index, number in enumerate(numbers):
    print(index, number)
```

`enumerate()` is useful when we need both index and value.

## 8. List comprehension

A shorter way of creating lists using an existing iterable.

Syntax:

`[expression for item in iterable if condition]`

```python
numbers = [1, 2, 3, 4, 5]

# Square of each number
squares = [number ** 2 for number in numbers]

# Get even numbers
even_numbers = [
    number for number in numbers
    if number % 2 == 0
]

# Get odd numbers
odd_numbers = [
    number for number in numbers
    if number % 2 != 0
]

# If-else
result = [
    "Even" if number % 2 == 0 else "Odd"
    for number in numbers
]
```

## 9. Copying lists

Important concept: Python variables store references to objects.

### Assignment

Both variables point to the same list.

```python
original = [10, 20, 30]

copied = original
copied.append(40)

print(original)  # [10, 20, 30, 40]
```

### Shallow copy

Creates a new outer list.

```python
original = [10, 20, 30]

copied = original.copy()
copied.append(40)

print(original)  # [10, 20, 30]
print(copied)    # [10, 20, 30, 40]
```

Other ways:

```python
copied = original[:]
copied = list(original)
```

### Deep copy

Useful when working with nested lists.

```python
import copy

original = [[1, 2], [3, 4]]

copied = copy.deepcopy(original)

copied[0].append(5)

print(original)  # [[1, 2], [3, 4]]
print(copied)    # [[1, 2, 5], [3, 4]]
```

## 10. Nested lists (2D lists)

A list can contain other lists.

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

print(matrix[0][0])    # 1
print(matrix[1][2])    # 6

# Iterating through a matrix
for row in matrix:
    for element in row:
        print(element)
```

Creating a 2D list:

```python
rows = 3
columns = 4

matrix = [
    [0 for column in range(columns)]
    for row in range(rows)
]
```

Be careful with:

```python
matrix = [[0] * 4] * 3
```

All rows refer to the same inner list. Modifying one row will affect the others.

## 11. Tuples

Tuples are similar to lists, but they cannot be modified after creation.

```python
numbers = (10, 20, 30, 40)

numbers[0]       # 10
numbers[-1]      # 40

numbers.count(20)
numbers.index(30)
```

For a tuple with one element:

```python
numbers = (10,)
```

| List | Tuple |
|---|---|
| Mutable | Immutable |
| Uses [] | Uses () |
| Can add/remove elements | Cannot modify elements |
| Used for dynamic data | Used for fixed data |

## 12. Python Array module

Python has an array module that stores elements of the same data type.

```python
from array import array

numbers = array('i', [10, 20, 30, 40])

numbers.append(50)
numbers.insert(1, 15)
numbers.remove(30)
numbers.pop()

print(numbers)
```

Some common type codes:

| Type code | Meaning |
|---|---|
| i | Signed integer |
| I | Unsigned integer |
| f | Float |
| d | Double |

## 13. NumPy arrays

NumPy is commonly used for mathematical operations and data analytics.

Installation:

```bash
pip install numpy
```

Creating arrays:

```python
import numpy as np

numbers = np.array([10, 20, 30, 40])

# 2D array
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

np.zeros(5)
np.ones(5)
np.arange(1, 10)
np.linspace(1, 10, 5)
```

### Operations on arrays

Unlike normal Python lists, NumPy arrays support element-wise mathematical operations.

```python
numbers = np.array([10, 20, 30, 40])

numbers + 10
numbers * 2
numbers ** 2

np.sum(numbers)
np.mean(numbers)
np.min(numbers)
np.max(numbers)
np.median(numbers)
np.std(numbers)
```

### Indexing and slicing

```python
numbers = np.array([10, 20, 30, 40, 50])

numbers[0]
numbers[-1]
numbers[1:4]
numbers[::-1]
```

### Shape and dimensions

```python
numbers = np.array([1, 2, 3, 4, 5, 6])

numbers.shape       # (6,)
numbers.ndim        # Number of dimensions
numbers.size        # Total number of elements

matrix = numbers.reshape(2, 3)
```

### Filtering arrays

```python
numbers = np.array([10, 15, 20, 25, 30])

# Numbers greater than 20
result = numbers[numbers > 20]

# Even numbers
result = numbers[numbers % 2 == 0]

# Multiple conditions
result = numbers[(numbers > 10) & (numbers < 30)]
```

## 14. Common list problems

### Find the second-largest number

```python
numbers = [10, 20, 50, 30, 40]

unique_numbers = sorted(set(numbers))

second_largest = unique_numbers[-2]
```

### Remove duplicates

```python
numbers = [1, 2, 2, 3, 4, 4, 5]

unique_numbers = list(dict.fromkeys(numbers))
```

### Find common elements

```python
list1 = [1, 2, 3, 4]
list2 = [3, 4, 5, 6]

common = [
    number for number in list1
    if number in list2
]
```

### Flatten a nested list

```python
matrix = [[1, 2], [3, 4], [5, 6]]

result = [
    element
    for row in matrix
    for element in row
]
```

### Count frequency of elements

```python
numbers = [1, 2, 2, 3, 3, 3, 4]

frequency = {}

for number in numbers:
    frequency[number] = frequency.get(number, 0) + 1

print(frequency)
```

