

## 1. Problem Summary
The objective of this project was to perform comprehensive data cleaning, quality auditing, and exploratory data analysis on a raw sales dataset to ensure data integrity for business reporting and decision-making.

## 2. Dataset Description
The raw dataset comprised **912 initial records** covering various sales transactions, including regional data, shipping information, financial metrics, and order statuses.

## 3. Tools Used
* **Microsoft Excel:** Used for data profiling, cleaning, deduplication, pivot table analysis, and visualization.
* **Markdown:** Used for documentation (`README.md` and `cleaning_log.md`).

## 4. Cleaning Steps Performed
* **Deduplication:** Removed 20 exact duplicate system rows.
* **Imputation:** Filled missing values in `Ship Mode` and `Region` with "Unknown" and `Discount` with 0.
* **Flagging:** Identified and flagged 91 records with invalid shipping dates (shipping date preceding order date).
* **Validation:** Verified calculation accuracy for 88 records showing profit/sales discrepancies.

## 5. Business Rules Applied
* Missing `Region` & `Ship Mode` were filled as "Unknown".
* Missing `Discount` was treated as 0 (validated against sales).
* Cancelled and failed payment orders were excluded from final sales summaries.
* Refunded orders were tracked in a separate `Order Status Summary`.

## 6. Summary of Data Quality Issues Found
* 20 exact duplicate rows.
* 24 records with conflicting transactional details across 12 shared Order IDs.
* 91 records with logical date inconsistencies.
* 88 records with mathematical profit/sales mismatches.

## 7. Summary of Final Pivot Reports
* Regional performance analysis (Sales/Profit).
* Category/Sub-category breakdown (Sorted).
* Ship mode efficiency reports.
* Customer segment profit margins.
* Monthly sales trends and Order Status summaries.

## 8. Key Business Insights
* Identification of high-risk shipping anomalies that may impact delivery SLAs.
* Clear visibility into cancelled/returned orders allowing for better operational planning.
* Accurate financial reporting achieved by separating flagged/invalid records from clean sales data.

## 9. Assumptions and Limitations
* **Assumptions:** Conflicting Order IDs were retained for management review rather than deleted to avoid data loss. Missing discounts were assumed to be zero-discount transactions.
* **Limitations:** Unable to perform root-cause analysis on upstream data entry errors due to lack of access to original transactional logs.

## 10. Screenshots


* **Raw Data Preview:** ![Raw Data](raw_data_preview.png)
* **Cleaned Data Preview:** ![Cleaned Data](cleaned_data_preview.png)
* **Pivot Summary 1 (Category Breakdown):** ![Pivot 1](pivot_summary_1.png)
* **Pivot Summary 2 (Order Status):** ![Pivot 2](pivot_summary_2.png)
