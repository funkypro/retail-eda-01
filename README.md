### Retail Data Audit, Recovery & Intelligent Analytics

A complete end-to-end EDA project on a corrupted retail dataset (~5,200 rows). Covers data auditing, cleaning, feature engineering, outlier detection, correlation analysis and business insights - built using Python.

---

## Problem Statement

A retail organization shared a highly corrupted dataset extracted from multiple internal systems. The objective was to:
- Audit the raw data and identify all quality issues
- Clean and recover the dataset systematically
- Engineer new features and perform advanced analysis
- Derive actionable business insights

---

## Dataset

| Property | Detail |
|---|---|
| Rows | ~5,200 |
| Columns | 10 |
| Domain | Retail / E-commerce |
| Format | CSV |

**Columns:** `Order_ID`, `Product`, `Category`, `Price`, `Quantity`, `Discount`, `Region`, `Payment_Mode`, `Customer_Rating`, `Sales_Date`

---

## Project Structure

```
retail-eda-01/
│
├── retail_sales.csv                          # Raw dataset
├── Retail_Data_Audit_Intelligent_Analytics   # Main Jupyter notebook
└── README.md                                 # You are here
```

---

## What's Inside the Notebook

### Section A — Data Audit
- Identified 10 distinct data quality issues
- Categorized into: Missing Data, Inconsistent Formats, Invalid Values, Structural Issues
- Explained impact of 3 critical issues on analytics and ML models

### Section B — Data Cleaning Pipeline
- Step-by-step cleaning workflow with justification for every decision
- Handled: duplicates, casing inconsistencies, mixed date formats, text in numeric columns, negative values
- Before vs After comparison

### Section C — Feature Engineering & Advanced Analysis
- Derived `Revenue = Price × Quantity` and `Final_Revenue = Revenue × (1 - Discount)`
- Segmented orders into Low / Medium / High value using quartile boundaries
- Category-wise and Region-wise revenue analysis
- Outlier detection using IQR and Z-score methods
- Correlation heatmap with business interpretation

### Section D — Business Insights
- Identified highest revenue category and lowest performing region
- Discovered 2 key trends: revenue concentration and payment mode preferences
- Provided 2 actionable business recommendations

---

## Key Findings

- **Electronics** is the highest revenue generating category
- **East** region is the lowest performing region by total revenue
- **Price** is the single strongest driver of revenue (correlation = 1.0)
- **Discounts** show weak negative correlation with Final Revenue (-0.07) — deep discounting is not widespread but does hurt margins where applied
- **59 high-value outliers (1.5%)** detected in Final Revenue using IQR method
- Order distribution: Medium (1,995 orders) > Low (998) = High (998)

---

## Data Issues Found & Fixed

| Issue | Category | Fix Applied |
|---|---|---|
| Missing Product, Category, Region, Payment_Mode, Discount, Sales_Date | Missing Data | Imputed or dropped |
| Rows with both Product & Category missing | Missing Data | Dropped |
| Region casing (North / NORTH / north) | Inconsistent Format | `.str.title()` |
| Payment_Mode casing (upi / UPI) | Inconsistent Format | `.str.upper()` |
| Mixed date formats in Sales_Date | Inconsistent Format | `pd.to_datetime()` |
| Discount contains "ten" and "?" | Invalid Value | Coerced to NaN → median imputed |
| Negative and zero Quantity | Invalid Value | Rows dropped |
| Negative Price | Invalid Value | Rows dropped |
| Customer Rating exceeds scale | Invalid Value | Flagged |
| 200 duplicate rows | Structural | `drop_duplicates()` |

---

## Tech Stack

- Python 3.x
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy

---

## How to Run

```bash
# Clone the repo
git clone https://github.com/funkypro/retail-eda-01.git
cd retail-eda-01

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy jupyter

# Launch notebook
jupyter notebook
```

---

## Learnings

- IQR is more robust than Z-score for skewed revenue data
- Inconsistent casing in categorical columns silently inflates cardinality during ML encoding
- Negative quantity and price corrupt all downstream revenue features — must be fixed before feature engineering
- `pd.to_datetime(errors='coerce')` handles mixed date formats gracefully

