---
section_id: Data Analysis with R
nav_order: 6
title: Data Visualization
topics: ggplot2, visualization
---

**Visualizations help reveal patterns** in clinical data — such as **disease prevalence, lab result distributions, and relationships between vital signs** — and effectively communicate findings to support medical decisions or publications.

{% include question.html header="Basic Plotting with ggplot2" text="

**Load package and set theme**

```r
library(ggplot2)
theme_set(theme_bw())
```

**Histogram — Distribution of Glucose Levels**

💡 *Use case:* Quickly visualize how many patients fall into normal, prediabetic, or diabetic glucose ranges.

```r
ggplot(df, aes(x = Glucose)) +
  geom_histogram(bins = 20, fill = \"skyblue\", color = \"black\", alpha = 0.7) +
  labs(
    title = \"Distribution of Fasting Glucose Levels\",
    x     = \"Glucose (mg/dL)\",
    y     = \"Number of Patients\"
  )
```

**Box plot — Glucose by Diagnosis**

💡 *Use case:* Compare glucose variability across different conditions (e.g., Diabetes, Hypertension, Normal).

```r
ggplot(df, aes(x = Diagnosis, y = Glucose, fill = Diagnosis)) +
  geom_boxplot(alpha = 0.7) +
  labs(
    title = \"Glucose Distribution by Diagnosis\",
    x     = \"Diagnosis\",
    y     = \"Glucose (mg/dL)\"
  ) +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```
" %}

{% include question.html header="Advanced Plotting with ggplot2" text="

**Correlation heatmap**

💡 *Use case:* Identify correlations (e.g., between Age and Blood Pressure).

```r
library(reshape2)   # or use tidyr::pivot_longer

corr_matrix <- cor(df |> select(Age, Glucose, Blood_Pressure), use = \"complete.obs\")
corr_melt   <- melt(corr_matrix)

ggplot(corr_melt, aes(x = Var1, y = Var2, fill = value)) +
  geom_tile() +
  geom_text(aes(label = round(value, 2)), color = \"white\") +
  scale_fill_gradient2(low = \"blue\", mid = \"white\", high = \"red\", midpoint = 0) +
  labs(title = \"Correlation Matrix of Clinical Variables\")
```

**Scatter plot with regression line**

💡 *Use case:* Explore whether glucose tends to rise with age and how it differs by diagnosis.

```r
ggplot(df, aes(x = Age, y = Glucose, color = Diagnosis)) +
  geom_point(alpha = 0.7) +
  geom_smooth(method = \"lm\", se = FALSE, color = \"red\") +
  labs(title = \"Age vs Glucose by Diagnosis\")
```

**Density plot**

💡 *Use case:* Compare glucose distributions across diagnoses using kernel density estimation.

```r
ggplot(df, aes(x = Glucose, fill = Diagnosis, color = Diagnosis)) +
  geom_density(alpha = 0.3) +
  labs(title = \"Glucose Distribution by Diagnosis\")
```

**Violin plot**

💡 *Use case:* Examine BMI variation among diagnostic categories.

```r
ggplot(df, aes(x = Diagnosis, y = Blood_Pressure, fill = Diagnosis)) +
  geom_violin(alpha = 0.7) +
  geom_boxplot(width = 0.1, fill = \"white\") +
  labs(title = \"Blood Pressure Distribution by Diagnosis\") +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

**Count/bar plot**

💡 *Use case:* Display patient counts per glucose category within each diagnosis.

```r
ggplot(df, aes(x = Glucose_Category, fill = Diagnosis)) +
  geom_bar(position = \"dodge\") +
  labs(
    title = \"Glucose Categories by Diagnosis\",
    x     = \"Glucose Category\",
    y     = \"Count\"
  ) +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```
" %}

{% include question.html header="Combining Multiple Plots" text="

💡 *Use case:* Summarize proportions of diagnoses and visualize clinical indicators together.

```r
library(ggplot2)
library(patchwork)   # install.packages(\"patchwork\")

# Age distribution
p1 <- ggplot(df, aes(x = Age)) +
  geom_histogram(bins = 15, fill = \"lightblue\", color = \"black\") +
  labs(title = \"Age Distribution\", x = \"Age (years)\", y = \"Count\")

# Average Glucose by Diagnosis
avg_glucose <- df |>
  group_by(Diagnosis) |>
  summarise(Mean_Glucose = mean(Glucose)) |>
  arrange(desc(Mean_Glucose))

p2 <- ggplot(avg_glucose, aes(x = reorder(Diagnosis, -Mean_Glucose), y = Mean_Glucose, fill = Diagnosis)) +
  geom_col() +
  labs(title = \"Average Glucose by Diagnosis\", x = \"Diagnosis\", y = \"Glucose (mg/dL)\")

# Scatter: Age vs Blood Pressure
p3 <- ggplot(df, aes(x = Age, y = Blood_Pressure)) +
  geom_point(alpha = 0.6, color = \"darkgreen\") +
  labs(title = \"Age vs Blood Pressure\", x = \"Age\", y = \"BP (mmHg)\")

# Diagnosis composition (pie-like bar)
p4 <- ggplot(df, aes(x = \"\", fill = Diagnosis)) +
  geom_bar(width = 1) +
  coord_polar(\"y\") +
  labs(title = \"Diagnosis Composition\") +
  theme_void()

# Combine with patchwork
(p1 + p2) / (p3 + p4)
```
" %}

{% capture text %}
**Key Takeaways**

- `ggplot2` uses a layered **grammar of graphics** — start with data, add aesthetics, then layers.
- Plots like density, violin, and scatter with regression add statistical depth.
- Visualizations are crucial for **pattern recognition, data quality assessment, and research presentation**.
- Use them to **compare distributions, examine relationships, and summarize populations in any data**.
{% endcapture %}
{% include alert.html text=text color=secondary %}