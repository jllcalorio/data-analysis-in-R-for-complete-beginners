---
section: Beginning Python
nav_order: 7
title: Dictionaries
topics: dictionary, store values, key-value pairs
---

**Dictionaries** store data in *key-value pairs*. They're perfect for organizing related information!

{% include question.html header="Creating Dictionaries" text="

**Dictionaries** are great for storing structured data — like a patient’s ```demographic information```, ```diagnosis```, and ```vital signs``` — **all in one variable**.

```python
# Empty dictionary
empty_dict = {}

# Dictionary with data
patient_record = {
    \"name\": \"John Doe\",
    \"age\": 45,
    \"sex\": \"Male\",
    \"diagnosis\": \"Hypertension\",
    \"bp\": \"140/90\",
    \"is_admitted\": True
}

print(patient_record)
# {'name': 'John Doe', 'age': 45, 'sex': 'Male', 'diagnosis': 'Hypertension', 'bp': '140/90', 'is_admitted': True}
```
" %}

{% include question.html header="Accessing Dictionary Values" text="
```python
print(patient_record[\"diagnosis\"])              # Hypertension
print(patient_record.get(\"bp\"))                 # 140/90
print(patient_record.get(\"heart_rate\", \"N/A\"))  # N/A (Default if key doesn't exist)
```

This is like checking a patient’s chart — if a piece of information doesn’t exist, Python can return a default value (e.g., “N/A”).
" %}

{% include question.html header="Modifying Dictionaries" text="

Adding/updating values

```python
patient_record[\"bp\"] = \"130/85\"        # Update blood pressure
patient_record[\"heart_rate\"] = 72      # Add new key-value pair

print(patient_record)
# {'name': 'John Doe', 'age': 45, 'sex': 'Male', 'diagnosis': 'Hypertension', 'bp': '130/85', 'is_admitted': True, 'heart_rate': 72}
```

Removing items

```python
del patient_record[\"is_admitted\"]
removed_value = patient_record.pop(\"heart_rate\", \"Not found\")

print(patient_record)
# {'name': 'John Doe', 'age': 45, 'sex': 'Male', 'diagnosis': 'Hypertension', 'bp': '130/85'}
```
" %}

{% include question.html header="Dictionary Methods" text="

Get the keys

```python
print(patient_record.keys())     # dict_keys(['name', 'age', 'sex', 'diagnosis', 'bp'])
```

Get the values

```python
print(patient_record.values())   # dict_values(['John Doe', 45, 'Male', 'Hypertension', '130/85'])
```

Get the item pairs

```python
print(patient_record.items())    # dict_items([('name', 'John Doe'), ('age', 45), ('sex', 'Male'), ('diagnosis', 'Hypertension'), ('bp', '130/85')])
```

Check if key exists

```python
print(\"diagnosis\" in patient_record)  # True
print(\"temperature\" in patient_record)  # False
```

**In hospital data systems**, you might check if certain patient information (like ```temperature``` or ```lab_results```) exists before performing calculations or updates.
" %}

{% capture text %}
Imagine you’re developing a script to summarize patient data from an Excel file — how could dictionaries help you store and retrieve each patient’s details efficiently?

Think of one real-world scenario in your medical or research setting where a dictionary-like structure could simplify your workflow.
{% endcapture %}
{% include alert.html text=text color=secondary %}
