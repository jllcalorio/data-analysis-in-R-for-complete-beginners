---
section: Data Analysis with R
nav_order: 9
title: Data Visualization
topics: ggplot2, visualization
---

**Visualizations help reveal patterns** in clinical data — such as **disease prevalence, lab result distributions, and relationships between vital signs** — and effectively communicate findings to support medical decisions or publications.

{% include question.html header="Basic Plotting with ggplot2" text="

**Load package and set default theme**

```r
library(ggplot2)
theme_pub <- theme_classic(base_size = 35) +
  theme(
    plot.title = element_text(
      size = 20,
      face = \"bold\",
      hjust = 0.5
    ),
    axis.title = element_text(
      size = 20,
      face = \"bold\"
    ),
    axis.text = element_text(
      size = 20,
      color = \"black\"
    ),
    legend.title = element_text(
      size = 20,
      face = \"bold\"
    ),
    legend.text = element_text(
      size = 20
    ),
    plot.margin = margin(10, 10, 10, 10)
  )
```
" %}

{% include question.html header="Histogram — Distribution of Glucose Levels" text="

💡 *Use case:* Quickly visualize how many patients fall into normal, prediabetic, or diabetic glucose ranges.

```r
ggplot(df, aes(x = Glucose)) +
  geom_histogram(
    bins = 20,
    fill = \"#2C7FB8\",
    color = \"white\",
    linewidth = 0.5
  ) +
  labs(
    title = \"Distribution of Fasting Glucose Levels\",
    x = \"Glucose (mg/dL)\",
    y = \"Number of Patients\"
  ) +
  theme_pub
```
" %}

{% include figure.html img="dist_fgl.png" alt="distribution of fasting glucose levels" caption="" width="100%" %}

{% include question.html header="Box plot — Glucose by Diagnosis" text="

💡 *Use case:* Compare glucose variability across different conditions (e.g., Diabetes, Hypertension, Normal).

```r
ggplot(df, aes(x = Diagnosis, y = Glucose, fill = Diagnosis)) +
  geom_boxplot(
    width = 0.5,
    alpha = 0.8,
    outlier.shape = NA
  ) +
  geom_jitter(
    width = 0.15,
    alpha = 0.5,
    size = 1.8
  ) +
  scale_fill_brewer(
    palette = \"Set2\",
    guide = \"none\"
  ) +
  labs(
    title = \"Glucose Distribution by Diagnosis\",
    x = \"Diagnosis\",
    y = \"Glucose (mg/dL)\"
  ) +
  theme_pub +
  theme(
    axis.text.x = element_text(
      angle = 0,
      hjust = 0.5
    )
  )
```
" %}

{% include figure.html img="boxplot_glucose_dist.png" alt="distribution of fasting glucose levels" caption="" width="100%" %}

{% include question.html header="Advanced Plotting with ggplot2" text="
Here, we'll produce the following plots:

- Correlation heatmap
- Scatter plot
- Density plot
- Violin plot
- Count/bar plot
" %}

{% include question.html header="Correlation heatmap" text="

💡 *Use case:* Identify correlations (e.g., between Age and Blood Pressure).

```r
library(reshape2)   # or use tidyr::pivot_longer

corr_matrix <- cor(df |> select(Age, Glucose, Blood_Pressure), use = \"complete.obs\")
corr_melt   <- melt(corr_matrix)

ggplot(corr_melt,
       aes(
         x = Var1,
         y = Var2,
         fill = value
       )) +
  geom_tile(
    color = \"white\",
    linewidth = 0.5
  ) +
  geom_text(
    aes(label = sprintf(\"%.2f\", value)),
    size = 4.5
  ) +
  scale_fill_gradient2(
    low = \"#2166AC\",
    mid = \"white\",
    high = \"#B2182B\",
    midpoint = 0,
    limits = c(-1, 1),
    name = \"Correlation\"
  ) +
  coord_fixed() +
  labs(
    title = \"Correlation Matrix of Clinical Variables\",
    x = NULL,
    y = NULL
  ) +
  theme_minimal(base_size = 14) +
  theme(
    plot.title = element_text(
      face = \"bold\",
      size = 16,
      hjust = 0.5
    ),
    axis.text = element_text(
      color = \"black\"
    ),
    panel.grid = element_blank()
  )
```
" %}

{% include figure.html img="corr_heatmap.png" alt="correlation between clinical variables" caption="" width="100%" %}

{% include question.html header="Scatter plot with regression line" text="

💡 *Use case:* Explore whether glucose tends to rise with age and how it differs by diagnosis.

```r
ggplot(
  df,
  aes(
    x = Age,
    y = Glucose,
    color = Diagnosis
  )
) +
  geom_point(
    size = 2.5,
    alpha = 0.7
  ) +
  geom_smooth(
    method = \"lm\",
    se = TRUE,
    linewidth = 1
  ) +
  labs(
    title = \"Association Between Age and Glucose\",
    x = \"Age (Years)\",
    y = \"Glucose (mg/dL)\",
    color = \"Diagnosis\"
  ) +
  theme_pub
```
" %}

{% include figure.html img="scatter_plot.png" alt="scatterp lot between age and glucose" caption="" width="100%" %}

{% include question.html header="Density plot" text="

💡 *Use case:* Compare glucose distributions across diagnoses using kernel density estimation.

```r
ggplot(
  df,
  aes(
    x = Glucose,
    fill = Diagnosis,
    color = Diagnosis
  )
) +
  geom_density(
    alpha = 0.25,
    linewidth = 1
  ) +
  labs(
    title = \"Distribution of Glucose Levels by Diagnosis\",
    x = \"Glucose (mg/dL)\",
    y = \"Density\"
  ) +
  theme_pub
```
" %}

{% include figure.html img="density_plot.png" alt="density plot of glucose levels by diagnosis" caption="" width="100%" %}

{% include question.html header="Violin plot" text="

💡 *Use case:* Examine BMI variation among diagnostic categories.

```r
ggplot(
  df,
  aes(
    x = Diagnosis,
    y = Blood_Pressure,
    fill = Diagnosis
  )
) +
  geom_violin(
    trim = FALSE,
    alpha = 0.7
  ) +
  geom_boxplot(
    width = 0.12,
    fill = \"white\",
    linewidth = 0.5
  ) +
  labs(
    title = \"Blood Pressure Distribution by Diagnosis\",
    x = \"Diagnosis\",
    y = \"Blood Pressure (mmHg)\"
  ) +
  scale_fill_brewer(
    palette = \"Set2\",
    guide = \"none\"
  ) +
  theme_pub +
  theme(
    axis.text.x = element_text(
      angle = 45,
      hjust = 1
    )
  )
```
" %}

{% include figure.html img="violin_plot.png" alt="violiin plot of blood pressure distribution by diagnosis" caption="" width="100%" %}

{% include question.html header="Count/bar plot" text="

💡 *Use case:* Display patient counts per glucose category within each diagnosis.

```r
ggplot(
  df,
  aes(
    x = Glucose_Category,
    fill = Diagnosis
  )
) +
  geom_bar(
    position = position_dodge(width = 0.8),
    width = 0.7
  ) +
  labs(
    title = \"Glucose Categories by Diagnosis\",
    x = \"Glucose Category\",
    y = \"Count\",
    fill = \"Diagnosis\"
  ) +
  theme_pub +
  theme(
    axis.text.x = element_text(
      angle = 0,
      hjust = 0.5
    )
  )
```
" %}

{% include figure.html img="count_bar_chart.png" alt="count bar chart of glucose categories by diagnosis" caption="" width="100%" %}

{% include question.html header="Combining Multiple Plots" text="

💡 *Use case:* Summarize proportions of diagnoses and visualize clinical indicators together.

```r
library(patchwork)

p1 <- ggplot(df, aes(x = Age)) +
  geom_histogram(
    bins = 15,
    fill = \"#2C7FB8\",
    color = \"white\"
  ) +
  labs(
    title = \"A. Age Distribution\",
    x = \"Age (Years)\",
    y = \"Count\"
  ) +
  theme_pub

avg_glucose <- df |>
  group_by(Diagnosis) |>
  summarise(
    Mean_Glucose = mean(
      Glucose,
      na.rm = TRUE
    ),
    .groups = \"drop\"
  ) |>
  arrange(desc(Mean_Glucose))

p2 <- ggplot(
  avg_glucose,
  aes(
    x = reorder(Diagnosis, Mean_Glucose),
    y = Mean_Glucose
  )
) +
  geom_col(
    fill = \"#2C7FB8\",
    width = 0.7
  ) +
  coord_flip() +
  labs(
    title = \"B. Mean Glucose by Diagnosis\",
    x = NULL,
    y = \"Mean Glucose (mg/dL)\"
  ) +
  theme_pub

p3 <- ggplot(
  df,
  aes(
    x = Age,
    y = Blood_Pressure
  )
) +
  geom_point(
    alpha = 0.7,
    size = 2
  ) +
  geom_smooth(
    method = \"lm\",
    color = \"black\",
    se = TRUE
  ) +
  labs(
    title = \"C. Age vs Blood Pressure\",
    x = \"Age (Years)\",
    y = \"Blood Pressure (mmHg)\"
  ) +
  theme_pub

p4 <- ggplot(
  df,
  aes(
    x = \"\",
    fill = Diagnosis
  )
) +
  geom_bar(
    width = 1
  ) +
  coord_polar(\"y\") +
  labs(
    title = \"D. Diagnosis Composition\"
  ) +
  theme_void(base_size = 14) +
  theme(
    plot.title = element_text(
      face = \"bold\",
      size = 16,
      hjust = 0.5
    )
  )

(p1 + p2) /
(p3 + p4)
```
" %}

{% include figure.html img="multi_plot.png" alt="multiple figures in one plot" caption="" width="100%" %}

{% capture text %}
**Key Takeaways**

- `ggplot2` uses a layered **grammar of graphics** — start with data, add aesthetics, then layers.
- Plots like density, violin, and scatter with regression add statistical depth.
- Visualizations are crucial for **pattern recognition, data quality assessment, and research presentation**.
- Use them to **compare distributions, examine relationships, and summarize populations in any data**.
{% endcapture %}
{% include alert.html text=text color=secondary %}