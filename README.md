# ASA-SF-Student-Data-Challenge-2026
This repository showcases my award-winning work for the **2026 ASA South Florida Student Data Challenge**. I received the **Excellence Award (sole recipient)** and ranked **#1 overall** with **RMSE = 4.4336**.

---

## 📌 Competition Overview
The **ASA South Florida Student Data Challenge (2026)** organized by the American Statistical Association(ASA) South Florida Chapter is a student competition where the task is to build models to predict a noise-perturbed version of **Direct HDL Cholesterol** using a NHANES 2024–based dataset.

✅ **Goal:** Predict `LBDHDD_outcome` (noise-perturbed HDL cholesterol, mg/dL) for the 200-row test set  
📈 **Ranking metric:** **RMSE (Root Mean Squared Error)** — lower is better

---

## 🧾 Dataset Description
The dataset is derived from the **2024 National Health and Nutrition Examination Survey (NHANES)** and includes dietary, demographic, and anthropometric predictors.

- **Total individuals:** 1,200  
- **Training set:** 1,000 rows (includes target `LBDHDD_outcome`)  
- **Test set:** 200 rows (target hidden)  
- **Variables:** 97 in training (including target), 96 in test  
- **Target:** `LBDHDD_outcome` (noise-perturbed Direct HDL Cholesterol, mg/dL)

📂 **Files included**
- `train.csv` — training data (includes `LBDHDD_outcome`)
- `test.csv` — test data (no target)
- `variable_labels.csv` — variable names + labels

> Note: The outcome is noise-perturbed to protect original NHANES values while preserving realistic structure.

---

## 🗂️ Repository Contents
- 📓 **Notebook:** `JadeMuyambo_2026 ASA South Florida Student Data Challenge.ipynb` (end-to-end workflow)
- 📝 **Report:** `JadeMuyambo_2026DataChallengeReport.pdf` (≤ 4 pages)
- 📤 **Submission file:** `pred.csv` (one column `pred`, 200 rows)
- 🏅 **Certificate:** `certificateJade.pdf`
- 📊 **Data:** `train.csv`, `test.csv`, `variable_labels.csv`

---

## 🧰 Tools & Environment
Built in **Python** using **JupyterLab / Jupyter Notebook**.

**Main libraries**
- `pandas`, `numpy` — data loading and preparation
- `scikit-learn` — preprocessing, model training, validation, and tuning

**Key scikit-learn tools**
- `Pipeline`, `ColumnTransformer`, `SimpleImputer`
- `RepeatedKFold`, `cross_val_score`
- `RandomizedSearchCV`
- `Ridge`, `ElasticNet`
- `HistGradientBoostingRegressor`
- `ExtraTreesRegressor`
- `StackingRegressor`

---

## 🔬 Methodology (High-Level)
### 1) Data Cleaning & Setup
- Removed the index-like column `Unnamed: 0` from train and test.
- Split training data into predictors **X** and target **y** (`LBDHDD_outcome`) to avoid leakage.
- Aligned test columns to training predictors with `test.reindex(columns=X.columns)`.

### 2) Preprocessing (Leakage-Safe)
- All predictors were numeric in this dataset.
- Used **median imputation** for missing values.
- Imputation was kept **inside the pipeline**, so it was fit only on training folds during cross-validation.

### 3) Validation Strategy
- Evaluated models using **RMSE** (the competition metric).
- Used **Repeated K-Fold Cross-Validation**:
  - 5 folds × 5 repeats = **25 validation splits**
- This produces a more stable estimate than a single split and supports fair comparisons.

### 4) Modeling Approach
✅ Stage-by-stage improvement:
1. **Baseline:** Ridge Regression  
2. **Tuned model:** HistGradientBoostingRegressor (RandomizedSearchCV)  
3. **Final model:** **Stacking ensemble** to combine complementary models

---

## 📈 Model Selection & Performance
Model choice was based on: **lowest cross-validated RMSE**.

| Model | CV RMSE (mean) | CV RMSE (SD) | Notes |
|------|----------------:|-------------:|------|
| Ridge baseline | 6.058 | 0.344 | Linear benchmark + median imputation |
| Tuned HistGradientBoosting | 4.839 | 0.255 | Best single tuned nonlinear model |
| ⭐ **Stacking ensemble (final)** | **4.708** | **0.226** | HGB + Ridge + ElasticNet + ExtraTrees |

🏁 **Final competition result**
- **Final test RMSE:** **4.4336**
- **Rank:** **#1 overall**
- **Award:** **Excellence Award (sole recipient)**

---

## 💡 Key Takeaways
- Simple preprocessing + **leakage-safe pipelines** made results trustworthy and reproducible.
- **Repeated cross-validation** provided a stable benchmark for fair model comparison.
- **Tuned gradient boosting** captured nonlinear relationships efficiently.
- **Stacking complementary models** reduced RMSE further than any single model.

---

## 📃 License
This project is licensed under the MIT lisence. See license file for details.

## 📃 Author
Jade Muyambo
M.S. Data Science — University of Miami
Faculty Mentor: Dr. Liang Liang

If you’d like to connect, feel free to reach out:
💼 LinkedIn: [https://www.linkedin.com/in/jade-m-5292a7177/]
🌐 Portfolio: [https://jademuyambo.carrd.co]

## Acknowledgement
Thank you to the ASA South Florida Chapter for organizing the Student Data Challenge and providing the dataset and evaluation framework.
