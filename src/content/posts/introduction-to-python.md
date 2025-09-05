---
title: "Introduction to python"
published: 2025-09-04
draft: false
toc: true
description: "A simple introduction for those who already know programming and want a quick refresher on Python syntax and concepts."
tags: ['python']
---

## Installation
On Debian-based systems, you can install Python using apt. Else you can download it from the [official Python website](https://www.python.org/downloads/).

```bash
sudo apt update
sudo apt install python3
```

## Basic Syntax

### Print Function
The `print()` function is used to output data to the terminal.

```python
print("Hello, World!")
```

### Comments
Comments are created using the `#` symbol.

```python
# This is a comment
print("Hello, World!")  # This will print to the terminal
```

### Variables
Variables can be reassigned to new values and new types. There is no constante.

```python
a = 5
b, c = 1, 2
a = "Hello"
```

### Data Types
Python has various data types including integers, floats, strings, and booleans.

```python
x = 5               # int
y = 3.14            # float
is_valid = True     # boolean
z = "Hello"         # string '' or ""
multiline_string = """This is line one.
This is line two.
This is line three."""
```

To check the type of a variable.

```python
type(x)  # <class 'int'>
type(y)  # <class 'float'>
type(is_valid)  # <class 'bool'>
type(z)  # <class 'str'>
```

## Data Manipulation
### String manipulation

You can extract substrings using slicing.
```python
"Hello World!"[0:5]  # "Hello"
"Hello World!"[6:]   # "World!"
"Hello World!"[0]   # "H"
```

You can use f-strings (formatted string literals) to embed expressions inside string literals.
```python
name = "Alice"
age = 30
greeting = f"Hello, {name}. You are {age}."
```

```python
len("Hello")  # 5
```

You can concatenate strings using the `+` operator.
```python
"Hello" + " " + "World!"  # "Hello World!"
```

Justify left or right
```python
z.ljust(10)  # "Hello     "
z.rjust(10)  # "     Hello"
```

```python
z.upper()  # "HELLO"
z.lower()  # "hello"
```

### Number Manipulation
Python supports basic arithmetic operations.

```python
c = a + b  # Addition
c += 1     # Increment
d = a - b  # Subtraction
e = a * b  # Multiplication
f = a / b  # Division
```

## Data structures

### Lists
Lists are ordered collections of items.

```python
fruits = ["apple", "banana", "cherry"]
mixed = [1, "apple", 3.14]
```

You can manipulate lists using various methods.

```python
fruits.append("orange")         # Add an item at the end
fruits.insert(1, "blueberry")   # Insert an item

fruits.pop()                    # Remove the last item
fruits.pop(1)                   # Remove an item at a specific index
fruits.remove("banana")         # Remove an item

first_fruit = fruits[0]         # Access an item
fruits[1] = "blueberry"         # Change an item

len([0, 1, 2])                  # Get the number of items, start at 1
# Output: 3
```

### Tuples
Tuples are immutable ordered collections. They are indexed, they use a little bit less RAM.

```python
coordinates = (10.0, 20.0)
x, y = coordinates  # Unpacking

len(coordinates)  
# Output: 2
```

### Dictionaries
Dictionaries are key-value pairs.

```python
person = {
    "name": "Alice",
    "age": 30
}

person["name"]                 # "Alice"
person["city"] = "Wonderland"  # Assign a new key-value pair
```

## Control Structures

### Conditions
Conditional statements allow you to execute code based on certain conditions.

```python
if x > 0:
    print("Positive")
elif x < 0:
    print("Negative")
else:
    print("Zero")
```

### Logical operators
Logical operators are used to combine conditional statements.

```python
x > 0 and y > 0
x > 0 or y > 0
not x > 0
```

### Loops
Python supports both `for` and `while` loops.

```python
for i in range(7):
    if i == 3:
        continue
    if i == 5:
        break
    print(i)
# Output: 0 1 2 4

list_of_lists = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
for a, b, c in list_of_lists:
    print(a, b, c)

while x > 0:
    print(x)
    x -= 1
```

### Functions
Functions are defined using the `def` keyword.

```python
def greet(name):
    print("Hello, " + name)

greet("Alice")

# Output: Hello, Alice
```

### Try and Except
You can handle exceptions using try and except blocks.

```python
try:
    mem = psutil.virtual_memory()
    with open('file.txt', 'r') as file:
        content = file.read()
except (psutil.AccessDenied, PermissionError) as e:
    print(f"Permission error: {e}", file=sys.stderr)
except Exception as e:
    print("An error occurred:", e)
finally:
    print("Execution completed.")
```

### With statement
The `with` statement is used for resource management and exception handling.

```python
with open('file.txt', 'r') as file:
    content = file.read()
# File is automatically closed after the block
```

## Virtual Environments
It's a good practice to use virtual environments to manage dependencies for different projects.

```bash
# To create a virtual environment in a directory named 'myenv'
python3 -m venv myenv

# To activate the virtual environment
source myenv/bin/activate  # On Windows use `myenv\Scripts\activate`

# To exit the virtual environment
deactivate
```

## Standard Library
You can import modules to use additional functionality.

### sys
```python
import sys 

# sys to access system-specific parameters and functions
sys.platform  # 'linux', 'win32', 'darwin', etc.
sys.version   # Python version
sys.exit()    # Exit the program
sys.argv      # Command line arguments

sys.stdout = open('output.txt', 'w')  # Redirect output to a file
sys.stderr = open('error.txt', 'w')   # Redirect errors to a file
```

### os
```python
# os to interact with the operating system
os.getcwd()             # Get current working directory
os.listdir()            # List files in the current directory
os.mkdir('new_folder')  # Create a new directory

os.environ['PATH'] += os.pathsep + '/new/path'  # Modify environment variables
```

### subprocess
```python
# subprocess to run external commands
subprocess.run(['ls', '-l'])         # List files in long format on Unix

result = subprocess.run(['toto'], capture_output=True, text=True)  # List files on Windows
if result.returncode == 0:
    subprocess.run(['echo', 'Command succeeded'])
    print(result.stdout)
else:
    print("Error:", result.stderr)
```

### shutil
```python
import shutil

shutil.copy('source.txt', 'destination.txt')  # Copy a file
shutil.move('old_folder', 'new_folder')       # Move a folder
shutil.rmtree('folder_to_delete')             # Delete a folder and its contents
```

You can use external libraries using the package manager pip.

## External Libraries

### psutil
Get information about system utilization (CPU, memory, disks, network, sensors) and running processes.

```bash
pip install psutil
```

```python
import psutil

psutil.cpu_percent(interval=1)  # CPU usage percentage
psutil.virtual_memory()          # Memory usage
psutil.disk_usage('/')           # Disk usage
```
