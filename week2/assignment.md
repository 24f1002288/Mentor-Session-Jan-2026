# Week 2 Programming Exercises
## Intermediate to Hard Level

These exercises test your understanding of ** Week 2 concepts**. You can now use:
- Week 1: Variables, operators, type conversion, print, input, lists, strings, indexing/slicing
- Week 2: Dynamic typing, string methods, if/elif/else statements, imports (especially random)

---

## Exercise 1: Password Strength Checker with Feedback
**Difficulty: Intermediate**

Create a password validation program that:
1. Takes a password as input
2. Checks multiple criteria using if-elif-else and string methods:
   - Minimum 8 characters
   - Contains uppercase letter
   - Contains lowercase letter
   - Contains digit
   - Contains special character (!@#$%^&*)
3. Calculates a strength score (0-5, one point per criterion)
4. Uses if-elif-else to categorize: "Very Weak" (0-1), "Weak" (2), "Medium" (3), "Strong" (4), "Very Strong" (5)
5. Provides specific feedback on what's missing

**Sample Output:**
```
Enter password: Hello123

Password Analysis:
✓ Length (8+ characters)
✓ Contains uppercase
✓ Contains lowercase
✓ Contains digit
✗ Contains special character

Strength Score: 4/5
Rating: Strong

Suggestions:
- Add a special character (!@#$%^&*) to make it stronger
```

---

## Exercise 2: Smart Calculator with Validation
**Difficulty: Intermediate**

Build a calculator that:
1. Takes two numbers and an operator (+, -, *, /, //, %, **) as input
2. Validates that inputs are numbers using string methods
3. Checks for division by zero
4. Uses if-elif-else to perform the correct operation
5. Formats output with appropriate messages
6. For division, shows both regular and floor division results

**Sample Output:**
```
Enter first number: 10
Enter second number: 3
Enter operator (+, -, *, /, //, %, **): /

Result: 10 / 3 = 3.3333333333333335
Floor division: 10 // 3 = 3
Remainder: 10 % 3 = 1
```

**Edge Cases:**
- Division by zero
- Invalid operator
- Non-numeric input

---

## Exercise 3: Text Analyzer and Transformer
**Difficulty: Intermediate-Hard**

Create a program that takes a sentence and provides analysis:
1. Display original sentence
2. Count: total characters, letters, digits, spaces, special characters
3. Word count and average word length
4. Show the sentence in different cases (upper, lower, title, swap)
5. Find and display the longest word
6. Check if sentence starts with a capital letter and ends with punctuation
7. Use if statements to provide feedback on sentence quality

**Sample Output:**
```
Enter a sentence: Hello World! Python 3 is Great.

Original: Hello World! Python 3 is Great.

Character Analysis:
- Total characters: 33
- Letters: 26
- Digits: 1
- Spaces: 5
- Special characters: 2

Word Analysis:
- Word count: 6
- Average word length: 4.67

Case Transformations:
- UPPERCASE: HELLO WORLD! PYTHON 3 IS GREAT.
- lowercase: hello world! python 3 is great.
- Title Case: Hello World! Python 3 Is Great.
- sWaPcAsE: hELLO wORLD! pYTHON 3 IS gREAT.

Longest word: Python (6 letters)

Quality Check:
✓ Starts with capital letter
✓ Ends with punctuation
✓ Good sentence structure!
```

---

## Exercise 4: Number Guessing Game
**Difficulty: Intermediate**

Create a number guessing game using random:
1. Generate a random number between 1 and 100
2. Give the user 3 attempts to guess
3. After each guess, tell them if they're too high or too low
4. Calculate how close they were (difference)
5. Use if-elif-else for different responses
6. Track number of attempts used
7. Reveal the number at the end if they don't guess it

**Sample Output:**
```
I'm thinking of a number between 1 and 100...

Attempt 1/3
Your guess: 50
Too high! You were off by 23.

Attempt 2/3
Your guess: 30
Too low! You were off by 3.

Attempt 3/3
Your guess: 27
🎉 Correct! You guessed it in 3 attempts!
```

---

## Exercise 5: Email Validator and Formatter
**Difficulty: Intermediate-Hard**

Create an email validation and formatting tool:
1. Take an email address as input
2. Clean it (strip whitespace, convert to lowercase)
3. Validate using string methods and if statements:
   - Contains exactly one @
   - Has characters before @
   - Has characters after @
   - Domain ends with .com, .edu, .org, or .net
   - No spaces in email
4. Extract username and domain
5. Provide detailed feedback if invalid

**Sample Output:**
```
Enter email:   USER@Example.COM  

Cleaned email: user@example.com

Validation Results:
✓ Contains @ symbol
✓ Has username
✓ Has domain
✓ Valid domain extension (.com)
✓ No spaces

Email is VALID!
Username: user
Domain: example.com
```

**Invalid Example:**
```
Enter email: userexample.com

Validation Results:
✗ Missing @ symbol

Email is INVALID!
```

---

## Exercise 6: Grade Calculator with Statistics
**Difficulty: Hard**

Create a grade calculator that:
1. Takes 5 subject scores as input
2. Validates each score (0-100 range)
3. Calculate: total, average, highest, lowest
4. Assign letter grade based on average using if-elif-else
5. Use random to generate a random motivational message
6. Determine pass/fail (passing >= 40 in all subjects and average >= 50)
7. Format output professionally

**Sample Output:**
```
Enter score for Subject 1: 85
Enter score for Subject 2: 90
Enter score for Subject 3: 78
Enter score for Subject 4: 92
Enter score for Subject 5: 88

Grade Report
============
Scores: 85, 90, 78, 92, 88

Statistics:
- Total: 433/500
- Average: 86.60%
- Highest: 92
- Lowest: 78
- Grade: B

Status: PASSED ✓

Motivational Message:
"Great job! Keep up the excellent work!"
```

---

## Exercise 7: Username Generator
**Difficulty: Intermediate-Hard**

Create a username generator that:
1. Takes first name and last name as input
2. Offers 5 different username formats using if-elif-else:
   - Type 1: firstlast (e.g., johnsmith)
   - Type 2: first.last (e.g., john.smith)
   - Type 3: first_last (e.g., john_smith)
   - Type 4: flast (first initial + last) (e.g., jsmith)
   - Type 5: first + random 2-digit number (e.g., john47)
3. Clean names (strip whitespace, handle capitalization)
4. Validate that names contain only letters
5. Display all options and let user choose with if-elif-else

**Sample Output:**
```
Enter first name: John
Enter last name: Smith

Available username formats:
1. johnsmith
2. john.smith
3. john_smith
4. jsmith
5. john47

Which format do you prefer? (1-5): 3
Your username: john_smith
```

---

## Exercise 8: Random Quiz Generator
**Difficulty: Hard**

Create a quiz program that:
1. Has 5 math questions stored (e.g., "What is 7 + 5?")
2. Use random.choice() to select a question
3. Generate random numbers for calculations using random.randint()
4. Take user's answer as input
5. Validate the answer is numeric
6. Check if correct using if-else
7. Provide encouraging feedback
8. Show correct answer if wrong

**Sample Output:**
```
Random Math Quiz!

Question: What is 8 × 7?
Your answer: 56

✓ Correct! Well done!

---

Question: What is 15 + 23?
Your answer: 37

✗ Incorrect. The correct answer is 38.
Don't worry, keep practicing!
```

---

## Exercise 9: String Cipher with Choice
**Difficulty: Hard**

Create an encoding/decoding program:
1. Ask user to choose: (1) Encode or (2) Decode
2. Take a message as input
3. Use if-elif-else to determine operation
4. For encoding:
   - Reverse the string
   - Swap case
   - Replace vowels with numbers (a→4, e→3, i→1, o→0, u→5)
5. For decoding: reverse the operations
6. Display original and transformed message

**Sample Output (Encoding):**
```
Choose operation:
1. Encode message
2. Decode message

Your choice: 1
Enter message: Hello World

Original: Hello World
Encoded: DLR0W 0LL3H

Process:
1. Reversed: dlroW olleH
2. Swapped case: DLROw OLLEh
3. Replaced vowels: DLR0W 0LL3H
```

---

## Exercise 10: Rock Paper Scissors Game
**Difficulty: Intermediate-Hard**

Create a Rock-Paper-Scissors game:
1. Use random.choice() for computer's move
2. Take user input (rock/paper/scissors)
3. Validate input using string methods (strip, lower)
4. Use if-elif-else to determine winner:
   - Rock beats Scissors
   - Scissors beats Paper
   - Paper beats Rock
5. Keep score (user wins, computer wins, ties)
6. Ask if user wants to play again
7. Display final statistics

**Sample Output:**
```
Rock, Paper, Scissors!

Your choice: rock
Computer chose: scissors

Rock crushes scissors!
You WIN! 🎉

Score - You: 1, Computer: 0, Ties: 0

Play again? (yes/no): yes

Your choice: paper
Computer chose: paper

It's a TIE! 🤝

Score - You: 1, Computer: 0, Ties: 1

Play again? (yes/no): no

Final Score:
You: 1 wins
Computer: 0 wins
Ties: 1

Thanks for playing!
```

---

## Bonus Challenge: Advanced Password Generator

Create a password generator that:
1. Ask user for desired password length (minimum 8)
2. Ask what to include using if statements: uppercase, lowercase, digits, special chars
3. Validate at least two types are selected
4. Use random.choice() to build password character by character
5. Ensure password meets selected criteria
6. Display the generated password
7. Calculate and show password strength

**Sample Output:**
```
Password Generator
==================

Desired length (min 8): 12

Include:
- Uppercase letters? (yes/no): yes
- Lowercase letters? (yes/no): yes
- Digits? (yes/no): yes
- Special characters? (yes/no): no

Generated Password: aB3kLm9pQr2X

Password Strength: Strong
- Length: 12 ✓
- Uppercase: Yes ✓
- Lowercase: Yes ✓
- Digits: Yes ✓
- Special characters: No

Your password is ready to use!
```

---

## Tips for Success

1. **Use String Methods:** lower(), upper(), strip(), isdigit(), isalpha(), count(), etc.
2. **Validate Input:** Always check user input with if statements
3. **Use random Module:** Import and use randint(), choice(), etc.
4. **Chain String Methods:** You can do `text.strip().lower()` in one line
5. **Test Edge Cases:** Empty strings, invalid input, boundary values
6. **Use Meaningful Variable Names:** `user_choice` is better than `x`
7. **Add User Feedback:** Make your program interactive and friendly
8. **Format Output:** Use clear labels and structure

**Remember:** You can now use:
- ✓ if/elif/else statements for decisions
- ✓ String methods for text processing
- ✓ random module for games and generators
- ✓ All Week 1 concepts (operators, type conversion, etc.)
