---
section: Data Analysis with Python
nav_order: 6
title: Data Visualization
topics: matplotlib, seaborn, visualization
---

Visualizations help reveal patterns in clinical data — such as **disease prevalence, lab result distributions, and relationships between vital signs** — and effectively communicate findings to support medical decisions or publications.

{% include question.html header="Basic Plotting with Matplotlib" text="

**Import modules**

```python
import matplotlib.pyplot as plt
```

**Set up plotting style**

```python
plt.style.use('default')
fig_size = (12, 8)
```

**Histogram - Distribution of Glucose Levels**

💡 *Use case:* Quickly visualize how many patients fall into normal, prediabetic, or diabetic glucose ranges.

```python
plt.figure(figsize=fig_size)
plt.hist(df['Glucose'], bins=20, edgecolor='black', alpha=0.7, color='skyblue')
plt.title('Distribution of Fasting Glucose Levels', fontsize=16)
plt.xlabel('Glucose (mg/dL)', fontsize=12)
plt.ylabel('Number of Patients', fontsize=12)
plt.grid(True, alpha=0.3)
plt.show()
```

**Box plot - Glucose by Diagnosis**

💡 *Use case:* Compare glucose variability across different conditions (e.g., Diabetes, Hypertension, Normal).

```python
plt.figure(figsize=fig_size)
diagnoses = df['Diagnosis'].unique()
glucose_by_diag = [df[df['Diagnosis'] == d]['Glucose'] for d in diagnoses]

plt.boxplot(glucose_by_diag, labels=diagnoses)
plt.title('Glucose Distribution by Diagnosis', fontsize=16)
plt.xlabel('Diagnosis', fontsize=12)
plt.ylabel('Glucose (mg/dL)', fontsize=12)
plt.xticks(rotation=45)
plt.grid(True, alpha=0.3)
plt.show()
```
" %}

{% include question.html header="Advanced Plotting with Seaborn" text="

Set up.

```python
# Import module
import seaborn as sns

# Set seaborn style
sns.set_style(\"whitegrid\")
plt.figure(figsize=(15, 10))
```

**Correlation heatmap**

💡 *Use case:* Identify correlations (e.g., between BMI and blood pressure).

```python
plt.subplot(2, 3, 1)
corr_matrix = df[['Age', 'Glucose', 'BMI', 'Blood_Pressure']].corr()
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Matrix of Clinical Variables')
```

**Scatter plot with regression line**

💡 *Use case:* Explore whether glucose tends to rise with age and how it differs by diagnosis.

```python
plt.subplot(2, 3, 2)
sns.scatterplot(data=df, x='Age', y='Glucose', hue='Diagnosis', alpha=0.7)
sns.regplot(data=df, x='Age', y='Glucose', scatter=False, color='red')
plt.title('Age vs Glucose by Diagnosis')
```

**Distribution plot**

💡 *Use case:* Compare glucose distributions across diagnoses using kernel density estimation.

```python
plt.subplot(2, 3, 3)
for diag in df['Diagnosis'].unique():
    diag_data = df[df['Diagnosis'] == diag]['Glucose']
    sns.kdeplot(diag_data, label=diag)
plt.title('Glucose Distribution by Diagnosis')
plt.legend()
```

**Box plot**

💡 *Use case:* Examine BMI variation among diagnostic categories.

```python
plt.subplot(2, 3, 4)
sns.boxplot(data=df, x='Diagnosis', y='BMI')
plt.title('BMI by Diagnosis')
plt.xticks(rotation=45)
```

**Count plot**

💡 *Use case:* Display patient counts per glucose category within each diagnosis.

```python
plt.subplot(2, 3, 5)
sns.countplot(data=df, x='Glucose_Category', hue='Diagnosis')
plt.title('Glucose Categories by Diagnosis')
plt.xticks(rotation=45)
```

**Violin plot**

💡 *Use case:* Visualize the full distribution of blood pressure across age groups.

```python
plt.subplot(2, 3, 6)
sns.violinplot(data=df, x='Age_Group', y='Blood_Pressure')
plt.title('Blood Pressure Distribution by Age Group')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```
" %}

{% include question.html header="Interactive Plotting Concepts" text="

💡 *Use case:* Summarize proportions of diagnoses and visualize clinical indicators interactively.

**Creating summary visualizations**

```python
fig, axes = plt.subplots(2, 2, figsize=(15, 12))
```

**Age distribution**

```python
axes[0, 0].hist(df['Age'], bins=15, edgecolor='black', alpha=0.7, color='lightblue')
axes[0, 0].set_title('Age Distribution of Patients')
axes[0, 0].set_xlabel('Age (years)')
axes[0, 0].set_ylabel('Number of Patients')
```

**Average Glucose by Department**

```python
dept_avg_glucose = df.groupby('Department')['Glucose'].mean().sort_values(ascending=False)
axes[0, 1].bar(dept_avg_glucose.index, dept_avg_glucose.values, color='salmon')
axes[0, 1].set_title('Average Glucose by Department')
axes[0, 1].set_xlabel('Department')
axes[0, 1].set_ylabel('Glucose (mg/dL)')
axes[0, 1].tick_params(axis='x', rotation=45)
```

**Years of Follow-up vs BMI**

```python
axes[1, 0].scatter(df['Years_Followup'], df['BMI'], alpha=0.6, color='green')
axes[1, 0].set_title('Years of Follow-up vs BMI')
axes[1, 0].set_xlabel('Years of Follow-up')
axes[1, 0].set_ylabel('BMI')
```

**Diagnosis Composition (Pie Chart)**

```python
diag_counts = df['Diagnosis'].value_counts()
axes[1, 1].pie(diag_counts.values, labels=diag_counts.index, autopct='%1.1f%%', startangle=90)
axes[1, 1].set_title('Diagnosis Composition of Patients')
plt.tight_layout()
plt.show()
```
" %}

{% capture text %}
**Key Takeaways**

- **Matplotlib** is great for quick and customizable visualizations (histograms, box plots).
- **Seaborn** adds elegance and statistical strength with plots like KDE, violin, and regression plots.
- Visualizations are crucial for **pattern recognition**, **data quality assessment**, and **research presentation**.
- Use them to **compare distributions**, **examine relationships**, and **summarize populations in any data**.
{% endcapture %}
{% include alert.html text=text color=secondary %}
