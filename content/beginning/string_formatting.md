---
section: Beginning Python
nav_order: 8
title: String Formatting
topics: string, format
---

**String formatting** makes your output clean, readable, and useful for generating patient summaries, research reports, or formatted outputs from clinical data.

{% include question.html header="f-strings (Recommended - Python 3.6+)" text="

Set the data.

```python
name = \"Dr. Santos\"
age = 45
bp = \"130/85\"
diagnosis = \"Hypertension\"
```
You can combine text and variable values neatly using ```f-strings```, perfect for generating dynamic summaries or reports.

```python
message = f\"Patient seen by {name}, age {age}, with a diagnosis of {diagnosis}.\"
print(message)

# Patient seen by Dr. Santos, age 45, with a diagnosis of Hypertension.
```

You can also format numerical outputs — for instance, when displaying lab results or computed values:

```python
glucose = 92.457
print(f\"Fasting blood glucose: {glucose:.1f} mg/dL\")  # Fasting blood glucose: 92.5 mg/dL
print(f\"Fasting blood glucose: {glucose:.0f} mg/dL\")  # Fasting blood glucose: 92 mg/dL
```
" %}

{% include question.html header=".format() Method" text="

Before f-strings, Python commonly used the .format() method — it’s still useful and readable:

```python
patient_name = \"Maria Cruz\"
age = 60
bp = \"150/90\"

message = \"Patient {} ({} y/o) has a BP reading of {}.\".format(patient_name, age, bp)
print(message)

# Patient Maria Cruz (60 y/o) has a BP reading of 150/90.

```

This approach is especially useful when your variables are defined elsewhere in your program, such as when reading from files or data entry forms.
" %}

{% include question.html header="String Methods" text="

Python includes many built-in methods to clean or modify text — perfect when cleaning raw data (like patient notes or survey entries).

```python
text = \"  Hypertension Stage II  \"

print(text)                                 #   Hypertension Stage II  
print(text.upper())                         #   HYPERTENSION STAGE II
print(text.lower())                         #   hypertension stage ii
print(text.strip())                         # Hypertension Stage II (removes whitespace)
print(text.replace(\"Stage II\", \"Stage I\"))  #   Hypertension Stage I
```

Splitting and joining

Useful for converting comma-separated values (like lab results or medication lists) into lists for easier analysis.

```python
medications = \"Aspirin,Metformin,Lisinopril\"
med_list = medications.split(\",\")      # ['Aspirin', 'Metformin', 'Lisinopril']
rejoined = \" | \".join(med_list)        # Aspirin | Metformin | Lisinopril

print(medications)
print(med_list)
print(rejoined)
```
" %}

{% capture text %}
**String formatting** helps you present data in clear, readable, and professional ways — whether you’re summarizing patient data, generating reports, or printing analysis results. Clean text formatting is essential in medical reporting and data communication.
{% endcapture %}
{% include alert.html text=text color=secondary %}
