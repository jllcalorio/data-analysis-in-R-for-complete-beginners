---
section: Data Analysis with R
nav_order: 8
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

Result:

```r
Diagnosis statistics:
# A tibble: 3 × 8
  Diagnosis    mean_bp median_bp sd_bp     n mean_age min_age max_age
  <chr>          <dbl>     <dbl> <dbl> <int>    <dbl>   <dbl>   <dbl>
1 Diabetes        139.      138.  23.7    36     45.6      18      75
2 Healthy         134.      127   25.8    23     42.3      19      75
3 Hypertension    145.      146   19.8    41     50.6      22      75
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

Result:

```r
Custom aggregation:
# A tibble: 3 × 4
  Diagnosis    bp_range mean_bp n_patients
  <chr>           <dbl>   <dbl>      <int>
1 Diabetes           79    139.         36
2 Healthy            79    134.         23
3 Hypertension       72    145.         41
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

Result:

```r
New columns created:
# A tibble: 6 × 5
  Name      Glucose Glucose_Category   Age Age_Group  
  <chr>       <dbl> <chr>            <dbl> <chr>      
1 Patient_1     120 Prediabetes         66 Elderly    
2 Patient_2      79 Normal              54 Middle-aged
3 Patient_3     190 Diabetes            18 Child      
4 Patient_4     158 Diabetes            42 Middle-aged
5 Patient_5     106 Prediabetes         27 Young Adult
6 Patient_6      96 Normal              53 Middle-aged
```
" %}

{% include question.html header="Sorting and Ranking" text="

**Sorting data**

```r
glucose_sorted <- df |> arrange(desc(Glucose))
cat(\"Top 5 patients with highest glucose:\n\")
print(head(glucose_sorted |> select(Name, Glucose, Diagnosis)))
```

```r
Top 5 patients with highest glucose:
# A tibble: 6 × 3
  Name       Glucose Diagnosis   
  <chr>        <dbl> <chr>       
1 Patient_29     200 Diabetes    
2 Patient_39     200 Diabetes    
3 Patient_72     194 Hypertension
4 Patient_14     192 Hypertension
5 Patient_24     191 Diabetes    
6 Patient_3      190 Diabetes
```

**Multiple column sorting**

```r
multi_sorted <- df |> arrange(Diagnosis, desc(Glucose))
cat(\"\nSorted by diagnosis, then glucose (desc):\n\")
print(head(multi_sorted |> select(Name, Diagnosis, Glucose), 10))
```

```r
Sorted by diagnosis, then glucose (desc):
# A tibble: 10 × 3
   Name       Diagnosis Glucose
   <chr>      <chr>       <dbl>
 1 Patient_29 Diabetes      200
 2 Patient_39 Diabetes      200
 3 Patient_24 Diabetes      191
 4 Patient_3  Diabetes      190
 5 Patient_54 Diabetes      185
 6 Patient_33 Diabetes      184
 7 Patient_30 Diabetes      180
 8 Patient_92 Diabetes      179
 9 Patient_55 Diabetes      177
10 Patient_87 Diabetes      176
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

```r
Rankings:
# A tibble: 6 × 4
  Name      Diagnosis    Blood_Pressure Dept_BP_Rank
  <chr>     <chr>                 <dbl>        <dbl>
1 Patient_1 Diabetes                153         14  
2 Patient_2 Hypertension            130         31  
3 Patient_3 Diabetes                142         18  
4 Patient_4 Hypertension            151         17.5
5 Patient_5 Healthy                 180          1.5
6 Patient_6 Diabetes                158          9.5
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