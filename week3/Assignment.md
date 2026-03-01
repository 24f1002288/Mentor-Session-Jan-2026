# Week 3 Programming Exercises
## Intermediate to Hard Level

These exercises test your understanding of **Weeks 1, 2, and 3 concepts**. You can now use:
- Week 1: Variables, operators, type conversion, print, input, lists, strings, indexing/slicing
- Week 2: String methods, if/elif/else, imports (random), dynamic typing
- Week 3: while loops, for loops, range(), break, continue, pass, nested loops

**Important:** All exercises must use loops!

---

## Exercise 1: Number Pattern Pyramid
**Difficulty: Intermediate**

Create a program that takes a number as input and prints a number pyramid:

**Sample Input:**
```
Enter number of rows: 5
```

**Sample Output:**
```
    1
   121
  12321
 1234321
123454321
```

**Requirements:**
1. Use nested for loops
2. Print spaces for alignment
3. Numbers increase then decrease on each row
4. Validate input is positive

---

## Exercise 2: Prime Number Finder
**Difficulty: Intermediate**

Write a program that finds all prime numbers between 1 and a given number.

**Sample Input:**
```
Enter upper limit: 20
```

**Sample Output:**
```
Prime numbers between 1 and 20:
2, 3, 5, 7, 11, 13, 17, 19

Total prime numbers found: 8
```

**Requirements:**
1. Use nested loops to check divisibility
2. Use break when a divisor is found
3. Count and display total primes
4. A number is prime if divisible only by 1 and itself

---

## Exercise 3: Multiplication Table Generator
**Difficulty: Intermediate**

Create a program that generates a multiplication table based on user input.

**Sample Input:**
```
Enter table number: 7
Enter range (how many multiples): 10
```

**Sample Output:**
```
Multiplication Table of 7:
7 × 1 = 7
7 × 2 = 14
7 × 3 = 21
7 × 4 = 28
7 × 5 = 35
7 × 6 = 42
7 × 7 = 49
7 × 8 = 56
7 × 9 = 63
7 × 10 = 70
```

**Requirements:**
1. Use a for loop or while loop
2. Format output neatly
3. Ask if user wants another table (use while True with break)

---

## Exercise 4: Factorial Calculator with Input Validation
**Difficulty: Intermediate**

Calculate the factorial of a number with proper validation.

**Sample Run 1:**
```
Enter a number: -5
Error: Number cannot be negative!

Enter a number: abc
Error: Please enter a valid number!

Enter a number: 5
5! = 120

Calculation steps:
1! = 1
2! = 2
3! = 6
4! = 24
5! = 120
```

**Requirements:**
1. Use while loop for input validation
2. Use a loop to calculate factorial
3. Display step-by-step calculation
4. Handle edge case: 0! = 1

---

## Exercise 5: String Reversal Methods
**Difficulty: Intermediate-Hard**

Create a program that reverses a string using THREE different methods:

**Sample Input:**
```
Enter a string: Python
```

**Sample Output:**
```
Original: Python

Method 1 (Using while loop): nohtyP
Method 2 (Using for loop - backward range): nohtyP
Method 3 (Using for loop - building reversed): nohtyP

All methods produce the same result: True
```

**Requirements:**
1. Method 1: Use while loop with index
2. Method 2: Use for loop with range() going backwards
3. Method 3: Use for loop to build reversed string character by character
4. Verify all three produce same result

---

## Exercise 6: Guessing Game with Limited Attempts
**Difficulty: Intermediate-Hard**

Create a number guessing game with hints and attempt tracking.

**Sample Run:**
```
I'm thinking of a number between 1 and 100.
You have 7 attempts.

Attempt 1: Enter your guess: 50
Too high! The number is less than 50.

Attempt 2: Enter your guess: 25
Too low! The number is greater than 25.

Attempt 3: Enter your guess: 37
Too high! The number is less than 37.

Attempt 4: Enter your guess: 31
Correct! You guessed it in 4 attempts!

Your score: 3/7 stars
(Stars based on: 7 attempts = 1 star, 4-6 = 2 stars, 1-3 = 3 stars)

Play again? (yes/no): no
Thanks for playing!
```

**Requirements:**
1. Use random.randint() to generate number
2. Use while loop with attempt counter
3. Provide range hints after each guess
4. Calculate star rating based on attempts
5. Ask if player wants to play again (nested while loop)

---

## Exercise 7: Pattern Printer Menu
**Difficulty: Hard**

Create a menu-driven program that prints different patterns.

**Sample Run:**
```
=== PATTERN PRINTER ===
1. Right Triangle
2. Inverted Triangle
3. Diamond
4. Number Pyramid
5. Exit

Choose pattern (1-5): 1
Enter size: 5

*
**
***
****
*****

Press Enter to continue...

=== PATTERN PRINTER ===
1. Right Triangle
2. Inverted Triangle
3. Diamond
4. Number Pyramid
5. Exit

Choose pattern (1-5): 3
Enter size: 5

  *
 ***
*****
 ***
  *

Press Enter to continue...
```

**Requirements:**
1. Use while True loop for menu
2. Use if-elif-else for pattern selection
3. Use nested loops for each pattern
4. For diamond: combine upper and lower triangles
5. Input validation for menu choice and size

---

## Exercise 8: Digit Sum and Reversal
**Difficulty: Intermediate-Hard**

Write a program that processes a number in multiple ways.

**Sample Input:**
```
Enter a number: 1234
```

**Sample Output:**
```
Original number: 1234

Analysis:
1. Digit count: 4
2. Sum of digits: 10 (1+2+3+4)
3. Product of digits: 24 (1×2×3×4)
4. Reversed number: 4321
5. Digits list: [1, 2, 3, 4]
6. Is palindrome: False

Process another number? (yes/no): yes
Enter a number: 12321

Original number: 12321

Analysis:
1. Digit count: 5
2. Sum of digits: 9
3. Product of digits: 12
4. Reversed number: 12321
5. Digits list: [1, 2, 3, 2, 1]
6. Is palindrome: True
```

**Requirements:**
1. Use while loop to extract digits
2. Calculate sum, product, count simultaneously
3. Check if number is palindrome
4. Store digits in a list
5. Ask if user wants to process another number

---

## Exercise 9: Character Frequency Counter
**Difficulty: Hard**

Count the frequency of each character in a string.

**Sample Input:**
```
Enter a string: Hello World
```

**Sample Output:**
```
Character Frequency Analysis:
(Case-insensitive, excluding spaces)

H: 1
E: 1
L: 3
O: 2
W: 1
R: 1
D: 1

Total unique characters: 7
Total characters (no spaces): 10
Most frequent character: L (appears 3 times)
```

**Requirements:**
1. Use nested loops to count each character
2. Convert to lowercase for case-insensitive counting
3. Skip spaces
4. Find the most frequent character
5. Use continue to skip already counted characters

---

## Exercise 10: FizzBuzz Enhanced
**Difficulty: Intermediate-Hard**

Create an enhanced FizzBuzz game with custom rules.

**Sample Run:**
```
=== FIZZBUZZ GAME ===

Enter start number: 1
Enter end number: 20
Enter first divisor (default 3): 3
Enter second divisor (default 5): 5

Results:
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
16
17
Fizz
19
Buzz

Statistics:
- Total numbers: 20
- Fizz count: 5
- Buzz count: 3
- FizzBuzz count: 1
- Regular numbers: 11
```

**Requirements:**
1. Use for loop with range()
2. Use if-elif-else for conditions
3. Allow custom divisors and range
4. Count each category
5. Print "Fizz" if divisible by first number
6. Print "Buzz" if divisible by second number
7. Print "FizzBuzz" if divisible by both

---

## Exercise 11: Password Strength Validator (with attempts)
**Difficulty: Hard**

Create a password validator that gives users multiple attempts to create a strong password.

**Sample Run:**
```
=== PASSWORD VALIDATOR ===
You have 3 attempts to create a valid password.

Requirements:
- At least 8 characters long
- Contains uppercase letter
- Contains lowercase letter
- Contains digit
- Contains special character (!@#$%^&*)

Attempt 1/3
Enter password: hello
✗ Too short (minimum 8 characters)
✗ Missing uppercase letter
✗ Missing digit
✗ Missing special character
Password strength: Weak (1/5 criteria met)

Attempt 2/3
Enter password: Hello123
✗ Missing special character
Password strength: Strong (4/5 criteria met)

Attempt 3/3
Enter password: Hello123!
✓ All requirements met!
Password strength: Very Strong (5/5 criteria met)

Password accepted!
```

**Requirements:**
1. Use while loop with attempt counter (max 3 attempts)
2. Use multiple loops to check each requirement
3. Use string methods (isupper, islower, isdigit)
4. Display which requirements are missing
5. Calculate strength score
6. Break if password is valid

---

## Exercise 12: Sum of Series Calculator
**Difficulty: Intermediate-Hard**

Calculate the sum of different mathematical series.

**Sample Run:**
```
=== SERIES CALCULATOR ===

Choose series type:
1. Sum of natural numbers: 1+2+3+...+n
2. Sum of squares: 1²+2²+3²+...+n²
3. Sum of cubes: 1³+2³+3³+...+n³
4. Alternating series: 1-2+3-4+5-...±n
5. Exit

Enter choice: 1
Enter n: 10

Series: 1+2+3+4+5+6+7+8+9+10
Sum: 55

Formula verification: n(n+1)/2 = 55 ✓

Calculate another? (yes/no): yes

Choose series type:
1. Sum of natural numbers: 1+2+3+...+n
2. Sum of squares: 1²+2²+3²+...+n²
3. Sum of cubes: 1³+2³+3³+...+n³
4. Alternating series: 1-2+3-4+5-...±n
5. Exit

Enter choice: 4
Enter n: 10

Series: 1-2+3-4+5-6+7-8+9-10
Sum: -5

Calculate another? (yes/no): no
Thank you!
```

**Requirements:**
1. Use while True for menu loop
2. Use for loops to calculate sums
3. Display the series as a string
4. Verify sum with formula (for series 1)
5. Handle alternating signs for series 4

---

## Bonus Challenge: Nested Loop Matrix Operations

Create a program that performs operations on a matrix.

**Sample Run:**
```
Enter matrix size (rows): 3
Enter matrix size (columns): 3

Enter values for 3×3 matrix:
Row 1: 1 2 3
Row 2: 4 5 6
Row 3: 7 8 9

Matrix Display:
1  2  3
4  5  6
7  8  9

Operations:
1. Sum of all elements: 45
2. Sum of each row: [6, 15, 24]
3. Sum of each column: [12, 15, 18]
4. Sum of diagonal: 15 (1+5+9)
5. Find maximum: 9 at position (3, 3)
6. Find minimum: 1 at position (1, 1)
7. Transpose matrix:
   1  4  7
   2  5  8
   3  6  9
```

**Requirements:**
1. Use nested loops to input matrix
2. Use nested loops for all operations
3. Store matrix as list of lists
4. Calculate row sums, column sums, diagonal sum
5. Find max/min with their positions
6. Create transposed matrix

---

## Tips for Success

### Loop Selection Guide

**Use FOR loop when:**
- You know exact number of iterations
- Iterating over a collection (list, string, range)
- Processing each character in a string
- Creating patterns with known size

**Use WHILE loop when:**
- Unknown number of iterations
- Input validation
- Game loops
- Menu systems (while True with break)
- Condition-based iteration

### Common Patterns

**Pattern 1: Input Validation**
```python
while True:
    value = input("Enter value: ")
    if valid_condition:
        break
    print("Invalid, try again!")
```

**Pattern 2: Counter with Loop**
```python
count = 0
for item in collection:
    if condition:
        count += 1
```

**Pattern 3: Building Result String**
```python
result = ""
for char in text:
    result += process(char)
```

**Pattern 4: Finding Maximum/Minimum**
```python
maximum = list[0]
for item in list:
    if item > maximum:
        maximum = item
```

### Debugging Loop Tips

1. **Print loop variables** - See what's happening each iteration
2. **Check loop bounds** - Ensure range is correct
3. **Verify update statement** - Make sure loop variable changes
4. **Test with small inputs** - Easier to trace
5. **Watch for infinite loops** - Always have an exit condition

### Remember

- Every exercise requires loops (it's Week 3!)
- Use appropriate loop type (for vs while)
- Validate all user input
- Use break/continue when appropriate
- Test edge cases (empty input, zero, negative numbers)
- Format output neatly
- Add helpful messages for users

Good luck with your exercises! Loops are powerful - master them! 🐍
