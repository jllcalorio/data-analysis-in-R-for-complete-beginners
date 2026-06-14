---
section: Intermediate R
nav_order: 6
title: Packages
topics: package, library, source, script
---

Understanding **packages** is essential to organizing your code and taking full advantage of R's extensive ecosystem. In healthcare and biomedical research, packages allow you to separate reusable logic — such as calculations, data cleaning, or patient analytics — into organized files and shareable bundles.

## What Are Packages?

A package is a collection of functions, datasets, and documentation stored in a standardized structure.

Any `.R` file can be sourced into another R script using `source()`. Formal packages are built with tools like `devtools` and submitted to CRAN or GitHub.

Packages help you:

- Reuse code across multiple projects
- Keep your code organized and maintainable
- Share your work with colleagues or research collaborators

{% include question.html header="Creating Your Own Script of Functions" text="

Let's create a file named medical_calculator.R — a simple script that performs **basic medical computations**.

**Example:** medical_calculator.R

This script provides basic biomedical calculations that could be used in clinical or research contexts.

```r
# medical_calculator.R

bmi <- function(weight, height) {
  # Calculate Body Mass Index.
  weight / (height ^ 2)
}

bsa <- function(weight, height) {
  # Calculate Body Surface Area (Mosteller formula).
  # weight in kg, height in cm
  sqrt((height * weight) / 3600)
}

mean_arterial_pressure <- function(systolic, diastolic) {
  # Calculate Mean Arterial Pressure (MAP).
  (2 * diastolic + systolic) / 3
}

temperature_c_to_f <- function(celsius) {
  # Convert Celsius to Fahrenheit.
  (celsius * 9 / 5) + 32
}

temperature_f_to_c <- function(fahrenheit) {
  # Convert Fahrenheit to Celsius.
  (fahrenheit - 32) * 5 / 9
}

# Module-level constants
NORMAL_BMI_RANGE   <- c(18.5, 24.9)
BODY_WATER_PERCENT <- 0.6

cat(\"Medical Calculator script loaded successfully.\n\")
```

**Self-test block** (runs only when the file itself is executed directly):

```r
if (sys.nframe() == 0) {
  cat(\"Running tests for Medical Calculator...\n\")
  cat(sprintf(\"BMI (70 kg, 1.75 m): %.2f\n\", bmi(70, 1.75)))
  cat(sprintf(\"BSA (70 kg, 175 cm): %.2f\n\", bsa(70, 175)))
  cat(sprintf(\"MAP (120/80 mmHg):   %.2f\n\", mean_arterial_pressure(120, 80)))
}
```
" %}

{% include question.html header="Using Your Script" text="

Now create another file, main.R, where we source and use our script.

```r
source(\"medical_calculator.R\")
```

**Use functions from the script:**

```r
bmi_value <- bmi(65, 1.68)
map_value <- mean_arterial_pressure(118, 76)

cat(sprintf(\"BMI: %.2f\n\",                         bmi_value))
cat(sprintf(\"Mean Arterial Pressure: %.1f mmHg\n\", map_value))
```

**Using specific functions after sourcing**

Because **source()** loads everything in the file, all functions are immediately available in your environment. You can then call any of them directly:

```r
cat(sprintf(\"BMI: %.2f\n\",           bmi(58, 1.60)))
cat(sprintf(\"BSA: %.2f\n\",           bsa(58, 160)))
cat(sprintf(\"Temperature: %.1f°F\n\", temperature_c_to_f(37)))
```
" %}

{% include question.html header="🩺 Why This Matters?" text="
Using scripts and packages helps healthcare professionals, researchers, and data analysts reuse and standardize computations across projects.

For example:

- Standardize BMI formulas for all datasets
- Maintain consistency in how blood pressure is interpreted
- Reduce errors when analyzing patient data
" %}

{% capture text %}
Scripts and packages make your **code modular, reusable, and easier to maintain** — crucial for building reliable healthcare tools and analysis pipelines.

Whether you're creating a clinical calculator, automating data cleaning, or building a patient outcome model, modular programming ensures **accuracy, collaboration, and scalability**.
{% endcapture %}
{% include alert.html text=text color=secondary %}