---
section: Data Analysis with R
nav_order: 7
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

```r
  [1] \"Patient_1\"   \"Patient_2\"   \"Patient_3\"   \"Patient_4\"   \"Patient_5\"   \"Patient_6\"   \"Patient_7\"   \"Patient_8\"   \"Patient_9\"   \"Patient_10\"  \"Patient_11\"  \"Patient_12\"  \"Patient_13\"  \"Patient_14\" 
 [15] \"Patient_15\"  \"Patient_16\"  \"Patient_17\"  \"Patient_18\"  \"Patient_19\"  \"Patient_20\"  \"Patient_21\"  \"Patient_22\"  \"Patient_23\"  \"Patient_24\"  \"Patient_25\"  \"Patient_26\"  \"Patient_27\"  \"Patient_28\" 
 [29] \"Patient_29\"  \"Patient_30\"  \"Patient_31\"  \"Patient_32\"  \"Patient_33\"  \"Patient_34\"  \"Patient_35\"  \"Patient_36\"  \"Patient_37\"  \"Patient_38\"  \"Patient_39\"  \"Patient_40\"  \"Patient_41\"  \"Patient_42\" 
 [43] \"Patient_43\"  \"Patient_44\"  \"Patient_45\"  \"Patient_46\"  \"Patient_47\"  \"Patient_48\"  \"Patient_49\"  \"Patient_50\"  \"Patient_51\"  \"Patient_52\"  \"Patient_53\"  \"Patient_54\"  \"Patient_55\"  \"Patient_56\" 
 [57] \"Patient_57\"  \"Patient_58\"  \"Patient_59\"  \"Patient_60\"  \"Patient_61\"  \"Patient_62\"  \"Patient_63\"  \"Patient_64\"  \"Patient_65\"  \"Patient_66\"  \"Patient_67\"  \"Patient_68\"  \"Patient_69\"  \"Patient_70\" 
 [71] \"Patient_71\"  \"Patient_72\"  \"Patient_73\"  \"Patient_74\"  \"Patient_75\"  \"Patient_76\"  \"Patient_77\"  \"Patient_78\"  \"Patient_79\"  \"Patient_80\"  \"Patient_81\"  \"Patient_82\"  \"Patient_83\"  \"Patient_84\" 
 [85] \"Patient_85\"  \"Patient_86\"  \"Patient_87\"  \"Patient_88\"  \"Patient_89\"  \"Patient_90\"  \"Patient_91\"  \"Patient_92\"  \"Patient_93\"  \"Patient_94\"  \"Patient_95\"  \"Patient_96\"  \"Patient_97\"  \"Patient_98\" 
 [99] \"Patient_99\"  \"Patient_100\"
```

**Multiple column selection**

💡 *Use case:* Extracting basic demographic and diagnosis data for a summary table.

```r
basic_info <- df |> select(Name, Age, Diagnosis)
print(basic_info)
```

Output:

```r
# A tibble: 100 × 3
   Name         Age Diagnosis   
   <chr>      <dbl> <chr>       
 1 Patient_1     66 Diabetes    
 2 Patient_2     54 Hypertension
 3 Patient_3     18 Diabetes    
 4 Patient_4     42 Hypertension
 5 Patient_5     27 Healthy     
 6 Patient_6     53 Diabetes    
 7 Patient_7     35 Diabetes    
 8 Patient_8     75 Healthy     
 9 Patient_9     66 Hypertension
10 Patient_10    64 Hypertension
# ℹ 90 more rows
# ℹ Use `print(n = ...)` to see more rows
```

**Column selection by type**

💡 *Use case:* Identifying all numeric variables (e.g., blood pressure, glucose) for statistical analysis.

```r
numeric_columns <- df |> select(where(is.numeric))
cat(\"Numeric columns:\", paste(names(numeric_columns), collapse = \", \"), \"\n\")
print(numeric_columns)
```
" %}

Output:

```r
# A tibble: 100 × 4
   Patient_ID   Age Blood_Pressure Glucose
        <dbl> <dbl>          <dbl>   <dbl>
 1          1    66            153     120
 2          2    54            130      79
 3          3    18            142     190
 4          4    42            151     158
 5          5    27            180     106
 6          6    53            158      96
 7          7    35            126     115
 8          8    75            129     100
 9          9    66            151     160
10         10    64            174     169
# ℹ 90 more rows
# ℹ Use `print(n = ...)` to see more rows
```

{% include question.html header="Selecting Rows" text="

**Row selection by position**

💡 *Use case:* Quickly view the first few patient records.

```r
first_patient       <- df[1, ]         # First row
first_five_patients <- df[1:5, ]       # First 5 rows

print(first_patient)
print(first_five_patients)
```

Results:

```r
# A tibble: 1 × 7
  Patient_ID Name        Age Diagnosis Blood_Pressure Glucose Admission_Date
       <dbl> <chr>     <dbl> <chr>              <dbl>   <dbl> <date>        
1          1 Patient_1    66 Diabetes             153     120 2024-01-01    
```

```r
# A tibble: 5 × 7
  Patient_ID Name        Age Diagnosis    Blood_Pressure Glucose Admission_Date
       <dbl> <chr>     <dbl> <chr>                 <dbl>   <dbl> <date>        
1          1 Patient_1    66 Diabetes                153     120 2024-01-01    
2          2 Patient_2    54 Hypertension            130      79 2024-01-08    
3          3 Patient_3    18 Diabetes                142     190 2024-01-15    
4          4 Patient_4    42 Hypertension            151     158 2024-01-22    
5          5 Patient_5    27 Healthy                 180     106 2024-01-29 
```

**Row selection by condition**

💡 *Use case:* Filtering patients with hyperglycemia or a specific medical condition.

```r
high_glucose          <- df |> filter(Glucose > 150)
hypertensive_patients <- df |> filter(Diagnosis == \"Hypertension\")

print(high_glucose)
print(hypertensive_patients)

cat(\"High glucose patients:\",    nrow(high_glucose),          \"\n\") # High glucose patients: 43
cat(\"Hypertensive patients:\",    nrow(hypertensive_patients), \"\n\") # Hypertensive patients: 41
```

High-glucose patients:

```r
# A tibble: 43 × 7
   Patient_ID Name         Age Diagnosis    Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>                 <dbl>   <dbl> <date>        
 1          3 Patient_3     18 Diabetes                142     190 2024-01-15    
 2          4 Patient_4     42 Hypertension            151     158 2024-01-22    
 3          9 Patient_9     66 Hypertension            151     160 2024-02-26    
 4         10 Patient_10    64 Hypertension            174     169 2024-03-04    
 5         11 Patient_11    41 Healthy                 180     189 2024-03-11    
 6         14 Patient_14    42 Hypertension            161     192 2024-04-01    
 7         15 Patient_15    54 Healthy                 112     161 2024-04-08    
 8         17 Patient_17    37 Diabetes                148     162 2024-04-22    
 9         20 Patient_20    64 Diabetes                116     165 2024-05-13    
10         21 Patient_21    20 Diabetes                132     171 2024-05-20    
# ℹ 33 more rows
# ℹ Use `print(n = ...)` to see more rows
```

Hypertensive patients:

```r
# A tibble: 41 × 7
   Patient_ID Name         Age Diagnosis    Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>                 <dbl>   <dbl> <date>        
 1          2 Patient_2     54 Hypertension            130      79 2024-01-08    
 2          4 Patient_4     42 Hypertension            151     158 2024-01-22    
 3          9 Patient_9     66 Hypertension            151     160 2024-02-26    
 4         10 Patient_10    64 Hypertension            174     169 2024-03-04    
 5         14 Patient_14    42 Hypertension            161     192 2024-04-01    
 6         16 Patient_16    63 Hypertension            162     102 2024-04-15    
 7         22 Patient_22    58 Hypertension            127     177 2024-05-27    
 8         25 Patient_25    53 Hypertension            107      99 2024-06-17    
 9         28 Patient_28    62 Hypertension            112      97 2024-07-08    
10         31 Patient_31    51 Hypertension            129      78 2024-07-29    
# ℹ 31 more rows
# ℹ Use `print(n = ...)` to see more rows
```

**Multiple conditions**

💡 *Use case:* Identify high-risk patient groups for focused analysis.

```r
elderly_diabetics <- df |> filter(Age > 60, Diagnosis == \"Diabetes\")
young_healthy     <- df |> filter(Age < 30, Diagnosis == \"Healthy\")

print(elderly_diabetics)
print(young_healthy)

cat(\"Elderly diabetics:\",         nrow(elderly_diabetics), \"\n\") # Elderly diabetics: 8
cat(\"Young healthy individuals:\", nrow(young_healthy),   \"\n\")   # Young healthy individuals: 9
```

Elderly diabetics:

```r
# A tibble: 8 × 7
  Patient_ID Name         Age Diagnosis Blood_Pressure Glucose Admission_Date
       <dbl> <chr>      <dbl> <chr>              <dbl>   <dbl> <date>        
1          1 Patient_1     66 Diabetes             153     120 2024-01-01    
2         19 Patient_19    67 Diabetes             100     114 2024-05-06    
3         20 Patient_20    64 Diabetes             116     165 2024-05-13    
4         43 Patient_43    75 Diabetes             102      86 2024-10-21    
5         54 Patient_54    73 Diabetes             153     185 2025-01-06    
6         55 Patient_55    67 Diabetes             154     177 2025-01-13    
7         73 Patient_73    75 Diabetes             119     128 2025-05-19    
8         98 Patient_98    71 Diabetes             106      79 2025-11-10
```

Early diabetics:

```r
# A tibble: 9 × 7
  Patient_ID Name         Age Diagnosis Blood_Pressure Glucose Admission_Date
       <dbl> <chr>      <dbl> <chr>              <dbl>   <dbl> <date>        
1          5 Patient_5     27 Healthy              180     106 2024-01-29    
2         34 Patient_34    20 Healthy              136     151 2024-08-19    
3         44 Patient_44    25 Healthy              152     151 2024-10-28    
4         51 Patient_51    22 Healthy              121     159 2024-12-16    
5         52 Patient_52    21 Healthy              125     130 2024-12-23    
6         65 Patient_65    19 Healthy              113     116 2025-03-24    
7         67 Patient_67    20 Healthy              110      91 2025-04-07    
8         70 Patient_70    19 Healthy              154     136 2025-04-28    
9         85 Patient_85    29 Healthy              110     179 2025-08-11
```
" %}

{% include question.html header="Advanced Querying" text="

**Using `filter()` with complex conditions**

💡 *Use case:* Query diabetic patients with high blood pressure.

```r
high_bp_diabetics  <- df |> filter(Diagnosis == \"Diabetes\", Blood_Pressure > 140)
recent_admissions  <- df |> filter(Admission_Date > as.Date(\"2024-06-01\"))

print(high_bp_diabetics)
print(recent_admissions)

cat(\"High BP diabetics:\",  nrow(high_bp_diabetics),  \"\n\")  # High BP diabetics: 18
cat(\"Recent admissions:\",  nrow(recent_admissions),  \"\n\")  # Recent admissions: 78
```

High BP diabetics:

```r
# A tibble: 18 × 7
   Patient_ID Name         Age Diagnosis Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>              <dbl>   <dbl> <date>        
 1          1 Patient_1     66 Diabetes             153     120 2024-01-01    
 2          3 Patient_3     18 Diabetes             142     190 2024-01-15    
 3          6 Patient_6     53 Diabetes             158      96 2024-02-05    
 4         12 Patient_12    24 Diabetes             172     122 2024-03-18    
 5         17 Patient_17    37 Diabetes             148     162 2024-04-22    
 6         18 Patient_18    43 Diabetes             160     105 2024-04-29    
 7         26 Patient_26    54 Diabetes             179     123 2024-06-24    
 8         30 Patient_30    37 Diabetes             164     180 2024-07-22    
 9         32 Patient_32    45 Diabetes             150     123 2024-08-05    
10         33 Patient_33    57 Diabetes             159     184 2024-08-12    
11         41 Patient_41    32 Diabetes             172      89 2024-10-07    
12         46 Patient_46    21 Diabetes             178     163 2024-11-11    
13         54 Patient_54    73 Diabetes             153     185 2025-01-06    
14         55 Patient_55    67 Diabetes             154     177 2025-01-13    
15         57 Patient_57    41 Diabetes             157     158 2025-01-27    
16         74 Patient_74    27 Diabetes             178     138 2025-05-26    
17         89 Patient_89    52 Diabetes             153     126 2025-09-08    
18         92 Patient_92    54 Diabetes             158     179 2025-09-29
```

Recent admissions:

```r
# A tibble: 78 × 7
   Patient_ID Name         Age Diagnosis    Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>                 <dbl>   <dbl> <date>        
 1         23 Patient_23    42 Healthy                 101      74 2024-06-03    
 2         24 Patient_24    44 Diabetes                130     191 2024-06-10    
 3         25 Patient_25    53 Hypertension            107      99 2024-06-17    
 4         26 Patient_26    54 Diabetes                179     123 2024-06-24    
 5         27 Patient_27    48 Healthy                 102      71 2024-07-01    
 6         28 Patient_28    62 Hypertension            112      97 2024-07-08    
 7         29 Patient_29    22 Diabetes                111     200 2024-07-15    
 8         30 Patient_30    37 Diabetes                164     180 2024-07-22    
 9         31 Patient_31    51 Hypertension            129      78 2024-07-29    
10         32 Patient_32    45 Diabetes                150     123 2024-08-05    
# ℹ 68 more rows
# ℹ Use `print(n = ...)` to see more rows
```

**Using `%in%` for multiple values**

💡 *Use case:* Selecting patients with comorbidities.

```r
target_conditions <- df |> filter(Diagnosis %in% c(\"Diabetes\", \"Hypertension\"))
cat(\"Patients with Diabetes or Hypertension:\", nrow(target_conditions), \"\n\")

# Output
# Patients with Diabetes or Hypertension: 77 
print(target_conditions)
```

```r
# A tibble: 77 × 7
   Patient_ID Name         Age Diagnosis    Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>                 <dbl>   <dbl> <date>        
 1          1 Patient_1     66 Diabetes                153     120 2024-01-01    
 2          2 Patient_2     54 Hypertension            130      79 2024-01-08    
 3          3 Patient_3     18 Diabetes                142     190 2024-01-15    
 4          4 Patient_4     42 Hypertension            151     158 2024-01-22    
 5          6 Patient_6     53 Diabetes                158      96 2024-02-05    
 6          7 Patient_7     35 Diabetes                126     115 2024-02-12    
 7          9 Patient_9     66 Hypertension            151     160 2024-02-26    
 8         10 Patient_10    64 Hypertension            174     169 2024-03-04    
 9         12 Patient_12    24 Diabetes                172     122 2024-03-18    
10         13 Patient_13    53 Diabetes                116      93 2024-03-25    
# ℹ 67 more rows
# ℹ Use `print(n = ...)` to see more rows
```

**String operations**

💡 *Use case:* Useful for data cleaning or searching names.

```r
patients_with_a <- df |> filter(grepl(\"a\", Name, ignore.case = TRUE))
cat(\"Patients with 'a' in name:\", nrow(patients_with_a), \"\n\")       # Patients with 'a' in name: 100

print(patients_with_a)
```

```r
# A tibble: 100 × 7
   Patient_ID Name         Age Diagnosis    Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>                 <dbl>   <dbl> <date>        
 1          1 Patient_1     66 Diabetes                153     120 2024-01-01    
 2          2 Patient_2     54 Hypertension            130      79 2024-01-08    
 3          3 Patient_3     18 Diabetes                142     190 2024-01-15    
 4          4 Patient_4     42 Hypertension            151     158 2024-01-22    
 5          5 Patient_5     27 Healthy                 180     106 2024-01-29    
 6          6 Patient_6     53 Diabetes                158      96 2024-02-05    
 7          7 Patient_7     35 Diabetes                126     115 2024-02-12    
 8          8 Patient_8     75 Healthy                 129     100 2024-02-19    
 9          9 Patient_9     66 Hypertension            151     160 2024-02-26    
10         10 Patient_10    64 Hypertension            174     169 2024-03-04    
# ℹ 90 more rows
# ℹ Use `print(n = ...)` to see more rows
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