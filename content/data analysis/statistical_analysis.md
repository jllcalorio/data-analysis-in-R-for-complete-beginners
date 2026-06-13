---
section: Data Analysis with Python
nav_order: 7
title: Statistical Analysis
topics: statistics, t-test, ANOVA, chi-square, correlation, regression
---

**Statistical analysis** is at the heart of **medical research and clinical decision-making**. It allows us to determine whether observed patterns in patient data are due to chance or represent meaningful differences or associations.

{% include question.html header="Descriptive Statistics" text="

Descriptive statistics **summarize your dataset** and provide the foundation for deeper analysis.

In medicine, these **metrics describe patient demographics, laboratory results, and treatment outcomes** — helping you quickly understand what’s typical or unusual in your data.

Think of them as the **vital signs of your dataset** — providing a snapshot before diagnosing deeper relationships.

🧪 **Common Measures**
- Measures of central tendency:
  - Mean (e.g., average blood pressure)
  - Median (e.g., middle value of patient age)
  - Mode (e.g., most common diagnosis)
- Measures of variability:
  - Range (e.g., youngest to oldest patient)
  - Standard deviation (e.g., how spread out glucose levels are)
- Frequencies and proportions:
  - Counts and percentages (e.g., 60% of patients are female)
- Visual summaries (although this belongs to the 'Data Visualization' part, but still are descriptive in nature):
  - Tables, histograms, pie charts — like those in journal articles or case reports


**To start**, let's import the stuff that we need to use.

```python
from scipy import stats
import numpy as np
```

**Let's define a function to describe clinical data.**

```python
def describe_data(data, column_name):
    \"\"\"Generate comprehensive descriptive statistics.\"\"\"
    print(f\"\n=== Descriptive Statistics for {column_name} ===\")
    print(f\"Count: {len(data)}\")
    print(f\"Mean: {np.mean(data):.2f}\")
    print(f\"Median: {np.median(data):.2f}\")
    print(f\"Mode: {stats.mode(data, keepdims=True)[0][0]:.2f}\")
    print(f\"Standard Deviation: {np.std(data, ddof=1):.2f}\")
    print(f\"Range: {np.max(data) - np.min(data):.2f}\")
    print(f\"IQR: {np.percentile(data, 75) - np.percentile(data, 25):.2f}\")
```

**Example Use**

```python
describe_data(df['Glucose'], 'Fasting Glucose (mg/dL)')
describe_data(df['Age'], 'Patient Age (years)')
```
" %}

## Univariate tests

{% include question.html header="t-tests" text="

**One-sample t-test**

Check if the **average fasting glucose** differs significantly from the normal fasting level of **100 mg/dL**.

```python
population_mean = 100
t_stat, p_value = stats.ttest_1samp(df['Glucose'], population_mean)

print(\"\n=== One-Sample T-Test ===\")
print(f\"Testing if mean glucose differs from {population_mean} mg/dL\")
print(f\"Sample mean: {df['Glucose'].mean():.2f}\")
print(f\"T-statistic: {t_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
```

💡 *Clinical meaning:* A significant p-value (< 0.05) suggests that your patient group’s glucose levels are not within normal limits.

**Two-sample t-test**

Compare **cholesterol levels** between **male** and **female** patients.

```python
male_chol = df[df['Sex'] == 'Male']['Cholesterol']
female_chol = df[df['Sex'] == 'Female']['Cholesterol']

t_stat, p_value = stats.ttest_ind(male_chol, female_chol)

print(\"\n=== Two-Sample T-Test ===\")
print(f\"T-statistic: {t_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
```

💡 *Clinical meaning:* Tests if there’s a significant sex-based difference in cholesterol levels.

**Paired t-test example (if we had before/after data)**

Evaluate if **blood pressure medication** effectively reduces **systolic BP**.

```python
np.random.seed(42)
bp_before = df['Systolic_BP_Before'].sample(30).values
bp_after = df['Systolic_BP_After'].sample(30).values

t_stat, p_value = stats.ttest_rel(bp_before, bp_after)

print(\"\n=== Paired T-Test ===\")
print(f\"Mean before: {np.mean(bp_before):.2f}\")
print(f\"Mean after: {np.mean(bp_after):.2f}\")
print(f\"P-value: {p_value:.4f}\")
```

💡 *Clinical meaning:* Determines whether treatment significantly lowered blood pressure.
" %}

{% include question.html header="ANOVA (Analysis of Variance)" text="

**One-way Analysis of Variance (ANOVA)**

ANOVA is an extension to t-test, where there can be more than 2 groups being compared. In this case, we want to compare the **mean BMI** across **different hospital departments** (e.g., Pediatrics, Internal Medicine, Surgery).

```python
dept_groups = [group['BMI'].values for name, group in df.groupby('Department')]
f_stat, p_value = stats.f_oneway(*dept_groups)

print(\"\n=== One-Way ANOVA ===\")
print(f\"F-statistic: {f_stat:.4f}, P-value: {p_value:.4f}\")
```

💡 *Clinical meaning:* Tests if BMI differs across departments — perhaps due to varying patient populations or conditions.

**Post-hoc analysis** is required to be implemented if ANOVA is significant, i.e., the p-value < 0.05. This threshold is the usual threshold for significant p-values. You can be very strict and go down to 0.01, or maybe less strict by going up to 0.10. However, the latter is not very recommended because studies with these thresholds

- have results that are considered to have **weak evidence** and increases the risk of **Type I errors**—falsely rejecting a true null hypothesis
- are less likely to replicate in future studies
- Journals and reviewers may view such results as tentative or inconclusive, reducing their impact
- can lead to overstated claims or misleading conclusions in public-facing research

```python
if p_value < 0.05:
    print(\"\nPost-hoc pairwise comparisons:\")
    departments = df['Department'].unique()
    for i, dept1 in enumerate(departments):
        for dept2 in departments[i+1:]:
            group1 = df[df['Department'] == dept1]['BMI']
            group2 = df[df['Department'] == dept2]['BMI']
            _, p_val = stats.ttest_ind(group1, group2)
            print(f\"{dept1} vs {dept2}: p = {p_val:.4f} {'*' if p_val < 0.05 else ''}\")
```
" %}

{% include question.html header="Chi-Square Tests" text="

**Chi-square test of independence**

Check if **Diagnosis** is associated with **Smoking Status**.

```python
contingency = pd.crosstab(df['Diagnosis'], df['Smoker'])
chi2, p, dof, exp = stats.chi2_contingency(contingency)

print(\"\n=== Chi-Square Test of Independence ===\")
print(contingency)
print(f\"P-value: {p:.4f}\")
```

💡 *Clinical meaning:* A significant association suggests smoking status may relate to diagnosis (e.g., higher COPD rates among smokers).

**Chi-square goodness of fit test**

Test if **blood type distribution** follows expected population proportions.

```python
observed = df['Blood_Type'].value_counts().sort_index()
expected_proportions = [0.44, 0.42, 0.10, 0.04]  # Example for O, A, B, AB
expected = np.array(expected_proportions) * len(df)

chi2, p_value = stats.chisquare(observed, expected)
print(\"\n=== Chi-Square Goodness of Fit ===\")
print(f\"P-value: {p_value:.4f}\")
```
" %}

## Correlation and Regression Analysis

**Correlation**

💡 *Clinical meaning:* Identify linear relationships (e.g., BMI positively correlating with fasting glucose).

```python
print(\"\n=== Correlation Analysis ===\")
numeric_cols = ['Age', 'BMI', 'Glucose']
corr_matrix = df[numeric_cols].corr()
print(corr_matrix.round(3))
```
" %}

{% include question.html header="Simple Linear Regression" text="

**Predict Glucose from BMI.**

```python
slope, intercept, r, p, std_err = stats.linregress(df['BMI'], df['Glucose'])
print(\"\n=== Linear Regression ===\")
print(f\"Slope: {slope:.2f}, R²: {r**2:.3f}, P-value: {p:.4f}\")
```

💡 *Clinical meaning:* Each 1-unit increase in BMI predicts an average rise of X mg/dL in glucose.
" %}

{% include question.html header="Logistic Regression" text="

**Predict **presence of hypertension** (Yes/No) using **Age** and **BMI**.**

**Import stuff**

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report, confusion_matrix
```

**Set DataFrame**

```python
df['Hypertensive'] = (df['Systolic_BP'] >= 140).astype(int)

X = df[['Age', 'BMI']].values
y = df['Hypertensive'].values
```

**Split data to training and testing data sets.**

This is a common practice in building a regression model.

```python
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```

**Fit logistic regression model.**

```python
log_reg = LogisticRegression()
log_reg.fit(X_train, y_train)
y_pred = log_reg.predict(X_test)
```
**Print the results.**

```python
print(\"\n=== Logistic Regression: Predicting Hypertension ===\")
print(f\"Accuracy: {log_reg.score(X_test, y_test):.3f}\")
print(\"\nClassification Report:\")
print(classification_report(y_test, y_pred))
print(\"\nConfusion Matrix:\")
print(confusion_matrix(y_test, y_pred))
```
" %}

{% capture text %}
**Key Takeaway**

- Use **descriptive statistics** to summarize patient data.
- Apply **t-tests** and **ANOVA** to detect significant group differences.
- Use **Chi-square tests** for categorical associations.
- **Correlation** and **regression** uncover relationships and prediction patterns.

Together, these tools form the **backbone of clinical research and evidence-based medicine** — helping transform raw data into actionable insights.
{% endcapture %}
{% include alert.html text=text color=secondary %}
