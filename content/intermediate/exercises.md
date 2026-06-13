---
section: Intermediate Python
nav_order: 6
title: Simple Exercises with Solutions
topics: exercises
---

{% include question.html header="Exercise 1: BMI Calculator Module" text="

**Goal:**

Write a simple module (```bmi_calculator.py```) that computes **Body Mass Index (BMI)** and interprets the result.

**Instructions:**

1. Create a function ```calculate_bmi(weight, height)``` that:
  - Takes ```weight``` (in kilograms) and ```height``` (in meters)
  - Returns the BMI value
2. Create another function ```interpret_bmi(bmi)``` that:
  - Returns ```\"Underweight\"```, ```\"Normal weight\"```, ```\"Overweight\"```, or ```\"Obese\"``` depending on the BMI
3. In the main program (```main.py```), ask the user for their weight and height, then print their BMI and category.

" solution="

**bmi_calculator.py**

```python
\"\"\"Simple BMI Calculator Module\"\"\"

def calculate_bmi(weight, height):
    \"\"\"Compute BMI = weight / height²\"\"\"
    return weight / (height ** 2)

def interpret_bmi(bmi):
    \"\"\"Return BMI classification.\"\"\"
    if bmi < 18.5:
        return \"Underweight\"
    elif bmi < 25:
        return \"Normal weight\"
    elif bmi < 30:
        return \"Overweight\"
    else:
        return \"Obese\"
```

**main.py**

```python
import bmi_calculator as bmi

weight = float(input(\"Enter your weight (kg): \"))
height = float(input(\"Enter your height (m): \"))

bmi_value = bmi.calculate_bmi(weight, height)
category = bmi.interpret_bmi(bmi_value)

print(f\"Your BMI is {bmi_value:.1f} ({category})\")
```
" %}

{% include question.html header="Exercise 2: Medication Dosage Calculator" text="

**Goal:**

Create a function that calculates a child’s **drug dosage** based on weight (e.g., for Paracetamol).

**Instructions:**

1. The safe dose for Paracetamol is **10–15 mg/kg per dose**.
2. Create a module (```dosage_calculator.py```) with:
  - Function ```calculate_dosage(weight, dose_mg_per_kg)```
  - Function ```recommend_range(weight)``` that prints the safe dosage range (10–15 mg/kg)
3. Test with a few sample inputs.

" solution="

**dosage_calculator.py**

```python
\"\"\"Simple medication dosage calculator\"\"\"

def calculate_dosage(weight, dose_mg_per_kg):
    \"\"\"Calculate dose in mg given weight in kg.\"\"\"
    return weight * dose_mg_per_kg

def recommend_range(weight):
    \"\"\"Print recommended Paracetamol dose range (mg).\"\"\"
    min_dose = calculate_dosage(weight, 10)
    max_dose = calculate_dosage(weight, 15)
    print(f\"Safe range: {min_dose:.0f} mg - {max_dose:.0f} mg per dose\")
```

**main.py**

```python
import dosage_calculator as dose

weight = float(input(\"Enter child's weight (kg): \"))

dose.recommend_range(weight)

chosen_dose = float(input(\"Enter dose in mg/kg (10–15): \"))
total_mg = dose.calculate_dosage(weight, chosen_dose)

print(f\"Total dose: {total_mg:.0f} mg\")
```
" %}

{% include question.html header="Exercise 3: Heart Rate Evaluator" text="

**Goal:**

Create a function that classifies a **resting heart rate** reading based on simple rules.

**Instructions:**

1. Create a module (heart_rate.py) with:
  - Function classify_heart_rate(rate)
2. Classification rules:
  - Below 60 → \"Bradycardia\"
  - 60–100 → \"Normal\"
  - Above 100 → \"Tachycardia\"
3. Test the function using different values.

" solution="

**heart_rate.py**

```python
\"\"\"Heart rate classification module\"\"\"

def classify_heart_rate(rate):
    \"\"\"Return classification of resting heart rate.\"\"\"
    if rate < 60:
        return \"Bradycardia (Low heart rate)\"
    elif rate <= 100:
        return \"Normal\"
    else:
        return \"Tachycardia (High heart rate)\"
```

**main.py**

```python
import heart_rate as hr

rate = int(input(\"Enter resting heart rate (bpm): \"))
classification = hr.classify_heart_rate(rate)

print(f\"Heart Rate: {rate} bpm → {classification}\")
```
" %}

{% capture text %}
**Concepts Practiced**
- Creating and importing simple modules (```.py``` files)
- Defining and calling functions with parameters
- Returning and printing results
- Applying programming to medical contexts
{% endcapture %}
{% include alert.html text=text color=secondary %}
