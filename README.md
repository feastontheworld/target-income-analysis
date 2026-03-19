# Target Corporation Income Statement Analysis (FY2021–FY2025)

**Tools:** Python, pandas, SQLite, SQL, Jupyter Notebook, DB Browser for SQLite, Microsoft Excel  
**Data Source:** Target Corporation 10-K filings, SEC EDGAR, FY2021–FY2025

---

## Overview

This project analyzes Target Corporation's income statement across five fiscal years to decompose a significant operating income collapse in FY2023. Despite revenue growing 2.9% to $109.1B, operating income fell 56.3% from $9.1B to $4.0B — a $5.1B decline in a single year. Using SQL-based variance decomposition, this analysis identifies the drivers behind that divergence and quantifies each one's contribution.

---

## Key Finding

Gross margin deterioration accounted for $5.14B of the $5.10B total operating income decline in FY2023 — effectively the entire collapse. COGS as a percentage of revenue spiked 4.71 percentage points from 70.72% to 75.43%, driven by excess inventory markdowns in discretionary categories. Revenue growth contributed a partially offsetting +$266M while SG&A increases absorbed $262M — the two effects canceling each other out almost exactly.

The variance decomposition model explains 99.3% of the actual operating income change.

---

## Project Structure
```
target_project/
│
├── target_income_analysis.ipynb   # Full analysis pipeline
├── target_financials_raw.xlsx     # Raw income statement data (source of truth)
├── target_analysis.xlsx           # Variance bridge + dashboard charts
├── target_analysis.db             # SQLite database
└── target_analysis_brief.pdf      # Full analytical brief with figures
```

---

## Methodology

**1. Data Collection**  
Income statement line items manually entered from Target's 10-K filings for FY2021–FY2025: net sales, cost of sales, gross profit, SG&A expenses, operating income, and net income. All figures in millions USD.

**2. SQL Feature Engineering**  
Raw data loaded into SQLite via pandas. Computed metrics table built using SQL: gross margin %, operating margin %, SG&A %, and COGS %. Year-over-year changes calculated using `LAG()` window functions ordered by fiscal period.

**3. Variance Decomposition**  
Operating income change decomposed into three drivers:
- Revenue volume effect — incremental revenue applied at prior year margin rate
- Gross margin impact — margin rate change applied to current year revenue
- SG&A impact — overhead rate change applied to current year revenue

**4. Visualization**  
Results visualized as a waterfall bridge chart (FY2022→FY2023 operating income bridge) and a three-chart dashboard covering margin trends, revenue vs operating income divergence, and COGS % over time. Built in Excel.

---

## Results Summary

| Fiscal Year | Revenue | Gross Margin % | Operating Margin % | COGS % |
|---|---|---|---|---|
| FY2021 | $93.6B | 29.27% | 7.06% | 70.73% |
| FY2022 | $106.0B | 29.28% | 8.55% | 70.72% |
| FY2023 | $109.1B | 24.57% | 3.63% | 75.43% |
| FY2024 | $107.4B | 27.54% | 5.49% | 72.46% |
| FY2025 | $106.6B | 28.21% | 5.39% | 71.79% |

---

## How to Run

1. Clone the repository
2. Open `target_income_analysis.ipynb` in Jupyter Notebook
3. Ensure `target_financials_raw.xlsx` is in the same directory
4. Run all cells sequentially
5. Output database `target_analysis.db` can be opened in DB Browser for SQLite

---

## Full Analysis

See `target_analysis_brief.pdf` for the complete analytical brief including variance decomposition methodology, interpretation, and implications for FP&A practice.