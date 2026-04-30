# Week 9: Recursion and Binary Search - Complete Notes

## Table of Contents
1. [Introduction to Recursion](#introduction-to-recursion)
2. [Theoretical Introduction to Recursion](#theoretical-introduction-to-recursion)
3. [Recursion - An Illustration](#recursion-an-illustration)
4. [Recursion: A Simple Question](#recursion-a-simple-question)
5. [Recursion: Find 0 in a List](#recursion-find-0-in-a-list)
6. [Sorting Recursively](#sorting-recursively)
7. [Introduction to Binary Search](#introduction-to-binary-search)
8. [Warm Up for Binary Search](#warm-up-for-binary-search)
9. [Binary Search Implementation](#binary-search-implementation)
10. [Binary Search Recursion Way](#binary-search-recursion-way)

---

## L9.1: Introduction to Recursion

### What is Recursion?

**Recursion** is a programming technique where a function calls itself to solve a problem by breaking it down into smaller, similar subproblems.

**Definition:** A recursive function is a function that calls itself directly or indirectly.

### Real-World Analogies

#### 1. Russian Nesting Dolls (Matryoshka)
Each doll contains a smaller version of itself until you reach the smallest doll.

#### 2. Mirrors Facing Each Other
When two mirrors face each other, they create infinite reflections - each reflection contains the image again.

#### 3. Looking Up a Word in Dictionary
- You look up "recursion"
- Definition says "see recursion"
- You look up "recursion" again...

### Simple Example

```python
def countdown(n):
    if n <= 0:  # Base case
        print("Blastoff!")
    else:
        print(n)
        countdown(n - 1)  # Recursive call

countdown(5)
# Output:
# 5
# 4
# 3
# 2
# 1
# Blastoff!
```

### Two Essential Components

Every recursive function needs:

1. **Base Case** - The stopping condition
   - Prevents infinite recursion
   - Provides the simplest answer

2. **Recursive Case** - The function calling itself
   - Breaks problem into smaller parts
   - Moves toward the base case

```python
def example(n):
    # Base case - when to stop
    if n == 0:
        return "Done"
    
    # Recursive case - function calls itself
    return example(n - 1)
```

### Why Use Recursion?

**Advantages:**
- ✅ Elegant and clean code
- ✅ Natural for tree/graph structures
- ✅ Simplifies complex problems
- ✅ Some problems are naturally recursive

**Disadvantages:**
- ❌ Can be memory intensive (call stack)
- ❌ May be slower than iteration
- ❌ Risk of stack overflow
- ❌ Can be harder to debug

### When to Use Recursion?

Use recursion when:
- Problem can be broken into smaller similar subproblems
- Working with tree or graph structures
- Implementing divide-and-conquer algorithms
- Problem has natural recursive definition (factorial, fibonacci)

---

## L9.2: Theoretical Introduction to Recursion

### How Recursion Works

When a function calls itself, each call is added to the **call stack**.

#### The Call Stack

```python
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n - 1)

result = factorial(4)
```

**Call Stack Visualization:**
```
factorial(4)
  → 4 * factorial(3)
       → 3 * factorial(2)
            → 2 * factorial(1)
                 → returns 1
            → returns 2 * 1 = 2
       → returns 3 * 2 = 6
  → returns 4 * 6 = 24
```

**Step by Step:**
1. `factorial(4)` → needs `factorial(3)`
2. `factorial(3)` → needs `factorial(2)`
3. `factorial(2)` → needs `factorial(1)`
4. `factorial(1)` → **base case**, returns 1
5. `factorial(2)` → returns 2 × 1 = 2
6. `factorial(3)` → returns 3 × 2 = 6
7. `factorial(4)` → returns 4 × 6 = 24

### Memory in Recursion

Each recursive call:
- Takes memory on the call stack
- Stores local variables and parameters
- Stores return address

```python
def recursive_sum(n):
    if n == 0:
        return 0
    return n + recursive_sum(n - 1)

# Call: recursive_sum(5)
# Stack frames:
# recursive_sum(5) → 5 + recursive_sum(4)
# recursive_sum(4) → 4 + recursive_sum(3)
# recursive_sum(3) → 3 + recursive_sum(2)
# recursive_sum(2) → 2 + recursive_sum(1)
# recursive_sum(1) → 1 + recursive_sum(0)
# recursive_sum(0) → 0 (base case)
# 
# Unwinding:
# 0
# 1 + 0 = 1
# 2 + 1 = 3
# 3 + 3 = 6
# 4 + 6 = 10
# 5 + 10 = 15
```

### Types of Recursion

#### 1. Direct Recursion
Function calls itself directly.

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)  # Direct call to itself
```

#### 2. Indirect Recursion
Function A calls Function B, which calls Function A.

```python
def function_a(n):
    if n > 0:
        print("A:", n)
        function_b(n - 1)

def function_b(n):
    if n > 0:
        print("B:", n)
        function_a(n - 1)

function_a(3)
# Output:
# A: 3
# B: 2
# A: 1
```

#### 3. Tail Recursion
Recursive call is the last operation in the function.

```python
# Tail recursive
def factorial_tail(n, accumulator=1):
    if n <= 1:
        return accumulator
    return factorial_tail(n - 1, n * accumulator)

# Not tail recursive
def factorial_not_tail(n):
    if n <= 1:
        return 1
    return n * factorial_not_tail(n - 1)  # Multiplication after recursive call
```

#### 4. Head Recursion
Recursive call is the first operation.

```python
def head_recursive(n):
    if n > 0:
        head_recursive(n - 1)  # Recursive call first
        print(n)  # Operation after

head_recursive(3)
# Output: 1, 2, 3
```

### Recursion vs Iteration

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| **Approach** | Function calls itself | Loops (for, while) |
| **Memory** | Uses call stack | Uses fixed memory |
| **Speed** | Generally slower | Generally faster |
| **Code** | Often cleaner | Sometimes verbose |
| **Termination** | Base case | Loop condition |
| **Overflow Risk** | Stack overflow possible | No such risk |

**Example - Both Approaches:**

```python
# Recursive factorial
def factorial_recursive(n):
    if n <= 1:
        return 1
    return n * factorial_recursive(n - 1)

# Iterative factorial
def factorial_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

print(factorial_recursive(5))  # 120
print(factorial_iterative(5))  # 120
```

### Mathematical Recurrence Relations

Many recursive functions implement mathematical recurrence relations:

#### Factorial
```
n! = n × (n-1)!
0! = 1
```

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)
```

#### Fibonacci
```
F(n) = F(n-1) + F(n-2)
F(0) = 0, F(1) = 1
```

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

#### Power
```
x^n = x × x^(n-1)
x^0 = 1
```

```python
def power(x, n):
    if n == 0:
        return 1
    return x * power(x, n - 1)
```

---

## L9.3: Recursion - An Illustration

### Example 1: Printing Numbers

#### Forward (1 to n)

```python
def print_forward(n):
    if n > 0:
        print_forward(n - 1)  # Recursive call first
        print(n)  # Then print

print_forward(5)
# Output: 1, 2, 3, 4, 5
```

**How it works:**
```
print_forward(5)
  print_forward(4)
    print_forward(3)
      print_forward(2)
        print_forward(1)
          print_forward(0) → base case, returns
        print(1)
      print(2)
    print(3)
  print(4)
print(5)
```

#### Backward (n to 1)

```python
def print_backward(n):
    if n > 0:
        print(n)  # Print first
        print_backward(n - 1)  # Then recursive call

print_backward(5)
# Output: 5, 4, 3, 2, 1
```

### Example 2: Sum of Numbers

```python
# Sum from 1 to n
def sum_numbers(n):
    if n == 0:
        return 0
    return n + sum_numbers(n - 1)

print(sum_numbers(5))  # 15 (1+2+3+4+5)
```

**Trace:**
```
sum_numbers(5)
= 5 + sum_numbers(4)
= 5 + (4 + sum_numbers(3))
= 5 + (4 + (3 + sum_numbers(2)))
= 5 + (4 + (3 + (2 + sum_numbers(1))))
= 5 + (4 + (3 + (2 + (1 + sum_numbers(0)))))
= 5 + (4 + (3 + (2 + (1 + 0))))
= 5 + (4 + (3 + (2 + 1)))
= 5 + (4 + (3 + 3))
= 5 + (4 + 6)
= 5 + 10
= 15
```

### Example 3: String Reversal

```python
def reverse_string(s):
    if len(s) == 0:
        return ""
    return s[-1] + reverse_string(s[:-1])

print(reverse_string("hello"))  # "olleh"
```

**Trace:**
```
reverse_string("hello")
= "o" + reverse_string("hell")
= "o" + ("l" + reverse_string("hel"))
= "o" + ("l" + ("l" + reverse_string("he")))
= "o" + ("l" + ("l" + ("e" + reverse_string("h"))))
= "o" + ("l" + ("l" + ("e" + ("h" + reverse_string("")))))
= "o" + ("l" + ("l" + ("e" + ("h" + ""))))
= "o" + ("l" + ("l" + ("e" + "h")))
= "o" + ("l" + ("l" + "eh"))
= "o" + ("l" + "leh")
= "o" + "lleh"
= "olleh"
```

### Example 4: Palindrome Check

```python
def is_palindrome(s):
    # Remove spaces and convert to lowercase
    s = s.replace(" ", "").lower()
    
    # Base cases
    if len(s) <= 1:
        return True
    
    # Check first and last character
    if s[0] != s[-1]:
        return False
    
    # Recursively check middle portion
    return is_palindrome(s[1:-1])

print(is_palindrome("racecar"))  # True
print(is_palindrome("hello"))    # False
print(is_palindrome("A man a plan a canal Panama"))  # True
```

### Example 5: List Sum

```python
def sum_list(lst):
    if len(lst) == 0:
        return 0
    return lst[0] + sum_list(lst[1:])

print(sum_list([1, 2, 3, 4, 5]))  # 15
```

**Trace:**
```
sum_list([1, 2, 3, 4, 5])
= 1 + sum_list([2, 3, 4, 5])
= 1 + (2 + sum_list([3, 4, 5]))
= 1 + (2 + (3 + sum_list([4, 5])))
= 1 + (2 + (3 + (4 + sum_list([5]))))
= 1 + (2 + (3 + (4 + (5 + sum_list([])))))
= 1 + (2 + (3 + (4 + (5 + 0))))
= 15
```

### Visualization Tool

```python
def visualize_recursion(n, indent=0):
    """Visualize recursive calls"""
    spaces = "  " * indent
    print(f"{spaces}→ Called with n={n}")
    
    if n <= 0:
        print(f"{spaces}← Base case reached")
        return 0
    
    result = n + visualize_recursion(n - 1, indent + 1)
    print(f"{spaces}← Returning {result}")
    return result

visualize_recursion(3)
```

**Output:**
```
→ Called with n=3
  → Called with n=2
    → Called with n=1
      → Called with n=0
      ← Base case reached
    ← Returning 1
  ← Returning 3
← Returning 6
```

---

## L9.4: Recursion - A Simple Question

### Problem: Calculate n raised to power m

**Mathematical Definition:**
```
n^m = n × n^(m-1)
n^0 = 1
```

### Recursive Solution

```python
def power(n, m):
    """Calculate n raised to power m"""
    # Base case
    if m == 0:
        return 1
    
    # Recursive case
    return n * power(n, m - 1)

print(power(2, 5))   # 32  (2^5)
print(power(3, 4))   # 81  (3^4)
print(power(5, 0))   # 1   (5^0)
```

**Trace for power(2, 3):**
```
power(2, 3)
= 2 * power(2, 2)
= 2 * (2 * power(2, 1))
= 2 * (2 * (2 * power(2, 0)))
= 2 * (2 * (2 * 1))
= 2 * (2 * 2)
= 2 * 4
= 8
```

### Iterative Solution (for comparison)

```python
def power_iterative(n, m):
    result = 1
    for i in range(m):
        result *= n
    return result

print(power_iterative(2, 5))  # 32
```

### Optimized Recursive Solution (Fast Power)

For large exponents, we can optimize using divide-and-conquer:

```python
def fast_power(n, m):
    """Optimized power calculation using divide-and-conquer"""
    # Base case
    if m == 0:
        return 1
    
    # If exponent is even: n^m = (n^(m/2))^2
    if m % 2 == 0:
        half = fast_power(n, m // 2)
        return half * half
    
    # If exponent is odd: n^m = n × n^(m-1)
    else:
        return n * fast_power(n, m - 1)

print(fast_power(2, 10))  # 1024
```

**Why is it faster?**
- Regular: O(m) multiplications
- Fast: O(log m) multiplications

**Example: 2^8**
```
Regular power(2, 8): 8 multiplications
2 * 2 * 2 * 2 * 2 * 2 * 2 * 2

Fast power(2, 8): 3 multiplications
2^8 = (2^4)^2
2^4 = (2^2)^2
2^2 = (2^1)^2 = 2 * 2
```

### More Simple Recursive Problems

#### 1. Count Digits

```python
def count_digits(n):
    """Count number of digits in n"""
    if n < 10:
        return 1
    return 1 + count_digits(n // 10)

print(count_digits(12345))  # 5
```

#### 2. Sum of Digits

```python
def sum_digits(n):
    """Calculate sum of digits"""
    if n < 10:
        return n
    return (n % 10) + sum_digits(n // 10)

print(sum_digits(12345))  # 15 (1+2+3+4+5)
```

#### 3. Reverse Number

```python
def reverse_number(n, reversed_num=0):
    """Reverse digits of a number"""
    if n == 0:
        return reversed_num
    
    last_digit = n % 10
    reversed_num = reversed_num * 10 + last_digit
    return reverse_number(n // 10, reversed_num)

print(reverse_number(12345))  # 54321
```

#### 4. GCD (Greatest Common Divisor)

```python
def gcd(a, b):
    """Calculate GCD using Euclidean algorithm"""
    if b == 0:
        return a
    return gcd(b, a % b)

print(gcd(48, 18))  # 6
```

**Trace:**
```
gcd(48, 18)
= gcd(18, 48 % 18)
= gcd(18, 12)
= gcd(12, 18 % 12)
= gcd(12, 6)
= gcd(6, 12 % 6)
= gcd(6, 0)
= 6
```

---

## L9.5: Recursion - Find 0 in a List

### Problem Statement

Given a list of numbers, find if 0 exists in the list using recursion.

### Solution 1: Basic Recursive Search

```python
def find_zero(lst):
    """Check if 0 exists in list"""
    # Base case 1: empty list
    if len(lst) == 0:
        return False
    
    # Base case 2: found 0
    if lst[0] == 0:
        return True
    
    # Recursive case: check rest of list
    return find_zero(lst[1:])

# Test
print(find_zero([1, 2, 3, 4, 5]))      # False
print(find_zero([1, 2, 0, 4, 5]))      # True
print(find_zero([]))                    # False
```

**Trace for find_zero([1, 2, 0, 4]):**
```
find_zero([1, 2, 0, 4])
→ lst[0] = 1, not 0
→ find_zero([2, 0, 4])
  → lst[0] = 2, not 0
  → find_zero([0, 4])
    → lst[0] = 0, found!
    ← return True
  ← return True
← return True
```

### Solution 2: With Index Parameter

```python
def find_zero_index(lst, index=0):
    """Find 0 in list and return its index"""
    # Base case 1: reached end of list
    if index >= len(lst):
        return -1  # Not found
    
    # Base case 2: found 0
    if lst[index] == 0:
        return index
    
    # Recursive case: check next element
    return find_zero_index(lst, index + 1)

# Test
print(find_zero_index([1, 2, 3, 4, 5]))    # -1 (not found)
print(find_zero_index([1, 2, 0, 4, 5]))    # 2 (found at index 2)
print(find_zero_index([0, 1, 2, 3]))       # 0 (found at index 0)
```

### Solution 3: Find All Occurrences

```python
def find_all_zeros(lst, index=0, positions=None):
    """Find all positions where 0 occurs"""
    if positions is None:
        positions = []
    
    # Base case: reached end
    if index >= len(lst):
        return positions
    
    # If current element is 0, add to positions
    if lst[index] == 0:
        positions.append(index)
    
    # Recursive case: check next element
    return find_all_zeros(lst, index + 1, positions)

# Test
print(find_all_zeros([1, 0, 2, 0, 3, 0]))  # [1, 3, 5]
print(find_all_zeros([1, 2, 3, 4, 5]))     # []
```

### Solution 4: Count Zeros

```python
def count_zeros(lst):
    """Count how many zeros are in the list"""
    # Base case: empty list
    if len(lst) == 0:
        return 0
    
    # Check first element and add to count from rest
    if lst[0] == 0:
        return 1 + count_zeros(lst[1:])
    else:
        return count_zeros(lst[1:])

# Test
print(count_zeros([1, 0, 2, 0, 3, 0]))  # 3
print(count_zeros([1, 2, 3, 4, 5]))     # 0
```

### Generalized: Find Any Element

```python
def find_element(lst, target):
    """Find if target exists in list"""
    # Base case 1: empty list
    if len(lst) == 0:
        return False
    
    # Base case 2: found target
    if lst[0] == target:
        return True
    
    # Recursive case
    return find_element(lst[1:], target)

# Test
print(find_element([1, 2, 3, 4, 5], 3))   # True
print(find_element([1, 2, 3, 4, 5], 6))   # False
print(find_element([1, 2, 3, 4, 5], 0))   # False
```

### Find Element with Position

```python
def find_element_position(lst, target, index=0):
    """Find target in list and return position"""
    # Base case 1: reached end
    if index >= len(lst):
        return -1
    
    # Base case 2: found target
    if lst[index] == target:
        return index
    
    # Recursive case
    return find_element_position(lst, target, index + 1)

# Test
print(find_element_position([1, 2, 3, 4, 5], 3))  # 2
print(find_element_position([1, 2, 3, 4, 5], 6))  # -1
```

### Linear Search (Recursive)

```python
def linear_search_recursive(lst, target, start=0, end=None):
    """Recursive linear search"""
    if end is None:
        end = len(lst)
    
    # Base case: not found
    if start >= end:
        return -1
    
    # Base case: found
    if lst[start] == target:
        return start
    
    # Recursive case: search in rest
    return linear_search_recursive(lst, target, start + 1, end)

# Test
numbers = [5, 2, 8, 1, 9, 3, 7]
print(linear_search_recursive(numbers, 9))  # 4
print(linear_search_recursive(numbers, 10)) # -1
```

---

## L9.6: Sorting Recursively

### Merge Sort

**Concept:** Divide-and-conquer sorting algorithm
- Divide array into two halves
- Recursively sort each half
- Merge the sorted halves

**Time Complexity:** O(n log n)

#### Implementation

```python
def merge_sort(arr):
    """Sort array using merge sort"""
    # Base case: array with 0 or 1 element is already sorted
    if len(arr) <= 1:
        return arr
    
    # Divide: find middle point
    mid = len(arr) // 2
    left = arr[:mid]
    right = arr[mid:]
    
    # Conquer: recursively sort both halves
    left = merge_sort(left)
    right = merge_sort(right)
    
    # Combine: merge sorted halves
    return merge(left, right)

def merge(left, right):
    """Merge two sorted arrays"""
    result = []
    i = j = 0
    
    # Compare elements from left and right
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    # Add remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    
    return result

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
sorted_numbers = merge_sort(numbers)
print(sorted_numbers)  # [11, 12, 22, 25, 34, 64, 90]
```

**Visualization of merge_sort([38, 27, 43, 3]):**
```
[38, 27, 43, 3]
    ↓ divide
[38, 27]  [43, 3]
    ↓ divide
[38] [27]  [43] [3]
    ↓ merge
[27, 38]  [3, 43]
    ↓ merge
[3, 27, 38, 43]
```

### Quick Sort

**Concept:** Divide-and-conquer sorting
- Choose a pivot element
- Partition array: elements < pivot on left, > pivot on right
- Recursively sort left and right partitions

**Time Complexity:** O(n log n) average, O(n²) worst case

#### Implementation

```python
def quick_sort(arr):
    """Sort array using quick sort"""
    # Base case
    if len(arr) <= 1:
        return arr
    
    # Choose pivot (middle element)
    pivot = arr[len(arr) // 2]
    
    # Partition
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    
    # Recursively sort and combine
    return quick_sort(left) + middle + quick_sort(right)

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
sorted_numbers = quick_sort(numbers)
print(sorted_numbers)  # [11, 12, 22, 25, 34, 64, 90]
```

**Visualization of quick_sort([3, 6, 8, 10, 1, 2, 1]):**
```
[3, 6, 8, 10, 1, 2, 1]  pivot=10
  ↓
left=[3, 6, 8, 1, 2, 1]  middle=[10]  right=[]
  ↓
[3, 6, 8, 1, 2, 1]  pivot=1
  ↓
left=[]  middle=[1, 1]  right=[3, 6, 8, 2]
           ↓
       [3, 6, 8, 2]  pivot=6
         ↓
       left=[3, 2]  middle=[6]  right=[8]
         ↓
       [2, 3]
         ↓
[1, 1, 2, 3, 6, 8, 10]
```

### Quick Sort - In-Place Version

```python
def quick_sort_inplace(arr, low=0, high=None):
    """In-place quick sort"""
    if high is None:
        high = len(arr) - 1
    
    if low < high:
        # Partition and get pivot position
        pivot_index = partition(arr, low, high)
        
        # Recursively sort left and right
        quick_sort_inplace(arr, low, pivot_index - 1)
        quick_sort_inplace(arr, pivot_index + 1, high)
    
    return arr

def partition(arr, low, high):
    """Partition array and return pivot index"""
    pivot = arr[high]
    i = low - 1
    
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
quick_sort_inplace(numbers)
print(numbers)  # [11, 12, 22, 25, 34, 64, 90]
```

### Comparison: Merge Sort vs Quick Sort

| Aspect | Merge Sort | Quick Sort |
|--------|------------|------------|
| **Best Case** | O(n log n) | O(n log n) |
| **Average Case** | O(n log n) | O(n log n) |
| **Worst Case** | O(n log n) | O(n²) |
| **Space** | O(n) | O(log n) |
| **Stable** | Yes | No |
| **In-place** | No | Yes |

### Selection Sort (Recursive)

```python
def selection_sort_recursive(arr, start=0):
    """Recursive selection sort"""
    # Base case
    if start >= len(arr) - 1:
        return arr
    
    # Find minimum element in remaining array
    min_index = start
    for i in range(start + 1, len(arr)):
        if arr[i] < arr[min_index]:
            min_index = i
    
    # Swap with first element
    arr[start], arr[min_index] = arr[min_index], arr[start]
    
    # Recursively sort rest
    return selection_sort_recursive(arr, start + 1)

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
selection_sort_recursive(numbers)
print(numbers)  # [11, 12, 22, 25, 34, 64, 90]
```

### Insertion Sort (Recursive)

```python
def insertion_sort_recursive(arr, n=None):
    """Recursive insertion sort"""
    if n is None:
        n = len(arr)
    
    # Base case
    if n <= 1:
        return
    
    # Sort first n-1 elements
    insertion_sort_recursive(arr, n - 1)
    
    # Insert last element at correct position
    last = arr[n - 1]
    j = n - 2
    
    while j >= 0 and arr[j] > last:
        arr[j + 1] = arr[j]
        j -= 1
    
    arr[j + 1] = last

# Test
numbers = [64, 34, 25, 12, 22, 11, 90]
insertion_sort_recursive(numbers)
print(numbers)  # [11, 12, 22, 25, 34, 64, 90]
```

---

## L9.7: Introduction to Binary Search

### What is Binary Search?

**Binary Search** is an efficient algorithm for finding an item in a **sorted** list.

**Key Requirement:** The list must be sorted!

### How Binary Search Works

1. Compare target with middle element
2. If target equals middle: Found!
3. If target < middle: Search left half
4. If target > middle: Search right half
5. Repeat until found or search space is empty

### Why Binary Search is Efficient

**Linear Search:** O(n) - check each element
**Binary Search:** O(log n) - eliminate half each time

**Example:** Finding element in list of 1,000,000 items
- Linear Search: up to 1,000,000 comparisons
- Binary Search: at most 20 comparisons!

### Analogy: Guessing a Number

You're thinking of a number between 1 and 100. I try to guess it:

**Linear Search Approach:**
- Is it 1? No
- Is it 2? No
- Is it 3? No
- ... (could take 100 guesses!)

**Binary Search Approach:**
- Is it 50? Lower
- Is it 25? Higher
- Is it 37? Lower
- Is it 31? Higher
- Is it 34? Higher
- Is it 35? Correct!
- (Only 6 guesses!)

### Visual Example

```
Searching for 31 in [3, 7, 12, 19, 23, 31, 45, 52, 67, 88]

Step 1: Check middle (23)
[3, 7, 12, 19, 23] | 31 | [45, 52, 67, 88]
31 > 23, search right →

Step 2: Check middle (52)
[31, 45, 52] | 67 | [88]
31 < 52, search left ←

Step 3: Check middle (45)
[31] | 45 | [52]
31 < 45, search left ←

Step 4: Check element (31)
[31]
Found!
```

### When to Use Binary Search

✅ **Use when:**
- List is sorted
- Need fast search (O(log n))
- List is large
- Doing multiple searches

❌ **Don't use when:**
- List is unsorted (or sorting cost > benefit)
- List is very small (linear search is fine)
- List changes frequently (maintaining sorted order is expensive)

### Binary Search vs Linear Search

```python
# Linear Search - works on unsorted lists
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# Binary Search - requires sorted list
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

### Comparison

| Aspect | Linear Search | Binary Search |
|--------|---------------|---------------|
| **Time Complexity** | O(n) | O(log n) |
| **Sorted Required** | No | Yes |
| **Best For** | Small/unsorted lists | Large sorted lists |
| **Implementation** | Simpler | Slightly complex |

**Example Performance:**

```
List size: 1,000,000 elements

Linear Search worst case: 1,000,000 comparisons
Binary Search worst case: 20 comparisons

Binary Search is 50,000x faster!
```

---

## L9.8: Warm Up for Binary Search

### Prerequisites and Concepts

#### 1. Understanding Mid Point Calculation

```python
# Method 1: Simple (may overflow for very large numbers)
mid = (left + right) // 2

# Method 2: Safer (prevents overflow)
mid = left + (right - left) // 2

# Both give same result for normal cases
left, right = 0, 10
print((left + right) // 2)          # 5
print(left + (right - left) // 2)   # 5
```

#### 2. Search Space Reduction

Binary search works by repeatedly halving the search space:

```
Initial: 16 elements
After 1 comparison: 8 elements
After 2 comparisons: 4 elements
After 3 comparisons: 2 elements
After 4 comparisons: 1 element

Number of comparisons = log₂(n)
```

#### 3. Loop Conditions

```python
# Important: left <= right (not left < right)
while left <= right:  # Continue while there are elements to search
    mid = (left + right) // 2
    # ...
```

### Simple Examples Leading to Binary Search

#### Example 1: Find Peak Element

```python
def find_peak(arr):
    """Find a peak element (element greater than neighbors)"""
    left, right = 0, len(arr) - 1
    
    while left < right:
        mid = (left + right) // 2
        
        # Check if mid is peak
        if arr[mid] > arr[mid + 1]:
            # Peak is on left side (including mid)
            right = mid
        else:
            # Peak is on right side
            left = mid + 1
    
    return left

# Test
arr = [1, 3, 20, 4, 1, 0]
print(find_peak(arr))  # 2 (element 20 at index 2)
```

#### Example 2: Find First Occurrence

```python
def find_first(arr, target):
    """Find first occurrence of target"""
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid
            right = mid - 1  # Continue searching on left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

# Test
arr = [1, 2, 2, 2, 3, 4, 5]
print(find_first(arr, 2))  # 1 (first occurrence at index 1)
```

#### Example 3: Find Last Occurrence

```python
def find_last(arr, target):
    """Find last occurrence of target"""
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid
            left = mid + 1  # Continue searching on right
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

# Test
arr = [1, 2, 2, 2, 3, 4, 5]
print(find_last(arr, 2))  # 3 (last occurrence at index 3)
```

#### Example 4: Count Occurrences

```python
def count_occurrences(arr, target):
    """Count how many times target appears"""
    first = find_first(arr, target)
    if first == -1:
        return 0
    
    last = find_last(arr, target)
    return last - first + 1

# Test
arr = [1, 2, 2, 2, 3, 4, 5]
print(count_occurrences(arr, 2))  # 3
```

### Understanding Search Boundaries

```python
def demo_boundaries(arr, target):
    """Demonstrate how boundaries change"""
    left, right = 0, len(arr) - 1
    iteration = 0
    
    while left <= right:
        iteration += 1
        mid = (left + right) // 2
        
        print(f"Iteration {iteration}:")
        print(f"  Search space: arr[{left}:{right+1}] = {arr[left:right+1]}")
        print(f"  Middle index: {mid}, value: {arr[mid]}")
        
        if arr[mid] == target:
            print(f"  Found at index {mid}!")
            return mid
        elif arr[mid] < target:
            print(f"  {arr[mid]} < {target}, search right half")
            left = mid + 1
        else:
            print(f"  {arr[mid]} > {target}, search left half")
            right = mid - 1
        print()
    
    print("Not found!")
    return -1

# Demo
arr = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
demo_boundaries(arr, 13)
```

**Output:**
```
Iteration 1:
  Search space: arr[0:10] = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
  Middle index: 4, value: 9
  9 < 13, search right half

Iteration 2:
  Search space: arr[5:10] = [11, 13, 15, 17, 19]
  Middle index: 7, value: 15
  15 > 13, search left half

Iteration 3:
  Search space: arr[5:7] = [11, 13]
  Middle index: 6, value: 13
  Found at index 6!
```

---

## L9.9: Binary Search Implementation

### Iterative Binary Search

```python
def binary_search(arr, target):
    """
    Binary search implementation (iterative)
    
    Args:
        arr: Sorted list of elements
        target: Element to search for
    
    Returns:
        Index of target if found, -1 otherwise
    """
    left = 0
    right = len(arr) - 1
    
    while left <= right:
        # Calculate middle index
        mid = (left + right) // 2
        
        # Check if target is at mid
        if arr[mid] == target:
            return mid
        
        # If target is greater, ignore left half
        elif arr[mid] < target:
            left = mid + 1
        
        # If target is smaller, ignore right half
        else:
            right = mid - 1
    
    # Target not found
    return -1

# Test cases
arr = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]

print(binary_search(arr, 23))   # 5
print(binary_search(arr, 2))    # 0
print(binary_search(arr, 78))   # 10
print(binary_search(arr, 100))  # -1 (not found)
```

### Step-by-Step Example

```python
def binary_search_verbose(arr, target):
    """Binary search with detailed output"""
    left = 0
    right = len(arr) - 1
    step = 0
    
    print(f"Searching for {target} in {arr}\n")
    
    while left <= right:
        step += 1
        mid = (left + right) // 2
        
        print(f"Step {step}:")
        print(f"  Left: {left}, Right: {right}, Mid: {mid}")
        print(f"  Checking arr[{mid}] = {arr[mid]}")
        
        if arr[mid] == target:
            print(f"  ✓ Found! Target {target} is at index {mid}\n")
            return mid
        elif arr[mid] < target:
            print(f"  → Target is greater, search right half")
            left = mid + 1
        else:
            print(f"  ← Target is smaller, search left half")
            right = mid - 1
        print()
    
    print(f"✗ Target {target} not found in array\n")
    return -1

# Example
arr = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
binary_search_verbose(arr, 13)
```

### Binary Search with Custom Comparator

```python
def binary_search_custom(arr, target, compare_func=None):
    """
    Binary search with custom comparison function
    
    Args:
        arr: Sorted list
        target: Element to find
        compare_func: Function(a, b) returning -1, 0, or 1
    """
    if compare_func is None:
        compare_func = lambda a, b: -1 if a < b else (1 if a > b else 0)
    
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        cmp = compare_func(arr[mid], target)
        
        if cmp == 0:
            return mid
        elif cmp < 0:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# Test with strings
words = ["apple", "banana", "cherry", "date", "elderberry"]
print(binary_search_custom(words, "cherry"))  # 2

# Test with tuples (compare by first element)
pairs = [(1, "a"), (3, "b"), (5, "c"), (7, "d")]
compare_first = lambda a, b: -1 if a[0] < b else (1 if a[0] > b else 0)
print(binary_search_custom(pairs, 5, compare_first))  # 2
```

### Finding Insertion Point

```python
def binary_search_insert(arr, target):
    """
    Find the index where target should be inserted to maintain sorted order
    
    Returns:
        Index where target should be inserted
    """
    left, right = 0, len(arr)
    
    while left < right:
        mid = (left + right) // 2
        
        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid
    
    return left

# Test
arr = [1, 3, 5, 7, 9]
print(binary_search_insert(arr, 6))  # 3 (insert at index 3)
print(binary_search_insert(arr, 0))  # 0 (insert at beginning)
print(binary_search_insert(arr, 10)) # 5 (insert at end)
```

### Binary Search in Range

```python
def binary_search_range(arr, target, left, right):
    """
    Binary search in specific range [left, right]
    """
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# Test
arr = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
print(binary_search_range(arr, 13, 0, 9))   # 6
print(binary_search_range(arr, 13, 0, 5))   # -1 (not in range)
```

### Using Python's bisect Module

```python
import bisect

arr = [1, 3, 5, 7, 9, 11, 13, 15]

# Find insertion point (left)
print(bisect.bisect_left(arr, 7))   # 3

# Find insertion point (right)
print(bisect.bisect_right(arr, 7))  # 4

# Insert and maintain sorted order
bisect.insort(arr, 6)
print(arr)  # [1, 3, 5, 6, 7, 9, 11, 13, 15]

# Check if element exists
def contains(arr, x):
    i = bisect.bisect_left(arr, x)
    return i < len(arr) and arr[i] == x

print(contains(arr, 7))   # True
print(contains(arr, 8))   # False
```

---

## L9.10: Binary Search - Recursion Way

### Recursive Binary Search

```python
def binary_search_recursive(arr, target, left=0, right=None):
    """
    Binary search using recursion
    
    Args:
        arr: Sorted list
        target: Element to search
        left: Left boundary (default: 0)
        right: Right boundary (default: len(arr) - 1)
    
    Returns:
        Index of target if found, -1 otherwise
    """
    # Initialize right on first call
    if right is None:
        right = len(arr) - 1
    
    # Base case: search space is empty
    if left > right:
        return -1
    
    # Calculate middle
    mid = (left + right) // 2
    
    # Check if target is at mid
    if arr[mid] == target:
        return mid
    
    # If target is in left half
    elif arr[mid] > target:
        return binary_search_recursive(arr, target, left, mid - 1)
    
    # If target is in right half
    else:
        return binary_search_recursive(arr, target, mid + 1, right)

# Test
arr = [2, 5, 8, 12, 16, 23, 38, 45, 56, 67, 78]
print(binary_search_recursive(arr, 23))   # 5
print(binary_search_recursive(arr, 2))    # 0
print(binary_search_recursive(arr, 100))  # -1
```

### Recursive Binary Search with Visualization

```python
def binary_search_recursive_visual(arr, target, left=0, right=None, depth=0):
    """Recursive binary search with call stack visualization"""
    if right is None:
        right = len(arr) - 1
    
    indent = "  " * depth
    print(f"{indent}Searching in arr[{left}:{right+1}] = {arr[left:right+1]}")
    
    # Base case
    if left > right:
        print(f"{indent}Not found")
        return -1
    
    mid = (left + right) // 2
    print(f"{indent}Mid: {mid}, Value: {arr[mid]}")
    
    # Found
    if arr[mid] == target:
        print(f"{indent}✓ Found at index {mid}!")
        return mid
    
    # Search left
    elif arr[mid] > target:
        print(f"{indent}→ Search left half")
        return binary_search_recursive_visual(arr, target, left, mid - 1, depth + 1)
    
    # Search right
    else:
        print(f"{indent}→ Search right half")
        return binary_search_recursive_visual(arr, target, mid + 1, right, depth + 1)

# Demo
arr = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
print(f"\nSearching for 13:\n")
binary_search_recursive_visual(arr, 13)
```

**Output:**
```
Searching for 13:

Searching in arr[0:10] = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
Mid: 4, Value: 9
→ Search right half
  Searching in arr[5:10] = [11, 13, 15, 17, 19]
  Mid: 7, Value: 15
  → Search left half
    Searching in arr[5:7] = [11, 13]
    Mid: 6, Value: 13
    ✓ Found at index 6!
```

### Call Stack Analysis

```python
def binary_search_with_stack_trace(arr, target, left=0, right=None, call_stack=None):
    """Show call stack for recursive binary search"""
    if call_stack is None:
        call_stack = []
    
    if right is None:
        right = len(arr) - 1
    
    # Add current call to stack
    call_info = f"binary_search(arr, {target}, {left}, {right})"
    call_stack.append(call_info)
    
    print(f"Call Stack Depth: {len(call_stack)}")
    print(f"Current Call: {call_info}\n")
    
    # Base case
    if left > right:
        call_stack.pop()
        return -1
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        print(f"Found! Returning {mid}")
        print(f"Call Stack: {call_stack}\n")
        call_stack.pop()
        return mid
    elif arr[mid] > target:
        result = binary_search_with_stack_trace(arr, target, left, mid - 1, call_stack)
    else:
        result = binary_search_with_stack_trace(arr, target, mid + 1, right, call_stack)
    
    call_stack.pop()
    return result

# Demo
arr = [1, 3, 5, 7, 9, 11, 13]
binary_search_with_stack_trace(arr, 7)
```

### Comparison: Iterative vs Recursive

```python
import time

def compare_implementations(arr, target):
    """Compare iterative and recursive implementations"""
    
    # Iterative
    start = time.time()
    result_iter = binary_search(arr, target)
    time_iter = time.time() - start
    
    # Recursive
    start = time.time()
    result_rec = binary_search_recursive(arr, target)
    time_rec = time.time() - start
    
    print(f"Target: {target}")
    print(f"Iterative: Index {result_iter}, Time: {time_iter:.6f}s")
    print(f"Recursive: Index {result_rec}, Time: {time_rec:.6f}s")
    print()

# Test with large array
arr = list(range(0, 1000000, 2))  # Even numbers up to 1,000,000
compare_implementations(arr, 999998)
```

### Tail Recursive Version

```python
def binary_search_tail_recursive(arr, target, left=0, right=None):
    """
    Tail recursive binary search
    Last operation is recursive call (can be optimized by compiler)
    """
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return binary_search_tail_recursive(arr, target, left, mid - 1)
    else:
        return binary_search_tail_recursive(arr, target, mid + 1, right)

# Test
arr = [1, 3, 5, 7, 9, 11, 13, 15]
print(binary_search_tail_recursive(arr, 11))  # 5
```

### Recursive Binary Search - Variations

#### Find First Occurrence (Recursive)

```python
def find_first_recursive(arr, target, left=0, right=None):
    """Find first occurrence using recursion"""
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    # If found and (it's first element OR previous element is different)
    if arr[mid] == target and (mid == 0 or arr[mid - 1] != target):
        return mid
    
    # If target is on left side or mid is not first occurrence
    if arr[mid] >= target:
        return find_first_recursive(arr, target, left, mid - 1)
    
    # Target is on right side
    return find_first_recursive(arr, target, mid + 1, right)

# Test
arr = [1, 2, 2, 2, 3, 4, 5]
print(find_first_recursive(arr, 2))  # 1
```

#### Find Last Occurrence (Recursive)

```python
def find_last_recursive(arr, target, left=0, right=None):
    """Find last occurrence using recursion"""
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    # If found and (it's last element OR next element is different)
    if arr[mid] == target and (mid == len(arr) - 1 or arr[mid + 1] != target):
        return mid
    
    # If target is on right side or mid is not last occurrence
    if arr[mid] <= target:
        return find_last_recursive(arr, target, mid + 1, right)
    
    # Target is on left side
    return find_last_recursive(arr, target, left, mid - 1)

# Test
arr = [1, 2, 2, 2, 3, 4, 5]
print(find_last_recursive(arr, 2))  # 3
```

### Maximum Recursion Depth

```python
import sys

# Check current recursion limit
print(f"Current recursion limit: {sys.getrecursionlimit()}")

# Set higher limit if needed (use with caution!)
# sys.setrecursionlimit(10000)

# Binary search depth is O(log n), so rarely an issue
# Example: array of 1 million elements needs only ~20 recursive calls
arr = list(range(1000000))
result = binary_search_recursive(arr, 999999)
print(f"Found at index: {result}")
```

---

## Summary

### Key Concepts - Week 9

1. **Recursion Fundamentals**
   - Function calls itself
   - Needs base case and recursive case
   - Uses call stack
   - Can be elegant but memory-intensive

2. **Recursive Problem Solving**
   - Break problem into smaller subproblems
   - Solve smallest case (base case)
   - Combine solutions

3. **Recursive Sorting**
   - Merge Sort: O(n log n), stable, requires extra space
   - Quick Sort: O(n log n) average, in-place

4. **Binary Search**
   - Requires sorted array
   - O(log n) time complexity
   - Eliminates half of search space each iteration
   - Can be implemented iteratively or recursively

### Recursion vs Iteration Comparison

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| **Code Style** | Often cleaner | Can be verbose |
| **Memory** | Uses call stack | Uses fixed memory |
| **Performance** | Function call overhead | Generally faster |
| **Termination** | Base case | Loop condition |
| **Risk** | Stack overflow | Infinite loop |
| **Natural For** | Trees, divide-and-conquer | Simple loops |

### When to Use Each Approach

**Use Recursion:**
- Problem naturally recursive (factorial, fibonacci)
- Tree/graph traversal
- Divide-and-conquer algorithms
- Code clarity is priority

**Use Iteration:**
- Simple loops
- Performance critical
- Large datasets (avoid stack overflow)
- Limited memory

### Quick Reference

```python
# Recursive Template
def recursive_function(n):
    # Base case
    if n <= 0:
        return base_value
    
    # Recursive case
    return some_operation(recursive_function(n - 1))

# Binary Search (Iterative)
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Binary Search (Recursive)
def binary_search_recursive(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
    if left > right:
        return -1
    mid = (left + right) // 2
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid + 1, right)
    else:
        return binary_search_recursive(arr, target, left, mid - 1)
```

### Time Complexities

| Algorithm | Best | Average | Worst | Space |
|-----------|------|---------|-------|-------|
| **Linear Search** | O(1) | O(n) | O(n) | O(1) |
| **Binary Search** | O(1) | O(log n) | O(log n) | O(1) iterative, O(log n) recursive |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) |

---
