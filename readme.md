# 🏦 The "Credit Risk" Quant Challenge
### *Can you predict who will default when the data is messy and the target is missing?*

---

## 1. Executive Summary
Credit scoring is the backbone of modern banking. It objectively quantifies risk, allowing banks to lend to millions. However, in the startup world, data doesn't come in neat packages. It comes from legacy systems, manual entry forms, and disparate databases.

You are acting as a **Lead Data Scientist for a FinTech startup**. You have been given a raw, messy dump of applicant data and their repayment history. Your task is not just to build a model, but to **clean the data, engineer meaningful features, and define the target variable itself.**

This is not a standard competition dataset. It reflects the reality of financial engineering—where the definition of a "Bad Customer" is something you must construct, and the input data requires significant cleaning before it is usable.

---

## 2. The Objective
Your task is to take these raw files and build a credit scoring model. To do this, you must:

1.  **Integrate Data Sources:** You have two separate files: one for applicant profiles and one for payment history. You must determine the relationship between them.
2.  **Standardize the Data:** The `application_record` comes from multiple legacy sources. You will find inconsistencies in units, formatting, and data types. You must identify and unify them.
3.  **Construct the Label (Vintage Analysis):** The dataset **does not** have a target column. You must use the payment history to define what constitutes a "Default" and map it back to each user.
4.  **Predict:** Build a Classification model to identify high-risk applicants.

---

## 3. Dataset Description

You are provided with two CSV files. You must determine the relationship between them to build your training set.

### File 1: `application_record.csv` (Applicant Profiles)
This file contains personal and financial information about the applicants.

| Data Field | Description |
| :--- | :--- |
| `ID` | Client Number (Unique Identifier) |
| `CODE_GENDER` | Gender |
| `FLAG_OWN_CAR` | Owns a car |
| `FLAG_OWN_REALTY` | Owns property |
| `CNT_CHILDREN` | Number of Children |
| `AMT_INCOME_TOTAL` | Annual Income |
| `NAME_INCOME_TYPE` | Income Category (Salary, Pensioner, etc.) |
| `NAME_EDUCATION_TYPE`| Education Level |
| `NAME_FAMILY_STATUS` | Marital Status |
| `NAME_HOUSING_TYPE` | Living Situation |
| `DAYS_BIRTH` | Age Information |
| `DAYS_EMPLOYED` | Days since employment (Count backwards) |
| `FLAG_WORK_PHONE` | Work phone indicator |
| `FLAG_EMAIL` | Email indicator |
| `OCCUPATION_TYPE` | Job Title |
| `CNT_FAM_MEMBERS` | Family Size |

### File 2: `credit_record.csv` (Payment History)
This file contains the monthly repayment status for the applicants.

| Data Field | Description |
| :--- | :--- |
| `ID` | Client Number |
| `MONTHS_BALANCE` | Record Month (`0` = Current, `-1` = Previous, etc.) |
| `STATUS` | Payment Status (Codes listed below) |

**Status Codes Legend:**
* `C`: Paid off that month
* `X`: No loan for the month
* `0`: 1-29 days past due
* `1`: 30-59 days past due
* `2`: 60-89 days past due
* `3`: 90-119 days past due
* `4`: 120-149 days past due
* `5`: Overdue/Bad Debt (>150 days)

---

## 4. Key Challenges to Solve

We are not telling you *how* to process the data, but your model will fail if you do not address these core questions during your EDA (Exploratory Data Analysis):

1.  **Data Consistency:** Are numerical columns actually numerical? Or do they contain noise from manual entry?
2.  **The "Default" Definition:** A customer who is 1 day late "Bad."? At what point do you classify a customer as a defaulter? You must define this logic.
3.  **Categorical Noise:** Are the categories in some columns unique, or are there synonyms that need grouping?
4.  **Class Imbalance:** In finance, defaults are rare events. How will you ensure your model doesn't just predict "Good" for everyone to get a high accuracy score?

---

## 5. Judging Criteria

Evaluation will be based on the robustness of your pipeline, not just the final accuracy score.

| Metric | Description |
| :--- | :--- |
| **Data Munging** | Did you identify the anomalies in the raw text/numbers? Is your parsing logic robust? |
| **Feature Engineering** | Did you extract meaningful financial ratios (e.g., Income per Family Member) or demographic bins? |
| **Target Construction** | How did you define the "Bad" label using the history file? Is your logic sound? |
| **Modeling Strategy** | How did you handle the class imbalance? Did you optimize for the right metric (Recall/F1 vs Accuracy)? |

---

## 6. Submission Requirements

You must submit a **Jupyter Notebook** (`.ipynb`) containing:

1.  **EDA & Cleaning Log:** A section demonstrating the inconsistencies you found in the application data and how you fixed them.
2.  **Target Construction Code:** Code showing how you aggregated the history file to create the `Target` label.
3.  **Modeling & Evaluation:** Your training process and final metrics (Confusion Matrix, F1-Score).

---

### 💡 Pro-Tips for Participants
* **Investigate Data Types:** Don't assume a column is an integer just because it looks like one. Check for hidden strings or formatting issues.
* **Define "Bad" Carefully:** A common banking standard for default is **overdue by 60+ days**. Use this as a starting point for your label construction.
* **The "Accuracy Paradox":** If 98% of users are good, a model that predicts "Good" for everyone has 98% accuracy but is useless. Focus on catching the bad guys (Recall).