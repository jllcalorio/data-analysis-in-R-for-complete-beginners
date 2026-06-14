---
section_id: Data Analysis with R
nav_order: 5
title: Data Filtering and Transformation
topics: filtering, transformation, dplyr, mutate
---

**Transforming data** helps uncover patterns in **patient records, clinical measurements, and laboratory results**.

In medical data analysis, we often group data (e.g., by hospital department or diagnosis), compute summary statistics (e.g., average glucose by group), and create derived variables such as BMI or risk categories.

{% include question.html header="Grouping and Aggregation" text="

**Basic `group_by()` operations**

```r
library(dplyr)

dept_stats <- df |>
  group_by(Diagnosis) |>
  summarise(
    mean_bp   = round(mean(Blood_Pressure),   2),
    median_bp = round(median(Blood_Pressure), 2),
    sd_bp     = round(sd(Blood_Pressure),     2),
    n         = n(),
    mean_age  = round(mean(Age),              2),
    min_age   = min(Age),
    max_age   = max(Age)
  )

cat(\"Diagnosis statistics:\n\")
print(dept_stats)
```

**Custom aggregation functions**

```r
bp_range <- function(x) max(x) - min(x)

custom_stats <- df |>
  group_by(Diagnosis) |>
  summarise(
    bp_range   = bp_range(Blood_Pressure),
    mean_bp    = mean(Blood_Pressure),
    n_patients = n()
  )

cat(\"\nCustom aggregation:\n\")
print(custom_stats)
```
" %}

{% include question.html header="Data Transformation" text="

**Creating new columns with `mutate()`**

```r
df <- df |>
  mutate(
    # Categorize fasting glucose levels
    Glucose_Category = case_when(
      Glucose <= 100              ~ \"Normal\",
      Glucose <= 125              ~ \"Prediabetes\",
      Glucose <= 200              ~ \"Diabetes\",
      TRUE                        ~ \"Critical\"
    ),
    # Age group classification
    Age_Group = case_when(
      Age <= 18  ~ \"Child\",
      Age <= 40  ~ \"Young Adult\",
      Age <= 60  ~ \"Middle-aged\",
      TRUE       ~ \"Elderly\"
    )
  )

cat(\"New columns created:\n\")
print(head(df |> select(Name, Glucose, Glucose_Category, Age, Age_Group)))
```
" %}

{% include question.html header="Sorting and Ranking" text="

**Sorting data**

```r
glucose_sorted <- df |> arrange(desc(Glucose))
cat(\"Top 5 patients with highest glucose:\n\")
print(head(glucose_sorted |> select(Name, Glucose, Diagnosis)))
```

**Multiple column sorting**

```r
multi_sorted <- df |> arrange(Diagnosis, desc(Glucose))
cat(\"\nSorted by diagnosis, then glucose (desc):\n\")
print(head(multi_sorted |> select(Name, Diagnosis, Glucose), 10))
```

**Ranking**

```r
df <- df |>
  mutate(
    Glucose_Rank = rank(-Glucose),
    Dept_BP_Rank = ave(Blood_Pressure, Diagnosis, FUN = function(x) rank(-x))
  )

cat(\"\nRankings:\n\")
print(head(df |> select(Name, Diagnosis, Blood_Pressure, Dept_BP_Rank)))
```
" %}

{% capture text %}
**Key Takeaways**

- **Grouping and aggregation** summarize patient data efficiently (e.g., average BP or glucose by diagnosis).
- **Custom aggregation** lets you compute medical-specific metrics like BP range or mean BMI.
- **Data transformation** with `mutate()` helps create derived health indicators (e.g., glucose category, age group).
- **Sorting and ranking** assist in prioritizing patients or identifying extreme cases.
{% endcapture %}
{% include alert.html text=text color=secondary %}