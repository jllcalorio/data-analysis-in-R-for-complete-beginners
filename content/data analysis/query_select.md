---
section: Data Analysis with Python
nav_order: 4
title: Data Querying and Selection
topics: query, select, filter
---

When analyzing clinical or research data, we often need to **filter patients**, **extract specific variables**, or **identify subgroups** (e.g., diabetic patients with high glucose).

This section teaches you how to efficiently query and select relevant medical data using pandas.

{% include question.html header="Selecting Columns" text="

**Single column selection**

💡 *Use case:* Selecting only the **patient names** for anonymization or reporting.

```python
names = df['name']
print(f\"Names (Series): {type(names)}\")
```

**Multiple column selection**

💡 *Use case:* Extracting basic demographic and diagnosis data for a summary table.

```python
basic_info = df[['Name', 'Age', 'Diagnosis']]
print(f\"Basic info (DataFrame): {type(basic_info)}\")
```

**Column selection with conditions**

💡 *Use case:* Identifying all numeric variables (e.g., blood pressure, glucose) for statistical analysis.

```python
numeric_columns = df.select_dtypes(include=[np.number])
print(f\"Numeric columns: {list(numeric_columns.columns)}\")
```
" %}

{% include question.html header="Selecting Rows" text="

**Row selection by index**

💡 *Use case:* Quickly view the first few patient records.

```python
first_patient = df.iloc[0]          # First row
first_five_patients = df.iloc[0:5]  # First 5 rows
```

**Row selection by condition**

💡 *Use case:* Filtering patients with **hyperglycemia** or a specific medical condition.

```python
high_glucose = df[df['Glucose'] > 150]
hypertensive_patients = df[df['Diagnosis'] == 'Hypertension']

print(f\"High glucose patients: {len(high_glucose)}\")
print(f\"Hypertensive patients: {len(hypertensive_patients)}\")
```

**Multiple conditions**

💡 *Use case:* Identify **high-risk patient groups** for focused analysis.

```python
elderly_diabetics = df[(df['Age'] > 60) & (df['Diagnosis'] == 'Diabetes')]
young_healthy = df[(df['Age'] < 30) & (df['Diagnosis'] == 'Healthy')]

print(f\"Elderly diabetics: {len(elderly_diabetics)}\")
print(f\"Young healthy individuals: {len(young_healthy)}\")
```
" %}

{% include question.html header="Advanced Querying" text="

**Using ```query``` method (more readable for complex conditions)**

💡 *Use case:* Query diabetic patients with hypertension or recent hospital admissions.

```python
high_bp_diabetics = df.query('Diagnosis == \"Diabetes\" and Blood_Pressure > 140')
recent_admissions = df.query('Admission_Date > \"2024-01-01\"')

print(f\"High BP diabetics: {len(high_bp_diabetics)}\")
print(f\"Recent admissions: {len(recent_admissions)}\")
```

**Using ```isin``` for multiple values**

💡 *Use case:* Selecting patients with comorbidities.

```python
target_conditions = df[df['Diagnosis'].isin(['Diabetes', 'Hypertension'])]
print(f\"Patients with Diabetes or Hypertension: {len(target_conditions)}\")
```

**String operations**

💡 *Use case:* Useful for **data cleaning or searching names**.

```python
patients_with_a = df[df['Name'].str.contains('a', case=False)]
print(f\"Patients with 'a' in name: {len(patients_with_a)}\")
```
" %}

{% capture text %}
**Key Takeaways**

- You can **select and filter** medical data easily using pandas.
- Use **row and column selection** to extract specific patient subsets.
- **Conditional filtering** allows targeted analysis (e.g., high-risk patients, comorbidities).
- The ```query()``` method makes complex filters more readable and natural.
- These skills are essential for **clinical research**, **public health analytics**, and **hospital record management**.
{% endcapture %}
{% include alert.html text=text color=secondary %}
