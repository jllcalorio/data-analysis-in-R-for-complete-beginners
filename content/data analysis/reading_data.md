---
section_id: Data Analysis with R
nav_order: 3
title: Reading and Loading Data
topics: read, import, readr, csv
---

In medical research and hospital informatics, data often comes from **electronic health records (EHRs), lab systems, or survey results** — usually in formats like CSV, Excel, or JSON.

This section will teach you how to **load these files into R**, so you can begin analyzing them effectively.

{% include question.html header="Reading CSV Files" text="

CSV (Comma-Separated Values) is one of the most common formats for exporting medical data — from patient logs to laboratory results.

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
  \"data.csv\",
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

**Reading JSON files**

```r
library(DBI)
library(RSQLite)

con    <- dbConnect(RSQLite::SQLite(), \"hospital.db\")
df_sql <- dbGetQuery(con, \"SELECT * FROM patients\")
dbDisconnect(con)
```

**Working with Our Sample CSV**

```r
df <- read_csv(\"sample_patients.csv\")
df$Admission_Date <- as.Date(df$Admission_Date)

cat(\"Data loaded successfully!\n\")
print(head(df))
```
" %}

{% include question.html header="Handling Missing Data" text="

Missing data is very common in medical research — for example, when a lab result isn't recorded or a patient skips a follow-up visit.

Let's simulate and handle missing values:

```r
library(dplyr)

df_with_missing <- df
df_with_missing$Glucose[6:11]    <- NA
df_with_missing$Diagnosis[16:21] <- NA

cat(\"Missing data summary:\n\")
print(colSums(is.na(df_with_missing)))
```

**Strategies for handling missing data**

**Drop rows with missing values**

```r
df_dropped <- na.omit(df_with_missing)
```

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

cat(sprintf(\"Original shape:       %d rows\n\", nrow(df_with_missing)))
cat(sprintf(\"After dropping NAs:   %d rows\n\", nrow(df_dropped)))
cat(sprintf(\"After filling NAs:    %d rows\n\", nrow(df_filled)))
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