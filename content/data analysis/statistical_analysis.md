---
section_id: Data Analysis with R
nav_order: 7
title: Statistical Analysis
topics: statistics, t-test, ANOVA, chi-square, correlation, regression
---

**Statistical analysis** is at the heart of **medical research and clinical decision-making**. It allows us to determine whether observed patterns in patient data are due to chance or represent meaningful differences or associations.

{% include question.html header="Descriptive Statistics" text="

Descriptive statistics **summarize your dataset** and provide the foundation for deeper analysis.

In medicine, these **metrics describe patient demographics, laboratory results, and treatment outcomes** — helping you quickly understand what's typical or unusual in your data.

🧪 **Common Measures**

- Measures of central tendency:

    - Mean (e.g., average blood pressure)
    - Median (e.g., middle value of patient age)
    - Mode (e.g., most common diagnosis)

- Measures of variability:

    - Range (e.g., youngest to oldest patient)
    - Standard deviation (e.g., how spread out glucose levels are)

- Frequencies and proportions:

    - Counts and percentages (e.g., 60% of patients are female)

**Let's define a function to describe clinical data.**

```r
describe_data <- function(x, column_name) {
  # Generate comprehensive descriptive statistics.
  mode_val <- as.numeric(names(sort(table(x), decreasing = TRUE)[1]))
  iqr_val  <- IQR(x, na.rm = TRUE)

  cat(sprintf(\"\n=== Descriptive Statistics for %s ===\n\", column_name))
  cat(sprintf(\"Count:              %d\n\",    sum(!is.na(x))))
  cat(sprintf(\"Mean:               %.2f\n\",  mean(x,   na.rm = TRUE)))
  cat(sprintf(\"Median:             %.2f\n\",  median(x, na.rm = TRUE)))
  cat(sprintf(\"Mode:               %.2f\n\",  mode_val))
  cat(sprintf(\"Standard Deviation: %.2f\n\",  sd(x,     na.rm = TRUE)))
  cat(sprintf(\"Range:              %.2f\n\",  diff(range(x, na.rm = TRUE))))
  cat(sprintf(\"IQR:                %.2f\n\",  iqr_val))
}
```

**Example Use**

```r
describe_data(df$Glucose,        \"Fasting Glucose (mg/dL)\")
describe_data(df$Age,            \"Patient Age (years)\")
```
" %}

# **Univariate Tests**

{% include question.html header="t-tests" text="

# **One-sample t-test**

Check if the **average fasting glucose** differs significantly from the normal fasting level of **100 mg/dL**.

```r
population_mean <- 100
result <- t.test(df$Glucose, mu = population_mean)

cat(\"\n=== One-Sample T-Test ===\n\")
cat(sprintf(\"Testing if mean glucose differs from %d mg/dL\n\", population_mean))
cat(sprintf(\"Sample mean:   %.2f\n\",  mean(df$Glucose)))
cat(sprintf(\"T-statistic:   %.4f\n\",  result$statistic))
cat(sprintf(\"P-value:       %.4f\n\",  result$p.value))
```

💡 **Clinical meaning:** A significant p-value (< 0.05) suggests that your patient group's glucose levels are not within normal limits.

# **Two-sample t-test**

Compare blood pressure between diabetic and hypertensive patients.

```r
bp_diabetic     <- df$Blood_Pressure[df$Diagnosis == \"Diabetes\"]
bp_hypertensive <- df$Blood_Pressure[df$Diagnosis == \"Hypertension\"]

result <- t.test(bp_diabetic, bp_hypertensive)

cat(\"\n=== Two-Sample T-Test ===\n\")
cat(sprintf(\"T-statistic: %.4f\n\", result$statistic))
cat(sprintf(\"P-value:     %.4f\n\", result$p.value))
```

💡 *Clinical meaning:* Tests if there's a significant difference in blood pressure between the two groups.

# **Paired t-test example (before/after data)**

Evaluate if **blood pressure medication** effectively reduces **systolic BP**.

```r
set.seed(42)
bp_before <- sample(df$Blood_Pressure, 30)
bp_after  <- bp_before - rnorm(30, mean = 5, sd = 10)   # Simulated reduction

result <- t.test(bp_before, bp_after, paired = TRUE)

cat(\"\n=== Paired T-Test ===\n\")
cat(sprintf(\"Mean before: %.2f\n\", mean(bp_before)))
cat(sprintf(\"Mean after:  %.2f\n\", mean(bp_after)))
cat(sprintf(\"P-value:     %.4f\n\", result$p.value))
```
💡 *Clinical meaning:* Determines whether treatment significantly lowered blood pressure.
" %}

{% include question.html header="ANOVA (Analysis of Variance)" text="

# **One-way Analysis of Variance (ANOVA)**

ANOVA is an extension to the t-test, where there can be more than 2 groups being compared. Here we compare **mean blood pressure** across **different diagnosis groups**.

```r
anova_result <- aov(Blood_Pressure ~ Diagnosis, data = df)
summary_result <- summary(anova_result)

f_stat  <- summary_result[[1]]$`F value`[1]
p_value <- summary_result[[1]]$`Pr(>F)`[1]

cat(\"\n=== One-Way ANOVA ===\n\")
cat(sprintf(\"F-statistic: %.4f, P-value: %.4f\n\", f_stat, p_value))
```

💡 *Clinical meaning:* Tests if blood pressure differs across diagnosis groups.

## **Post-hoc analysis** is required when ANOVA is significant (p-value < 0.05).

```r
if (p_value < 0.05) {
  cat(\"\nPost-hoc pairwise comparisons (Tukey HSD):\n\")
  print(TukeyHSD(anova_result))
}
```
A p-value threshold of 0.05 is the conventional standard. Going above (e.g., 0.10) increases the risk of:

- **Type I errors **— falsely rejecting a true null hypothesis
- Results that are **less likely to replicate** in future studies
- Conclusions that **reviewers may view as tentative or inconclusive**
" %}

{% include question.html header="Chi-Square Tests" text="

# **Chi-square test of independence**

Check if **Diagnosis** is associated with a **binary risk factor** (e.g., high blood pressure threshold).

```r
df$High_BP <- ifelse(df$Blood_Pressure >= 140, \"High\", \"Normal\")

contingency <- table(df$Diagnosis, df$High_BP)
result      <- chisq.test(contingency)

cat(\"\n=== Chi-Square Test of Independence ===\n\")
print(contingency)
cat(sprintf(\"P-value: %.4f\n\", result$p.value))
```

💡 *Clinical meaning:* A significant association suggests high blood pressure may relate to diagnosis.

# **Chi-square goodness of fit test**

Test if **diagnosis distribution** follows expected population proportions.

```r
observed            <- table(df$Diagnosis)
expected_proportions <- c(Diabetes = 0.33, Healthy = 0.34, Hypertension = 0.33)
expected            <- expected_proportions * nrow(df)

result <- chisq.test(observed, p = expected_proportions)
cat(\"\n=== Chi-Square Goodness of Fit ===\n\")
cat(sprintf(\"P-value: %.4f\n\", result$p.value))
```
" %}

# **Correlation and Regression Analysis**

{% include question.html header="Correlation" text="

💡 *Clinical meaning:* Identify linear relationships (e.g., Age positively correlating with blood pressure).

```r
cat(\"\n=== Correlation Analysis ===\n\")
numeric_cols  <- df |> select(Age, Glucose, Blood_Pressure)
corr_matrix   <- cor(numeric_cols, use = \"complete.obs\")
print(round(corr_matrix, 3))
```
" %}

{% include question.html header="Simple Linear Regression" text="

**Predict Glucose from Age.**

```r
model   <- lm(Glucose ~ Age, data = df)
summary_m <- summary(model)

slope     <- coef(model)[\"Age\"]
r_squared <- summary_m$r.squared
p_value   <- summary_m$coefficients[\"Age\", \"Pr(>|t|)\"]

cat(\"\n=== Linear Regression ===\n\")
cat(sprintf(\"Slope: %.2f, R²: %.3f, P-value: %.4f\n\", slope, r_squared, p_value))
```

💡 *Clinical meaning:* Each 1-year increase in age predicts an average change of X mg/dL in glucose.
" %}

{% include question.html header="Logistic Regression" text="

**Predict presence of high blood pressure (Yes/No) using Age.**

Load packages

```r
library(dplyr)
```

Prepare data

```r
df <- df |>
  mutate(Hypertensive = as.integer(Blood_Pressure >= 140))

set.seed(42)
train_idx <- sample(seq_len(nrow(df)), size = floor(0.7 * nrow(df)))
train_df  <- df[train_idx, ]
test_df   <- df[-train_idx, ]
```

Fit logistic regression model

```r
log_model <- glm(Hypertensive ~ Age + Glucose, data = train_df, family = binomial)
```

Predict and evaluate

```r
pred_prob  <- predict(log_model, newdata = test_df, type = \"response\")
pred_class <- ifelse(pred_prob > 0.5, 1, 0)

accuracy <- mean(pred_class == test_df$Hypertensive)

cat(\"\n=== Logistic Regression: Predicting Hypertension ===\n\")
cat(sprintf(\"Accuracy: %.3f\n\", accuracy))

cat(\"\nConfusion Matrix:\n\")
print(table(Predicted = pred_class, Actual = test_df$Hypertensive))
```
" %}

{% capture text %}
**Key Takeaway**

- Use **descriptive statistics** to summarize patient data.
- Apply **t-tests** and **ANOVA** to detect significant group differences.
- Use **Chi-square** tests for categorical associations.
- **Correlation** and **regression** uncover relationships and prediction patterns.

Together, these tools form the **backbone of clinical research and evidence-based medicine** — helping transform raw data into actionable insights.
{% endcapture %}
{% include alert.html text=text color=secondary %}