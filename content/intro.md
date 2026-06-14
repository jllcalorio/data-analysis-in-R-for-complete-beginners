---
nav_order: 1
title: Introduction
---

Welcome to this beginner-friendly workshop designed especially for medical students and healthcare professionals. Over three immersive days, you'll learn R from the ground up — not just as a programming language, but as a practical tool for analyzing clinical and research data.

---

{% include question.html header="Workshop Overview" text="

R has become one of the most widely used languages in healthcare research and medical informatics. From analyzing patient data and visualizing disease trends to supporting AI-based diagnostics, R is transforming how health professionals handle data.

This workshop provides a **hands-on, structured approach to learning R fundamentals and applying them to real-world medical and research datasets**.
" %}

{% include question.html header="Workshop Overview" text="

R has become one of the most widely used languages in healthcare research and medical informatics. From analyzing patient data and visualizing disease trends to supporting AI-based diagnostics, R is transforming how health professionals handle data.

This workshop provides a hands-on, structured approach to learning R fundamentals and applying them to real-world medical and research datasets.
" %}

{% include question.html header="Duration & Format" text="


- **Duration:** 3-day intensive workshop
- **Format:** Hands-on learning with practical exercises
- **Schedule:** Sometime in 2026
- **Delivery:** Interactive sessions with live coding demonstrations
" %}

---

## **Learning Objectives**

By the end of this workshop, participants will be able to:

{% include question.html header="Technical Skills" text="

- **Handle Data Effectively:** Organize and manage patient or laboratory data using R's built-in structures
- **Perform Data Analysis:** Use dplyr to explore health-related datasets and compute descriptive statistics
- **Create Visualizations:** Generate charts for patient outcomes, clinical trials, or epidemiological trends
- **Perform Common statistical tests:** Apply tests such as t-test, ANOVA, chi-square, and logistic regression tests to biomedical datasets
- **Build a Foundation:** Prepare for advanced applications like biostatistics, machine learning, and clinical decision support
" %}

{% include question.html header="Practical Applications" text="

- **Read and process data** from various file formats
- **Filter and query datasets** to extract meaningful insights
- **Perform statistical tests** (`t-tests`, `ANOVA`, `chi-square`, `logistic regression`)
- Create professional **data visualizations**
- **Build a foundation** for advanced R applications
" %}

---

## **Target Audience**

This workshop is specially designed for DMSFI students and healthcare professionals who are ready to explore how programming and data can enhance medical decision-making, research, and innovation.

{% include question.html header="Primary Audience" text="

- **Students** in the Davao Medical School Foundation, Inc.
- **Complete beginners** with no prior programming experience
- **Professionals** looking to add R skills to their toolkit
- **Researchers** who need to analyze data programmatically
" %}


{% include question.html header="Prerequisites" text="

- **No programming experience required** - we start from the very basics
- **Basic computer literacy** (file management, using applications)
- **Willingness to learn** and practice hands-on coding
- **A laptop** with internet connection for installation and practice
" %}


{% include question.html header="Who Will Benefit Most" text="

- **Medical professionals** aiming to integrate data science into clinical practice or research
- **Medical students** preparing for coursework or electives involving biostatistics, informatics, or computational tools
- **Clinicians and researchers** seeking to enhance decision-making through data-driven approaches
- **Healthcare professionals** curious about programming, data analysis, and their applications in medicine
" %}

---

## **Expected Outcomes**

{% include question.html header="Immediate Skills (End of Workshop)" text="

- Confidently write **basic to intermediate** R programs and functions
- **Understand and apply** fundamental programming concepts
- Perform basic **data manipulation and analysis tasks**
- Create **simple visualizations** from datasets
" %}


{% include question.html header="Long-term Benefits: Clinical & Research Impact" text="

- **Data-Driven Insight:** Confidently explore and interpret clinical or survey data
- **Research Independence:** Perform your own data cleaning and analysis for publications
- **Problem-Solving:** Develop computational thinking skills
- **Foundation Building:** Prepared for advanced topics like machine learning
- **Automation in Practice:** Streamline repetitive workflows, such as summarizing lab data or generating reports
" %}


{% include question.html header="Practical Projects" text="

By workshop completion, you'll have created:

- **A personal library** of useful R functions
- **Mini-projects** analyzing sample clinical datasets (e.g., patient demographics, vital signs, or lab results)
- **Solutions to data-driven questions** often encountered in healthcare and research
- **A foundation** for continued learning and development
" %}

---

## **Workshop Structure**

{% include question.html header="Day 1: Foundation Building" text="

- R basics and development environment setup
- Variables, data types, and basic operations
- Introduction to programming logic
" %}


{% include question.html header="Day 2: Building Complexity" text="

- Control structures and functions
- Working with packages and handling errors
- Hands-on practice with increasingly complex problems
" %}


{% include question.html header="Day 3: Real-World Application" text="

- Data analysis with `dplyr`
- Statistical analysis and visualization
- Capstone project and wrap-up
" %}

---

## **What You'll Take Away**

{% include question.html header="Skills Portfolio" text="

- Comprehensive understanding of R fundamentals
- Experience with industry-standard data analysis tools
- Portfolio of completed programming projects
- Confidence to tackle new programming challenges
" %}


{% include question.html header="Resources for Continued Learning" text="

- Complete workshop materials and code examples
- Recommended resources for further study
- Clear pathways for advancing your R skills
" %}


{% include question.html header="Certificate of Completion" text="

Participants who complete all workshop activities will receive a Certificate of Completion in \"Data Analysis in R for Complete Beginners,\" issued by the Center for Research and Development, DMSFI.
" %}

---

## **Definition of Terms**

{% include question.html header="I. Programming and Data Basics" text="

- **Variable** – A named container used to store data values in a program.
- **Data Type** – The classification of data that tells R what kind of value is being stored (e.g., `numeric`, `character`, `logical`).
- **Vector** – An ordered collection of values of the same type (e.g., `c(10, 20, 30)`).
- **List** – A flexible collection that can hold elements of different types.
- **Function** – A reusable block of code that performs a specific task.
- **Package** – A collection of pre-written R functions and tools (e.g., `dplyr`, `gtsummary`, `ggplot2`).
- **Data Frame** – R's version of a spreadsheet or database table. It organizes data into rows and columns, making it easy to store, manipulate, analyze, and visualize datasets.
- **Control Structures** – Logical structures that determine the order in which code executes, such as loops (`for`, `while`) and conditionals (`if`, `else`).
" %}

{% include question.html header="II. Data Manipulation and Querying" text="

- **Querying** – Extracting specific subsets of data based on defined criteria or conditions.
- **Filtering** – Selecting rows that meet one or more conditions (e.g., `heart rate > 100 BPM`).
- **Subsetting** – Accessing specific rows, columns, or observations from a dataset.
- **Indexing** – Accessing elements using row and column positions or names.
- **Bracket Notation `[ ]`** – Base R method for selecting rows and columns.
- **Logical Indexing** – Using logical conditions (`TRUE`/`FALSE`) to subset data.
- **`dplyr::filter()`** – A convenient function for selecting rows based on conditions.
- **`dplyr::select()`** – Used to choose specific columns from a dataset.
- **Membership Testing (`%in%`)** – Filters observations whose values match one or more values in a specified list.
- **String Operations** – Text-based filtering and transformation using functions such as `grepl()`, `gsub()`, `stringr::str_detect()`, and `stringr::str_replace()`.
- **Conditional Transformation** – Creating new variables based on conditions using `ifelse()` or `dplyr::case_when()`.
" %}

{% include question.html header="III. Data Transformation and Aggregation" text="

- **Grouping (`group_by()`)** – Organizing observations into groups based on one or more variables.
- **Aggregation (`summarise()`)** – Computing summary statistics such as mean, median, count, standard deviation, or percentages for each group.
- **Custom Aggregation** – Applying user-defined calculations to summarize grouped data.
- **Mutating (`mutate()`)** – Creating new variables or transforming existing variables.
- **Sorting (`arrange()`)** – Ordering rows in ascending or descending order based on one or more variables.
- **Pipelining (`|>`, `%>%`)** – Combining multiple data manipulation steps into a streamlined workflow.
- **Chained Operations** – Performing filtering, transformation, aggregation, and sorting in a single sequence of commands.
" %}

{% include question.html header="IV. Data Visualization" text="

- **ggplot2** – The most widely used R package for creating elegant and customizable data visualizations.
- **Base R Graphics** – Built-in plotting functions such as `plot()`, `hist()`, and `boxplot()`.
- **Plot** – A graphical representation of data used to explore patterns and communicate results.
- **Aesthetics (`aes()`)** – Visual properties such as position, color, shape, and size mapped to variables.
- **Histogram** – Displays the frequency distribution of a numeric variable.
- **Box Plot** – Visualizes the distribution of data and highlights potential outliers.
- **Scatter Plot** – Displays the relationship between two numeric variables.
- **Bar Plot** – Represents categorical data using bars.
- **Violin Plot** – Combines box plots and density plots to show the distribution of data.
- **Density Plot** – Visualizes the distribution of a continuous variable.
- **Heatmap** – Displays values using colors, often for correlation matrices or expression data.
- **Pie Chart** – Represents category proportions in a circular chart.
- **Legend** – Identifies the meaning of colors, shapes, or other visual elements.
- **Regression Line** – A fitted line showing the trend or relationship between variables.
- **Faceting** – Creating multiple plots based on levels of a categorical variable.
" %}

{% include question.html header="V. Descriptive and Inferential Statistics" text="

- **Statistics** – The science of collecting, analyzing, interpreting, and presenting data.
- **Descriptive Statistics** – Methods used to summarize and describe the characteristics of a dataset.
- **Inferential Statistics** – Methods used to draw conclusions about a population based on sample data.

### 🔹 **Descriptive Measures**

- **Mean** – The arithmetic average.
- **Median** – The middle value when data are sorted.
- **Mode** – The most frequently occurring value.
- **Range** – Difference between the maximum and minimum values.
- **Standard Deviation (SD)** – Measures how spread out the data are from the mean.
- **Variance** – Square of the standard deviation.
- **Interquartile Range (IQR)** – Difference between the 75th and 25th percentiles.
- **Quartiles** – Values that divide data into four equal parts.
- **Summary Statistics** – A collection of descriptive measures used to characterize a dataset.
" %}

### 🔹 **Inferential Measures**

{% include question.html header="VI. Hypothesis Testing" text="

- **Null Hypothesis (H₀)** – The default assumption that there is **no effect or difference**.
- **Alternative Hypothesis (H₁)** – States that there **is an effect or difference**.
- **p-value** – Probability of observing the data (or more extreme) assuming H₀ is true.
- **Significance Level (`α`)** – Threshold (commonly `0.05`) used to decide whether to reject H₀.
- **Type I Error** – Incorrectly rejecting a true null hypothesis (false positive).
- **Type II Error** – Failing to reject a false null hypothesis (false negative).
- **Statistical Significance** – Evidence that an observed result is unlikely to have occurred by chance alone.
" %}

{% include question.html header="VII. Common Statistical Tests" text="

- **t-test** – Compares means between groups.

    - **One-sample t-test:** compares sample mean to a known population mean.
    - **Independent (two-sample) t-test:** compares means of two independent groups.
    - **Paired t-test:** compares means of the same group before and after a treatment.

- **ANOVA (Analysis of Variance)** – Tests differences among means of three or more groups.

    - **One-way ANOVA:** compares one factor across multiple groups.
    - **Two-way ANOVA:** examines the effect of two factors simultaneously.
    - **Post-hoc tests:** pairwise comparisons following a significant ANOVA result.

- **Chi-Square Test** – Tests relationships between categorical variables.

    - **Test of Independence:** determines if two categorical variables are related.
    - **Goodness of Fit:** checks if observed data match expected distributions.
" %}

{% include question.html header="VIII. Correlation and Regression" text="

- **Correlation** – Measures the strength and direction of a linear relationship between two variables (range: -1 to +1).

    - **Positive correlation:** variables increase together.
    - **Negative correlation:** one increases while the other decreases.

    - **Pearson's r** – The most common correlation coefficient for continuous variables.

- **Regression Analysis** – Predicts the value of a dependent variable based on one or more independent variables.

    - **Simple Linear Regression** – Uses one predictor variable to predict an outcome.

        - **Slope:** change in outcome for every one-unit increase in predictor.
        - **Intercept:** predicted outcome when the predictor is zero.
        - **R-squared:** proportion of variance in the dependent variable explained by the independent variable.

    - **Logistic Regression** – Predicts binary outcomes (e.g., `yes/no`, `0/1`, `Disease/Healthy`) using continuous or categorical predictors.

        - **Odds Ratio:** how much the odds of the outcome change with a one-unit increase in the predictor.
        - **onfusion Matrix:** table showing correct and incorrect predictions.
        - **Accuracy:** proportion of correct predictions.
" %}

{% include question.html header="IX. Data Science Utilities" text="

- **Train-Test Split** – Dividing data into training (for model building) and testing (for evaluation).
- **Random Seed (`set.seed()`)** – Ensures reproducibility of analyses involving randomness.
- **Feature (Predictor Variable)** – An independent variable or predictor in a dataset.
- **Target Variable (Response Variable)** – The dependent variable or outcome being predicted.
- **Normalization / Scaling** – Adjusting data values to a common scale without distorting differences.
- **Standardization** – Transforming data to have a mean of 0 and a standard deviation of 1.
- **Missing Data Handling** – Identifying, removing, or imputing missing values.
- **Reproducibility** – Ensuring analyses can be consistently repeated and verified by others.
" %}

---

## **Getting Started**

Ready to begin your R journey? Let's dive into the fundamentals and start building your programming skills from the ground up. The next section will introduce you to the basic building blocks of R programming.

**Important:** Before the workshop begins, please install **R** and **RStudio** on your laptop. Don't worry — I'll guide you step by step during the first session.

{% include question.html header="Let's install R in your computer!" text="

1. To **download R**, go to [https://cran.r-project.org/](https://cran.r-project.org/). Select your operating system (Windows, macOS, or Linux), download the installer, and follow the default installation steps.
2. To **download Rstudio**, go to [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/). RStudio provides an integrated development environment (IDE) that makes writing, running, and managing R code much easier.
" %}

---

{% capture text %}
This workshop is brought to you by the **Senior Statistician** *(which most times a Data Scientist, sometimes a Bioinformatician, sometimes a Biostatistician)*, of the [Center for Research and Development](https://www.facebook.com/dmsfiCRD), at [Davao Medical School Foundation, Inc.](https://www.facebook.com/DavaoMedical) — committed to empowering medical professionals with the tools of data science, evidence-based research, and digital innovation.{% endcapture %}
{% include alert.html text=text color=secondary %}
