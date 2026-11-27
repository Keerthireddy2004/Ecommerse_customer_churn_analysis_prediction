# E-Commerce Customer Churn Analysis & Prediction

Which customers leave an online store, and can we predict them? This project explores an e-commerce customer dataset, finds the main churn patterns and builds a Logistic Regression model to flag customers likely to churn.

**Dataset:** [E-Commerce Customer Churn (Kaggle)](https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction) · 5,630 customers · 20 columns · target column `Churn` (1 = customer left, 0 = stayed)

## What I did
1. **Load & explore** the data (`head`, `info`, `describe`, correlation heatmap)
2. **Clean** the data: filled missing values in numeric columns with the median, removed duplicates
3. **Find insights** with `groupby` on tenure, complaints and order category
4. **Visualise** churn distribution and tenure vs churn
5. **Predict churn** with Logistic Regression (80/20 train-test split)

## Key findings
| Finding | Result |
|---|---|
| Overall churn rate | **16.8%** |
| Average tenure, churned vs retained customers | **3.9 vs 11.4 months** |
| Churn rate, customers who complained vs not | **31.7% vs 10.9%** |
| Order category with highest churn | Mobile (about 27%) |
| Order category with lowest churn | Grocery (4.9%) |

New customers and customers who complained are the most likely to leave.

## Model
- **Algorithm:** Logistic Regression (`class_weight='balanced'`)
- **Features:** `Tenure`, `CashbackAmount`, `Complain`
- **Split:** 80% train / 20% test (stratified, `random_state=42`)

| Metric | Result |
|---|---|
| Accuracy | 71.8% |
| Churn recall | 80% |
| Churn precision | 35% |

Only about 17% of customers churn, so accuracy alone is misleading. I used `class_weight='balanced'` so the model catches more real churners: it finds **80% of customers who actually churn**, at the cost of more false alarms.

## Recommendations
- Offer onboarding support and discounts to new customers in their first months.
- Follow up quickly after a customer complaint.
- Look into why the Mobile category has higher churn.

## Limitations and next steps
- The model uses only 3 features. Next: add more features (satisfaction score, days since last order), try Random Forest, and tune the decision threshold.
- The dataset has no revenue column, so the financial impact of churn is not estimated.

## Files
- `churn_own.ipynb`: full analysis with outputs and graphs

## How to run
1. Download the dataset from Kaggle and save it as `E_Commerce_Dataset.xlsx` (sheet name: `E Comm`).
2. Install libraries: `pip install pandas matplotlib seaborn scikit-learn openpyxl jupyter`
3. Open the notebook with Jupyter, update the file path in the first code cell to where you saved the dataset, then **Kernel → Restart & Run All**.

**Tech stack:** Python, pandas, matplotlib, seaborn, scikit-learn
