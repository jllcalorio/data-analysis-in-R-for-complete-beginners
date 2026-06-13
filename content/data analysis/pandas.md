---
section: Data Analysis with Python
nav_order: 2
title: Introduction to Pandas
topics: pandas, DataFrame, structured data
---

**Pandas** is the cornerstone of medical data analysis in Python. It allows you to organize, clean, and analyze structured data — similar to how you might handle patient records or hospital information in Excel or EHR systems.

With pandas, you can easily handle datasets containing patient demographics, lab results, or hospital statistics — making it an essential tool for **clinical research, epidemiology, and medical audits**.

## Key Data Structures in pandas

{% include question.html header="Series – One-Dimensional Data" text="

A **Series** is like a column in a spreadsheet — it holds a single type of data, such as patients’ ages or cholesterol levels.

**Example:** Creating a Series of patients’ ages

```python
import pandas as pd

ages = pd.Series([34, 45, 29, 50, 41],
                 index=['Ana', 'Luis', 'Maria', 'Jose', 'Carmen'])

print(ages)
print(f\"Data type: {ages.dtype}\")
print(f\"Shape: {ages.shape}\")

# Basic operations
print(f\"Mean age: {ages.mean()}\")
print(f\"Oldest patient: {ages.idxmax()}\")
```
" %}

{% include question.html header="DataFrame – Two-Dimensional Data" text="

A **DataFrame** is like a full spreadsheet (Like Microsoft Excel or Google Sheets) or a patient table — rows represent patients, and columns represent variables (e.g., age, diagnosis, or lab values).

**Example:** Creating a DataFrame of patient information

```python
data = {
    'Patient_ID': [101, 102, 103, 104, 105],
    'Name': ['Ana', 'Luis', 'Maria', 'Jose', 'Carmen'],
    'Age': [34, 45, 29, 50, 41],
    'Diagnosis': ['Diabetes', 'Hypertension', 'Healthy', 'Diabetes', 'Hypertension'],
    'Cholesterol': [210, 190, 170, 250, 230]
}

df = pd.DataFrame(data)
```

**Inspecting the DataFrame:**

Let’s check its structure and summary. Some ```print``` functions to see what are the characteristics of ```data```.

```python
print(df)
print(f\"DataFrame shape: {df.shape}\")
print(f\"Column names: {list(df.columns)}\")
print(f\"Data types:\n{df.dtypes}\")
```
" %}

{% include question.html header="DataFrame Inspection Methods" text="

Pandas provides several ways to **quickly explore and summarize** your dataset.

**This code prints the 1st 3 rows of the DataFrame.**

```python
print(df.head(3))
```

**This code prints the last 2 rows of the DataFrame.**

```python
print(df.tail(2))
```

**This code prints the some information about the DataFrame.**

```python
print(df.info())
```

**This code prints quick and simple descriptive statistics for the DataFrame.**

```python
print(df.describe())
```

**This code prints column-specific information from a DataFrame.**

```python
print(df['Diagnosis'].value_counts())  # Frequency of each diagnosis
print(df['Cholesterol'].mean())        # Average cholesterol level
```
" %}

{% capture text %}
- **pandas** is essential for managing structured datasets — just like a digital spreadsheet for clinical data.
- A **Series** represents a single column of medical data (e.g., patient age or blood pressure).
- A **DataFrame** is a full table of patient information (e.g., demographics, diagnoses, lab values).
- You can **inspect, summarize, and analyze** datasets efficiently using pandas methods.
- This skill is crucial for **research, quality assurance, and data-driven healthcare decisions**.
{% endcapture %}
{% include alert.html text=text color=secondary %}
