# Retail Sales & Business Performance Dashboard (Excel)

Sumerix Global - Data Analytics & Business Intelligence Internship, **Task 1**

## Project overview
A retail company collects daily sales from several regions but has no reporting system. This project cleans the raw sales data, organises it in an Excel Table, summarises it with pivot-style reports, and presents an interactive executive dashboard with business recommendations.

## Dataset
Synthetic practice dataset (generated with `documentation/01_make_raw.py`) that mimics a retail/Superstore dataset: 1,240 raw rows, 13 columns (orders, customers, segments, regions, categories, products, quantity, price, cost, discount) for calendar year 2024. Currency is assumed INR. It deliberately contains typical quality problems so the cleaning steps are meaningful.

## Folder structure
```
Retail-Sales-Analytics/
├── dataset/             Raw_Data.xlsx, Cleaned_Data.xlsx
├── Excel Dashboard/     Retail_Sales_Analytics.xlsx   <- main deliverable
├── Report/              Project_Report_Sumerix_Global_Task1, dashboard.png
└── README.md
```

## Workbook sheets
| Sheet | Purpose |
|---|---|
| Dashboard | KPI cards, 5 charts, Region and Category drop-down filters, live insights |
| Executive_Summary | Findings and recommendations |
| Pivot_Tables | Monthly, category, product, segment, region summaries + Region x Category matrix + cross-checks |
| Cleaned_Data | Excel Table `tblSales`, formula columns, data validation, conditional formatting |
| Raw_Data | Untouched original data |
| Cleaning_Log | Every issue found, count, action taken, business rules |
| Lookups | Drop-down lists and the editable High-value threshold |

## Data cleaning summary
| Issue | Records | Action |
|---|---|---|
| Exact duplicate rows | 40 | Removed |
| Inconsistent case / spaces (Region, Segment, Category) | 392 | TRIM + proper case |
| Text dates in 3 formats | 962 | Converted to real dates (dd-mm-yyyy) |
| Unit_Price stored as text with "$" | 179 | Converted to numbers |
| Missing Customer_Name / Region | 25 / 20 | Filled from the customer's other orders |
| Missing Unit_Price | 15 | Filled with the product list price |
| Missing Discount | 30 | Assumed 0% |
| Missing Quantity or Order_Date | 13 | Rows removed (not recoverable) |

Result: **1,187 clean rows**, no blanks.

## Excel functions used
`SUM, ROUND, IF, IFERROR, MONTH, SUMIFS, COUNTIFS, INDEX, MATCH, MAX, ROWS, COUNTA`
Revenue = Qty x Unit Price x (1 - Discount); Profit = Revenue - Qty x Unit Cost (all formulas, no hard-coded results).

## Key results (full year, no filters)
- Revenue **571,720**, profit **151,783**, margin **26.5%**, **1,187** orders, average order value **482**
- Highest region: **West** (160,296; 28.0%); lowest: **Central** (47,220)
- Best products by revenue: **Laptop, Smartphone, Standing Desk**
- Best months: **Nov, Sep, Dec**; Q4 = 29.8% of revenue
- 10 orders sold at a loss; deep discounts (30%) cut margin sharply

## Recommendations
1. Approval rule for discounts above 20%.
2. Build inventory and staffing before the Q4 peak; run promotions in weak months.
3. Protect West; run a targeted campaign in Central.
4. Promote high-margin products; review pricing/cost of low-margin ones.
5. Loyalty/bundle offers for the largest (Consumer) segment.

## How to use the dashboard
Open `excel/Retail_Sales_Analytics.xlsx` -> **Dashboard**. Use the yellow Region and Category drop-downs; KPIs, charts and insights update. Cross-checks on `Pivot_Tables` (cells J16:N20) should all read **OK**.

## Validation
Totals were checked three ways: Excel formulas, an independent pandas calculation, and the Region x Category matrix grand total. All match (571,720.25 revenue). A filtered test (West + Technology) also matched exactly.

## Assumptions and limitations
- Synthetic data; currency assumed INR.
- Summaries are formula-driven (SUMIFS) rather than native PivotTables, and filtering uses drop-downs instead of slicers/timelines - see `documentation/Native_PivotTables_and_Slicers_Guide.md` to add them in Excel (5-10 minutes).
- Executive summary text is written from the unfiltered data; re-write it if you swap the dataset.
