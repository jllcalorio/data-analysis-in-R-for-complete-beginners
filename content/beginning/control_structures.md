---
section: Beginning R
nav_order: 9
title: Control structures
topics: loop, if, for, while, functions
---

**Control structures** determine **the order in which your code executes**, allowing you to create decision-making and repetition logic that drives your program's behavior in R.

Control structures can automate workflows such as checking patient eligibility, iterating over lab results, or categorizing patients based on diagnostic criteria.

{% include question.html header="If Statements" text="

The `if` statement is used for conditional execution, allowing a block of code to run only if a specified condition is true. This is done to create decision-making logic in your programs.

```r
age <- 72
bp  <- 145

if (age >= 60 & bp > 140) {
  print(\"High-risk: Schedule follow-up consultation.\")
} else if (age >= 60 & bp <= 140) {
  print(\"Monitor regularly.\")
} else {
  print(\"Low-risk: Maintain routine check-ups.\")
}

# Output
# \"High-risk: Schedule follow-up consultation.\"
```

The code above helps automatically classify patients based on age and blood pressure (`bp`) readings, similar to decision rules used in clinical triage systems.
" %}

{% include question.html header="For Loops" text="

`for` loops repeat a block of code for each item in a collection. They are crucial for automating repetitive tasks.

**Loop through a vector**

```r
patients <- c(\"Alice\", \"Bob\", \"Carlos\")
for (name in patients) {
  cat(\"Processing lab report for\", name, \"\n\")
}

# Output:
# Processing lab report for Alice
# Processing lab report for Bob
# Processing lab report for Carlos
```
This loop ensures that all patient reports are processed without manual repetition — useful when automating data cleaning or report generation for large datasets.

**Loop through a range of numbers**

```r
for (i in 0:4) {
  cat(\"Count:\", i, \"\n\")
}

# Output:
# Count: 0
# Count: 1
# Count: 2
# Count: 3
# Count: 4
```

**Loop through a named list**

```r
student <- list(name = \"Alice\", age = 20, is_diabetic = TRUE)

for (key in names(student)) {
  cat(key, \":\", as.character(student[[key]]), \"\n\")
}

# Output:
# name : Alice
# age : 20
# is_diabetic : TRUE
```
" %}

{% include question.html header="While Loops" text="

`while` loops repeat a block of code **as long as a condition is `TRUE`**.

**Basic `while` loop**

```r
count <- 0
while (count < 5) {
  cat(\"Count is\", count, \"\n\")
  count <- count + 1
}

# Output:
# Count is 0
# Count is 1
# Count is 2
# Count is 3
```

**`while` loop with a break condition**

```r
user_input <- \"\"
while (user_input != \"quit\") {
  user_input <- readline(prompt = \"Enter a command (or 'quit' to exit): \")
  if (user_input != \"quit\") {
    cat(\"You entered:\", user_input, \"\n\")
  }
}

# Output
# Enter a command (or 'quit' to exit): 10
# You entered: 10 
# Enter a command (or 'quit' to exit): 5
# You entered: 5 
# Enter a command (or 'quit' to exit): 1
# You entered: 1 
# Enter a command (or 'quit' to exit): 0
# You entered: 0 
# Enter a command (or 'quit' to exit): quit
```

After the user inputs the word \"quit\", the loop ends.

Note: `readline()` is used for interactive console input in R. In scripts or R Markdown, user input is typically handled differently.
" %}

{% include question.html header="Functions" text="

**Functions** are *reusable blocks of code* designed to perform a specific task. They are used to break down complex problems into smaller, manageable pieces, promote code reusability, and improve the organization and readability of your programs.

**Basic function**

```r
greet <- function(name) {
  return(paste(\"Hello,\", name, \"!\"))
}
```

**Function with default parameters**

```r
introduce <- function(name, age = 25) {
  return(paste0(\"Hi, I'm \", name, \" and I'm \", age, \" years old.\"))
}
```

**Function with multiple parameters**

```r
calculate_area <- function(length, width) {
  area <- length * width
  return(area)
}
```

**Using the functions**

```r
message   <- greet(\"Alice\")
print(message)                                # Hello, Alice !

intro <- introduce(\"Bob\")                     # Uses default age
print(intro)                                  # Hi, I'm Bob and I'm 25 years old.

room_area <- calculate_area(10, 12)
cat(\"Room area:\", room_area, \"square feet\n\") # Room area: 120 square feet
```
" %}

{% include question.html header="Reusable Function for BMI Classification" text="

This function encapsulates a clinical rule (BMI categories), demonstrating how logic and computation combine to yield meaningful interpretations in healthcare analytics.

```r
classify_bmi <- function(weight_in_kg, height_in_meters) {
  bmi <- weight_in_kg / (height_in_meters ^ 2)
  if (bmi < 18.5) {
    return(\"Underweight\")
  } else if (bmi < 25) {
    return(\"Normal\")
  } else if (bmi < 30) {
    return(\"Overweight\")
  } else {
    return(\"Obese\")
  }
}

print(classify_bmi(70, 1.75))       # \"Normal\"
```
" %}

{% capture text %}
Note:
Remember the curly braces `{ }` in your `if`, `for`, and `while` statements and in your functions. They tell R which lines of code belong inside the block. **Good indentation (2 or 4 spaces) is strongly recommended for readability**, even though **R does not enforce** it like Python does.
{% endcapture %}
{% include alert.html text=text color=secondary %}
