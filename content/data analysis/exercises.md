---
section: Data Analysis with R
nav_order: 11
title: Exercises with Solutions
topics: exercises
---

{% include question.html header="Exercise 1: Data Visualization" text="

**Goal:** Visualize the relationship between Age and Blood Pressure using a scatter plot.

**Instructions:**

1. Use `ggplot2`.
2. Add axis labels and a title.

**Question:**

**What trend** do you observe between Age and Blood Pressure across diagnoses?

" solution="

```r
library(ggplot2)

ggplot(df, aes(x = Age, y = Blood_Pressure, color = Diagnosis)) +
  geom_point(alpha = 0.7) +
  labs(
    title = \"Age vs Blood Pressure by Diagnosis\",
    x     = \"Age\",
    y     = \"Blood Pressure (mmHg)\"
  ) +
  theme_bw()
```
" %}

{% include question.html header="Exercise 2: Independent t-test" text="

**Goal:** Compare if the average glucose of Diabetes and Healthy groups are significantly different.

**Instructions:**

1. Extract glucose data for both groups.
2. Use `t.test()`.
3. Print the t-statistic and p-value.

**Question:**

Is there a statistically significant difference at **α = 0.05**?

" solution="

```r
glucose_diabetes <- df$Glucose[df$Diagnosis == \"Diabetes\"]
glucose_healthy  <- df$Glucose[df$Diagnosis == \"Healthy\"]

result <- t.test(glucose_diabetes, glucose_healthy)

cat(sprintf(\"T-statistic: %.3f, P-value: %.4f\n\",
            result$statistic, result$p.value))
```
" %}

{% include question.html header="Exercise 3: Logistic Regression" text="

**Goal:** Predict whether a patient has a high glucose level (above median) using `Age` and `Blood_Pressure`.

**Instructions:**

1. Create a binary column **High_Glucose** (1 = above median, 0 = below).
2. Split the data into training/testing sets.
3. Fit a logistic regression model and check accuracy.

**Question:**

**How well does the model predict** high-glucose patients based on age and blood pressure?

" solution="

```r
library(dplyr)

# Create target variable
median_glucose <- median(df$Glucose)
df <- df |> mutate(High_Glucose = as.integer(Glucose > median_glucose))

# Train/test split
set.seed(42)
train_idx  <- sample(seq_len(nrow(df)), size = floor(0.7 * nrow(df)))
train_data <- df[train_idx, ]
test_data  <- df[-train_idx, ]

# Train model
model <- glm(High_Glucose ~ Age + Blood_Pressure, data = train_data, family = binomial)

# Predict and evaluate
pred_prob  <- predict(model, newdata = test_data, type = \"response\")
pred_class <- ifelse(pred_prob > 0.5, 1, 0)
accuracy   <- mean(pred_class == test_data$High_Glucose)

cat(sprintf(\"Model accuracy: %.2f\n\", accuracy))
```
" %}