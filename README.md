# 🎓 Course Completion Prediction Using R

### 📊 Statistical Modeling | Predictive Analytics | Educational Data Science

![R](https://img.shields.io/badge/Language-R-276DC3?logo=r&logoColor=white) ![Statistics](https://img.shields.io/badge/Focus-Statistical%20Modeling-4B8BBE) ![Machine Learning](https://img.shields.io/badge/Focus-Predictive%20Analytics-2E8B57) ![Status](https://img.shields.io/badge/Status-Academic%20Project-blue)

## 📌 Project Overview

This project explores **student course completion prediction** using statistical inference, feature engineering, and classification models in **R**. The analysis investigates how learner engagement, academic performance, course characteristics, and activity patterns relate to course completion, then compares predictive approaches on a held-out test set.

The target variable is **`Completed`**, converted in the script to the binary variable `Completed_num` (1 for `Completed` or `Complete`; 0 otherwise).

## 🎯 Objectives

- 🧹 Inspect and preprocess student course records, including duplicate and missing-value checks.
- 📈 Explore completion patterns and key learning-engagement indicators.
- 🧪 Apply statistical hypothesis tests to examine relationships between variables.
- 🧠 Build and compare classification models for course completion.
- 🔎 Evaluate feature selection, regularization, and dimensionality reduction.
- 🎛️ Explore Bayesian decision thresholds for classification.

## 🗂️ Dataset

**File:** `Course_Completion_Prediction.csv`

The dataset contains student, course, activity, and performance fields, including:

| Category | Example variables |
|---|---|
| 👤 Student characteristics | `Age`, `Gender`, `Education_Level`, `Employment_Status` |
| 📚 Course information | `Category`, `Course_Level`, `Course_Duration_Days` |
| ⏱️ Engagement | `Time_Spent_Hours`, `Days_Since_Last_Login`, `Video_Completion_Rate`, `App_Usage_Percentage` |
| 📝 Performance | `Quiz_Score_Avg`, `Project_Grade`, `Progress_Percentage`, `Assignments_Missed` |
| 🎯 Outcome | `Completed` |

> **Data note:** The CSV also includes student identifiers and names. Review the dataset's provenance, consent, and sharing permissions before publishing it publicly. If it contains real student information, anonymize or exclude identifying fields.

## 🛠️ Technologies and Libraries

- **R** — statistical computing and predictive modeling
- **readr** — data import utilities
- **dplyr** — data cleaning and transformation
- **ggplot2** — data visualization
- **leaps** — best subset selection
- **glmnet** — LASSO, Ridge, and Elastic Net regression
- **e1071** — Naïve Bayes classification
- **arm** — Bayesian-style regularized logistic regression via `bayesglm()`

## 🔄 Project Workflow

### 1. 🧹 Data Preprocessing

- Check and remove duplicate observations.
- Examine missing values and their percentages.
- Convert categorical predictors to factors.
- Remove selected administrative fields from modeling data.
- Encode the course completion outcome as a binary variable.

### 2. ⚙️ Feature Engineering

The script creates additional predictors:

| Engineered feature | Definition |
|---|---|
| `Total_Engagement_Score` | `Time_Spent_Hours × (Video_Completion_Rate / 100)` |
| `Inactivity_Penalty_Ratio` | `Days_Since_Last_Login / (Progress_Percentage + 1)` |
| `Paid_Engagement` | 1 if `Payment_Amount > 0`, otherwise 0 |

### 3. 📊 Exploratory Data Analysis

The script examines:

- Course completion distribution (bar chart)
- Time spent by completion status (boxplot)
- Average quiz score distribution (histogram)
- Mean and standard deviation of time spent and quiz scores

### 4. 🧪 Statistical Hypothesis Testing

The analysis includes:

| Test | Purpose |
|---|---|
| Two-sample t-test | Compare time spent between completion groups |
| One-way ANOVA | Compare quiz scores across course levels |
| Chi-square tests | Examine completion associations with gender, employment status, and device type |
| F-test for variances | Compare variability in time spent across completion groups |

### 5. 🤖 Predictive Modeling and Model Selection

The script uses a **70% training / 30% testing split** with `set.seed(123)` and implements:

1. **Logistic Regression** — binary completion prediction.
2. **Best Subset Selection** — exhaustive predictor subset exploration using BIC.
3. **Forward and Backward Selection** — stepwise predictor selection.
4. **LASSO Regression** — L1-regularized logistic regression.
5. **Ridge Regression** — L2-regularized logistic regression.
6. **Elastic Net** — combined L1/L2 regularization.
7. **Naïve Bayes** — probabilistic classification.
8. **Bayesian-Style Logistic Regression** — regularized logistic modeling using `arm::bayesglm()`.

Regularized models use cross-validation to select the penalty parameter (`lambda.min`).

### 6. 📉 Principal Component Analysis (PCA)

PCA is applied to selected numerical engagement and performance predictors using standardized inputs (`scale. = TRUE`). The script reports component summaries and produces a variance plot.

### 7. 📏 Model Evaluation and Decision Thresholds

The script calculates **confusion matrices** and **test-set classification accuracy** for its predictive models. It also explores Bayesian classification thresholds from **0.30 to 0.70**, in increments of **0.05**.

> **Results:** Model accuracy values are computed when the R script is executed; this README intentionally does not claim specific results without verified execution output. Threshold selection on the test set is exploratory and should use a separate validation set for an unbiased final evaluation.


## 🚀 Getting Started

### Prerequisites

Install [R](https://cran.r-project.org/) and optionally [RStudio](https://posit.co/download/rstudio-desktop/).

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/Course-Completion-Prediction-Using-R.git
cd Course-Completion-Prediction-Using-R
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Install required packages

```r
install.packages(c("readr", "dplyr", "ggplot2", "leaps", "glmnet", "e1071", "arm"))
```

### 3. Verify the dataset filename

The original script uses:

```r
student_data <- read.csv("student_course_completion_prediction.csv")
```

If you keep the uploaded CSV filename, change that line to:

```r
student_data <- read.csv("Course_Completion_Prediction.csv")
```

Keep the script and CSV in the same working directory, or provide the correct relative path.

### 4. Run the analysis

Open `Course_Completion_Prediction.R` in RStudio and run the script, or run it from the repository directory:

```bash
Rscript Course_Completion_Prediction.R
```

The script prints statistical test outputs, model summaries, confusion matrices, and accuracy measurements, and produces visualizations.

## 💡 Practical Applications

- 🎓 Identify patterns associated with course completion.
- 📚 Support learning analytics and educational research.
- 📉 Investigate indicators associated with student disengagement.
- 🧠 Compare statistical and machine-learning methods on educational data.

## ⚠️ Limitations and Future Improvements

- Review missing-value handling before fitting models; the current script checks missingness but does not implement a full imputation pipeline.
- Investigate potential **target leakage**: variables such as `Progress_Percentage` or `Video_Completion_Rate` may reflect outcomes measured late in a course. Their suitability depends on when predictions are intended to be made.
- Consider stratified splitting, repeated cross-validation, and a separate validation set for threshold tuning.
- Extend evaluation with precision, recall, F1-score, and ROC-AUC, particularly if the classes are imbalanced.
- Review privacy and sharing permissions before publishing student-level records.





---

