---
section_id: Intermediate R
nav_order: 5
title: Errors and Exception Handling
topics: errors
---

**Errors are inevitable in programming** — even in medical research and clinical data management. Learning how to handle them gracefully ensures that your programs remain **robust, safe, and user-friendly**, especially when dealing with sensitive or life-impacting information.

# **Types of Errors**

{% include question.html header="Syntax Errors" text="

These occur when R cannot parse your code due to incorrect syntax. They prevent the script from running entirely.

```r
print(\"Patient record loaded\"    # Missing closing parenthesis
if (age = 45) {                  # Should use == not =
print(\"Valid age\")               # Improperly placed brace
```

**Pop quiz**

Where do you think the errors are?

" solution="
```r
1. Missing closing parenthesis on the print() call
2. The condition should use == (comparison) instead of = (assignment)
3. Missing opening brace { for the if block
```
" %}

{% include question.html header="Runtime Errors (Conditions)" text="

These occur **during execution** — the syntax is correct, but something unexpected happens (like dividing by zero or accessing a missing element).

```r
10 / 0                   # Inf (R returns Infinity, not an error)
log(-1)                  # NaN with a warning
c(1, 2, 3)[10]           # NA — out-of-range index returns NA
as.integer(\"fever\")      # NA with a warning
nonexistent_object       # Error: object not found
```

**Note:** R is more lenient than many languages — division by zero gives `Inf`, and many type errors give `NA` with a warning rather than stopping execution. This makes it important to always check your results!

**Example:**

A clinical data program might silently return `NA` when trying to convert a non-numeric lab value. Always validate your inputs.
" %}

## **Basic Error Handling**

{% include question.html header="tryCatch Blocks" text="

Handle potential errors using `tryCatch()`.

```r
safe_bmi <- function(weight, height) {
  # Safely calculate BMI with error handling.
  tryCatch({
    if (height == 0) stop(\"Height cannot be zero!\")
    bmi <- weight / (height ^ 2)
    return(bmi)
  },
  error = function(e) {
    cat(\"Error:\", conditionMessage(e), \"\n\")
    return(NULL)
  })
}

result1 <- safe_bmi(60, 1.65)
result2 <- safe_bmi(70, 0)
```

**Output for result2:**

`Error: Height cannot be zero!`
" %}

{% include question.html header="Handling Warnings and Multiple Conditions" text="

Sometimes multiple things can go wrong — invalid inputs, missing values, or type coercion warnings.

```r
get_patient_age <- function(age_input) {
  # Process patient age input safely.
  tryCatch({
    age <- as.integer(age_input)
    if (is.na(age)) stop(\"Invalid input: age could not be converted to an integer.\")
    if (age < 0)    stop(\"Age cannot be negative.\")

    birth_year <- 2025 - age
    return(birth_year)
  },
  error = function(e) {
    cat(\"Invalid input:\", conditionMessage(e), \"\n\")
    return(NULL)
  },
  warning = function(w) {
    cat(\"Warning:\", conditionMessage(w), \"\n\")
    return(NULL)
  })
}

year <- get_patient_age(\"35\")
if (!is.null(year)) cat(\"You were born in\", year, \"\n\")

get_patient_age(\"fever\")
get_patient_age(-5)
```
" %}

{% include question.html header="tryCatch with finally" text="

These blocks let you **handle file operations safely**, which is vital when working with electronic medical records or lab results.

```r
read_patient_file <- function(filename) {
  # Read patient data with comprehensive error handling.
  con <- NULL
  tryCatch({
    con     <- file(filename, \"r\")
    content <- readLines(con)
    cat(\"Patient file read successfully!\n\")
    cat(\"File contains\", length(content), \"lines.\n\")
    return(content)
  },
  error = function(e) {
    cat(\"Error reading file:\", conditionMessage(e), \"\n\")
    return(NULL)
  },
  finally = {
    if (!is.null(con)) {
      close(con)
      cat(\"File connection closed.\n\")
    }
  })
}
```
" %}

{% include question.html header="Raising Custom Conditions" text="

Custom conditions make your programs **specific to your domain** — like raising an error when pharmacy stock is insufficient.

```r
# Define a custom condition constructor
insufficient_stock_error <- function(message, call = sys.call(-1)) {
  structure(
    class = c(\"insufficient_stock_error\", \"error\", \"condition\"),
    list(message = message, call = call)
  )
}

dispense_medication <- function(stock, quantity) {
  # Dispense medication with error checks.
  if (quantity <= 0) stop(\"Dispense quantity must be positive.\")
  if (quantity > stock) {
    stop(insufficient_stock_error(
      paste0(\"Cannot dispense \", quantity, \" units. Only \", stock, \" available.\")
    ))
  }
  stock <- stock - quantity
  return(stock)
}

tryCatch(
  dispense_medication(stock = 20, quantity = 50),
  insufficient_stock_error = function(e) {
    cat(\"Dispensing failed:\", conditionMessage(e), \"\n\")
  }
)
```

" %}

# **Debugging Tips**

Debugging helps you trace problems when something goes wrong in your data pipeline or algorithm.

```r
debug_lab_results <- function(data) {
  # Debugging function for lab result entries.
  cat(sprintf(\"DEBUG: Input class: %s\n\", class(data)))
  cat(sprintf(\"DEBUG: Input value: %s\n\", as.character(data)[1]))

  tryCatch({
    if (is.character(data)) {
      result <- toupper(data)
    } else if (is.numeric(data)) {
      result <- data * 2
    } else if (is.list(data)) {
      result <- lapply(data, function(x) x * 2)
    } else {
      stop(paste(\"Unsupported data type:\", class(data)))
    }

    cat(sprintf(\"DEBUG: Processed result: %s\n\", as.character(result)[1]))
    return(result)

  }, error = function(e) {
    cat(\"DEBUG: Exception occurred:\",   conditionMessage(e), \"\n\")
    cat(\"DEBUG: Exception class:\",      class(e)[1],         \"\n\")
    stop(e)   # Re-raise
  })
}

test_data <- list(\"hello\", 42, list(1, 2, 3))

for (item in test_data) {
  tryCatch({
    result <- debug_lab_results(item)
    cat(\"Success:\", as.character(result)[1], \"\n\n\")
  }, error = function(e) {
    cat(\"Failed:\", conditionMessage(e), \"\n\n\")
  })
}
```

{% capture text %}
Error handling is not just about preventing crashes — it's about **ensuring reliability and trust** in your programs.

In healthcare applications, properly handled errors can prevent incorrect medication doses, invalid data entries, or loss of patient information.

Robust error handling ensures that your systems **fail gracefully**, log meaningful messages, and protect both users and data integrity.
{% endcapture %}
{% include alert.html text=text color=secondary %}