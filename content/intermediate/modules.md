---
section: Intermediate Python
nav_order: 4
title: Modules
topics: Template; Basic Configuration
---

Understanding **modules** is essential to organizing your code and taking full advantage of Python’s extensive ecosystem. In healthcare and biomedical research, modules allow you to separate reusable logic — such as calculations, data cleaning, or patient analytics — into organized files.

## What Are Modules?

A module is simply a Python file containing **functions**, **classes**, and **variables**.

Any ```.py``` file can be imported as a module into another Python script.

Modules help you:

- Reuse code across multiple projects
- Keep your code organized and maintainable
- Share your work with colleagues or research collaborators


{% include question.html header="Creating Your Own Modules" text="

Let’s create a file named ```medical_calculator.py``` — a simple module that **performs basic medical computations**.

**Example:** ```medical_calculator.py```

This module provides **basic biomedical calculations** that could be used in clinical or research contexts.

Let's define the functions:

```python
def bmi(weight, height):
    \"\"\"Calculate Body Mass Index.\"\"\"
    return weight / (height ** 2)

def bsa(weight, height):
    \"\"\"Calculate Body Surface Area (Mosteller formula).\"\"\"
    return ((height * weight) / 3600) ** 0.5

def mean_arterial_pressure(systolic, diastolic):
    \"\"\"Calculate Mean Arterial Pressure (MAP).\"\"\"
    return (2 * diastolic + systolic) / 3

def temperature_c_to_f(celsius):
    \"\"\"Convert Celsius to Fahrenheit.\"\"\"
    return (celsius * 9/5) + 32

def temperature_f_to_c(fahrenheit):
    \"\"\"Convert Fahrenheit to Celsius.\"\"\"
    return (fahrenheit - 32) * 5/9
```

**Let's also define module-level variables**

You can also define **constants** that are commonly used in medical calculations.

```python
NORMAL_BMI_RANGE = (18.5, 24.9)
BODY_WATER_PERCENT = 0.6
```

Code That Runs When the Module Is Imported

```python
print(\"Medical Calculator module loaded successfully.\")
```

Code That Runs When the Module Is Executed Directly

```python
if __name__ == \"__main__\":
    print(\"Running tests for Medical Calculator module...\")
    print(f\"BMI (70kg, 1.75m): {bmi(70, 1.75):.2f}\")
    print(f\"BSA (70kg, 175cm): {bsa(70, 175):.2f}\")
    print(f\"MAP (120/80 mmHg): {mean_arterial_pressure(120, 80):.2f}\")
```
" %}

{% include question.html header="Using Your Module" text="

Now create another file, main.py, where we import and use our module.

```python
import medical_calculator
```

**Use functions from the module:**

```python
bmi_value = medical_calculator.bmi(65, 1.68)
map_value = medical_calculator.mean_arterial_pressure(118, 76)

print(f\"BMI: {bmi_value:.2f}\")
print(f\"Mean Arterial Pressure: {map_value:.1f} mmHg\")
```

**Alternative import methods**

```python
from medical_calculator import bmi, bsa

print(f\"BMI: {bmi(58, 1.60):.2f}\")
print(f\"BSA: {bsa(58, 160):.2f}\")
```

**Import With Alias**

```python
import medical_calculator as mc

print(f\"Temperature: {mc.temperature_c_to_f(37):.1f}°F\")
```
" %}

{% include question.html header="🩺 Why This Matters?" text="
Using modules helps healthcare professionals, researchers, and data analysts reuse and standardize computations across projects.

For example:

- Standardize BMI formulas for all datasets
- Maintain consistency in how blood pressure is interpreted
- Reduce errors when analyzing patient data
" %}

{% capture text %}
Modules make your code **modular, reusable, and easier to maintain** — crucial for building reliable healthcare tools and analysis pipelines.

Whether you’re creating a clinical calculator, automating data cleaning, or building a patient outcome model, modular programming ensures **accuracy, collaboration, and scalability**.
{% endcapture %}
{% include alert.html text=text color=secondary %}
