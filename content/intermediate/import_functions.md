---
section: Intermediate Python
nav_order: 2
title: Importing Functions from Modules
topics: import, function, module
---

Python's power comes from its vast ecosystem of modules. Learning to import and use functions from modules effectively is crucial for productive programming.

{% include question.html header="Basic Import Statements" text="

Below are the common ways to import functions that are already built by other people, i.e., the developers of the functions.

**Import entire module**

The ```import math``` code below actually imports the 'module' called ```math```.

A ```module```:

- contains a single ```.py``` file containing Python codes
- can define functions, classes, variables, or runnable codes

```python
import math
result = math.sqrt(16)  # Use with module.function
print(result)           # 4.0
```

**Import specific functions**

From a package, we import only the functions we want.

Why we do not import all the functions inside a package?

- a package contains a lot of modules and functions
- importing all of it could slow down the importing process
- however, you could import all of the functions IF you do not know which function you specifically want to use. Just use ```from package_name import *```

```python
from math import sqrt, pi, ceil

result = sqrt(25)  # Use directly without module name
area = pi * 5**2
rounded_up = ceil(4.2)
```

**Import with alias**

Importing a module as an alias has become a common practice for developers, programmers, and normal users of Python. Using an alias for a module means that instead of using the whole module name, you give it a short name... or nickname.

This just shortens the amount of time you type the module, but ultimately, makes the code cleaner and reduce the human error.

**Example 1:**

```python
import math as m

result = m.factorial(5)
print(result)                    # 120
```

**Example 2:**

```python
from math import factorial as fact

result = fact(5)
print(result)                    # 120
```

**Example 3:**

```python
import numpy as np

array = np.array([1, 2, 3, 4])
mean_value = np.mean(array)
print(mean_value)                # 2.5
```
" %}

## Common Built-in Modules

{% include question.html header="Math Module" text="
```python
import math
```
Basic mathematical operations

```python
print(math.sqrt(16))        # Square root: 4.0
print(math.pow(2, 3))       # Power: 8.0, the same as 2^3
print(math.factorial(5))    # Factorial: 120, in mathematics, this is '5! = 5*4*3*2*1'
```

Trigonometric functions

```python
print(math.sin(math.pi/2))  # Sine: 1.0
print(math.cos(0))          # Cosine: 1.0
```

Logarithms

```python
print(math.log(10))         # Natural log
print(math.log10(100))      # Base-10 log: 2.0
```

Rounding and ceiling

```python
print(math.ceil(4.2))       # Round up: 5 (this is the ceiling function)
print(math.floor(4.8))      # Round down: 4 (this is the floor function)
```

Constants

These are numbers in mathematics that **do not end**.

```python
print(math.pi)              # 3.141592653589793
print(math.e)               # 2.718281828459045
```
" %}

{% include question.html header="Random Module" text="


```python
import random
```

Generate random numbers.

This can be used for randomization purposes. Remember when your panelists ask you how did you randomize your participants to be assigned in the Control Group, Treatment, etc.? This is it! Python can do that.

```python
print(random.random())            # Float between   0-1
print(random.randint(1, 10))      # Integer between 1-10
print(random.uniform(1.5, 10.5))  # Float between   1.5-10.5
```

Work with sequences

```python
fruits = [\"apple\", \"banana\", \"orange\", \"grape\"]
print(random.choice(fruits))    # Random choice
print(random.sample(fruits, 2)) # Random sample of 2 items
```

Shuffle a list

```python
numbers = [1, 2, 3, 4, 5]
random.shuffle(numbers)
print(numbers)  # List is now shuffled
```

Set seed for reproducible results

```python
random.seed(42)
print(random.randint(1, 100))  # Will always be the same with seed 42
```
" %}

{% include question.html header="Datetime Module" text="

Import the ```datetime``` module

```python
from datetime import datetime, date, timedelta
```

Current date and time

```python
now = datetime.now()
today = date.today()

print(f\"Current datetime: {now}\")
print(f\"Today's date: {today}\")
```

Formatting dates

```python
formatted_date = now.strftime(\"%Y-%m-%d %H:%M:%S\")
print(f\"Formatted: {formatted_date}\")
```

Date arithmetic

```python
tomorrow = today + timedelta(days=1)
next_week = today + timedelta(weeks=1)
past_date = today - timedelta(days=30)

print(f\"Tomorrow: {tomorrow}\")
print(f\"Next week: {next_week}\")
print(f\"30 days ago: {past_date}\")
```

Parse date strings

```python
date_string = \"2025-12-25\"
christmas = datetime.strptime(date_string, \"%Y-%m-%d\")
print(f\"Christmas: {christmas}\")
```
" %}

{% include question.html header="OS Module" text="

Import the ```os``` module

```python
import os
```

Get current working directory

```python
current_dir = os.getcwd()
print(f\"Current directory: {current_dir}\")
```

List files in directory

```python
files = os.listdir(\".\")
print(f\"Files in current directory: {files}\")
```

Environment variables

```python
user = os.getenv(\"USER\", \"Unknown\")  # Get USER env var with default
print(f\"Current user: {user}\")
```

Path operations

```python
file_path = os.path.join(\"data\", \"files\", \"example.txt\")
print(f\"File path: {file_path}\")
```

Check if file/directory exists

```python
print(f\"Path exists: {os.path.exists(file_path)}\")
```
" %}

{% include question.html header="Creating Import-Friendly Functions" text="



```python
# utils.py - A module you might create
def format_currency(amount, currency=\"USD\"):
    \"\"\"Format a number as currency.\"\"\"
    return f\"{currency} {amount:,.2f}\"
```

Basic email validation

```python
def validate_email(email):
    \"\"\"Basic email validation.\"\"\"
    return \"@\" in email and \".\" in email.split(\"@\")[1]
```

Calculate tip amount

```python
def calculate_tip(bill_amount, tip_percentage=15):
    \"\"\"Calculate tip amount.\"\"\"
    return bill_amount * (tip_percentage / 100)
```



```python
# main.py - Using your module
from utils import format_currency, calculate_tip
```

Execute the function

```python
bill = 85.50
tip = calculate_tip(bill, 18)
total = bill + tip

print(f\"Bill: {format_currency(bill)}\")
print(f\"Tip: {format_currency(tip)}\")
print(f\"Total: {format_currency(total)}\")
```
" %}

{% capture text %}
**PRO TIP**

You might have heard of something called a ```package```. A package is a **directory** that contains **one or more modules** and a special ```__init__.py``` file. It allows you to organize **related modules** under a common namespace.

You can import modules from a package like:

```python
from my_package import my_module
```
{% endcapture %}
{% include alert.html text=text color=secondary%}
