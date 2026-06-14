---
section: Beginning R
nav_order: 8
title: String Formatting
topics: string, format
---

**String formatting** in R is typically done using the `paste()` or `paste0()` functions to combine text and variables, and `sprintf()` for formatted numeric output.

{% include question.html header="Using paste() and paste0()" text="

```r
name      <- \"Dr. Santos\"
diagnosis <- \"Hypertension\"

message <- paste(\"Patient seen by\", name, \"with\", diagnosis)
print(message) 

# Output
# \"Patient seen by Dr. Santos with Hypertension\"
```

To format numbers (e.g., decimals), use `sprintf()`:

```r
glucose       <- 92.457
formatted_msg <- sprintf(\"Fasting blood glucose: %.1f mg/dL\", glucose)
print(formatted_msg)   # Fasting blood glucose: 92.5 mg/dL
```
" %}

{% include question.html header="Cleaning Text with Base R" text="

R includes functions to clean or modify text — perfect for cleaning patient notes or survey entries.

```r
text <- \"  Hypertension Stage II  \"

print(toupper(text))                           # \"  HYPERTENSION STAGE II  \"
print(tolower(text))                           # \"  hypertension stage ii  \"
print(trimws(text))                            # \"Hypertension Stage II\" (removes whitespace)
print(gsub(\"Stage II\", \"Stage I\", text))       # \"  Hypertension Stage I  \" (Replaces text)
```
" %}

{% include question.html header="Splitting and Joining" text="

```r
medications <- \"Aspirin,Metformin,Lisinopril\"
med_list    <- strsplit(medications, \",\")[[1]]        # Split into a vector
rejoined    <- paste(med_list, collapse = \" | \")      # Join back with a separator

print(med_list)                                       # \"Aspirin\"    \"Metformin\"  \"Lisinopril\"
print(rejoined)                                       # \"Aspirin | Metformin | Lisinopril\"
```
" %}

{% capture text %}
String formatting helps you present data in clear, readable, and professional ways — whether you're summarizing patient data, generating reports, or printing analysis results. Clean text formatting is essential in medical reporting and data communication.
{% endcapture %}
{% include alert.html text=text color=secondary %}
