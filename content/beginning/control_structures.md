---
section: Beginning Python
nav_order: 9
title: Control structures
topics: loop, if, for, while, functions
---

**Control structures** determine **the order in which your code executes**, allowing you to create decision-making and repetition logic that drives your program’s behavior.

Control structures can automate workflows such as checking patient eligibility, iterating over lab results, or categorizing patients based on diagnostic criteria.

{% include question.html header="If Statements" text="

The ```if``` statements are used for conditional execution, allowing a block of code to run only if a specified condition is true (e.g., ```if temperature > 30: print \"It's hot!\"```). This is done **to create decision-making logic** in your programs.

```python
age = 72
bp = 145

if age >= 60 and bp > 140:
    print(\"High-risk: Schedule follow-up consultation.\")
elif age >= 60 and bp <= 140:
    print(\"Monitor regularly.\")
else:
    print(\"Low-risk: Maintain routine check-ups.\")
```

The code above helps automatically classify patients based on age and blood pressure readings, similar to decision rules used in clinical triage systems.
" %}

{% include question.html header="For Loops" text="

```for``` loops are employed for iteration, repeating a block of code a fixed number of times or for each item in a collection (e.g., ```for item in list_of_items: process item```). They are crucial for **automating repetitive tasks**.

Loop through a list

```python
patients = [\"Alice\", \"Bob\", \"Carlos\"]
for name in patients:
    print(f\"Processing lab report for {name}\")

# Output
# Processing lab report for Alice
# Processing lab report for Bob
# Processing lab report for Carlos
```
This loop ensures that all patient reports are processed without manual repetition—useful when automating data cleaning or report generation for large datasets.

**Loop through a range of numbers**

```python
for i in range(5):  # 0 to 4
    print(f\"Count: {i}\")

# Output:
# Count: 0
# Count: 1
# Count: 2
# Count: 3
# Count: 4
```

**Loop through a dictionary**

```python
student = {\"name\": \"Alice\", \"age\": 20, \"is_diabetic\": True}
for key, value in student.items():
    print(f\"{key}: {value}\")

# Output
# name: Alice
# age: 20
# is_diabetic: True
```
" %}

{% include question.html header="While Loops" text="

```when``` (often found in languages like ```switch``` in R) is a construct for multi-way branching, providing a cleaner alternative to nested ```if-else if``` statements when you have multiple possible conditions to check against a single value (e.g., ```when day_of_week: \"Monday\" -> print \"Start of the week\"```). This improves code readability and maintainability.

Basic 'while' loop

```python
count = 0
while count < 5:
    print(f\"Count is {count}\")
    count += 1
```

'while' loop with user input

```python
user_input = \"\"
while user_input != \"quit\":
    user_input = input(\"Enter a command (or 'quit' to exit): \")
    if user_input != \"quit\":
        print(f\"You entered: {user_input}\")
```
" %}

{% include question.html header="Functions" text="

**Functions** are *reusable blocks of code* designed to perform a specific task (e.g., ```def calculate_area(length, width): return length * width```). They are used to break down complex problems into smaller, manageable pieces, promote code reusability, and improve the organization and readability of your programs.

Basic function

```python
def greet(name):
    return f\"Hello, {name}!\"
```

Function with default parameters

```python
def introduce(name, age=25):
    return f\"Hi, I'm {name} and I'm {age} years old.\"

```

Function with multiple parameters

```python
def calculate_area(length, width):
    area = length * width
    return area
```

Using functions

```python
message = greet(\"Alice\")
print(message)  # Hello, Alice!

intro = introduce(\"Bob\")  # Uses default age
print(intro)              # Hi, I'm Bob and I'm 25 years old.

room_area = calculate_area(10, 12)
print(f\"Room area: {room_area} square feet\")
```
" %}

{% include question.html header="Reusable Function for BMI Classification" text="

This function encapsulates a clinical rule (BMI categories), demonstrating how logic and computation combine to yield meaningful interpretations in healthcare analytics.

```python
def classify_bmi(weight_in_kg, height_in_meters):
    bmi = weight_in_kg / (height_in_meters ** 2)
    if bmi < 18.5:
        return \"Underweight\"
    elif bmi < 25:
        return \"Normal\"
    elif bmi < 30:
        return \"Overweight\"
    else:
        return \"Obese\"

print(classify_bmi(70, 1.75))
```
" %}

{% capture text %}
**Note:**
Remember the **indents** in your ```if```, ```for```, ```while``` statements and in your functions. They act as indicators for Python to recognize that the next line of code is part of the if statement or function.{% endcapture %}
{% include alert.html text=text color=secondary %}
