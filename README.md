# DA5401-Assignment-6 Imputation via Regression for Missing Data
- Name: Aryan Prasad  
- Roll No: DA25M007  

---

## Overview

This project investigates **missing data imputation strategies** and their impact on classification performance using the **UCI Credit Card Default Dataset**.  
The analysis introduces **Missing At Random (MAR)** values and compares four distinct approaches to handle incomplete data, evaluating their influence on predictive accuracy and reliability.

The objective is to understand:
- How different imputation methods affect model performance  
- The trade-offs between **data deletion** and **data retention**  
- Which regression-based imputation (Linear vs. Non-linear) better preserves information  

The notebook integrates **statistical reasoning**, **data visualization**, and **model evaluation metrics** to assess real-world implications of imputation.

---

## Dataset Description

- **Dataset:** UCI Credit Card Default Clients Dataset  
- **Samples:** 30,000  
- **Features:** 23 numerical and categorical predictors  
- **Target:** `default.payment.next.month` (Binary: 1 = Default, 0 = Non-default)  
- **Artificial Missingness:**  
  - 5% MAR introduced into `AGE` and `BILL_AMT` columns  

---

## Key Techniques and Workflow

### **Part A — Data Preprocessing and Imputation**
- Loaded dataset and introduced 5% MAR missing values.  
- Created four derived datasets:
  1. **Dataset A — Median Imputation (Baseline)**  
  2. **Dataset B — Linear Regression Imputation**  
  3. **Dataset C — Decision Tree (Non-linear) Imputation**  
  4. **Dataset D — Listwise Deletion (Row Removal)**  
- Standardized all features using `StandardScaler`.  
- Compared the distribution of imputed columns before and after imputation using frequency plots.

---

### **Part B — Model Training and Evaluation**
- Trained a **Logistic Regression Classifier** on each imputed dataset.  
- Split data into 70% training and 30% testing.  
- Evaluation Metrics:
  - **Accuracy**
  - **Precision**
  - **Recall**
  - **F1-score**
  - **ROC–AUC**
  - **PR–AUC**
- Generated **classification reports** for both classes:
  - **Class 0:** Non-defaulters  
  - **Class 1:** Defaulters  

**Visualizations:**
- Before/After Imputation Distribution (AGE vs Frequency)  
- Bar Graph — Precision, Recall, F1 for Class 0 & Class 1  
- ROC & PR Curves  
- AUC Comparison Chart  

---

### **Part C — Comparative Analysis**

#### **C.1 Results Comparison**

| Model | Precision (Class 1) | Recall (Class 1) | F1 | ROC AUC | PR AUC |
|:--|:--:|:--:|:--:|:--:|:--:|
| Dataset A (Median) | 0.70 | 0.24 | 0.35 | 0.714 | 0.497 |
| Dataset B (Linear Regression) | 0.70 | 0.24 | 0.35 | 0.714 | 0.497 |
| Dataset C (Decision Tree) | 0.69 | 0.24 | 0.35 | 0.714 | 0.497 |
| Dataset D (Listwise Deletion) | **0.72** | **0.23** | **0.35** | **0.723** | **0.510** |

**Key Findings:**
- All models show nearly identical metrics → Missing data handling had minimal influence.  
- Listwise Deletion shows slightly inflated AUC due to smaller sample variance, not genuine performance gain.  
- Recall for defaulters remains low (≈ 0.23–0.24), reflecting class imbalance rather than imputation effects.

---

#### **C.2 Efficacy Discussion**

- **Median Imputation:** Simplest and robust to outliers but reduces variance.  
- **Linear Regression Imputation:** Best balance between accuracy and interpretability.  
- **Decision Tree Imputation:** Captures non-linear patterns; performs similarly because relationships between variables are largely linear.  
- **Listwise Deletion:** Discards valid data and reduces representativeness. Marginally higher AUC comes from smaller dataset size, not better performance.  

**Conclusion:**  
Regression-based imputations (Linear and Decision Tree) preserve data structure and stability better than simple median filling or deletion.  
The logistic regression model’s weakness stems from **class imbalance**, not imputation strategy.

---

## Theoretical Background

This project discusses:
- The concept of **Missing At Random (MAR)** and why it’s a realistic simulation of real-world missing data.  
- **Logistic Regression** as a linear classifier for predicting binary outcomes.  
- Common **evaluation metrics** (Precision, Recall, F1, ROC–AUC, PR–AUC) for imbalanced classification.  
- How imputation affects statistical variance and feature relationships.  

---

## Results Summary

| Metric | Observation |
|:--|:--|
| **ROC AUC (All Imputations)** | ≈ 0.71 — Fair discrimination capability |
| **PR AUC (All Imputations)** | ≈ 0.50 — Weak detection of minority class |
| **Median vs Regression** | No significant performance gap |
| **Listwise Deletion** | Slight AUC inflation due to reduced data variance |
| **Recall (Class 1)** | Remains very low (≈ 0.23) — confirms imbalance-driven weakness |

---

## Insights and Recommendations

- **Imputation Robustness:**  
  Small MAR missingness (<10%) has minimal impact on model accuracy.  
- **Avoid Deletion:**  
  Listwise deletion introduces bias and discards valuable information.  
- **Linear Imputation Preferred:**  
  Maintains relationships and interpretability without reducing data variance.  
- **Future Work:**  
  - Handle class imbalance using **SMOTE / ADASYN**  
  - Apply **class-weighted logistic regression**  
  - Use **non-linear ensemble models (Random Forest, XGBoost)** for improved recall  

---

## Summary

This assignment demonstrates that:
- Regression-based imputations preserve data integrity better than deletion.  
- Performance limitations arise primarily from **class imbalance**, not missing data handling.  
- For small MAR missingness, **Linear Regression Imputation** is the most effective and conceptually sound approach.  

> ✅ Data imputation should aim for **information retention**, not mere data cleaning, ensuring reliable and fair model performance.
