---
section_id: Beginning R
nav_order: 10
title: Practice Exercises
topics: exercises
---

{% include question.html header="Exercise 1: Medical Staff Profile" text="Create a program that:

- Stores a healthcare worker's basic information (name, age, department)
- Calculates their year of birth
- Creates a formatted introduction message

" solution="
```r
name         <- \"Dr. Maria Santos\"
age          <- 35
department   <- \"Pediatrics\"
current_year <- 2026

birth_year <- current_year - age
intro <- sprintf(\"Hi! I'm %s, a %d-year-old physician from the %s department, born in %d.\",
                 name, age, department, birth_year)

print(intro)
```
" %}

{% include question.html header="Exercise 2: Medication Inventory Manager" text="Create a program that:

- Starts with a vector of medications
- Adds new medications to the vector
- Removes one discontinued medication
- Prints the final list with numbering

" solution="
```r
med_inventory <- c(\"Paracetamol\", \"Amoxicillin\", \"Ibuprofen\", \"Metformin\", \"Amlodipine\")
med_inventory <- c(med_inventory, \"Cefalexin\", \"Losartan\")   # Add new medications
med_inventory <- med_inventory[med_inventory != \"Ibuprofen\"]   # Remove discontinued

cat(\"Medication Inventory:\n\")
for (i in seq_along(med_inventory)) {
  cat(i, \".\", med_inventory[i], \"\n\", sep = \"\")
}
```
" %}

{% include question.html header="Exercise 3: Grade Calculator" text="Create a program that:

- Stores student information in a list
- Calculates the average grade
- Determines letter grade based on average
- Prints a formatted report

" solution="
```r
student <- list(
  name   = \"Alice\",
  grades = c(85, 92, 78, 96, 88)
)

average <- mean(student$grades)

if (average >= 90) {
  letter_grade <- \"A\"
} else if (average >= 80) {
  letter_grade <- \"B\"
} else if (average >= 70) {
  letter_grade <- \"C\"
} else if (average >= 60) {
  letter_grade <- \"D\"
} else {
  letter_grade <- \"F\"
}

cat(\"Student:\", student$name, \"\n\")
cat(\"Grades:\", paste(student$grades, collapse = \", \"), \"\n\")
cat(sprintf(\"Average: %.1f\n\", average))
cat(\"Letter Grade:\", letter_grade, \"\n\")
```
" %}

{% include question.html header="Exercise 4: Patient Vital Score Calculator" text="Create a program that:

- Stores a patient's recorded vital scores (e.g., from multiple checkups)
- Calculates the average
- Categorizes the patient's overall condition

" solution="
```r
patient <- list(
  name      = \"Juan Dela Cruz\",
  bp_scores = c(120, 130, 125, 128, 118)
)

average <- mean(patient$bp_scores)

if (average >= 140) {
  condition <- \"Hypertensive\"
} else if (average >= 120) {
  condition <- \"Prehypertensive\"
} else {
  condition <- \"Normal\"
}

cat(\"Patient:\", patient$name, \"\n\")
cat(\"BP Readings:\", paste(patient$bp_scores, collapse = \", \"), \"\n\")
cat(sprintf(\"Average BP: %.1f\n\", average))
cat(\"Condition:\", condition, \"\n\")
```
" %}

{% include question.html header="Exercise 5: Health Record Access Validator" text="Create a function that validates a hospital staff's password before they can access patient records:

- At least 8 characters long
- Contains at least one number
- Contains at least one uppercase letter

" solution="
```r
validate_password <- function(password) {
  if (nchar(password) < 8) {
    return(list(valid = FALSE, message = \"Password must be at least 8 characters long\"))
  }

  has_number <- grepl(\"[0-9]\", password)
  has_upper  <- grepl(\"[A-Z]\", password)

  if (!has_number) {
    return(list(valid = FALSE, message = \"Password must contain at least one number\"))
  }

  if (!has_upper) {
    return(list(valid = FALSE, message = \"Password must contain at least one uppercase letter\"))
  }

  return(list(valid = TRUE, message = \"Password is valid\"))
}

# Test the function
test_passwords <- c(\"weak\", \"StrongPass1\", \"nodigits\", \"NONUMBERS\")

for (pwd in test_passwords) {
  result <- validate_password(pwd)
  cat(sprintf(\"'%s': %s\n\", pwd, result$message))
}
```
" %}

{% capture text %}
**Good luck!!!**
{% endcapture %}
{% include alert.html text=text color=secondary %}
