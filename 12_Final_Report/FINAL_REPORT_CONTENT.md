# IT3091 Machine Learning — Final Report

## 1. Introduction

Customer churn is a major challenge for telecommunications providers because replacing lost customers is typically more expensive than retaining existing ones. This project uses the IBM Telco Customer Churn dataset to estimate each customer's churn risk, identify patterns among higher-risk customers, and support more focused retention decisions. The work covers data understanding, exploratory analysis, preprocessing, model comparison, evaluation, high-risk profiling, and business recommendations.

## 2. Business Problem

The retention manager needs a repeatable way to decide which customers should receive a retention offer. Without a risk-based process, the organisation may spend its limited campaign budget on customers who are unlikely to leave while missing customers at genuine risk. The model is therefore intended to rank customers by churn probability and support—not replace—retention-team decisions.

## 3. Problem Framing

The unit of analysis is one customer at a single point in time. The target is `Churn` (Yes/No), and the machine-learning task is binary classification. Success was defined before modelling as strong ranking performance, measured primarily through PR-AUC and ROC-AUC, followed by campaign value under transparent business assumptions. High-risk profiling is a secondary lens used to explain the segment identified by the model.

## 4. Dataset and Data Understanding

The dataset contains 7,043 customers and 21 columns. It includes demographic indicators, account tenure, services, contract type, payment method, monthly charges, total charges, and churn status. There were no duplicate rows or duplicate customer IDs. `TotalCharges` was stored as text and had 11 blank values; all were customers with zero tenure, so these values were converted to zero after confirming they represented customers not yet billed. The dataset is a public IBM sample and is not evidence of the behaviour of a particular real telecom provider.

## 5. Exploratory Data Analysis

Overall churn was 26.5%, so accuracy alone would be misleading: a model predicting no churn for every customer would achieve about 73.5% accuracy but no useful churn detection. Churn was concentrated among month-to-month customers (42.7%), fibre-optic customers (42.1%), and electronic-check customers (45.7%). Tenure showed a strong pattern: churn was 47.3% for customers with 0–12 months of tenure, compared with 9.9% for those with 49–72 months. These are associations in the sample; they do not prove that a service type, payment method, or contract causes churn.

## 6. Preprocessing and Feature Engineering

`customerID` was excluded because it is an identifier rather than a meaningful predictor. `TotalCharges` was converted to numeric, and redundant categories such as “No internet service” and “No phone service” were simplified. Categorical variables were one-hot encoded, while numeric variables were scaled only for scale-sensitive models. All transformations were included in sklearn pipelines to prevent leakage. Candidate engineered features were number of add-ons, automatic payment, and the gap between expected and observed charges. Only number of add-ons was retained; gender was removed because it did not add measurable predictive value. Class weighting was evaluated but not used because it did not improve the primary PR-AUC criterion.

## 7. Models

A majority-class Dummy classifier, Logistic Regression, Decision Tree, Random Forest, and HistGradientBoosting were evaluated using five-fold stratified cross-validation on the training set. The Dummy model had PR-AUC 0.265, equal to the churn prevalence. The untuned models achieved PR-AUC values of 0.661 for Logistic Regression, 0.613 for Decision Tree, 0.658 for Random Forest, and 0.644 for HistGradientBoosting. Hyperparameters were then tuned with RandomizedSearchCV inside nested cross-validation.

## 8. Model Comparison

Random Forest achieved the highest nested-CV PR-AUC (0.664 ± 0.019), but Logistic Regression (0.661 ± 0.019) was within one standard error of the best model. Following the pre-defined preference for the simplest statistically comparable model, Logistic Regression was selected. Its tuned regularisation parameter was C = 4.5706.

## 9. Evaluation

The final model was evaluated once on the untouched 20% test set of 1,409 customers. It achieved ROC-AUC 0.842, PR-AUC 0.631, F1 0.607 at the conventional 0.50 threshold, and Brier score 0.138. These results indicate useful ranking ability above the 26.5% baseline churn rate, but they do not guarantee the same performance on new real-world data.

The operating threshold was selected from out-of-fold training predictions using stated campaign assumptions: a cost of 20 per contacted customer, a 30% save rate among contacted churners, and retained value equal to 12 months of monthly charges. The value-maximising threshold was 0.07. On the test set this produced 37.9% precision, 97.3% recall, F1 of 0.546, and flagged 68.1% of customers. This is an intentionally broad policy under the assumptions, not a universal threshold. If campaign capacity is limited, the top 20% of scored customers offer a more focused list with 66.3% observed precision.

## 10. High-Risk Customer Profiling

At the 0.07 threshold, flagged customers had an observed test-set churn rate of 37.9%, compared with 2.2% among customers not flagged. The flagged group had median tenure of 16 months compared with 57 months for the unflagged group. It was also 78.1% month-to-month, 58.5% fibre-optic, and 46.7% electronic-check customers. Permutation importance identified tenure, internet service, monthly charges, and contract as the strongest predictors. These findings describe the model's risk pattern; they should not be interpreted as causal effects.

## 11. Retention Recommendations

The retention team should use the score as a prioritisation tool, beginning with a capacity-appropriate segment such as the top 10% or top 20% of risk scores. For example, the top 20% policy contacted 282 customers and reached 187 observed churners, with 66.3% precision. Potential interventions include reviewing service and price experience for higher-risk fibre-optic customers, engaging newer customers early, and offering contract or payment-method changes where appropriate. These interventions should be tested, not assumed effective. Before rollout, the provider should run an A/B test that compares contacted and comparable uncontacted high-risk customers to measure incremental retention caused by the offer.

## 12. Responsible AI Considerations

The model must be used as decision support, not as an automatic decision-maker. A retention agent should be able to review a customer's score, the relevant account context, campaign eligibility, and any customer preferences before contact. The model should never be used to deny service, impose a penalty, or make decisions that materially disadvantage a customer.

Gender was removed because it did not improve performance. The SeniorCitizen feature remains and should receive extra governance attention because it is age-related. On the test set, the model flagged 85.6% of senior customers and 64.9% of non-senior customers; observed churn also differed (44.1% versus 23.3%). This difference may reflect genuine risk differences, data structure, or bias, and the senior subgroup is relatively small (222 customers). The telecom provider should monitor flagged rate, recall, false-positive rate, and offer outcomes by relevant protected or vulnerable groups using real operational data. If unfair disparities appear, the feature set, threshold, campaign design, or model should be reviewed.

False positives may create unnecessary contact costs or frustrate customers; false negatives may leave likely churners without support. The chosen low threshold prioritises recall and accepts many false positives, which is only appropriate when outreach is low-risk and the business assumptions are credible. Customers should be given clear, non-manipulative offers and normal options to decline communications.

## 13. Limitations

This is a fictional IBM sample dataset with no external validation, no dates, and an ambiguous churn time window. It has no real customer lifetime value, offer cost, treatment-response, service-quality, competitor, or complaint information. Financial estimates therefore depend on assumptions rather than observed commercial outcomes. The dataset is a snapshot, so it cannot establish whether churn risk changes over time. Associations from EDA, coefficients, and feature importance are not causal claims. Finally, the 1,409-customer test set has sampling uncertainty, and the feature-selection process occurred before nested model comparison, so cross-validation estimates may be mildly optimistic.

## 14. Conclusion

The project demonstrates that a simple, interpretable Logistic Regression model can meaningfully rank churn risk in this dataset, achieving test ROC-AUC 0.842 and PR-AUC 0.631. Higher-risk customers were commonly newer, month-to-month, fibre-optic, and electronic-check customers. The model should support a carefully monitored retention campaign rather than automate customer treatment. The recommended next step is a controlled A/B test using real costs and response outcomes to determine whether targeted offers produce incremental retention value.

## 15. References

1. IBM Telco Customer Churn dataset, distributed through Kaggle: https://www.kaggle.com/datasets/blastchar/telco-customer-churn
2. IBM Community. “Telco Customer Churn (1113).” https://community.ibm.com/community/user/businessanalytics/blogs/steven-macko/2019/07/11/telco-customer-churn-1113
3. Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12, 2825–2830.

## Submission Note

Add a truthful AI-use disclosure required by the module or institution. It must accurately state which tools were used and how the group verified the work; do not make a generic declaration that is not true.

## Demo Video

3-minute YouTube demo: https://youtu.be/NYgSR7QvhAY
