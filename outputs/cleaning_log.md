
## 1. List of Issues Found
During the initial profiling and audit of the raw dataset containing **912 initial records**, the following specific data quality issues were discovered:
* **Duplicate Records:** 20 completely identical system rows (exact duplicates) were found.
* **Conflicting Order IDs:** 24 rows shared duplicate `Order ID`s but contained conflicting transactional details (representing 12 unique Order IDs).
* **Missing Shipping Values:** 21 records lacked critical `Ship Mode` values.
* **Missing Regional Values:** 15 records were found with missing or blank `Region` attributes.
* **Missing Financial Values:** 9 records had missing or blank `Discount` indicators.
* **Logical Date Anomalies (Invalid Shipping):** 91 records had `Ship Date` chronologically preceding the `Order Date`.
* **Shipping Warnings:** 11 records triggered late delivery or shipping mode mismatch inconsistencies.
* **Sales/Profit Metrics Mismatch:** 88 records demonstrated mathematical discrepancies between reported Sales, Costs, and Profit Margin equations.

---

## 2. Cleaning Actions Performed
The following sequential data cleaning actions were executed to resolve the issues:
1. **Deduplication:** Removed exactly 20 fully identical structural rows using the Excel Deduplication tool, safely reducing the baseline to 892 records.
2. **Imputation for Missing Values:**
   * Filled 21 missing `ship_mode` blanks with `"Unknown"`.
   * Filled 15 missing `region` blanks with `"Unknown"`.
   * Treated 9 missing `discount` fields as `0` after ensuring all corresponding sales figures were validated.
3. **Flagging Chronological Inconsistencies:** Isolated 91 shipping anomaly records where execution dates logically conflicted with entry dates.
4. **Mathematical Balancing:** Verified and isolated 88 records exhibiting anomalous profit margin metrics to protect the baseline reporting layer.

---

## 3. Business Rules Applied
Per the explicit instructions outlines in *Task 5: Apply Business Rules*, the following constraints were enforced:
* **Rule Area: Missing region** -> Filled as `"Unknown"` and explicitly logged in this quality report.
* **Rule Area: Missing ship_mode** -> Filled as `"Unknown"` and explicitly logged in this quality report.
* **Rule Area: Missing discount** -> Treated as `0` strictly because corresponding core sales numeric fields were verified as valid.
* **Rule Area: Negative / Out-of-Range Discounts** -> Evaluated and flagged dynamically within the structural audit.
* **Rule Area: Cancelled & Failed Payment Orders** -> Excluded from contributing to any final completed sales operational summary tables to avoid revenue inflation.
* **Rule Area: Refunded / Returned Orders** -> Separated into an independent tracking summary row within the *Order Status Summary* (163 Returned rows documented).
* **Rule Area: Ship date before order date** -> Documented and flagged as invalid shipping records (91 counts locked).

---

## 4. Assumptions Made
* **Conflicting Duplicates Integrity:** Assumed that rows sharing identical `Order ID`s but carrying different item properties represent legitimate, complex multi-item orders or operational logging conflicts. They were **not deleted silently** to prevent severe data loss, but were safely flagged for management review.
* **Zero Discount Default:** Assumed blanks in the discount fields imply that no promotional code or markdown was applied during checkout, rather than systematic data deletion.

---

## 5. Records Removed
* **Total Rows Deleted:** **20 records**
* **Reasoning:** Exact system duplicate clones that offered no unique transactional value and artificially inflated unit sales metrics.

---

## 6. Records Flagged
* **Conflicting Order ID Records:** **24 records** (safely retained and highlighted using conditional formatting rules).
* **Invalid Shipping Anomaly Records:** **91 records** (flagged in the Date Issue Summary layer).
* **Calculation Mismatches:** **88 records** (flagged via custom evaluation formulas).

---

## 7. Limitations of Your Cleaning Process
* **Historical Source Inaccessibility:** Due to lack of access to live transaction logs or upstream databases, structural discrepancies (like the 91 invalid shipping dates or 88 profit mismatches) could only be flagged rather than auto-corrected.
* **Textual Ambiguity:** Imputing missing dimensions as `"Unknown"` preserves baseline integrity but limits granular segmentation until master-data lookup keys are restored.