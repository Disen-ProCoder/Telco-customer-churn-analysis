# IT3091 Telco Customer Churn — 3-Minute Demo Script

**Group ID:** 2026-DS-87  
**Track:** Guided Data Track — Telecommunications  
**Presenters:** Disen M.L.S. (Speaker A), Hannadige L.H.D. (Speaker B), Manelka H.D.L. (Speaker C)

## Speaker A — Disen M.L.S. (Slides 1–3, about 55 seconds)

### Slide 1: Title

Hello everyone. I’m Disen, this is Hannadige, and this is Manelka. Our project predicts which telco customers may leave, so the company can help them before they go.

### Slide 2: Dataset and EDA

We used the IBM Telco dataset with 7,043 customers. About 26.5 percent of them left. Look at the charts. Customers on month-to-month contracts leave 42.7 percent of the time. On two-year contracts, only 2.9 percent leave. New customers also leave more: 47 percent in the first year, but only about 10 percent after four years.

### Slide 3: Machine Learning Approach

For modelling, we split the data 80/20 and kept the test part untouched. We tried five models and checked them with cross-validation. Several scored almost the same, so we chose the simplest: Logistic Regression. Now Manelka will show how we built it.

## Speaker C — Manelka H.D.L. (Notebook, about 45 seconds)

**Screen order:** imports cell → data-quality cell for blank `TotalCharges` → model-comparison bar chart in section 12 → threshold chart in section 15.

Thanks. In the notebook, we first import pandas and NumPy for data, Matplotlib and Seaborn for charts, and scikit-learn for the models. Then we checked data quality. There were no duplicates, but 11 customers had a blank `TotalCharges`. They were all brand-new customers with zero tenure, so we set it to zero. We split the data before any deeper analysis, so the test set stays clean. Here we compare the models. Their ROC-AUC is close, between 0.83 and 0.85, so a complex model gave no real gain. We also tested extra features and class weights. Only one new feature, number of add-ons, helped, so we kept it and dropped gender. Last, this chart shows how we picked the threshold. The expected benefit is highest at 0.07.

## Speaker B — Hannadige L.H.D. (Slides 4–7, about 60 seconds)

### Slide 4: Results

Thanks. On the test data, our model scored a ROC-AUC of 0.842 and a PR-AUC of 0.631. A random guess gives only 0.265 for PR-AUC, so the model is much better. The most important factors are tenure, internet service, monthly charges, and contract.

### Slide 5: High-Risk Customers

With the threshold of 0.07, we flag 68 percent of customers. Of these, 37.9 percent really left. Of the others, only 2.2 percent left. Flagged customers are mostly on month-to-month contracts, and their median tenure is 16 months, compared with 57.

### Slide 6: Recommendation

Our advice: use the scores to choose who to contact first. Start with the top 20 percent, which is 282 customers. This reaches 187 people who would leave. Then test the offers with an A/B experiment before a bigger rollout. These patterns do not prove the cause.

### Slide 7: Limitations

Limitations: the data is a public sample with no dates, and the money numbers are assumptions. Senior citizens are flagged more often, so we must watch fairness. The model helps people decide. It does not decide alone. Thank you for watching.
