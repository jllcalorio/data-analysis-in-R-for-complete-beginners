---
section: Beginning R
nav_order: 5
title: Operators
topics: arithmetic, comparison, logical, assignment, operators
---

Operators allow you to perform calculations and logical checks on variables and values. In medical and research contexts, you might use operators to:

- Compute a patient's BMI from height and weight
- Compare lab results to normal ranges
- Combine conditions like "is diabetic AND hypertensive"

{% include question.html header="Arithmetic Operators" text="

R can perform all standard mathematical operations. If you remember PEMDAS, yes, it applies here too.

**Set the variables.**

```r
weight_kg <- 70
height_m  <- 1.75
```

**Arithmetic operations using medical data**

```r
bmi <- weight_kg / (height_m ^ 2)
print(bmi)   # BMI calculation using division and exponentiation

# Output
# 22.85714
```

**Basic arithmetic**

```r
age                    <- 30
years_until_retirement <- 65 - age
print(years_until_retirement)   # Output: 35
```

**Example of integer division and modulus.**

- Integer division (`%/%`): divides and returns only the whole-number part
- Modulus (`%%`): returns the remainder after division

```r
patients      <- 53
beds_per_room <- 4

print(patients %/% beds_per_room)   # 13 full rooms
print(patients %% beds_per_room)    # 1 remaining patient without a full room
```

In case you want to try other variables:

```r
a <- 10
b <- 3

print(a + b)      # Addition:         13
print(a - b)      # Subtraction:      7
print(a * b)      # Multiplication:   30
print(a / b)      # Division:         3.333...
print(a %/% b)    # Integer division: 3
print(a %% b)     # Modulus:          1
print(a ^ b)      # Exponentiation:   1000  (same as a^b = 10^3)
```

Remember that PEMDAS stands for?

" solution="

PEMDAS is a mathematical acronym for the order of operations, namely

- **P**arentheses,
- **E**xponents,
- **M**ultiplication,
- **D**ivision,
- **A**ddition, and
- **S**ubtraction.
" %}

{% include question.html header="Comparison Operators" text="

In R, you can compare values to check if they are the same, different, or if one is larger or smaller than the other.

Use double equal signs `==` to check equality — a single `=` or `<-` is the assignment operator, not a comparison.

```r
patient_temp <- 38.2
normal_temp  <- 37.0

print(patient_temp == normal_temp)   # FALSE, temperature is not equal
print(patient_temp >  normal_temp)   # TRUE,  patient has fever
print(patient_temp <  normal_temp)   # FALSE, not lower
print(patient_temp >= 38.0)          # TRUE,  borderline fever
print(patient_temp != normal_temp)   # TRUE,  definitely different
```
" %}

{% include question.html header="Logical Operators" text="

Logical operators combine or invert truth values (`TRUE`/`FALSE`).

```r
has_diabetes     <- TRUE
has_hypertension <- FALSE

print(has_diabetes & has_hypertension)    # FALSE — patient has only one condition
print(has_diabetes | has_hypertension)    # TRUE  — at least one condition is TRUE
print(!has_diabetes)                      # FALSE — inverts TRUE to FALSE
```

🩺 **Logical operators** are often used when filtering datasets — for example, **'Find all patients who are diabetic AND hypertensive'.**
" %}

{% include question.html header="Assignment Operators" text="

R's primary assignment operator is `<-`. You can also use `=` inside function calls. Compound assignment (like `+=` in Python) does not exist in base R, but you can replicate the effect:

```r
patient_count <- 100                  # Start with 100 patients
patient_count <- patient_count + 5    # 5 new admissions
patient_count <- patient_count - 3    # 3 discharged
patient_count <- patient_count * 1.05 # 5% increase projected
patient_count <- patient_count / 2    # Split between two wards

print(patient_count)                  # Output: 53.55
```
" %}

{% capture text %}
**Why this matters:**

Operators are one of the foundations of data analysis. You'll use them to calculate averages, compare lab results, and set conditions in your analyses — just like evaluating whether a patient meets diagnostic criteria.
{% endcapture %}
{% include alert.html text=text color=secondary %}
