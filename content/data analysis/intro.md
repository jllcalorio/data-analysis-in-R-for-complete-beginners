---
section_id: Data Analysis with R
nav_order: 1
title: Data Analysis with R
topics: introduction, data analysis, statistics, modules
---

# **Welcome to the exciting world of data analysis!**

This section will help you move beyond basic R programming and show you how to turn health and clinical data into meaningful insights that can inform patient care, research, and medical education.

You'll learn to use powerful R packages such as:

- `dplyr` — for cleaning and analyzing patient datasets
- `ggplot2` — for creating clear, evidence-based visualizations
- `stats` (built-in) — for performing statistical tests and clinical comparisons

By the end of this section, you'll be able to:

- **Load and explore datasets** from sources such as hospital records or surveys
- **Clean and transform** messy data (e.g., missing values in lab tests)
- **Visualize patterns** such as blood pressure trends or lab result distributions
- **Perform basic statistical analyses** to support clinical and research conclusions

# **Introduction to Data Analysis Packages**

{% include question.html header="Essential packages" text="

Before diving into analysis, let's explore the core R packages that make data analysis possible — and how they apply to the medical field.

```r
library(dplyr)     # Data manipulation and analysis
library(tidyr)     # Data reshaping
library(ggplot2)   # Data visualization
library(readr)     # Fast CSV reading
```

These packages are all part of the tidyverse — a coherent collection of R packages designed for data science. You can install them all at once:

```r
install.packages(\"tidyverse\")
library(tidyverse)
```
" %}

{% include question.html header="1. dplyr — For Data Manipulation" text="
What it does: Handles tabular data (like Excel sheets or patient records) using intuitive, readable verbs.

```r
library(dplyr)

# Example patient dataset
data <- data.frame(
  Name           = c(\"Ana\", \"Luis\", \"Maria\"),
  Age            = c(34, 45, 29),
  Blood_Pressure = c(120, 135, 110)
)

# View average blood pressure
mean(data$Blood_Pressure)
```
💡*Use case:* Compute the average blood pressure of patients in a study.
" %}

{% include question.html header="2. Base R — For Numerical Calculations" text="
What it does: Performs fast mathematical operations on vectors and matrices — no extra package needed.

```r
# Systolic blood pressure readings
bp <- c(120, 130, 110, 125, 140)

# Compute mean and standard deviation
cat(\"Mean BP:\", mean(bp), \"\n\")
cat(\"SD BP:\",   sd(bp),   \"\n\")
```
💡*Use case:* Analyze variability in blood pressure readings from a clinical trial.
" %}

{% include question.html header="3. ggplot2 — For Visualization" text="
What it does: Creates elegant, layered plots and charts.

```r
library(ggplot2)

ages <- c(23, 45, 34, 50, 29)
df_ages <- data.frame(Age = ages)

ggplot(df_ages, aes(x = Age)) +
  geom_histogram(bins = 5, fill = \"steelblue\", color = \"white\") +
  labs(
    title = \"Age Distribution of Study Participants\",
    x     = \"Age\",
    y     = \"Count\"
  ) +
  theme_bw()
```
💡 *Use case:* Visualize the age distribution of your study participants.
" %}

{% include question.html header="4. ggplot2 — For Statistical Data Visualization" text="
What it does: Makes elegant statistical plots with very little code.

```r
library(ggplot2)

df <- data.frame(
  Gender      = c(\"Male\", \"Female\", \"Female\", \"Male\"),
  Cholesterol = c(190, 170, 210, 200)
)

ggplot(df, aes(x = Gender, y = Cholesterol, fill = Gender)) +
  geom_boxplot() +
  labs(title = \"Cholesterol Levels by Gender\") +
  theme_bw()
```
💡 *Use case:* Compare cholesterol levels across genders or groups.
" %}

{% include question.html header="5. stats — For Statistical Analysis" text="
What it does: Performs statistical tests, correlations, and probability functions. It is built into R — no installation needed.

```r
# Two groups of fasting blood sugar values
group_A <- c(95, 100, 110, 120, 130)
group_B <- c(90,  92,  88,  85,  93)

result  <- t.test(group_A, group_B)
cat(\"t-statistic:\", result$statistic, \"\n\")
cat(\"p-value:\",     result$p.value,   \"\n\")
```
💡 *Use case:* Compare two treatment groups' fasting blood sugar levels.
" %}

{% capture text %}
**In short**

R offers powerful tools for **handling, visualizing, and analyzing data**.

- `dplyr` is your best friend for managing patient records or clinical datasets.
- **Base R** enables fast, vectorized calculations on medical measurements.
- `ggplot2` helps you visualize trends clearly for research or presentations.
- `stats` (built-in) provides statistical tools to support evidence-based conclusions.


Together, these packages form the foundation of data analytics in R.
{% endcapture %}
{% include alert.html text=text color=secondary %}