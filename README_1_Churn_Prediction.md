# Telecom Customer Churn Prediction
### Python · SQL Server · Power BI · Random Forest · ~88% Accuracy

> **Business problem:** A telecom company was losing customers with no early warning system. This project builds an end-to-end solution — from raw data to a live Power BI risk-scoring dashboard — that identifies customers likely to churn before they leave.

---

## Results at a glance

| Metric | Value |
|---|---|
| Model accuracy | ~88% |
| High-risk segments identified | Customers with 30%+ higher churn probability |
| Data pipeline | SQL Server ETL → Python ML → Power BI integration |
| Business impact | Enables targeted retention campaigns, reducing churn cost |

---

## Project architecture

```
Raw telecom data (SQL Server)
        ↓
  ETL & data cleaning (SQL Server — stg_Churn → prod_Churn)
        ↓
  Feature engineering & model training (Python / Scikit-Learn)
        ↓
  Random Forest classifier (~88% accuracy)
        ↓
  Predictions exported → Power BI real-time risk scoring dashboard
```

---

## Step-by-step process

### Step 1 — ETL pipeline (SQL Server)
- Ingested raw telecom data into staging table `stg_Churn`
- Cleaned nulls, standardised values, inserted into production table `prod_Churn`
- Created two views for downstream use:
  - `vw_ChurnData` — historical churned/stayed customers (model training)
  - `vw_JoinData` — newly joined customers (prediction targets)

### Step 2 & 3 — Power BI data transformation
- Converted churn status to binary (Stayed = 0, Churned = 1)
- Engineered charge bands: `<20`, `20–50`, `50–100`, `>100`
- Built reference tables for Age groups, Tenure groups, and Service flags
- Created DAX measures: Total Customers, New Joiners, Total Churn, Churn Rate

### Step 4 — Power BI dashboard
- Interactive dashboard tracking churn KPIs, customer segments, and retention metrics
- Visual breakdown by age group, tenure, contract type, and service usage

### Step 5 — Random Forest churn prediction
- Trained on `vw_ChurnData` using Python (Scikit-Learn)
- Predicted churn probability for `vw_JoinData` (new customers)
- Integrated predictions back into Power BI for live customer risk scoring
- Identified customer segments with **30%+ higher churn risk**

---

## Key findings

- **Month-to-month contract customers** churn at significantly higher rates than annual contract holders
- **Customers without online security or device protection** show elevated churn risk
- **Early tenure customers (< 6 months)** are the highest-risk segment

---

## Tech stack

| Tool | Purpose |
|---|---|
| SQL Server | ETL pipeline, staging and production tables, views |
| Python (Pandas, NumPy, Scikit-Learn) | Feature engineering, Random Forest model |
| Power BI | Dashboard, DAX measures, ML prediction integration |
| Jupyter Notebook | Model development and evaluation |

---

## Files in this repo

| File | Description |
|---|---|
| `Churn_Analyst.ipynb` | Full Python pipeline — EDA, feature engineering, Random Forest model |
| `Churn Dashboard.pbix` | Power BI dashboard with churn KPIs and prediction visuals |
| `Analysis.md` | Detailed methodology and findings |

---

## How to run

1. Clone the repo
2. Open `Churn_Analyst.ipynb` in Jupyter Notebook
3. Install dependencies: `pip install pandas numpy scikit-learn matplotlib seaborn`
4. Run all cells — model trains and outputs predictions
5. Open `Churn Dashboard.pbix` in Power BI Desktop to explore the dashboard

---

*Project associated with MSc Data Analytics — De Montfort University (2025)*
