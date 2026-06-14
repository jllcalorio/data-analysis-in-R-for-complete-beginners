---
section: Intermediate R
nav_order: 8
title: Simple Exercises with Solutions
topics: exercises
---

{% include question.html header="Exercise 1: BMI Calculator Script" text="

**Goal:**

Write a simple script (bmi_calculator.R) that computes Body Mass Index (BMI) and interprets the result.

**Instructions:**

1. Create a function `calculate_bmi(weight, height)` that:
    - Takes `weight` (in kilograms) and `height` (in meters)
    - Returns the BMI value
2. Create another function `interpret_bmi(bmi)` that:
    - Returns \"`Underweight`\", \"`Normal weight`\", \"Overw`e`ight\", or \"`Obese`\" depending on the BMI
3. In the main script (`main.R`), ask the user for their weight and height, then print their BMI and category.

" solution="

**bmi_calculator.R**

```r
# Simple BMI Calculator Script

calculate_bmi <- function(weight, height) {
  # Compute BMI = weight / height^2
  weight / (height ^ 2)
}

interpret_bmi <- function(bmi) {
  # Return BMI classification.
  if (bmi < 18.5) {
    return(\"Underweight\")
  } else if (bmi < 25) {
    return(\"Normal weight\")
  } else if (bmi < 30) {
    return(\"Overweight\")
  } else {
    return(\"Obese\")
  }
}
```

**main.R**

```r
source(\"bmi_calculator.R\")

weight <- as.numeric(readline(prompt = \"Enter your weight (kg): \"))
height <- as.numeric(readline(prompt = \"Enter your height (m): \"))

bmi_value <- calculate_bmi(weight, height)
category  <- interpret_bmi(bmi_value)

cat(sprintf(\"Your BMI is %.1f (%s)\n\", bmi_value, category))
```
" %}

{% include question.html header="Exercise 2: Medication Dosage Calculator" text="

**Goal:**

Create a function that calculates a child's **drug dosage** based on weight (e.g., for Paracetamol).

**Instructions:**

1. The safe dose for Paracetamol is **10–15 mg/kg per dose**.
2. Create a script (`dosage_calculator.R`) with:
    - Function calculate_dosage(`weight`, `dose_mg_per_kg`)
    - Function `recommend_range(weight)` that prints the safe dosage range (`10–15 mg/kg`)
3. Test with a few sample inputs.


" solution="

**dosage_calculator.R**

```r
# Simple medication dosage calculator

calculate_dosage <- function(weight, dose_mg_per_kg) {
  # Calculate dose in mg given weight in kg.
  weight * dose_mg_per_kg
}

recommend_range <- function(weight) {
  # Print recommended Paracetamol dose range (mg).
  min_dose <- calculate_dosage(weight, 10)
  max_dose <- calculate_dosage(weight, 15)
  cat(sprintf(\"Safe range: %.0f mg - %.0f mg per dose\n\", min_dose, max_dose))
}
```

**main.R**

```r
source(\"dosage_calculator.R\")

weight <- as.numeric(readline(prompt = \"Enter child's weight (kg): \"))
recommend_range(weight)

chosen_dose <- as.numeric(readline(prompt = \"Enter dose in mg/kg (10-15): \"))
total_mg    <- calculate_dosage(weight, chosen_dose)

cat(sprintf(\"Total dose: %.0f mg\n\", total_mg))
```
" %}

{% include question.html header="Exercise 3: Heart Rate Evaluator" text="

Goal:

Create a function that classifies a **resting heart rate** reading based on simple rules.

Instructions:

1. Create a script (`heart_rate.R`) with:
2. Function `classify_heart_rate(rate)`
3. Classification rules:
    - Below 60 → \"`Bradycardia`\"
    - 60–100 → \"`Normal`\"
    - Above 100 → \"`Tachycardia`\"
4. Test the function using different values.

" solution="

**heart_rate.R**

```r
# Heart rate classification script

classify_heart_rate <- function(rate) {
  # Return classification of resting heart rate.
  if (rate < 60) {
    return(\"Bradycardia (Low heart rate)\")
  } else if (rate <= 100) {
    return(\"Normal\")
  } else {
    return(\"Tachycardia (High heart rate)\")
  }
}
```

**main.R**

```r
source(\"heart_rate.R\")

rate           <- as.integer(readline(prompt = \"Enter resting heart rate (bpm): \"))
classification <- classify_heart_rate(rate)

cat(sprintf(\"Heart Rate: %d bpm → %s\n\", rate, classification))
```
" %}

{% capture text %}
**Concepts Practiced**

- Creating and sourcing simple scripts (`.R `files)
- Defining and calling functions with parameters
- Returning and printing results
- Applying programming to medical contexts
{% endcapture %}
{% include alert.html text=text color=secondary %}