# IT3091 Machine Learning — Initial Report

## Telco Customer Churn — Customer Retention Analysis

**Track:** Guided Data Track  
**Domain:** Telecommunications (Code 7)  
**Group ID:** 2026-DS-87  
**Group members:** Disen M.L.S. (IT24102214), Manelka H.D.L. (IT24101762), Hannadige L.H.D. (IT24102552)

## 1. Track

This project follows the **Guided Data Track** in the telecommunications domain. The project uses machine learning and data analysis to help a telecom provider understand customer churn and make better retention decisions.

## 2. Business Context and Problem

Customer churn occurs when a customer stops using a telecom provider's services. Losing customers reduces revenue, and acquiring new customers is usually more expensive than retaining existing customers. The retention team has limited time and budget for calls, offers, and discounts. Without a systematic method, the team may contact customers who are unlikely to leave while missing customers who are genuinely at risk.

The business problem is to identify customers who are most likely to churn so that the retention team can prioritise suitable customers for retention outreach.

## 3. Lenses and Reasons

### Primary Lens: Churn Risk

The primary lens is **customer churn risk**. The project will estimate the probability that each customer will churn. This is the most suitable lens because the retention manager needs to decide which customers should be contacted first when campaign resources are limited. A risk score allows customers to be ranked from highest to lowest risk and supports a flexible campaign cut-off.

### Secondary Lens: High-Risk Customer Profiling

The secondary lens is **high-risk customer profiling**. After identifying customers with high predicted churn risk, the project will describe the common characteristics of this group. These characteristics may include tenure, contract type, internet service, payment method, and monthly charges. This lens is useful because the retention team needs to understand the type of customers identified by the model, not only receive a list of customer IDs.

## 4. Proposed Task and Output

The proposed machine-learning task is **binary classification**. The target variable is `Churn`, which has the values Yes and No. The model will predict a churn probability for each customer rather than only a simple yes-or-no result.

The planned outputs are:

- A trained churn-classification model that produces a probability score for each customer.
- A ranked list of customers from highest to lowest churn risk.
- A recommended risk threshold or capacity-based top-risk segment for retention outreach.
- A comparison of suitable machine-learning models using fair evaluation measures.
- A profile of high-risk customers and practical retention recommendations.

## 5. Dataset

The project uses the IBM Telco Customer Churn dataset available on Kaggle. The dataset contains 7,043 customer records and 21 columns. It includes customer demographics, account tenure, services, contract type, payment method, monthly charges, total charges, and churn status.

Dataset source: https://www.kaggle.com/datasets/blastchar/telco-customer-churn/data

## 6. Proposed Workflow

The project will follow this workflow:

1. **Data understanding:** inspect the dataset structure, variable meanings, data types, missing values, duplicate records, and data quality issues.
2. **Train-test split:** split the data into stratified training and test sets before deeper analysis or modelling to reduce data leakage.
3. **Exploratory data analysis:** analyse churn patterns by tenure, contract type, payment method, internet service, monthly charges, and other relevant variables.
4. **Data preprocessing:** convert data types where required, handle missing values, remove identifiers, encode categorical variables, and scale numerical variables when needed.
5. **Feature engineering:** test useful derived features and retain them only when they improve model performance.
6. **Model training and comparison:** compare a baseline model with Logistic Regression, Decision Tree, Random Forest, and Gradient Boosting models using cross-validation.
7. **Evaluation and threshold selection:** evaluate the selected model using ROC-AUC, PR-AUC, precision, recall, F1-score, and calibration. Select a practical threshold based on campaign assumptions and capacity.
8. **High-risk profiling and recommendations:** describe high-risk customers, provide retention recommendations, state limitations, and recommend testing interventions through an A/B test.

## 7. Core Responsibility of Each Member

| Group member | Student ID | Core responsibility | Planned contribution |
|---|---|---|---|
| Disen M.L.S. | IT24102214 | Data preprocessing, final notebook/report integration, and consistency checking | Prepare the data for modelling, document preprocessing decisions, integrate project work into the final notebook and report, and check that project documents use consistent figures. |
| Hannadige L.H.D. | IT24102552 | Model training, model comparison, evaluation, and high-risk profiling | Train and compare machine-learning models, evaluate the selected model, support threshold selection, and identify characteristics of high-risk customers. |
| Manelka H.D.L. | IT24101762 | Exploratory data analysis, business framing, recommendations, and presentation interpretation | Analyse churn patterns, help define the business problem and lenses, develop practical recommendations, and communicate findings in the report and presentation. |

## 8. Expected Value

The expected value of this project is a repeatable process that helps the retention manager focus outreach on customers with higher predicted churn risk. The model will support human decision-making and should not automatically make decisions about customer treatment. Any retention offer should be tested using real campaign outcomes before wider implementation.

## 9. Reference

Blastchar. (n.d.). *Telco customer churn*. Kaggle. https://www.kaggle.com/datasets/blastchar/telco-customer-churn/data
