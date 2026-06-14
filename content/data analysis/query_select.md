---
section_id: Data Analysis with R
nav_order: 4
title: Data Querying and Selection
topics: query, select, filter, dplyr
---

When analyzing clinical or research data, we often need to filter patients, extract specific variables, or identify subgroups (e.g., diabetic patients with high glucose).

This section teaches you how to efficiently query and select relevant medical data using `dplyr`.

{% include question.html header="Selecting Columns" text="

**Single column selection**

💡 *Use case:* Selecting only the patient names for anonymization or reporting.

```r
library(dplyr)

names_col <- df |> select(Name)
cat(\"Names (data frame):\", class(names_col), \"\n\")

# As a vector
names_vec <- df$Name
```

**Multiple column selection**

💡 *Use case:* Extracting basic demographic and diagnosis data for a summary table.

```r
basic_info <- df |> select(Name, Age, Diagnosis)
```

**Column selection by type**

💡 *Use case:* Identifying all numeric variables (e.g., blood pressure, glucose) for statistical analysis.

```r
numeric_columns <- df |> select(where(is.numeric))
cat(\"Numeric columns:\", paste(names(numeric_columns), collapse = \", \"), \"\n\")
```
" %}

{% include question.html header="Selecting Rows" text="

**Row selection by position**

💡 *Use case:* Quickly view the first few patient records.

```r
first_patient      <- df[1, ]          # First row
first_five_patients <- df[1:5, ]       # First 5 rows
```

**Row selection by condition**

💡 *Use case:* Filtering patients with hyperglycemia or a specific medical condition.

```r
high_glucose          <- df |> filter(Glucose > 150)
hypertensive_patients <- df |> filter(Diagnosis == \"Hypertension\")

cat(\"High glucose patients:\",    nrow(high_glucose),          \"\n\")
cat(\"Hypertensive patients:\",    nrow(hypertensive_patients), \"\n\")
```

**Multiple conditions**

💡 *Use case:* Identify high-risk patient groups for focused analysis.

```r
elderly_diabetics <- df |> filter(Age > 60, Diagnosis == \"Diabetes\")
young_healthy     <- df |> filter(Age < 30, Diagnosis == \"Healthy\")

cat(\"Elderly diabetics:\",       nrow(elderly_diabetics), \"\n\")
cat(\"Young healthy individuals:\", nrow(young_healthy),   \"\n\")
```
" %}

{% include question.html header="Advanced Querying" text="

**Using `filter()` with complex conditions**

💡 *Use case:* Query diabetic patients with high blood pressure.

```r
high_bp_diabetics  <- df |> filter(Diagnosis == \"Diabetes\", Blood_Pressure > 140)
recent_admissions  <- df |> filter(Admission_Date > as.Date(\"2024-06-01\"))

cat(\"High BP diabetics:\",  nrow(high_bp_diabetics),  \"\n\")
cat(\"Recent admissions:\",  nrow(recent_admissions),   \"\n\")
```

**Using `%in%` for multiple values**

💡 *Use case:* Selecting patients with comorbidities.

```r
target_conditions <- df |> filter(Diagnosis %in% c(\"Diabetes\", \"Hypertension\"))
cat(\"Patients with Diabetes or Hypertension:\", nrow(target_conditions), \"\n\")
```

**String operations**

💡 *Use case:* Useful for data cleaning or searching names.

```r
patients_with_a <- df |> filter(grepl(\"a\", Name, ignore.case = TRUE))
cat(\"Patients with 'a' in name:\", nrow(patients_with_a), \"\n\")
```
" %}

{% capture text %}
**Key Takeaways**

- You can **select and filter** medical data easily using `dplyr`.
- Use **column and row selection** to extract specific patient subsets.
- **Conditional filtering** allows targeted analysis (e.g., high-risk patients, comorbidities).
- The `|>` pipe operator makes complex filters more readable and natural.
- These skills are essential for **clinical research, public health analytics, and hospital record management**.
{% endcapture %}
{% include alert.html text=text color=secondary %}