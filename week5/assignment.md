## Exercise 1: Dictionary Basics (10 points)

### Part A: Student Management System (5 points)
Create a dictionary to store information about a student with the following keys:
- `name` (string)
- `age` (integer)
- `major` (string)
- `gpa` (float)
- `courses` (list of course names)

Write code to:
1. Create the dictionary with sample data
2. Print all the keys
3. Print all the values
4. Add a new key `email` with a value
5. Update the `gpa` to a new value
6. Remove the `age` key from the dictionary
7. Print the final dictionary

### Part B: Dictionary Operations (5 points)
Given the following dictionary:
```python
inventory = {
    "apple": 50,
    "banana": 30,
    "orange": 45,
    "mango": 20,
    "grape": 60
}
```

Write code to:
1. Check if "banana" is in the inventory
2. Get the quantity of "mango" using the `get()` method
3. Add a new item "pineapple" with quantity 25
4. Increase the quantity of "apple" by 10
5. Create a new dictionary with only items that have quantity > 40
6. Print the total number of items in inventory (sum of all quantities)

---

## Exercise 2: Advanced Dictionary Operations (10 points)

### Part A: Word Frequency Counter (5 points)
Write a program that:
1. Takes a sentence as input from the user
2. Creates a dictionary that counts how many times each word appears (case-insensitive)
3. Prints the word frequency dictionary
4. Prints the most common word and its count
5. Prints all words that appear more than once

**Example:**
```
Input: "Hello world hello Python world"
Output: {'hello': 2, 'world': 2, 'python': 1}
Most common word: hello (appears 2 times)
Words appearing more than once: hello, world
```

### Part B: Dictionary Manipulation (5 points)
Given two dictionaries:
```python
dict1 = {"a": 100, "b": 200, "c": 300}
dict2 = {"b": 250, "c": 350, "d": 400}
```

Write code to:
1. Merge the two dictionaries (dict2 values should override dict1 for common keys)
2. Create a dictionary with only the common keys and their values from dict1
3. Create a dictionary with keys from dict1 and values from dict2 (for common keys only)
4. Invert dict1 (swap keys and values)
5. Sort dict1 by values in descending order

---

## Exercise 3: Nested Dictionaries (10 points)

### Part A: Student Grade Book (10 points)
Create a nested dictionary to represent a grade book for 3 students. Each student should have:
- Name
- Student ID
- Grades (dictionary with subjects as keys and scores as values)

Example structure:
```python
gradebook = {
    "S001": {
        "name": "Alice",
        "grades": {"Math": 85, "Science": 90, "English": 88}
    },
    # Add 2 more students
}
```

Write functions to:
1. `add_student(gradebook, student_id, name, grades)` - Add a new student
2. `get_student_average(gradebook, student_id)` - Calculate and return a student's average grade
3. `get_top_student(gradebook)` - Return the name of the student with highest average
4. `add_grade(gradebook, student_id, subject, score)` - Add a new subject grade for a student
5. `get_class_average(gradebook, subject)` - Calculate average score for a specific subject across all students

Test all your functions with the gradebook.

---

## Exercise 4: Collections and Data Structures (10 points)

### Part A: Choose the Right Collection (4 points)
For each scenario below, state which collection type (list, tuple, set, or dictionary) would be most appropriate and why:

1. Storing unique visitor IDs to a website
2. Storing RGB color values (red, green, blue)
3. Storing student names and their corresponding grades
4. Storing a shopping list where items can repeat
5. Storing the order of tasks to be completed
6. Storing unique email addresses
7. Storing geographical coordinates (latitude, longitude)
8. Storing product names with their prices

### Part B: Collection Operations (6 points)
Given the following collections:
```python
list1 = [1, 2, 3, 4, 5, 4, 3, 2, 1]
tuple1 = (10, 20, 30, 40, 50)
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}
dict1 = {"a": 1, "b": 2, "c": 3}
```

Write code to:
1. Remove all duplicates from list1 and convert to a sorted list
2. Convert tuple1 to a list, add 60, and convert back to tuple
3. Find the union of set1 and set2
4. Find the intersection of set1 and set2
5. Find elements in set1 but not in set2
6. Create a list of all values from dict1

---

## Exercise 5: Sorting (10 points)

### Part A: Basic Sorting (3 points)
Given the following list:
```python
numbers = [23, 45, 12, 67, 34, 89, 23, 56, 78]
```

Write code to:
1. Sort the list in ascending order (create new list)
2. Sort the list in descending order (modify original)
3. Sort the list by the last digit of each number

### Part B: Sorting Complex Data (7 points)
Given the following list of tuples (name, age, salary):
```python
employees = [
    ("Alice", 30, 70000),
    ("Bob", 25, 50000),
    ("Charlie", 35, 80000),
    ("Diana", 28, 65000),
    ("Eve", 30, 75000)
]
```

Write code to:
1. Sort by age (ascending)
2. Sort by salary (descending)
3. Sort by name (alphabetically)
4. Sort by age first, then by salary (both ascending)
5. Sort by age (descending), then by name (alphabetically)

Now, given this list of dictionaries:
```python
products = [
    {"name": "Laptop", "price": 1200, "rating": 4.5},
    {"name": "Mouse", "price": 25, "rating": 4.2},
    {"name": "Keyboard", "price": 80, "rating": 4.7},
    {"name": "Monitor", "price": 300, "rating": 4.3}
]
```

6. Sort by price (ascending)
7. Sort by rating (descending)

---

## Exercise 6: Matrix Operations (15 points)

### Part A: Matrix Creation (3 points)
Write functions to:
1. `create_zero_matrix(rows, cols)` - Create a matrix filled with zeros
2. `create_identity_matrix(n)` - Create an n×n identity matrix
3. `create_random_matrix(rows, cols, min_val, max_val)` - Create matrix with random integers

### Part B: Matrix Operations (6 points)
Implement the following functions:

1. `print_matrix(matrix)` - Print matrix in a readable format
2. `matrix_add(A, B)` - Add two matrices (return error if dimensions don't match)
3. `matrix_subtract(A, B)` - Subtract matrix B from A
4. `scalar_multiply(matrix, scalar)` - Multiply matrix by a scalar
5. `transpose(matrix)` - Return the transpose of a matrix
6. `get_diagonal(matrix)` - Return the diagonal elements of a square matrix

### Part C: Matrix Multiplication (6 points)
1. Implement `matrix_multiply(A, B)` that:
   - Checks if multiplication is possible
   - Returns appropriate error message if not
   - Performs multiplication if possible
   - Returns the result matrix

2. Test your function with:
   ```python
   A = [[1, 2, 3],
        [4, 5, 6]]
   
   B = [[7, 8],
        [9, 10],
        [11, 12]]
   
   C = [[1, 2],
        [3, 4]]
   ```
   
   Calculate:
   - A × B
   - C × C (C squared)
   - Try B × A and handle the error

3. Create a function `matrix_power(matrix, n)` that calculates matrix^n (matrix multiplied by itself n times)

---

## Exercise 7: Functions (15 points)

### Part A: Basic Functions (5 points)
Write functions for the following:

1. `calculate_bmi(weight, height)` - Calculate BMI (weight in kg, height in meters)
   - Return BMI value
   - Also return category: "Underweight" (<18.5), "Normal" (18.5-24.9), "Overweight" (25-29.9), "Obese" (≥30)

2. `is_prime(n)` - Return True if n is prime, False otherwise

3. `fibonacci_list(n)` - Return a list of first n Fibonacci numbers

4. `count_vowels(text)` - Return count of vowels in the text (case-insensitive)

5. `reverse_words(sentence)` - Reverse the order of words in a sentence
   - Example: "Hello World" → "World Hello"

### Part B: Advanced Functions (5 points)
Write functions with different parameter types:

1. `create_profile(name, age, *hobbies, **details)` - Create a profile dictionary
   ```python
   # Example call:
   profile = create_profile("Alice", 25, "reading", "gaming", city="NYC", job="Engineer")
   # Should return:
   # {"name": "Alice", "age": 25, "hobbies": ["reading", "gaming"], "city": "NYC", "job": "Engineer"}
   ```

2. `calculate_stats(*numbers)` - Return dictionary with min, max, mean, median of numbers

3. `merge_dicts(**dicts)` - Merge multiple dictionaries passed as keyword arguments

### Part C: Recursive Functions (5 points)

1. `factorial(n)` - Calculate factorial recursively

2. `sum_digits(n)` - Sum all digits of a number recursively
   - Example: sum_digits(1234) → 10

3. `reverse_string(s)` - Reverse a string recursively

4. `gcd(a, b)` - Find greatest common divisor using Euclidean algorithm (recursive)

5. `power(base, exp)` - Calculate base^exp recursively (don't use ** operator)

---

## Exercise 8: Scope and Variables (5 points)

### Part A: Scope Questions (2 points)
What will be the output of the following code? Explain why.

```python
x = 10

def outer():
    x = 20
    
    def inner():
        x = 30
        print("Inner:", x)
    
    inner()
    print("Outer:", x)

outer()
print("Global:", x)
```

### Part B: Global and Nonlocal (3 points)

1. Write a function `update_counter()` that uses a global variable `counter` (initialized to 0) and increments it each time the function is called. The function should print the current count.

2. Write a function `create_counter()` that returns an inner function. The inner function should increment and return a count each time it's called. Use `nonlocal`.
   ```python
   # Example usage:
   counter1 = create_counter()
   print(counter1())  # 1
   print(counter1())  # 2
   print(counter1())  # 3
   
   counter2 = create_counter()
   print(counter2())  # 1
   ```

3. Explain the difference between using `global` and `nonlocal` keywords.

---

## Exercise 9: Iterators and Generators (10 points)

### Part A: Understanding Iterators (3 points)

1. Create a custom iterator class `Countdown` that counts down from a given number to 1.
   ```python
   # Example usage:
   for num in Countdown(5):
       print(num)  # Prints: 5, 4, 3, 2, 1
   ```

2. Create a custom iterator class `EvenNumbers` that generates even numbers up to a given limit.

### Part B: Generator Functions (7 points)

Write generator functions for the following:

1. `infinite_sequence()` - Generate infinite sequence of numbers starting from 1

2. `squares(n)` - Generate squares of numbers from 1 to n

3. `fibonacci_gen()` - Generate Fibonacci sequence infinitely

4. `read_file_lines(filename)` - Read a file line by line (generator for memory efficiency)

5. `filter_numbers(numbers, condition)` - Yield only numbers that meet the condition
   ```python
   # Example usage:
   nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   evens = filter_numbers(nums, lambda x: x % 2 == 0)
   for num in evens:
       print(num)  # Prints: 2, 4, 6, 8, 10
   ```

6. Compare memory usage: Create a list comprehension and a generator expression for squares of numbers 1 to 1,000,000. Print the size of each using `sys.getsizeof()`.

7. Write a generator `prime_generator()` that yields prime numbers infinitely. Get the first 20 prime numbers from this generator.

---

## Exercise 10: Lambda, Map, Filter, and Functional Programming (15 points)

### Part A: Lambda Functions (3 points)

Write lambda functions for:
1. Adding two numbers
2. Checking if a number is even
3. Getting the last character of a string
4. Finding the maximum of three numbers
5. Converting Celsius to Fahrenheit: F = C × 9/5 + 32

### Part B: Map (3 points)

Given the following data:
```python
temperatures_celsius = [0, 10, 20, 30, 40, 100]
```

Use `map()` to:
1. Convert all temperatures to Fahrenheit
2. Round all temperatures to nearest integer
3. Create strings in format "X°C"

Given:
```python
words = ["hello", "world", "python", "programming"]
```

Use `map()` to:
4. Convert all words to uppercase
5. Get the length of each word
6. Reverse each word

### Part C: Filter (3 points)

Given:
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

Use `filter()` to:
1. Get all even numbers
2. Get all numbers divisible by 3
3. Get all prime numbers (write a helper function)

Given:
```python
words = ["apple", "banana", "cherry", "date", "elderberry", "fig", "grape"]
```

Use `filter()` to:
4. Get all words with more than 5 letters
5. Get all words that start with a vowel
6. Get all words that contain the letter 'e'

### Part D: Enumerate (2 points)

Given:
```python
fruits = ["apple", "banana", "cherry", "date", "elderberry"]
```

Use `enumerate()` to:
1. Print each fruit with its index (starting from 0)
2. Print each fruit with its position (starting from 1)
3. Create a dictionary with index as key and fruit as value
4. Find all indices where fruit name has more than 5 letters

### Part E: Zip (2 points)

Given:
```python
names = ["Alice", "Bob", "Charlie", "Diana"]
ages = [25, 30, 35, 28]
cities = ["NYC", "LA", "Chicago", "Boston"]
salaries = [70000, 80000, 75000, 85000]
```

Use `zip()` to:
1. Create a list of tuples combining all information
2. Create a dictionary with names as keys and ages as values
3. Print formatted strings: "Name is Age years old and lives in City"
4. Find the person with the highest salary
5. Create a list of dictionaries with keys: name, age, city, salary

### Part F: Combining Functions (2 points)

Given:
```python
data = [
    {"name": "Alice", "age": 25, "salary": 70000},
    {"name": "Bob", "age": 30, "salary": 80000},
    {"name": "Charlie", "age": 35, "salary": 75000},
    {"name": "Diana", "age": 28, "salary": 85000},
    {"name": "Eve", "age": 32, "salary": 72000}
]
```

Write one-line solutions using combinations of map, filter, lambda:
1. Get names of all people older than 30
2. Get salaries of all people, increased by 10%
3. Get average age of people earning more than 75000
4. Create a list of formatted strings: "Name (Age years old)"
5. Find the name of the oldest person

---

## Bonus Exercise: Real-World Application (10 points extra credit)

### Library Management System

Create a complete library management system using dictionaries, functions, and all concepts learned this week.

**Requirements:**

1. **Data Structure**: Create a library system with:
   - Books: dictionary with ISBN as key, containing {title, author, year, available, borrowed_by}
   - Members: dictionary with member_id as key, containing {name, email, borrowed_books[]}

2. **Functions to implement**:
   - `add_book(library, isbn, title, author, year)` - Add a new book
   - `add_member(members, member_id, name, email)` - Add a new member
   - `borrow_book(library, members, isbn, member_id)` - Borrow a book
   - `return_book(library, members, isbn, member_id)` - Return a book
   - `search_books(library, **criteria)` - Search by title, author, or year
   - `get_member_books(members, member_id)` - Get all books borrowed by a member
   - `get_available_books(library)` - List all available books
   - `get_statistics(library, members)` - Return dict with total books, available books, total members, books on loan

3. **Advanced Features**:
   - Use generator to iterate through all books
   - Use map/filter to find specific books
   - Use lambda for sorting books by different criteria
   - Handle errors (book not found, member not found, book already borrowed, etc.)

4. **Test Your System**:
   - Add at least 5 books
   - Add at least 3 members
   - Perform various operations (borrow, return, search)
   - Print statistics

---


*Remember: The goal is to learn and understand the concepts, not just to complete the assignment. Take your time and enjoy coding!*
