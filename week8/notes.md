# Week 8: File Handling in Python - Complete Notes

## Table of Contents
1. [Introduction to File Handling](#introduction-to-file-handling)
2. [Opening and Closing Files](#opening-and-closing-files)
3. [Reading Files](#reading-files)
4. [Writing to Files](#writing-to-files)
5. [File Modes](#file-modes)
6. [Handling Large Files with readline()](#handling-large-files-with-readline)
7. [File Positioning with seek() and tell()](#file-positioning-with-seek-and-tell)
8. [Working with Different File Types](#working-with-different-file-types)
9. [Error Handling in File Operations](#error-handling-in-file-operations)
10. [Best Practices](#best-practices)

---

## Introduction to File Handling

### What is File Handling?

File handling is the process of working with files stored on disk - creating, reading, writing, updating, and deleting files.

**Why File Handling?**
- Store data permanently (persistence)
- Share data between programs
- Process large datasets
- Create logs and reports
- Configuration management
- Data backup and recovery

### Types of Files

1. **Text Files** - Contain human-readable text (`.txt`, `.csv`, `.json`, `.xml`)
2. **Binary Files** - Contain binary data (`.jpg`, `.png`, `.pdf`, `.exe`)

---

## Opening and Closing Files

### The `open()` Function

```python
file_object = open(filename, mode)
```

**Parameters:**
- `filename` - Path to the file (string)
- `mode` - How to open the file (optional, default is 'r')

**Returns:** A file object

### Basic Example

```python
# Opening a file
file = open("example.txt", "r")

# Perform operations
content = file.read()
print(content)

# IMPORTANT: Always close the file
file.close()
```

### Using `with` Statement (Recommended)

The `with` statement automatically closes the file, even if an error occurs.

```python
# Best practice - file closes automatically
with open("example.txt", "r") as file:
    content = file.read()
    print(content)
# File is automatically closed here

# No need to call file.close()
```

**Why use `with`?**
- Automatic file closing
- Proper exception handling
- Cleaner code
- Prevents resource leaks

### Checking if File Exists

```python
import os

# Check if file exists
if os.path.exists("example.txt"):
    print("File exists")
else:
    print("File does not exist")

# Check if it's a file (not directory)
if os.path.isfile("example.txt"):
    print("It's a file")

# Check if it's a directory
if os.path.isdir("my_folder"):
    print("It's a directory")
```

---

## Reading Files

### Method 1: `read()` - Read Entire File

Reads the entire file content as a single string.

```python
# Read entire file
with open("example.txt", "r") as file:
    content = file.read()
    print(content)

# Read specific number of characters
with open("example.txt", "r") as file:
    first_10_chars = file.read(10)  # Read first 10 characters
    print(first_10_chars)
```

**Example:**
```python
# example.txt contains:
# Hello World
# This is line 2
# This is line 3

with open("example.txt", "r") as file:
    content = file.read()
    print(content)

# Output:
# Hello World
# This is line 2
# This is line 3
```

**Pros:** Simple, good for small files  
**Cons:** Loads entire file into memory (problem for large files)

### Method 2: `readline()` - Read One Line at a Time

Reads a single line from the file (including newline character `\n`).

```python
with open("example.txt", "r") as file:
    line1 = file.readline()  # Read first line
    line2 = file.readline()  # Read second line
    line3 = file.readline()  # Read third line
    
    print(line1)  # Includes \n
    print(line2)
    print(line3)
```

**Removing newline character:**
```python
with open("example.txt", "r") as file:
    line = file.readline()
    clean_line = line.strip()  # Remove \n and whitespace
    print(clean_line)
```

**Reading all lines with readline():**
```python
with open("example.txt", "r") as file:
    while True:
        line = file.readline()
        
        # readline() returns empty string when EOF reached
        if line == "":
            break
        
        print(line.strip())
```

**Better approach:**
```python
with open("example.txt", "r") as file:
    while True:
        line = file.readline()
        if not line:  # Empty string is falsy
            break
        print(line.strip())
```

### Method 3: `readlines()` - Read All Lines as List

Reads all lines and returns them as a list.

```python
with open("example.txt", "r") as file:
    lines = file.readlines()  # Returns list of lines
    print(lines)

# Output: ['Hello World\n', 'This is line 2\n', 'This is line 3\n']

# Process each line
for line in lines:
    print(line.strip())
```

**Note:** `readlines()` loads entire file into memory.

### Method 4: Iterating Over File Object (Best for Large Files)

The file object itself is an iterator!

```python
with open("example.txt", "r") as file:
    for line in file:  # Memory efficient!
        print(line.strip())
```

**This is the most Pythonic and memory-efficient way** to read files line by line.

### Comparison of Reading Methods

```python
# Method 1: read() - entire file as string
with open("example.txt", "r") as file:
    content = file.read()
    print(type(content))  # <class 'str'>

# Method 2: readline() - one line at a time
with open("example.txt", "r") as file:
    line = file.readline()
    print(type(line))  # <class 'str'>

# Method 3: readlines() - all lines as list
with open("example.txt", "r") as file:
    lines = file.readlines()
    print(type(lines))  # <class 'list'>

# Method 4: iteration - yields one line at a time
with open("example.txt", "r") as file:
    for line in file:
        print(type(line))  # <class 'str'>
```

### Reading Files - Practical Examples

#### Example 1: Count Lines in a File

```python
def count_lines(filename):
    with open(filename, "r") as file:
        count = 0
        for line in file:
            count += 1
    return count

# Or shorter:
def count_lines_v2(filename):
    with open(filename, "r") as file:
        return len(file.readlines())

# Or even shorter:
def count_lines_v3(filename):
    with open(filename, "r") as file:
        return sum(1 for line in file)

print(f"Total lines: {count_lines('example.txt')}")
```

#### Example 2: Count Words in a File

```python
def count_words(filename):
    with open(filename, "r") as file:
        text = file.read()
        words = text.split()
        return len(words)

print(f"Total words: {count_words('example.txt')}")
```

#### Example 3: Search for a Word

```python
def search_word(filename, word):
    with open(filename, "r") as file:
        for line_num, line in enumerate(file, 1):
            if word in line:
                print(f"Line {line_num}: {line.strip()}")

search_word("example.txt", "Python")
```

#### Example 4: Read Specific Lines

```python
def read_lines(filename, start, end):
    """Read lines from start to end (inclusive)"""
    with open(filename, "r") as file:
        for i, line in enumerate(file, 1):
            if start <= i <= end:
                print(f"Line {i}: {line.strip()}")
            if i > end:
                break

read_lines("example.txt", 5, 10)  # Read lines 5-10
```

---

## Writing to Files

### Method 1: `write()` - Write String to File

```python
# Writing to a file (creates new file or overwrites existing)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is line 2\n")

# Note: write() doesn't add newline automatically
```

**Important:** `write()` does NOT add newline (`\n`) automatically!

```python
with open("output.txt", "w") as file:
    file.write("Line 1")
    file.write("Line 2")  # This will appear on same line!

# output.txt will contain: Line 1Line 2

# Correct way:
with open("output.txt", "w") as file:
    file.write("Line 1\n")
    file.write("Line 2\n")
```

### Method 2: `writelines()` - Write List of Strings

```python
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]

with open("output.txt", "w") as file:
    file.writelines(lines)

# Note: writelines() doesn't add newlines either!
# You must include \n in each string
```

**Without newlines:**
```python
lines = ["Line 1", "Line 2", "Line 3"]

with open("output.txt", "w") as file:
    file.writelines(lines)

# output.txt will contain: Line 1Line 2Line 3 (all on one line!)

# Correct way:
with open("output.txt", "w") as file:
    for line in lines:
        file.write(line + "\n")

# Or:
with open("output.txt", "w") as file:
    file.writelines(line + "\n" for line in lines)
```

### Writing Numbers

```python
# Numbers must be converted to strings
number = 42

with open("output.txt", "w") as file:
    # file.write(number)  # Error: expected str, got int
    file.write(str(number))  # Correct
    file.write("\n")

# Writing multiple numbers
numbers = [1, 2, 3, 4, 5]

with open("numbers.txt", "w") as file:
    for num in numbers:
        file.write(str(num) + "\n")
```

### Appending to Files

Use mode `"a"` to append (add to end) instead of overwriting.

```python
# Append to existing file
with open("output.txt", "a") as file:
    file.write("This line is appended\n")
    file.write("Another appended line\n")
```

### Writing - Practical Examples

#### Example 1: Create a Simple Log File

```python
from datetime import datetime

def log_message(message):
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    with open("app.log", "a") as file:
        file.write(f"[{timestamp}] {message}\n")

log_message("Application started")
log_message("User logged in")
log_message("Error: File not found")
```

#### Example 2: Save List to File

```python
def save_list(filename, items):
    with open(filename, "w") as file:
        for item in items:
            file.write(str(item) + "\n")

shopping_list = ["Milk", "Eggs", "Bread", "Butter"]
save_list("shopping.txt", shopping_list)
```

#### Example 3: Copy File Content

```python
def copy_file(source, destination):
    with open(source, "r") as src:
        with open(destination, "w") as dst:
            content = src.read()
            dst.write(content)

# Or line by line (better for large files):
def copy_file_v2(source, destination):
    with open(source, "r") as src:
        with open(destination, "w") as dst:
            for line in src:
                dst.write(line)

copy_file("original.txt", "backup.txt")
```

#### Example 4: Write Dictionary to File

```python
student = {
    "name": "Alice",
    "age": 20,
    "grade": "A",
    "courses": ["Math", "Physics", "Chemistry"]
}

with open("student.txt", "w") as file:
    for key, value in student.items():
        file.write(f"{key}: {value}\n")
```

---

## File Modes

### Common File Modes

| Mode | Description | Creates File | Overwrites | Read | Write |
|------|-------------|--------------|------------|------|-------|
| `'r'` | Read only (default) | No | No | ✓ | ✗ |
| `'w'` | Write only | Yes | Yes | ✗ | ✓ |
| `'a'` | Append only | Yes | No | ✗ | ✓ |
| `'r+'` | Read and write | No | No | ✓ | ✓ |
| `'w+'` | Write and read | Yes | Yes | ✓ | ✓ |
| `'a+'` | Append and read | Yes | No | ✓ | ✓ |

### Binary Modes

Add `'b'` to any mode for binary files:
- `'rb'` - Read binary
- `'wb'` - Write binary
- `'ab'` - Append binary
- `'rb+'` - Read/write binary

### Detailed Mode Explanations

#### Mode `'r'` - Read (Default)

```python
# File must exist, or FileNotFoundError
with open("example.txt", "r") as file:
    content = file.read()

# Same as:
with open("example.txt") as file:  # 'r' is default
    content = file.read()
```

**Characteristics:**
- File must exist
- Cannot write
- File pointer at beginning

#### Mode `'w'` - Write

```python
# Creates file if doesn't exist
# OVERWRITES if file exists!
with open("output.txt", "w") as file:
    file.write("New content")
```

**Characteristics:**
- Creates file if doesn't exist
- **Overwrites existing file** (be careful!)
- Cannot read
- File pointer at beginning

#### Mode `'a'` - Append

```python
# Adds to end of file
with open("log.txt", "a") as file:
    file.write("New log entry\n")
```

**Characteristics:**
- Creates file if doesn't exist
- Appends to end (doesn't overwrite)
- Cannot read
- File pointer at end

#### Mode `'r+'` - Read and Write

```python
with open("data.txt", "r+") as file:
    content = file.read()  # Read
    file.write("New line\n")  # Write
```

**Characteristics:**
- File must exist
- Can read and write
- File pointer at beginning
- Doesn't overwrite automatically

#### Mode `'w+'` - Write and Read

```python
with open("output.txt", "w+") as file:
    file.write("Hello\n")  # Write
    file.seek(0)  # Move to beginning
    content = file.read()  # Read
```

**Characteristics:**
- Creates file if doesn't exist
- **Overwrites existing file**
- Can write and read
- File pointer at beginning

#### Mode `'a+'` - Append and Read

```python
with open("log.txt", "a+") as file:
    file.write("New entry\n")  # Append
    file.seek(0)  # Move to beginning
    content = file.read()  # Read
```

**Characteristics:**
- Creates file if doesn't exist
- Appends (doesn't overwrite)
- Can append and read
- File pointer at end

### Mode Examples

```python
# Example 1: Safe write (doesn't overwrite accidentally)
import os

def safe_write(filename, content):
    if os.path.exists(filename):
        print(f"Warning: {filename} already exists!")
        response = input("Overwrite? (y/n): ")
        if response.lower() != 'y':
            print("Write cancelled")
            return
    
    with open(filename, "w") as file:
        file.write(content)
    print(f"Written to {filename}")

safe_write("important.txt", "Important data")

# Example 2: Using r+ mode
with open("data.txt", "r+") as file:
    lines = file.readlines()  # Read all lines
    file.seek(0)  # Go back to start
    file.write("First line modified\n")  # Overwrite first line
    file.writelines(lines[1:])  # Write rest of lines
```

---

## Handling Large Files with readline()

### Why readline() for Large Files?

**Problem with read():**
```python
# DON'T do this for large files!
with open("huge_file.txt", "r") as file:
    content = file.read()  # Loads entire file into memory!
    # For a 10GB file, this needs 10GB of RAM!
```

**Solution - readline():**
```python
# Memory efficient - processes one line at a time
with open("huge_file.txt", "r") as file:
    while True:
        line = file.readline()
        if not line:  # Empty string when EOF
            break
        process(line)  # Only one line in memory at a time!
```

### Using readline() - Basic Pattern

```python
def process_large_file(filename):
    with open(filename, "r") as file:
        line_count = 0
        
        while True:
            line = file.readline()
            
            # Check for end of file
            if not line:
                break
            
            # Process the line
            line_count += 1
            print(f"Line {line_count}: {line.strip()}")
        
        print(f"Total lines processed: {line_count}")

process_large_file("large_data.txt")
```

### readline() vs File Iterator

Both are memory efficient:

```python
# Method 1: Using readline()
with open("large_file.txt", "r") as file:
    while True:
        line = file.readline()
        if not line:
            break
        process(line)

# Method 2: Using file iterator (More Pythonic!)
with open("large_file.txt", "r") as file:
    for line in file:
        process(line)
```

**File iterator is usually preferred** (cleaner, more Pythonic), but `readline()` gives more control.

### Practical Examples with readline()

#### Example 1: Process Large CSV File

```python
def process_csv(filename):
    with open(filename, "r") as file:
        # Read header
        header = file.readline()
        print(f"Columns: {header.strip()}")
        
        # Process data rows
        row_count = 0
        while True:
            line = file.readline()
            if not line:
                break
            
            # Process row
            values = line.strip().split(",")
            row_count += 1
            
            # Example: print every 1000th row
            if row_count % 1000 == 0:
                print(f"Processed {row_count} rows...")
        
        print(f"Total rows: {row_count}")

process_csv("large_data.csv")
```

#### Example 2: Find Pattern in Large File

```python
def find_pattern(filename, pattern):
    with open(filename, "r") as file:
        line_number = 0
        matches = 0
        
        while True:
            line = file.readline()
            if not line:
                break
            
            line_number += 1
            
            if pattern in line:
                matches += 1
                print(f"Line {line_number}: {line.strip()}")
        
        print(f"\nFound {matches} matches")

find_pattern("server.log", "ERROR")
```

#### Example 3: Read File in Chunks

```python
def read_in_chunks(filename, chunk_size=1024):
    """Read file in chunks of specified size (bytes)"""
    with open(filename, "r") as file:
        while True:
            chunk = file.read(chunk_size)  # Read chunk_size characters
            if not chunk:
                break
            
            # Process chunk
            print(f"Processing {len(chunk)} characters...")
            # Do something with chunk
    
    print("File processing complete")

read_in_chunks("large_file.txt", 4096)  # 4KB chunks
```

#### Example 4: Filter Large File

```python
def filter_file(input_file, output_file, condition):
    """Copy only lines that meet condition"""
    with open(input_file, "r") as infile:
        with open(output_file, "w") as outfile:
            line_count = 0
            written_count = 0
            
            while True:
                line = infile.readline()
                if not line:
                    break
                
                line_count += 1
                
                # Check condition
                if condition(line):
                    outfile.write(line)
                    written_count += 1
                
                # Progress indicator
                if line_count % 10000 == 0:
                    print(f"Processed {line_count} lines...")
            
            print(f"\nTotal lines: {line_count}")
            print(f"Lines written: {written_count}")

# Example usage: copy only lines containing "ERROR"
filter_file(
    "server.log",
    "errors.log",
    lambda line: "ERROR" in line
)
```

#### Example 5: Reading Large File with Progress Bar

```python
import os

def process_with_progress(filename):
    # Get file size
    file_size = os.path.getsize(filename)
    
    with open(filename, "r") as file:
        bytes_read = 0
        
        while True:
            line = file.readline()
            if not line:
                break
            
            bytes_read += len(line.encode('utf-8'))
            
            # Calculate progress
            progress = (bytes_read / file_size) * 100
            
            # Display progress
            print(f"\rProgress: {progress:.2f}%", end="")
            
            # Process line
            # ...
        
        print("\nComplete!")

process_with_progress("large_file.txt")
```

### Memory Comparison

```python
import sys

# Method 1: read() - loads entire file
with open("data.txt", "r") as file:
    content = file.read()
    print(f"Memory used: {sys.getsizeof(content)} bytes")

# Method 2: readline() - one line at a time
with open("data.txt", "r") as file:
    while True:
        line = file.readline()
        if not line:
            break
        print(f"Memory per line: {sys.getsizeof(line)} bytes")
        # Only one line in memory at a time!
```

---

## File Positioning with seek() and tell()

### Understanding File Pointer

Every open file has a **file pointer** that tracks the current position in the file.

```python
with open("example.txt", "r") as file:
    # File pointer starts at 0 (beginning)
    print(file.read(5))  # Read 5 chars, pointer moves to position 5
    print(file.read(5))  # Read next 5 chars, pointer moves to position 10
```

### The `tell()` Method

Returns the current position of the file pointer (in bytes).

```python
with open("example.txt", "r") as file:
    print(f"Position: {file.tell()}")  # 0 (start)
    
    file.read(10)
    print(f"Position: {file.tell()}")  # 10
    
    file.read(5)
    print(f"Position: {file.tell()}")  # 15
```

**Example:**
```python
# example.txt contains: "Hello World"

with open("example.txt", "r") as file:
    print(file.tell())  # 0
    
    char = file.read(1)  # Read 'H'
    print(f"Read: {char}, Position: {file.tell()}")  # 1
    
    word = file.read(5)  # Read 'ello '
    print(f"Read: {word}, Position: {file.tell()}")  # 6
```

### The `seek()` Method

Moves the file pointer to a specific position.

**Syntax:**
```python
file.seek(offset, whence)
```

**Parameters:**
- `offset` - Number of bytes to move
- `whence` - Reference point (optional, default is 0)
  - `0` - Beginning of file (default)
  - `1` - Current position
  - `2` - End of file

#### seek() with whence=0 (from beginning)

```python
# example.txt contains: "Hello World"

with open("example.txt", "r") as file:
    file.seek(6)  # Move to position 6
    print(file.read())  # "World"
    
    file.seek(0)  # Move back to start
    print(file.read())  # "Hello World"
```

#### seek() with whence=1 (from current position)

```python
with open("example.txt", "rb") as file:  # Must use binary mode!
    file.read(5)  # Position at 5
    file.seek(2, 1)  # Move 2 positions forward from current
    print(file.read())
```

**Note:** `whence=1` and `whence=2` only work in **binary mode** (`'rb'`).

#### seek() with whence=2 (from end)

```python
with open("example.txt", "rb") as file:  # Binary mode required
    file.seek(-5, 2)  # Move 5 positions back from end
    print(file.read())
```

### Practical Examples with seek() and tell()

#### Example 1: Read File from Specific Position

```python
def read_from_position(filename, start_position, num_chars):
    with open(filename, "r") as file:
        file.seek(start_position)
        content = file.read(num_chars)
        return content

# Read 10 characters starting from position 20
content = read_from_position("data.txt", 20, 10)
print(content)
```

#### Example 2: Read Last N Lines of File

```python
def read_last_lines(filename, n):
    with open(filename, "rb") as file:  # Binary mode
        # Go to end
        file.seek(0, 2)
        file_size = file.tell()
        
        # Read backwards to find n newlines
        lines_found = 0
        position = file_size - 1
        
        while position >= 0 and lines_found < n:
            file.seek(position)
            char = file.read(1)
            
            if char == b'\n':
                lines_found += 1
            
            position -= 1
        
        # Read from this position to end
        file.seek(position + 2)
        lines = file.read().decode('utf-8')
        return lines

# Get last 5 lines
last_lines = read_last_lines("log.txt", 5)
print(last_lines)
```

#### Example 3: Modify Specific Part of File

```python
def modify_file(filename, position, new_text):
    # Read entire file
    with open(filename, "r") as file:
        content = file.read()
    
    # Modify content
    modified = content[:position] + new_text + content[position + len(new_text):]
    
    # Write back
    with open(filename, "w") as file:
        file.write(modified)

# Replace 5 characters starting at position 10
modify_file("data.txt", 10, "XXXXX")
```

#### Example 4: Read File in Reverse

```python
def read_reverse(filename):
    with open(filename, "rb") as file:
        # Go to end
        file.seek(0, 2)
        position = file.tell()
        
        # Read backwards
        while position >= 0:
            file.seek(position)
            char = file.read(1)
            
            if char:
                print(char.decode('utf-8'), end='')
            
            position -= 1

read_reverse("example.txt")
```

#### Example 5: Get File Statistics

```python
def file_stats(filename):
    with open(filename, "r") as file:
        # Get file size
        file.seek(0, 2)  # Go to end
        size = file.tell()
        
        # Count lines
        file.seek(0)  # Back to start
        lines = sum(1 for line in file)
        
        # Count words
        file.seek(0)
        words = sum(len(line.split()) for line in file)
        
        # Count characters
        file.seek(0)
        chars = len(file.read())
        
        return {
            "size_bytes": size,
            "lines": lines,
            "words": words,
            "characters": chars
        }

stats = file_stats("document.txt")
print(f"File statistics: {stats}")
```

#### Example 6: Implementing tail Command (Last N Lines)

```python
def tail(filename, n=10):
    """Show last n lines of file (like Unix tail command)"""
    with open(filename, "r") as file:
        # Read all lines
        lines = file.readlines()
        
        # Print last n lines
        for line in lines[-n:]:
            print(line, end='')

# Show last 10 lines
tail("log.txt", 10)
```

#### Example 7: Implementing head Command (First N Lines)

```python
def head(filename, n=10):
    """Show first n lines of file (like Unix head command)"""
    with open(filename, "r") as file:
        for i in range(n):
            line = file.readline()
            if not line:
                break
            print(line, end='')

# Show first 10 lines
head("log.txt", 10)
```

#### Example 8: Random Access to Lines

```python
class RandomAccessFile:
    def __init__(self, filename):
        self.filename = filename
        self.line_positions = []
        
        # Build index of line positions
        with open(filename, "r") as file:
            position = 0
            while True:
                self.line_positions.append(position)
                line = file.readline()
                if not line:
                    break
                position = file.tell()
    
    def get_line(self, line_number):
        """Get specific line by number (0-indexed)"""
        if line_number >= len(self.line_positions):
            return None
        
        with open(self.filename, "r") as file:
            file.seek(self.line_positions[line_number])
            return file.readline()
    
    def get_lines(self, start, end):
        """Get range of lines"""
        lines = []
        for i in range(start, min(end, len(self.line_positions))):
            lines.append(self.get_line(i))
        return lines

# Usage
raf = RandomAccessFile("data.txt")
print(raf.get_line(100))  # Get line 100 instantly!
print(raf.get_lines(50, 60))  # Get lines 50-60
```

### seek() and tell() - Key Points

```python
# Key Point 1: tell() returns current position
with open("example.txt", "r") as file:
    print(file.tell())  # 0 (start)
    file.read(5)
    print(file.tell())  # 5

# Key Point 2: seek(0) goes to beginning
with open("example.txt", "r") as file:
    file.read()  # Read all
    print(file.tell())  # At end
    file.seek(0)  # Back to start
    print(file.tell())  # 0

# Key Point 3: Reading moves pointer
with open("example.txt", "r") as file:
    line1 = file.readline()  # Pointer after line 1
    line2 = file.readline()  # Pointer after line 2
    # Can't read line 1 again without seek(0)

# Key Point 4: Writing also moves pointer
with open("example.txt", "w") as file:
    print(file.tell())  # 0
    file.write("Hello")
    print(file.tell())  # 5

# Key Point 5: Append mode starts at end
with open("example.txt", "a") as file:
    print(file.tell())  # At end of file
```

---

## Working with Different File Types

### Text Files (.txt)

```python
# Write text file
with open("notes.txt", "w") as file:
    file.write("My notes\n")
    file.write("Line 2\n")

# Read text file
with open("notes.txt", "r") as file:
    content = file.read()
    print(content)
```

### CSV Files

```python
# Manual CSV handling
def write_csv(filename, data):
    with open(filename, "w") as file:
        for row in data:
            line = ",".join(str(item) for item in row)
            file.write(line + "\n")

def read_csv(filename):
    rows = []
    with open(filename, "r") as file:
        for line in file:
            row = line.strip().split(",")
            rows.append(row)
    return rows

# Usage
data = [
    ["Name", "Age", "City"],
    ["Alice", "25", "NYC"],
    ["Bob", "30", "LA"]
]

write_csv("data.csv", data)
rows = read_csv("data.csv")
print(rows)

# Using csv module (better!)
import csv

# Write CSV
with open("data.csv", "w", newline='') as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Age", "City"])
    writer.writerow(["Alice", 25, "NYC"])

# Read CSV
with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

### JSON Files

```python
import json

# Write JSON
data = {
    "name": "Alice",
    "age": 25,
    "courses": ["Math", "Physics"]
}

with open("data.json", "w") as file:
    json.dump(data, file, indent=4)

# Read JSON
with open("data.json", "r") as file:
    data = json.load(file)
    print(data)
```

### Binary Files

```python
# Write binary
data = bytes([65, 66, 67, 68, 69])  # ABCDE in ASCII

with open("data.bin", "wb") as file:
    file.write(data)

# Read binary
with open("data.bin", "rb") as file:
    content = file.read()
    print(content)  # b'ABCDE'
    print(list(content))  # [65, 66, 67, 68, 69]
```

### Image Files (Binary)

```python
# Copy image file
def copy_image(source, destination):
    with open(source, "rb") as src:
        with open(destination, "wb") as dst:
            # Read in chunks for large files
            while True:
                chunk = src.read(4096)  # 4KB chunks
                if not chunk:
                    break
                dst.write(chunk)

copy_image("original.jpg", "copy.jpg")
```

---

## Error Handling in File Operations

### Common File Errors

1. **FileNotFoundError** - File doesn't exist
2. **PermissionError** - No permission to access file
3. **IsADirectoryError** - Path is a directory, not a file
4. **IOError** - General I/O error

### Basic Error Handling

```python
# Without error handling (bad!)
file = open("nonexistent.txt", "r")  # Crashes if file doesn't exist!

# With error handling (good!)
try:
    with open("nonexistent.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("Error: File not found!")
```

### Comprehensive Error Handling

```python
def safe_read_file(filename):
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"Error: '{filename}' not found")
        return None
    except PermissionError:
        print(f"Error: No permission to read '{filename}'")
        return None
    except IsADirectoryError:
        print(f"Error: '{filename}' is a directory, not a file")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None

# Usage
content = safe_read_file("data.txt")
if content:
    print(content)
```

### Error Handling for Writing

```python
def safe_write_file(filename, content):
    try:
        with open(filename, "w") as file:
            file.write(content)
        print(f"Successfully written to {filename}")
        return True
    except PermissionError:
        print(f"Error: No permission to write to '{filename}'")
        return False
    except IOError as e:
        print(f"I/O error: {e}")
        return False
    except Exception as e:
        print(f"Unexpected error: {e}")
        return False

# Usage
if safe_write_file("output.txt", "Hello, World!"):
    print("Write successful")
else:
    print("Write failed")
```

### Checking File Existence Before Operations

```python
import os

def read_if_exists(filename):
    if not os.path.exists(filename):
        print(f"File '{filename}' does not exist")
        return None
    
    if not os.path.isfile(filename):
        print(f"'{filename}' is not a file")
        return None
    
    try:
        with open(filename, "r") as file:
            return file.read()
    except Exception as e:
        print(f"Error reading file: {e}")
        return None

content = read_if_exists("data.txt")
```

### Finally Block for Cleanup

```python
# Using finally (old style - not needed with 'with')
file = None
try:
    file = open("data.txt", "r")
    content = file.read()
    print(content)
except FileNotFoundError:
    print("File not found")
finally:
    if file:
        file.close()  # Ensures file is closed
        print("File closed")

# Better: Use 'with' statement (automatic cleanup)
try:
    with open("data.txt", "r") as file:
        content = file.read()
        print(content)
except FileNotFoundError:
    print("File not found")
# File automatically closed!
```

---

## Best Practices

### 1. Always Use `with` Statement

```python
# Bad
file = open("data.txt", "r")
content = file.read()
file.close()  # Might not execute if error occurs!

# Good
with open("data.txt", "r") as file:
    content = file.read()
# File automatically closed
```

### 2. Handle Errors Appropriately

```python
# Bad
content = open("file.txt").read()  # Crashes if file doesn't exist

# Good
try:
    with open("file.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("File not found")
    content = ""
```

### 3. Use Appropriate File Modes

```python
# Bad - overwrites existing file!
with open("important.txt", "w") as file:
    file.write("Oops, old data gone!")

# Good - append instead
with open("important.txt", "a") as file:
    file.write("New data\n")

# Better - check before writing
import os
if os.path.exists("important.txt"):
    mode = "a"  # Append if exists
else:
    mode = "w"  # Create new if doesn't exist

with open("important.txt", mode) as file:
    file.write("Data\n")
```

### 4. Process Large Files Efficiently

```python
# Bad - loads entire file into memory
with open("huge_file.txt", "r") as file:
    lines = file.readlines()  # Entire file in memory!
    for line in lines:
        process(line)

# Good - process line by line
with open("huge_file.txt", "r") as file:
    for line in file:  # One line at a time
        process(line)
```

### 5. Use Binary Mode for Binary Files

```python
# Bad - corrupts binary files!
with open("image.jpg", "r") as file:
    content = file.read()

# Good
with open("image.jpg", "rb") as file:
    content = file.read()
```

### 6. Close Files Properly

```python
# Bad
file1 = open("file1.txt", "r")
file2 = open("file2.txt", "r")
# Files might not close if error occurs

# Good
with open("file1.txt", "r") as file1:
    with open("file2.txt", "r") as file2:
        # Both automatically closed

# Also good (Python 3.1+)
with open("file1.txt", "r") as file1, open("file2.txt", "r") as file2:
    # Both automatically closed
```

### 7. Use Path Libraries for File Paths

```python
# Bad - hardcoded paths
file_path = "C:\\Users\\Name\\Documents\\file.txt"  # Windows only!

# Good - use os.path
import os
file_path = os.path.join("Documents", "file.txt")

# Better - use pathlib (Python 3.4+)
from pathlib import Path
file_path = Path("Documents") / "file.txt"
```

### 8. Validate File Paths

```python
import os

def safe_file_operation(filename):
    # Check if file exists
    if not os.path.exists(filename):
        print("File doesn't exist")
        return
    
    # Check if it's a file (not directory)
    if not os.path.isfile(filename):
        print("Not a file")
        return
    
    # Check read permission
    if not os.access(filename, os.R_OK):
        print("No read permission")
        return
    
    # Now safe to read
    with open(filename, "r") as file:
        return file.read()
```

### 9. Use Encoding When Necessary

```python
# Default encoding may vary by system
with open("data.txt", "r") as file:
    content = file.read()

# Explicit encoding (better for portability)
with open("data.txt", "r", encoding="utf-8") as file:
    content = file.read()

# Handling non-UTF8 files
with open("legacy.txt", "r", encoding="latin-1") as file:
    content = file.read()
```

### 10. Use Context Managers for Multiple Files

```python
# Reading from one file, writing to another
with open("input.txt", "r") as infile:
    with open("output.txt", "w") as outfile:
        for line in infile:
            outfile.write(line.upper())

# Shorter syntax
with open("input.txt", "r") as infile, open("output.txt", "w") as outfile:
    for line in infile:
        outfile.write(line.upper())
```

---

## Summary

### Key Concepts

1. **File Operations**
   - Open: `open(filename, mode)`
   - Read: `read()`, `readline()`, `readlines()`, iteration
   - Write: `write()`, `writelines()`
   - Close: `close()` or use `with` statement

2. **File Modes**
   - `'r'` - Read (default)
   - `'w'` - Write (overwrites)
   - `'a'` - Append
   - `'r+'`, `'w+'`, `'a+'` - Read/Write combinations
   - `'b'` - Binary mode

3. **Large File Handling**
   - Use `readline()` or file iteration
   - Avoid loading entire file with `read()`
   - Process line by line or in chunks

4. **File Positioning**
   - `tell()` - Get current position
   - `seek(offset, whence)` - Move to position
   - Useful for random access and file manipulation

5. **Best Practices**
   - Always use `with` statement
   - Handle exceptions
   - Use appropriate file modes
   - Process large files efficiently
   - Close files properly

### Quick Reference

```python
# Reading
with open("file.txt", "r") as f:
    content = f.read()              # Entire file
    line = f.readline()             # One line
    lines = f.readlines()           # All lines as list
    for line in f:                  # Iterate (best for large files)
        process(line)

# Writing
with open("file.txt", "w") as f:
    f.write("text\n")               # Write string
    f.writelines(["line1\n", "line2\n"])  # Write list

# Appending
with open("file.txt", "a") as f:
    f.write("new line\n")

# File positioning
with open("file.txt", "r") as f:
    pos = f.tell()                  # Get position
    f.seek(0)                       # Go to start
    f.seek(10)                      # Go to position 10
    f.seek(-5, 2)                   # 5 bytes before end (binary mode)

# Error handling
try:
    with open("file.txt", "r") as f:
        content = f.read()
except FileNotFoundError:
    print("File not found")
```

---

*End of Week 8 Notes*

**Happy Coding! 🚀**
