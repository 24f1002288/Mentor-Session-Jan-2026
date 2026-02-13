# Week 1: Python Fundamentals

## Table of Contents
1. [Variables and Data Types](#variables-and-data-types)
2. [Type Conversion](#type-conversion)
3. [Print Statement](#print-statement)
4. [Input Function](#input-function)
5. [Statement vs Expression](#statement-vs-expression)
6. [Operators](#operators)
7. [Lists (Basic)](#lists-basic)
8. [Strings](#strings)

---

## Variables and Data Types

### What are Variables?
Variables are containers for storing data values. In Python, you don't need to declare a variable's type explicitly - Python infers it automatically.

### Creating Variables
```python
name = "Alice"          # String
age = 25                # Integer
height = 5.6            # Float
is_student = True       # Boolean
```

### Basic Data Types

#### 1. **Integer (int)**
Whole numbers, positive or negative, without decimals.
```python
x = 10
y = -5
z = 0
```

#### 2. **Float (float)**
Numbers with decimal points.
```python
pi = 3.14159
temperature = -2.5
price = 99.99
```

#### 3. **String (str)**
Text data enclosed in single, double, or triple quotes.
```python
name = "John"
message = 'Hello World'
paragraph = """This is a
multi-line string"""
```

#### 4. **Boolean (bool)**
Represents True or False values.
```python
is_active = True
has_permission = False
```

### The type() Function
The `type()` function returns the data type of a variable or value.

```python
x = 42
print(type(x))          # <class 'int'>

y = 3.14
print(type(y))          # <class 'float'>

name = "Python"
print(type(name))       # <class 'str'>

flag = True
print(type(flag))       # <class 'bool'>
```

### Variable Naming Rules
- Must start with a letter or underscore (_)
- Can contain letters, numbers, and underscores
- Case-sensitive (age, Age, and AGE are different)
- Cannot use Python keywords (if, for, while, etc.)

```python
# Valid variable names
student_name = "Alice"
_age = 25
score1 = 95

# Invalid variable names
# 1student = "Bob"      # Cannot start with number
# my-variable = 10      # Cannot use hyphens
# class = "Python"      # Cannot use keywords
```

---

## Type Conversion

Type conversion (also called type casting) is the process of converting one data type to another.

### Implicit Type Conversion
Python automatically converts one data type to another when needed.

```python
x = 10      # int
y = 3.5     # float
z = x + y   # z becomes float (13.5)
print(type(z))  # <class 'float'>
```

### Explicit Type Conversion
You manually convert data types using built-in functions.

#### 1. **int() - Convert to Integer**
```python
# Float to int (decimal part is removed, not rounded)
x = int(3.9)        # 3
y = int(3.1)        # 3

# String to int
age = int("25")     # 25

# Boolean to int
flag = int(True)    # 1
flag2 = int(False)  # 0

# Note: This will cause an error
# num = int("3.14")  # ValueError - cannot convert string with decimal
```

#### 2. **float() - Convert to Float**
```python
# Int to float
x = float(10)           # 10.0

# String to float
price = float("19.99")  # 19.99

# Boolean to float
val = float(True)       # 1.0
```

#### 3. **str() - Convert to String**
```python
# Int to string
age = str(25)           # "25"

# Float to string
pi = str(3.14)          # "3.14"

# Boolean to string
flag = str(True)        # "True"
```

#### 4. **bool() - Convert to Boolean**
```python
# Non-zero numbers are True, zero is False
print(bool(1))          # True
print(bool(0))          # False
print(bool(-5))         # True

# Non-empty strings are True, empty string is False
print(bool("Hello"))    # True
print(bool(""))         # False

# Other examples
print(bool(3.14))       # True
print(bool(0.0))        # False
```

---

## Print Statement

The `print()` function outputs data to the console.

### Basic Usage
```python
print("Hello, World!")
print(42)
print(3.14)
```

### Printing Multiple Values
```python
name = "Alice"
age = 25
print("Name:", name, "Age:", age)
# Output: Name: Alice Age: 25
```

### The `sep` Parameter
The `sep` parameter specifies how to separate multiple values. Default is a space.

```python
# Default separator (space)
print("Python", "is", "fun")
# Output: Python is fun

# Custom separator
print("Python", "is", "fun", sep="-")
# Output: Python-is-fun

print("2024", "01", "15", sep="/")
# Output: 2024/01/15

print("A", "B", "C", sep="")
# Output: ABC
```

### The `end` Parameter
The `end` parameter specifies what to print at the end. Default is a newline (`\n`).

```python
# Default end (newline)
print("Hello")
print("World")
# Output:
# Hello
# World

# Custom end
print("Hello", end=" ")
print("World")
# Output: Hello World

print("Loading", end="...")
print("Done!")
# Output: Loading...Done!

# Printing on same line
for i in range(5):
    print(i, end=" ")
# Output: 0 1 2 3 4
```

### Combining `sep` and `end`
```python
print("A", "B", "C", sep="-", end=" | ")
print("X", "Y", "Z", sep="+")
# Output: A-B-C | X+Y+Z
```

---

## Input Function

The `input()` function allows you to get user input from the console. It always returns a **string**.

### Basic Usage
```python
name = input("Enter your name: ")
print("Hello,", name)
```

### Important: Input Always Returns a String
```python
age = input("Enter your age: ")
print(type(age))  # <class 'str'>
```

### Converting Input to Other Types
```python
# Get integer input
age = int(input("Enter your age: "))
print(type(age))  # <class 'int'>

# Get float input
height = float(input("Enter your height in meters: "))
print(type(height))  # <class 'float'>

# Example calculation
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
sum = num1 + num2
print("Sum:", sum)
```

### Input Without Prompt
```python
# You can call input() without a prompt message
data = input()  # User types and presses Enter
```

---

## Statement vs Expression

### Expression
An expression is a combination of values, variables, and operators that evaluates to a single value.

```python
# Examples of expressions
5 + 3                    # Evaluates to 8
x * 2                    # Evaluates to a value
"Hello" + " World"       # Evaluates to "Hello World"
10 > 5                   # Evaluates to True
age >= 18 and age < 65   # Evaluates to True or False
```

**Key Point:** Expressions have a value that can be used or assigned.

```python
result = 5 + 3           # 5 + 3 is an expression
x = (10 * 2) + 5        # (10 * 2) + 5 is an expression
```

### Statement
A statement is a complete line of code that performs an action. It doesn't necessarily evaluate to a value.

```python
# Examples of statements
x = 10                   # Assignment statement
print("Hello")           # Function call statement
if x > 5:                # Conditional statement
    print("Greater")
```

**Key Point:** Statements do something, but don't have a value themselves.

### Key Differences

| Expression | Statement |
|------------|-----------|
| Evaluates to a value | Performs an action |
| Can be part of a statement | Cannot be part of an expression |
| Example: `3 + 5` | Example: `x = 3 + 5` |
| Example: `x > 10` | Example: `print(x)` |

### Examples
```python
# Expression inside a statement
x = 5 + 3        # "5 + 3" is expression, whole line is assignment statement

# Multiple expressions in one statement
y = (10 * 2) + (5 - 3)  # Two expressions combined

# Expression as part of print statement
print(10 + 5)    # "10 + 5" is expression, print() is statement

# You can't assign a statement
# x = (y = 10)   # This causes an error in Python
```

---

## Operators

Operators are special symbols that perform operations on operands (values or variables).

### Operands and Operators
```python
result = 10 + 5
#        ↑   ↑  ↑
#     operand operator operand
```

### Types of Operators

## 1. Arithmetic Operators

Used for mathematical calculations.

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `10 - 4` | `6` |
| `*` | Multiplication | `4 * 3` | `12` |
| `/` | Division | `15 / 4` | `3.75` |
| `//` | Floor Division | `15 // 4` | `3` |
| `%` | Modulus (Remainder) | `15 % 4` | `3` |
| `**` | Exponentiation | `2 ** 3` | `8` |

```python
# Examples
a = 10
b = 3

print(a + b)    # 13
print(a - b)    # 7
print(a * b)    # 30
print(a / b)    # 3.333...
print(a // b)   # 3 (integer division)
print(a % b)    # 1 (remainder)
print(a ** b)   # 1000 (10^3)
```

### Different Behaviors Based on Operand Types

#### Addition (+)
```python
# Numbers
print(5 + 3)              # 8 (arithmetic addition)

# Strings
print("Hello" + "World")  # "HelloWorld" (concatenation)

# Mixed types cause error
# print("5" + 3)          # TypeError
print("5" + str(3))       # "53" (concatenation)
```

#### Multiplication (*)
```python
# Numbers
print(5 * 3)              # 15 (arithmetic multiplication)

# String and number
print("Ha" * 3)           # "HaHaHa" (repetition)
print(3 * "Ha")           # "HaHaHa" (repetition)
```

## 2. Relational (Comparison) Operators

Used to compare two values. Always return a Boolean (True or False).

| Operator | Name | Example | Result |
|----------|------|---------|--------|
| `==` | Equal to | `5 == 5` | `True` |
| `!=` | Not equal to | `5 != 3` | `True` |
| `>` | Greater than | `5 > 3` | `True` |
| `<` | Less than | `5 < 3` | `False` |
| `>=` | Greater than or equal | `5 >= 5` | `True` |
| `<=` | Less than or equal | `3 <= 5` | `True` |

```python
x = 10
y = 20

print(x == y)   # False
print(x != y)   # True
print(x > y)    # False
print(x < y)    # True
print(x >= 10)  # True
print(y <= 15)  # False
```

### Comparison with Different Types
```python
# Strings (lexicographic comparison)
print("apple" < "banana")   # True
print("apple" == "Apple")   # False (case-sensitive)

# Numbers
print(5 == 5.0)             # True (value comparison)
print(5 is 5.0)             # False (identity comparison)
```

## 3. Logical Operators

Used to combine conditional statements.

| Operator | Description | Example |
|----------|-------------|---------|
| `and` | True if both operands are True | `True and False` → `False` |
| `or` | True if at least one operand is True | `True or False` → `True` |
| `not` | Reverses the boolean value | `not True` → `False` |

### Truth Tables

**AND Operator:**
| A | B | A and B |
|---|---|---------|
| True | True | True |
| True | False | False |
| False | True | False |
| False | False | False |

**OR Operator:**
| A | B | A or B |
|---|---|--------|
| True | True | True |
| True | False | True |
| False | True | True |
| False | False | False |

**NOT Operator:**
| A | not A |
|---|-------|
| True | False |
| False | True |

```python
# Examples
x = 10
y = 20
z = 30

# AND
print(x < y and y < z)      # True and True → True
print(x > y and y < z)      # False and True → False

# OR
print(x > y or y < z)       # False or True → True
print(x > y or y > z)       # False or False → False

# NOT
print(not (x > y))          # not False → True
print(not (x < y))          # not True → False

# Complex conditions
age = 25
has_license = True
print(age >= 18 and has_license)  # True
```

### Operator Precedence

Operator precedence determines the order in which operations are performed.

**Precedence (High to Low):**
1. `**` (Exponentiation)
2. `*`, `/`, `//`, `%` (Multiplication, Division)
3. `+`, `-` (Addition, Subtraction)
4. `<`, `<=`, `>`, `>=`, `==`, `!=` (Comparison)
5. `not` (Logical NOT)
6. `and` (Logical AND)
7. `or` (Logical OR)

```python
# Examples
result = 2 + 3 * 4          # Multiplication first: 2 + 12 = 14
print(result)               # 14

result = (2 + 3) * 4        # Parentheses first: 5 * 4 = 20
print(result)               # 20

result = 10 - 2 ** 3        # Exponent first: 10 - 8 = 2
print(result)               # 2

result = 5 > 3 and 10 < 20  # Comparison first, then AND
print(result)               # True

# Complex example
result = 2 + 3 * 4 > 10 and not False or 5 < 3
# Step 1: 3 * 4 = 12
# Step 2: 2 + 12 = 14
# Step 3: 14 > 10 = True
# Step 4: not False = True
# Step 5: 5 < 3 = False
# Step 6: True and True = True
# Step 7: True or False = True
print(result)               # True
```

**Best Practice:** Use parentheses to make your code clearer, even when not strictly necessary.

```python
# Less clear
result = x > 5 and y < 10 or z == 20

# More clear
result = ((x > 5) and (y < 10)) or (z == 20)
```

---

## Lists (Basic)

A list is an ordered, mutable collection of items. Lists can contain items of different types.

### Creating Lists
```python
# Empty list
empty_list = []

# List with integers
numbers = [1, 2, 3, 4, 5]

# List with strings
fruits = ["apple", "banana", "cherry"]

# Mixed types
mixed = [1, "hello", 3.14, True]

# Nested lists
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

### Basic Indexing

Python uses **zero-based indexing** - the first element is at index 0.

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]
#         0        1         2         3       4
```

#### Positive Indexing
```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]

print(fruits[0])    # "apple"
print(fruits[1])    # "banana"
print(fruits[2])    # "cherry"
print(fruits[4])    # "elderberry"
```

#### Negative Indexing
Negative indices count from the end of the list.

```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]
#         -5       -4        -3        -2      -1

print(fruits[-1])   # "elderberry" (last item)
print(fruits[-2])   # "date" (second to last)
print(fruits[-5])   # "apple" (first item)
```

#### Modifying List Elements
```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "blueberry"
print(fruits)  # ["apple", "blueberry", "cherry"]
```

#### Getting List Length
```python
fruits = ["apple", "banana", "cherry"]
print(len(fruits))  # 3
```

#### Index Errors
```python
fruits = ["apple", "banana", "cherry"]
# print(fruits[10])  # IndexError: list index out of range
```

#### Basic List Operations
```python
# Concatenation
list1 = [1, 2, 3]
list2 = [4, 5, 6]
combined = list1 + list2
print(combined)  # [1, 2, 3, 4, 5, 6]

# Repetition
numbers = [1, 2]
repeated = numbers * 3
print(repeated)  # [1, 2, 1, 2, 1, 2]

# Checking membership
fruits = ["apple", "banana", "cherry"]
print("apple" in fruits)      # True
print("grape" in fruits)      # False
print("grape" not in fruits)  # True
```

---

## Strings

Strings are sequences of characters enclosed in quotes. They are **immutable** (cannot be changed after creation).

### Creating Strings
```python
# Single quotes
name = 'Alice'

# Double quotes
message = "Hello, World!"

# Triple quotes (for multi-line strings)
paragraph = """This is a
multi-line
string"""

# Empty string
empty = ""
```

### String Concatenation

Joining strings together using the `+` operator.

```python
first_name = "John"
last_name = "Doe"

# Concatenation
full_name = first_name + " " + last_name
print(full_name)  # "John Doe"

# Multiple concatenations
greeting = "Hello" + ", " + "World" + "!"
print(greeting)  # "Hello, World!"

# Concatenation with variables and literals
age = 25
# message = "Age: " + age  # TypeError - cannot concatenate str and int
message = "Age: " + str(age)
print(message)  # "Age: 25"
```

### String Indexing

Strings are indexed just like lists, starting from 0.

```python
text = "Python"
#       012345
#      -6-5-4-3-2-1

# Positive indexing
print(text[0])   # "P"
print(text[1])   # "y"
print(text[5])   # "n"

# Negative indexing
print(text[-1])  # "n" (last character)
print(text[-2])  # "o"
print(text[-6])  # "P" (first character)

# Strings are immutable - this causes an error
# text[0] = "J"  # TypeError: 'str' object does not support item assignment
```

### String Slicing
```python
text = "Python Programming"

# Basic slicing [start:end]
print(text[0:6])    # "Python"
print(text[7:18])   # "Programming"

# Omitting start or end
print(text[:6])     # "Python" (from beginning)
print(text[7:])     # "Programming" (to end)
print(text[:])      # "Python Programming" (entire string)
```

### String Comparison

Strings are compared lexicographically (dictionary order) based on Unicode values.

```python
# Equality
print("hello" == "hello")     # True
print("hello" == "Hello")     # False (case-sensitive)

# Inequality
print("apple" != "orange")    # True

# Less than / Greater than
print("apple" < "banana")     # True (a comes before b)
print("zebra" > "apple")      # True (z comes after a)

# Comparison is case-sensitive
print("Apple" < "apple")      # True (uppercase letters have lower Unicode values)

# Comparing by length (using len)
word1 = "cat"
word2 = "elephant"
print(len(word1) < len(word2))  # True
```

**Lexicographic Comparison:**
- Compares character by character from left to right
- Uses Unicode values (A=65, a=97, etc.)
- Uppercase letters come before lowercase

```python
print("a" < "b")         # True
print("A" < "a")         # True (65 < 97)
print("abc" < "abd")     # True (third character differs)
print("apple" < "apply") # True (fifth character differs)
```

### Common String Methods

Methods are functions that belong to an object. String methods don't modify the original string (since strings are immutable) but return new strings.

#### 1. **Case Conversion Methods**
```python
text = "Hello World"

# Convert to uppercase
print(text.upper())       # "HELLO WORLD"

# Convert to lowercase
print(text.lower())       # "hello world"

# Convert to title case
print(text.title())       # "Hello World"

# Capitalize first letter only
print("hello world".capitalize())  # "Hello world"

# Swap case
print(text.swapcase())    # "hELLO wORLD"
```

#### 2. **Checking String Content**
```python
text = "Hello123"

# Check if all characters are alphabetic
print("Hello".isalpha())      # True
print("Hello123".isalpha())   # False

# Check if all characters are digits
print("12345".isdigit())      # True
print("123a".isdigit())       # False

# Check if all characters are alphanumeric
print("Hello123".isalnum())   # True
print("Hello 123".isalnum())  # False (space is not alphanumeric)

# Check if string is uppercase
print("HELLO".isupper())      # True
print("Hello".isupper())      # False

# Check if string is lowercase
print("hello".islower())      # True
print("Hello".islower())      # False
```

#### 3. **Trimming Whitespace**
```python
text = "   Hello World   "

# Remove leading and trailing whitespace
print(text.strip())       # "Hello World"

# Remove leading whitespace only
print(text.lstrip())      # "Hello World   "

# Remove trailing whitespace only
print(text.rstrip())      # "   Hello World"
```

#### 4. **Finding and Replacing**
```python
text = "Hello World, Hello Python"

# Find substring (returns index of first occurrence, -1 if not found)
print(text.find("World"))      # 6
print(text.find("Java"))       # -1

# Count occurrences
print(text.count("Hello"))     # 2
print(text.count("o"))         # 4

# Replace substring
print(text.replace("Hello", "Hi"))  # "Hi World, Hi Python"
```

#### 5. **Splitting and Joining**
```python
# Split string into list
sentence = "Python is awesome"
words = sentence.split()          # ["Python", "is", "awesome"]
print(words)

# Split by specific delimiter
data = "apple,banana,cherry"
fruits = data.split(",")          # ["apple", "banana", "cherry"]
print(fruits)

# Join list into string
words = ["Python", "is", "fun"]
sentence = " ".join(words)        # "Python is fun"
print(sentence)

separator = "-"
result = separator.join(["2024", "01", "15"])
print(result)                     # "2024-01-15"
```

#### 6. **Checking Start and End**
```python
filename = "document.pdf"

# Check if string starts with substring
print(filename.startswith("doc"))     # True
print(filename.startswith("image"))   # False

# Check if string ends with substring
print(filename.endswith(".pdf"))      # True
print(filename.endswith(".txt"))      # False
```

### String Length
```python
text = "Python Programming"
length = len(text)
print(length)  # 18
```

### String Repetition
```python
text = "Ha"
repeated = text * 3
print(repeated)  # "HaHaHa"
```

### Escape Sequences
Special characters that start with a backslash.

```python
# Newline
print("Hello\nWorld")
# Output:
# Hello
# World

# Tab
print("Name:\tJohn")
# Output: Name:    John

# Backslash
print("C:\\Users\\Documents")
# Output: C:\Users\Documents

# Quote inside string
print("She said, \"Hello!\"")
# Output: She said, "Hello!"
```
