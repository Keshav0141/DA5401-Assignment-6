# DA5401-Assignment-6 — Imputation via Regression for Missing Data
- **Name:** Aryan Prasad  
- **Roll No:** DA25M007  

---

## Overview

This project focuses on **handling missing data through regression-based imputation** and evaluating its impact on model performance using the **UCI Credit Card Default Dataset**.  
Artificial **Missing At Random (MAR)** values were introduced to simulate real-world data issues, and multiple imputation strategies were compared against each other and listwise deletion.

The objectives are to:
- Analyze how imputation techniques affect classification outcomes  
- Compare **data retention (imputation)** vs **data loss (deletion)** approaches  
- Evaluate whether **linear or non-linear regression** produces better imputations  

The notebook integrates **data preprocessing**, **statistical reasoning**, **model evaluation**, and **visual analysis** to assess how missing value treatment influences predictive stability and fairness.

---

## Dataset Description

- **Dataset:** UCI Credit Card Default Clients Dataset (via Kaggle)  
- **Records:** 30,000  
- **Features:** 23 predictors (demographics, payment history, bill amounts, etc.)  
- **Target:** `default.payment.next.month` (Binary: 1 = Default, 0 = Non-default)  
- **Artificial Missingness:**  
  - Introduced **5–10% MAR missing values** in:
    - `AGE`
    - `BILL_AMT1`
    - `PAY_AMT1`

---

## Key Techniques and Workflow

### **Part A — Data Preprocessing and Imputation**
- Introduced MAR-type missing values (5–10%) in selected numerical features.  
- Constructed four datasets representing different strategies:
  1. **Dataset A — Median Imputation (Baseline)**  
  2. **Dataset B — Linear Regression Imputation**  
  3. **Dataset C — Decision Tree (Non-linear) Imputation**  
  4. **Dataset D — Listwise Deletion (Row Removal)**  
- Standardized all datasets using `StandardScaler`.  
- Visualized before/after imputation distributions for the affected columns to assess bias.

---

### **Part B — Model Training and Evaluation**
- Trained **Logistic Regression** models on each imputed dataset.  
- Splitted data into 70% training and 30% testing with stratified sampling.  
- Applied consistent preprocessing and evaluation metrics across all datasets.

**Evaluation Metrics**
- Accuracy  
- Precision  
- Recall  
- F1-score  
- ROC–AUC  
- PR–AUC  

**Visualizations**
- AGE Distributions — Before vs After Imputation  
- Bar Charts — Precision, Recall, F1 (Class 0 and Class 1)  
- ROC and Precision–Recall Curves  
- AUC Comparison Charts  

---

## Part C — Comparative Analysis

### **C.1 Results Comparison**

| Model | Precision (Class 1) | Recall (Class 1) | F1 | ROC AUC | PR AUC |
|:--|:--:|:--:|:--:|:--:|:--:|
| Dataset A (Median) | 0.70 | 0.24 | 0.35 | 0.714 | 0.497 |
| Dataset B (Linear Regression) | 0.70 | 0.24 | 0.35 | 0.715 | 0.498 |
| Dataset C (Decision Tree) | 0.69 | 0.24 | 0.35 | 0.715 | 0.498 |
| Dataset D (Listwise Deletion) | **0.72** | **0.23** | **0.36** | **0.721** | **0.501** |

**Key Findings**
- All models perform almost identically — missing value handling had minimal effect.  
- Listwise Deletion shows slightly higher AUC but only because of reduced sample size.  
- Recall for defaulters remains low (~0.23), showing that **class imbalance** dominates model behavior, not imputation strategy.  
- Linear and non-linear imputations yield almost identical results, implying weak feature dependence for the missing variable (`AGE`).

---

### **C.2 Efficacy Discussion**

- **Median Imputation:** Fast and robust against outliers, but ignores inter-feature relationships.  
- **Linear Regression Imputation:** Preserves correlations, simple to interpret, and statistically sound under MAR assumption.  
- **Decision Tree Imputation:** Captures non-linear patterns but shows no gain here since missingness is limited and relationships are mostly linear.  
- **Listwise Deletion:** Reduces dataset by 22%; inflates accuracy due to smaller, cleaner subset but loses valuable information and generalizability.  

**Interpretation**
- All models show that imputation strategy has minimal impact on final accuracy (~0.81).  
- The biggest limitation is **class imbalance**, which suppresses recall for defaulters.  
- Deletion leads to **biased sampling**, while imputation retains representativeness.  

**Conclusion**
- **Regression-based imputation** (Linear or Decision Tree) retains information and avoids unnecessary data loss.  
- For small MAR missingness, **Linear Regression Imputation (Dataset B)** is the most balanced and interpretable choice.  
- The model’s main weakness is imbalance in the target class — not the imputation method.

---

## Theoretical Background

This project covers:
- The concept of **Missing At Random (MAR)** and its implications for data preprocessing.  
- The role of **Logistic Regression** in binary classification tasks.  
- Evaluation metrics for **imbalanced classification problems**.  
- How imputation affects statistical variance, correlation, and overall data stability.  

---

## Results Summary

| Metric | Observation |
|:--|:--|
| **ROC AUC (All Imputations)** | ≈ 0.71 — Moderate discrimination |
| **PR AUC (All Imputations)** | ≈ 0.50 — Weak minority class detection |
| **Median vs Regression** | Nearly identical outcomes |
| **Listwise Deletion** | Slightly inflated results due to smaller dataset |
| **Recall (Class 1)** | Low (~0.23) — driven by class imbalance |

---

## Insights and Recommendations

- **Impact of Missing Data:**  
  Small MAR missingness (<10%) barely affects model performance.  
- **Avoid Deletion:**  
  Listwise deletion discards valuable samples and can bias results.  
- **Regression Imputation:**  
  Linear regression is computationally efficient and retains relationships.  
- **Future Improvements:**  
  - Address class imbalance via **SMOTE**, **ADASYN**, or **class weights**  
  - Use advanced models like **XGBoost** or **Random Forest** for higher recall 

---

## Final Summary

This assignment demonstrates that:
- **Regression-based imputation** maintains dataset completeness without performance degradation.  
- **Listwise Deletion** causes unnecessary data loss and potential bias.  
- Model weakness arises from **class imbalance**, not missing value treatment.  
- For small MAR missingness, **Linear Regression Imputation (Dataset B)** is the most effective and interpretable approach.  

> ✅ **Key Takeaway:**  
> Data imputation should prioritize **information retention** and **distribution integrity** — not just data cleaning —  
> ensuring that predictive models remain both accurate and fair.
