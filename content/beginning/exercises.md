---
section: Beginning Python
nav_order: 10
title: Practice Exercises
topics: exercises
---

{% include question.html header="Exercise 1: Medical Staff Profile" text="Create a program that:

- Stores a healthcare worker’s basic information (name, age, department)
- Calculates their year of birth
- Creates a formatted introduction message
" solution="
```python
name = \"Dr. Maria Santos\"
age = 35
department = \"Pediatrics\"
current_year = 2025

birth_year = current_year - age
intro = f\"Hi! I'm {name}, a {age}-year-old physician from the {department} department, born in {birth_year}.\"

print(intro)
```
" %}

{% include question.html header="Exercise 2: Medication Inventory Manager" text="Create a program that:

- Create a program that:
- Starts with a list of medications
- Adds new medications to the list
- Removes one discontinued medication
- Prints the final list with numbering
" solution="
```python
med_inventory = [\"Paracetamol\", \"Amoxicillin\", \"Ibuprofen\", \"Metformin\", \"Amlodipine\"]
med_inventory.extend([\"Cefalexin\", \"Losartan\"])
med_inventory.remove(\"Ibuprofen\")

print(\"Medication Inventory:\")
for i, med in enumerate(med_inventory, 1):
    print(f\"{i}. {med}\")
```
" %}

{% include question.html header="Exercise 3: Grade Calculator" text="Create a program that:

- Stores student information in a dictionary
- Calculates the average grade
- Determines letter grade based on average
- Prints a formatted report
" solution="
```python
student = {
    \"name\": \"Alice\",
    \"grades\": [85, 92, 78, 96, 88]
}

average = sum(student[\"grades\"]) / len(student[\"grades\"])

if average >= 90:
    letter_grade = \"A\"
elif average >= 80:
    letter_grade = \"B\"
elif average >= 70:
    letter_grade = \"C\"
elif average >= 60:
    letter_grade = \"D\"
else:
    letter_grade = \"F\"

print(f\"Student: {student['name']}\")
print(f\"Grades: {student['grades']}\")
print(f\"Average: {average:.1f}\")
print(f\"Letter Grade: {letter_grade}\")
```
" %}

{% include question.html header="Exercise 4: Patient Vital Score Calculator" text="Create a program that:
- Stores a patient’s recorded vital scores (e.g., from multiple checkups)
- Calculates the average
- Categorizes the patient’s overall condition
" solution="
```python
patient = {
    \"name\": \"Juan Dela Cruz\",
    \"bp_scores\": [120, 130, 125, 128, 118]
}

average = sum(patient[\"bp_scores\"]) / len(patient[\"bp_scores\"])

if average >= 140:
    condition = \"Hypertensive\"
elif average >= 120:
    condition = \"Prehypertensive\"
else:
    condition = \"Normal\"

print(f\"Patient: {patient['name']}\")
print(f\"BP Readings: {patient['bp_scores']}\")
print(f\"Average BP: {average:.1f}\")
print(f\"Condition: {condition}\")
```
" %}

{% include question.html header="Exercise 5: Health Record Access Validator" text="Create a function that validates a hospital staff’s password before they can access patient records:

- At least 8 characters long
- Contains at least one number
- Contains at least one uppercase letter
" solution="
```python
def validate_password(password):
    if len(password) < 8:
        return False, \"Password must be at least 8 characters long\"

    has_number = any(char.isdigit() for char in password)
    has_upper = any(char.isupper() for char in password)

    if not has_number:
        return False, \"Password must contain at least one number\"

    if not has_upper:
        return False, \"Password must contain at least one uppercase letter\"

    return True, \"Password is valid\"

# Test the function
test_passwords = [\"weak\", \"StrongPass1\", \"nodigits\", \"NONUMBERS\"]
for pwd in test_passwords:
    is_valid, message = validate_password(pwd)
    print(f\"'{pwd}': {message}\")
```
" %}

{% capture text %}
**Good luck!!!**
{% endcapture %}
{% include alert.html text=text color=secondary %}
