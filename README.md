# Business Analytics Assignment — Part 1: Data Cleaning

## Problem Summary
This project involves cleaning and analysing an e-commerce orders dataset (`raw_orders.xlsx`). The goal is to produce a cleaned dataset, a quality audit report, and pivot-based business insights.

## Dataset Description
| Attribute | Value |
|-----------|-------|
| Source file | raw_orders.xlsx |
| Raw record count | 932 |
| Columns | 21 |
| Date range | 2024–2025 |
| Geographic scope | India (states & cities) |

**Columns:** order_id, order_date, ship_date, customer_id, customer_name, segment, region, state, city, category, sub_category, product_name, ship_mode, quantity, unit_price, discount, sales, cost, profit, payment_status, order_status

## Tools Used
- **Python 3** (pandas, openpyxl, python-dateutil)
- Data processing, cleaning, and Excel file generation handled entirely via Python scripts

## Cleaning Steps
1. **Text normalisation** — stripped whitespace, fixed case, removed special characters across all categorical columns
2. **Date standardisation** — parsed 4 date formats into YYYY-MM-DD; flagged missing, invalid, and illogical dates
3. **Duplicate removal** — removed 20 exact duplicates; flagged 12 conflicting duplicate order IDs for review
4. **Discount cleaning** — converted percentage strings, filled valid missing values with 0, flagged negatives and out-of-range values
5. **Missing value treatment** — filled missing region/ship_mode with "Unknown"; tracked with flags
6. **Calculated columns** — added calculated_sales, calculated_profit, profit_margin, shipping_delay_days, order_month, order_year, data_quality_flag

## Applied Business Rules
- Missing `region` → filled with `"Unknown"` and flagged
- Missing `ship_mode` → filled with `"Unknown"` and flagged
- Missing `discount` → set to `0` only when `quantity` and `unit_price` are valid
- Negative/invalid discounts → flagged as `Invalid`, excluded from calculations
- Orders with `Cancelled` status or `Failed` payment → excluded from completed sales totals

## Data Quality Summary
| Flag | Count |
|------|-------|
| Clean | 744 |
| Warning | 153 |
| Invalid | 15 |
| **Total** | 912 |

## Pivot Insights
- **Top sales region:** West
- **Top category by sales:** Technology
- **Highest profit-margin segment:** Corporate
- Monthly sales trend available in `pivot_summary.xlsx` → "Monthly Sales Trend" sheet
- Refunded/cancelled order distribution available in "Issues by Region" sheet

## Output Files
| File | Location | Description |
|------|----------|-------------|
| `cleaned_orders.xlsx` | `data/` | Cleaned dataset with all calculated columns |
| `data_quality_report.xlsx` | `outputs/` | 7-sheet audit report |
| `pivot_summary.xlsx` | `outputs/` | 6 pivot/summary tables |
| `cleaning_log.md` | `outputs/` | Detailed cleaning log |
| `README.md` | `/` | This file |

## Screenshots
> *(Insert screenshots here)*
- `screenshots/raw_data_preview.png` — Raw data preview
- `screenshots/cleaned_data_preview.png` — Cleaned data preview
- `screenshots/pivot_summary_1.png` — Pivot table 1
- `screenshots/pivot_summary_2.png` — Pivot table 2

## Repository Structure
```
studentname_studentid_part1_data_cleaning/
├── data/
│   └── cleaned_orders.xlsx
├── outputs/
│   ├── data_quality_report.xlsx
│   ├── pivot_summary.xlsx
│   └── cleaning_log.md
├── screenshots/
│   ├── raw_data_preview.png
│   ├── cleaned_data_preview.png
│   ├── pivot_summary_1.png
│   └── pivot_summary_2.png
└── README.md
```
