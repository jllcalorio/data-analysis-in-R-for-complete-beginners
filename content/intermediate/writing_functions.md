---
section_id: Intermediate Python
nav_order: 1
title: Writing Functions
topics: functions
---

**Functions** are the building blocks of well-organized code. They let you write logic once and reuse it across multiple scenarios — an essential skill when automating tasks like calculating BMI, summarizing lab results, or cleaning patient datasets.

{% include question.html header="Function Basics Review" text="

Let's say we want to create a function that greets a patient when their name is entered into a system.

```r
greet <- function(name) {
  # A simple function that greets someone.
  return(paste0(\"Hello, \", name, \"! Welcome to your appointment.\"))
}
```

Call the function:

```r
message <- greet(\"Dr. Reyes\")
print(message)                   # Output: Hello, Dr. Reyes! Welcome to your appointment.
```
" %}

# Advanced Function Features

{% include question.html header="Default Parameters" text="

Let's define a function that creates a **basic patient profile** — similar to what you'd store in an electronic medical record (EMR).

```r
create_profile <- function(name, age, city = \"Davao\", diagnosis = \"Not yet diagnosed\") {
  # Create a patient profile with default values.
  profile <- list(
    name      = name,
    age       = age,
    city      = city,
    diagnosis = diagnosis
  )
  return(profile)
}
```

Run the function using

1. default parameters and
2. custom parameters:

```r
patient1 <- create_profile(\"Ana Santos\", 35)
patient2 <- create_profile(\"Miguel Cruz\", 58, \"Davao\", \"Hypertension\")

print(patient1)   # city and diagnosis use defaults
print(patient2)   # all parameters specified
```
" %}

{% include question.html header="Variable-Length Arguments with ..." text="

R uses `...` (the ellipsis) to pass a variable number of arguments to a function.

**Example 1:** Calculate average blood glucose readings:

```r
calculate_average <- function(...) {
  # Calculate average of any number of readings.
  values <- c(...)
  if (length(values) == 0) return(0)
  return(mean(values))
}
```

**Example 2:** Create a patient record with flexible fields using a named list:

```r
create_patient_record <- function(name, ...) {
  # Create a patient record with flexible information.
  extra <- list(...)
  record <- c(list(name = name), extra)
  return(record)
}
```

Use the functions:

```r
avg_glucose <- calculate_average(92, 110, 87, 105)
cat(sprintf(\"Average Glucose: %.1f mg/dL\n\", avg_glucose))

patient <- create_patient_record(
  \"Maria Dela Cruz\",
  age         = 47,
  condition   = \"Diabetes\",
  medications = c(\"Metformin\", \"Insulin\"),
  last_visit  = \"2025-09-10\"
)
print(patient)
```
" %}

{% include question.html header="Anonymous Functions" text="

R supports anonymous (inline) functions — compact, one-line functions useful for quick calculations or passing logic to other functions.

```r
# Named function
bmi <- function(weight, height) weight / (height ^ 2)

# Anonymous function equivalent (R 4.1+ shorthand)
bmi_anon <- \\(weight, height) weight / (height ^ 2)

print(bmi_anon(70, 1.75))   # Output: 22.85714
```

Filtering a list of patients using `Filter()`:

```r
patients <- list(
  list(name = \"Ana\",   bmi = 22.5),
  list(name = \"Ben\",   bmi = 29.8),
  list(name = \"Clara\", bmi = 18.9)
)

# Get only overweight patients (BMI >= 25)
overweight <- Filter(\\(p) p$bmi >= 25, patients)
print(overweight)
```

**Advantages of anonymous functions:**

- Defined inline without naming
- Ideal for short, single-use logic inside functions like `Filter()`, `Map()`, `sapply()`

**Disadvantages:**

- Can reduce readability if overused or applied to complex logic
- For multi-step operations, a named function is usually clearer

Another example using `sapply()`:

```r
numbers <- 1:5
squared <- sapply(numbers, \\(x) x ^ 2)
print(squared)   # 1  4  9 16 25

students <- list(
  list(name = \"Alice\",   grade = 85),
  list(name = \"Bob\",     grade = 92),
  list(name = \"Charlie\", grade = 78)
)

high_performers <- Filter(\\(s) s$grade >= 85, students)
print(high_performers)
```
" %}

{% capture text %}
Functions let you **automate repetitive tasks**, from **calculating averages** of lab results to **generating formatted patient summaries**.

They make your code **modular, reusable, and easier to understand**, especially when analyzing multiple patient records or large datasets.
{% endcapture %}
{% include alert.html text=text color=secondary %}
