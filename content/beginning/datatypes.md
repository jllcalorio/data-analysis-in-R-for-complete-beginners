---
section: Beginning Python
nav_order: 4
title: Basic Data Types
topics: data type, int, float, string
---

Python has several built-in data types, each designed to represent different kinds of information.
In healthcare and research, you’ll often deal with patient names (text), ages (numbers), lab results (decimals), and test outcomes (True/False). Understanding these data types helps ensure your analyses are accurate and meaningful.

# **The Four Main Data Types**

{% include question.html header="Strings (str)" text="

*Strings* are considered as text data enclosed in single or double quotation marks, and are often used to store text data such as ```patient names```, ```diagnoses```, or ```remarks``` in a medical record.

```python
patient_name = 'Maria Santos'
diagnosis = 'Hypertension'
note = 'Patient advised to monitor blood pressure daily.'
```
" %}

{% include question.html header="Integers (int)" text="

Integers are numbers, specifically whole numbers. These data are numbers that do not contain decimal places. They can be ```age```, ```heart rate```, or ```number of visits```.

```python
patient_age = 45
admission_year = 2025
heart_rate = 78
```
" %}

{% include question.html header="Floats (float)" text="

*Floats* represent numeric values with decimals — common in lab values, ```BMI```, etc.

```python
body_temperature = 36.8
blood_glucose = 5.7
bmi = 24.5
```
" %}

{% include question.html header="Booleans (bool)" text="

Booleans are either 'True' or 'False' data. For example, whether a patient ```has diabetes```, ```is pregnant```, or ```is a smoker```.

```python
has_allergies = True
is_smoker = False
```
" %}

{% include question.html header="On to Checking Data Types" text="

You can use the ```type()``` function to check the data type of any variable.
For example, is a lab result value '42' stored as text or as a number?

" solution="
```python
result = '42'
print(type(result))  # Output: <class 'str'>

value = 42
print(type(value))  # <class 'int'>
```
" %}

{% include question.html header="Converting Between Data Types" text="

In many datasets, data imported from hospital systems **may be stored as text even if they represent numbers**.

Converting them to integers or floats allows you to perform calculations like ```average age``` or ```mean blood glucose```.

```python
age_str = \"25\"
age_int = int(age_str)
print(age_int + 5)       # Output: 30
```
" %}

{% include question.html header="Integer to string" text="

We can also do vice-versa.

```python
patient_bmi = 22.5
bmi_str = str(patient_bmi)
print('Patient BMI is ' + bmi_str)
```
" %}

{% include question.html header="String to float" text="
```python
glucose_str = '5.8'
glucose_float = float(glucose_str)
print(glucose_float + 0.2)            # Output: 6.0
```
" %}

{% include question.html header="Float to integer (truncates decimal)" text="
```python
heart_rate = int(75.6)  # Result: 75
```

When converting from ```float``` to ```integer```, **Python removes (truncates) the decimal** — this is useful when you only need whole-number data, such as rounding heart rate readings.
" %}

{% include question.html header="Boolean conversions" text="
```python
print(bool(1))       # True → e.g., 1 could represent 'Yes' in a dataset
print(bool(0))       # False → e.g., 0 could represent 'No'
print(bool(''))      # False → No value provided
print(bool('Yes'))   # True → Non-empty string
```
" %}

{% capture text %}
**Closing**

🩺 **In medical data analysis**, understanding data types ensures you store and analyze information correctly — for example, calculating the average age (integers) or comparing lab results (floats) without errors.
{% endcapture %}
{% include alert.html text=text color=secondary %}
