---
section: Beginning R
nav_order: 7
title: Named Lists
topics: list, store values, key-value pairs
---

In R, **Named Lists** are used to store data in *key-value pairs*. They're perfect for organizing related information of different types!

{% include question.html header="Creating Named Lists" text="

**Lists** are great for storing structured data — like a patient’s `demographic information`, `diagnosis`, and `vital signs` — **all in one variable**.

```r
# Empty list
empty_list <- list()

# List with data
patient_record <- list(
    name        = \"John Doe\",
    age         = 45,
    sex         = \"Male\",
    diagnosis   = \"Hypertension\",
    bp          = \"140/90\",
    is_admitted = TRUE
)

print(patient_record)
# $name
# [1] \"John Doe\"
#
# $age
# [1] 45
#
# $sex
# [1] \"Male\"
#
# $diagnosis
# [1] \"Hypertension\"
#
# $bp
# [1] \"140/90\"
#
# $is_admitted
# [1] TRUE
```
" %}

{% include question.html header="Accessing List Values" text="
```r
print(patient_record$diagnosis)     # Hypertension
print(patient_record$bp)            # 140/90
print(patient_record$heart_rate)    # NULL (Default if doesn't exist)
```

This is like checking a patient’s chart — if a piece of information doesn’t exist, R can return a default value (e.g., `NULL`).
" %}

{% include question.html header="Updating and Adding to a List" text="

You can access items using the `$` symbol or double brackets `[[ ]]`

```r
patient_record$bp         <- \"130/85\"   # Update blood pressure
patient_record$heart_rate <- 72         # Add new key-value pair, added at the end of the list

print(patient_record)
# $name
# [1] \"John Doe\"
#
# $age
# [1] 45
#
# $sex
# [1] \"Male\"
#
# $diagnosis
# [1] \"Hypertension\"
#
# $bp
# [1] \"130/85\"
#
# $is_admitted
# [1] TRUE
#
# $heart_rate
# [1] 72
```

**Removing items**

```r
patient_record$is_admitted <- NULL   # Remove item by setting to NULL

print(patient_record)
# $name
# [1] \"John Doe\"
#
# $age
# [1] 45
#
# $sex
# [1] \"Male\"
#
# $diagnosis
# [1] \"Hypertension\"
#
# $bp
# [1] \"130/85\"
#
# $heart_rate
# [1] 72
```
" %}

{% include question.html header="List Metadata" text="

```r
# Get all labels
names(patient_record)    # [1] \"name\" \"age\" \"sex\" \"diagnosis\" \"bp\" \"heart_rate\"

# Get number of items
length(patient_record)   # [1] 6
```

**In hospital data systems**, you might check if certain patient information (like `temperature` or `lab_results`) exists before performing calculations or updates.
" %}

{% capture text %}
Imagine you’re developing a script to summarize patient data — how could lists help you store and retrieve each patient’s details efficiently?

Think of one real-world scenario in your medical or research setting where a list structure could simplify your workflow.
{% endcapture %}
{% include alert.html text=text color=secondary %}
