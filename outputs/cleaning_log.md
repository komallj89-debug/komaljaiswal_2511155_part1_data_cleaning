# Data Cleaning Log — raw_orders.xlsx

## Overview
- **Source file:** raw_orders.xlsx  
- **Raw records:** 932  
- **Post-cleaning records:** 912  
- **Records removed:** 20 (exact duplicates)

---

## Issues Found

### Text / Category Inconsistencies
- Multiple case variants across `segment`, `region`, `category`, `sub_category`, `ship_mode`, `payment_status`, `order_status` (e.g., "CONSUMER", "consumer", "Consumer")
- Leading/trailing/double spaces in many text columns
- Variant spellings: "Small  Business", "Standard  Class", "Office  Supplies"

### Date Issues
- Four different date formats detected: `DD Mon YYYY`, `MM/DD/YYYY`, `DD-MM-YYYY`, `YYYY-MM-DD`
- 94 records where ship_date precedes order_date
- Total date flags raised: 94

### Duplicate Records
- 20 exact duplicate rows identified
- 12 order_ids found with conflicting data across rows

### Discount Issues
- 18 missing discount values
- 15 negative or invalid discount values
- Some discounts expressed as percentage strings (e.g., "70%")

### Missing Values
- region: 25 missing
- ship_mode: 21 missing
- discount: 18 missing (in original raw data)

---

## Actions Performed

- TEXT CLEANING: Removed extra/leading/trailing whitespace from all text columns.
- TEXT CLEANING: Fixed case inconsistencies (title case) across segment, region, category, sub_category, ship_mode, payment_status, order_status.
- TEXT CLEANING: Standardized 'Small Business', 'Home Office', 'Standard Class', 'Office Supplies' variants.
- TEXT CLEANING: Removed unwanted special characters from text fields.
- DATE CLEANING: Standardized all dates to YYYY-MM-DD format. Formats found: 'DD Mon YYYY', 'MM/DD/YYYY', 'DD-MM-YYYY', 'YYYY-MM-DD'.
- DATE CLEANING: 94 records flagged where ship_date < order_date.
- DATE CLEANING: Total date issues flagged: 94.
- DUPLICATES: 20 exact duplicate rows found and removed.
- DUPLICATES: 12 order_ids with conflicting data found — 24 rows flagged for review (not removed).
- BUSINESS RULES: 25 missing region values filled with 'Unknown'.
- BUSINESS RULES: 21 missing ship_mode values filled with 'Unknown'.
- DISCOUNT: 18 missing discounts filled with 0 (valid sales data present).
- DISCOUNT: 15 negative/invalid discount values flagged.
- CALCULATED COLUMNS: Added calculated_sales, calculated_profit, profit_margin, shipping_delay_days, order_month, order_year, data_quality_flag.
- DATA QUALITY: Clean=744, Warning=153, Invalid=15.
- BUSINESS RULES: Rows with Failed payment or Cancelled order excluded from completed sales calculations.

---

## Business Rules Applied

- Cancelled/Failed payment orders excluded from completed sales calculations.
- Missing discount → 0 (only if quantity and unit_price are valid).
- Missing region → "Unknown" with flag.
- Missing ship_mode → "Unknown" with flag.

---

## Assumptions Made

- ASSUMPTION: Ambiguous dates (e.g., 06/08/2024) parsed as MM/DD/YYYY (US format).
- ASSUMPTION: Missing ship/order dates are flagged but rows are retained for review.
- ASSUMPTION: Missing region and ship_mode filled with 'Unknown' per business rules.
- ASSUMPTION: Discount values expressed as percentages (e.g., '70%') converted to decimals (0.70).
- ASSUMPTION: Negative discounts flagged as invalid; not applied in calculations.

---

## Records Summary
| Category | Count |
|----------|-------|
| Raw records | 932 |
| Exact duplicates removed | 20 |
| Conflicting duplicates flagged (kept) | 24 |
| Final record count | 912 |
| Clean records | 744 |
| Warning records | 153 |
| Invalid records | 15 |

