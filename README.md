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
|-----|-----|
| `notebooks/Superstore_Analysis.ipynb` | Full analysis notebook — cleaning, EDA, classification, regression, hyperparameter tuning (run top to bottom) |
| `dashboard` | Power BI dashboard |
| `requirements.txt` | Pinned Python dependency versions |
| `SuperStoreOrders.csv` | The dataset |

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
<img width="2224" height="1260" alt="image" src="https://github.com/user-attachments/assets/20a6b55b-8e98-40dd-bc58-ec90192a38e0" />
<img width="2232" height="1256" alt="image" src="https://github.com/user-attachments/assets/29b41b0b-2bdf-4d90-9bde-79fc27a6e151" />
<img width="2232" height="1264" alt="image" src="https://github.com/user-attachments/assets/d63d9051-de8b-42c5-a461-2afb79145cc9" />

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

## Contributors

This project was completed as a team effort:

| Name | GitHub |
|---|---|
| Adewale Odoffin | [@odoffin](https://github.com/odoffin) |
| Rachna Chatterjee | [RachnaChatterjee](https://github.com/RachnaChatterjee)|
| Nagasubramanyam Thodupunoori | — |
| Basanta Shahi | [@basanta999s-ship-it](https://github.com/basanta999s-ship-it) |
| Luiz Paulo Pacheco |[ @luiz-analyst](https://github.com/luiz-analyst) |
| Christian Prime Guerra | [@ChristianPrime](https://github.com/ChristianPrime) |
