# credit-risk-modeling-fintech-challenge
Credit risk prediction project using messy real‑world data. Includes cleaning, feature engineering, target creation from repayment history, SMOTE balancing, and ML models (RF, XGBoost, LightGBM).
# 🏦 Credit Risk Modeling – FinTech Challenge 🚀

Predicting which customers are likely to default is one of the most crucial problems in modern banking.  
This project replicates a **real-world FinTech workflow**: dealing with messy data, defining the target from scratch, balancing extreme class imbalance, and training strong ML models.

---

## 📂 Project Overview

This repository contains:

- 🔄 **Data Cleaning & Preprocessing**  
- 🧩 **Feature Engineering** (age, employment features, cleaned flags, etc.)  
- 🎯 **Target Construction** from `credit_record.csv` using repayment history  
- ⚖️ **Handling Class Imbalance** using SMOTE  
- 🤖 **Machine Learning Models**  
  - Random Forest  
  - XGBoost  
  - LightGBM  
- 📊 **Evaluation Metrics**  
  - Accuracy  
  - Recall (priority for catching defaulters)  
  - Confusion Matrix  
  - Classification Report  

---

## 📁 Dataset Files

### `application_record.csv`
Contains demographic + financial details such as:
- Gender, education, income type  
- Income, children count  
- Employment duration  
- Housing and family status  

### `credit_record.csv`
Contains:
- Monthly credit repayment logs  
- STATUS codes (0, 1, ..., 5, C, X)  
- MONTHS_BALANCE timeline  

---

## 🧠 Target Definition (BAD_FLAG)

A customer is labeled **BAD_FLAG = 1** if they have ever had:
- STATUS `2`, `3`, `4`, or `5`  
(60+ days overdue → default)

Otherwise:
- **BAD_FLAG = 0**

---

## ⚙️ Techniques Used

- ✔️ Merging datasets via ID  
- ✔️ Cleaning inconsistent text & categorical values  
- ✔️ Encoding categorical columns  
- ✔️ Train/validation/test split  
- ✔️ SMOTE oversampling for minority class  
- ✔️ Hyperparameter tuning for ML models  

---

## 🏆 Model Performance (Highlights)

- **LightGBM achieved best recall on test set: ~0.81**
- Accuracy ≈ 0.97 across models
- Significant improvement over baseline using SMOTE + tuned models

---

## 📈 Outputs

The final notebook generates:

- Default probability (`DEFAULT_PROB`)  
- Ranked risk list for all customers  
- Plots and confusion matrices  
- Full pipeline ready for deployment  

---

## 👨‍💻 Contributors

| Name | Role |
|------|------|
| **Aaditya** | Lead Data Scientist / Project Owner |
| **Dev Gandhi** | Contributor |
| **Rishi Selam** | Contributor |

💙 Thank you all for collaborating!

---

## 🚀 How to Run

1. Clone the repo  
   ```bash
   git clone https://github.com/yourusername/credit-risk-modeling-fintech-challenge.git
