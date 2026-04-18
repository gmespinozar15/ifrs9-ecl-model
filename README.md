# 🏦 IFRS 9 — Expected Credit Loss (ECL) Model

![Python](https://img.shields.io/badge/Python-3.11-blue)
![IFRS9](https://img.shields.io/badge/Framework-IFRS%209-darkblue)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.4-green)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

## 📌 Description

Implementation of the Expected Credit Loss (ECL) model under the
**IFRS 9** accounting standard. The model estimates credit loss provisions
for a portfolio of 112,035 customers using the three-component formula:

> ECL = PD × LGD × EAD


## 🎯 Objectives

- Estimate **PD** (Probability of Default) using Logistic Regression
- Calculate **LGD** (Loss Given Default) based on debt ratio and Basel III floors
- Estimate **EAD** (Exposure at Default) from revolving utilization
- Compute ECL per customer and aggregate at portfolio level
- Classify customers into **IFRS 9 Stages 1, 2 and 3**
- Generate regulatory-ready portfolio summary report

## 🛠️ Tech Stack

| Tool | Usage |
|---|---|
| Python 3.11 | Core language |
| Pandas, NumPy | Data manipulation |
| Scikit-learn | PD model (Logistic Regression) |
| Matplotlib, Seaborn | Visualizations |
| JupyterLab | Model development |


## 📊 Dataset

[Give Me Some Credit — Kaggle](https://www.kaggle.com/c/GiveMeSomeCredit)

- 150,000 customer records (112,035 after cleaning)
- Target: SeriousDlqin2yrs — 90+ day delinquency
- Default rate: 6.68%


## 📁 Repository Structure
ifrs9-ecl-model/
│
├── data/
│   ├── raw/                    # Original dataset (cs-training.csv)
│   └── processed/              # ECL results (ecl_results.csv)
│
├── notebooks/
│   └── 01_ECL_Model.ipynb      # Full pipeline: PD + LGD + EAD + ECL + Staging
│
├── reports/
│   └── figures/
│       ├── lgd_distribution.png
│       └── ecl_analysis.png
│
├── src/
│   ├── pd_model.py             # Probability of Default model
│   ├── lgd_model.py            # Loss Given Default estimation
│   ├── ead_model.py            # Exposure at Default calculation
│   └── ecl.py                  # ECL aggregation and staging
│
├── requirements.txt
├── .gitignore
├── main.py
└── README.md



## 📈 Model Results

### PD Model Performance
| Metric | Value |
|---|---|
| AUC-ROC | 0.7952 |
| Gini | 0.5904 |
| Approach | Logistic Regression + Balanced Weights |

### Portfolio ECL Summary
| Metric | Value |
|---|---|
| Total customers | 112,035 |
| Total exposure (EAD) | $352,048,000 |
| **Total ECL** | **$102,448,216** |
| **ECL coverage ratio** | **29.09%** |
| Average ECL per customer | $914.43 |

### IFRS 9 Staging
| Stage | Customers | Avg PD | Total ECL | ECL % |
|---|---|---|---|---|
| Stage 1 — Performing | 89 | 2% | $715 | 0.0% |
| Stage 2 — Underperforming | 22,328 | 16% | $617,371 | 0.6% |
| Stage 3 — Non-Performing | 89,618 | 45% | $101,830,130 | 99.4% |

> Stage 3 concentrates 99.4% of total ECL — consistent with real-world
> credit portfolios where defaulted customers drive provisioning requirements.



## 🔢 Methodology

### PD — Probability of Default
Logistic Regression trained on behavioral features with `class_weight='balanced'`
to handle the 6.68% default rate imbalance.

### LGD — Loss Given Default
Rule-based estimation using debt ratio as collateral proxy:
- Regulatory floor: 45% (Basel III unsecured retail)
- Ceiling: 90%
- Formula: `LGD = 0.45 + (DebtRatio × 0.10)`

### EAD — Exposure at Default
Estimated from revolving credit utilization:
- `EAD = RevolvingUtilization × $10,000 assumed limit`
- Clipped between $100 and $50,000

### IFRS 9 Staging
| Stage | PD Threshold | Treatment |
|---|---|---|
| Stage 1 | PD < 5% | 12-month ECL |
| Stage 2 | 5% ≤ PD < 20% | Lifetime ECL |
| Stage 3 | PD ≥ 20% | Lifetime ECL (credit-impaired) |


## 🚀 How to Run
git clone https://github.com/gmespinozar15/ifrs9-ecl-model.git
cd ifrs9-ecl-model
pip install -r requirements.txt
jupyter lab


Open `notebooks/01_ECL_Model.ipynb` and run all cells.

> Download `cs-training.csv` from [Kaggle](https://www.kaggle.com/c/GiveMeSomeCredit/data)
> and place it in `data/raw/` before running.



## 💼 Business Relevance

This model replicates the provisioning framework required by:
- IFRS 9 — International Financial Reporting Standard (effective 2018)
- Basel III — LGD floors for unsecured retail exposures
- SBS Peru — Superintendencia de Banca, Seguros y AFP requirements

Applicable to credit risk teams at banks, fintechs and AFP institutions.


## 👩‍💻 Author

**Gabriela Espinoza** — Data Analyst | Lima, Peru
[LinkedIn](linkedin.com/in/gabriela-espinoza-a75447388) · [GitHub](https://github.com/gmespinozar15)


This project is part of a Data Science portfolio focused on finance and risk analytics.