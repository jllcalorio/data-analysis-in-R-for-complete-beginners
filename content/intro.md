---
nav_order: 1
title: Introduction
---

Welcome to this beginner-friendly workshop designed especially for medical students and healthcare professionals. Over three immersive days, you’ll learn Python from the ground up — not just as a programming language, but as a practical tool for analyzing clinical and research data.

---

{% include question.html header="Workshop Overview" text="

Python has become one of the most widely used languages in healthcare research and medical informatics. From analyzing patient data and visualizing disease trends to supporting AI-based diagnostics, Python is transforming how health professionals handle data.

This workshop provides a **hands-on, structured approach to learning Python fundamentals and applying them to real-world medical and research datasets**.
" %}

{% include question.html header="Duration & Format" text="
- **Duration**: 3-day intensive workshop
- **Format**: Hands-on learning with practical exercises
- **Schedule**: October 2025
- **Delivery**: Interactive sessions with live coding demonstrations
" %}

---

## Learning Objectives

By the end of this workshop, participants will be able to:

{% include question.html header="Technical Skills" text="
- **Handle Data Effectively:** Organize and manage patient or laboratory data using Python’s built-in structures
- **Perform Data Analysis:** Use ```pandas``` to explore health-related datasets and compute descriptive statistics
- **Create Visualizations:** Generate charts for patient outcomes, clinical trials, or epidemiological trends
- **Perform Statistical Tests:** Apply tests such as *```t-test```*, *```ANOVA```*, *```chi-square```*, and *```logistic regression```* tests to biomedical datasets
- **Build a Foundation:** Prepare for advanced applications like biostatistics, machine learning, and clinical decision support
" %}

{% include question.html header="Practical Applications" text="
- **Read and process** data from various file formats
- **Filter and query** datasets to extract meaningful insights
- **Perform statistical tests** (t-tests, ANOVA, chi-square, logistic regression)
- Create professional **data visualizations**
- **Build a foundation** for advanced Python applications
" %}
---

## Target Audience

This workshop is specially designed for DMSFI students and healthcare professionals who are ready to explore how programming and data can enhance medical decision-making, research, and innovation.

{% include question.html header="Primary Audience" text="
- **Students** in the Davao Medical School Foundation, Inc.
- **Complete beginners** with no prior programming experience
- **Professionals** looking to add Python skills to their toolkit
- **Researchers** who need to analyze data programmatically
" %}

{% include question.html header="Prerequisites" text="
- **No programming experience required** - we start from the very basics
- **Basic computer literacy** (file management, using applications)
- **Willingness to learn** and practice hands-on coding
- **A laptop with internet connection** for installation and practice
" %}

{% include question.html header="Who Will Benefit Most" text="
- **Medical professionals** aiming to integrate data science into clinical practice or research
- **Medical students** preparing for coursework or electives involving biostatistics, informatics, or computational tools
- **Clinicians and researchers** seeking to enhance decision-making through data-driven approaches
- **Healthcare professionals** curious about programming, data analysis, and their applications in medicine
" %}
---

## Expected Outcomes

{% include question.html header="Immediate Skills (End of Workshop)" text="
- Confidently **write basic to intermediate** Python programs
- **Understand and apply** fundamental programming concepts
- Perform basic **data manipulation and analysis tasks**
- Create **simple visualizations** from datasets
" %}

{% include question.html header="Long-term Benefits: Clinical & Research Impact" text="
- **Data-Driven Insight**: Confidently explore and interpret clinical or survey data
- **Research Independence**: Perform your own data cleaning and analysis for publications
- **Problem-Solving**: Develop computational thinking skills
- **Foundation Building**: Prepared for advanced topics like machine learning
- **Automation in Practice**: Streamline repetitive workflows, such as summarizing lab data or generating reports
" %}

{% include question.html header="Practical Projects" text="
By workshop completion, you'll have created:
- A personal library of useful Python functions
- Mini-projects analyzing sample clinical datasets (e.g., patient demographics, vital signs, or lab results)
- Solutions to data-driven questions often encountered in healthcare and research
- A foundation for continued learning and development
" %}
---

## Workshop Structure

{% include question.html header="Day 1: Foundation Building" text="
- Python basics and development environment setup
- Variables, data types, and basic operations
- Introduction to programming logic
" %}

{% include question.html header="Day 2: Building Complexity" text="
- Control structures and functions
- Working with modules and handling errors
- Hands-on practice with increasingly complex problems
" %}

{% include question.html header="Day 3: Real-World Application" text="
- Data analysis with pandas
- Statistical analysis and visualization
- Capstone project and wrap-up
" %}
---

## What You'll Take Away

{% include question.html header="Skills Portfolio" text="
- Comprehensive understanding of Python fundamentals
- Experience with industry-standard data analysis tools
- Portfolio of completed programming projects
- Confidence to tackle new programming challenges
" %}

{% include question.html header="Resources for Continued Learning" text="
- Complete workshop materials and code examples
- Recommended resources for further study
- Clear pathways for advancing your Python skills
" %}

{% include question.html header="Certificate of Completion" text="
Participants who complete all workshop activities will receive a **Certificate of Completion in \"Data Analysis in Python for Complete Beginners,\"** issued by the Center for Research and Development, DMSFI.
" %}
---

## Definition of Terms

{% include question.html header="I. Programming and Data Basics" text="
- **Variable** – A named container used to store data values in a program.
- **Data Type** – The classification of data that tells Python what kind of value is being stored (e.g., ```integer```, ```float```, ```string```, ```boolean```).
- **List** – An ordered, mutable collection of items (e.g., ```[10, 20, 30]```).
- **Dictionary** – A collection of key-value pairs (e.g., ```{'name': 'John', 'age': 30}```).
- **Function** – A reusable block of code that performs a specific task.
- **Module / Library** – A collection of pre-written Python functions and tools (e.g., ```numpy```, ```pandas```, ```matplotlib```).
- **DataFrame** – A two-dimensional, labeled data structure in ```pandas``` similar to an Excel spreadsheet, with rows and columns.
- **Series** – A one-dimensional labeled array (e.g., a single column of a DataFrame).
- **Control Structures** – Logical structures that determine the order in which code executes, such as **loops** (```for```, ```while```) and **conditionals** (```if```, ```else```).
" %}

{% include question.html header="II. Data Querying and Selection" text="
- **Querying** – Extracting specific subsets of data based on certain criteria or conditions.
- **Filtering** – Selecting rows or columns in a dataset that meet a particular condition (e.g., heart rate greater than 100 BPM).
- **Indexing** – Accessing data using row or column labels or positions.
- **iloc** – Index-based selection (integer position).
- **loc** – Label-based selection (using column or row names).
- **Boolean Masking** – Using logical conditions (```True```/```False```) to filter data.
- **```isin()``` Function** – Filters rows where a column’s value matches any in a given list.
- **String Operations** – Text-based filters or transformations (e.g., ```str.contains()``` to find names with a certain substring).
- **```query()``` Method** – A more readable way to filter data using string expressions (e.g., ```df.query('age > 30 and heart_rate > 100')```).
" %}

{% include question.html header="III. Data Transformation and Aggregation" text="
- **Grouping (```groupby```)** – Combining rows with the same value in one or more columns to perform summary calculations.
- **Aggregation** – Calculating summary statistics such as ```mean```, ```median```, ```count```, or ```standard deviation``` for each group.
- **Custom Aggregation** – User-defined summary functions applied to groups (e.g., ```calculating body mass index```).
- **Sorting** – Arranging rows in ascending or descending order based on column values.
- **Chained Operations** – Combining multiple DataFrame methods in a single line (e.g., filtering → sorting → selecting).
" %}

{% include question.html header="IV. Data Visualization" text="
- **Matplotlib** – A powerful Python library for creating static, 2D plots like ```histograms```, ```scatter plots```, and ```bar charts```.
- **Seaborn** – A visualization library built on ```Matplotlib``` that simplifies statistical plotting with cleaner aesthetics.
- **Figure** – The entire plotting area that may contain one or more subplots.
- **Axes / Subplot** – Individual plots within a figure.
- **Histogram** – Displays the frequency distribution of a numeric variable.
- **Box Plot** – Visualizes data spread and detects outliers using quartiles.
- **Scatter Plot** – Shows relationships or correlations between two numeric variables.
- **Bar Plot** – Represents categorical data using rectangular bars.
- **Violin Plot** – Combines box plot and density plot to show data distribution.
- **Heatmap** – Displays a color-coded correlation matrix or table of values.
- **Pie Chart** – Represents proportions of categories in a circular chart.
- **Legend** – A key that identifies what each color or symbol represents in a plot.
- **Regression Line** – A line that shows the general trend in scatter plot data (e.g., using ```sns.regplot```).
" %}

{% include question.html header="V. Descriptive and Inferential Statistics" text="
- **Statistics** – The branch of mathematics dealing with the collection, analysis, interpretation, and presentation of data.
- **Descriptive Statistics** – Summarize data features without drawing conclusions beyond the data itself.
- **Inferential Statistics** – Use sample data to make generalizations about a larger population.

**🔹 Descriptive Measures**

- **Mean** – The arithmetic average.
- **Median** – The middle value when data are sorted.
- **Mode** – The most frequently occurring value.
- **Range** – Difference between the maximum and minimum values.
- **Standard Deviation (SD)** – Measures how spread out the data are from the mean.
- **Variance** – Square of the standard deviation.
- **Interquartile Range (IQR)** – Difference between the 75th and 25th percentiles.
" %}

{% include question.html header="VI. Hypothesis Testing" text="
- **Null Hypothesis (H₀)** – The default assumption that there is **no effect or difference**.
- **Alternative Hypothesis (H₁)** – States that **we fail to reject the null hypothesis**.
- **p-value** – Probability of observing the data (or more extreme) assuming H₀ is true.
- **Significance Level (α)** – Threshold (commonly ```0.05```) used to decide whether to reject H₀.
- **Type I Error** – Incorrectly rejecting a true null hypothesis (false positive).
- **Type II Error** – Failing to reject a false null hypothesis (false negative).
" %}

{% include question.html header="VII. Common Statistical Tests" text="
- **T-test** – Compares means between groups.
  - *One-sample t-test:* compares sample mean to a known population mean.
  - *Independent (two-sample) t-test:* compares means of two independent groups.
  - *Paired t-test:* compares means of the same group before and after a treatment.
- **ANOVA (Analysis of Variance)** – Tests differences among means of three or more groups.
  - *One-way ANOVA:* compares one factor across multiple groups.
  - *Two-way ANOVA:* examines the effect of two factors simultaneously.
  - *Post-hoc tests:* pairwise comparisons following a significant ANOVA result.
- **Chi-Square Test** – Tests relationships between categorical variables.
  - *Test of Independence:* determines if two categorical variables are related. This is usually the case.
  - *Goodness of Fit:* checks if observed data match expected distributions. This is when we have a theoretical distribution or percentages.
" %}

{% include question.html header="VIII. Correlation and Regression" text="
- **Correlation** – Measures the strength and direction of a linear relationship between two variables (range: -1 to +1).
  - *Positive correlation:* variables increase together.
  - *Negative correlation:* one increases while the other decreases.
- **Pearson’s r** – The most common correlation coefficient for continuous variables.
- **Regression Analysis** – Predicts the value of a dependent variable based on one or more independent variables.
- **Simple Linear Regression** – Uses one predictor variable to predict an outcome.
  - *Slope:* change in outcome for every one-unit increase in predictor.
  - *Intercept:* predicted outcome when the predictor is zero.
  - *R-squared:* proportion of variance in the dependent variable explained by the independent variable.
- **Logistic Regression** – Predicts binary outcomes (e.g., ```yes/no```, ```0/1```) using continuous or categorical predictors.
  - *Odds Ratio:* how much the odds of the outcome change with a one-unit increase in the predictor.
  - *Confusion Matrix:* table showing correct and incorrect predictions.
  - *Accuracy:* proportion of correct predictions.
" %}

{% include question.html header="IX. Data Science Utilities" text="
- **Train-Test Split** – Dividing data into training (for model building) and testing (for evaluation).
- **Random Seed** – Ensures reproducibility by fixing random number generation.
- **Feature** – An independent variable or predictor in a dataset.
- **Target Variable** – The dependent variable or outcome being predicted.
- **Normalization / Scaling** – Adjusting data values to a common scale without distorting differences.
" %}
---

## Getting Started

Ready to begin your Python journey? Let's dive into the fundamentals and start building your programming skills from the ground up. The next section will introduce you to the basic building blocks of Python programming.

**Important**: Before the workshop begins, please install **Python** and **Anaconda** on your laptop. Don’t worry — I’ll guide you step by step during the first session.

{% include question.html header="Let's install Python in your computer!" text="
1. To **download Python**, go to [https://www.python.org/downloads/](https://www.python.org/downloads/) and click '**Download Python x.xx.x**'. There are separate download options depending on your operating system (OS), example, Windows, macOS, Linux, etc. Double-click the downloaded file and follow the default options for installation.
2. To **download Anaconda**, go to [https://www.anaconda.com/download/success](https://www.anaconda.com/download/success) and click one of the options under \"**Distribution Installers**\". Once download is finished, double-click the downloaded file and follow the default options for installation.
  - Anaconda is a free and open-source distribution of the Python and R programming languages for scientific computing. It simplifies package management and deployment, making it the standard choice for data science.

Once installed, open **Anaconda Navigator**, find **Jupyter Notebook**, and click **Launch** — you’re ready to code!
" %}
---

{% capture text %}
This workshop is brought to you by the **Senior Statistician** *(which most times a Data Scientist, sometimes a Bioinformatician, sometimes a Biostatistician)*, of the [Center for Research and Development](https://www.facebook.com/dmsfiCRD), at [Davao Medical School Foundation, Inc.](https://www.facebook.com/DavaoMedical) — committed to empowering medical professionals with the tools of data science, evidence-based research, and digital innovation.{% endcapture %}
{% include alert.html text=text color=secondary %}
