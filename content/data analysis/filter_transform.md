---
section: Data Analysis with Python
nav_order: 5
title: Data Filtering and Transformation
topics: filtering, transformation
---

**Transforming data** helps uncover patterns in **patient records**, **clinical measurements**, and **laboratory results**.

In medical data analysis, we often group data (e.g., by hospital department or diagnosis), compute summary statistics (e.g., average glucose by group), and create derived variables such as BMI or risk categories.

{% include question.html header="Grouping and Aggregation" text="

**Basic ```groupby``` operations**

```python
dept_stats = df.groupby('Department').agg({
    'Blood_Pressure': ['mean', 'median', 'std', 'count'],
    'Age': ['mean', 'min', 'max']
}).round(2)

print(\"Department statistics:\")
print(dept_stats)
```

**Custom aggregation functions**

```python
def bp_range(series):
    return series.max() - series.min()

custom_stats = df.groupby('Diagnosis').agg({
    'Blood_Pressure': [bp_range, 'mean'],
    'Age': ['count']
})

print(\"\nCustom aggregation:\")
print(custom_stats)
```
" %}

{% include question.html header="Data Transformation" text="

**Creating new columns**

```python
# Categorize fasting glucose levels
df['Glucose_Category'] = pd.cut(df['Glucose'],
                               bins=[0, 100, 125, 200, float('inf')],
                               labels=['Normal', 'Prediabetes', 'Diabetes', 'Critical'])

# Calculate BMI if height and weight are given
df['BMI'] = (df['Weight_kg'] / (df['Height_m'] ** 2)).round(1)

# Age group classification
df['Age_Group'] = pd.cut(df['Age'],
                         bins=[0, 18, 40, 60, 100],
                         labels=['Child', 'Young Adult', 'Middle-aged', 'Elderly'])

print(\"New columns created:\")
print(df[['Name', 'Glucose', 'Glucose_Category', 'BMI', 'Age_Group']].head())
```
" %}

{% include question.html header="Sorting and Ranking" text="

**Sorting data**

```python
glucose_sorted = df.sort_values('Glucose', ascending=False)
print(\"Top 5 patients with highest glucose:\")
print(glucose_sorted[['Name', 'Glucose', 'Diagnosis']].head())
```

**Multiple column sorting**

```python
multi_sorted = df.sort_values(['Diagnosis', 'Glucose'], ascending=[True, False])
print(\"\nSorted by diagnosis, then glucose (desc):\")
print(multi_sorted[['Name', 'Diagnosis', 'Glucose']].head(10))
```

**Ranking**

```python
df['Glucose_Rank'] = df['Glucose'].rank(ascending=False)
df['Dept_BP_Rank'] = df.groupby('Department')['Blood_Pressure'].rank(ascending=False)

print(\"\nRankings:\")
print(df[['Name', 'Department', 'Blood_Pressure', 'Dept_BP_Rank']].head())
```
" %}

{% capture text %}
**Key Takeaways**

- **Grouping and aggregation** summarize patient data efficiently (e.g., average BP or glucose by diagnosis).
- **Custom aggregation** lets you compute medical-specific metrics like BP range or mean BMI.
- **Data transformation** helps create derived health indicators (e.g., BMI, glucose category, age group).
- **Sorting and ranking** assist in prioritizing patients or identifying extreme cases.
{% endcapture %}
{% include alert.html text=text color=secondary %}
