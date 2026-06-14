---
section_id: Data Analysis with R
nav_order: 2
title: Introduction to Data Frames
topics: data frame, tibble, structured data
---

Data frames are the cornerstone of medical data analysis in R. They allow you to organize, clean, and analyze structured data — similar to how you might handle patient records or hospital information in Excel or EHR systems.

With data frames, you can easily handle datasets containing patient demographics, lab results, or hospital statistics — making them an essential structure for clinical research, epidemiology, and medical audits.

# Key Data Structures in R

{% include question.html header="Vectors – One-Dimensional Data" text="

A **vector** is like a column in a spreadsheet — it holds values of a single type, such as patients' ages or cholesterol levels.

**Example:** Creating a vector of patients' ages

```r
ages <- c(34, 45, 29, 50, 41)
names(ages) <- c(\"Ana\", \"Luis\", \"Maria\", \"Jose\", \"Carmen\")

print(ages)
cat(\"Data type:\",    class(ages),  \"\n\")
cat(\"Length:\",       length(ages), \"\n\")

# Basic operations
cat(\"Mean age:\",     mean(ages),   \"\n\")
cat(\"Oldest patient:\", names(which.max(ages)), \"\n\")
```
" %}

{% include question.html header="Data Frame – Two-Dimensional Data" text="

A **data frame** is like a full spreadsheet (like Microsoft Excel or Google Sheets) — rows represent patients, and columns represent variables (e.g., age, diagnosis, or lab values).

**Example:** Creating a data frame of patient information

```r
df <- data.frame(
  Patient_ID  = 101:105,
  Name        = c(\"Ana\", \"Luis\", \"Maria\", \"Jose\", \"Carmen\"),
  Age         = c(34, 45, 29, 50, 41),
  Diagnosis   = c(\"Diabetes\", \"Hypertension\", \"Healthy\", \"Diabetes\", \"Hypertension\"),
  Cholesterol = c(210, 190, 170, 250, 230)
)
```

**Inspecting the data frame:**

```r
print(df)
cat(\"Dimensions:\",   nrow(df), \"rows x\", ncol(df), \"columns\n\")
cat(\"Column names:\", paste(names(df), collapse = \", \"), \"\n\")
str(df)    # Compact structure overview
```
" %}

{% include question.html header="Data Frame Inspection Methods" text="

R provides several ways to quickly explore and summarize your dataset.

**First 3 rows:**

```r
head(df, 3)
```

**Last 2 rows:**

```r
tail(df, 2)
```

**Structure and data types:**

```r
str(df)
```

**Quick descriptive statistics:**

```r
summary(df)
```

**Column-specific information:**

```r
table(df$Diagnosis)            # Frequency of each diagnosis
mean(df$Cholesterol)           # Average cholesterol level
```
" %}

{% capture text %}


- **data frames** are essential for managing structured datasets — just like a digital spreadsheet for clinical data.
- A **vector** represents a single column of medical data (e.g., patient age or blood pressure).
- A **data frame** is a full table of patient information (e.g., demographics, diagnoses, lab values).
- You can **inspect, summarize, and analyze** datasets efficiently using base R and dplyr.
- This skill is crucial for **research, quality assurance, and data-driven healthcare decisions**.
{% endcapture %}
{% include alert.html text=text color=secondary %}