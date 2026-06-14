---
section: Data Analysis with R
nav_order: 5
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

#  Ana   Luis  Maria   Jose Carmen 
#   34     45     29     50     41 

cat(\"Data type:\",      class(ages),  \"\n\")            # Data type: numeric 
cat(\"Length:\",         length(ages), \"\n\")            # length: 5

# Basic operations
cat(\"Mean age:\",       mean(ages),   \"\n\")            # Mean age: 39.8 
cat(\"Oldest patient:\", names(which.max(ages)), \"\n\")  # Oldest patient: Jose
```
" %}

{% include question.html header="Data Frame – Two-Dimensional Data" text="

A **data frame** is like a full spreadsheet (like Microsoft Excel or Google Sheets) — rows represent patients, and columns represent variables (e.g., age, diagnosis, or lab values).

**Example:** Creating a data frame of patient information

```r
sample_df <- data.frame(
  Patient_ID  = 101:105,
  Name        = c(\"Ana\", \"Luis\", \"Maria\", \"Jose\", \"Carmen\"),
  Age         = c(34, 45, 29, 50, 41),
  Diagnosis   = c(\"Diabetes\", \"Hypertension\", \"Healthy\", \"Diabetes\", \"Hypertension\"),
  Cholesterol = c(210, 190, 170, 250, 230)
)
```

This is how the data frame looks like:

```r
  Patient_ID   Name Age    Diagnosis Cholesterol
1        101    Ana  34     Diabetes         210
2        102   Luis  45 Hypertension         190
3        103  Maria  29      Healthy         170
4        104   Jose  50     Diabetes         250
5        105 Carmen  41 Hypertension         230
```
" %}

{% include question.html header="Data Frame Inspection Methods" text="

R provides several ways to quickly explore and summarize your dataset.

**First 3 rows:**

```r
head(sample_df, 3)
```

Result:

```r
  Patient_ID  Name Age    Diagnosis Cholesterol
1        101   Ana  34     Diabetes         210
2        102  Luis  45 Hypertension         190
3        103 Maria  29      Healthy         170
```

**Last 2 rows:**

```r
tail(sample_df, 2)
```

Result:

```r
  Patient_ID   Name Age    Diagnosis Cholesterol
4        104   Jose  50     Diabetes         250
5        105 Carmen  41 Hypertension         230
```

**Structure and data types:**

```r
str(sample_df)
```

Result:

```r
'data.frame':	5 obs. of  5 variables:
 $ Patient_ID : int  101 102 103 104 105
 $ Name       : chr  \"Ana\" \"Luis\" \"Maria\" \"Jose\" ...
 $ Age        : num  34 45 29 50 41
 $ Diagnosis  : chr  \"Diabetes\" \"Hypertension\" \"Healthy\" \"Diabetes\" ...
 $ Cholesterol: num  210 190 170 250 230
```

**Quick descriptive statistics:**

```r
summary(sample_df)
```

Result:

```r
   Patient_ID      Name                Age        Diagnosis          Cholesterol 
 Min.   :101   Length:5           Min.   :29.0   Length:5           Min.   :170  
 1st Qu.:102   Class :character   1st Qu.:34.0   Class :character   1st Qu.:190  
 Median :103   Mode  :character   Median :41.0   Mode  :character   Median :210  
 Mean   :103                      Mean   :39.8                      Mean   :210  
 3rd Qu.:104                      3rd Qu.:45.0                      3rd Qu.:230  
 Max.   :105                      Max.   :50.0                      Max.   :250
```

**Column-specific information:**

```r
table(sample_df$Diagnosis)  # Frequency of each diagnosis :  Diabetes Healthy Hypertension 
                            #                                       2       1            2
mean(sample_df$Cholesterol) # Average cholesterol level   : 210
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