# Superstore Order Profitability: EDA, Classification & Regression

End-to-end analysis of the Global Superstore Orders dataset (2011–2014):
data cleaning, feature engineering, exploratory analysis, and two
predictive pipelines — a **classifier** that flags loss-making orders
before they ship, and a **regressor** that estimates the dollar
profit/loss of an order — with hyperparameter tuning on the best model
from each pipeline. The project also includes an interactive Power BI
dashboard for exploring the same findings visually.

## Business questions

1. **Diagnostic:** Where is the business making or losing money — by
   category, region, discount level, and shipping mode?
2. **Predictive:** Can we flag a loss-making order before it ships, and
   estimate how much profit or loss it will generate?

## Key findings

- Orders discounted **more than 30%** lose money **92.7%** of the time —
  loss probability climbs from 2% (no discount) to 93% (high discount),
  a cliff, not a gradual slope.
- **Tables** is the only sub-category, out of 17, that loses money
  overall (−$64,083); **Copiers** is the single largest profit
  contributor (+$258,568).
- **Office Supplies in the West region** shows the highest average
  profit margin of any region-category pairing (28.6%) — a separate
  finding from Technology leading on raw revenue ($4.74M).
- **XGBoost** is the strongest classifier for flagging unprofitable
  orders (ROC-AUC 0.969, improving to 0.970 after hyperparameter tuning).
- **Random Forest** is the strongest regressor for estimating profit
  dollar amount (R² 0.708, improving to 0.715 after tuning).

## Repo contents

| Path | Purpose |
|---|---|
| `notebooks/Superstore_Analysis.ipynb` | Full analysis notebook — cleaning, EDA, classification, regression, hyperparameter tuning (run top to bottom) |
| `dashboard` | Power BI dashboard — see below |
| `requirements.txt` | Pinned Python dependency versions |
| `SuperStoreOrders.csv` | The dataset — see Data source below |

## Data source

This project uses the "Global Superstore" dataset (order-level retail
transactions, 2011–2014). Place `SuperStoreOrders.csv` in the repo root
before running the notebook.

## How to run the notebook

```bash
pip install -r requirements.txt
jupyter notebook notebooks/Superstore_Analysis.ipynb
```

Run all cells top to bottom. The hyperparameter-tuning cells (Section 10)
are the slowest part (a few minutes on a laptop CPU); everything else
runs in well under a minute.

## Power BI Dashboard

A three-page interactive dashboard (Overview / Sales / Profit) built on
the same dataset, covering:
- KPI scorecards, sales and profit trends, category and regional
  breakdowns
- Discount-tier loss analysis and a profit-margin heatmap by region ×
  category
- An order-level scatter plot (discount vs. profit) with outlier
  highlighting, using the same IQR-based outlier definition as the
  notebook (orders outside −$55 to $92 profit)

*(Add a screenshot or two here once exported — a `dashboard/` folder with
a `.pbix` file and a PNG preview makes this section far more compelling
for anyone browsing the repo without opening Power BI.)*

## Notebook structure

1. Loading Dataset & Initial Audit
2. Data Cleaning & Standardization
3. Feature Engineering
4. Exploratory Data Analysis (EDA)
5. Visualization
6. Business Performance Analysis (discount sensitivity, sub-category
   profitability, KPIs & outlier detection)
7. Predictive Modeling: Classification Pipeline (Logistic Regression,
   Random Forest, KNN, XGBoost, Deep Neural Network)
8. Model Evaluation & Benchmarking
9. Profit Regression Analysis (Linear Regression vs. Random Forest)
10. Hyperparameter Tuning — best classifier (XGBoost) and best regressor
    (Random Forest), with cross-validated `RandomizedSearchCV`
11. Conclusion & Strategic Recommendations

## Model results

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.920 | 0.930 | 0.970 | 0.950 | 0.953 |
| Random Forest | 0.919 | 0.926 | 0.969 | 0.947 | 0.958 |
| KNN (k=15) | 0.899 | 0.909 | 0.959 | 0.933 | 0.939 |
| **XGBoost** | **0.923** | **0.929** | **0.971** | **0.949** | **0.969** |
| DNN | 0.920 | 0.920 | 0.970 | 0.950 | 0.960 |

| Model | Metric | Untuned | Tuned |
|---|---|---|---|
| XGBoost (classifier) | ROC-AUC | 0.969 | 0.970 |
| Random Forest (regressor) | R² | 0.708 | 0.715 |

