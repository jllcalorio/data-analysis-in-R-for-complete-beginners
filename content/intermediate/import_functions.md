---
section: Intermediate R
nav_order: 5
title: Importing Functions from Packages
topics: import, function, module
---

R's power comes from its vast ecosystem of packages. Learning to load and use functions from packages effectively is crucial for productive programming.

{% include question.html header="Basic Library Statements" text="

Below are the common ways to load packages that are already built by other developers.

**Load an entire package**

```r
library(dplyr)

# Create a sample data
sample_df <- data.frame(
  Patient_ID  = 101:105,
  Name        = c(\"Ana\", \"Luis\", \"Maria\", \"Jose\", \"Carmen\"),
  Age         = c(34, 45, 29, 50, 41)
)

# This is what sample_df looks like:
print(sample_df)
#   Patient_ID   Name Age
# 1        101    Ana  34
# 2        102   Luis  45
# 3        103  Maria  29
# 4        104   Jose  50
# 5        105 Carmen  41

result <- filter(sample_df, Age > 40)   # Use package functions directly

# This is what the filtered data looks like:
print(result)
#   Patient_ID   Name Age
# 1        102   Luis  45
# 2        104   Jose  50
# 3        105 Carmen  41
```

Install a package first (if not already installed)

```r
install.packages(\"dplyr\")
library(dplyr)
```

Use a function from a package without loading it

You can call a single function from a package using `::` without loading the whole package.

```r
result <- dplyr::filter(sample_df, Age > 40)
```

This is useful when you only need one function, or when two packages have functions with the same name.

**Why not load everything?**

- Packages can contain many functions; loading only what you need keeps your workspace clean.
- Name conflicts between packages can cause unexpected errors.
- Use `package::function()` notation when **conflicts arise**.
" %}

**Common Built-in and Base R Functions**

{% include question.html header="Math Functions (base R)" text="

R has a rich set of built-in mathematical functions — no package needed.

```r
# Square root and power
sqrt(16)         # 4
2 ^ 3            # 8

# Factorial and logarithms
factorial(5)     # 120
log(10)          # Natural log:    2.302585
log10(100)       # Base-10 log:    2
log2(8)          # Base-2 log:     3

# Trigonometric
sin(pi / 2)      # 1
cos(0)           # 1

# Rounding
ceiling(4.2)     # Round up:   5
floor(4.8)       # Round down: 4
round(4.567, 2)  # Round to 2 decimal places: 4.57

# Constants
pi               # 3.141593
exp(1)           # e = 2.718282
```

" %}

{% include question.html header="Random Number Functions (base R)" text="

R has built-in random number generation — useful for randomization in research.

```r
# Generate random numbers
runif(1)                   # One random float between 0 and 1
sample(1:10, 1)            # Random integer between 1 and 10
runif(1, min = 1.5, max = 10.5)   # Random float in a range
```

**Work with vectors**

```r
fruits <- c(\"apple\", \"banana\", \"orange\", \"grape\")
sample(fruits, 1)    # Random choice (1 item)
sample(fruits, 2)    # Random sample of 2 items (without replacement)
```

**Shuffle a vector**

```r
numbers <- 1:5
shuffled <- sample(numbers)
print(shuffled)   # Vector is now shuffled
```

**Set seed for reproducible results**

```r
set.seed(42)
sample(1:100, 1)   # Will always return the same value with seed 42

# The result will always be 49
```
" %}

{% include question.html header="Date and Time Functions (base R)" text="

```r
# Current date and time
now   <- Sys.time()
today <- Sys.Date()

cat(\"Current datetime:\", format(now), \"\n\")
cat(\"Today's date:\",    format(today), \"\n\")
```

**Formatting dates**

```r
formatted_date <- format(now, \"%Y-%m-%d %H:%M:%S\")
cat(\"Formatted:\", formatted_date, \"\n\")
```

**Date arithmetic**

```r
tomorrow  <- today + 1
next_week <- today + 7
past_date <- today - 30

cat(\"Tomorrow:\",  format(tomorrow),  \"\n\")
cat(\"Next week:\", format(next_week), \"\n\")
cat(\"30 days ago:\", format(past_date), \"\n\")
```

**Parse date strings**

```r
date_string <- \"2025-12-25\"
christmas   <- as.Date(date_string, format = \"%Y-%m-%d\")
cat(\"Christmas:\", format(christmas), \"\n\")
```
" %}

{% include question.html header="File and Path Utilities (base R)" text="

```r
# Get current working directory
current_dir <- getwd()
cat(\"Current directory:\", current_dir, \"\n\")

# List files in directory
files <- list.files(\".\")
cat(\"Files in current directory:\", paste(files, collapse = \", \"), \"\n\")

# Path construction
file_path <- file.path(\"data\", \"files\", \"example.txt\")
cat(\"File path:\", file_path, \"\n\")

# Check if file/directory exists
cat(\"Path exists:\", file.exists(file_path), \"\n\")
```
" %}

{% include question.html header="Creating Reusable Functions in a Script" text="

You can organize your own reusable functions in a separate .R file and load them with `source()`.

```r
# utils.R — A script you might create
format_currency <- function(amount, currency = \"PHP\") {
  # Format a number as currency.
  formatC(amount, format = \"f\", digits = 2, big.mark = \",\") |>
    paste(currency, x = currency, sep = \" \")
}

validate_email <- function(email) {
  # Basic email validation.
  grepl(\"@\", email) & grepl(\"\\\\.\", sub(\".*@\", \"\", email))
}

calculate_tip <- function(bill_amount, tip_percentage = 15) {
  # Calculate tip amount.
  bill_amount * (tip_percentage / 100)
}
```

```r
# main.R — Using your script
source(\"utils.R\")

bill  <- 85.50
tip   <- calculate_tip(bill, 18)
total <- bill + tip

cat(sprintf(\"Bill:  PHP %.2f\n\", bill))    # Bill:  PHP 85.50
cat(sprintf(\"Tip:   PHP %.2f\n\", tip))     # Tip:   PHP 15.39
cat(sprintf(\"Total: PHP %.2f\n\", total))   # Total: PHP 100.89
```
" %}

{% capture text %}
PRO TIP

In R, a package is a collection of functions, datasets, and documentation bundled together. You install packages once with `install.packages()` and load them per session with `library()`. The `::` operator lets you use a single function from a package without loading it globally — helpful for avoiding name conflicts.
{% endcapture %}
{% include alert.html text=text color=secondary %}