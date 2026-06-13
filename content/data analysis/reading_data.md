---
section: Data Analysis with Python
nav_order: 3
title: Reading and Loading Data
topics: read, import, pandas, csv
---

In medical research and hospital informatics, data often comes from **electronic health records (EHRs)**, **lab systems**, or **survey results** — usually in formats like CSV, Excel, or JSON.

This section will teach you how to **load these files into Python using pandas**, so you can begin analyzing them effectively.

{% include question.html header="Reading CSV Files" text="

CSV (Comma-Separated Values) is one of the most common formats for exporting medical data — from patient logs to laboratory results.

```python
import pandas as pd
import numpy as np

# Load clinical data
df = pd.read_csv('patients_data.csv')
print(df.head())
```

**Common Parameters When Reading CSV Files**

You can customize how your data is read:

```python
df_csv = pd.read_csv(
    'data.csv',
    sep=',',                         # Separator (default is comma)
    header=0,                        # Row to use as column names
    index_col=0,                     # Column to use as row index
    na_values=['N/A', 'NULL'],       # Treat these as missing
    parse_dates=['Admission_Date'],  # Automatically parse dates
    encoding='utf-8'                 # File encoding
)
```

**Creating and Saving Sample Medical Data**

Let’s create a simple medical dataset that simulates patient information:

```python
sample_data = pd.DataFrame({
    'Patient_ID': range(1, 101),
    'Name': [f'Patient_{i}' for i in range(1, 101)],
    'Age': np.random.randint(18, 80, 100),
    'Diagnosis': np.random.choice(['Diabetes', 'Hypertension', 'Healthy'], 100),
    'Blood_Pressure': np.random.randint(100, 180, 100),
    'Glucose': np.random.randint(70, 200, 100),
    'Admission_Date': pd.date_range('2024-01-01', periods=100, freq='W')
})

# Save sample data
sample_data.to_csv('sample_patients.csv', index=False)
print(\"Sample patient data created and saved!\")
```

Now you have a CSV file that simulates a hospital registry or research cohort.
" %}

{% include question.html header="Reading Other File Formats" text="

Medical data can also come in Excel, JSON, or even databases.

**Reading Excel files**

```python
df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet1')
```

**Reading JSON files**

```python
df_json = pd.read_json('data.json')
```

**Read SQL database (requires SQLAlchemy)**

```python
from sqlalchemy import create_engine
engine = create_engine('sqlite:///hospital.db')
df_sql = pd.read_sql('SELECT * FROM patients', engine)
```

**Working with Our Sample CSV**

For our workshop, let's work with the CSV we created

```python
df = pd.read_csv('sample_patients.csv')
df['Admission_Date'] = pd.to_datetime(df['Admission_Date'])

print(\"Data loaded successfully!\")
print(df.head())
```
" %}

{% include question.html header="Handling Missing Data" text="

Missing data is very common in medical research — for example, when a lab result isn’t recorded or a patient skips a follow-up visit.

Let’s simulate and handle missing values:

```python
df_with_missing = df.copy()
df_with_missing.loc[5:10, 'Glucose'] = np.nan
df_with_missing.loc[15:20, 'Diagnosis'] = np.nan

print(\"Missing data summary:\")
print(df_with_missing.isnull().sum())
```

**Strategies for handling missing data**

**Drop rows with missing values**

```python
df_dropped = df_with_missing.dropna()
```

**Fill missing values with default or statistical measures**

```python
df_filled = df_with_missing.fillna({
    'Glucose': df_with_missing['Glucose'].median(),
    'Diagnosis': 'Unknown'
})
```

**Forward fill or backward fill**

```python
df_ffill = df_with_missing.fillna(method='ffill')

print(f\"Original shape: {df_with_missing.shape}\")
print(f\"After dropping NaN: {df_dropped.shape}\")
print(f\"After filling NaN: {df_filled.shape}\")
```
" %}

{% capture text %}
**Key Takeaways**

- **pandas** allows you to easily load, explore, and **clean real-world medical data** from CSV, Excel, JSON, or databases.
- **Missing data** is common in healthcare datasets — learn to handle it responsibly through **filling, dropping, or flagging**.
- **CSV remains the most widely used format** for clinical and research data exchange.
- Understanding how to **properly import and clean data** is the first step in medical data analysis.
{% endcapture %}
{% include alert.html text=text color=secondary %}
