---
section: Intermediate Python
nav_order: 5
title: Errors and Exception Handling
topics: errors
---

**Errors are inevitable in programming** — even in medical research and clinical data management. Learning how to handle them gracefully ensures that your programs remain **robust, safe, and user-friendly**, especially when dealing with sensitive or life-impacting information.

## Types of Errors

{% include question.html header="Syntax Errors" text="

These occur when Python cannot understand your code due to incorrect syntax. They prevent the program from running entirely.

```python
print(\"Patient record loaded\"
if age = 45:
    print(\"Valid age\")
```

**Pop quiz**

Where do you think the errors are?

" solution="

```python
1. Missing closing parenthesis
2. The condition should use == instead of =
3. Improper indentation
```
" %}

{% include question.html header="Runtime Errors (Exceptions)" text="

These occur **during execution** — the syntax is correct, but something unexpected happens (like dividing by zero or accessing missing data)..

```python
print(10 / 0)              # ZeroDivisionError
print(ages[10])            # IndexError (if the list has fewer than 11 items)
print(int(\"fever\"))        # ValueError
print(patient_record)      # NameError (if not defined)
```

**Example:**

A clinical data program might crash when trying to divide by zero if a patient’s height is accidentally recorded as **0** during BMI computation.
" %}

## Basic Exception Handling

{% include question.html header="Try-Except Blocks" text="

Handle potential errors using ```try``` and ```except``` statements.

```python
def safe_bmi(weight, height):
    \"\"\"Safely calculate BMI with error handling.\"\"\"
    try:
        bmi = weight / (height ** 2)
        return bmi
    except ZeroDivisionError:
        print(\"Error: Height cannot be zero!\")
        return None
```

Execute the function.

```python
result1 = safe_bmi(60, 1.65)
result2 = safe_bmi(70, 0)
```

**Output:**

Error: Height cannot be zero!
" %}

{% include question.html header="Handling Multiple Exceptions" text="

Sometimes multiple things can go wrong — like invalid inputs or user interruptions.

```python
def get_patient_age():
    \"\"\"Process patient age input safely.\"\"\"
    try:
        age = int(input(\"Enter patient age: \"))
        if age < 0:
            raise ValueError(\"Age cannot be negative\")

        birth_year = 2025 - age
        return birth_year

    except ValueError as e:
        print(f\"Invalid input: {e}\")
        return None
    except KeyboardInterrupt:
        print(\"\nOperation cancelled by user.\")
        return None
```

This **ensures your program won’t crash** even if the **user makes a mistake**.

Execute the function.

```python
year = get_patient_age()
if year:
    print(f\"You were born in {year}\")
```
" %}

{% include question.html header="Try-Except-Else-Finally" text="

These blocks let you **handle file operations safely**, which is vital when working with electronic medical records or lab results.

```python
def read_patient_file(filename):
    \"\"\"Read patient data with comprehensive error handling.\"\"\"
    file_handle = None
    try:
        file_handle = open(filename, 'r')
        content = file_handle.read()
        print(\"Patient file read successfully!\")

    except FileNotFoundError:
        print(f\"Error: File '{filename}' not found.\")
        content = None

    except PermissionError:
        print(f\"Error: No permission to read '{filename}'.\")
        content = None

    except Exception as e:
        print(f\"Unexpected error: {e}\")
        content = None

    else:
        print(f\"File contains {len(content)} characters.\")
    finally:
        if file_handle:
            file_handle.close()
            print(\"File closed.\")
    return content
```
" %}

{% include question.html header="Raising Custom Exceptions" text="

Custom exceptions make your programs **specific to your domain** — like raising an error when a hospital account or pharmacy balance is insufficient.

```python
class InsufficientStockError(Exception):
    \"\"\"Custom exception for low medication stock.\"\"\"
    pass

class PharmacyInventory:
    def __init__(self, stock=0):
        self.stock = stock

    def dispense(self, quantity):
        \"\"\"Dispense medication with error checks.\"\"\"
        if quantity <= 0:
            raise ValueError(\"Dispense quantity must be positive.\)
        if quantity > self.stock:
            raise InsufficientStockError(
                f\"Cannot dispense {quantity} units. Only {self.stock} available.\"
            )
        self.stock -= quantity
        return self.stock
```

Execute the function.

```python
inventory = PharmacyInventory(20)

try:
    inventory.dispense(50)
except InsufficientStockError as e:
    print(f\"Dispensing failed: {e}\")
```
" %}

# Debugging Tips

Debugging helps you **trace problems** when something goes wrong in your data pipeline or algorithm.

```python
def debug_lab_results(data):
    \"\"\"Debugging function for lab result entries.\"\"\"
    print(f\"DEBUG: Input type: {type(data)}\")
    print(f\"DEBUG: Input value: {data}\")

    try:
        if isinstance(data, str):
            result = data.upper()
        elif isinstance(data, (int, float)):
            result = data * 2
        elif isinstance(data, list):
            result = [value * 2 for value in data]
        else:
            raise TypeError(f\"Unsupported data type: {type(data)}\")

        print(f\"DEBUG: Processed result: {result}\")
        return result

    except Exception as e:
        print(f\"DEBUG: Exception occurred: {e}\")
        print(f\"DEBUG: Exception type: {type(e).__name__}\")
        raise  # Re-raise the exception for further investigation
```

Execute the function.

```python
test_data = [\"hello\", 42, [1, 2, 3], {\"key\": \"value\"}]

for data in test_data:
    try:
        result = debug_lab_results(data)
        print(f\"Success: {result}\n\")
    except Exception as e:
        print(f\"Failed: {e}\n\")
```

{% capture text %}
Error handling is not just about preventing crashes — it’s about **ensuring reliability and trust** in your programs.
In healthcare applications, properly handled errors can prevent incorrect medication doses, invalid data entries, or loss of patient information.

Robust exception handling ensures that your systems **fail gracefully**, log meaningful messages, and protect both users and data integrity.
{% endcapture %}
{% include alert.html text=text color=secondary %}
