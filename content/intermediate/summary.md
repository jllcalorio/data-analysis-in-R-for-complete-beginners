---
section_id: Intermediate R
nav_order: 7
title: Summary
topics: summary, next steps
---

# **Congratulations!** 

You've completed the Intermediate R section and significantly expanded your programming capabilities. Let's review what you've accomplished:

# **What You’ve Mastered**

{% include question.html header="Advanced Functions" text="

- Handled parameters with default values and the `...` ellipsis for variable-length arguments
- Used **anonymous functions** (`\\(x) ...`) and higher-order functions (`Filter`, `Map`, sappl`y)
- Added **comments** and **documentation** for clarity
- Designed **clean, reusable, well-structured** functions
" %}

{% include question.html header="Packages and Scripts" text="

- Imported and organized code effectively using `library()` and `source()`
- Used **built-in base R functions** (e.g., math, date/time, file utilities)
- Created **custom scripts** for reuse across projects
- Called specific package functions with the `::` operator
- Followed best practices for **readable and testable** code
" %}

{% include question.html header="Error Handling" text="

- Understood **common condition types** (errors, warnings, messages)
- Used `tryCatch()` and `finally` for controlled error management
- Defined **custom conditions** for domain-specific use cases
- Practiced **debugging and robust programming** techniques
" %}

# **Real-World Applications You Built**

{% include question.html header="Through the exercises, you've built:" text="

- **BMI Calculator** – a simple script (`bmi_calculator.R`) that computes **Body Mass Index (BMI)**
- **Medication Dosage Calculator** – a function that calculates a child's **drug dosage** based on weight
- **Heart Rate Evaluator** – a function that classifies a **resting heart rate**
" %}

# **Key Programming Principles You Now Understand:**

{% include question.html header="Code Organization" text="

- Break big problems into smaller, logical **functions**
- Group related logic into **scripts** and eventually **packages**
- Use `if (sys.nframe() == 0)` to protect self-test blocks in sourced files
" %}

{% include question.html header="Error Prevention and Handling" text="

- Anticipate and validate inputs
- Provide **clear, actionable error messages**
- Catch specific conditions with `tryCatch()` instead of generic handlers
" %}

{% include question.html header="Professional Practices" text="

- Add **inline comments** explaining purpose and assumptions
- Follow **snake_case naming conventions**
- Write simple **test calls** for critical functions
" %}

# **What You Can Build Now**

{% include question.html header="Intermediate Applications" text="

- Multi-file **R programs** with good structure
- Programs that handle files and user input safely
- **Utility scripts** that others can `source()` and use
- Apps with **graceful error handling** and informative output
" %}

{% include question.html header="Next Steps" text="

You're ready for Data Analysis with R, where you'll apply these skills to real-world datasets using powerful packages like:

- `dplyr` — for data manipulation
- `ggplot2` — for visualization
- `tidyr` — for reshaping data
- Base R statistics and `stats` package — for hypothesis testing
" %}

# **Next Steps:**

The foundation you've built here will serve you well as we move into Data Analysis with R, where you'll apply these skills to real-world data problems using powerful packages like `dplyr`, `ggplot2`, and `stats`.

{% capture text %}
**Remember:**

The best way to master R is through consistent practice.

Type out the examples.

Experiment with your own variations.

Break your code. Fix it. Learn from it.

Every function you write strengthens your foundation.
{% endcapture %}
{% include alert.html text=text color=secondary %}