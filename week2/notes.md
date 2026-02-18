# Week 2: Python Fundamentals - Control Flow and Advanced Concepts

## Table of Contents
1. [Variables - Advanced Concepts](#variables-advanced-concepts)
2. [String Methods - Complete Reference](#string-methods-complete-reference)
3. [If Statements and Control Flow](#if-statements-and-control-flow)
4. [Import Statements](#import-statements)

---

## Variables - Advanced Concepts

### Dynamic Typing vs Static Typing

#### What is Dynamic Typing?
Python uses **dynamic typing**, which means you don't need to declare the type of a variable before using it. The type is determined at runtime based on the value assigned.

```python
# Dynamic Typing (Python)
x = 10          # x is an integer
x = "Hello"     # Now x is a string (type changed!)
x = 3.14        # Now x is a float
```

#### What is Static Typing?
In statically-typed languages (like Java, C++), you must declare the type of a variable, and it cannot change.

```java
// Static Typing (Java)
int x = 10;        // x is declared as integer
x = "Hello";       // ERROR! Cannot assign string to int variable
```

#### Implications of Dynamic Typing in Python

**Advantages:**
- **Flexibility:** Variables can hold any type of data
- **Less code:** No need to declare types
- **Faster development:** Write code quickly without type declarations
- **Easier to learn:** Simpler syntax for beginners

```python
# Flexible variable usage
data = 100
print(data)         # 100

data = "Python"
print(data)         # Python

data = [1, 2, 3]
print(data)         # [1, 2, 3]
```

**Disadvantages:**
- **Runtime errors:** Type errors only caught when code runs
- **Less efficient:** Type checking happens at runtime
- **Harder to debug:** Type-related bugs can be subtle
- **No compile-time checking:** Errors discovered later

```python
# Potential issues with dynamic typing
def add_numbers(a, b):
    return a + b

result = add_numbers(5, 3)        # 8 (works fine)
result = add_numbers("5", "3")    # "53" (concatenates instead!)
result = add_numbers(5, "3")      # TypeError (only at runtime)
```

#### Checking Types in Python

Use `type()` to check the current type of a variable:

```python
x = 42
print(type(x))      # <class 'int'>

x = "Hello"
print(type(x))      # <class 'str'>

# Check if variable is of specific type
x = 100
print(isinstance(x, int))      # True
print(isinstance(x, str))      # False
```

---

### Assignment Methods

#### Basic Assignment
```python
x = 10
name = "Alice"
is_student = True
```

#### Multiple Assignment
Assign the same value to multiple variables:

```python
x = y = z = 0
print(x, y, z)      # 0 0 0

a = b = c = "Same"
print(a, b, c)      # Same Same Same
```

#### Tuple Unpacking (Parallel Assignment)
Assign multiple values to multiple variables in one line:

```python
# Basic tuple unpacking
x, y, z = 1, 2, 3
print(x)    # 1
print(y)    # 2
print(z)    # 3

# Unpacking from a list
name, age, city = ["Alice", 25, "NYC"]
print(name)     # Alice
print(age)      # 25
print(city)     # NYC

# Unpacking from a tuple
coordinates = (10, 20, 30)
x, y, z = coordinates
print(x, y, z)  # 10 20 30
```

#### Swapping Values
Use tuple unpacking to swap variables without a temporary variable:

```python
# Traditional swap (requires temp variable)
a = 5
b = 10
temp = a
a = b
b = temp
print(a, b)     # 10 5

# Python swap (elegant!)
x = 5
y = 10
x, y = y, x
print(x, y)     # 10 5
```

#### Unpacking with Rest Operator (*)
Use `*` to collect remaining values:

```python
# Basic rest operator
first, *rest = [1, 2, 3, 4, 5]
print(first)    # 1
print(rest)     # [2, 3, 4, 5]

# Rest in the middle
first, *middle, last = [1, 2, 3, 4, 5]
print(first)    # 1
print(middle)   # [2, 3, 4]
print(last)     # 5

# Ignore values with underscore
first, _, third = [1, 2, 3]
print(first)    # 1
print(third)    # 3
```

---

### Shorthand Operators

Shorthand operators combine an operation with assignment.

#### Arithmetic Shorthand Operators

| Operator | Long Form | Shorthand | Example |
|----------|-----------|-----------|---------|
| += | `x = x + 5` | `x += 5` | Add and assign |
| -= | `x = x - 3` | `x -= 3` | Subtract and assign |
| *= | `x = x * 2` | `x *= 2` | Multiply and assign |
| /= | `x = x / 4` | `x /= 4` | Divide and assign |
| //= | `x = x // 3` | `x //= 3` | Floor divide and assign |
| %= | `x = x % 5` | `x %= 5` | Modulus and assign |
| **= | `x = x ** 2` | `x **= 2` | Exponent and assign |

```python
# Addition
x = 10
x += 5      # Same as: x = x + 5
print(x)    # 15

# Subtraction
y = 20
y -= 7      # Same as: y = y - 7
print(y)    # 13

# Multiplication
z = 4
z *= 3      # Same as: z = z * 3
print(z)    # 12

# Division
a = 20
a /= 4      # Same as: a = a / 4
print(a)    # 5.0

# Floor Division
b = 17
b //= 5     # Same as: b = b // 5
print(b)    # 3

# Modulus
c = 17
c %= 5      # Same as: c = c % 5
print(c)    # 2

# Exponentiation
d = 2
d **= 3     # Same as: d = d ** 3
print(d)    # 8
```

#### Shorthand with Strings
```python
# String concatenation
message = "Hello"
message += " World"     # Same as: message = message + " World"
print(message)          # "Hello World"

# String repetition
text = "Ha"
text *= 3               # Same as: text = text * 3
print(text)             # "HaHaHa"
```

#### Shorthand with Lists
```python
# List concatenation
numbers = [1, 2, 3]
numbers += [4, 5]       # Same as: numbers = numbers + [4, 5]
print(numbers)          # [1, 2, 3, 4, 5]

# List repetition
items = [0]
items *= 5              # Same as: items = items * 5
print(items)            # [0, 0, 0, 0, 0]
```

---

### Escape Characters and Quotes

#### Escape Characters
Escape characters are special character sequences that start with a backslash (`\`) and represent characters that are difficult to type or have special meaning.

| Escape Sequence | Description | Example |
|----------------|-------------|---------|
| `\n` | Newline | `"Line1\nLine2"` |
| `\t` | Tab | `"Name:\tJohn"` |
| `\\` | Backslash | `"C:\\Users"` |
| `\'` | Single quote | `'It\'s nice'` |
| `\"` | Double quote | `"She said \"Hi\""` |
| `\r` | Carriage return | `"Text\rOver"` |
| `\b` | Backspace | `"Hell\bo"` |

```python
# Newline
print("Hello\nWorld")
# Output:
# Hello
# World

# Tab
print("Name:\tAlice\nAge:\t25")
# Output:
# Name:   Alice
# Age:    25

# Backslash
print("C:\\Users\\Documents\\file.txt")
# Output: C:\Users\Documents\file.txt

# Quotes inside strings
print("She said, \"Python is awesome!\"")
# Output: She said, "Python is awesome!"

print('It\'s a beautiful day')
# Output: It's a beautiful day
```

#### Types of Quotes in Python

Python allows three types of quote styles for strings:

**1. Single Quotes (`'...'`)**
```python
message = 'Hello World'
name = 'Alice'

# Use double quotes inside without escaping
text = 'She said, "Hello"'
print(text)     # She said, "Hello"

# Need to escape single quotes
text = 'It\'s a nice day'
print(text)     # It's a nice day
```

**2. Double Quotes (`"..."`)**
```python
message = "Hello World"
name = "Bob"

# Use single quotes inside without escaping
text = "It's a beautiful day"
print(text)     # It's a beautiful day

# Need to escape double quotes
text = "He said, \"Hello\""
print(text)     # He said, "Hello"
```

**3. Triple Quotes (`'''...'''` or `"""..."""`)**
Triple quotes allow multi-line strings and can contain both single and double quotes without escaping.

```python
# Multi-line string with triple double quotes
paragraph = """This is a long paragraph.
It spans multiple lines.
No need to use \n for newlines."""

print(paragraph)
# Output:
# This is a long paragraph.
# It spans multiple lines.
# No need to use \n for newlines.

# Multi-line string with triple single quotes
poem = '''Roses are red,
Violets are blue,
Python is great,
And so are you!'''

print(poem)

# Can contain both quote types
text = """He said, "It's a nice day!" """
print(text)     # He said, "It's a nice day!"
```

#### Raw Strings (r-prefix)
Raw strings treat backslashes as literal characters (useful for regex, file paths):

```python
# Normal string (backslashes are escape characters)
path = "C:\new\test"
print(path)         # C:
                    # ew  est (weird output!)

# Raw string (backslashes are literal)
path = r"C:\new\test"
print(path)         # C:\new\test

# Useful for regular expressions
pattern = r"\d+\.\d+"
print(pattern)      # \d+\.\d+
```

#### Comparing Quote Styles

```python
# All these are equivalent:
s1 = "Hello"
s2 = 'Hello'
print(s1 == s2)     # True

# Choose based on content
text1 = "It's easy"              # Use double quotes (easier)
text2 = 'He said "Hi"'           # Use single quotes (easier)
text3 = "He said, \"It's ok\""   # Need escaping (less clean)

# Best practice: Be consistent in your code
# Many Python style guides prefer double quotes
```

---

## String Methods - Complete Reference

### Important: String Immutability

**Strings in Python are immutable** - they cannot be changed after creation. String methods return **new strings** and don't modify the original.

```python
text = "hello"
result = text.upper()

print(text)         # "hello" (original unchanged)
print(result)       # "HELLO" (new string)

# You can reassign the variable
text = text.upper()
print(text)         # "HELLO" (variable now holds new string)
```

---

### Case Conversion Methods

#### 1. `lower()` - Convert to Lowercase
Returns a string with all characters in lowercase.

```python
text = "HELLO World"
result = text.lower()
print(result)       # "hello world"

# Useful for case-insensitive comparisons
user_input = "Yes"
if user_input.lower() == "yes":
    print("Confirmed!")     # This will print
```

#### 2. `upper()` - Convert to Uppercase
Returns a string with all characters in uppercase.

```python
text = "hello World"
result = text.upper()
print(result)       # "HELLO WORLD"

# Common use case
password = "secret123"
print(password.upper())     # "SECRET123"
```

#### 3. `capitalize()` - Capitalize First Letter
Returns a string with the first letter capitalized and the rest lowercase.

```python
text = "hello world"
result = text.capitalize()
print(result)       # "Hello world"

text = "PYTHON programming"
result = text.capitalize()
print(result)       # "Python programming"

# Note: Only first letter capitalized, rest become lowercase
text = "hELLO wORLD"
print(text.capitalize())    # "Hello world"
```

#### 4. `title()` - Title Case
Returns a string with the first letter of each word capitalized.

```python
text = "hello world from python"
result = text.title()
print(result)       # "Hello World From Python"

text = "HELLO WORLD"
print(text.title())         # "Hello World"

# Works with various word separators
text = "python-programming is_fun"
print(text.title())         # "Python-Programming Is_Fun"
```

#### 5. `swapcase()` - Swap Case
Returns a string with uppercase letters converted to lowercase and vice versa.

```python
text = "Hello World"
result = text.swapcase()
print(result)       # "hELLO wORLD"

text = "PyThOn 3.11"
print(text.swapcase())      # "pYtHoN 3.11"
```

**Comparison of Case Methods:**
```python
original = "hELLo WoRLD"

print(original.lower())         # "hello world"
print(original.upper())         # "HELLO WORLD"
print(original.capitalize())    # "Hello world"
print(original.title())         # "Hello World"
print(original.swapcase())      # "HellO wOrld"
```

---

### Character Type Checking Methods

These methods return `True` or `False` based on the content of the string.

#### 6. `isdigit()` - Check if All Characters are Digits
Returns `True` if all characters are digits (0-9).

```python
text = "12345"
print(text.isdigit())       # True

text = "123.45"
print(text.isdigit())       # False (contains '.')

text = "abc123"
print(text.isdigit())       # False (contains letters)

text = ""
print(text.isdigit())       # False (empty string)

# Practical use
user_input = input("Enter your age: ")
if user_input.isdigit():
    age = int(user_input)
    print("Valid age:", age)
else:
    print("Please enter numbers only")
```

#### 7. `isalpha()` - Check if All Characters are Alphabetic
Returns `True` if all characters are letters (a-z, A-Z).

```python
text = "Hello"
print(text.isalpha())       # True

text = "Hello123"
print(text.isalpha())       # False (contains digits)

text = "Hello World"
print(text.isalpha())       # False (contains space)

text = "HelloWorld"
print(text.isalpha())       # True

# Practical use
name = input("Enter your name: ")
if name.isalpha():
    print("Valid name")
else:
    print("Name should contain only letters")
```

#### 8. `isalnum()` - Check if All Characters are Alphanumeric
Returns `True` if all characters are letters or digits (no spaces or special characters).

```python
text = "Hello123"
print(text.isalnum())       # True

text = "User2024"
print(text.isalnum())       # True

text = "Hello World"
print(text.isalnum())       # False (contains space)

text = "User@123"
print(text.isalnum())       # False (contains @)

# Practical use - validate username
username = "User123"
if username.isalnum():
    print("Valid username")
else:
    print("Username can only contain letters and numbers")
```

**Comparison:**
```python
text1 = "Python"
print(text1.isdigit())      # False
print(text1.isalpha())      # True
print(text1.isalnum())      # True

text2 = "12345"
print(text2.isdigit())      # True
print(text2.isalpha())      # False
print(text2.isalnum())      # True

text3 = "Python123"
print(text3.isdigit())      # False
print(text3.isalpha())      # False
print(text3.isalnum())      # True
```

---

### Whitespace Removal Methods

#### 9. `strip()` - Remove Leading and Trailing Whitespace
Removes spaces, tabs, and newlines from both ends.

```python
text = "   Hello World   "
result = text.strip()
print(result)               # "Hello World"
print(len(text))            # 18
print(len(result))          # 11

# Remove specific characters
text = "###Hello###"
result = text.strip("#")
print(result)               # "Hello"

# Useful for cleaning user input
user_input = input("Enter your name: ")  # User types "  Alice  "
clean_name = user_input.strip()          # "Alice"
```

#### 10. `lstrip()` - Remove Leading (Left) Whitespace
Removes whitespace only from the beginning (left side).

```python
text = "   Hello World   "
result = text.lstrip()
print(result)               # "Hello World   "
print(repr(result))         # 'Hello World   ' (repr shows spaces)

# Remove specific characters from left
text = "###Hello###"
result = text.lstrip("#")
print(result)               # "Hello###"
```

#### 11. `rstrip()` - Remove Trailing (Right) Whitespace
Removes whitespace only from the end (right side).

```python
text = "   Hello World   "
result = text.rstrip()
print(result)               # "   Hello World"
print(repr(result))         # '   Hello World'

# Remove specific characters from right
text = "###Hello###"
result = text.rstrip("#")
print(result)               # "###Hello"
```

**Comparison:**
```python
text = "   Hello World   "

print(repr(text.strip()))       # 'Hello World'
print(repr(text.lstrip()))      # 'Hello World   '
print(repr(text.rstrip()))      # '   Hello World'
```

---

### Search and Check Methods

#### 12. `startswith()` - Check if String Starts With Substring
Returns `True` if the string starts with the specified substring.

```python
text = "Hello World"
print(text.startswith("Hello"))     # True
print(text.startswith("World"))     # False
print(text.startswith("H"))         # True

# Case-sensitive
print(text.startswith("hello"))     # False

# Can specify start position
text = "Python Programming"
print(text.startswith("Program", 7))    # True (starts at index 7)

# Practical use - file extensions
filename = "document.pdf"
if filename.startswith("doc"):
    print("This is a document file")
```

#### 13. `endswith()` - Check if String Ends With Substring
Returns `True` if the string ends with the specified substring.

```python
text = "Hello World"
print(text.endswith("World"))       # True
print(text.endswith("Hello"))       # False
print(text.endswith("d"))           # True

# Case-sensitive
print(text.endswith("world"))       # False

# Practical use - file extensions
filename = "report.pdf"
if filename.endswith(".pdf"):
    print("This is a PDF file")

filename = "image.jpg"
if filename.endswith((".jpg", ".png", ".gif")):  # Check multiple
    print("This is an image file")
```

#### 14. `count()` - Count Occurrences of Substring
Returns the number of times a substring appears in the string.

```python
text = "Hello World, Hello Python"
count = text.count("Hello")
print(count)                # 2

text = "banana"
print(text.count("a"))      # 3
print(text.count("an"))     # 2
print(text.count("na"))     # 2

# Case-sensitive
text = "Hello hello HELLO"
print(text.count("hello"))  # 1

# Can specify start and end positions
text = "aaabbbaaabbb"
print(text.count("a", 3))       # 3 (count from index 3 onwards)
print(text.count("a", 0, 6))    # 3 (count from index 0 to 6)
```

#### 15. `index()` - Find Index of Substring
Returns the index of the first occurrence of substring. Raises `ValueError` if not found.

```python
text = "Hello World"
index = text.index("World")
print(index)                # 6

text = "Python Programming"
print(text.index("Pro"))    # 7
print(text.index("o"))      # 4 (first occurrence)

# ValueError if not found
try:
    index = text.index("Java")
except ValueError:
    print("Substring not found!")

# Can specify start and end
text = "Hello Hello"
print(text.index("Hello"))          # 0 (first occurrence)
print(text.index("Hello", 1))       # 6 (start searching from index 1)
```

**Note:** `find()` is similar to `index()` but returns `-1` instead of raising an error:
```python
text = "Hello World"
print(text.find("World"))       # 6
print(text.find("Java"))        # -1 (not found)

# index() vs find()
# Use find() when not finding is normal
# Use index() when not finding is an error
```

---

### Modification Methods

#### 16. `replace()` - Replace Substring
Returns a new string with all occurrences of a substring replaced.

```python
text = "Hello World"
result = text.replace("World", "Python")
print(result)               # "Hello Python"
print(text)                 # "Hello World" (original unchanged)

# Replace multiple occurrences
text = "I love apples. Apples are great!"
result = text.replace("apples", "oranges")
print(result)               # "I love oranges. Apples are great!"
# Note: case-sensitive, only "apples" replaced, not "Apples"

# Replace with case-insensitive
text = "I love apples. Apples are great!"
result = text.lower().replace("apples", "oranges")
print(result)               # "i love oranges. oranges are great!"

# Limit number of replacements
text = "one one one one"
result = text.replace("one", "two", 2)  # Replace only first 2
print(result)               # "two two one one"

# Remove substring (replace with empty string)
text = "Hello, World!"
result = text.replace(",", "")
print(result)               # "Hello World!"
```

**Practical Examples:**
```python
# Remove spaces
text = "Hello World"
no_spaces = text.replace(" ", "")
print(no_spaces)            # "HelloWorld"

# Replace multiple characters (chain calls)
text = "Hello World!"
result = text.replace("!", "").replace(" ", "_").lower()
print(result)               # "hello_world"

# Clean phone numbers
phone = "(123) 456-7890"
clean = phone.replace("(", "").replace(")", "").replace(" ", "").replace("-", "")
print(clean)                # "1234567890"
```

---

### Additional Useful String Methods

#### 17. `split()` - Split String into List
Splits a string into a list of substrings.

```python
text = "Hello World Python"
words = text.split()
print(words)                # ['Hello', 'World', 'Python']

# Split by specific delimiter
text = "apple,banana,cherry"
fruits = text.split(",")
print(fruits)               # ['apple', 'banana', 'cherry']

# Limit number of splits
text = "one two three four"
result = text.split(" ", 2)
print(result)               # ['one', 'two', 'three four']
```

#### 18. `join()` - Join List into String
Joins a list of strings into a single string with a separator.

```python
words = ["Hello", "World", "Python"]
text = " ".join(words)
print(text)                 # "Hello World Python"

# Different separators
fruits = ["apple", "banana", "cherry"]
print(", ".join(fruits))    # "apple, banana, cherry"
print("-".join(fruits))     # "apple-banana-cherry"
print("".join(fruits))      # "applebananacherry"
```

#### 19. `find()` - Find Index (Returns -1 if Not Found)
```python
text = "Hello World"
print(text.find("World"))   # 6
print(text.find("Python"))  # -1 (not found)
```

#### 20. `len()` - Get String Length
(Not a method, but a built-in function)

```python
text = "Hello World"
length = len(text)
print(length)               # 11
```

---

### String Method Chaining

You can chain multiple string methods together:

```python
text = "  HELLO world  "
result = text.strip().lower().capitalize()
print(result)               # "Hello world"

# Step by step:
# "  HELLO world  ".strip()     → "HELLO world"
# "HELLO world".lower()          → "hello world"
# "hello world".capitalize()     → "Hello world"

# Practical example
email = "  USER@EXAMPLE.COM  "
clean_email = email.strip().lower()
print(clean_email)          # "user@example.com"
```

---

### Summary Table of String Methods

| Method | Purpose | Returns | Example |
|--------|---------|---------|---------|
| `lower()` | Convert to lowercase | New string | `"HELLO".lower()` → `"hello"` |
| `upper()` | Convert to uppercase | New string | `"hello".upper()` → `"HELLO"` |
| `capitalize()` | Capitalize first letter | New string | `"hello".capitalize()` → `"Hello"` |
| `title()` | Title case | New string | `"hello world".title()` → `"Hello World"` |
| `swapcase()` | Swap case | New string | `"Hello".swapcase()` → `"hELLO"` |
| `isdigit()` | Check if digits | Boolean | `"123".isdigit()` → `True` |
| `isalpha()` | Check if alphabetic | Boolean | `"abc".isalpha()` → `True` |
| `isalnum()` | Check if alphanumeric | Boolean | `"abc123".isalnum()` → `True` |
| `strip()` | Remove whitespace (both ends) | New string | `" hi ".strip()` → `"hi"` |
| `lstrip()` | Remove whitespace (left) | New string | `" hi".lstrip()` → `"hi"` |
| `rstrip()` | Remove whitespace (right) | New string | `"hi ".rstrip()` → `"hi"` |
| `startswith()` | Check if starts with | Boolean | `"Hello".startswith("He")` → `True` |
| `endswith()` | Check if ends with | Boolean | `"Hello".endswith("lo")` → `True` |
| `count()` | Count occurrences | Integer | `"banana".count("a")` → `3` |
| `index()` | Find index (error if not found) | Integer | `"Hello".index("e")` → `1` |
| `find()` | Find index (-1 if not found) | Integer | `"Hello".find("x")` → `-1` |
| `replace()` | Replace substring | New string | `"Hi".replace("i", "o")` → `"Ho"` |

---

## If Statements and Control Flow

### What is Control Flow?

**Control flow** is the order in which individual statements, instructions, or function calls are executed in a program. By default, Python executes code line by line from top to bottom. Control flow statements allow you to change this order based on conditions.

```python
# Without control flow (linear execution)
print("Step 1")
print("Step 2")
print("Step 3")

# With control flow (conditional execution)
age = 20
if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")
```

---

### The `if` Statement

The `if` statement executes a block of code only if a condition is `True`.

#### Basic Syntax:
```python
if condition:
    # Code to execute if condition is True
    statement1
    statement2
```

**Important:** Python uses **indentation** (4 spaces or 1 tab) to define code blocks.

#### Examples:
```python
# Simple if statement
age = 20
if age >= 18:
    print("You are an adult")
# Output: You are an adult

# If condition is False, code block is skipped
age = 15
if age >= 18:
    print("You are an adult")
# No output (condition is False)

# Multiple statements in if block
score = 85
if score >= 80:
    print("Great job!")
    print("You passed with distinction")
    grade = "A"
# Output:
# Great job!
# You passed with distinction
```

---

### The `if-else` Statement

The `else` statement provides an alternative block of code when the `if` condition is `False`.

#### Syntax:
```python
if condition:
    # Code if condition is True
    statement1
else:
    # Code if condition is False
    statement2
```

#### Examples:
```python
# Basic if-else
age = 15
if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")
# Output: You cannot vote yet

# Another example
temperature = 25
if temperature > 30:
    print("It's hot outside")
else:
    print("The weather is pleasant")
# Output: The weather is pleasant

# Assigning values based on condition
score = 75
if score >= 60:
    result = "Pass"
else:
    result = "Fail"
print("Result:", result)
# Output: Result: Pass
```

---

### The `if-elif-else` Statement

The `elif` (else if) statement allows you to check multiple conditions in sequence.

#### Syntax:
```python
if condition1:
    # Code if condition1 is True
    statement1
elif condition2:
    # Code if condition2 is True
    statement2
elif condition3:
    # Code if condition3 is True
    statement3
else:
    # Code if all conditions are False
    statement4
```

#### Examples:
```python
# Grade classification
score = 75

if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

print("Grade:", grade)
# Output: Grade: C

# Traffic light system
light = "yellow"

if light == "green":
    print("Go")
elif light == "yellow":
    print("Slow down")
elif light == "red":
    print("Stop")
else:
    print("Invalid light color")
# Output: Slow down

# Multiple elif statements
age = 25

if age < 13:
    category = "Child"
elif age < 20:
    category = "Teenager"
elif age < 60:
    category = "Adult"
else:
    category = "Senior"

print("Category:", category)
# Output: Category: Adult
```

**Important Notes:**
- Python checks conditions from top to bottom
- Only the **first** `True` condition's block executes
- Once a condition is `True`, remaining `elif` and `else` are skipped

```python
# Demonstration of sequential checking
score = 95

if score >= 60:
    print("Pass")       # This executes
elif score >= 80:
    print("Good")       # This is skipped (even though True)
elif score >= 90:
    print("Excellent")  # This is skipped (even though True)

# Output: Pass (only first True condition executes)
```

---

### Nested If Statements

You can place `if` statements inside other `if` statements.

```python
# Nested if example
age = 25
has_license = True

if age >= 18:
    print("You are an adult")
    if has_license:
        print("You can drive")
    else:
        print("You need a license to drive")
else:
    print("You are too young to drive")

# Output:
# You are an adult
# You can drive

# Another example - login system
username = "admin"
password = "secret123"

if username == "admin":
    if password == "secret123":
        print("Login successful")
    else:
        print("Wrong password")
else:
    print("User not found")
# Output: Login successful
```

---

### Logical Operators in If Statements

Use logical operators to create complex conditions.

```python
# AND operator - both conditions must be True
age = 25
has_ticket = True

if age >= 18 and has_ticket:
    print("You can enter the concert")
else:
    print("Entry denied")
# Output: You can enter the concert

# OR operator - at least one condition must be True
is_weekend = False
is_holiday = True

if is_weekend or is_holiday:
    print("You can relax!")
else:
    print("Time to work")
# Output: You can relax!

# NOT operator - reverses the condition
is_raining = False

if not is_raining:
    print("Let's go for a walk")
else:
    print("Stay inside")
# Output: Let's go for a walk

# Complex conditions
age = 25
income = 50000
credit_score = 720

if age >= 21 and income >= 30000 and credit_score >= 650:
    print("Loan approved")
else:
    print("Loan denied")
# Output: Loan approved
```

---

### Comparison with Other Values

```python
# Comparing strings
name = "Alice"
if name == "Alice":
    print("Hello, Alice!")

# Comparing numbers
x = 10
y = 20
if x < y:
    print("x is smaller than y")

# Checking membership
word = "Python"
if "P" in word:
    print("Contains P")

# Checking list membership
fruits = ["apple", "banana", "cherry"]
if "banana" in fruits:
    print("We have bananas")
```

---

### Match-Case Statement (Python 3.10+)

Python 3.10 introduced the `match-case` statement, similar to `switch` in other languages.

#### Syntax:
```python
match variable:
    case value1:
        # Code for value1
    case value2:
        # Code for value2
    case _:
        # Default case (like else)
```

#### Examples:
```python
# Basic match-case
day = "Monday"

match day:
    case "Monday":
        print("Start of the week")
    case "Friday":
        print("Almost weekend!")
    case "Saturday" | "Sunday":  # Multiple patterns
        print("Weekend!")
    case _:  # Default case
        print("Midweek day")

# Output: Start of the week

# Matching numbers
status_code = 404

match status_code:
    case 200:
        print("Success")
    case 404:
        print("Not Found")
    case 500:
        print("Server Error")
    case _:
        print("Unknown status")

# Output: Not Found

# Pattern matching with conditions
age = 25

match age:
    case age if age < 13:
        print("Child")
    case age if age < 20:
        print("Teenager")
    case age if age < 60:
        print("Adult")
    case _:
        print("Senior")

# Output: Adult
```

**Note:** Match-case is only available in Python 3.10 and later. For earlier versions, use `if-elif-else`.

---

### Ternary (Conditional) Operator

A shorthand way to write simple `if-else` statements in one line.

#### Syntax:
```python
value_if_true if condition else value_if_false
```

#### Examples:
```python
# Basic ternary
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)       # "Adult"

# Equivalent to:
if age >= 18:
    status = "Adult"
else:
    status = "Minor"

# Another example
score = 85
result = "Pass" if score >= 60 else "Fail"
print(result)       # "Pass"

# In print statement
x = 10
print("Even" if x % 2 == 0 else "Odd")  # "Even"

# Nested ternary (not recommended - less readable)
score = 75
grade = "A" if score >= 90 else "B" if score >= 80 else "C" if score >= 70 else "F"
print(grade)        # "C"
```

---

### Common Patterns and Best Practices

#### 1. Validating Input
```python
age = int(input("Enter your age: "))

if age < 0:
    print("Age cannot be negative")
elif age > 150:
    print("Invalid age")
elif age < 18:
    print("You are a minor")
else:
    print("You are an adult")
```

#### 2. Multiple Conditions
```python
# Check multiple conditions
username = "admin"
password = "pass123"

if username == "admin" and password == "pass123":
    print("Access granted")
else:
    print("Access denied")
```

#### 3. Checking Empty Values
```python
name = input("Enter your name: ")

if name:  # True if name is not empty
    print("Hello,", name)
else:
    print("Name cannot be empty")
```

#### 4. Range Checking
```python
score = 75

if 0 <= score <= 100:
    print("Valid score")
else:
    print("Score must be between 0 and 100")
```

---

## Import Statements

### What are Imports?

**Imports** allow you to use code from other modules (files) or libraries in your program. Python has many built-in libraries, and you can also install external ones.

```python
# Without import - can't use math functions
# result = sqrt(16)  # Error: sqrt is not defined

# With import - can use math functions
import math
result = math.sqrt(16)
print(result)  # 4.0
```

---

### Ways to Import

#### 1. Import Entire Module
Import the entire module and use `module.function()` syntax.

```python
import math

# Use functions with module prefix
print(math.sqrt(16))        # 4.0
print(math.pi)              # 3.141592653589793
print(math.pow(2, 3))       # 8.0
```

#### 2. Import with Alias (as)
Give the module a shorter or different name.

```python
import math as m

# Use the alias
print(m.sqrt(16))           # 4.0
print(m.pi)                 # 3.141592653589793
```

**Common aliases:**
```python
import numpy as np          # Data science
import pandas as pd         # Data analysis
import matplotlib.pyplot as plt  # Plotting
```

#### 3. Import Specific Functions/Variables
Import only what you need from a module.

```python
from math import sqrt, pi

# Use directly without module prefix
print(sqrt(16))             # 4.0
print(pi)                   # 3.141592653589793
# print(math.pow(2, 3))     # Error: math is not defined
```

#### 4. Import Specific with Alias
```python
from math import sqrt as square_root

print(square_root(16))      # 4.0
# print(sqrt(16))           # Error: sqrt is not defined
```

#### 5. Import Everything (*)
Import all functions and variables from a module (not recommended).

```python
from math import *

# Use all functions directly
print(sqrt(16))             # 4.0
print(pi)                   # 3.141592653589793
print(pow(2, 3))            # 8.0
print(ceil(3.2))            # 4
print(floor(3.8))           # 3
```

**Warning:** Using `import *` can cause name conflicts and makes code less readable. It's generally not recommended.

```python
# Potential problem with import *
from math import *
from statistics import *

# If both modules have a function with same name, one overwrites the other
# This can cause confusion
```

---

### The `random` Library

The `random` library provides functions for generating random numbers and making random selections.

#### Importing random:
```python
import random
```

---

#### 1. `random.randint(a, b)` - Random Integer
Returns a random integer between `a` and `b` (both inclusive).

```python
import random

# Random number between 1 and 10 (inclusive)
number = random.randint(1, 10)
print(number)       # Could be 1, 2, 3, ..., 10

# Simulating a dice roll
dice = random.randint(1, 6)
print("You rolled:", dice)

# Random year
year = random.randint(1900, 2024)
print("Random year:", year)
```

#### 2. `random.randrange(start, stop, step)` - Random from Range
Returns a random number from a range (similar to `range()`).

```python
import random

# Random number from 0 to 9 (stop is exclusive)
number = random.randrange(10)
print(number)       # 0, 1, 2, ..., 9

# Random number from 1 to 10 (exclusive)
number = random.randrange(1, 11)
print(number)       # 1, 2, 3, ..., 10

# Random even number between 0 and 20
even = random.randrange(0, 21, 2)
print(even)         # 0, 2, 4, 6, ..., 20

# Random odd number between 1 and 19
odd = random.randrange(1, 20, 2)
print(odd)          # 1, 3, 5, 7, ..., 19
```

**Difference between `randint` and `randrange`:**
```python
import random

# randint: both endpoints INCLUSIVE
random.randint(1, 10)       # Can give 1, 2, 3, ..., 10

# randrange: stop is EXCLUSIVE (like range)
random.randrange(1, 11)     # Can give 1, 2, 3, ..., 10
random.randrange(10)        # Can give 0, 1, 2, ..., 9
```

#### 3. `random.random()` - Random Float
Returns a random float between 0.0 and 1.0 (0.0 inclusive, 1.0 exclusive).

```python
import random

# Random decimal between 0 and 1
number = random.random()
print(number)       # e.g., 0.734523456

# Scale to different ranges
# Random float between 0 and 10
number = random.random() * 10
print(number)       # e.g., 7.23456

# Random float between 5 and 15
number = random.random() * 10 + 5
print(number)       # e.g., 12.6789

# Random percentage
percentage = random.random() * 100
print(f"{percentage:.2f}%")     # e.g., 73.45%
```

---

### Other Useful `random` Functions

#### 4. `random.choice()` - Random Element from Sequence
```python
import random

# Random choice from list
colors = ["red", "green", "blue", "yellow"]
color = random.choice(colors)
print(color)        # e.g., "green"

# Random letter
letter = random.choice("ABCDEFG")
print(letter)       # e.g., "D"

# Random word
words = ["hello", "world", "python", "programming"]
word = random.choice(words)
print(word)
```

#### 5. `random.shuffle()` - Shuffle List
```python
import random

# Shuffle a list in place
cards = ["A", "K", "Q", "J", "10"]
random.shuffle(cards)
print(cards)        # e.g., ['Q', '10', 'A', 'J', 'K']

# Shuffle again
random.shuffle(cards)
print(cards)        # Different order
```

#### 6. `random.sample()` - Random Sample
```python
import random

# Select multiple random elements
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
sample = random.sample(numbers, 3)
print(sample)       # e.g., [7, 2, 9]

# Random lottery numbers
lottery = random.sample(range(1, 50), 6)
print(lottery)      # e.g., [23, 7, 42, 15, 31, 8]
```

---

### Practical Examples with `random`

#### Example 1: Dice Rolling Game
```python
import random

print("Rolling two dice...")
dice1 = random.randint(1, 6)
dice2 = random.randint(1, 6)

print(f"Dice 1: {dice1}")
print(f"Dice 2: {dice2}")
print(f"Total: {dice1 + dice2}")

if dice1 == dice2:
    print("Doubles!")
```

#### Example 2: Random Password Generator
```python
import random

# Character sets
lowercase = "abcdefghijklmnopqrstuvwxyz"
uppercase = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
digits = "0123456789"
special = "!@#$%^&*"

# Combine all characters
all_chars = lowercase + uppercase + digits + special

# Generate random password
password = ""
for i in range(8):
    password += random.choice(all_chars)

print("Random Password:", password)
```

#### Example 3: Guess the Number Game
```python
import random

# Computer picks random number
secret = random.randint(1, 100)
print("I'm thinking of a number between 1 and 100")

# User guesses
guess = int(input("Your guess: "))

if guess == secret:
    print("Correct!")
elif guess < secret:
    print("Too low!")
else:
    print("Too high!")

print(f"The number was {secret}")
```

#### Example 4: Random Quiz Question
```python
import random

# List of questions
questions = [
    "What is the capital of France?",
    "What is 2 + 2?",
    "What color is the sky?",
    "What is Python?"
]

# Select random question
question = random.choice(questions)
print("Random Question:", question)
```

---

### Import Best Practices

#### 1. Import at the Top
Always place import statements at the top of your file.

```python
# Good
import random
import math

name = "Alice"
number = random.randint(1, 10)

# Avoid
name = "Alice"
import random  # Don't import in the middle
```

#### 2. Use Specific Imports When Possible
```python
# Good - clear what you're using
from random import randint, choice

number = randint(1, 10)
color = choice(["red", "blue"])

# Okay - when you need many functions
import random

number = random.randint(1, 10)
color = random.choice(["red", "blue"])
```

#### 3. Avoid `import *`
```python
# Bad - unclear where functions come from
from random import *
number = randint(1, 10)

# Good - clear module source
import random
number = random.randint(1, 10)
```

#### 4. Use Standard Aliases
```python
# Common conventions
import numpy as np              # Not import numpy as n
import pandas as pd             # Not import pandas as p
import matplotlib.pyplot as plt # Standard alias
```

---

### Common Built-in Modules

Here are some commonly used Python modules:

| Module | Purpose | Example |
|--------|---------|---------|
| `math` | Mathematical functions | `math.sqrt(16)` |
| `random` | Random numbers | `random.randint(1, 10)` |
| `datetime` | Date and time | `datetime.datetime.now()` |
| `os` | Operating system | `os.getcwd()` |
| `sys` | System-specific | `sys.version` |
| `json` | JSON data | `json.loads('{"key":"value"}')` |
| `re` | Regular expressions | `re.match(pattern, string)` |
| `time` | Time functions | `time.sleep(1)` |

---

## Week 2 Summary

### Key Concepts Learned:

**Variables:**
- Dynamic vs static typing
- Multiple assignment methods (tuple unpacking, swapping)
- Shorthand operators (+=, -=, *=, etc.)
- Escape characters and quote types

**String Methods:**
- Case conversion (lower, upper, title, capitalize, swapcase)
- Character checking (isdigit, isalpha, isalnum)
- Whitespace removal (strip, lstrip, rstrip)
- Search methods (startswith, endswith, count, index, find)
- Modification (replace)
- Remember: strings are immutable!

**Control Flow:**
- if, elif, else statements
- Nested if statements
- Logical operators in conditions
- match-case statement (Python 3.10+)
- Ternary operator

**Imports:**
- Different import methods
- Using aliases
- The random library (randint, randrange, random)
- Best practices for imports

### Practice Tips:

1. **Experiment with string methods** - try chaining them together
2. **Practice control flow** - write programs with multiple conditions
3. **Use random module** - create simple games
4. **Read error messages** - they help you understand what went wrong
5. **Test edge cases** - what happens with empty strings, zero, negative numbers?

### Next Steps:

Now that you understand control flow and imports, you're ready to write more complex programs! In the upcoming weeks, you'll learn about loops, functions, and data structures that will allow you to create even more powerful applications.

Happy coding! 🐍
