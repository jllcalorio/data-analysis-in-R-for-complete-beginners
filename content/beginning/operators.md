---
section: Beginning Python
nav_order: 5
title: Operators
topics: arithmetic, comparison, logical, assignment, operators
---

Operators allow you to perform calculations and logical checks on variables and values. In medical and research contexts, you might use operators to:

- Compute a patient’s BMI from height and weight
- Compare lab results to normal ranges
- Combine conditions like “is diabetic AND hypertensive”

{% include question.html header="Arithmetic Operators" text="

Performing mathematical operators can be done in Python. If you remember PEMDAS, yes, it can be done.

**Set the variables.**

```python
weight_kg = 70
height_m = 1.75
```

**Arithmetic operations using medical data**

```python
bmi = weight_kg / (height_m ** 2)
print(bmi)   # BMI calculation using division and exponentiation
```

**Basic arithmetic**

```python
age = 30
years_until_retirement = 65 - age
print(years_until_retirement)  # Output: 35
```

**Example of floor division and modulus.**

- Floor division: Divides one number by another and rounds down to the nearest whole number (integer)
- Modulus (remainder): returns the remainder after dividing one number by another

```python
patients = 53
beds_per_room = 4

print(patients // beds_per_room)  # 13 full rooms
print(patients % beds_per_room)   # 1 remaining patient without a full room
```

In case you want to try other variables:

```python
a = 10
b = 3

print(a + b)   # Addition: 13
print(a - b)   # Subtraction: 7
print(a * b)   # Multiplication: 30
print(a / b)   # Division: 3.333...
print(a // b)  # Floor division: 3 [divides 'a' by 'b' and rounds down to the nearest whole number (integer)]
print(a % b)   # Modulus (remainder): 1 [an operator that returns the remainder after dividing 'a' by 'b']
print(a ** b)  # Exponentiation: 1000, in Excel, this is a^b = 10^3
```

Remember that PEMDAS stands for?

" solution="
PEMDAS is a mathematical acronym for the order of operations, namely
- Parentheses,
- Exponents,
- Multiplication,
- Division,
- Addition, and
- Subtraction.
" %}

{% include question.html header="Comparison Operators" text="

In Python, you can compare values if they are the same or different, or if a value is larger/smaller than the other value.

If you want to check if two (2) values are the same, you should use double equal sign (==), not just one. Why? Because using one equal sign (=) corresponds to setting the left side of the equal sign to be the 'variable' name.

```python
patient_temp = 38.2
normal_temp = 37.0

print(patient_temp == normal_temp)   # False, temperature is not equal
print(patient_temp > normal_temp)    # True, patient has fever
print(patient_temp < normal_temp)    # False, not lower
print(patient_temp >= 38.0)          # True, borderline fever
print(patient_temp != normal_temp)   # True, definitely different
```
" %}

{% include question.html header="Logical Operators" text="

Logical operators are Boolean operators used to combine or invert truth values.

```python
has_diabetes = True
has_hypertension = False

print(has_diabetes and has_hypertension)  # False, patient has only one condition
print(has_diabetes or has_hypertension)   # True, at least one condition is True
print(not has_diabetes)                   # False, inverts True to False
```

🩺 **Logical operators** are often used when filtering datasets — for example, **'Find all patients who are diabetic AND hypertensive'.**
" %}

{% include question.html header="Assignment Operators" text="

Assignment operators are used to assign values to variables and, in many cases, to update existing values using shorthand notation.

They combine a basic operation (like addition or multiplication) with assignment, making code more concise and readable.

```python
patient_count = 100    # Start with 100 patients
patient_count += 5     # 5 new admissions
patient_count -= 3     # 3 discharged
patient_count *= 1.05  # 5% increase projected
patient_count /= 2     # Split between two wards

print(patient_count)  # Output: 51.75
```
" %}

{% capture text %}
**Why this matters:**

Operators are one of the foundations of data analysis. You’ll use them to calculate averages, compare lab results, and set conditions in your analyses — just like evaluating whether a patient meets diagnostic criteria.
{% endcapture %}
{% include alert.html text=text color=secondary %}
