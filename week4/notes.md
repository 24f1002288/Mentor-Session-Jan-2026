# Week 4: Python Fundamentals - Data Structures Deep Dive

## Table of Contents
1. [Lists - Deep Dive](#lists-deep-dive)
2. [Sets - Introduction and Usage](#sets-introduction-and-usage)
3. [Lists vs Sets - Comparison](#lists-vs-sets-comparison)
4. [Tuples - Immutable Sequences](#tuples-immutable-sequences)
5. [Hashability Concept](#hashability-concept)
6. [How Data Structures are Stored](#how-data-structures-are-stored)
7. [References and Identity](#references-and-identity)
8. [Type Checking with isinstance()](#type-checking-with-isinstance)
9. [Introduction to Functions](#introduction-to-functions)
10. [Comprehensions](#comprehensions)

---

## Lists - Deep Dive

### Review: What are Lists?

Lists are **ordered, mutable collections** that can store multiple values of any type.

```python
# Creating lists
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]
nested = [[1, 2], [3, 4], [5, 6]]
empty = []
```

### Important List Methods

#### 1. append() - Add Single Element to End
```python
fruits = ["apple", "banana"]
fruits.append("cherry")
print(fruits)  # ["apple", "banana", "cherry"]

# Note: Modifies the original list
```

#### 2. extend() - Add Multiple Elements to End
```python
fruits = ["apple", "banana"]
fruits.extend(["cherry", "date"])
print(fruits)  # ["apple", "banana", "cherry", "date"]

# Difference from append
fruits2 = ["apple", "banana"]
fruits2.append(["cherry", "date"])
print(fruits2)  # ["apple", "banana", ["cherry", "date"]]
# append adds the whole list as one element!
```

#### 3. insert() - Add Element at Specific Position
```python
fruits = ["apple", "cherry"]
fruits.insert(1, "banana")  # Insert at index 1
print(fruits)  # ["apple", "banana", "cherry"]

# Insert at beginning
fruits.insert(0, "mango")
print(fruits)  # ["mango", "apple", "banana", "cherry"]
```

#### 4. remove() - Remove First Occurrence of Value
```python
fruits = ["apple", "banana", "cherry", "banana"]
fruits.remove("banana")  # Removes first "banana"
print(fruits)  # ["apple", "cherry", "banana"]

# ValueError if element doesn't exist
# fruits.remove("mango")  # Error!
```

#### 5. pop() - Remove and Return Element
```python
fruits = ["apple", "banana", "cherry"]

# Remove last element
last = fruits.pop()
print(last)    # "cherry"
print(fruits)  # ["apple", "banana"]

# Remove at specific index
fruits = ["apple", "banana", "cherry"]
second = fruits.pop(1)
print(second)  # "banana"
print(fruits)  # ["apple", "cherry"]
```

#### 6. index() - Find Index of Element
```python
fruits = ["apple", "banana", "cherry"]
position = fruits.index("banana")
print(position)  # 1

# ValueError if not found
# fruits.index("mango")  # Error!

# Safe check before index
if "banana" in fruits:
    position = fruits.index("banana")
```

#### 7. count() - Count Occurrences
```python
numbers = [1, 2, 3, 2, 4, 2, 5]
count = numbers.count(2)
print(count)  # 3
```

#### 8. sort() - Sort List In-Place
```python
numbers = [3, 1, 4, 1, 5, 9, 2]
numbers.sort()
print(numbers)  # [1, 1, 2, 3, 4, 5, 9]

# Reverse sort
numbers.sort(reverse=True)
print(numbers)  # [9, 5, 4, 3, 2, 1, 1]

# Note: Modifies original list, returns None
```

#### 9. reverse() - Reverse List In-Place
```python
fruits = ["apple", "banana", "cherry"]
fruits.reverse()
print(fruits)  # ["cherry", "banana", "apple"]
```

#### 10. clear() - Remove All Elements
```python
fruits = ["apple", "banana", "cherry"]
fruits.clear()
print(fruits)  # []
```

#### 11. copy() - Create Shallow Copy
```python
original = [1, 2, 3]
duplicate = original.copy()

duplicate.append(4)
print(original)   # [1, 2, 3] - unchanged
print(duplicate)  # [1, 2, 3, 4]
```

### List Characteristics

**Ordered:** Elements maintain their position
```python
list1 = [1, 2, 3]
list2 = [3, 2, 1]
print(list1 == list2)  # False - order matters
```

**Mutable:** Can be modified after creation
```python
fruits = ["apple", "banana"]
fruits[0] = "mango"
print(fruits)  # ["mango", "banana"]
```

**Allows Duplicates:** Same value can appear multiple times
```python
numbers = [1, 2, 2, 3, 3, 3]
print(len(numbers))  # 6
```

**Dynamic Size:** Can grow or shrink
```python
numbers = []
numbers.append(1)
numbers.append(2)
print(numbers)  # [1, 2]
```

### List Access Time

**Access by Index: O(1) - Constant Time**
```python
fruits = ["apple", "banana", "cherry", "date"]
print(fruits[2])  # Instant access - O(1)
```
Very fast! Direct memory access by index.

**Search by Value: O(n) - Linear Time**
```python
fruits = ["apple", "banana", "cherry", "date"]
if "cherry" in fruits:  # Must check each element - O(n)
    print("Found!")
```
Slower! Must check elements one by one.

---

## Sets - Introduction and Usage

### What are Sets?

**Sets** are **unordered, mutable collections** of **unique elements**. Think of them as mathematical sets.

**Key Properties:**
1. **Unordered** - No indexing, no guaranteed order
2. **Unique elements** - Automatically removes duplicates
3. **Mutable** - Can add/remove elements
4. **Only hashable elements** - Can only store immutable types

### Creating Sets

```python
# Using curly braces
fruits = {"apple", "banana", "cherry"}
print(fruits)  # {"apple", "banana", "cherry"} (order may vary)

# Using set() constructor
numbers = set([1, 2, 3, 4, 5])
print(numbers)  # {1, 2, 3, 4, 5}

# Empty set (must use set(), not {})
empty = set()  # Correct
# empty = {}  # Wrong! This creates a dictionary

# Automatic duplicate removal
numbers = {1, 2, 2, 3, 3, 3, 4}
print(numbers)  # {1, 2, 3, 4} - duplicates removed!

# From string (each character becomes element)
letters = set("hello")
print(letters)  # {'h', 'e', 'l', 'o'} - only unique characters
```

### Important Set Methods

#### 1. add() - Add Single Element
```python
fruits = {"apple", "banana"}
fruits.add("cherry")
print(fruits)  # {"apple", "banana", "cherry"}

# Adding duplicate has no effect
fruits.add("apple")
print(fruits)  # Still {"apple", "banana", "cherry"}
```

#### 2. update() - Add Multiple Elements
```python
fruits = {"apple", "banana"}
fruits.update(["cherry", "date"])
print(fruits)  # {"apple", "banana", "cherry", "date"}

# Can also use another set
fruits.update({"elderberry", "fig"})
```

#### 3. remove() - Remove Element (Error if Not Found)
```python
fruits = {"apple", "banana", "cherry"}
fruits.remove("banana")
print(fruits)  # {"apple", "cherry"}

# KeyError if element doesn't exist
# fruits.remove("mango")  # Error!
```

#### 4. discard() - Remove Element (No Error)
```python
fruits = {"apple", "banana", "cherry"}
fruits.discard("banana")
print(fruits)  # {"apple", "cherry"}

# No error if element doesn't exist
fruits.discard("mango")  # Safe! No error
```

#### 5. pop() - Remove and Return Random Element
```python
fruits = {"apple", "banana", "cherry"}
item = fruits.pop()  # Removes arbitrary element
print(item)    # Could be any fruit
print(fruits)  # Two remaining fruits

# Note: Sets are unordered, so you can't control which element is removed
```

#### 6. clear() - Remove All Elements
```python
fruits = {"apple", "banana", "cherry"}
fruits.clear()
print(fruits)  # set()
```

### Set Operations (Mathematical Operations)

#### Union - All Elements from Both Sets
```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

# Method 1: Using union()
result = set1.union(set2)
print(result)  # {1, 2, 3, 4, 5}

# Method 2: Using | operator
result = set1 | set2
print(result)  # {1, 2, 3, 4, 5}
```

#### Intersection - Common Elements Only
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Method 1: Using intersection()
result = set1.intersection(set2)
print(result)  # {3, 4}

# Method 2: Using & operator
result = set1 & set2
print(result)  # {3, 4}
```

#### Difference - Elements in First but Not Second
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Method 1: Using difference()
result = set1.difference(set2)
print(result)  # {1, 2} - in set1 but not in set2

# Method 2: Using - operator
result = set1 - set2
print(result)  # {1, 2}

# Note: Order matters!
result = set2 - set1
print(result)  # {5, 6} - in set2 but not in set1
```

#### Symmetric Difference - Elements in Either but Not Both
```python
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

# Method 1: Using symmetric_difference()
result = set1.symmetric_difference(set2)
print(result)  # {1, 2, 5, 6}

# Method 2: Using ^ operator
result = set1 ^ set2
print(result)  # {1, 2, 5, 6}
```

### Set Comparison Methods

#### issubset() - Check if Subset
```python
set1 = {1, 2}
set2 = {1, 2, 3, 4}

print(set1.issubset(set2))  # True - all elements of set1 are in set2
print(set2.issubset(set1))  # False

# Using <= operator
print(set1 <= set2)  # True
```

#### issuperset() - Check if Superset
```python
set1 = {1, 2, 3, 4}
set2 = {1, 2}

print(set1.issuperset(set2))  # True - set1 contains all elements of set2
print(set2.issuperset(set1))  # False

# Using >= operator
print(set1 >= set2)  # True
```

#### isdisjoint() - Check if No Common Elements
```python
set1 = {1, 2, 3}
set2 = {4, 5, 6}
set3 = {3, 4, 5}

print(set1.isdisjoint(set2))  # True - no common elements
print(set1.isdisjoint(set3))  # False - 3 is common
```

### Set Characteristics

**Unordered:** No indexing, no guaranteed order
```python
fruits = {"apple", "banana", "cherry"}
# fruits[0]  # Error! No indexing
# Can't use position to access elements
```

**Unique Elements:** Automatically removes duplicates
```python
numbers = {1, 2, 2, 3, 3, 3}
print(numbers)  # {1, 2, 3}
```

**Mutable:** Can add/remove elements
```python
fruits = {"apple"}
fruits.add("banana")
fruits.remove("apple")
```

**Only Hashable Elements:** Can only contain immutable types
```python
# Valid - all hashable
valid_set = {1, "hello", 3.14, True, (1, 2)}

# Invalid - lists are not hashable
# invalid_set = {1, 2, [3, 4]}  # Error!
```

### Set Access Time

**Membership Test: O(1) - Constant Time**
```python
large_set = set(range(1000000))
print(1000 in large_set)  # Instant! - O(1)
```
Very fast! Uses hash table for direct lookup.

**No Index Access:** Can't access by position
```python
fruits = {"apple", "banana", "cherry"}
# fruits[0]  # Error! Sets don't support indexing
```

---

## Lists vs Sets - Comparison

### Feature Comparison Table

| Feature | List | Set |
|---------|------|-----|
| **Ordered** | Yes - maintains insertion order | No - unordered |
| **Indexing** | Yes - `list[0]` | No - no indexing |
| **Duplicates** | Allowed | Automatically removed |
| **Mutable** | Yes | Yes |
| **Syntax** | `[1, 2, 3]` | `{1, 2, 3}` |
| **Empty** | `[]` | `set()` |
| **Search Speed** | O(n) - Linear | O(1) - Constant |
| **Access by Index** | O(1) - Constant | Not supported |
| **Can Contain** | Any type | Only hashable types |
| **Use Cases** | Ordered data, duplicates OK | Unique items, fast lookup |

### Tradeoffs and When to Use

#### Use **LIST** when:

1. **Order matters**
```python
# Preserve order of tasks
tasks = ["wake up", "breakfast", "work", "dinner", "sleep"]
```

2. **You need indexing/position access**
```python
scores = [85, 90, 78, 92]
first_score = scores[0]
last_score = scores[-1]
```

3. **Duplicates are meaningful**
```python
# Count occurrences
votes = ["Alice", "Bob", "Alice", "Alice", "Bob"]
```

4. **You need to store unhashable types**
```python
# Store lists of coordinates
paths = [[0, 0], [1, 2], [3, 4]]
```

#### Use **SET** when:

1. **Only unique values needed**
```python
# Remove duplicates
numbers = [1, 2, 2, 3, 3, 3, 4]
unique_numbers = set(numbers)  # {1, 2, 3, 4}
```

2. **Fast membership testing required**
```python
# Check if user is admin (fast lookup)
admins = {"alice", "bob", "charlie"}
if username in admins:  # O(1) - instant
    print("Admin access granted")
```

3. **Mathematical set operations needed**
```python
# Find common interests
alice_interests = {"coding", "music", "sports"}
bob_interests = {"music", "art", "sports"}
common = alice_interests & bob_interests  # {"music", "sports"}
```

4. **Order doesn't matter**
```python
# Store unique tags
tags = {"python", "programming", "tutorial"}
```

### Performance Comparison

```python
import random

# Create large collections
numbers_list = list(range(100000))
numbers_set = set(range(100000))

# Searching
# List: O(n) - must check each element
if 99999 in numbers_list:  # Slow for large lists
    pass

# Set: O(1) - direct hash lookup
if 99999 in numbers_set:   # Always fast!
    pass

# Indexing
print(numbers_list[5000])  # Fast - O(1)
# print(numbers_set[5000])  # Error! Sets don't support indexing
```

### Conversion Between Lists and Sets

```python
# List to Set (removes duplicates)
numbers_list = [1, 2, 2, 3, 3, 3, 4]
numbers_set = set(numbers_list)
print(numbers_set)  # {1, 2, 3, 4}

# Set to List (creates ordered version)
numbers_set = {3, 1, 4, 1, 5}
numbers_list = list(numbers_set)
print(numbers_list)  # [1, 3, 4, 5] (order may vary)

# Remove duplicates from list
original = [1, 2, 2, 3, 3, 3, 4]
unique = list(set(original))
print(unique)  # [1, 2, 3, 4]
```

### Practical Example: Use Case Comparison

```python
# Scenario: Track student attendance

# Using List (preserves all records, including duplicates)
attendance_list = []
attendance_list.append("Alice")
attendance_list.append("Bob")
attendance_list.append("Alice")  # Alice came twice
print(f"Total check-ins: {len(attendance_list)}")  # 3
print(f"Alice came {attendance_list.count('Alice')} times")  # 2

# Using Set (only unique students)
attendance_set = set()
attendance_set.add("Alice")
attendance_set.add("Bob")
attendance_set.add("Alice")  # Duplicate ignored
print(f"Unique students: {len(attendance_set)}")  # 2
print(f"Did Alice attend? {'Alice' in attendance_set}")  # Fast check!
```

---

## Tuples - Immutable Sequences

### What are Tuples?

**Tuples** are **ordered, immutable sequences**. Similar to lists but cannot be modified after creation.

**Key Properties:**
1. **Ordered** - Elements maintain their position
2. **Immutable** - Cannot be changed after creation
3. **Allow duplicates** - Same value can appear multiple times
4. **Hashable** - Can be used as dictionary keys or set elements (if contains only hashable elements)

### Creating Tuples

```python
# Using parentheses
coordinates = (10, 20)
print(coordinates)  # (10, 20)

# Multiple elements
person = ("Alice", 25, "Engineer")
print(person)  # ("Alice", 25, "Engineer")

# Without parentheses (tuple packing)
point = 1, 2, 3
print(point)  # (1, 2, 3)

# Single element tuple (comma is required!)
single = (5,)  # Note the comma
print(type(single))  # <class 'tuple'>

# Wrong! This is just an integer
not_tuple = (5)
print(type(not_tuple))  # <class 'int'>

# Empty tuple
empty = ()
print(empty)  # ()

# Using tuple() constructor
from_list = tuple([1, 2, 3])
print(from_list)  # (1, 2, 3)

from_string = tuple("hello")
print(from_string)  # ('h', 'e', 'l', 'l', 'o')
```

### Accessing Tuple Elements

```python
# Indexing (same as lists)
coordinates = (10, 20, 30)
print(coordinates[0])   # 10
print(coordinates[-1])  # 30

# Slicing (same as lists)
numbers = (1, 2, 3, 4, 5)
print(numbers[1:4])   # (2, 3, 4)
print(numbers[:3])    # (1, 2, 3)
print(numbers[::2])   # (1, 3, 5)

# Tuple unpacking
point = (10, 20)
x, y = point
print(x)  # 10
print(y)  # 20

# Unpacking with multiple values
person = ("Alice", 25, "Engineer")
name, age, job = person
print(name)  # "Alice"
print(age)   # 25
print(job)   # "Engineer"

# Extended unpacking
numbers = (1, 2, 3, 4, 5)
first, *middle, last = numbers
print(first)   # 1
print(middle)  # [2, 3, 4]
print(last)    # 5
```

### Tuple Methods (Only 2!)

Tuples have very few methods because they're immutable.

#### 1. count() - Count Occurrences
```python
numbers = (1, 2, 3, 2, 4, 2, 5)
count = numbers.count(2)
print(count)  # 3
```

#### 2. index() - Find First Index
```python
numbers = (1, 2, 3, 2, 4, 2, 5)
position = numbers.index(3)
print(position)  # 2

# ValueError if not found
# numbers.index(10)  # Error!
```

### Immutability - The Defining Feature

**Cannot Modify Elements:**
```python
point = (10, 20)
# point[0] = 15  # Error! Tuples are immutable
```

**Cannot Add Elements:**
```python
coordinates = (10, 20)
# coordinates.append(30)  # Error! No append method
```

**Cannot Remove Elements:**
```python
point = (10, 20, 30)
# point.remove(20)  # Error! No remove method
# del point[1]      # Error! Cannot delete items
```

**BUT Can Reassign Entire Tuple:**
```python
point = (10, 20)
print(point)  # (10, 20)

point = (30, 40)  # Creating new tuple, not modifying
print(point)  # (30, 40)
```

**Nested Mutable Objects Can Change:**
```python
# Tuple containing a list
data = (1, 2, [3, 4])

# Cannot change tuple elements
# data[0] = 10  # Error!

# BUT can modify the list inside
data[2].append(5)
print(data)  # (1, 2, [3, 4, 5])

# This is because the tuple stores a reference to the list,
# not the list contents themselves
```

### Advantages of Tuples

#### 1. **Data Integrity - Cannot Be Accidentally Modified**
```python
# Configuration that shouldn't change
DATABASE_CONFIG = ("localhost", 5432, "mydb")

# Later in code...
# DATABASE_CONFIG[0] = "newhost"  # Error! Protected from change
```

#### 2. **Faster than Lists**
```python
# Tuples are slightly faster because they're immutable
tuple_data = (1, 2, 3, 4, 5)
list_data = [1, 2, 3, 4, 5]

# Tuple operations are faster (small difference)
```

#### 3. **Can Be Used as Dictionary Keys**
```python
# Tuple as key (works!)
locations = {
    (10, 20): "Point A",
    (30, 40): "Point B"
}
print(locations[(10, 20)])  # "Point A"

# List as key (doesn't work!)
# locations = {
#     [10, 20]: "Point A"  # Error! Lists are not hashable
# }
```

#### 4. **Can Be Stored in Sets**
```python
# Tuples in a set (works!)
points = {(0, 0), (1, 1), (2, 2)}
print(points)  # {(0, 0), (1, 1), (2, 2)}

# Lists in a set (doesn't work!)
# points = {[0, 0], [1, 1]}  # Error! Lists are not hashable
```

#### 5. **Safe Function Return Values**
```python
def get_coordinates():
    return (10, 20)  # Caller can't accidentally modify

coords = get_coordinates()
# coords[0] = 15  # Error! Protected
```

### Tradeoffs of Tuples

**Advantages:**
- Immutable (data integrity)
- Faster than lists
- Hashable (can be dict keys, set elements)
- Less memory usage
- Safe for concurrent access (if needed later)

**Disadvantages:**
- Cannot be modified (need to create new tuple)
- Fewer methods (only count and index)
- Less flexible than lists

### When to Use Tuples vs Lists

**Use TUPLE when:**
```python
# 1. Data shouldn't change (coordinates, RGB colors, dates)
point = (10, 20)
color = (255, 0, 0)  # RGB for red
date = (2024, 3, 15)

# 2. Function returns multiple values
def get_user_info():
    return ("Alice", 25, "alice@email.com")

# 3. Dictionary keys
city_coordinates = {
    ("New York", "USA"): (40.7128, -74.0060),
    ("London", "UK"): (51.5074, -0.1278)
}

# 4. Set elements (if needed)
coordinate_set = {(0, 0), (1, 1), (2, 2)}
```

**Use LIST when:**
```python
# 1. Data needs to change
tasks = ["task1", "task2"]
tasks.append("task3")  # Need to add more

# 2. Order matters and items can be added/removed
playlist = ["song1", "song2", "song3"]
playlist.remove("song2")

# 3. Need list-specific methods
numbers = [3, 1, 4, 1, 5]
numbers.sort()  # Tuples can't do this

# 4. Building collection gradually
results = []
for i in range(10):
    results.append(i * 2)
```

---

## Hashability Concept

### What is Hashability?

**Hashable** means an object can be converted to a **hash value** (a fixed-size integer) using a **hash function**.

**Key Point:** Hash value should remain constant throughout the object's lifetime.

### Why Does Hashability Matter?

Hash values enable:
1. **Fast lookups** in dictionaries and sets (O(1) time)
2. **Using objects as dictionary keys**
3. **Storing objects in sets**

### Hashable vs Unhashable Types

**Hashable (Immutable) Types:**
```python
# Numbers
hash(42)        # Works
hash(3.14)      # Works

# Strings
hash("hello")   # Works

# Tuples (if containing only hashable items)
hash((1, 2, 3))            # Works
hash(("a", "b", "c"))      # Works
hash((1, "hello", 3.14))   # Works

# Booleans
hash(True)      # Works
hash(False)     # Works

# None
hash(None)      # Works
```

**Unhashable (Mutable) Types:**
```python
# Lists
# hash([1, 2, 3])  # Error! Lists are mutable

# Sets
# hash({1, 2, 3})  # Error! Sets are mutable

# Dictionaries
# hash({"a": 1})   # Error! Dicts are mutable
```

### Why Immutable = Hashable?

**Mutable objects can change, which would change their hash value:**
```python
# Hypothetical scenario (doesn't actually work)
my_list = [1, 2, 3]
# hash1 = hash(my_list)  # Suppose this worked
my_list.append(4)
# hash2 = hash(my_list)  # Would be different!

# This would break dictionaries and sets!
```

**Immutable objects never change, so hash stays constant:**
```python
my_tuple = (1, 2, 3)
hash1 = hash(my_tuple)  # Some value
# my_tuple can't be modified
hash2 = hash(my_tuple)  # Same value
# hash1 == hash2  # Always True!
```

### Tuples and Hashability

**Tuples are hashable ONLY if all elements are hashable:**
```python
# Hashable tuple (all elements hashable)
tuple1 = (1, 2, "hello")
print(hash(tuple1))  # Works!

# Unhashable tuple (contains list)
tuple2 = (1, 2, [3, 4])
# print(hash(tuple2))  # Error! Contains unhashable list

# Can use hashable tuples as dict keys
locations = {
    (10, 20): "Point A",
    (30, 40): "Point B"
}

# Can store hashable tuples in sets
coordinates = {(0, 0), (1, 1), (2, 2)}
```

### Practical Examples

#### Example 1: Dictionary Keys
```python
# Hashable keys (work)
valid_dict = {
    1: "one",
    "two": 2,
    (3, 4): "tuple",
    True: "boolean"
}

# Unhashable keys (don't work)
# invalid_dict = {
#     [1, 2]: "list"  # Error!
# }
```

#### Example 2: Set Elements
```python
# Hashable elements (work)
valid_set = {1, "hello", (1, 2), True}

# Unhashable elements (don't work)
# invalid_set = {1, 2, [3, 4]}  # Error!
```

#### Example 3: Caching Results
```python
# Using tuples as cache keys
cache = {}

def expensive_calculation(x, y):
    key = (x, y)  # Tuple as key
    
    if key in cache:
        return cache[key]  # Fast lookup!
    
    result = x ** y  # Expensive operation
    cache[key] = result
    return result

print(expensive_calculation(2, 10))  # Calculates
print(expensive_calculation(2, 10))  # Returns cached
```

---

## How Data Structures are Stored

### Lists - Stored in Memory

**Lists store references to objects in contiguous memory:**

```python
numbers = [10, 20, 30]
```

**Memory Layout:**
```
List Object:
[Reference to 10] [Reference to 20] [Reference to 30]
     ↓                 ↓                 ↓
   [10]              [20]              [30]
```

**Key Points:**
1. List itself is an array of references
2. Actual objects stored elsewhere in memory
3. Fast index access (direct memory calculation)
4. Insert/delete in middle is slow (must shift elements)

### Sets - Stored Using Hash Table

**Sets use hash tables for storage:**

```python
fruits = {"apple", "banana", "cherry"}
```

**Memory Layout:**
```
Hash Table:
Index 0: [empty]
Index 1: → "apple"
Index 2: [empty]
Index 3: → "banana"
Index 4: [empty]
Index 5: → "cherry"
...
```

**How it works:**
1. Hash function converts element to index
2. Element stored at that index
3. Collisions handled (multiple elements same index)

**Key Points:**
- Very fast membership test: hash(element) → check index
- No order preservation
- More memory usage than lists (hash table overhead)

### Tuples - Stored in Memory

**Tuples similar to lists but more compact:**

```python
point = (10, 20, 30)
```

**Memory Layout:**
```
Tuple Object (immutable):
[Reference to 10] [Reference to 20] [Reference to 30]
     ↓                 ↓                 ↓
   [10]              [20]              [30]
```

**Key Points:**
1. More compact than lists (less overhead)
2. Cannot change, so more optimizations possible
3. Slightly faster access than lists
4. Can be cached more efficiently by Python

### Memory and Performance Implications

```python
# Lists: Good for indexing, bad for searching
my_list = [1, 2, 3, 4, 5]
print(my_list[2])      # Fast - O(1) direct access
print(5 in my_list)    # Slow - O(n) linear search

# Sets: Bad for indexing, good for searching
my_set = {1, 2, 3, 4, 5}
# print(my_set[2])     # Error! No indexing
print(5 in my_set)     # Fast - O(1) hash lookup

# Tuples: Like lists but more compact and faster
my_tuple = (1, 2, 3, 4, 5)
print(my_tuple[2])     # Fast - O(1) direct access
print(5 in my_tuple)   # Slow - O(n) linear search (like list)
```

---

## References and Identity

### Store by Reference

**Variables store references, not actual objects:**

```python
# Create a list
list1 = [1, 2, 3]
list2 = list1  # list2 references same object as list1

# Modify through list2
list2.append(4)

# Both variables show change (same object!)
print(list1)  # [1, 2, 3, 4]
print(list2)  # [1, 2, 3, 4]
```

**Visualization:**
```
list1 → [1, 2, 3, 4] ← list2
     (same object)
```

### The `is` Keyword - Identity Check

**`is` checks if two variables reference the SAME object:**

```python
# Same object
list1 = [1, 2, 3]
list2 = list1
print(list1 is list2)  # True - same object

# Different objects, same content
list3 = [1, 2, 3]
list4 = [1, 2, 3]
print(list3 is list4)  # False - different objects

# Use == to compare content
print(list3 == list4)  # True - same content
```

### `is` vs `==`

**`is` → Identity (same object?)**
**`==` → Equality (same content?)**

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True - same content
print(a is b)  # False - different objects

print(a == c)  # True - same content
print(a is c)  # True - same object
```

**Visual Representation:**
```
a → [1, 2, 3] ← c (same object, is returns True)

b → [1, 2, 3] (different object with same content, is returns False)
```

### Comparing Data Structures

#### Lists - Reference Comparison
```python
# Same reference
list1 = [1, 2, 3]
list2 = list1
print(list1 is list2)   # True
print(list1 == list2)   # True

# Different references, same content
list3 = [1, 2, 3]
list4 = [1, 2, 3]
print(list3 is list4)   # False
print(list3 == list4)   # True

# Creating a copy
list5 = [1, 2, 3]
list6 = list5.copy()    # or list5[:]
print(list5 is list6)   # False - different objects
print(list5 == list6)   # True - same content
```

#### Sets - Reference Comparison
```python
set1 = {1, 2, 3}
set2 = set1
print(set1 is set2)   # True

set3 = {1, 2, 3}
set4 = {1, 2, 3}
print(set3 is set4)   # False
print(set3 == set4)   # True
```

#### Tuples - Special Case
```python
# Small tuples may be cached by Python
tuple1 = (1, 2)
tuple2 = (1, 2)
print(tuple1 is tuple2)  # Might be True (caching)

# Larger tuples usually different
tuple3 = (1, 2, 3, 4, 5)
tuple4 = (1, 2, 3, 4, 5)
print(tuple3 is tuple4)  # Usually False

# Always use == for content comparison
print(tuple1 == tuple2)  # True - reliable
```

### Practical Implications

#### Modifying Through Multiple References
```python
# Danger: Unintended modification
original = [1, 2, 3]
reference = original

reference.append(4)
print(original)  # [1, 2, 3, 4] - Surprise!

# Solution: Create a copy
original = [1, 2, 3]
copy = original.copy()

copy.append(4)
print(original)  # [1, 2, 3] - Unchanged
print(copy)      # [1, 2, 3, 4]
```

#### Function Arguments
```python
def modify_list(lst):
    lst.append(999)  # Modifies original!

my_list = [1, 2, 3]
modify_list(my_list)
print(my_list)  # [1, 2, 3, 999]

# To avoid: Pass a copy
my_list = [1, 2, 3]
modify_list(my_list.copy())
print(my_list)  # [1, 2, 3] - Unchanged
```

#### With Tuples (Immutable)
```python
def try_modify_tuple(tup):
    # tup[0] = 10  # Error! Tuples are immutable
    tup = (10, 20)  # Creates new tuple, doesn't affect original

my_tuple = (1, 2, 3)
try_modify_tuple(my_tuple)
print(my_tuple)  # (1, 2, 3) - Safe!
```

---

## Type Checking with isinstance()

### What is isinstance()?

**isinstance()** is a built-in function that checks if an object is an instance of a specified type or class.

**Syntax:**
```python
isinstance(object, type)
isinstance(object, (type1, type2, type3))  # Check multiple types
```

**Returns:** `True` or `False`

### Basic Usage

```python
# Check integer
x = 42
print(isinstance(x, int))      # True
print(isinstance(x, str))      # False

# Check string
name = "Alice"
print(isinstance(name, str))   # True
print(isinstance(name, int))   # False

# Check float
price = 19.99
print(isinstance(price, float))  # True
print(isinstance(price, int))    # False

# Check boolean (bool is subclass of int!)
flag = True
print(isinstance(flag, bool))    # True
print(isinstance(flag, int))     # True (because bool inherits from int)

# Check list
numbers = [1, 2, 3]
print(isinstance(numbers, list))  # True
print(isinstance(numbers, set))   # False

# Check tuple
coordinates = (10, 20)
print(isinstance(coordinates, tuple))  # True

# Check set
unique = {1, 2, 3}
print(isinstance(unique, set))    # True
```

### Checking Multiple Types

```python
# Check if value is int OR float
value = 3.14
print(isinstance(value, (int, float)))  # True

value = "hello"
print(isinstance(value, (int, float)))  # False

# Check if value is any collection type
data = [1, 2, 3]
print(isinstance(data, (list, tuple, set)))  # True

data = {1, 2, 3}
print(isinstance(data, (list, tuple, set)))  # True

data = "hello"
print(isinstance(data, (list, tuple, set)))  # False
```

### isinstance() vs type()

**isinstance()** is generally preferred over **type()** for type checking.

```python
x = 42

# Using type() - exact type match
print(type(x) == int)        # True
print(type(x) == bool)       # False

# Using isinstance() - includes inheritance
print(isinstance(x, int))    # True

# Example with bool (subclass of int)
flag = True

print(type(flag) == int)           # False (exact type is bool)
print(isinstance(flag, int))       # True (bool inherits from int)
print(isinstance(flag, bool))      # True

# isinstance() is more flexible
print(type(flag) == bool)          # True
print(isinstance(flag, (int, bool)))  # True
```

### Practical Uses of isinstance()

#### 1. Input Validation
```python
def process_data(data):
    if isinstance(data, list):
        print("Processing list...")
        for item in data:
            print(item)
    elif isinstance(data, str):
        print("Processing string...")
        print(data.upper())
    elif isinstance(data, (int, float)):
        print("Processing number...")
        print(data * 2)
    else:
        print("Unsupported data type")

process_data([1, 2, 3])      # Processing list...
process_data("hello")        # Processing string...
process_data(42)             # Processing number...
```

#### 2. Safe Type Conversion
```python
value = input("Enter a number: ")

# Check if it's already a number or needs conversion
if isinstance(value, str):
    if value.isdigit():
        value = int(value)
        print(f"Converted to int: {value}")
    else:
        print("Not a valid number")
elif isinstance(value, (int, float)):
    print(f"Already a number: {value}")
```

#### 3. Working with Collections
```python
data = [1, 2, 3, 4, 5]

# Check if it's a collection we can iterate over
if isinstance(data, (list, tuple, set)):
    print("This is iterable:")
    for item in data:
        print(item)
else:
    print("Not a collection type")
```

#### 4. Type-Specific Operations
```python
def double_value(value):
    if isinstance(value, (int, float)):
        return value * 2
    elif isinstance(value, str):
        return value + value  # String repetition
    elif isinstance(value, list):
        return value + value  # List concatenation
    else:
        return None

print(double_value(5))        # 10
print(double_value("hi"))     # "hihi"
print(double_value([1, 2]))   # [1, 2, 1, 2]
```

### isinstance() with Data Structures

```python
# Distinguish between mutable and immutable sequences
data1 = [1, 2, 3]
data2 = (1, 2, 3)

if isinstance(data1, list):
    print("data1 is a list (mutable)")
    data1.append(4)  # Safe to modify

if isinstance(data2, tuple):
    print("data2 is a tuple (immutable)")
    # data2.append(4)  # Would cause error

# Check for hashable types
def can_be_dict_key(obj):
    if isinstance(obj, (int, float, str, tuple, bool)):
        return True
    elif isinstance(obj, (list, set)):
        return False
    else:
        return False

print(can_be_dict_key((1, 2)))     # True
print(can_be_dict_key([1, 2]))     # False
```

### isinstance() in Loops

```python
# Process mixed data types
mixed_data = [42, "hello", 3.14, [1, 2], (3, 4), {5, 6}]

for item in mixed_data:
    if isinstance(item, int):
        print(f"Integer: {item}")
    elif isinstance(item, str):
        print(f"String: {item}")
    elif isinstance(item, float):
        print(f"Float: {item}")
    elif isinstance(item, list):
        print(f"List with {len(item)} items")
    elif isinstance(item, tuple):
        print(f"Tuple with {len(item)} items")
    elif isinstance(item, set):
        print(f"Set with {len(item)} items")

# Output:
# Integer: 42
# String: hello
# Float: 3.14
# List with 2 items
# Tuple with 2 items
# Set with 2 items
```

### Common Type Checks

```python
# Numeric types
x = 10
print(isinstance(x, (int, float)))  # True - any number

# String types
s = "hello"
print(isinstance(s, str))  # True

# Sequence types (ordered)
seq = [1, 2, 3]
print(isinstance(seq, (list, tuple, str)))  # True

# Collection types
coll = {1, 2, 3}
print(isinstance(coll, (list, tuple, set)))  # True

# Check if None
value = None
print(isinstance(value, type(None)))  # True
print(value is None)  # Better way to check None
```

### isinstance() Best Practices

**DO:**
```python
# Use isinstance() for type checking
if isinstance(value, int):
    print("It's an integer")

# Check multiple types
if isinstance(value, (int, float)):
    print("It's a number")

# Use in validation
if not isinstance(data, list):
    print("Error: Expected a list")
```

**DON'T:**
```python
# Don't use type() for checking
# if type(value) == int:  # Less flexible

# Don't overuse - Python is dynamically typed
# Sometimes "duck typing" is better
# (if it walks like a duck, it's a duck)

# Instead of:
if isinstance(obj, (list, tuple)):
    for item in obj:
        print(item)

# Consider:
try:
    for item in obj:  # Just try to iterate
        print(item)
except TypeError:
    print("Not iterable")
```

---

## Introduction to Functions

### What are Functions?

**Functions** are reusable blocks of code that perform a specific task. They help organize code, avoid repetition, and make programs more modular.

**Benefits:**
- **Code reuse** - Write once, use many times
- **Organization** - Break complex problems into smaller pieces
- **Maintainability** - Easier to update and debug
- **Abstraction** - Hide implementation details

### Types of Functions in Python

#### 1. Built-in Functions

**Built-in functions** are pre-defined functions that come with Python.

**Examples:**
```python
# We've been using these all along!

# Input/Output
print("Hello")           # Display output
input("Enter name: ")    # Get user input

# Type conversion
int("42")               # Convert to integer
str(42)                 # Convert to string
float("3.14")           # Convert to float
list((1, 2, 3))        # Convert to list
set([1, 2, 2, 3])      # Convert to set
tuple([1, 2, 3])       # Convert to tuple

# Math functions
abs(-5)                 # Absolute value: 5
max(1, 5, 3)           # Maximum: 5
min(1, 5, 3)           # Minimum: 1
sum([1, 2, 3, 4])      # Sum: 10
len([1, 2, 3])         # Length: 3
round(3.14159, 2)      # Round: 3.14
pow(2, 3)              # Power: 8

# Type checking
type(42)               # Get type: <class 'int'>
isinstance(42, int)    # Check type: True

# Range
range(10)              # Generate sequence: 0-9

# Sorting
sorted([3, 1, 4, 1, 5])  # Returns sorted list: [1, 1, 3, 4, 5]
reversed([1, 2, 3])      # Returns reversed iterator

# Others
help(print)            # Get help on a function
dir([])                # List methods of object
```

**Common Built-in Functions:**

| Function | Purpose | Example |
|----------|---------|---------|
| `print()` | Display output | `print("Hello")` |
| `input()` | Get user input | `input("Name: ")` |
| `len()` | Get length | `len([1, 2, 3])` → 3 |
| `type()` | Get type | `type(42)` → int |
| `int()` | Convert to int | `int("5")` → 5 |
| `str()` | Convert to string | `str(42)` → "42" |
| `sum()` | Sum of items | `sum([1, 2, 3])` → 6 |
| `max()` | Maximum value | `max(1, 5, 3)` → 5 |
| `min()` | Minimum value | `min(1, 5, 3)` → 1 |
| `abs()` | Absolute value | `abs(-5)` → 5 |
| `round()` | Round number | `round(3.7)` → 4 |
| `sorted()` | Sort collection | `sorted([3,1,2])` → [1,2,3] |
| `enumerate()` | Index + value | See below |
| `zip()` | Combine iterables | See below |

#### 2. Methods

**Methods** are functions that belong to objects. They're called using dot notation.

**String Methods:**
```python
text = "hello"
text.upper()          # "HELLO"
text.capitalize()     # "Hello"
text.count("l")       # 2
text.replace("l", "L") # "heLLo"
```

**List Methods:**
```python
numbers = [1, 2, 3]
numbers.append(4)     # Add element
numbers.extend([5, 6]) # Add multiple elements
numbers.pop()         # Remove and return last
numbers.sort()        # Sort in place
numbers.reverse()     # Reverse in place
```

**Set Methods:**
```python
my_set = {1, 2, 3}
my_set.add(4)         # Add element
my_set.remove(2)      # Remove element
my_set.union({3, 4, 5}) # Set union
```

**Tuple Methods:**
```python
my_tuple = (1, 2, 3, 2)
my_tuple.count(2)     # Count occurrences: 2
my_tuple.index(3)     # Find index: 2
```

**Difference between Functions and Methods:**
```python
# Function - standalone
len([1, 2, 3])        # Function call

# Method - belongs to object
[1, 2, 3].append(4)   # Method call on list object
"hello".upper()       # Method call on string object
```

#### 3. User-Defined Functions

**User-defined functions** are functions we create ourselves using the `def` keyword.

**Basic Syntax:**
```python
def function_name():
    # Function body
    # Code to execute
    pass
```

**Simple Example:**
```python
# Define a function
def greet():
    print("Hello, World!")

# Call the function
greet()  # Output: Hello, World!
```

**Why Create Functions?**
```python
# Without function - repetitive
print("Welcome!")
print("Enjoy your stay!")
print("Goodbye!")

print("Welcome!")
print("Enjoy your stay!")
print("Goodbye!")

# With function - reusable
def welcome_message():
    print("Welcome!")
    print("Enjoy your stay!")
    print("Goodbye!")

welcome_message()  # First time
welcome_message()  # Second time - same code
```

### Function Parameters and Arguments

#### Functions with Parameters

**Parameters** are variables defined in the function. **Arguments** are values passed when calling.

```python
# Function with one parameter
def greet(name):
    print(f"Hello, {name}!")

# Call with argument
greet("Alice")    # Output: Hello, Alice!
greet("Bob")      # Output: Hello, Bob!
```

**Multiple Parameters:**
```python
def add_numbers(a, b):
    result = a + b
    print(f"{a} + {b} = {result}")

add_numbers(5, 3)    # Output: 5 + 3 = 8
add_numbers(10, 20)  # Output: 10 + 20 = 30
```

**Parameter vs Argument:**
```python
def greet(name):      # 'name' is a parameter
    print(f"Hello, {name}")

greet("Alice")        # "Alice" is an argument
```

#### Default Parameters

**Default parameters** have default values if no argument is provided.

```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet("Alice")   # Output: Hello, Alice!
greet()          # Output: Hello, Guest!  (uses default)
```

**Multiple Default Parameters:**
```python
def create_profile(name, age=0, city="Unknown"):
    print(f"Name: {name}")
    print(f"Age: {age}")
    print(f"City: {city}")

create_profile("Alice")
# Output:
# Name: Alice
# Age: 0
# City: Unknown

create_profile("Bob", 25)
# Output:
# Name: Bob
# Age: 25
# City: Unknown

create_profile("Charlie", 30, "NYC")
# Output:
# Name: Charlie
# Age: 30
# City: NYC
```

#### Keyword Arguments

**Keyword arguments** specify which parameter receives which value.

```python
def describe_pet(animal, name, age):
    print(f"I have a {animal} named {name} who is {age} years old.")

# Positional arguments (order matters)
describe_pet("dog", "Buddy", 3)

# Keyword arguments (order doesn't matter)
describe_pet(name="Buddy", age=3, animal="dog")
describe_pet(age=3, animal="dog", name="Buddy")

# Mix positional and keyword
describe_pet("dog", name="Buddy", age=3)
```

### Return Values

**Return statement** sends a value back to the caller.

```python
# Function without return (returns None)
def print_sum(a, b):
    print(a + b)

result = print_sum(5, 3)  # Prints: 8
print(result)             # Prints: None

# Function with return
def calculate_sum(a, b):
    return a + b

result = calculate_sum(5, 3)
print(result)             # Prints: 8
```

**Returning Multiple Values:**
```python
def get_min_max(numbers):
    minimum = min(numbers)
    maximum = max(numbers)
    return minimum, maximum  # Returns tuple

numbers = [3, 1, 4, 1, 5, 9, 2]
min_val, max_val = get_min_max(numbers)
print(f"Min: {min_val}, Max: {max_val}")  # Min: 1, Max: 9
```

**Return vs Print:**
```python
# Print - displays but doesn't return value
def show_result(x):
    print(x * 2)

a = show_result(5)  # Prints: 10
print(a)            # Prints: None

# Return - sends value back
def calculate_result(x):
    return x * 2

b = calculate_result(5)  # No output
print(b)                 # Prints: 10
```

### Function Examples

#### Example 1: Simple Calculation
```python
def calculate_area(length, width):
    area = length * width
    return area

result = calculate_area(5, 10)
print(f"Area: {result}")  # Area: 50
```

#### Example 2: String Processing
```python
def make_title(text):
    return text.title()

title = make_title("hello world")
print(title)  # Hello World
```

#### Example 3: List Processing
```python
def get_evens(numbers):
    evens = []
    for num in numbers:
        if num % 2 == 0:
            evens.append(num)
    return evens

result = get_evens([1, 2, 3, 4, 5, 6])
print(result)  # [2, 4, 6]
```

#### Example 4: Validation
```python
def is_valid_age(age):
    if age >= 0 and age <= 120:
        return True
    else:
        return False

# Simpler version
def is_valid_age_v2(age):
    return 0 <= age <= 120

print(is_valid_age(25))    # True
print(is_valid_age(-5))    # False
print(is_valid_age_v2(150)) # False
```

### Function Scope

**Scope** determines where variables are accessible.

```python
# Global variable
global_var = "I'm global"

def my_function():
    # Local variable
    local_var = "I'm local"
    print(global_var)   # Can access global
    print(local_var)    # Can access local

my_function()
print(global_var)       # Can access global
# print(local_var)      # Error! Can't access local outside function
```

**Variable Shadowing:**
```python
x = 10  # Global x

def test():
    x = 5  # Local x (shadows global)
    print(f"Inside function: {x}")  # 5

test()
print(f"Outside function: {x}")  # 10 (global unchanged)
```

### Using Functions with Data Structures

#### With Lists:
```python
def sum_list(numbers):
    total = 0
    for num in numbers:
        total += num
    return total

result = sum_list([1, 2, 3, 4, 5])
print(result)  # 15
```

#### With Sets:
```python
def find_common(set1, set2):
    return set1 & set2

common = find_common({1, 2, 3}, {2, 3, 4})
print(common)  # {2, 3}
```

#### With Tuples:
```python
def get_coordinates():
    x = 10
    y = 20
    return (x, y)  # Return tuple

coords = get_coordinates()
print(coords)  # (10, 20)

# Unpacking
x, y = get_coordinates()
print(f"x: {x}, y: {y}")  # x: 10, y: 20
```

### Practical Function Examples

#### Example 1: Temperature Converter
```python
def celsius_to_fahrenheit(celsius):
    fahrenheit = (celsius * 9/5) + 32
    return fahrenheit

temp_c = 25
temp_f = celsius_to_fahrenheit(temp_c)
print(f"{temp_c}°C = {temp_f}°F")  # 25°C = 77.0°F
```

#### Example 2: Grade Calculator
```python
def calculate_grade(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    elif score >= 60:
        return "D"
    else:
        return "F"

grade = calculate_grade(85)
print(f"Grade: {grade}")  # Grade: B
```

#### Example 3: List Statistics
```python
def get_statistics(numbers):
    if len(numbers) == 0:
        return None
    
    total = sum(numbers)
    count = len(numbers)
    average = total / count
    minimum = min(numbers)
    maximum = max(numbers)
    
    return (total, average, minimum, maximum)

data = [10, 20, 30, 40, 50]
stats = get_statistics(data)
if stats:
    total, avg, min_val, max_val = stats
    print(f"Total: {total}")
    print(f"Average: {avg}")
    print(f"Min: {min_val}")
    print(f"Max: {max_val}")
```

### Best Practices for Functions

**DO:**
```python
# Use descriptive names
def calculate_total_price(price, quantity):
    return price * quantity

# Keep functions focused on one task
def is_even(number):
    return number % 2 == 0

# Use return to send values back
def double(x):
    return x * 2

# Add docstrings (documentation)
def greet(name):
    """Print a greeting message for the given name."""
    print(f"Hello, {name}!")
```

**DON'T:**
```python
# Don't use unclear names
def f(x, y):  # What does f do?
    return x + y

# Don't make functions too long or complex
# (Keep them simple and focused)

# Don't rely only on print (use return)
def add(a, b):
    print(a + b)  # Can't use result elsewhere
# Better: return a + b
```

### Common Built-in Functions - Detailed

#### enumerate() - Get Index and Value
```python
fruits = ["apple", "banana", "cherry"]

# Without enumerate
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# With enumerate (better!)
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Output:
# 0: apple
# 1: banana
# 2: cherry

# Start index from 1
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}: {fruit}")
```

#### zip() - Combine Multiple Iterables
```python
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

# Combine three lists
for name, age, city in zip(names, ages, cities):
    print(f"{name} is {age} years old and lives in {city}")

# Output:
# Alice is 25 years old and lives in NYC
# Bob is 30 years old and lives in LA
# Charlie is 35 years old and lives in Chicago

# Create tuples from lists
combined = list(zip(names, ages))
print(combined)  # [('Alice', 25), ('Bob', 30), ('Charlie', 35)]
```

#### all() and any()
```python
# all() - True if all elements are True
numbers = [2, 4, 6, 8]
print(all(n % 2 == 0 for n in numbers))  # True (all even)

numbers = [2, 4, 5, 8]
print(all(n % 2 == 0 for n in numbers))  # False (5 is odd)

# any() - True if any element is True
numbers = [1, 3, 5, 7]
print(any(n % 2 == 0 for n in numbers))  # False (no evens)

numbers = [1, 3, 4, 7]
print(any(n % 2 == 0 for n in numbers))  # True (4 is even)
```

---

## Comprehensions

### What are Comprehensions?

**Comprehensions** provide a concise way to create lists, sets, and tuples from existing iterables using a single line of code.

**Benefits:**
- More readable than loops
- Faster execution
- More "Pythonic" style

### List Comprehension

#### Basic Syntax
```python
# Traditional approach with loop
squares = []
for i in range(5):
    squares.append(i ** 2)
print(squares)  # [0, 1, 4, 9, 16]

# List comprehension
squares = [i ** 2 for i in range(5)]
print(squares)  # [0, 1, 4, 9, 16]
```

**General Syntax:**
```python
[expression for item in iterable]
```

#### Basic Examples
```python
# Square numbers
squares = [x ** 2 for x in range(10)]
print(squares)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Convert to uppercase
words = ["hello", "world", "python"]
upper = [word.upper() for word in words]
print(upper)  # ["HELLO", "WORLD", "PYTHON"]

# Get lengths
words = ["hi", "hello", "hey"]
lengths = [len(word) for word in words]
print(lengths)  # [2, 5, 3]

# Double each number
numbers = [1, 2, 3, 4, 5]
doubled = [n * 2 for n in numbers]
print(doubled)  # [2, 4, 6, 8, 10]
```

### List Comprehension with `if` (Filtering)

**Syntax:**
```python
[expression for item in iterable if condition]
```

#### Examples
```python
# Even numbers only
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = [n for n in numbers if n % 2 == 0]
print(evens)  # [2, 4, 6, 8, 10]

# Odd numbers only
odds = [n for n in numbers if n % 2 != 0]
print(odds)  # [1, 3, 5, 7, 9]

# Positive numbers only
numbers = [-2, -1, 0, 1, 2, 3]
positive = [n for n in numbers if n > 0]
print(positive)  # [1, 2, 3]

# Words longer than 3 characters
words = ["hi", "hello", "hey", "python"]
long_words = [word for word in words if len(word) > 3]
print(long_words)  # ["hello", "python"]

# Squares of even numbers
squares_of_evens = [n ** 2 for n in range(10) if n % 2 == 0]
print(squares_of_evens)  # [0, 4, 16, 36, 64]
```

### List Comprehension with `if-else` (Conditional Expression)

**Syntax:**
```python
[expression_if_true if condition else expression_if_false for item in iterable]
```

**Note:** `if-else` comes BEFORE `for` (different from filtering!)

#### Examples
```python
# Label numbers as even or odd
numbers = [1, 2, 3, 4, 5]
labels = ["even" if n % 2 == 0 else "odd" for n in numbers]
print(labels)  # ["odd", "even", "odd", "even", "odd"]

# Replace negative with 0, keep positive
numbers = [-2, -1, 0, 1, 2]
non_negative = [n if n >= 0 else 0 for n in numbers]
print(non_negative)  # [0, 0, 0, 1, 2]

# Double evens, triple odds
numbers = [1, 2, 3, 4, 5]
result = [n * 2 if n % 2 == 0 else n * 3 for n in numbers]
print(result)  # [3, 4, 9, 8, 15]

# Absolute values
numbers = [-5, -3, 0, 2, 4]
absolute = [n if n >= 0 else -n for n in numbers]
print(absolute)  # [5, 3, 0, 2, 4]

# Categorize scores
scores = [85, 92, 78, 95, 88]
grades = ["A" if s >= 90 else "B" if s >= 80 else "C" for s in scores]
print(grades)  # ["B", "A", "C", "A", "B"]
```

### Difference: `if` vs `if-else` in Comprehensions

```python
numbers = [1, 2, 3, 4, 5, 6]

# Using if (filtering - removes items)
evens = [n for n in numbers if n % 2 == 0]
print(evens)  # [2, 4, 6] - Only 3 items

# Using if-else (transformation - keeps all items)
labels = ["even" if n % 2 == 0 else "odd" for n in numbers]
print(labels)  # ["odd", "even", "odd", "even", "odd", "even"] - All 6 items
```

### Nested List Comprehension

```python
# Create 2D matrix
matrix = [[i * j for j in range(3)] for i in range(3)]
print(matrix)
# [[0, 0, 0],
#  [0, 1, 2],
#  [0, 2, 4]]

# Flatten a 2D list
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat = [num for row in matrix for num in row]
print(flat)  # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# Pairs from two lists
list1 = [1, 2, 3]
list2 = ['a', 'b']
pairs = [(x, y) for x in list1 for y in list2]
print(pairs)  # [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b'), (3, 'a'), (3, 'b')]
```

### Set Comprehension

**Syntax:** Same as list comprehension but with `{}`

```python
# Basic set comprehension
numbers = [1, 2, 2, 3, 3, 3, 4]
unique_squares = {n ** 2 for n in numbers}
print(unique_squares)  # {1, 4, 9, 16} - duplicates removed

# With filtering
numbers = range(10)
even_squares = {n ** 2 for n in numbers if n % 2 == 0}
print(even_squares)  # {0, 64, 4, 36, 16}

# Characters in a string (unique)
text = "hello world"
unique_chars = {char for char in text if char != ' '}
print(unique_chars)  # {'h', 'e', 'l', 'o', 'w', 'r', 'd'}

# First letter of each word (unique)
words = ["apple", "banana", "apricot", "blueberry"]
first_letters = {word[0] for word in words}
print(first_letters)  # {'a', 'b'}
```

### Tuple Comprehension... or Not?

**There is NO tuple comprehension syntax!**

```python
# This creates a generator, not a tuple
gen = (x ** 2 for x in range(5))
print(type(gen))  # <class 'generator'>

# To create tuple, wrap generator in tuple()
squares_tuple = tuple(x ** 2 for x in range(5))
print(squares_tuple)  # (0, 1, 4, 9, 16)
print(type(squares_tuple))  # <class 'tuple'>

# Or convert list comprehension to tuple
squares_tuple = tuple([x ** 2 for x in range(5)])
print(squares_tuple)  # (0, 1, 4, 9, 16)
```

### Practical Comprehension Examples

#### Example 1: Data Transformation
```python
# Convert temperatures from Celsius to Fahrenheit
celsius = [0, 10, 20, 30, 40]
fahrenheit = [c * 9/5 + 32 for c in celsius]
print(fahrenheit)  # [32.0, 50.0, 68.0, 86.0, 104.0]
```

#### Example 2: String Processing
```python
# Extract numbers from strings
data = ["123", "abc", "456", "def", "789"]
numbers = [int(s) for s in data if s.isdigit()]
print(numbers)  # [123, 456, 789]

# Clean and lowercase words
words = ["  Hello  ", "WORLD", "  Python  "]
cleaned = [word.strip().lower() for word in words]
print(cleaned)  # ["hello", "world", "python"]
```

#### Example 3: Filtering Data
```python
# Get passing scores
scores = [45, 78, 92, 34, 88, 56, 95]
passing = [s for s in scores if s >= 60]
print(passing)  # [78, 92, 88, 95]

# Extract vowels
text = "Hello World"
vowels = [char for char in text.lower() if char in "aeiou"]
print(vowels)  # ['e', 'o', 'o']
```

#### Example 4: Creating Ranges
```python
# Multiple of 5 from 0 to 50
multiples = [i for i in range(51) if i % 5 == 0]
print(multiples)  # [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50]

# Or more directly
multiples = [i * 5 for i in range(11)]
print(multiples)  # [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
```

#### Example 5: Combining Operations
```python
# Square even numbers, cube odd numbers
numbers = range(1, 11)
result = [n ** 2 if n % 2 == 0 else n ** 3 for n in numbers]
print(result)  # [1, 4, 27, 16, 125, 36, 343, 64, 729, 100]
```

### When to Use Comprehensions

**Use comprehensions when:**
- Transformation is simple (one line)
- Creating new collection from existing one
- Filtering based on simple condition
- Code is more readable than loop

**Use traditional loops when:**
- Logic is complex (multiple lines needed)
- Need multiple operations per item
- Debugging is difficult
- Readability suffers

```python
# Good use of comprehension (simple, clear)
squares = [x ** 2 for x in range(10)]

# Bad use of comprehension (too complex, hard to read)
# Don't do this!
result = [x ** 2 if x % 2 == 0 else x ** 3 if x % 3 == 0 else x * 2 if x % 5 == 0 else x for x in range(100)]

# Better: Use a loop for complex logic
result = []
for x in range(100):
    if x % 2 == 0:
        result.append(x ** 2)
    elif x % 3 == 0:
        result.append(x ** 3)
    elif x % 5 == 0:
        result.append(x * 2)
    else:
        result.append(x)
```

---

## Summary

### Key Concepts Learned

**Lists:**
- Ordered, mutable, allow duplicates
- Fast index access O(1), slow search O(n)
- Many methods: append, extend, insert, remove, pop, etc.
- Use when order matters or need modification

**Sets:**
- Unordered, mutable, unique elements only
- Fast membership test O(1)
- Set operations: union, intersection, difference
- Use when uniqueness needed or fast lookup required

**Tuples:**
- Ordered, immutable, allow duplicates
- Only 2 methods: count, index
- Hashable (can be dict keys, set elements)
- Use when data shouldn't change

**Hashability:**
- Immutable objects are hashable
- Enables fast lookups in sets/dicts
- Required for dict keys and set elements

**Storage:**
- Lists: array of references (contiguous memory)
- Sets: hash table (fast lookup)
- Tuples: compact array (more efficient than lists)

**References:**
- Variables store references, not objects
- `is` checks identity (same object)
- `==` checks equality (same content)

**Comprehensions:**
- Concise way to create lists/sets/tuples
- List: `[expr for item in iterable]`
- With if: `[expr for item in iterable if condition]`
- With if-else: `[expr_if if cond else expr_else for item in iterable]`
- Set: Same with `{}`
- Tuple: `tuple(expr for item in iterable)`

### Comparison Table

| Feature | List | Set | Tuple |
|---------|------|-----|-------|
| **Ordered** | Yes | No | Yes |
| **Mutable** | Yes | Yes | No |
| **Duplicates** | Yes | No | Yes |
| **Indexing** | Yes | No | Yes |
| **Hashable** | No | No | Yes* |
| **Syntax** | `[1, 2]` | `{1, 2}` | `(1, 2)` |
| **Use Case** | General purpose | Unique items | Fixed data |

*Tuples hashable only if all elements hashable

### Practice Tips

1. **Choose the right data structure** based on requirements
2. **Use sets for uniqueness** and fast lookup
3. **Use tuples for immutable** data
4. **Understand hashability** for dict keys and sets
5. **Master comprehensions** for concise code
6. **Remember `is` vs `==`** for comparisons
7. **Be aware of references** when copying

### Common Patterns

```python
# Remove duplicates from list
unique = list(set(my_list))

# Check membership efficiently
if item in my_set:  # Fast!

# Protect data with tuple
config = (host, port, db)  # Can't be modified

# Transform list concisely
doubled = [x * 2 for x in numbers]

# Filter and transform
evens_squared = [x ** 2 for x in numbers if x % 2 == 0]
```

You now understand the core data structures in Python and how to use them effectively!
