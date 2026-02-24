# Week 3: Python Fundamentals - Loops

## Table of Contents
1. [Introduction to Loops](#introduction-to-loops)
2. [While Loop](#while-loop)
3. [For Loop](#for-loop)
4. [Range Function](#range-function)
5. [Loop Control Statements](#loop-control-statements)
6. [Nested Loops](#nested-loops)
7. [While vs For: When to Use Which](#while-vs-for-when-to-use-which)

---

## Introduction to Loops

### What are Loops?

**Loops** allow you to execute a block of code multiple times without writing it repeatedly. They are essential for:
- Repeating tasks
- Processing collections (lists, strings)
- Implementing algorithms
- Automating repetitive operations

**Two Types of Loops in Python:**
1. **while loop** - Repeats while a condition is True
2. **for loop** - Iterates over a sequence

### Why Use Loops?

**Without loops (repetitive code):**
```python
print("Hello")
print("Hello")
print("Hello")
print("Hello")
print("Hello")
```

**With loops (elegant code):**
```python
for i in range(5):
    print("Hello")
```

---

## While Loop

### Basic Structure

A **while loop** repeats a block of code as long as a condition remains True.

**Syntax:**
```python
while condition:
    # Code to execute
    # This runs repeatedly while condition is True
```

**Three Essential Components:**
1. **Initialization** - Set up variables before the loop
2. **Condition** - Test that determines if loop continues
3. **Update/Step** - Change that moves toward ending the loop

### Basic Example

```python
# Count from 1 to 5
counter = 1                    # 1. Initialization

while counter <= 5:            # 2. Condition
    print(counter)             # Code to execute
    counter += 1               # 3. Update/Step

# Output:
# 1
# 2
# 3
# 4
# 5
```

**How it works:**
1. `counter = 1` - Initialize
2. Check: Is `counter <= 5`? Yes (1 <= 5)
3. Execute: Print 1
4. Update: `counter` becomes 2
5. Check: Is `counter <= 5`? Yes (2 <= 5)
6. Execute: Print 2
7. Update: `counter` becomes 3
8. ... continues until counter is 6
9. Check: Is `counter <= 5`? No (6 <= 5 is False)
10. Exit loop

### Components Breakdown

#### 1. Initialization
Set up variables before entering the loop.

```python
# Example: Sum numbers 1 to 10
total = 0          # Initialize sum
number = 1         # Initialize counter

while number <= 10:
    total += number
    number += 1

print("Sum:", total)  # 55
```

#### 2. Condition (Stopping Condition)
The test that determines if the loop continues.

```python
# Different stopping conditions

# Count up
i = 1
while i <= 10:      # Stop when i exceeds 10
    print(i)
    i += 1

# Count down
i = 10
while i > 0:        # Stop when i reaches 0
    print(i)
    i -= 1

# Until specific value
password = ""
while password != "secret":
    password = input("Enter password: ")
print("Access granted!")
```

#### 3. Update/Step
The change that eventually makes the condition False.

```python
# Different step types

# Increment by 1
i = 0
while i < 5:
    print(i)
    i += 1        # Step: add 1

# Increment by 2 (even numbers)
i = 0
while i < 10:
    print(i)
    i += 2        # Step: add 2

# Decrement
i = 10
while i >= 0:
    print(i)
    i -= 1        # Step: subtract 1

# Multiply
i = 1
while i < 100:
    print(i)
    i *= 2        # Step: double each time (1, 2, 4, 8, 16, 32, 64)
```

### Different Styles of While Loops

#### Style 1: Counter-Based Loop
```python
# Print numbers 1 to 5
count = 1
while count <= 5:
    print(count)
    count += 1
```

#### Style 2: Sentinel Value (Run Until Specific Input)
```python
# Run until user types 'quit'
command = ""
while command != "quit":
    command = input("Enter command (or 'quit' to exit): ")
    if command != "quit":
        print(f"You entered: {command}")
```

#### Style 3: Boolean Flag
```python
# Run until user guesses correct number
import random

secret = random.randint(1, 10)
guessed = False

while not guessed:
    guess = int(input("Guess the number (1-10): "))
    if guess == secret:
        print("Correct!")
        guessed = True
    else:
        print("Wrong, try again!")
```

#### Style 4: While True (Infinite Loop with Break)
```python
# Run until break is encountered
while True:
    user_input = input("Enter a number (or 'done' to finish): ")
    
    if user_input == "done":
        break
    
    number = int(user_input)
    print(f"You entered: {number}")

print("Loop finished!")
```

**When to use `while True`:**
- When you don't know in advance how many iterations you need
- When the exit condition is complex
- For menu-driven programs

```python
# Menu system example
while True:
    print("\n=== MENU ===")
    print("1. Start")
    print("2. Settings")
    print("3. Exit")
    
    choice = input("Choose option: ")
    
    if choice == "1":
        print("Starting...")
    elif choice == "2":
        print("Opening settings...")
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid option")
```

### Common While Loop Patterns

#### Pattern 1: Counting
```python
# Count from start to end
start = 1
end = 10
current = start

while current <= end:
    print(current)
    current += 1
```

#### Pattern 2: Accumulation
```python
# Sum all numbers from 1 to 100
total = 0
number = 1

while number <= 100:
    total += number
    number += 1

print("Sum:", total)  # 5050
```

#### Pattern 3: Input Validation
```python
# Keep asking until valid input
age = -1

while age < 0 or age > 120:
    age = int(input("Enter your age (0-120): "))
    if age < 0 or age > 120:
        print("Invalid age, try again!")

print(f"Your age is {age}")
```

#### Pattern 4: Search/Find
```python
# Find first vowel in a string
text = "Python"
index = 0
found = False

while index < len(text) and not found:
    if text[index] in "aeiouAEIOU":
        print(f"First vowel is '{text[index]}' at position {index}")
        found = True
    index += 1

if not found:
    print("No vowels found")
```

### Practical Examples

#### Example 1: Factorial Calculation
```python
# Calculate n! (n factorial)
# 5! = 5 × 4 × 3 × 2 × 1 = 120

n = int(input("Enter a number: "))
factorial = 1
counter = 1

while counter <= n:
    factorial *= counter
    counter += 1

print(f"{n}! = {factorial}")

# Example with n = 5:
# Step 1: factorial = 1 * 1 = 1, counter = 2
# Step 2: factorial = 1 * 2 = 2, counter = 3
# Step 3: factorial = 2 * 3 = 6, counter = 4
# Step 4: factorial = 6 * 4 = 24, counter = 5
# Step 5: factorial = 24 * 5 = 120, counter = 6
# Stop (counter > n)
```

#### Example 2: Palindrome Checker
```python
# Check if a string reads the same forwards and backwards
text = input("Enter a word: ").lower()
is_palindrome = True
left = 0
right = len(text) - 1

while left < right:
    if text[left] != text[right]:
        is_palindrome = False
        break
    left += 1
    right -= 1

if is_palindrome:
    print(f"{text} is a palindrome!")
else:
    print(f"{text} is not a palindrome")

# Examples:
# "racecar" -> palindrome
# "hello" -> not palindrome
# "madam" -> palindrome
```

#### Example 3: Reverse a Number
```python
# Reverse the digits of a number
number = int(input("Enter a number: "))
reversed_num = 0

while number > 0:
    digit = number % 10           # Get last digit
    reversed_num = reversed_num * 10 + digit
    number = number // 10         # Remove last digit

print("Reversed:", reversed_num)

# Example with 1234:
# Step 1: digit=4, reversed=0*10+4=4, number=123
# Step 2: digit=3, reversed=4*10+3=43, number=12
# Step 3: digit=2, reversed=43*10+2=432, number=1
# Step 4: digit=1, reversed=432*10+1=4321, number=0
# Result: 4321
```

#### Example 4: Guess the Number Game
```python
import random

secret = random.randint(1, 100)
attempts = 0
max_attempts = 7

print("Guess the number between 1 and 100!")
print(f"You have {max_attempts} attempts.")

while attempts < max_attempts:
    guess = int(input(f"\nAttempt {attempts + 1}: "))
    attempts += 1
    
    if guess == secret:
        print(f"Correct! You won in {attempts} attempts!")
        break
    elif guess < secret:
        print("Too low!")
    else:
        print("Too high!")
    
    if attempts == max_attempts:
        print(f"\nGame Over! The number was {secret}")
```

### Infinite Loops (Common Mistake)

**Warning:** If the condition never becomes False, the loop runs forever!

```python
# INFINITE LOOP - DON'T RUN THIS!
counter = 1
while counter <= 5:
    print(counter)
    # Missing: counter += 1
    # Loop never ends because counter stays 1

# How to fix:
counter = 1
while counter <= 5:
    print(counter)
    counter += 1  # This is essential!
```

**Common causes of infinite loops:**
1. Forgetting to update the loop variable
2. Updating in the wrong direction
3. Condition that can never be False

```python
# Wrong direction
i = 1
while i < 10:
    print(i)
    i -= 1  # Decreasing instead of increasing - goes to -infinity!

# Correct:
i = 1
while i < 10:
    print(i)
    i += 1
```

---

## For Loop

### Basic Structure

A **for loop** iterates over a sequence (list, string, range, etc.).

**Syntax:**
```python
for variable in sequence:
    # Code to execute for each item
```

**Components:**
1. **Loop variable** - Takes each value from the sequence
2. **Sequence** - Collection to iterate over
3. **Body** - Code that executes for each item

### Iterating Over Different Sequences

#### 1. Iterating Over a List
```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)

# Output:
# apple
# banana
# cherry
```

#### 2. Iterating Over a String
```python
word = "Python"

for letter in word:
    print(letter)

# Output:
# P
# y
# t
# h
# o
# n
```

#### 3. Iterating Over a Range (Numbers)
```python
# Print numbers 0 to 4
for i in range(5):
    print(i)

# Output:
# 0
# 1
# 2
# 3
# 4
```

### For Loop with Index

#### Method 1: Using range() and len()
```python
fruits = ["apple", "banana", "cherry"]

for i in range(len(fruits)):
    print(f"Index {i}: {fruits[i]}")

# Output:
# Index 0: apple
# Index 1: banana
# Index 2: cherry
```

#### Method 2: Using enumerate()
```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"Index {index}: {fruit}")

# Output:
# Index 0: apple
# Index 1: banana
# Index 2: cherry
```

---

## Range Function

The `range()` function generates a sequence of numbers.

### Three Forms of range()

#### 1. range(stop)
Generates numbers from 0 to stop-1.

```python
for i in range(5):
    print(i)

# Output: 0, 1, 2, 3, 4
```

#### 2. range(start, stop)
Generates numbers from start to stop-1.

```python
for i in range(2, 6):
    print(i)

# Output: 2, 3, 4, 5
```

#### 3. range(start, stop, step)
Generates numbers from start to stop-1, incrementing by step.

```python
# Count by 2s
for i in range(0, 10, 2):
    print(i)

# Output: 0, 2, 4, 6, 8

# Count backwards
for i in range(10, 0, -1):
    print(i)

# Output: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

### Range Examples

```python
# Even numbers from 0 to 20
for num in range(0, 21, 2):
    print(num)

# Odd numbers from 1 to 19
for num in range(1, 20, 2):
    print(num)

# Countdown from 10 to 1
for num in range(10, 0, -1):
    print(num)
print("Blastoff!")

# Every 5th number
for num in range(0, 50, 5):
    print(num)  # 0, 5, 10, 15, 20, 25, 30, 35, 40, 45
```

### Converting range() to List

```python
# range() is not a list, but you can convert it
numbers = list(range(1, 6))
print(numbers)  # [1, 2, 3, 4, 5]

# This is useful for creating lists
evens = list(range(0, 20, 2))
print(evens)  # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
```

---

## Loop Control Statements

Loop control statements change the normal flow of loop execution.

### 1. break - Exit the Loop

The `break` statement immediately exits the loop, regardless of the condition.

**Syntax:**
```python
for/while ...:
    if condition:
        break
    # This code is skipped after break
```

**Example 1: Stop at First Match**
```python
# Find first negative number
numbers = [5, 3, -2, 8, -1, 4]

for num in numbers:
    if num < 0:
        print(f"First negative: {num}")
        break
# Output: First negative: -2
```

**Example 2: Exit on User Input**
```python
# Run until user types 'quit'
while True:
    command = input("Enter command: ")
    if command == "quit":
        break
    print(f"Processing: {command}")
print("Program ended")
```

**Example 3: Search in String**
```python
# Find if a character exists
text = "Python Programming"
search_char = "g"
found = False

for char in text:
    if char == search_char:
        found = True
        break

if found:
    print(f"'{search_char}' found!")
else:
    print(f"'{search_char}' not found")
```

### 2. continue - Skip to Next Iteration

The `continue` statement skips the rest of the current iteration and moves to the next one.

**Syntax:**
```python
for/while ...:
    if condition:
        continue
    # This code is skipped when continue executes
```

**Example 1: Skip Specific Values**
```python
# Print numbers 1-10 except 5
for i in range(1, 11):
    if i == 5:
        continue  # Skip when i is 5
    print(i)

# Output: 1, 2, 3, 4, 6, 7, 8, 9, 10
```

**Example 2: Skip Even Numbers**
```python
# Print only odd numbers
for i in range(1, 11):
    if i % 2 == 0:
        continue  # Skip even numbers
    print(i)

# Output: 1, 3, 5, 7, 9
```

**Example 3: Skip Vowels**
```python
# Print only consonants
word = "Python"
for letter in word:
    if letter.lower() in "aeiou":
        continue
    print(letter)

# Output: P, y, t, h, n
```

### 3. pass - Do Nothing (Placeholder)

The `pass` statement does nothing. It's used as a placeholder for future code.

**Syntax:**
```python
for/while ...:
    if condition:
        pass  # TODO: implement this later
```

**Example 1: Empty Loop Body**
```python
# Placeholder for future implementation
for i in range(5):
    pass  # Will add code later

print("Loop completed")
```

**Example 2: Conditional Placeholder**
```python
# Process some numbers
for num in range(1, 11):
    if num % 2 == 0:
        print(f"{num} is even")
    else:
        pass  # Will handle odd numbers later
```

**Example 3: Multiple Conditions**
```python
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    pass  # Will implement C grade logic later
else:
    pass  # Will implement failing grade logic later
```

### Comparison: break vs continue vs pass

```python
# Demonstrating all three
for i in range(1, 11):
    if i == 3:
        pass  # Do nothing, continue normally
    
    if i == 5:
        continue  # Skip the print for 5
    
    if i == 8:
        break  # Stop the loop at 8
    
    print(i)

# Output: 1, 2, 3, 4, 6, 7
# (5 is skipped by continue, 8+ not printed due to break)
```

### Practical Examples with Loop Control

#### Example 1: Input Validation
```python
# Get valid age
while True:
    age_input = input("Enter your age (0-120): ")
    
    if not age_input.isdigit():
        print("Please enter a number!")
        continue
    
    age = int(age_input)
    
    if age < 0 or age > 120:
        print("Age must be between 0 and 120!")
        continue
    
    break  # Valid input, exit loop

print(f"Your age is {age}")
```

#### Example 2: Prime Number Checker
```python
# Check if number is prime
num = int(input("Enter a number: "))

if num < 2:
    print("Not prime")
else:
    is_prime = True
    for i in range(2, num):
        if num % i == 0:
            is_prime = False
            break  # Found a divisor, no need to continue
    
    if is_prime:
        print(f"{num} is prime")
    else:
        print(f"{num} is not prime")
```

#### Example 3: Password Validator
```python
# Check password requirements
password = input("Enter password: ")
valid = True

# Check length
if len(password) < 8:
    print("Password too short")
    valid = False

# Check for digit
has_digit = False
for char in password:
    if char.isdigit():
        has_digit = True
        break  # Found one, no need to continue

if not has_digit:
    print("Password must contain a digit")
    valid = False

if valid:
    print("Password is valid!")
```

---

## Nested Loops

A **nested loop** is a loop inside another loop.

### Basic Nested Loop Structure

```python
for i in outer_sequence:
    for j in inner_sequence:
        # This code runs for each combination of i and j
```

### Simple Example

```python
# Print multiplication combinations
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} × {j} = {i * j}")

# Output:
# 1 × 1 = 1
# 1 × 2 = 2
# 1 × 3 = 3
# 2 × 1 = 2
# 2 × 2 = 4
# 2 × 3 = 6
# 3 × 1 = 3
# 3 × 2 = 6
# 3 × 3 = 9
```

### How Nested Loops Work

```python
# Execution flow
for i in range(1, 4):       # i = 1, then 2, then 3
    for j in range(1, 3):   # For each i, j goes 1, 2
        print(f"i={i}, j={j}")

# Output:
# i=1, j=1  (outer i=1, inner j=1)
# i=1, j=2  (outer i=1, inner j=2)
# i=2, j=1  (outer i=2, inner j=1)
# i=2, j=2  (outer i=2, inner j=2)
# i=3, j=1  (outer i=3, inner j=1)
# i=3, j=2  (outer i=3, inner j=2)
```

### Nested Loop Examples

#### Example 1: Multiplication Table
```python
# Print multiplication table 1-10
for i in range(1, 11):
    for j in range(1, 11):
        print(f"{i * j:4}", end="")  # :4 for spacing
    print()  # New line after each row

# Output:
#    1   2   3   4   5   6   7   8   9  10
#    2   4   6   8  10  12  14  16  18  20
#    3   6   9  12  15  18  21  24  27  30
# ...
```

#### Example 2: Pattern Printing
```python
# Print triangle pattern
rows = 5
for i in range(1, rows + 1):
    for j in range(i):
        print("*", end="")
    print()

# Output:
# *
# **
# ***
# ****
# *****

# Reverse triangle
for i in range(rows, 0, -1):
    for j in range(i):
        print("*", end="")
    print()

# Output:
# *****
# ****
# ***
# **
# *
```

#### Example 3: Number Pyramid
```python
# Print number pyramid
rows = 5
for i in range(1, rows + 1):
    # Print spaces
    for j in range(rows - i):
        print(" ", end="")
    # Print numbers
    for j in range(i):
        print(j + 1, end="")
    print()

# Output:
#     1
#    12
#   123
#  1234
# 12345
```

#### Example 4: Matrix Operations
```python
# Create and display a 3x3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Display matrix
for row in matrix:
    for element in row:
        print(element, end=" ")
    print()

# Output:
# 1 2 3
# 4 5 6
# 7 8 9

# Sum all elements
total = 0
for row in matrix:
    for element in row:
        total += element
print("Sum:", total)  # 45
```

#### Example 5: Finding Pairs
```python
# Find all pairs that sum to a target
numbers = [1, 2, 3, 4, 5]
target = 6

print(f"Pairs that sum to {target}:")
for i in range(len(numbers)):
    for j in range(i + 1, len(numbers)):
        if numbers[i] + numbers[j] == target:
            print(f"{numbers[i]} + {numbers[j]} = {target}")

# Output:
# 1 + 5 = 6
# 2 + 4 = 6
```

### Nested Loop Control

#### break in Nested Loops
```python
# break only exits the inner loop
for i in range(1, 4):
    for j in range(1, 4):
        if j == 2:
            break  # Exits inner loop only
        print(f"i={i}, j={j}")

# Output:
# i=1, j=1
# i=2, j=1
# i=3, j=1

# To break both loops, use a flag
found = False
for i in range(1, 4):
    for j in range(1, 4):
        if i == 2 and j == 2:
            found = True
            break
    if found:
        break
    print(f"Completed i={i}")
```

#### continue in Nested Loops
```python
# continue skips to next iteration of inner loop
for i in range(1, 4):
    for j in range(1, 4):
        if j == 2:
            continue  # Skip j=2
        print(f"i={i}, j={j}")

# Output:
# i=1, j=1
# i=1, j=3
# i=2, j=1
# i=2, j=3
# i=3, j=1
# i=3, j=3
```

---

## While vs For: When to Use Which

### Converting Between While and For

**Every for loop can be written as a while loop**, but not every while loop can be easily written as a for loop.

#### Example 1: Simple Counting

**For loop:**
```python
for i in range(5):
    print(i)
```

**Equivalent while loop:**
```python
i = 0
while i < 5:
    print(i)
    i += 1
```

#### Example 2: Iterating Over a List

**For loop:**
```python
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

**Equivalent while loop:**
```python
fruits = ["apple", "banana", "cherry"]
i = 0
while i < len(fruits):
    print(fruits[i])
    i += 1
```

#### Example 3: String Iteration

**For loop:**
```python
word = "Python"
for char in word:
    print(char)
```

**Equivalent while loop:**
```python
word = "Python"
i = 0
while i < len(word):
    print(word[i])
    i += 1
```

### When to Use FOR Loop

Use **for loop** when:
1. **You know the number of iterations in advance**
2. **Iterating over a collection** (list, string, range)
3. **Processing each item in a sequence**
4. **Counting within a specific range**

**Ideal FOR loop scenarios:**

| Scenario | Example |
|----------|---------|
| Fixed iterations | `for i in range(10):` |
| List processing | `for item in my_list:` |
| String processing | `for char in text:` |
| Counting with step | `for i in range(0, 100, 5):` |
| Nested iterations | `for i in range(3): for j in range(3):` |

**Examples:**
```python
# 1. Process all items in a list
scores = [85, 90, 78, 92, 88]
for score in scores:
    print(score)

# 2. Repeat action N times
for i in range(5):
    print("Hello")

# 3. Pattern generation
for i in range(1, 6):
    print("*" * i)

# 4. Process string characters
word = "Python"
for char in word:
    print(char.upper())
```

### When to Use WHILE Loop

Use **while loop** when:
1. **You don't know how many iterations needed**
2. **Loop depends on user input**
3. **Continue until a condition is met**
4. **Event-driven loops**

**Ideal WHILE loop scenarios:**

| Scenario | Example |
|----------|---------|
| User input validation | `while input != "quit":` |
| Unknown iterations | `while not found:` |
| Game loops | `while player_alive:` |
| Search operations | `while index < len and not found:` |
| Menu systems | `while True: ... break` |

**Examples:**
```python
# 1. Input validation (unknown iterations)
password = ""
while len(password) < 8:
    password = input("Enter password (min 8 chars): ")

# 2. Game loop
import random
secret = random.randint(1, 10)
guess = 0
while guess != secret:
    guess = int(input("Guess: "))

# 3. Menu system
while True:
    print("1. Play")
    print("2. Quit")
    choice = input("Choose: ")
    if choice == "2":
        break

# 4. Process until condition
number = 1234
while number > 0:
    digit = number % 10
    print(digit)
    number //= 10
```

### Comprehensive Comparison

#### Scenario 1: Fixed Range
```python
# FOR is better (cleaner)
for i in range(10):
    print(i)

# WHILE works but more verbose
i = 0
while i < 10:
    print(i)
    i += 1
```

#### Scenario 2: Unknown Iterations
```python
# FOR doesn't work well
# (You'd need a workaround)

# WHILE is ideal
total = 0
while total < 100:
    total += int(input("Add number: "))
```

#### Scenario 3: List Processing
```python
# FOR is cleaner
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num * 2)

# WHILE is more complex
numbers = [1, 2, 3, 4, 5]
i = 0
while i < len(numbers):
    print(numbers[i] * 2)
    i += 1
```

#### Scenario 4: Conditional Continue
```python
# FOR is fine
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)

# WHILE needs careful update placement
i = 0
while i < 10:
    if i % 2 == 0:
        i += 1
        continue
    print(i)
    i += 1
```

### Decision Flowchart

```
Do you know exact number of iterations?
    ├─ YES → Do you need to iterate over a collection?
    │         ├─ YES → Use FOR loop
    │         └─ NO → Use FOR with range()
    │
    └─ NO → Does loop depend on user input or condition?
              ├─ YES → Use WHILE loop
              └─ NO → Can you determine a maximum?
                        ├─ YES → Use FOR with break
                        └─ NO → Use WHILE loop
```

### Best Practices

1. **Prefer FOR for known iterations**
```python
# Good
for i in range(100):
    print(i)

# Less ideal
i = 0
while i < 100:
    print(i)
    i += 1
```

2. **Use WHILE for conditions**
```python
# Good
while user_input != "quit":
    user_input = input("Command: ")

# Awkward with FOR
# (Would need a different approach)
```

3. **FOR for collections**
```python
# Good
for item in collection:
    process(item)

# Less readable
i = 0
while i < len(collection):
    process(collection[i])
    i += 1
```

---

## Summary

### Key Concepts Learned

**While Loop:**
- Three components: initialization, condition, update
- Different styles: counter-based, sentinel, boolean flag, while True
- Use when iterations unknown
- Be careful of infinite loops

**For Loop:**
- Iterates over sequences
- Cleaner for known iterations
- Works with range(), lists, strings
- Every for can be written as while (but not vice versa)

**Range Function:**
- `range(stop)` - 0 to stop-1
- `range(start, stop)` - start to stop-1
- `range(start, stop, step)` - with custom step

**Loop Control:**
- `break` - Exit loop immediately
- `continue` - Skip to next iteration
- `pass` - Placeholder (do nothing)

**Nested Loops:**
- Loop inside a loop
- Useful for patterns, matrices, combinations
- Control statements affect only innermost loop (unless using flags)

**When to Use Which:**
- FOR: Known iterations, collections, ranges
- WHILE: Unknown iterations, conditions, user input

### Practice Tips

1. **Start simple** - Master basic loops before nesting
2. **Trace execution** - Follow loop variable values step by step
3. **Test edge cases** - Empty collections, single items, zero iterations
4. **Avoid infinite loops** - Always update loop variables
5. **Choose the right loop** - FOR for collections, WHILE for conditions
6. **Use meaningful names** - `for student in students` not `for x in y`

### Common Mistakes to Avoid

```python
# Mistake 1: Infinite loop
i = 0
while i < 10:
    print(i)
    # Forgot: i += 1

# Mistake 2: Off-by-one error
for i in range(10):
    print(i)  # Prints 0-9, not 1-10

# Mistake 3: Modifying list while iterating
numbers = [1, 2, 3, 4]
for num in numbers:
    numbers.remove(num)  # Don't do this!

# Mistake 4: Wrong continue placement with while
i = 0
while i < 10:
    if i == 5:
        continue  # Infinite loop! i never increments
    print(i)
    i += 1
```

---

## Practice Exercises

1. Write a while loop to print all even numbers from 2 to 20
2. Use a for loop to count vowels in a string
3. Create a countdown timer using a while loop
4. Print a multiplication table using nested loops
5. Find the sum of digits in a number using while loop
6. Check if a number is prime using for loop with break
7. Create a pattern using nested for loops
8. Validate password requirements using while True and break
9. Reverse a string using a loop
10. Calculate factorial using both while and for loops

You now have the tools to create complex programs with repetition and iteration. Practice these concepts extensively - loops are fundamental to programming!
