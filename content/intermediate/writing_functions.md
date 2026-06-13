---
section: Intermediate Python
nav_order: 1
title: Writing Functions
topics: functions
---

**Functions** are the building blocks of well-organized code. They let you write logic once and reuse it across multiple scenarios — an essential skill when automating tasks like calculating BMI, summarizing lab results, or cleaning patient datasets.

{% include question.html header="Function Basics Review" text="

Let’s say we want to create a function that greets a patient when their name is entered into a system.

```python
def greet(name):
    \"\"\"A simple function that greets someone.\"\"\"
    return f\"Hello, {name}! Welcome to your appointment.\"
```

Call the function:

```python
message = greet(\"Dr. Reyes\")
print(message)                     # Output: Hello, Dr. Reyes! Welcome to your appointment.
```
" %}

# Advanced Function Features

{% include question.html header="Default Parameters" text="

Let’s define a function that creates a **basic patient profile** — similar to what you’d store in an electronic medical record (EMR).

```python
def create_profile(name, age, city=\"Davao\", diagnosis=\"Not yet diagnosed\"):
    \"\"\"Create a patient profile with default values.\"\"\"
    profile = {
        \"name\": name,
        \"age\": age,
        \"city\": city,
        \"diagnosis\": diagnosis
    }
    return profile
```

Run the function using (1) default parameters and (2) custom parameters:

```python
patient1 = create_profile(\"Ana Santos\", 35)
patient2 = create_profile(\"Miguel Cruz\", 58, \"Davao\", \"Hypertension\")

print(patient1)  # city and diagnosis use defaults
print(patient2)  # all parameters specified
```
" %}

{% include question.html header="Keyword Arguments" text="

Here’s a fun analogy: imagine writing a function that **orders medical supplies** (instead of pizza).

```python
def order_supplies(quantity, *items, **details):
    \"\"\"Order medical supplies with flexible arguments.\"\"\"
    print(f\"Order quantity: {quantity}\")
    print(f\"Items: {', '.join(items)}\")

    for key, value in details.items():
        print(f\"{key}: {value}\")
```

Call the function:

```python
order_supplies(3, \"syringes\", \"bandages\",
               urgent=True, delivery=\"Next-day\")
```
" %}

{% include question.html header="Variable-Length Arguments" text="

You can also design flexible functions that handle **any number of lab results** or patient details.

**Example 1:** Calculate average blood glucose readings:

```python
def calculate_average(*values):
    \"\"\"Calculate average of any number of readings.\"\"\"
    if not values:
        return 0
    return sum(values) / len(values)
```

**Example 2:** Create a **patient record** with flexible fields:

```python
def create_patient_record(name, **info):
    \"\"\"Create a patient record with flexible information.\"\"\"
    record = {\"name\": name}
    record.update(info)
    return record
```

Use the functions:

```python
avg_glucose = calculate_average(92, 110, 87, 105)
print(f\"Average Glucose: {avg_glucose:.1f} mg/dL\")

patient = create_patient_record(
    \"Maria Dela Cruz\",
    age=47,
    condition=\"Diabetes\",
    medications=[\"Metformin\", \"Insulin\"],
    last_visit=\"2025-09-10\"
)
print(patient)
```
" %}

{% include question.html header="Lambda Functions (Anonymous Functions)" text="

**Lambda** functions are **compact, one-line functions** useful for quick calculations or filtering data.

For instance, you could quickly identify patients with elevated BMI values.

```python
# Regular function
def bmi(weight, height):
    return weight / (height ** 2)

# Lambda equivalent
bmi_lambda = lambda weight, height: weight / (height ** 2)

print(bmi_lambda(70, 1.75))  # Output: 22.86
```

Filtering a list of patients:

```python
patients = [
    {\"name\": \"Ana\", \"bmi\": 22.5},
    {\"name\": \"Ben\", \"bmi\": 29.8},
    {\"name\": \"Clara\", \"bmi\": 18.9}
]

# Get only overweight patients (BMI ≥ 25)
overweight = list(filter(lambda p: p[\"bmi\"] >= 25, patients))
print(overweight)
```

What are its advantages of a ```lambda``` function.

- **Inline definition:** You can define a function in a single line without naming it
- **Saves space:** Ideal for short, throwaway functions used once or in a small scope
- Great for **Testing and Prototyping**

What are the disadvantages?

- they can hurt readability if overused or used for complex logic
- if your function spans multiple operations or needs documentation, a named def function is usually better

**Let's see another example:**

```python
# Lambda equivalent
square_lambda = lambda x: x ** 2

# Common use with built-in functions
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# Filtering with lambda
students = [
    {\"name\": \"Alice\", \"grade\": 85},
    {\"name\": \"Bob\", \"grade\": 92},
    {\"name\": \"Charlie\", \"grade\": 78}
]

high_performers = list(filter(lambda s: s[\"grade\"] >= 85, students))
print(high_performers)
```
" %}

{% capture text %}
Functions let you **automate repetitive tasks**, from **calculating averages** of lab results to **generating formatted patient summaries**.

They make your code **modular, reusable, and easier to understand**, especially when analyzing multiple patient records or large datasets.
{% endcapture %}
{% include alert.html text=text color=secondary %}
