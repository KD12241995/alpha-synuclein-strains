# alpha-synuclein-strains


Analysis code for: **α-Synuclein strain dynamics predict cognitive transitions in Parkinson's disease
# PD α-Synuclein Biomarker Analysis Pipeline**

---

## Overview

This pipeline performs comprehensive analysis of α-synuclein biomarkers (THT + DLS) for predicting cognitive impairment in Parkinson's disease, using two independent cohorts (JHU, UW, n=227).

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| `Kundlik_demographic.ipynb` | Demographic table generation (Kruskal-Wallis, Chi-square) |
| `021526_Kundlik_odds_ratio.ipynb` | Multivariable logistic regression & odds ratio analysis |
| `PD_cross_sectional_Final.ipynb` | Cross-sectional ML classification (HC vs PD, PD-NC vs PD-CI, 4-class) |
| `PD_time_varying_python.ipynb` | Longitudinal survival analysis (time-varying Cox, RSF, GBM, SHAP) |

Run notebooks in the order listed above.

---

## Requirements

```bash
pip install pandas numpy matplotlib seaborn scipy statsmodels openpyxl
pip install scikit-learn xgboost catboost
pip install scikit-survival shap lifelines
```

---

## Input Data

| File | Used in |
|------|---------|
| `For demographic_KD.xlsx` | `Kundlik_demographic.ipynb` |
| `02092026_cross_sectional.csv` | `021526_Kundlik_odds_ratio.ipynb`, `PD_cross_sectional_Final.ipynb` |
| `01062026-longitudinal-DLS_new.csv` | `PD_time_varying_python.ipynb` |
| `02092026_longitudinal.csv` | `PD_time_varying_python.ipynb` |

> **Note:** Notebooks were originally developed in Google Colab. File paths use `/content/` — adjust to your local path if running outside Colab.

---

## Cohort

| Group | n |
|-------|---|
| HC (Healthy Control) | 49 |
| PD-NC | 47 |
| PD-MCI | 98 |
| PDD | 33 |
| **Total** | **227** |

- Cohort 1 (JHU): n=113
- Cohort 2 (UW): n=114

---

## Analysis Steps & Output

### 1. Demographic Analysis (`Kundlik_demographic.ipynb`)
- Baseline characteristics by group and cohort
- Statistical tests: Kruskal-Wallis (continuous), Chi-square (categorical)
- **Output**: `Demographic_Tables_Final.xlsx`

### 2. Odds Ratio Analysis (`021526_Kundlik_odds_ratio.ipynb`)
- Multivariable logistic regression: PD-NC vs PD-CI
- Adjusted for sex, age, education, disease duration
- Combined + JHU + UW cohorts
- **Output**: `Logistic_Regression_OddsRatio_Results.xlsx`

### 3. Cross-Sectional ML Classification (`PD_cross_sectional_Final.ipynb`)
- Task 1: HC vs PD (16 features)
- Task 2: PD-NC vs PD-CI (17 features)
- Task 3: 4-class (HC / PD-NC / PD-MCI / PDD)
- Validation: RepeatedStratifiedKFold (5-fold × 10 repeats) + Leave-One-Cohort-Out
- Models: GBDT, XGBoost, Random Forest, Extra Trees, Decision Tree, Logistic Regression, CatBoost
- **Output**: `demographics_statistics.xlsx`, `biomarker_validation.xlsx`, `/final_corrected_results/`

### 4. Longitudinal Survival Analysis (`PD_time_varying_python.ipynb`)
- Time-varying Cox regression (univariate)
- ML survival models: LASSO-Cox, RSF, GBM
- Forward variable selection (2→6 variables)
- SHAP feature importance
- Validation: StratifiedGroupKFold (5-fold × 10 iterations)
- **Output**: `Univariate_Cox_Results_v2.xlsx`, `Forward_Selection_Complete.xlsx`, `SHAP_Results_Top3.xlsx`, `SHAP_Analysis_Top3.pdf`

---

## Contact

Kyungdo Kim, kkim207@jh.edu
Johns Hopkins University School of Medicine
