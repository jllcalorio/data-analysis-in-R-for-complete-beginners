---
section_id: Data Analysis with Python
nav_order: 4
title: Data Analysis with Python
topics: introduction, data analysis, statistics, modules
---

## Welcome to the exciting world of data analysis!

This section will help you move beyond basic Python programming and show you how to turn **health and clinical data** into meaningful insights that can inform **patient care, research, and medical education**.

You’ll learn to use powerful Python libraries such as:

- **pandas** — for cleaning and analyzing patient datasets
- **matplotlib** and **seaborn** — for creating clear, evidence-based visualizations
- **scipy** — for performing statistical tests and clinical comparisons

By the end of this section, you’ll be able to:

- **Load and explore datasets** from sources such as hospital records or surveys
- **Clean and transform** messy data (e.g., missing values in lab tests)
- **Visualize patterns** such as blood pressure trends or lab result distributions
- **Perform basic statistical analyses** to support clinical and research conclusions

## Introduction to Data Analysis Libraries

{% include question.html header="Essential libraries" text="

Before diving into analysis, let’s explore the core Python libraries that make data analysis possible — and how they apply to the medical field.

```python
import pandas as pd              # Data manipulation and analysis
import numpy as np               # Numerical computing
import matplotlib.pyplot as plt  # Basic plotting
import seaborn as sns            # Statistical data visualization
from scipy import stats          # Statistical functions
```
" %}

{% include question.html header="1. pandas — For Data Manipulation" text="
**What it does:** Handles tabular data (like Excel sheets or patient records).

You can filter, summarize, and transform data easily.

```python
import pandas as pd

# Example patient dataset
data = {'Name': ['Ana', 'Luis', 'Maria'],
        'Age': [34, 45, 29],
        'Blood_Pressure': [120, 135, 110]}
df = pd.DataFrame(data)

# View average blood pressure
print(\"Average BP:\", df['Blood_Pressure'].mean())
```

💡*Use case:* Compute the average blood pressure of patients in a study.
" %}

{% include question.html header="2. numpy — For Numerical Calculations" text="
**What it does:** Performs fast mathematical operations on arrays and matrices.

```python
import numpy as np

# Systolic blood pressure readings
bp = np.array([120, 130, 110, 125, 140])

# Compute mean and standard deviation
print(\"Mean BP:\", np.mean(bp))
print(\"SD BP:\", np.std(bp))
```

💡*Use case:* Analyze variability in blood pressure readings from a clinical trial.
" %}

{% include question.html header="3. matplotlib — For Basic Visualization" text="
**What it does:** Creates simple plots and charts.

```python
import matplotlib.pyplot as plt

ages = [23, 45, 34, 50, 29]
plt.hist(ages, bins=5)
plt.title(\"Age Distribution of Study Participants\")
plt.xlabel(\"Age\")
plt.ylabel(\"Count\")
plt.show()
```

💡 *Use case:* Visualize the age distribution of your study participants.
" %}

{% include question.html header="4. seaborn — For Statistical Data Visualization" text="
**What it does:** Makes elegant and easy statistical plots.

```python
import seaborn as sns
import pandas as pd

df = pd.DataFrame({
    'Gender': ['Male', 'Female', 'Female', 'Male'],
    'Cholesterol': [190, 170, 210, 200]
})

sns.boxplot(x='Gender', y='Cholesterol', data=df)
plt.title(\"Cholesterol Levels by Gender\")
plt.show()
```

💡 *Use case:* Compare cholesterol levels across genders or groups.
" %}

{% include question.html header="5. scipy — For Statistical Analysis" text="
**What it does:** Performs statistical tests, correlations, and probability functions.

```python
from scipy import stats

# Two groups of fasting blood sugar values
group_A = [95, 100, 110, 120, 130]
group_B = [90, 92, 88, 85, 93]

t_stat, p_value = stats.ttest_ind(group_A, group_B)
print(\"t-statistic:\", t_stat)
print(\"p-value:\", p_value)
```

💡 *Use case:* Compare two treatment groups’ fasting blood sugar levels.
" %}

{% capture text %}
**In short**

Python offers powerful tools for **handling, visualizing, and analyzing data**.

- **pandas** is your best friend for managing patient records or clinical datasets.
- **numpy** enables fast, vectorized calculations on medical measurements.
- **matplotlib** and **seaborn** help you visualize trends clearly for research or presentations.
- **scipy** provides statistical tools to support evidence-based conclusions.

Together, these libraries form the foundation of data analytics in Python.
{% endcapture %}
{% include alert.html text=text color=secondary %}
