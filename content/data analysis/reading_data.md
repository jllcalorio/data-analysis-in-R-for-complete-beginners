---
section: Data Analysis with R
nav_order: 6
title: Reading and Loading Data
topics: read, import, readr, csv
---

In medical research and hospital informatics, data often comes from **electronic health records (EHRs), lab systems, or survey results** — usually in formats like CSV, Excel, or JSON.

This section will teach you how to **load these files into R**, so you can begin analyzing them effectively.

{% include question.html header="Reading CSV Files" text="

CSV (Comma-Separated Values) is one of the most common formats for exporting medical data — from patient logs to laboratory results.

To try the codes below, download the [patients_data.csv file here](https://github.com/jllcalorio/data-analysis-in-R-for-complete-beginners/blob/main/patients_data.csv) and save (or move) it in your current working directory.

```r
library(readr)
library(dplyr)

# Load clinical data
df <- read_csv(\"patients_data.csv\")
print(head(df))
```

**Common Parameters When Reading CSV Files**

```r
df_csv <- read_csv(
  \"patients_data.csv\",
  col_names    = TRUE,             # First row as column names
  na           = c(\"N/A\", \"NULL\"), # Treat these as missing
  col_types    = cols(
    Admission_Date = col_date(format = \"%Y-%m-%d\")
  )
)
```

**Creating and Saving Sample Medical Data**

Let's create a simple medical dataset that simulates patient information:

```r
set.seed(42)
n <- 100

sample_data <- data.frame(
  Patient_ID     = 1:n,
  Name           = paste0(\"Patient_\", 1:n),
  Age            = sample(18:80, n, replace = TRUE),
  Diagnosis      = sample(c(\"Diabetes\", \"Hypertension\", \"Healthy\"), n, replace = TRUE),
  Blood_Pressure = sample(100:180, n, replace = TRUE),
  Glucose        = sample(70:200,  n, replace = TRUE),
  Admission_Date = seq.Date(as.Date(\"2024-01-01\"), by = \"week\", length.out = n)
)

# Save sample data
write_csv(sample_data, \"sample_patients.csv\")
cat(\"Sample patient data created and saved!\n\")
```
" %}

{% include question.html header="Reading Other File Formats" text="

Medical data can also come in Excel, JSON, or even databases.

**Reading Excel files**

```r
library(readxl)
df_excel <- read_excel(\"data.xlsx\", sheet = \"Sheet1\")
```

**Working with Our Sample CSV**

```r
df <- read_csv(\"sample_patients.csv\")
df$Admission_Date <- as.Date(df$Admission_Date)

cat(\"Data loaded successfully!\n\")
print(head(df))
```

Here is our data:

```r
# A tibble: 6 × 7
  Patient_ID Name        Age Diagnosis    Blood_Pressure Glucose Admission_Date
       <dbl> <chr>     <dbl> <chr>                 <dbl>   <dbl> <date>        
1          1 Patient_1    66 Diabetes                153     120 2024-01-01    
2          2 Patient_2    54 Hypertension            130      79 2024-01-08    
3          3 Patient_3    18 Diabetes                142     190 2024-01-15    
4          4 Patient_4    42 Hypertension            151     158 2024-01-22    
5          5 Patient_5    27 Healthy                 180     106 2024-01-29    
6          6 Patient_6    53 Diabetes                158      96 2024-02-05  
```

The `<dbl>`, `<chr>`, and `<date>` just below the character names tells us the data types of the variables we are working with.

- `<dbl>` indicates double, e.g., `class(66)`
- `<chr>` indicates character (string)
- `<date>` indicates double (date)
- `<int>` indicates integer (date), e.g., `class(66L)`

The result is of class `tibble`, which is a modern, optimized reimagining of the traditional data frame (`data.frame`) in R. Here, the data types are determined using `typeof()` instead of `class()` which are synonymous.
" %}

{% include question.html header="Handling Missing Data" text="

Missing data is very common in medical research — for example, when a lab result isn't recorded or a patient skips a follow-up visit.

Let's simulate and handle missing values:

```r
library(dplyr)

df_with_missing                  <- df
df_with_missing$Glucose  [6:11]  <- NA
df_with_missing$Diagnosis[16:21] <- NA

cat(\"Missing data summary:\n\")
print(colSums(is.na(df_with_missing)))
```

The result:

```r
Missing data summary:
    Patient_ID  Name  Age  Diagnosis Blood_Pressure  Glucose Admission_Date 
             0     0    0          6              0        6              0 
```

Here's the *new* data frame with missing values:

```r
print(df_with_missing, n = 30)
# A tibble: 100 × 7
   Patient_ID Name         Age Diagnosis    Blood_Pressure Glucose Admission_Date
        <dbl> <chr>      <dbl> <chr>                 <dbl>   <dbl> <date>        
 1          1 Patient_1     66 Diabetes                153     120 2024-01-01    
 2          2 Patient_2     54 Hypertension            130      79 2024-01-08    
 3          3 Patient_3     18 Diabetes                142     190 2024-01-15    
 4          4 Patient_4     42 Hypertension            151     158 2024-01-22    
 5          5 Patient_5     27 Healthy                 180     106 2024-01-29    
 6          6 Patient_6     53 Diabetes                158      NA 2024-02-05    
 7          7 Patient_7     35 Diabetes                126      NA 2024-02-12    
 8          8 Patient_8     75 Healthy                 129      NA 2024-02-19    
 9          9 Patient_9     66 Hypertension            151      NA 2024-02-26    
10         10 Patient_10    64 Hypertension            174      NA 2024-03-04    
11         11 Patient_11    41 Healthy                 180      NA 2024-03-11    
12         12 Patient_12    24 Diabetes                172     122 2024-03-18    
13         13 Patient_13    53 Diabetes                116      93 2024-03-25    
14         14 Patient_14    42 Hypertension            161     192 2024-04-01    
15         15 Patient_15    54 Healthy                 112     161 2024-04-08    
16         16 Patient_16    63 NA                      162     102 2024-04-15    
17         17 Patient_17    37 NA                      148     162 2024-04-22    
18         18 Patient_18    43 NA                      160     105 2024-04-29    
19         19 Patient_19    67 NA                      100     114 2024-05-06    
20         20 Patient_20    64 NA                      116     165 2024-05-13    
21         21 Patient_21    20 NA                      132     171 2024-05-20    
22         22 Patient_22    58 Hypertension            127     177 2024-05-27    
23         23 Patient_23    42 Healthy                 101      74 2024-06-03    
24         24 Patient_24    44 Diabetes                130     191 2024-06-10    
25         25 Patient_25    53 Hypertension            107      99 2024-06-17    
26         26 Patient_26    54 Diabetes                179     123 2024-06-24    
27         27 Patient_27    48 Healthy                 102      71 2024-07-01    
28         28 Patient_28    62 Hypertension            112      97 2024-07-08    
29         29 Patient_29    22 Diabetes                111     200 2024-07-15    
30         30 Patient_30    37 Diabetes                164     180 2024-07-22    
# ℹ 70 more rows
# ℹ Use `print(n = ...)` to see more rows
```


**Strategies for handling missing data**

**Drop rows with missing values**

```r
df_dropped <- na.omit(df_with_missing)
dim(df_dropeed)                            # 88 7
```

Since we have 12 missing values in the `df_with_missing` data frame, removing them results to a reduced 88-row data frame.

**Fill missing values with median or a default**

```r
median_glucose <- median(df_with_missing$Glucose, na.rm = TRUE)

df_filled <- df_with_missing |>
  mutate(
    Glucose   = ifelse(is.na(Glucose),   median_glucose, Glucose),
    Diagnosis = ifelse(is.na(Diagnosis), \"Unknown\",      Diagnosis)
  )
```

**Forward fill using `tidyr`**

```r
library(tidyr)
df_ffill <- df_with_missing |> fill(Glucose, Diagnosis, .direction = \"down\")

cat(sprintf(\"Original shape:     %d rows\n\", nrow(df_with_missing)))  # Original shape:     100 rows
cat(sprintf(\"After dropping NAs: %d rows\n\", nrow(df_dropped)))       # After dropping NAs: 88 rows
cat(sprintf(\"After filling NAs:  %d rows\n\", nrow(df_filled)))        # After filling NAs:  100 rows
```
" %}

{% capture text %}
**Key Takeaways**

- **readr and base R** allow you to easily load, explore, and **clean real-world medical data** from CSV, Excel, JSON, or databases.
- **Missing data** is common in healthcare datasets — learn to handle it responsibly through **filling, dropping, or flagging**.
**- CSV remains the most widely used format** for clinical and research data exchange.
- Understanding how to **properly import and clean data** is the first step in medical data analysis.
{% endcapture %}
{% include alert.html text=text color=secondary %}