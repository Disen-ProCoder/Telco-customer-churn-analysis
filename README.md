# Telco Customer Churn Analysis

Machine-learning project that predicts telecom customer churn, profiles higher-risk customers, and supports data-driven retention campaigns using the IBM Telco Customer Churn dataset.

## Project overview

The project answers a practical retention question: **which customers should receive a retention offer this period?**

It frames churn prediction as binary classification, producing a probability score for each customer. The score supports customer ranking and flexible campaign selection rather than automatic decisions.

## Key results

| Measure | Result |
|---|---:|
| Dataset | 7,043 customers and 21 columns |
| Overall churn rate | 26.5% |
| Final model | Logistic Regression (`C = 4.5706`) |
| Test ROC-AUC | 0.842 |
| Test PR-AUC | 0.631 |
| Test F1 at threshold 0.50 | 0.607 |
| Selected campaign threshold | 0.07 |
| Precision / recall at 0.07 | 37.9% / 97.3% |
| Customers flagged at 0.07 | 68.1% |
| Top-20% campaign policy | 282 contacted; 187 churners reached; 66.3% precision |

Random Forest had the highest mean nested-CV PR-AUC, but Logistic Regression was within one standard error of it. The project therefore selected the simpler, more interpretable model using a pre-defined rule.

## Repository structure

| Folder | Contents |
|---|---|
| `01_Project_Proposal` | Initial proposal and business framing |
| `02_Dataset` | IBM Telco CSV and data dictionary |
| `03_Problem_Framing` | Problem Framing Canvas |
| `04_Workflow` | Project workflow diagram |
| `05_EDA` | Exploratory data analysis notebook and insight log |
| `06_Preprocessing` | Preprocessing notebook and feature-decision log |
| `07_Modeling` | Model-training notebook and comparison workbook |
| `08_Evaluation` | Evaluation notebook and test metrics |
| `09_High_Risk_Profiling` | High-risk profiling notebook and workbook |
| `10_Recommendations` | Retention recommendations |
| `11_Decision_Log` | Documented modelling decisions |
| `12_Final_Report` | Final written report |
| `13_Final_Notebook` | Complete end-to-end analysis notebook |
| `14_Demo` | Presentation deck and demo script |
| `15_Individual` | Individual learning reflections |
| `15_Viva_Preparation` | Viva preparation materials |

## How to run

The final, end-to-end workflow is in:

`13_Final_Notebook/Telco_Customer_Churn_Final.ipynb`

The notebooks were prepared for Google Colab and prompt for an upload of:

`02_Dataset/WA_Fn-UseC_-Telco-Customer-Churn.csv`

Required Python packages include:

```text
numpy
pandas
matplotlib
seaborn
scipy
scikit-learn
joblib
```

For reproducibility, use random seed `42`. The expected SHA-256 hash of the dataset is:

```text
88be4b93fbe0cc83421af1c503794c97c342eca914c1576db7c276e61d61358a
```

## Method summary

1. Split the data into stratified 80/20 training and test sets.
2. Clean `TotalCharges`, remove the identifier, simplify redundant service categories, and one-hot encode categorical variables in sklearn pipelines.
3. Compare Dummy, Logistic Regression, Decision Tree, Random Forest, and HistGradientBoosting models.
4. Tune models with nested cross-validation, using PR-AUC as the primary comparison measure.
5. Evaluate the selected model once on the untouched test set.
6. Select a campaign threshold using out-of-fold training predictions and transparent benefit assumptions.
7. Profile flagged customers and recommend an A/B test before operational rollout.

## Campaign assumptions

Expected-value estimates assume an offer cost of 20 per contacted customer, a 30% save rate among contacted churners, and retained value equal to 12 months of `MonthlyCharges`. These are scenario assumptions, not observed business outcomes.

## Limitations and responsible use

This uses a public IBM sample dataset, not real operational telecom data. It contains no dates, treatment-response data, true customer lifetime value, or externally validated outcomes. Patterns and feature importance show association, not causation.

The model should support trained retention staff rather than automatically determine customer treatment. Before deployment, validate it on current operational data, select policy according to campaign capacity, monitor subgroup outcomes, and test offers through a controlled A/B experiment.

## Data source

[IBM Telco Customer Churn dataset on Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
