# Week 5: Python Programming - Complete Notes

## Table of Contents
1. [Dictionaries](#dictionaries)
2. [More on Dictionaries](#more-on-dictionaries)
3. [Collections Summary](#collections-summary)
4. [Sorting using Functions](#sorting-using-functions)
5. [Matrix Multiplication](#matrix-multiplication)
6. [Scope of Variables](#scope-of-variables)
7. [Functions Tutorial](#functions-tutorial)
8. [Iterators and Generators](#iterators-and-generators)
9. [Lambda, Enumerate, Zip, Map, Filter](#lambda-enumerate-zip-map-filter)

---

## L5.1: Dictionaries

### What is a Dictionary?
A dictionary is a **mutable, unordered** collection of key-value pairs. Each key must be unique and immutable (strings, numbers, tuples), while values can be of any type.

**Syntax:**
```python
dictionary_name = {key1: value1, key2: value2, key3: value3}
```

### Creating Dictionaries

```python
# Empty dictionary
empty_dict = {}
empty_dict2 = dict()

# Dictionary with mixed data types
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A",
    "subjects": ["Math", "Physics", "Chemistry"]
}

# Dictionary with numeric keys
scores = {1: 95, 2: 87, 3: 92}

# Dictionary with tuple keys
coordinates = {
    (0, 0): "Origin",
    (1, 1): "Point A",
    (2, 3): "Point B"
}
```

### Accessing Dictionary Elements

```python
student = {"name": "Alice", "age": 20, "grade": "A"}

# Using square brackets
print(student["name"])        # Output: Alice
print(student["age"])         # Output: 20

# Using get() method (safer - doesn't raise error if key doesn't exist)
print(student.get("name"))    # Output: Alice
print(student.get("email"))   # Output: None
print(student.get("email", "Not provided"))  # Output: Not provided (default value)
```

**Difference between `[]` and `get()`:**
- `dictionary[key]` → Raises `KeyError` if key doesn't exist
- `dictionary.get(key)` → Returns `None` if key doesn't exist
- `dictionary.get(key, default)` → Returns default value if key doesn't exist

### Adding and Modifying Elements

```python
student = {"name": "Alice", "age": 20}

# Adding new key-value pair
student["grade"] = "A"
student["email"] = "alice@example.com"

# Modifying existing value
student["age"] = 21

print(student)
# Output: {'name': 'Alice', 'age': 21, 'grade': 'A', 'email': 'alice@example.com'}
```

### Removing Elements

```python
student = {"name": "Alice", "age": 20, "grade": "A", "email": "alice@example.com"}

# Using del keyword
del student["email"]

# Using pop() - removes and returns the value
grade = student.pop("grade")
print(grade)  # Output: A

# Using popitem() - removes and returns last inserted key-value pair (Python 3.7+)
item = student.popitem()
print(item)   # Output: ('age', 20)

# Using clear() - removes all items
student.clear()
print(student)  # Output: {}
```

### Dictionary Methods

```python
student = {"name": "Alice", "age": 20, "grade": "A"}

# keys() - returns all keys
print(student.keys())        # Output: dict_keys(['name', 'age', 'grade'])

# values() - returns all values
print(student.values())      # Output: dict_values(['Alice', 20, 'A'])

# items() - returns all key-value pairs as tuples
print(student.items())       # Output: dict_items([('name', 'Alice'), ('age', 20), ('grade', 'A')])

# copy() - creates a shallow copy
student_copy = student.copy()

# update() - updates dictionary with another dictionary
student.update({"email": "alice@example.com", "age": 21})
print(student)
# Output: {'name': 'Alice', 'age': 21, 'grade': 'A', 'email': 'alice@example.com'}
```

### Checking Key Existence

```python
student = {"name": "Alice", "age": 20, "grade": "A"}

# Using 'in' keyword
if "name" in student:
    print("Name exists")      # Output: Name exists

if "email" not in student:
    print("Email doesn't exist")  # Output: Email doesn't exist
```

### Iterating Through Dictionaries

```python
student = {"name": "Alice", "age": 20, "grade": "A"}

# Iterate through keys
for key in student:
    print(key)

# Iterate through values
for value in student.values():
    print(value)

# Iterate through key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")

# Output:
# name: Alice
# age: 20
# grade: A
```

### Nested Dictionaries

```python
# Dictionary of dictionaries
students = {
    "student1": {"name": "Alice", "age": 20, "grade": "A"},
    "student2": {"name": "Bob", "age": 22, "grade": "B"},
    "student3": {"name": "Charlie", "age": 21, "grade": "A"}
}

# Accessing nested dictionary
print(students["student1"]["name"])  # Output: Alice

# Iterating through nested dictionary
for student_id, details in students.items():
    print(f"{student_id}:")
    for key, value in details.items():
        print(f"  {key}: {value}")
```

### Dictionary Comprehension

```python
# Creating dictionary using comprehension
squares = {x: x**2 for x in range(1, 6)}
print(squares)  # Output: {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# With condition
even_squares = {x: x**2 for x in range(1, 11) if x % 2 == 0}
print(even_squares)  # Output: {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}

# From two lists
keys = ["name", "age", "grade"]
values = ["Alice", 20, "A"]
student = {k: v for k, v in zip(keys, values)}
print(student)  # Output: {'name': 'Alice', 'age': 20, 'grade': 'A'}
```

---

## L5.2: More on Dictionaries

### Advanced Dictionary Operations

#### 1. **setdefault() Method**
Returns the value of a key if it exists; if not, inserts the key with a default value.

```python
student = {"name": "Alice", "age": 20}

# Key exists
name = student.setdefault("name", "Unknown")
print(name)  # Output: Alice

# Key doesn't exist
email = student.setdefault("email", "not@provided.com")
print(email)  # Output: not@provided.com
print(student)  # Output: {'name': 'Alice', 'age': 20, 'email': 'not@provided.com'}
```

#### 2. **fromkeys() Method**
Creates a new dictionary with specified keys and a common value.

```python
# Create dictionary with default value
keys = ["name", "age", "grade"]
student = dict.fromkeys(keys, "Unknown")
print(student)  # Output: {'name': 'Unknown', 'age': 'Unknown', 'grade': 'Unknown'}

# With None as default
keys = ["a", "b", "c"]
new_dict = dict.fromkeys(keys)
print(new_dict)  # Output: {'a': None, 'b': None, 'c': None}
```

#### 3. **Merging Dictionaries**

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}
dict3 = {"b": 5, "e": 6}

# Method 1: Using update()
result = dict1.copy()
result.update(dict2)
print(result)  # Output: {'a': 1, 'b': 2, 'c': 3, 'd': 4}

# Method 2: Using ** unpacking (Python 3.5+)
merged = {**dict1, **dict2, **dict3}
print(merged)  # Output: {'a': 1, 'b': 5, 'c': 3, 'd': 4, 'e': 6}

# Method 3: Using | operator (Python 3.9+)
merged = dict1 | dict2 | dict3
print(merged)  # Output: {'a': 1, 'b': 5, 'c': 3, 'd': 4, 'e': 6}
```

#### 4. **Sorting Dictionaries**

```python
student_scores = {"Alice": 85, "Bob": 92, "Charlie": 78, "Diana": 95}

# Sort by keys
sorted_by_keys = dict(sorted(student_scores.items()))
print(sorted_by_keys)
# Output: {'Alice': 85, 'Bob': 92, 'Charlie': 78, 'Diana': 95}

# Sort by values
sorted_by_values = dict(sorted(student_scores.items(), key=lambda item: item[1]))
print(sorted_by_values)
# Output: {'Charlie': 78, 'Alice': 85, 'Bob': 92, 'Diana': 95}

# Sort by values (descending)
sorted_desc = dict(sorted(student_scores.items(), key=lambda item: item[1], reverse=True))
print(sorted_desc)
# Output: {'Diana': 95, 'Bob': 92, 'Alice': 85, 'Charlie': 78}
```

#### 5. **Inverting a Dictionary**

```python
# Original dictionary
original = {"a": 1, "b": 2, "c": 3}

# Invert keys and values
inverted = {v: k for k, v in original.items()}
print(inverted)  # Output: {1: 'a', 2: 'b', 3: 'c'}

# Warning: If values are not unique, some keys will be lost
original = {"a": 1, "b": 2, "c": 1}
inverted = {v: k for k, v in original.items()}
print(inverted)  # Output: {1: 'c', 2: 'b'} - 'a' is lost!
```

#### 6. **Filtering Dictionaries**

```python
student_scores = {"Alice": 85, "Bob": 92, "Charlie": 78, "Diana": 95, "Eve": 88}

# Filter students with score > 85
high_scorers = {k: v for k, v in student_scores.items() if v > 85}
print(high_scorers)  # Output: {'Bob': 92, 'Diana': 95, 'Eve': 88}

# Filter by key (names starting with 'A')
a_students = {k: v for k, v in student_scores.items() if k.startswith('A')}
print(a_students)  # Output: {'Alice': 85}
```

#### 7. **Dictionary with Default Values (defaultdict)**

```python
from collections import defaultdict

# Regular dictionary - KeyError
regular_dict = {}
# regular_dict["key"] += 1  # This would raise KeyError

# defaultdict with int (default value 0)
count_dict = defaultdict(int)
count_dict["a"] += 1
count_dict["b"] += 2
print(count_dict)  # Output: defaultdict(<class 'int'>, {'a': 1, 'b': 2})

# defaultdict with list
list_dict = defaultdict(list)
list_dict["fruits"].append("apple")
list_dict["fruits"].append("banana")
list_dict["vegetables"].append("carrot")
print(list_dict)
# Output: defaultdict(<class 'list'>, {'fruits': ['apple', 'banana'], 'vegetables': ['carrot']})
```

#### 8. **Counting with Dictionaries**

```python
# Count character occurrences
text = "hello world"
char_count = {}

for char in text:
    if char in char_count:
        char_count[char] += 1
    else:
        char_count[char] = 1

print(char_count)
# Output: {'h': 1, 'e': 1, 'l': 3, 'o': 2, ' ': 1, 'w': 1, 'r': 1, 'd': 1}

# Using get() method (cleaner)
char_count = {}
for char in text:
    char_count[char] = char_count.get(char, 0) + 1

# Using Counter (easiest)
from collections import Counter
char_count = Counter(text)
print(char_count)
# Output: Counter({'l': 3, 'o': 2, 'h': 1, 'e': 1, ' ': 1, 'w': 1, 'r': 1, 'd': 1})
```

---

## L5.3: Collections Summary

### Overview of Python Collections

| Collection | Ordered | Mutable | Duplicates | Syntax |
|------------|---------|---------|------------|--------|
| **List** | ✓ | ✓ | ✓ | `[1, 2, 3]` |
| **Tuple** | ✓ | ✗ | ✓ | `(1, 2, 3)` |
| **Set** | ✗ | ✓ | ✗ | `{1, 2, 3}` |
| **Dictionary** | ✓ (3.7+) | ✓ | Keys: ✗, Values: ✓ | `{"a": 1}` |

### 1. Lists

```python
# Creation
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]

# Common operations
fruits.append("orange")           # Add to end
fruits.insert(1, "mango")         # Insert at index
fruits.remove("banana")           # Remove by value
popped = fruits.pop()             # Remove and return last
fruits.sort()                     # Sort in place
fruits.reverse()                  # Reverse in place
length = len(fruits)              # Get length

# Slicing
print(fruits[1:3])                # Elements at index 1 and 2
print(fruits[:2])                 # First two elements
print(fruits[-2:])                # Last two elements

# List comprehension
squares = [x**2 for x in range(1, 6)]
evens = [x for x in range(1, 11) if x % 2 == 0]
```

**When to use Lists:**
- When you need an ordered collection
- When you need to modify elements
- When duplicates are allowed
- For sequences that will change size

### 2. Tuples

```python
# Creation
coordinates = (10, 20)
single_element = (5,)  # Note the comma!
colors = ("red", "green", "blue")

# Common operations
print(coordinates[0])             # Access by index
print(len(colors))                # Get length
print(colors.count("red"))        # Count occurrences
print(colors.index("green"))      # Find index

# Unpacking
x, y = coordinates
r, g, b = colors

# Tuples are immutable
# coordinates[0] = 15  # This raises TypeError
```

**When to use Tuples:**
- When you need an immutable sequence
- For data that shouldn't change (coordinates, RGB values)
- As dictionary keys (tuples can be keys, lists cannot)
- For function return values with multiple items
- Slightly faster than lists

### 3. Sets

```python
# Creation
numbers = {1, 2, 3, 4, 5}
empty_set = set()  # Note: {} creates an empty dictionary, not set!
from_list = set([1, 2, 2, 3, 3, 3])  # Duplicates removed: {1, 2, 3}

# Common operations
numbers.add(6)                    # Add element
numbers.remove(2)                 # Remove element (raises error if not found)
numbers.discard(10)               # Remove if exists (no error)
popped = numbers.pop()            # Remove and return arbitrary element
numbers.clear()                   # Remove all elements

# Set operations
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

union = set1 | set2               # {1, 2, 3, 4, 5, 6}
intersection = set1 & set2        # {3, 4}
difference = set1 - set2          # {1, 2}
symmetric_diff = set1 ^ set2      # {1, 2, 5, 6}

# Set comprehension
even_squares = {x**2 for x in range(1, 11) if x % 2 == 0}
```

**When to use Sets:**
- When you need unique elements only
- For membership testing (very fast: O(1))
- For mathematical set operations (union, intersection)
- When order doesn't matter
- For removing duplicates from a list

### 4. Dictionaries (Covered in detail above)

```python
# Quick recap
student = {
    "name": "Alice",
    "age": 20,
    "grades": [85, 90, 92]
}

# Access
print(student["name"])
print(student.get("email", "Not provided"))

# Modify
student["age"] = 21
student["email"] = "alice@example.com"

# Iterate
for key, value in student.items():
    print(f"{key}: {value}")
```

**When to use Dictionaries:**
- When you need key-value associations
- For fast lookups by key (O(1))
- When data has named fields
- For counting or grouping data

### Choosing the Right Collection

```python
# Use LIST when:
shopping_list = ["milk", "eggs", "bread", "milk"]  # Order matters, duplicates OK

# Use TUPLE when:
rgb_color = (255, 128, 0)  # Immutable, fixed size, represents single entity

# Use SET when:
unique_visitors = {"user1", "user2", "user3"}  # Only unique values needed

# Use DICTIONARY when:
user_profile = {"name": "Alice", "age": 25, "city": "NYC"}  # Key-value pairs
```

## L5.4: Sorting using Functions

### Basic Sorting

#### 1. **sorted() Function**
Returns a new sorted list, leaving the original unchanged.

```python
# Sorting lists
numbers = [5, 2, 8, 1, 9]
sorted_numbers = sorted(numbers)
print(sorted_numbers)  # [1, 2, 5, 8, 9]
print(numbers)         # [5, 2, 8, 1, 9] - original unchanged

# Reverse order
sorted_desc = sorted(numbers, reverse=True)
print(sorted_desc)     # [9, 8, 5, 2, 1]

# Sorting strings
words = ["banana", "apple", "cherry"]
sorted_words = sorted(words)
print(sorted_words)    # ['apple', 'banana', 'cherry']

# Sorting tuples
tuples = [(1, 2), (3, 1), (2, 4)]
sorted_tuples = sorted(tuples)
print(sorted_tuples)   # [(1, 2), (2, 4), (3, 1)] - sorts by first element
```

#### 2. **list.sort() Method**
Sorts the list in-place, modifying the original.

```python
numbers = [5, 2, 8, 1, 9]
numbers.sort()
print(numbers)         # [1, 2, 5, 8, 9] - original modified

# Reverse order
numbers.sort(reverse=True)
print(numbers)         # [9, 8, 5, 2, 1]
```

**Difference: sorted() vs sort()**
- `sorted()` - Returns new list, works on any iterable
- `sort()` - Modifies list in-place, only for lists
- `sorted()` - Can be used on tuples, sets, dictionaries
- `sort()` - Only for lists, returns None

### Sorting with key Parameter

The `key` parameter accepts a function that defines custom sorting logic.

#### 1. **Sorting by String Length**

```python
words = ["python", "is", "awesome", "fun"]

# Sort by length
sorted_by_length = sorted(words, key=len)
print(sorted_by_length)  # ['is', 'fun', 'python', 'awesome']

# Sort by length (descending)
sorted_by_length_desc = sorted(words, key=len, reverse=True)
print(sorted_by_length_desc)  # ['awesome', 'python', 'fun', 'is']
```

#### 2. **Sorting Case-Insensitive**

```python
words = ["banana", "Apple", "cherry", "Date"]

# Default sorting (case-sensitive)
print(sorted(words))
# ['Apple', 'Date', 'banana', 'cherry'] - uppercase comes first

# Case-insensitive sorting
sorted_case_insensitive = sorted(words, key=str.lower)
print(sorted_case_insensitive)
# ['Apple', 'banana', 'cherry', 'Date']
```

#### 3. **Sorting by Absolute Value**

```python
numbers = [-5, 2, -8, 1, -9, 3]

# Sort by absolute value
sorted_by_abs = sorted(numbers, key=abs)
print(sorted_by_abs)  # [1, 2, 3, -5, -8, -9]
```

#### 4. **Sorting Lists of Tuples/Lists**

```python
# List of tuples (name, age, grade)
students = [
    ("Alice", 20, 85),
    ("Bob", 22, 92),
    ("Charlie", 21, 78),
    ("Diana", 20, 95)
]

# Sort by age (index 1)
sorted_by_age = sorted(students, key=lambda x: x[1])
print(sorted_by_age)
# [('Alice', 20, 85), ('Diana', 20, 95), ('Charlie', 21, 78), ('Bob', 22, 92)]

# Sort by grade (index 2)
sorted_by_grade = sorted(students, key=lambda x: x[2])
print(sorted_by_grade)
# [('Charlie', 21, 78), ('Alice', 20, 85), ('Bob', 22, 92), ('Diana', 20, 95)]

# Sort by grade (descending)
sorted_by_grade_desc = sorted(students, key=lambda x: x[2], reverse=True)
print(sorted_by_grade_desc)
# [('Diana', 20, 95), ('Bob', 22, 92), ('Alice', 20, 85), ('Charlie', 21, 78)]
```

#### 5. **Sorting Dictionaries**

```python
students = {
    "Alice": 85,
    "Bob": 92,
    "Charlie": 78,
    "Diana": 95
}

# Sort by keys
sorted_by_keys = dict(sorted(students.items()))
print(sorted_by_keys)
# {'Alice': 85, 'Bob': 92, 'Charlie': 78, 'Diana': 95}

# Sort by values
sorted_by_values = dict(sorted(students.items(), key=lambda item: item[1]))
print(sorted_by_values)
# {'Charlie': 78, 'Alice': 85, 'Bob': 92, 'Diana': 95}

# Get top 3 students
top_3 = dict(sorted(students.items(), key=lambda item: item[1], reverse=True)[:3])
print(top_3)
# {'Diana': 95, 'Bob': 92, 'Alice': 85}
```

#### 6. **Sorting List of Dictionaries**

```python
students = [
    {"name": "Alice", "age": 20, "grade": 85},
    {"name": "Bob", "age": 22, "grade": 92},
    {"name": "Charlie", "age": 21, "grade": 78},
    {"name": "Diana", "age": 20, "grade": 95}
]

# Sort by name
sorted_by_name = sorted(students, key=lambda x: x["name"])
print(sorted_by_name)

# Sort by grade (descending)
sorted_by_grade = sorted(students, key=lambda x: x["grade"], reverse=True)
print(sorted_by_grade)
# [{'name': 'Diana', ...}, {'name': 'Bob', ...}, ...]

# Sort by multiple criteria: age first, then grade
sorted_multi = sorted(students, key=lambda x: (x["age"], x["grade"]))
print(sorted_multi)
```

#### 7. **Custom Sorting Functions**

```python
def sort_by_last_char(word):
    return word[-1]

words = ["banana", "apple", "cherry", "date"]
sorted_words = sorted(words, key=sort_by_last_char)
print(sorted_words)  # ['banana', 'apple', 'date', 'cherry']

# Complex custom sorting
def priority_sort(item):
    # Sort by priority: even numbers first, then odd
    if item % 2 == 0:
        return (0, item)  # (priority 0, value)
    else:
        return (1, item)  # (priority 1, value)

numbers = [5, 2, 8, 1, 9, 4]
sorted_numbers = sorted(numbers, key=priority_sort)
print(sorted_numbers)  # [2, 4, 8, 1, 5, 9]
```

### Stability in Sorting

Python's sort is **stable** - maintains the relative order of elements with equal keys.

```python
students = [
    ("Alice", 85),
    ("Bob", 92),
    ("Charlie", 85),
    ("Diana", 92)
]

# Sort by grade - students with same grade maintain their original order
sorted_students = sorted(students, key=lambda x: x[1])
print(sorted_students)
# [('Alice', 85), ('Charlie', 85), ('Bob', 92), ('Diana', 92)]
# Alice comes before Charlie (both 85), Bob before Diana (both 92)
```

---

## L5.5 & L5.6: Matrix Multiplication

### What is a Matrix?

A matrix is a 2D array of numbers arranged in rows and columns.

```python
# Matrix representation in Python (list of lists)
matrix_a = [
    [1, 2, 3],
    [4, 5, 6]
]  # 2x3 matrix (2 rows, 3 columns)

matrix_b = [
    [7, 8],
    [9, 10],
    [11, 12]
]  # 3x2 matrix
```

### Matrix Basics

#### 1. **Creating Matrices**

```python
# Method 1: Direct creation
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Method 2: Using list comprehension
rows, cols = 3, 4
matrix = [[0 for j in range(cols)] for i in range(rows)]
print(matrix)
# [[0, 0, 0, 0], [0, 0, 0, 0], [0, 0, 0, 0]]

# Method 3: Identity matrix
n = 3
identity = [[1 if i == j else 0 for j in range(n)] for i in range(n)]
print(identity)
# [[1, 0, 0], [0, 1, 0], [0, 0, 1]]
```

#### 2. **Accessing Matrix Elements**

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access element at row i, column j
element = matrix[1][2]  # Row 1, Column 2 → 6

# Get entire row
row_1 = matrix[1]  # [4, 5, 6]

# Get entire column (requires iteration)
col_1 = [row[1] for row in matrix]  # [2, 5, 8]
```

#### 3. **Matrix Dimensions**

```python
matrix = [[1, 2, 3], [4, 5, 6]]

rows = len(matrix)           # 2
cols = len(matrix[0])        # 3

print(f"Matrix dimensions: {rows}x{cols}")
```

### Matrix Operations

#### 1. **Matrix Addition**

Matrices must have the same dimensions.

```python
def matrix_addition(A, B):
    rows = len(A)
    cols = len(A[0])
    
    # Check if dimensions match
    if rows != len(B) or cols != len(B[0]):
        return "Matrices must have same dimensions"
    
    # Create result matrix
    result = [[0 for j in range(cols)] for i in range(rows)]
    
    # Add corresponding elements
    for i in range(rows):
        for j in range(cols):
            result[i][j] = A[i][j] + B[i][j]
    
    return result

# Example
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]

C = matrix_addition(A, B)
print(C)  # [[6, 8], [10, 12]]
```

#### 2. **Matrix Subtraction**

```python
def matrix_subtraction(A, B):
    rows = len(A)
    cols = len(A[0])
    
    if rows != len(B) or cols != len(B[0]):
        return "Matrices must have same dimensions"
    
    result = [[A[i][j] - B[i][j] for j in range(cols)] for i in range(rows)]
    return result

# Example
A = [[5, 6], [7, 8]]
B = [[1, 2], [3, 4]]

C = matrix_subtraction(A, B)
print(C)  # [[4, 4], [4, 4]]
```

#### 3. **Scalar Multiplication**

```python
def scalar_multiplication(matrix, scalar):
    rows = len(matrix)
    cols = len(matrix[0])
    
    result = [[matrix[i][j] * scalar for j in range(cols)] for i in range(rows)]
    return result

# Example
A = [[1, 2], [3, 4]]
scalar = 3

B = scalar_multiplication(A, scalar)
print(B)  # [[3, 6], [9, 12]]
```

#### 4. **Matrix Transpose**

Swap rows and columns.

```python
def transpose(matrix):
    rows = len(matrix)
    cols = len(matrix[0])
    
    # Create transposed matrix (cols x rows)
    result = [[matrix[i][j] for i in range(rows)] for j in range(cols)]
    return result

# Example
A = [
    [1, 2, 3],
    [4, 5, 6]
]

A_T = transpose(A)
print(A_T)
# [[1, 4], [2, 5], [3, 6]]
```

### Matrix Multiplication

**Rule:** To multiply A (m×n) by B (p×q), we need n = p.
The result will be an m×q matrix.

```
A(m×n) × B(n×q) = C(m×q)
```

**Formula:** 
```
C[i][j] = Σ(A[i][k] × B[k][j]) for k from 0 to n-1
```

#### Matrix Multiplication - Method 1 (Nested Loops)

```python
def matrix_multiply(A, B):
    # Get dimensions
    rows_A = len(A)
    cols_A = len(A[0])
    rows_B = len(B)
    cols_B = len(B[0])
    
    # Check if multiplication is possible
    if cols_A != rows_B:
        return f"Cannot multiply: A is {rows_A}x{cols_A}, B is {rows_B}x{cols_B}"
    
    # Create result matrix (rows_A × cols_B)
    result = [[0 for j in range(cols_B)] for i in range(rows_A)]
    
    # Perform multiplication
    for i in range(rows_A):
        for j in range(cols_B):
            for k in range(cols_A):
                result[i][j] += A[i][k] * B[k][j]
    
    return result

# Example
A = [
    [1, 2, 3],
    [4, 5, 6]
]  # 2x3

B = [
    [7, 8],
    [9, 10],
    [11, 12]
]  # 3x2

C = matrix_multiply(A, B)
print(C)
# [[58, 64], [139, 154]]

# Explanation for C[0][0]:
# C[0][0] = (1×7) + (2×9) + (3×11) = 7 + 18 + 33 = 58
```

#### Matrix Multiplication - Method 2 (List Comprehension)

```python
def matrix_multiply_compact(A, B):
    rows_A = len(A)
    cols_A = len(A[0])
    cols_B = len(B[0])
    
    if cols_A != len(B):
        return "Cannot multiply"
    
    result = [
        [
            sum(A[i][k] * B[k][j] for k in range(cols_A))
            for j in range(cols_B)
        ]
        for i in range(rows_A)
    ]
    
    return result

# Example
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]

C = matrix_multiply_compact(A, B)
print(C)  # [[19, 22], [43, 50]]
```

#### Matrix Multiplication - Method 3 (Using zip)

```python
def matrix_multiply_zip(A, B):
    # Transpose B for easier multiplication
    B_T = [[B[j][i] for j in range(len(B))] for i in range(len(B[0]))]
    
    result = [
        [sum(a * b for a, b in zip(row_A, col_B)) for col_B in B_T]
        for row_A in A
    ]
    
    return result

# Example
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]

C = matrix_multiply_zip(A, B)
print(C)  # [[19, 22], [43, 50]]
```

### Matrix Multiplication with Functions

#### Using helper functions for clarity:

```python
def get_matrix_dimensions(matrix):
    return len(matrix), len(matrix[0])

def create_zero_matrix(rows, cols):
    return [[0 for j in range(cols)] for i in range(rows)]

def print_matrix(matrix):
    for row in matrix:
        print(row)

def matrix_multiply_v2(A, B):
    rows_A, cols_A = get_matrix_dimensions(A)
    rows_B, cols_B = get_matrix_dimensions(B)
    
    if cols_A != rows_B:
        print(f"Error: Cannot multiply {rows_A}x{cols_A} by {rows_B}x{cols_B}")
        return None
    
    result = create_zero_matrix(rows_A, cols_B)
    
    for i in range(rows_A):
        for j in range(cols_B):
            for k in range(cols_A):
                result[i][j] += A[i][k] * B[k][j]
    
    return result

# Example usage
A = [[1, 2, 3], [4, 5, 6]]
B = [[7, 8], [9, 10], [11, 12]]

print("Matrix A:")
print_matrix(A)
print("\nMatrix B:")
print_matrix(B)
print("\nMatrix A × B:")
C = matrix_multiply_v2(A, B)
if C:
    print_matrix(C)
```

### Matrix Multiplication Examples

```python
# Example 1: 2x2 matrices
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]
C = matrix_multiply(A, B)
# Result: [[19, 22], [43, 50]]

# Example 2: 3x3 identity matrix
I = [[1, 0, 0], [0, 1, 0], [0, 0, 1]]
A = [[2, 3, 4], [5, 6, 7], [8, 9, 10]]
C = matrix_multiply(I, A)
# Result: A (multiplying by identity gives original matrix)

# Example 3: Non-square matrices
A = [[1, 2, 3]]  # 1x3
B = [[4], [5], [6]]  # 3x1
C = matrix_multiply(A, B)
# Result: [[32]] (1x1 matrix)

# Example 4: Incompatible dimensions
A = [[1, 2], [3, 4]]  # 2x2
B = [[5, 6, 7], [8, 9, 10]]  # 2x3
C = matrix_multiply(A, B)
# Result: [[21, 24, 27], [47, 54, 61]] (2x3)

D = [[1, 2, 3]]  # 1x3
E = [[4, 5], [6, 7]]  # 2x2
F = matrix_multiply(D, E)
# Error: Cannot multiply (columns of D ≠ rows of E)
```

### Using NumPy for Matrix Operations

```python
import numpy as np

# Create matrices
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

# Matrix multiplication
C = np.matmul(A, B)  # or A @ B
print(C)
# [[19 22]
#  [43 50]]

# Element-wise multiplication
D = A * B  # NOT matrix multiplication!
print(D)
# [[ 5 12]
#  [21 32]]

# Other operations
print(A + B)      # Addition
print(A - B)      # Subtraction
print(2 * A)      # Scalar multiplication
print(A.T)        # Transpose
print(np.linalg.inv(A))  # Inverse
print(np.linalg.det(A))  # Determinant
```

---

## L5.7: Scope of Variables

### What is Scope?

**Scope** determines where a variable can be accessed in your code. Python has different levels of scope:

### LEGB Rule

Python follows the **LEGB** rule for variable lookup:

1. **L**ocal - Inside the current function
2. **E**nclosing - In enclosing functions (nested functions)
3. **G**lobal - At the module level
4. **B**uilt-in - Python built-in names

### 1. Local Scope

Variables defined inside a function are **local** to that function.

```python
def my_function():
    x = 10  # Local variable
    print(x)

my_function()  # Output: 10
# print(x)  # Error: NameError - x is not defined outside function
```

### 2. Global Scope

Variables defined outside all functions are **global**.

```python
x = 10  # Global variable

def my_function():
    print(x)  # Can access global variable

my_function()  # Output: 10
print(x)       # Output: 10
```

### 3. Local vs Global

```python
x = 10  # Global

def my_function():
    x = 20  # Local (shadows the global x)
    print(f"Inside function: {x}")

my_function()       # Output: Inside function: 20
print(f"Outside function: {x}")  # Output: Outside function: 10
```

### 4. The `global` Keyword

Use `global` to modify a global variable inside a function.

```python
x = 10  # Global

def modify_global():
    global x  # Declare that we're using the global x
    x = 20
    print(f"Inside function: {x}")

modify_global()     # Output: Inside function: 20
print(f"Outside function: {x}")  # Output: Outside function: 20 (modified!)
```

**Without `global`:**
```python
x = 10

def try_to_modify():
    x = 20  # Creates a new local variable, doesn't modify global

try_to_modify()
print(x)  # Output: 10 (global x unchanged)
```

### 5. Enclosing Scope (Nested Functions)

```python
def outer():
    x = "outer"  # Enclosing scope
    
    def inner():
        print(x)  # Can access enclosing variable
    
    inner()

outer()  # Output: outer
```

### 6. The `nonlocal` Keyword

Use `nonlocal` to modify a variable in the enclosing scope.

```python
def outer():
    x = "outer"
    
    def inner():
        nonlocal x  # Modify enclosing x
        x = "inner"
        print(f"Inside inner: {x}")
    
    inner()
    print(f"Inside outer: {x}")

outer()
# Output:
# Inside inner: inner
# Inside outer: inner (modified!)
```

**Without `nonlocal`:**
```python
def outer():
    x = "outer"
    
    def inner():
        x = "inner"  # Creates new local variable
        print(f"Inside inner: {x}")
    
    inner()
    print(f"Inside outer: {x}")

outer()
# Output:
# Inside inner: inner
# Inside outer: outer (unchanged)
```

### 7. Built-in Scope

Python's built-in functions and constants (like `print`, `len`, `True`, etc.)

```python
# Built-in function
print(len([1, 2, 3]))  # Output: 3

# Can shadow built-ins (but shouldn't!)
len = 10  # Bad practice!
# print(len([1, 2, 3]))  # Error: int is not callable

# Restore built-in
del len
print(len([1, 2, 3]))  # Output: 3 (works again)
```

### Complete LEGB Example

```python
x = "global"  # Global

def outer():
    x = "enclosing"  # Enclosing
    
    def inner():
        x = "local"  # Local
        print(x)
    
    inner()
    print(x)

outer()
print(x)

# Output:
# local      (Local scope in inner)
# enclosing  (Enclosing scope in outer)
# global     (Global scope)
```

### Scope Lookup Example

```python
x = "global"

def outer():
    # x is not defined here, so looks in enclosing scopes
    
    def inner():
        print(x)  # No local x, no enclosing x, finds global x
    
    inner()

outer()  # Output: global
```

### Common Pitfalls

#### Pitfall 1: Forgetting `global`

```python
count = 0

def increment():
    count += 1  # Error: UnboundLocalError
    # Python sees assignment, treats count as local
    # But tries to use it before assignment

increment()

# Fix:
def increment():
    global count
    count += 1
```

#### Pitfall 2: Mutable Default Arguments

```python
def add_to_list(item, my_list=[]):  # Default argument created once!
    my_list.append(item)
    return my_list

print(add_to_list(1))  # [1]
print(add_to_list(2))  # [1, 2] - Oops! Same list!

# Fix:
def add_to_list(item, my_list=None):
    if my_list is None:
        my_list = []
    my_list.append(item)
    return my_list

print(add_to_list(1))  # [1]
print(add_to_list(2))  # [2] - Correct!
```

#### Pitfall 3: Loop Variables

```python
# Loop variables persist after loop
for i in range(5):
    pass

print(i)  # Output: 4 (i still exists!)

# In list comprehension, variable doesn't leak (Python 3)
[x for x in range(5)]
# print(x)  # Error: x not defined
```

### Best Practices

1. **Minimize global variables** - use function parameters and return values
2. **Don't shadow built-ins** - avoid naming variables `list`, `dict`, `str`, etc.
3. **Use `global` and `nonlocal` sparingly** - they can make code harder to understand
4. **Be explicit** - use clear variable names to avoid confusion

```python
# Bad: Global variable modified everywhere
total = 0

def add(x):
    global total
    total += x

# Good: Use parameters and return values
def add(current_total, x):
    return current_total + x

total = 0
total = add(total, 5)
total = add(total, 10)
```

---

## L5.8: Tutorial on Functions

### What are Functions?

Functions are reusable blocks of code that perform specific tasks.

**Benefits:**
- Code reusability
- Better organization
- Easier testing and debugging
- Abstraction

### Defining Functions

```python
def function_name(parameters):
    """Docstring: describes what the function does"""
    # Function body
    return value
```

### 1. Basic Functions

```python
# Function with no parameters
def greet():
    print("Hello, World!")

greet()  # Output: Hello, World!

# Function with parameters
def greet_person(name):
    print(f"Hello, {name}!")

greet_person("Alice")  # Output: Hello, Alice!

# Function with return value
def add(a, b):
    return a + b

result = add(5, 3)
print(result)  # Output: 8
```

### 2. Parameters vs Arguments

```python
def greet(name, greeting):  # name, greeting are PARAMETERS
    print(f"{greeting}, {name}!")

greet("Alice", "Hello")  # "Alice", "Hello" are ARGUMENTS
```

### 3. Types of Arguments

#### a) Positional Arguments

```python
def describe_person(name, age, city):
    print(f"{name} is {age} years old and lives in {city}")

describe_person("Alice", 25, "NYC")
# Output: Alice is 25 years old and lives in NYC
```

#### b) Keyword Arguments

```python
describe_person(name="Bob", city="LA", age=30)
# Output: Bob is 30 years old and lives in LA
# Order doesn't matter with keyword arguments
```

#### c) Default Arguments

```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")              # Output: Hello, Alice!
greet("Bob", "Hi")          # Output: Hi, Bob!
greet("Charlie", greeting="Hey")  # Output: Hey, Charlie!
```

#### d) Variable-Length Arguments (*args)

```python
def sum_all(*numbers):
    total = 0
    for num in numbers:
        total += num
    return total

print(sum_all(1, 2, 3))        # Output: 6
print(sum_all(1, 2, 3, 4, 5))  # Output: 15

# *args creates a tuple of arguments
def print_args(*args):
    print(type(args))  # <class 'tuple'>
    for arg in args:
        print(arg)

print_args(1, "hello", 3.14)
```

#### e) Variable-Length Keyword Arguments (**kwargs)

```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="NYC")
# Output:
# name: Alice
# age: 25
# city: NYC

# **kwargs creates a dictionary
def show_kwargs(**kwargs):
    print(type(kwargs))  # <class 'dict'>
    print(kwargs)

show_kwargs(a=1, b=2, c=3)
# Output: {'a': 1, 'b': 2, 'c': 3}
```

#### f) Combining Different Argument Types

```python
def complex_function(a, b, *args, c=10, **kwargs):
    print(f"a: {a}")
    print(f"b: {b}")
    print(f"args: {args}")
    print(f"c: {c}")
    print(f"kwargs: {kwargs}")

complex_function(1, 2, 3, 4, 5, c=20, x=100, y=200)
# Output:
# a: 1
# b: 2
# args: (3, 4, 5)
# c: 20
# kwargs: {'x': 100, 'y': 200}
```

**Order must be:**
1. Positional arguments
2. *args
3. Keyword arguments
4. **kwargs

### 4. Return Values

```python
# Single return value
def square(x):
    return x ** 2

# Multiple return values (returns tuple)
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers) / len(numbers)

minimum, maximum, average = get_stats([1, 2, 3, 4, 5])
print(f"Min: {minimum}, Max: {maximum}, Avg: {average}")

# Return None (implicit)
def print_greeting():
    print("Hello!")
    # No return statement - returns None

result = print_greeting()
print(result)  # Output: None

# Early return
def is_positive(num):
    if num > 0:
        return True
    return False
```

### 5. Docstrings

Documentation strings help explain what a function does.

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.
    
    Parameters:
    length (float): The length of the rectangle
    width (float): The width of the rectangle
    
    Returns:
    float: The area of the rectangle
    """
    return length * width

# Access docstring
print(calculate_area.__doc__)
help(calculate_area)
```

### 6. Lambda Functions (Anonymous Functions)

Small, one-line functions.

```python
# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square = lambda x: x ** 2

print(square(5))  # Output: 25

# Lambda with multiple arguments
add = lambda x, y: x + y
print(add(3, 5))  # Output: 8

# Common use: with sorted, map, filter
numbers = [1, 5, 3, 9, 2]
sorted_numbers = sorted(numbers, key=lambda x: -x)  # Sort descending
print(sorted_numbers)  # [9, 5, 3, 2, 1]
```

### 7. Recursive Functions

Functions that call themselves.

```python
# Factorial
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # 5! = 120

# Fibonacci
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(6))  # 8

# Sum of list (recursive)
def recursive_sum(numbers):
    if len(numbers) == 0:
        return 0
    return numbers[0] + recursive_sum(numbers[1:])

print(recursive_sum([1, 2, 3, 4, 5]))  # 15
```

### 8. Higher-Order Functions

Functions that take other functions as arguments or return functions.

```python
# Function as argument
def apply_operation(x, y, operation):
    return operation(x, y)

def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

print(apply_operation(5, 3, add))       # 8
print(apply_operation(5, 3, multiply))  # 15

# Function returning function
def create_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

times_2 = create_multiplier(2)
times_5 = create_multiplier(5)

print(times_2(10))  # 20
print(times_5(10))  # 50
```

### 9. Nested Functions

```python
def outer(x):
    def inner(y):
        return x + y
    return inner

add_5 = outer(5)
print(add_5(10))  # 15
print(add_5(20))  # 25
```

### 10. Function Annotations (Type Hints)

```python
def greet(name: str, age: int) -> str:
    return f"{name} is {age} years old"

# Annotations don't enforce types, just documentation
result = greet("Alice", 25)
```

### Common Function Patterns

#### Pattern 1: Validation Function

```python
def is_valid_email(email):
    return "@" in email and "." in email.split("@")[1]

print(is_valid_email("test@example.com"))  # True
print(is_valid_email("invalid.email"))      # False
```

#### Pattern 2: Data Processing Function

```python
def process_scores(scores):
    return {
        "min": min(scores),
        "max": max(scores),
        "avg": sum(scores) / len(scores),
        "count": len(scores)
    }

scores = [85, 92, 78, 95, 88]
stats = process_scores(scores)
print(stats)
```

#### Pattern 3: Factory Function

```python
def create_person(name, age):
    return {
        "name": name,
        "age": age,
        "greet": lambda: f"Hi, I'm {name}"
    }

person = create_person("Alice", 25)
print(person["greet"]())  # Hi, I'm Alice
```

---

## L5.9: Iterators and Generators

### Iterators

An **iterator** is an object that can be iterated (looped) upon.

#### What is Iterable?

Objects like lists, tuples, strings, dictionaries are **iterable** - they can be looped over.

```python
# Iterables
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
my_string = "hello"

for item in my_list:
    print(item)
```

#### iter() and next()

```python
my_list = [1, 2, 3, 4, 5]

# Get iterator from iterable
my_iter = iter(my_list)

# Use next() to get items one by one
print(next(my_iter))  # 1
print(next(my_iter))  # 2
print(next(my_iter))  # 3
print(next(my_iter))  # 4
print(next(my_iter))  # 5
# print(next(my_iter))  # StopIteration error - no more items
```

#### Creating Custom Iterator

```python
class CountDown:
    def __init__(self, start):
        self.current = start
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        self.current -= 1
        return self.current + 1

# Usage
countdown = CountDown(5)
for num in countdown:
    print(num)
# Output: 5, 4, 3, 2, 1
```

### Generators

**Generators** are a simple way to create iterators using functions.

#### Generator Functions (using `yield`)

```python
def count_up_to(n):
    count = 1
    while count <= n:
        yield count
        count += 1

# Usage
counter = count_up_to(5)
print(next(counter))  # 1
print(next(counter))  # 2

# Or in a loop
for num in count_up_to(5):
    print(num)
# Output: 1, 2, 3, 4, 5
```

**Key Difference:**
- `return` - terminates function and returns value
- `yield` - pauses function, returns value, resumes from there next time

#### Generator vs Regular Function

```python
# Regular function - returns entire list (memory intensive)
def get_squares_list(n):
    result = []
    for i in range(1, n+1):
        result.append(i ** 2)
    return result

squares = get_squares_list(1000000)  # Creates huge list in memory

# Generator - yields one at a time (memory efficient)
def get_squares_generator(n):
    for i in range(1, n+1):
        yield i ** 2

squares = get_squares_generator(1000000)  # Generator object, minimal memory
```

#### Generator Examples

```python
# Example 1: Fibonacci generator
def fibonacci():
    a, b = 0, 1
    while True:  # Infinite generator
        yield a
        a, b = b, a + b

fib = fibonacci()
for _ in range(10):
    print(next(fib))
# Output: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34

# Example 2: Reading large files
def read_large_file(file_path):
    with open(file_path, 'r') as file:
        for line in file:
            yield line.strip()

# Memory efficient - processes one line at a time
# for line in read_large_file('huge_file.txt'):
#     process(line)

# Example 3: Prime number generator
def primes():
    num = 2
    while True:
        is_prime = True
        for i in range(2, int(num ** 0.5) + 1):
            if num % i == 0:
                is_prime = False
                break
        if is_prime:
            yield num
        num += 1

prime_gen = primes()
for _ in range(10):
    print(next(prime_gen))
# Output: 2, 3, 5, 7, 11, 13, 17, 19, 23, 29
```

#### Generator Expressions

Similar to list comprehensions, but use parentheses and are lazy (generate on demand).

```python
# List comprehension - creates entire list
squares_list = [x**2 for x in range(10)]
print(type(squares_list))  # <class 'list'>

# Generator expression - creates generator
squares_gen = (x**2 for x in range(10))
print(type(squares_gen))   # <class 'generator'>

# Use generator
for square in squares_gen:
    print(square)

# Another example
sum_of_squares = sum(x**2 for x in range(1000000))  # Memory efficient
```

#### Benefits of Generators

1. **Memory Efficient** - generate items one at a time
2. **Lazy Evaluation** - compute only when needed
3. **Can represent infinite sequences**
4. **Clean code** - easier to read than custom iterators

```python
# Compare memory usage
import sys

list_comp = [x for x in range(100000)]
gen_exp = (x for x in range(100000))

print(sys.getsizeof(list_comp))  # Large (e.g., 800984 bytes)
print(sys.getsizeof(gen_exp))    # Small (e.g., 112 bytes)
```

---

## L5.10: Lambda, Enumerate, Zip, Map, Filter

### 1. Lambda Functions

Anonymous functions created with `lambda` keyword.

**Syntax:** `lambda arguments: expression`

```python
# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square = lambda x: x ** 2

print(square(5))  # 25

# Multiple arguments
multiply = lambda x, y: x * y
print(multiply(3, 4))  # 12

# With conditional
max_of_two = lambda x, y: x if x > y else y
print(max_of_two(10, 20))  # 20
```

**Common Uses:**

```python
# 1. With sorted()
students = [("Alice", 85), ("Bob", 92), ("Charlie", 78)]
sorted_students = sorted(students, key=lambda x: x[1])  # Sort by grade
print(sorted_students)

# 2. With map()
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# 3. With filter()
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]
```

**Limitations:**
- Can only contain expressions, not statements
- Limited to a single line
- No docstrings
- Less readable for complex logic

```python
# Good use of lambda
add = lambda x, y: x + y

# Bad use of lambda (use regular function instead)
# complex_func = lambda x: x**2 if x > 0 else abs(x) if x < 0 else 0
```

### 2. Enumerate

Adds a counter to an iterable and returns enumerate object (of tuples).

**Syntax:** `enumerate(iterable, start=0)`

```python
# Basic usage
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")
# Output:
# 0: apple
# 1: banana
# 2: cherry

# Custom start index
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}: {fruit}")
# Output:
# 1: apple
# 2: banana
# 3: cherry

# Convert to list
indexed_fruits = list(enumerate(fruits))
print(indexed_fruits)
# [(0, 'apple'), (1, 'banana'), (2, 'cherry')]
```

**Practical Examples:**

```python
# Example 1: Finding index of specific item
fruits = ["apple", "banana", "cherry", "apple"]
for index, fruit in enumerate(fruits):
    if fruit == "apple":
        print(f"Found apple at index {index}")
# Output:
# Found apple at index 0
# Found apple at index 3

# Example 2: Processing with line numbers
lines = ["Line one", "Line two", "Line three"]
for line_num, line in enumerate(lines, start=1):
    print(f"{line_num}: {line}")

# Example 3: Create dictionary from list
colors = ["red", "green", "blue"]
color_dict = {i: color for i, color in enumerate(colors)}
print(color_dict)  # {0: 'red', 1: 'green', 2: 'blue'}
```

### 3. Zip

Combines multiple iterables into tuples.

**Syntax:** `zip(*iterables)`

```python
# Basic usage
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

combined = list(zip(names, ages, cities))
print(combined)
# [('Alice', 25, 'NYC'), ('Bob', 30, 'LA'), ('Charlie', 35, 'Chicago')]

# Iterate over zipped data
for name, age, city in zip(names, ages, cities):
    print(f"{name} is {age} years old and lives in {city}")
```

**Important:** `zip()` stops at the shortest iterable

```python
list1 = [1, 2, 3, 4, 5]
list2 = ['a', 'b', 'c']

result = list(zip(list1, list2))
print(result)  # [(1, 'a'), (2, 'b'), (3, 'c')] - stops at 3
```

**Practical Examples:**

```python
# Example 1: Create dictionary from two lists
keys = ["name", "age", "city"]
values = ["Alice", 25, "NYC"]
person = dict(zip(keys, values))
print(person)  # {'name': 'Alice', 'age': 25, 'city': 'NYC'}

# Example 2: Parallel iteration
prices = [10, 20, 30]
quantities = [2, 3, 1]

for price, quantity in zip(prices, quantities):
    print(f"Total: ${price * quantity}")
# Output: Total: $20, Total: $60, Total: $30

# Example 3: Transpose matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

transposed = list(zip(*matrix))  # * unpacks the matrix
print(transposed)
# [(1, 4, 7), (2, 5, 8), (3, 6, 9)]

# Convert back to lists
transposed = [list(row) for row in zip(*matrix)]
print(transposed)
# [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```

**Unzipping:**

```python
pairs = [(1, 'a'), (2, 'b'), (3, 'c')]
numbers, letters = zip(*pairs)
print(numbers)  # (1, 2, 3)
print(letters)  # ('a', 'b', 'c')
```

### 4. Map

Applies a function to all items in an iterable.

**Syntax:** `map(function, iterable, ...)`

```python
# Basic usage
numbers = [1, 2, 3, 4, 5]

# Square all numbers
squared = list(map(lambda x: x**2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# With regular function
def double(x):
    return x * 2

doubled = list(map(double, numbers))
print(doubled)  # [2, 4, 6, 8, 10]

# Multiple iterables
list1 = [1, 2, 3]
list2 = [10, 20, 30]

result = list(map(lambda x, y: x + y, list1, list2))
print(result)  # [11, 22, 33]
```

**Practical Examples:**

```python
# Example 1: Convert strings to integers
str_numbers = ["1", "2", "3", "4", "5"]
int_numbers = list(map(int, str_numbers))
print(int_numbers)  # [1, 2, 3, 4, 5]

# Example 2: Apply string method
words = ["hello", "world", "python"]
uppercase = list(map(str.upper, words))
print(uppercase)  # ['HELLO', 'WORLD', 'PYTHON']

# Example 3: Format strings
prices = [10.5, 20.99, 15.0]
formatted = list(map(lambda x: f"${x:.2f}", prices))
print(formatted)  # ['$10.50', '$20.99', '$15.00']

# Example 4: Dictionary transformation
persons = [
    {"name": "Alice", "age": 25},
    {"name": "Bob", "age": 30}
]

names = list(map(lambda x: x["name"], persons))
print(names)  # ['Alice', 'Bob']
```

**Map vs List Comprehension:**

```python
# Using map
squared_map = list(map(lambda x: x**2, range(5)))

# Using list comprehension (more Pythonic)
squared_comp = [x**2 for x in range(5)]

# Both produce: [0, 1, 4, 9, 16]
```

### 5. Filter

Filters items based on a function that returns True/False.

**Syntax:** `filter(function, iterable)`

```python
# Basic usage
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Filter even numbers
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]

# Filter odd numbers
odds = list(filter(lambda x: x % 2 != 0, numbers))
print(odds)  # [1, 3, 5, 7, 9]

# Filter numbers greater than 5
greater_than_5 = list(filter(lambda x: x > 5, numbers))
print(greater_than_5)  # [6, 7, 8, 9, 10]
```

**Practical Examples:**

```python
# Example 1: Filter strings by length
words = ["apple", "hi", "banana", "cat", "watermelon"]
long_words = list(filter(lambda x: len(x) > 5, words))
print(long_words)  # ['banana', 'watermelon']

# Example 2: Filter dictionaries
students = [
    {"name": "Alice", "grade": 85},
    {"name": "Bob", "grade": 92},
    {"name": "Charlie", "grade": 78},
    {"name": "Diana", "grade": 95}
]

high_scorers = list(filter(lambda x: x["grade"] >= 90, students))
print(high_scorers)
# [{'name': 'Bob', 'grade': 92}, {'name': 'Diana', 'grade': 95}]

# Example 3: Remove None/empty values
data = [1, None, 2, "", 3, 0, False, 4]
cleaned = list(filter(None, data))  # None as function removes falsy values
print(cleaned)  # [1, 2, 3, 4]

# Example 4: Filter with custom function
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

numbers = range(1, 21)
primes = list(filter(is_prime, numbers))
print(primes)  # [2, 3, 5, 7, 11, 13, 17, 19]
```

**Filter vs List Comprehension:**

```python
# Using filter
evens_filter = list(filter(lambda x: x % 2 == 0, range(10)))

# Using list comprehension (more Pythonic)
evens_comp = [x for x in range(10) if x % 2 == 0]

# Both produce: [0, 2, 4, 6, 8]
```

### Combining map() and filter()

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Square the even numbers
result = list(map(lambda x: x**2, filter(lambda x: x % 2 == 0, numbers)))
print(result)  # [4, 16, 36, 64, 100]

# More readable with list comprehension
result = [x**2 for x in numbers if x % 2 == 0]
print(result)  # [4, 16, 36, 64, 100]
```

### Reduce (from functools)

Applies a function cumulatively to items in an iterable.

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Sum all numbers
total = reduce(lambda x, y: x + y, numbers)
print(total)  # 15

# Equivalent to:
# ((((1 + 2) + 3) + 4) + 5) = 15

# Product of all numbers
product = reduce(lambda x, y: x * y, numbers)
print(product)  # 120

# Find maximum
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # 5

# With initial value
total = reduce(lambda x, y: x + y, numbers, 10)
print(total)  # 25 (10 + 1 + 2 + 3 + 4 + 5)
```

### Practical Combined Example

```python
# Process student data
students = [
    {"name": "Alice", "scores": [85, 90, 92]},
    {"name": "Bob", "scores": [78, 82, 88]},
    {"name": "Charlie", "scores": [95, 98, 93]},
    {"name": "Diana", "scores": [72, 75, 70]}
]

# 1. Calculate average for each student (map)
def calculate_average(student):
    avg = sum(student["scores"]) / len(student["scores"])
    return {**student, "average": avg}

students_with_avg = list(map(calculate_average, students))

# 2. Filter students with average >= 85 (filter)
high_performers = list(filter(lambda x: x["average"] >= 85, students_with_avg))

# 3. Get just the names (map)
names = list(map(lambda x: x["name"], high_performers))

print(names)  # ['Alice', 'Charlie']

# All in one (chained)
result = list(map(
    lambda x: x["name"],
    filter(
        lambda x: x["average"] >= 85,
        map(calculate_average, students)
    )
))
print(result)  # ['Alice', 'Charlie']

# Same with list comprehension (more readable)
result = [
    student["name"]
    for student in students
    if sum(student["scores"]) / len(student["scores"]) >= 85
]
print(result)  # ['Alice', 'Charlie']
```

---

## Summary

### Key Takeaways - Week 5

1. **Dictionaries** - Key-value pairs, mutable, fast lookups
2. **Collections** - Lists, tuples, sets, dicts - know when to use each
3. **Sorting** - `sorted()`, `sort()`, `key` parameter, lambda functions
4. **Matrix Operations** - Creation, addition, multiplication
5. **Scope** - LEGB rule, global, nonlocal keywords
6. **Functions** - Parameters, arguments, *args, **kwargs, return values
7. **Iterators & Generators** - Memory-efficient iteration, yield keyword
8. **Functional Programming** - lambda, enumerate, zip, map, filter, reduce

### Best Practices

- Use descriptive variable and function names
- Write docstrings for functions
- Prefer list comprehensions over map/filter when more readable
- Use generators for large datasets
- Minimize use of global variables
- Choose the right data structure for the task

---

*End of Week 5 Notes*
