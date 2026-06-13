---
section: Data Analysis with Python
nav_order: 8
title: Exercises with Solutions
topics: exercises
---

{% include question.html header="Exercise 1: Data Visualization" text="

**Goal:** Visualize the relationship between age and salary using a scatter plot.

**Instructions:**

1. Use matplotlib or seaborn.
2. Add axis labels and a title.

**Question:**

**What trend** do you observe between age and salary across departments?

" solution="

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Scatter plot of Age vs Salary
plt.figure(figsize=(8, 6))
sns.scatterplot(data=df, x='age', y='salary', hue='department', alpha=0.7)
plt.title('Age vs Salary by Department')
plt.xlabel('Age')
plt.ylabel('Salary ($)')
plt.show()
```
" %}

{% include question.html header="Exercise 2: Independent t-test" text="

**Goal:** Compare if the **average salary** of ```IT``` and ```Finance``` departments are significantly different.

**Instructions:**

1. Extract salary data for both departments.
2. Use ```scipy.stats.ttest_ind()```.
3. Print the t-statistic and p-value.

**Question:**

Is there a statistically significant difference at **α = 0.05**?

" solution="

```python
from scipy import stats

it_salary = df[df['department'] == 'IT']['salary']
finance_salary = df[df['department'] == 'Finance']['salary']

t_stat, p_val = stats.ttest_ind(it_salary, finance_salary)
print(f\"T-statistic: {t_stat:.3f}, P-value: {p_val:.4f}\")
```
" %}

{% include question.html header="Exercise 3: Logistic Regression" text="

**Goal:** Predict whether an employee has a **high salary (above median)** using ```age``` and ```years_employed```.

**Instructions:**

1. Create a binary column **high_salary** (1 = above median, 0 = below).
2. Split the data into training/testing sets.
3. Fit a logistic regression model and check accuracy.

**Question:**

**How well does the model predict** high-salary employees based on age and years employed?

" solution="

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# Create target variable
median_salary = df['salary'].median()
df['high_salary'] = (df['salary'] > median_salary).astype(int)

# Prepare features and labels
X = df[['age', 'years_employed']]
y = df['high_salary']

# Train/test split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Train model
model = LogisticRegression()
model.fit(X_train, y_train)

# Predict and evaluate
y_pred = model.predict(X_test)
print(f\"Model accuracy: {accuracy_score(y_test, y_pred):.2f}\")
```
" %}
