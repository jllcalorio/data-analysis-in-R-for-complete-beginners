---
section: Beginning R
nav_order: 3
title: Variables
topics: variable, data, values, comments
---

**Variables** are like **containers that store information** — think of them as labeled drawers where you can keep different kinds of data such as a `patient's name`, `age`, or `blood pressure`.

In R, you assign values to variables using the arrow operator `<-`. R automatically figures out the data type for you!

{% include question.html header="Creating variables is simple." text="

It's not an exaggeration that variables are going to be your friends in the long run.

```r
patient_name <- \"Maria Santos\"
patient_age  <- 45
patient_bmi  <- 24.6
has_diabetes <- TRUE

print(patient_name)   # Output: Maria Santos
print(patient_age)    # Output: 45
```

**Example context:** Imagine you're storing basic information from a patient's medical record — each variable holds one detail about the patient.

**Mini Exercise**

**Try It Yourself 🧠**

Create three variables to store:

- A patient's heart rate (in beats per minute)
- Their body temperature (in °C)
- Whether they are currently admitted (TRUE or FALSE)

Then, print all three variables!

" solution="
```r
# Use your own variables and values
heart_rate <- 140
body_temp  <- 36.4
admitted   <- TRUE

# Print the results using the \"print\" function
print(heart_rate)   # 140
print(body_temp)    # 36.4
print(admitted)     # TRUE
```
" %}

{% include question.html header="Bonus: Comments" text="

Comments are lines in the code that are ignored by R and serve as notes or explanations for humans reading the code. In healthcare data analysis, comments are useful when explaining what part of the data your code is processing, such as

- `# Calculate average blood pressure per patient or`
- `# Filter data for diabetic patients only.`

A comment starts with the # symbol and continues to the end of the line.

Example:

```r
# Store blood pressure readings of 2 patients
bp_1 <- 120
bp_2 <- 130

# Calculate average blood pressure
average_bp <- (bp_1 + bp_2) / 2
average_bp                           # 125
```
" %}

{% include question.html header="Variable Naming Rules" text="

Must start with a letter or a dot (`.`) not followed by a number
Can contain letters, numbers, underscores, and dots
Case-sensitive (`name` and `Name` are different)
Cannot use R reserved words (like `if`, `for`, `while`, `TRUE`, `FALSE`, `NULL`)
Use lowercase letters with underscores (snake_case) for variable names
Make names meaningful and specific to their purpose


💡 **Pro tip:** In medical or research projects, use clear, descriptive names like `blood_glucose_level` or `patient_weight_kg`. This makes your code easier for colleagues or research assistants to understand.
" %}

{% include question.html header="Variable Naming Practices" text="

**Good variable names**

```r
patient_id         <- \"P001\"
blood_glucose_mgdl <- 95
is_fasting         <- TRUE
```

**Avoid these**

```r
x           <- \"P001\"      # Not descriptive
patientName <- \"Maria\"     # Prefer snake_case
2patient    <- \"invalid\"   # Cannot start with a number — this will error
```
" %}

{% capture text %}
🧩 **Why this matters:**

In data science and healthcare analytics, variable names help you understand what data you're working with — just like clearly labeling patient charts ensures accurate communication in clinical settings.
{% endcapture %}
{% include alert.html text=text color=secondary %}
