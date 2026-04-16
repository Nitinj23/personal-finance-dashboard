# Personal Finance Dashboard · Power BI + Python

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logo=powerbi&logoColor=black)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-30%2B%20measures-0078D4?style=flat)
![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat)

A **portfolio-level personal finance dashboard** built end-to-end in Power BI (.pbip format) with embedded Python forecasting. Tracks real multi-currency spending (CAD + INR) across 3+ years, auto-generates monthly forecasts, and surfaces actionable insights — all without any manual data entry beyond the source Excel file.

---

## Dashboard Pages

| Page | What It Answers |
|---|---|
| **Annual Overview** | How is this year tracking vs last year? Am I on pace to save more? |
| **Monthly Overview** | Where did my money go this month? How does it compare to last month and last year? |
| **Spending Detail** | What did I spend this week, category by category? What was my biggest transaction? |

---

## Key Features

- **Automated forecast engine** — embedded Python script categorises each expense as *Monthly*, *Annual*, or *Ad-hoc* based on historical density, then projects forward to year-end with safety buffers
- **Multi-currency support** — INR amounts converted to CAD via a `Dim_ExchangeRate` table with fill-down logic; all analysis in a single currency
- **Week-level drill-through** — right-click any weekly bar to drill through to the `Spending Detail` page scoped to that exact week
- **30+ DAX measures** with consistent naming convention across two measure tables
- **Conditional formatting driven by measures** — card reference labels turn red/green based on direction of change vs prior month and prior year
- **Git-friendly .pbip format** — full text-based project, no binary .pbix; every visual and measure is version-controlled

---

## Tech Stack

| Layer | Technology |
|---|---|
| Data model | Power BI `.pbip` / TMDL (star schema) |
| ETL & forecast | Python 3, pandas, numpy embedded in Power Query M |
| Analytics | DAX (30+ measures: income, expense, savings, forecast, variance, colour logic) |
| Data source | Excel (.xlsx) with multi-currency transactions |
| Version control | Git / GitHub |

---

## Forecast Logic

Categories are auto-classified on every refresh based on historical spend density:

- **Monthly** — appears in 80%+ of recent months → forecast = median x 1.20
- **Annual** — appears in 2+ years but not monthly → forecast = avg of last 2 x 1.30
- **Ad-hoc** — irregular, excluded from forecast
- **Salary** — special rule: floor = min of last 2 months x 0.90

---

## DAX Naming Convention

| Prefix | Purpose | Example |
|---|---|---|
| `msr` | Numeric value | `msrIncome_CM`, `msrExpense_PM` |
| `msrPct_` | Percentage | `msrSavingsPct_CM` |
| `msrTxt_` | Label / text output | `msrTxt_Label_Expense_LY` |
| `msrClr_` | Colour string for conditional formatting | `msrClr_Savings_vs_LY` |

Period suffixes: `_CM` (current month) · `_PM` (prior month) · `_LY_CM` (last year same month) · `_YTD` · `_CY`

---

## Running the Project

1. Clone this repository
2. Add your own `data/Expenses.xlsx` with columns: Date, Category, Sub Category, Expense Group, Amount, Currency, Country, City, Source
3. Open `CostReport.pbip` in **Power BI Desktop**
4. Refresh — Python forecast runs automatically on every refresh

> `data/Expenses.xlsx` is excluded from this repo (personal financial data). A sample anonymised dataset will be added in a future update.

---

## Project Status

- [x] Star schema data model (Fact + 2 Dims + 2 Measure tables)
- [x] Multi-currency ETL (CAD/INR)
- [x] Automated Python forecast engine
- [x] Annual Overview page (YTD vs LY, savings rate, category breakdown)
- [x] Monthly Overview page (MoM + YoY KPI cards, donut, weekly comparison)
- [x] Spending Detail drill-through page (week-level, transaction table)
- [ ] Standalone Python pipeline
- [ ] Prophet ML forecasting with confidence bands
- [ ] Z-score anomaly detection
- [ ] Sample / anonymised dataset

---

## Author

**Nitin Joshi** · Data Analyst · Sarnia, ON → Toronto/Remote  
[LinkedIn](https://www.linkedin.com/in/nitinjoshi23) · [GitHub](https://github.com/Nitinj23)
