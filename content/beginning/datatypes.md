---
section: Beginning R
nav_order: 4
title: Basic Data Types
topics: data type, numeric, integer, character, logical
---

R has several built-in data types, each designed to represent different kinds of information.

In healthcare and research, you'll often deal with patient names (text), ages (whole numbers), lab results (decimals), and test outcomes (`TRUE`/`FALSE`). Understanding these data types helps ensure your analyses are accurate and meaningful.

# **The Four Main Data Types**

{% include question.html header="Characters (character)" text="

**Characters** (also called strings) are text data enclosed in single or double quotation marks, and are often used to store text data such as `patient names`, `diagnoses`, or `remarks` in a medical record.

```r
patient_name <- \"Maria Santos\"
diagnosis    <- \"Hypertension\"
note         <- \"Patient advised to monitor blood pressure daily.\"
```
" %}

{% include question.html header="Integers (integer)" text="

**Integers** are numbers, specifically whole numbers. These data are numbers that do not contain decimal places. They can be ```age```, ```heart rate```, or ```number of visits```.

```r
patient_age    <- 45L
admission_year <- 2025L
heart_rate     <- 78L
```
" %}

{% include question.html header="Numerics / Doubles (numeric)" text="

**Numerics** represent values with decimals — common in lab values, `BMI`, `temperatures`, etc.

```r
body_temperature <- 36.8
blood_glucose    <- 5.7
bmi              <- 24.5
```
" %}

{% include question.html header="Logicals (logical)" text="

**Logicals** are either `TRUE` or `FALSE`. For example, whether a patient `has diabetes`, `is pregnan`t, or `is a smoker`.

```r
has_allergies <- TRUE
is_smoker     <- FALSE
```
" %}

{% include question.html header="On to Checking Data Types" text="

You can use the `class()` function to check the data type of any variable.
For example, is a lab result value \"42\" stored as text or as a number?

" solution="
```r
result <- \"42\"
class(result)   # Output: \"character\"

value <- 42
class(value)    # Output: \"numeric\"

value_int <- 42L
class(value_int) # Output: \"integer\"
```
" %}

{% include question.html header="Converting Between Data Types" text="

In many datasets, data imported from hospital systems may be stored as text even if they represent numbers.

Converting them to `numeric` or `integer` allows you to perform calculations like `average age` or `mean blood glucose`.

```r
age_str <- \"25\"
age_int <- as.integer(age_str)
print(age_int + 5)   # Output: 30
```
" %}

{% include question.html header="Integer to character" text="

We can also do the reverse.

```r
patient_bmi <- 22.5
bmi_str     <- as.character(patient_bmi)
cat(\"Patient BMI is\", bmi_str, \"\n\")

# Output
# Patient BMI is 22.5 
```
" %}

{% include question.html header="Character to numeric" text="
```r
glucose_str   <- \"5.8\"
glucose_num   <- as.numeric(glucose_str)
print(glucose_num + 0.2)   # Output: 6
```
" %}

{% include question.html header="Numeric to integer (truncates decimal)" text="
```r
heart_rate <- as.integer(75.6)   # Result: 75
```

When converting from `numeric` to `integer`, **R removes (truncates) the decimal** — this is useful when you only need whole-number data, such as rounding heart rate readings.
" %}

{% include question.html header="Logical conversions" text="
```r
as.logical(1)     # TRUE  → e.g., 1 could represent \"Yes\" in a dataset
as.logical(0)     # FALSE → e.g., 0 could represent \"No\"
as.logical(\"\")    # NA    → empty strings become missing in R
as.logical(\"Yes\") # NA    → only \"TRUE\"/\"FALSE\"/\"T\"/\"F\" are recognized
```
Note: Unlike `Python`, `R` does not treat arbitrary non-empty strings as `TRUE`. Use explicit `TRUE`/`FALSE` values in your data wherever possible.
" %}

{% capture text %}
**Closing**

🩺 **In medical data analysis**, understanding data types ensures you store and analyze information correctly — for example, calculating the average age (integers or numerics) or comparing lab results (numerics) without errors.
{% endcapture %}
{% include alert.html text=text color=secondary %}
