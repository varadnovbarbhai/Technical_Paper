# Python Dictionary Cheatsheet

## 1. What is a Dictionary?

A dictionary is a built-in Python data structure that stores data in **key-value pairs**.

- Keys must be unique.
- Values can be of any data type.
- Dictionaries are mutable (can be modified).
- Dictionaries preserve insertion order (Python 3.7+).
- Keys must be hashable (e.g. strings, numbers, tuples containing hashable elements).

### Syntax

```python
student = {
    "name": "Varad",
    "age": 25,
    "city": "Pune"
}
```

Accessing values:

```python
print(student["name"])
print(student["age"])
```

Output:

```text
Varad
25
```

---

## 2. Creating Dictionaries

### Empty dictionary

```python
student = {}
```

Alternative:

```python
student = dict()
```

### Dictionary with values

```python
student = {
    "name": "Varad",
    "age": 25,
    "marks": 90
}
```

### Using dict()

```python
student = dict(name="Varad", age=25)
```

### Dictionary with different data types

```python
student = {
    "name": "Varad",
    "age": 25,
    "marks": [80, 90, 95],
    "is_passed": True
}
```

### Dictionary with nested dictionaries

```python
students = {
    "student1": {
        "name": "Varad",
        "age": 25
    },
    "student2": {
        "name": "Rahul",
        "age": 24
    }
}
```

---

## 3. Accessing Dictionary Elements

### Using square brackets

```python
student = {"name": "Varad", "age": 25}

print(student["name"])
```

Note: If the key does not exist, Python raises a `KeyError`.

### Using get()

```python
print(student.get("name"))
```

If the key does not exist:

```python
print(student.get("city"))
```

Output:

```text
None
```

Provide a default value:

```python
print(student.get("city", "Not Available"))
```

Output:

```text
Not Available
```

**Difference:**

| Method | Missing key |
|---|---|
| `student["city"]` | Raises KeyError |
| `student.get("city")` | Returns None |
| `student.get("city", "Unknown")` | Returns Unknown |

---

## 4. Adding Elements

### Add a new key-value pair

```python
student = {"name": "Varad"}

student["age"] = 25

print(student)
```

Output:

```python
{"name": "Varad", "age": 25}
```

### Add multiple elements using update()

```python
student.update({
    "city": "Pune",
    "marks": 90
})
```

### Using setdefault()

Adds a key only if it does not already exist.

```python
student = {"name": "Varad"}

student.setdefault("age", 25)
student.setdefault("name", "Rahul")

print(student)
```

Output:

```python
{"name": "Varad", "age": 25}
```

`name` remains Varad because it already exists.

---

## 5. Updating Dictionary Elements

### Update an existing value

```python
student = {
    "name": "Varad",
    "age": 25
}

student["age"] = 26
```

### Update multiple values

```python
student.update({
    "age": 26,
    "city": "Mumbai"
})
```

Remember:
- `update()` modifies the original dictionary.
- Existing keys get new values.
- New keys are added.

---

## 6. Removing Elements

### pop()

Removes a specific key and returns its value.

```python
student = {
    "name": "Varad",
    "age": 25,
    "city": "Pune"
}

age = student.pop("age")

print(age)
print(student)
```

### popitem()

Removes and returns the last inserted key-value pair.

```python
student.popitem()
```

### del

Deletes a specific key.

```python
del student["city"]
```

### clear()

Removes all elements.

```python
student.clear()
```

### Comparison

| Method | Purpose |
|---|---|
| `pop(key)` | Removes specified key and returns value |
| `popitem()` | Removes last inserted pair |
| `del dict[key]` | Deletes specified key |
| `clear()` | Removes all elements |

---

## 7. Dictionary Methods

### keys()

Returns all keys.

```python
student = {"name": "Varad", "age": 25}

print(student.keys())
```

### values()

Returns all values.

```python
print(student.values())
```

### items()

Returns key-value pairs as tuples.

```python
print(student.items())
```

Output:

```python
dict_items([
    ("name", "Varad"),
    ("age", 25)
])
```

### copy()

Creates a shallow copy of the dictionary.

```python
student_copy = student.copy()
```

### get()

Returns the value associated with a key.

```python
print(student.get("name"))
```

### update()

Updates the dictionary.

```python
student.update({"age": 26})
```

### setdefault()

Returns the value of a key. If the key does not exist, inserts it with the specified default value.

```python
student.setdefault("city", "Pune")
```

### fromkeys()

Creates a dictionary using a sequence of keys and a common value.

```python
keys = ["name", "age", "city"]

student = dict.fromkeys(keys, None)

print(student)
```

Output:

```python
{
    "name": None,
    "age": None,
    "city": None
}
```

**Important:** Avoid using mutable values with `fromkeys()` if you expect each key to have an independent list or dictionary.

---

## 8. Iterating Through Dictionaries

### Iterate through keys

```python
student = {
    "name": "Varad",
    "age": 25,
    "city": "Pune"
}

for key in student:
    print(key)
```

Alternative:

```python
for key in student.keys():
    print(key)
```

### Iterate through values

```python
for value in student.values():
    print(value)
```

### Iterate through keys and values

Use `items()`:

```python
for key, value in student.items():
    print(key, value)
```

Output:

```text
name Varad
age 25
city Pune
```

---

## 9. Checking Whether a Key Exists

Use the `in` operator.

```python
student = {
    "name": "Varad",
    "age": 25
}

if "name" in student:
    print("Key exists")
```

Check whether a key does not exist:

```python
if "city" not in student:
    print("Key does not exist")
```

**Important:** By default, `in` checks dictionary keys, not values.

To check values:

```python
if "Varad" in student.values():
    print("Value exists")
```

---

## 10. Dictionary Length

Use `len()` to count key-value pairs.

```python
student = {
    "name": "Varad",
    "age": 25,
    "city": "Pune"
}

print(len(student))
```

Output:

```text
3
```

---

## 11. Nested Dictionaries

A dictionary can contain another dictionary.

```python
students = {
    1: {
        "name": "Varad",
        "marks": 90
    },
    2: {
        "name": "Rahul",
        "marks": 85
    }
}
```

### Access nested values

```python
print(students[1]["name"])
```

Output:

```text
Varad
```

### Update nested values

```python
students[1]["marks"] = 95
```

### Iterate through nested dictionaries

```python
for student_id, details in students.items():
    print(student_id, details["name"], details["marks"])
```

---

## 12. Dictionary Comprehension

Dictionary comprehension is a short way to create dictionaries.

### Basic syntax

```python
{key: value for item in iterable}
```

### Example 1: Squares

```python
squares = {
    number: number ** 2
    for number in range(1, 6)
}

print(squares)
```

Output:

```python
{
    1: 1,
    2: 4,
    3: 9,
    4: 16,
    5: 25
}
```

### Example 2: With condition

```python
even_squares = {
    number: number ** 2
    for number in range(1, 11)
    if number % 2 == 0
}
```

### Example 3: Convert two lists into a dictionary

```python
names = ["Varad", "Rahul", "Amit"]
ages = [25, 24, 26]

students = {
    name: age
    for name, age in zip(names, ages)
}
```

### Example 4: Convert keys to uppercase

```python
student = {
    "name": "Varad",
    "city": "Pune"
}

uppercase_student = {
    key.upper(): value
    for key, value in student.items()
}
```

---

## 13. Sorting Dictionaries

### Sort by keys

```python
student = {
    "c": 30,
    "a": 10,
    "b": 20
}

sorted_student = dict(sorted(student.items()))
```

Output:

```python
{"a": 10, "b": 20, "c": 30}
```

### Sort by values

```python
sorted_student = dict(
    sorted(student.items(), key=lambda item: item[1])
)
```

### Sort in descending order

```python
sorted_student = dict(
    sorted(
        student.items(),
        key=lambda item: item[1],
        reverse=True
    )
)
```

---

## 14. Merging Dictionaries

### Using update()

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

dict1.update(dict2)

print(dict1)
```

Note: `dict1` is modified.

### Using | operator (Python 3.9+)

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

merged = dict1 | dict2
```

This creates a new dictionary.

### Using unpacking

```python
merged = {**dict1, **dict2}
```

**Important:** If both dictionaries contain the same key, the value from the right-hand dictionary takes precedence.

---

## 15. Copying Dictionaries

### Shallow copy

```python
original = {
    "name": "Varad",
    "marks": [80, 90]
}

copied = original.copy()
```

A shallow copy creates a new outer dictionary, but nested mutable objects are still shared.

Example:

```python
copied["marks"].append(95)

print(original["marks"])
```

Output:

```python
[80, 90, 95]
```

### Deep copy

```python
import copy

original = {
    "name": "Varad",
    "marks": [80, 90]
}

copied = copy.deepcopy(original)
```

A deep copy also copies nested objects.

Changes to nested mutable objects in the copied dictionary do not affect the original.

---

## 16. Useful Built-in Functions

| Function | Purpose |
|---|---|
| `len(dict)` | Number of key-value pairs |
| `str(dict)` | Convert dictionary to string |
| `type(dict)` | Check data type |
| `sorted(dict)` | Return sorted list of keys |
| `min(dict)` | Smallest key |
| `max(dict)` | Largest key |
| `sum(dict.values())` | Sum of numeric values |
| `any(dict)` | Check whether any key is truthy |
| `all(dict)` | Check whether all keys are truthy |

Example:

```python
marks = {
    "Maths": 90,
    "Science": 85,
    "English": 95
}

print(len(marks))
print(sum(marks.values()))
print(max(marks.values()))
print(min(marks.values()))
```

---

## 17. Dictionary vs List vs Tuple vs Set

| Feature | Dictionary | List | Tuple | Set |
|---|---|---|---|---|
| Syntax | `{key: value}` | `[]` | `()` | `{}` |
| Ordered | Yes | Yes | Yes | No guaranteed order |
| Mutable | Yes | Yes | No | Yes |
| Duplicates | Keys unique | Allowed | Allowed | Not allowed |
| Access | By key | By index | By index | No indexing |
| Use case | Key-value data | Collection of items | Fixed collection | Unique elements |

**Note:** An empty `{}` creates a dictionary, not a set. Use `set()` to create an empty set.

---

## 18. Common Mistakes

### Mistake 1: Accessing a missing key

Incorrect:

```python
student = {"name": "Varad"}

print(student["age"])
```

Raises `KeyError`.

Better:

```python
print(student.get("age", 0))
```

### Mistake 2: Duplicate keys

```python
student = {
    "name": "Varad",
    "name": "Rahul"
}
```

The second value overwrites the first.

Result:

```python
{"name": "Rahul"}
```

### Mistake 3: Using a mutable key

Incorrect:

```python
student = {
    [1, 2]: "Varad"
}
```

Lists cannot be dictionary keys because they are mutable and unhashable.

Correct:

```python
student = {
    (1, 2): "Varad"
}
```

### Mistake 4: Modifying dictionary size while iterating

Avoid adding or deleting dictionary keys while directly iterating over it.

Incorrect:

```python
for key in student:
    del student[key]
```

Better:

```python
for key in list(student.keys()):
    del student[key]
```

Or simply:

```python
student.clear()
```

---

