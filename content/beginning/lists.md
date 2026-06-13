---
section: Beginning Python
nav_order: 6
title: Lists
topics: list, collection, multiple data storing
---

**Lists** can store multiple types of data, not just medical or clinical data. For instance, a hospital system might store a list of patient names, lab test results, or vital signs in a list and even salaries.

They're one of the most useful data structures in Python!

{% include question.html header="Creating Lists" text="

Lists in Python can be of any type: integers, strings, floats, Booleans, even other lists.

```python
# Empty list
empty_list = [] # Can be used to initialize a list as a container of results

# List with items
# Example: list of patient names
patients = ['Alice', 'Ben', 'Carla', 'David']

# Example: list of blood pressure readings (mmHg)
bp_readings = [120, 130, 110, 140]

# Example: mixed list of different data types
patient_info = ['John Doe', 45, 72.5, True]  # name, age, weight(kg), is_admitted
```
" %}

{% include question.html header="Accessing List Items" text="

Items in lists can be accessed using their ```index```. The index (or position) of the item in a list start at 0.

Thus, in ```patients = ['Alice', 'Ben', 'Carla', 'David']```, the index of Alice is 0, and the index of Ben is 1.

Weirdly, the index of the last item in the list is -1, while the 2nd to the last index is -2. Try it out in your PC!

**Tip:** In R, the index starts at 1.

```python
# Accessing by index (starts at 0)
print(patients[0])   # First patient: Alice
print(patients[1])   # Second patient: Ben
print(patients[-1])  # Last patient: David
print(patients[-2])  # Second to last: Carla
```

In clinical data, indexing can be used to retrieve specific patient records or lab results from a list.
" %}

{% include question.html header="List Methods" text="

These list methods are used when you want to:

- add item/s in the list (whether at the end or at a specific index)
- remove item/s in the list
- inspect/count items in a list
- reordering or copying items in a list

```python
patients = ['Alice', 'Ben']
```
Adding items

```python
patients.append('Carla')            # Add to end
patients.insert(1, 'David')         # Insert at position 1
print(patients)                     # ['Alice', 'David', 'Ben', 'Carla']
```
Removing items

```python
patients.remove('David')            # Remove specific patient
last_patient = patients.pop()       # Remove and return last patient
print(patients)                     # ['Alice', 'Ben']
print(last_patient)                 # Carla
```
Other useful methods

```python
patients.extend(['Ella', 'Fred'])   # Adding multiple new patients
print(len(patients))                # Get total count of patients: 4
print(patients.count('Alice'))      # Count occurrences of a specific patient: 1
```

These list operations are common when managing patient registries, lists of medications, or data collected in clinical studies.
" %}

{% include question.html header="List Slicing" text="

Slicing allows you to extract a portion of a list using a concise syntax.

It follows this syntax: ```list_name[start:stop:step]```

```python
temperatures = [36.5, 37.1, 36.8, 37.5, 38.0, 36.9, 37.2, 36.7, 37.3, 37.0]

print(temperatures[2:5])   # Readings 2 to 4: [36.8, 37.5, 38.0]
print(temperatures[:3])    # First 3 readings
print(temperatures[7:])    # Last few readings
print(temperatures[::2])   # Every second reading
print(temperatures[::-1])  # Readings in reverse order
```

**Slicing** is helpful when selecting subsets of data — for instance, extracting readings for a ```specific day``` or ```patient```.
" %}


{% capture text %}
Lists allow you to store and organize multiple pieces of related data in one place. In medicine, this could represent a patient’s list of medications, recorded temperatures, or test results. They’re flexible, easy to manipulate, and fundamental in handling repeated or time-series data.
{% endcapture %}
{% include alert.html text=text color=secondary %}
