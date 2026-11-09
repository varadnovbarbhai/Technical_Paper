# Python Strings Cheatsheet

A practical reference for Python string operations, indexing, slicing,
methods, formatting, and common problem-solving patterns.

## 1. What is a string?

A string is an immutable sequence of Unicode characters.

``` python
single = 'Hello'
double = "Python"
multiline = """This is
a multiline string."""
```

Strings can contain letters, digits, spaces, punctuation, symbols, and
Unicode characters.

``` python
message = "Hello @Varad! Python 3.14 😊"
```

### Immutability

You cannot change an individual character in an existing string. String
methods generally return a new string.

``` python
text = "Python"
# text[0] = "J"       # TypeError

text = "J" + text[1:] # Create a new string
print(text)           # Jython
```

## 2. String indexing

Indexing accesses one character. Positive indexes start at `0`; negative
indexes start at `-1` from the end.

``` python
text = "PYTHON"

print(text[0])   # P
print(text[2])   # T
print(text[-1])  # N
print(text[-2])  # O
```

  Character           P    Y    T    H    O    N
  ---------------- ---- ---- ---- ---- ---- ----
  Positive index      0    1    2    3    4    5
  Negative index     -6   -5   -4   -3   -2   -1

An index outside the valid range raises `IndexError`.

## 3. String slicing

Slicing extracts part of a string.

``` python
string[start:stop:step]
```

-   `start`: index to begin at (included; default is the beginning).
-   `stop`: index to stop before (excluded; default is the end).
-   `step`: how many positions to move each time (default is `1`).

``` python
text = "PYTHON"

print(text[0:3])   # PYT
print(text[2:5])   # THO
print(text[:3])    # PYT
print(text[3:])    # HON
print(text[:])     # PYTHON
print(text[::2])   # PTO
print(text[1::2])  # YHN
print(text[::-1])  # NOHTYP
print(text[-3:])   # HON
```

Remember: the stop index is not included.

## 4. Length

Use `len()` to get the number of characters. Spaces and punctuation
count too.

``` python
print(len("Python"))       # 6
print(len("Hello World"))  # 11
```

## 5. Case-conversion methods

  -------------------------------------------------------------------------
  Method                  Purpose                 Example result
  ----------------------- ----------------------- -------------------------
  `upper()`               Convert to uppercase    `"hello".upper()` →
                                                  `"HELLO"`

  `lower()`               Convert to lowercase    `"HELLO".lower()` →
                                                  `"hello"`

  `capitalize()`          Uppercase first         `"hELLO".capitalize()` →
                          character; lowercase    `"Hello"`
                          the rest                

  `title()`               Capitalize the          `"hello world".title()` →
                          beginning of each word  `"Hello World"`

  `swapcase()`            Switch uppercase and    `"PyThOn".swapcase()` →
                          lowercase               `"pYtHoN"`

  `casefold()`            Strong case             `"HELLO".casefold()` →
                          normalization for       `"hello"`
                          comparisons             
  -------------------------------------------------------------------------

``` python
text = "python programming"
print(text.upper())      # PYTHON PROGRAMMING
print(text.capitalize()) # Python programming
print(text.title())      # Python Programming
```

## 6. Searching and counting

  Method/operator     Purpose
  ------------------- -----------------------------------------------
  `find(sub)`         First index, or `-1` if not found
  `index(sub)`        First index; raises `ValueError` if not found
  `count(sub)`        Number of non-overlapping occurrences
  `startswith(sub)`   Checks the beginning
  `endswith(sub)`     Checks the ending
  `sub in text`       Checks whether a substring exists
  `sub not in text`   Checks whether a substring does not exist

``` python
text = "python programming"

print(text.find("program"))       # 7
print(text.index("python"))       # 0
print(text.count("m"))            # 2
print(text.startswith("python"))  # True
print(text.endswith("ming"))      # True
print("gram" in text)             # True
print("java" not in text)         # True
```

### `find()` versus `index()`

``` python
text = "python"

print(text.find("java"))  # -1
# print(text.index("java"))  # ValueError
```

Both return the first matching position when found. Use `find()` when a
missing value should produce `-1`; use `index()` when a missing value
should raise an error.

## 7. Removing whitespace

  Method       Purpose
  ------------ -----------------------------------------
  `strip()`    Remove leading and trailing whitespace
  `lstrip()`   Remove leading (left-side) whitespace
  `rstrip()`   Remove trailing (right-side) whitespace

``` python
text = "   Python   "

print(text.strip())   # "Python"
print(text.lstrip())  # "Python   "
print(text.rstrip())  # "   Python"
```

These methods can also accept a string of characters to remove from the
ends.

## 8. Replacing text

`replace(old, new, count)` returns a new string with replacements.

``` python
text = "apple apple apple"

print(text.replace("apple", "mango"))
# mango mango mango

print(text.replace("apple", "mango", 1))
# mango apple apple
```

## 9. Splitting and joining

### `split()`: string to list

``` python
text = "Python Java C++"
print(text.split())
# ['Python', 'Java', 'C++']

csv_text = "apple,banana,mango"
print(csv_text.split(","))
# ['apple', 'banana', 'mango']
```

With no separator, `split()` separates on runs of whitespace and ignores
leading/trailing whitespace.

### `join()`: iterable of strings to string

The separator is placed between the items.

``` python
fruits = ["apple", "banana", "mango"]

print(", ".join(fruits))
# apple, banana, mango
```

Remember: - `split()` converts a string into a list of strings. -
`join()` combines an iterable of strings into one string. - Every item
passed to `join()` must be a string.

## 10. String-checking methods

These methods return `True` or `False`.

  ---------------------------------------------------------------------------
  Method                  Returns `True` when...  Example
  ----------------------- ----------------------- ---------------------------
  `isalpha()`             All characters are      `"Python".isalpha()`
                          letters and string is   
                          non-empty               

  `isdigit()`             All characters are      `"123".isdigit()`
                          digits and string is    
                          non-empty               

  `isdecimal()`           All characters are      `"123".isdecimal()`
                          decimal characters      

  `isnumeric()`           All characters are      `"123".isnumeric()`
                          numeric characters      

  `isalnum()`             All characters are      `"abc123".isalnum()`
                          letters or numbers      

  `isspace()`             All characters are      `"  ".isspace()`
                          whitespace              

  `islower()`             Cased characters are    `"hello".islower()`
                          lowercase               

  `isupper()`             Cased characters are    `"HELLO".isupper()`
                          uppercase               

  `istitle()`             String follows          `"Hello World".istitle()`
                          title-case rules        
  ---------------------------------------------------------------------------

Examples:

``` python
print("Python".isalpha())  # True
print("123".isdigit())     # True
print("abc123".isalnum())  # True
print("hello!".islower())  # True
print("Hello World".istitle())  # True
```

An empty string returns `False` for these checking methods.

## 11. Concatenation and repetition

``` python
first = "Hello"
second = "Python"

print(first + " " + second)  # Hello Python
print("ha" * 3)              # hahaha
```

`+` joins strings. `*` repeats a string an integer number of times.

## 12. Membership operators

Use `in` and `not in` to test whether a character or substring occurs in
a string.

``` python
text = "Python Programming"

print("Python" in text)     # True
print("Java" in text)       # False
print("Java" not in text)   # True
```

Example: checking for a vowel.

``` python
vowels = "aeiou"
char = "a"

if char in vowels:
    print("Vowel")
else:
    print("Not a vowel")
```

## 13. Formatted strings (f-strings)

Place `f` before the opening quote and put variables or expressions
inside `{}`.

``` python
name = "Varad"
age = 25

print(f"My name is {name} and I am {age} years old.")
# My name is Varad and I am 25 years old.

a = 10
b = 20
print(f"Sum = {a + b}")  # Sum = 30
```

### Common formatting options

  Syntax             Purpose
  ------------------ ------------------------------------------
  `f"{price:.2f}"`   Two digits after decimal point
  `f"{number:,}"`    Thousands separators
  `f"{ratio:.2%}"`   Percentage with two decimal places
  `f"{name:<10}"`    Left-align in width 10
  `f"{name:>10}"`    Right-align in width 10
  `f"{name:^10}"`    Center-align in width 10
  `f"{value=}"`      Display expression and value (debugging)

``` python
price = 1234.567
ratio = 0.8567
name = "Python"

print(f"{price:.2f}")  # 1234.57
print(f"{price:,}")    # 1,234.567
print(f"{ratio:.2%}")  # 85.67%
print(f"{name:<10}|")
print(f"{name:>10}|")
print(f"{name:^10}|")
```

## 14. Escape characters and raw strings

  Escape   Meaning
  -------- -----------------
  `\n`     New line
  `\t`     Horizontal tab
  `\\`     Backslash
  `\'`     Single quote
  `\"`     Double quote
  `\r`     Carriage return
  `\b`     Backspace
  `\0`     Null character

``` python
print("Hello\nWorld")
print("Hello\tWorld")
print("It\'s Python")
print("A backslash: \\")
```

A raw string uses the `r` prefix. It is useful for paths and regular
expressions because backslashes are not treated as normal escape
sequences.

``` python
path = r"C:\Users\Varad\Documents"
print(path)
```

## 15. Character code conversion

Python's `ord()` returns a character's Unicode code point. `chr()`
converts a code point to a character.

``` python
print(ord("A"))  # 65
print(ord("a"))  # 97

print(chr(65))   # A
print(chr(97))   # a
```

## 16. Iterating through a string

### Direct iteration

``` python
text = "Python"

for char in text:
    print(char)
```

### Using indexes and `range()`

``` python
text = "Python"

for i in range(len(text)):
    print(i, text[i])
```

### Using `enumerate()`

``` python
text = "Python"

for index, char in enumerate(text):
    print(index, char)
```

`enumerate()` provides both the index and character.

## 17. Common string problem patterns

### Count vowels and consonants

For a lowercase English alphabet string:

``` python
def count_vowels_consonants(text):
    vowels = "aeiou"
    vowel_count = 0
    consonant_count = 0

    for char in text:
        if char in vowels:
            vowel_count += 1
        else:
            consonant_count += 1

    return [vowel_count, consonant_count]
```

If input may contain spaces, punctuation, or digits, check
`char.isalpha()` before counting it as a consonant.

### Reverse a string

``` python
text = "python"
print(text[::-1])  # nohtyp
```

### Check palindrome

``` python
def is_palindrome(text):
    return text == text[::-1]

print(is_palindrome("level"))  # True
print(is_palindrome("python")) # False
```

### Count a character

``` python
text = "programming"
print(text.count("m"))  # 2
```

### Count words

``` python
sentence = "Python is easy to learn"
words = sentence.split()
print(len(words))  # 5
```

### Character frequency using a dictionary

``` python
text = "banana"
frequency = {}

for char in text:
    if char not in frequency:
        frequency[char] = 0
    frequency[char] += 1

print(frequency)
# {'b': 1, 'a': 3, 'n': 2}
```

### Remove spaces

``` python
text = "Python is fun"
print(text.replace(" ", ""))  # Pythonisfun
```

## 18. Common mistakes to avoid

1.  **Strings are immutable:** `text[0] = "A"` raises `TypeError`.
2.  **String methods return new strings:** `text.upper()` does not
    change `text`; use `text = text.upper()` if you want to keep the
    result.
3.  **Slicing excludes the stop index:** `text[1:4]` includes indexes 1,
    2, and 3.
4.  **`find()` and `index()` differ when no match exists:** `find()`
    returns `-1`; `index()` raises `ValueError`.
5.  **`in` checks membership:** use `char in "aeiou"`, not
    `char == "aeiou"`, to check whether one character is a vowel.
6.  **`split()` returns a list:** it does not return a string.
7.  **`join()` needs strings:** convert non-string values with `str()`
    before joining them.

## 19. Quick revision table

  Task                      Syntax
  ------------------------- ------------------------------
  Uppercase                 `text.upper()`
  Lowercase                 `text.lower()`
  Reverse                   `text[::-1]`
  Length                    `len(text)`
  First character           `text[0]`
  Last character            `text[-1]`
  First three characters    `text[:3]`
  Last three characters     `text[-3:]`
  Every second character    `text[::2]`
  Find substring            `text.find("sub")`
  Count substring           `text.count("sub")`
  Replace substring         `text.replace("old", "new")`
  Split into words          `text.split()`
  Join words                `" ".join(words)`
  Remove outer whitespace   `text.strip()`
  Check substring           `"sub" in text`
  Check alphabetic          `text.isalpha()`
  Check digits              `text.isdigit()`

## 20. Practice questions

Try these without running the code first.

**Q1. What is the output?**

``` python
text = "Python"
print(text[::-1])
```

**Q2. What is the output?**

``` python
text = "programming"
print(text.count("m"))
```

**Q3. What is the output?**

``` python
text = "Hello World"
print(text[2:8:2])
```

**Q4. What happens here?**

``` python
text = "python"
print(text.find("java"))
print(text.index("java"))
```

**Q5. What is the output?**

 python
text = "apple,banana,mango"
print(text.split(","))


**Q6. What is the output?**

python
text = "Python"
print("th" in text)
print("java" not in text)

**Q7. What is the output, and why?**

 python
text = "hello"
text.upper()
print(text)


------------------------------------------------------------------------

