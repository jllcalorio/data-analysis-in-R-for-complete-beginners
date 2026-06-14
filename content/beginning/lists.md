---
section_id: Beginning R
nav_order: 6
title: Vectors and Lists
topics: vector, list, collection, multiple data storing
---

In R, we use **Vectors** for collections of the same type (like a list of ages) and Lists for collections that can hold different types (like a patient record).

{% include question.html header="Creating Vectors and Lists" text="

Vectors are created using `c() `(combine).

```r
# Vector of patient names
patients <- c(\"Alice\", \"Ben\", \"Carla\", \"David\")

# Vector of blood pressure readings
bp_readings <- c(120, 130, 110, 140)

# Lists can store mixed data types
patient_info <- list(\"John Doe\", 45, 72.5, TRUE)
```
" %}

{% include question.html header="Accessing Items (1-Based Indexing)" text="

**Important:** In R, indexing starts at `1`.

```r
# Accessing items
print(patients[1])   # First patient:  Alice
print(patients[2])   # Second patient: Ben
print(patients[4])   # Fourth patient: David
```

In clinical data, indexing retrieves specific records or results.
" %}

{% include question.html header="Modifying Collections" text="

```r
patients <- c(\"Alice\", \"Ben\")

# Adding items
patients <- c(patients, \"Carla\")       # Add to end
print(patients)                          # \"Alice\" \"Ben\" \"Carla\"

# Removing items (using negative index)
patients <- patients[-1]                 # Removes the FIRST item
print(patients)                          # \"Ben\" \"Carla\"

# Getting total count
length(patients)                         # 2
```
" %}

{% include question.html header="Vector Slicing" text="

Slicing in R uses the `start:stop` syntax (both ends inclusive).

```r
temperatures <- c(36.5, 37.1, 36.8, 37.5, 38.0, 36.9)

print(temperatures[2:4])   # 2nd to 4th readings: 37.1 36.8 37.5
print(temperatures[1:3])   # First 3 readings
```
" %}

{% capture text %}
Vectors and lists allow you to organize related data. In medicine, this could represent a patient's list of medications or recorded temperatures.
{% endcapture %}
{% include alert.html text=text color=secondary %}
