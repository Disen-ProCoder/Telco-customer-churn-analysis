# Results Source of Truth

Use these values consistently in the report, slides, recommendations, and demo.

| Item | Agreed value | Source |
|---|---:|---|
| Dataset | 7,043 customers; 21 columns | EDA / Final Notebook |
| Overall churn rate | 26.5% | EDA / Final Notebook |
| Train / test split | 5,634 / 1,409; stratified 80/20 | All modelling notebooks |
| Missing `TotalCharges` | 11 blank values; all tenure = 0 | EDA / Final Notebook |
| Final model | Logistic Regression; C = 4.5706 | Training / Evaluation |
| Selection rule | Simplest model within one standard error of best nested-CV PR-AUC | Training |
| Test ROC-AUC | 0.842 | Evaluation / Profiling / Final Notebook |
| Test PR-AUC | 0.631 | Evaluation / Final Notebook |
| Test F1 at 0.50 | 0.607 | Evaluation / Final Notebook |
| Brier score | 0.138 | Evaluation / Final Notebook |
| Chosen threshold | 0.07 | Evaluation / Profiling / Final Notebook |
| Precision / recall at 0.07 | 37.9% / 97.3% | Evaluation / Final Notebook |
| Customers flagged at 0.07 | 68.1% | Evaluation / Profiling / Final Notebook |
| Churn, flagged / not flagged | 37.9% / 2.2% | Profiling / Final Notebook |
| Median tenure, flagged / not flagged | 16 / 57 months | Profiling / Final Notebook |
| Month-to-month, flagged / not flagged | 78.1% / 5.1% | Profiling / Final Notebook |
| Fibre optic, flagged / not flagged | 58.5% / 11.4% | Profiling / Final Notebook |
| Top-20% policy | 282 contacted; 187 churners reached; 66.3% precision | Profiling / Recommendations |

All expected-net-benefit values rely on the project assumptions: offer cost = 20, save rate = 30%, and retained value = 12 months of MonthlyCharges. They are scenario estimates, not observed business results.
