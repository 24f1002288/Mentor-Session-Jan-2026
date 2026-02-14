# Week 1 Programming Exercises

## Exercise 1: String Slicer Pro
**Difficulty: Intermediate**

Write a program that takes a sentence as input and performs the following operations using only indexing and slicing:

1. Extract and print the first word (assume words are separated by spaces)
2. Extract and print the last word
3. Extract and print the middle character(s) of the entire sentence
4. Reverse the entire sentence using slicing
5. Extract every second character from the sentence

**Sample Input:**
```
Enter a sentence: Python is amazing
```

**Expected Output:**
```
First word: Python
Last word: amazing
Middle character(s): is
Reversed: gnizama si nohtyP
Every second character: Pto saaig
```

**Hints:**
- Use `find()` or `index()` to locate spaces
- Use negative indexing for last word
- Calculate middle using `len() // 2`
- Use slicing with step: `[::step]`

---

## Exercise 2: The Number Cruncher
**Difficulty: Intermediate**

Take three numbers as input and perform various calculations WITHOUT using conditionals:

1. Calculate the sum, difference, product, and quotient
2. Find the average
3. Calculate the result of: (num1 + num2) × num3 - num1 ÷ num2
4. Determine which operations result in even or odd numbers using modulus
5. Display all results with appropriate labels

**Sample Input:**
```
Enter first number: 10
Enter second number: 4
Enter third number: 5
```

**Expected Output:**
```
Sum: 14
Difference: 6
Product: 40
Quotient: 2.5
Average: 6.333333333333333
Complex calculation: 67.5
Sum is even: True
Product is even: True
```

**Hints:**
- Use `%` to check even/odd: `result % 2 == 0`
- Remember operator precedence
- Use parentheses for clarity

---

## Exercise 3: List Element Extractor
**Difficulty: Intermediate**

Given this list: `data = [23, 45, 67, 12, 89, 34, 56, 78, 90, 11]`

Perform these operations using ONLY indexing (no loops):

1. Print the first three elements
2. Print the last three elements
3. Print elements at even indices (0, 2, 4, ...)
4. Print elements at odd indices (1, 3, 5, ...)
5. Calculate the sum of first element + last element
6. Calculate the product of the middle two elements
7. Create a new list with elements in reverse order using slicing

**Expected Output:**
```
First three: [23, 45, 67]
Last three: [78, 90, 11]
Even indices: [23, 67, 89, 56, 90]
Odd indices: [45, 12, 34, 78, 11]
Sum of first and last: 34
Product of middle two: 3026
Reversed list: [11, 90, 78, 56, 34, 89, 12, 67, 45, 23]
```

**Hints:**
- Use slicing: `list[start:end:step]`
- Negative indices for last elements
- Calculate middle index: `len(data) // 2`

---

## Exercise 4: String Method Mastery
**Difficulty: Intermediate-Hard**

Take a sentence as input and use string methods to:

1. Convert to uppercase, lowercase, and title case
2. Count occurrences of the letter 'a' (case-insensitive)
3. Replace all spaces with hyphens
4. Check if the sentence starts with a vowel and ends with a consonant
5. Find the position of the first space
6. Split into words and count them
7. Remove leading/trailing whitespace if any

**Sample Input:**
```
Enter a sentence:   Advanced Python Programming  
```

**Expected Output:**
```
Uppercase: ADVANCED PYTHON PROGRAMMING
Lowercase: advanced python programming
Title Case: Advanced Python Programming
Count of 'a': 3
With hyphens: Advanced-Python-Programming
Starts with vowel: True
Ends with consonant: True
First space position: 8
Word count: 3
Trimmed: Advanced Python Programming
```

**Hints:**
- Use `.count()` after converting to lowercase
- Use `.startswith()` and `.endswith()`
- Use `.find()` for position
- Use `.split()` and `len()` for word count

---

## Exercise 5: The Calculator Expression Evaluator
**Difficulty: Hard**

Create a program that takes two numbers and evaluates multiple expressions:

1. Calculate: (a + b) × (a - b)
2. Calculate: (a × b) + (a / b)
3. Calculate: a² + b² (use exponentiation operator)
4. Calculate: √(a² + b²) - this is the hypotenuse formula
5. Use relational operators to compare: a > b, a == b, a < b
6. Use logical operators: (a > 0) and (b > 0), (a == 0) or (b == 0)

**Sample Input:**
```
Enter first number: 6
Enter second number: 8
```

**Expected Output:**
```
(a + b) × (a - b) = -28
(a × b) + (a / b) = 48.75
a² + b² = 100
Hypotenuse: 10.0
a > b: False
a == b: False
a < b: True
Both positive: True
Either is zero: False
```

**Hints:**
- Use `**` for exponentiation: `a ** 2`
- Use `** 0.5` for square root
- Parentheses control order of operations

---

## Exercise 6: Price Tag Builder
**Difficulty: Intermediate-Hard**

Create a program that takes a product name, price, and quantity, then builds a formatted price tag:

1. Calculate the total price (price × quantity)
2. Calculate 15% tax on the total
3. Calculate the final price (total + tax)
4. Format the output with currency symbols
5. Create a receipt string with all information
6. Display character count of the product name

**Sample Input:**
```
Enter product name: Wireless Mouse
Enter price per unit: 25.99
Enter quantity: 3
```

**Expected Output:**
```
Product: Wireless Mouse
Unit Price: $25.99
Quantity: 3
Subtotal: $77.97
Tax (15%): $11.70
Total: $89.67
Product name length: 14 characters
```

**Hints:**
- Use string concatenation and type conversion
- Round prices: `round(value, 2)`
- Build receipt using multiple print statements with `sep` and `end`

---

## Exercise 7: Text Statistics Analyzer
**Difficulty: Hard**

Take a paragraph as input and calculate various statistics WITHOUT loops:

1. Count total characters (including spaces)
2. Count characters without spaces
3. Count number of words using split
4. Calculate average word length
5. Count uppercase letters, lowercase letters, digits, and spaces manually for first 10 characters
6. Check if the text contains certain keywords using `in` operator

**Sample Input:**
```
Enter text: Python 3.11 is Amazing and Powerful
```

**Expected Output:**
```
Total characters: 37
Characters (no spaces): 31
Word count: 6
Average word length: 5.17
First 10 chars analysis:
  Character 0 (P): uppercase
  Character 1 (y): lowercase
  Character 2 (t): lowercase
  Character 3 (h): lowercase
  Character 4 (o): lowercase
  Character 5 (n): lowercase
  Character 6 ( ): space
  Character 7 (3): digit
  Character 8 (.): other
  Character 9 (1): digit
Contains 'Python': True
Contains 'Java': False
```

**Hints:**
- Manual checking: use `.isupper()`, `.islower()`, `.isdigit()`, `.isspace()`
- Total chars without spaces: `text.replace(" ", "")` then `len()`
- Check each of first 10 positions individually

---

## Exercise 8: Name Initials and Formatter
**Difficulty: Intermediate-Hard**

Take a full name (First Middle Last) and create various formatted versions:

1. Extract each name part using `split()` and indexing
2. Create initials (F.M.L.)
3. Create email format: first.last@email.com (lowercase)
4. Create username: flast (first initial + last name, lowercase)
5. Count total letters in full name (no spaces)
6. Display each name part with its length

**Sample Input:**
```
Enter full name: John Michael Smith
```

**Expected Output:**
```
First name: John (4 letters)
Middle name: Michael (7 letters)
Last name: Smith (5 letters)
Initials: J.M.S.
Email: john.smith@email.com
Username: jsmith
Total letters: 16
```

**Hints:**
- `names = full_name.split()`
- First name: `names[0]`
- Initials: `names[0][0] + "." + names[1][0] + "." + names[2][0]`
- Use `.lower()` for email/username

---

## Exercise 9: Boolean Logic Puzzle
**Difficulty: Hard**

Create a program that demonstrates all boolean operations:

Take two boolean inputs (as strings "True" or "False") and show:

1. AND operation result
2. OR operation result  
3. NOT of first boolean
4. NOT of second boolean
5. XOR (exclusive OR): (A or B) and not (A and B)
6. NAND: not (A and B)
7. NOR: not (A or B)

**Sample Input:**
```
Enter first boolean (True/False): True
Enter second boolean (True/False): False
```

**Expected Output:**
```
A = True, B = False

A AND B = False
A OR B = True
NOT A = False
NOT B = True
A XOR B = True
A NAND B = True
A NOR B = False
```

**Hints:**
- Convert string to boolean: `bool1 = (input1 == "True")`
- XOR: one is true but not both
- NAND: opposite of AND
- NOR: opposite of OR

---

## Exercise 10: Multi-Type Data Processor
**Difficulty: Hard**

Create a program that takes various inputs and converts between types:

1. Take a string representation of a number
2. Convert it to int, float, and show the boolean value
3. Take a decimal number and show integer division vs float division by 2
4. Take a string and convert each operation result to different types
5. Demonstrate type() function on all conversions

**Sample Input:**
```
Enter a number as string: 42
Enter a decimal number: 17.5
```

**Expected Output:**
```
Original string: "42"
As integer: 42 (type: <class 'int'>)
As float: 42.0 (type: <class 'float'>)
As boolean: True (type: <class 'bool'>)

Decimal number: 17.5
Integer division by 2: 8 (type: <class 'int'>)
Float division by 2: 8.75 (type: <class 'float'>)
Floor division by 2: 8.0 (type: <class 'float'>)

String "42" + 10 as string: 4210
String "42" + 10 as number: 52
```

**Hints:**
- Use `int()`, `float()`, `bool()`, `str()` for conversions
- `/` gives float, `//` gives floor division
- Show type using `type()` function

---

## Bonus Challenge: Ultimate Expression Builder

Create a single program that:
- Takes 3 numbers as input
- Uses ALL arithmetic operators (+, -, *, /, //, %, **)
- Uses ALL relational operators (==, !=, >, <, >=, <=)
- Uses ALL logical operators (and, or, not)
- Takes a string and performs at least 5 different string operations
- Uses list indexing with both positive and negative indices
- Uses the `print()` function with custom `sep` and `end` parameters
- Demonstrates type conversion at least 3 times

---
