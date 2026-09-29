# Credit Risk Dashboard — NorthTrust Financial

Power BI dashboard for monitoring a $445M loan portfolio across 2,200 borrowers.
Built as a portfolio project demonstrating credit risk modeling, DAX measure design,
and dark-theme dashboard development in Power BI.

## Dashboard Overview

**Page 1 — Portfolio Overview**
- KPI cards: Total Portfolio Value, Outstanding Exposure, EL Rate, Delinquency Rate, Avg Credit Score
- Loan count by Risk Grade (donut)
- Delinquency Rate by State (bar)
- Total Expected Loss by Loan Type and Risk Grade (stacked bar)
- Credit Score vs DTI % scatter by Risk Grade

**Page 2 — High Risk Watchlist (Grade D & E)**
- Pre-filtered KPIs: 37 high-risk loans, 12 severely delinquent, $205K expected loss, 7.50% EL rate
- Full loan detail table with grade badges and delinquency indicators
- EL by State and Avg Risk Score by Loan Type (bar charts)

## Technical Details

| Item | Detail |
|------|--------|
| Tool | Power BI Desktop |
| Data | Single flat table — 2,200 loans, 15 columns |
| Model | No star schema; all DAX on one table |
| Measures | 25+ DAX measures across KPIs, Expected Loss, Risk, and High Risk folders |
| Theme | Custom dark JSON theme (`NorthTrust Credit Risk`) |

## Key DAX Patterns

**Expected Loss (pre-aggregated in source data)**
```dax
Total Expected Loss = SUM('9_loan_portfolio_scored'[Expected_Loss])
```

**Pre-filtered High Risk measures (no page-level filter needed)**
```dax
Total EL High Risk =
CALCULATE(
    [Total Expected Loss],
    '9_loan_portfolio_scored'[Risk_Grade] IN {"D", "E"}
)
```

**Portfolio EL Rate**
```dax
Portfolio EL Rate =
DIVIDE([Total Expected Loss], [Total Outstanding Exposure])
```

## Risk Grade Model

| Grade | Score Range | Description |
|-------|-------------|-------------|
| A |
