## 2026-09-07 — Project Setup and Initial Data Inspection

### Progress
- Completed the Ethical Data Use Agreement before beginning technical work.
- Finalized the project folder structure and Git/GitHub setup.
- Added the 9 raw Olist CSV files to `02_data/raw/`.
- Confirmed the Python environment works with the planned core libraries.
- Created and ran the initial data inspection notebook.
- Inspected table sizes, columns, data types, missing values, exact duplicates,
  expected keys, and date/time fields.
- Created Data Inventory v1 identifying core, supporting, and optional tables.

### Initial Data Findings
- All 9 Olist files loaded successfully.
- Most expected keys were unique.
- `review_id` is not unique in the raw reviews table; some review IDs are associated
  with multiple orders. No cleaning decision has been made yet.
- The geolocation table contains substantial duplication and cannot be joined
  directly as a one-row-per-ZIP lookup.
- Review comment fields contain substantial missing data.
- Some order date fields and product fields contain missing values.
- Date/time fields are currently stored as strings and will be converted later.

### Next Steps
- Complete the Confucianism discussion.
- Meet with the technical advisor for PSD2.
- Ask for feedback on project scope, seller-performance metrics, use of review score,
  and the planned analytical variables.
- Begin relationship validation and data preparation after PSD2.
- Return to background research later.


## 2026-09-22 — Relationship Validation and Data Preparation

### Progress
- Validated the main relationships between orders, order items, reviews, payments, sellers, products, and customers.
- Confirmed that all tested foreign-key relationships matched without unmatched IDs.
- Tested direct joins and confirmed that one-to-many relationships can multiply rows and inflate results.
- Reduced the geolocation table to one representative latitude/longitude per ZIP prefix.
- Confirmed that 98.70% of item-containing orders are single-seller, making single-seller orders a strong basis for seller-review analysis.
- Completed identifier, categorical, numeric, product, and date/time checks.
- Added English product-category translations and manually mapped the 2 categories missing from the translation table.
- Created the first derived variables for delivery performance and order-level value/freight measures.

### Data Findings
- Directly joining orders, items, reviews, and payments increased the dataset from 99,441 orders to 119,143 rows, confirming the need to aggregate before some joins.
- Some orders contain multiple items, reviews, and payment records.
- 775 orders have no item records, 768 have no review records, and 1 has no payment record.
- Geolocation contains 1,000,163 raw rows but only 19,015 unique ZIP prefixes.
- 1,278 item-containing orders are multi-seller; 97,388 are single-seller.
- Two product categories were absent from the translation table, affecting 13 products.
- Some unusual numeric and date values were identified, including zero-value payments, zero installments, zero product weights, inconsistent date sequences, and a few 2020 shipping-limit dates.
- 96,476 orders have valid delivery-based measures, including 7,827 late deliveries.

### Next Steps
- Meet with TA
- Do EDA
- Make final drafts of Data Quality Report
- Continue building analysis-ready order-level and seller-level datasets.
- Create seller-performance metrics.
- Build the customer-experience analysis dataset.
- Continue documenting cleaning decisions and unresolved anomalies.
- Review extreme values during exploratory analysis rather than removing them automatically.
- Return to background research before final analysis and reporting.

## 2026-09-29 — Customer Experience Dataset and Data Quality Report Preparation

### Progress
- Completed the customer-experience analysis dataset at the order level.
- Aggregated reviews to one review score per order before joining.
- Created order-level product/category measures, including product count, category count, and a representative primary category.
- Identified seller count for each order and assigned seller characteristics only to single-seller orders.
- Added customer geography and selected seller characteristics to the order-level dataset.
- Validated that the final customer-experience dataset contains 99,441 rows, 99,441 unique order IDs, and no duplicate orders.
- Exported `customer_experience.csv` to `02_data/processed/` and saved the completed notebook to GitHub.
- Began the Data Information and Quality Report notebook.
- Created dataset-dimension, missingness, summary-statistics, review-score, late-delivery, and data-quality summaries.
- Created initial exploratory visualizations, including review-score distribution and average review score by delivery status.
- Prepared a compact data-quality issues table for use in the final report.

### Data Findings
- 98,673 orders have an aggregated review score; 768 orders have no review score.
- 98,666 orders contain item records; 775 orders have no item records.
- 97,388 item-containing orders are single-seller and 1,278 are multi-seller.
- Seller characteristics are unavailable for 2,053 orders: 775 orders without item/seller information plus 1,278 multi-seller orders.
- 2,965 orders do not have valid delivery-based measures because customer delivery dates are missing.
- Customer state is available for all 99,441 orders.
- Primary product category is missing for 2,164 orders because some orders have no item records or contain products with missing category information.
- Initial EDA showed an average review score of approximately 4.29 for on-time orders compared with 2.57 for late orders.
- The delivery/review relationship is an exploratory association and does not establish causation.

### Next Steps
- Finish formatting and writing the Data Information and Quality Report.
- Submit PSD3.
- Begin more detailed seller-performance and customer-experience EDA.
- Use the EDA results to determine appropriate statistical methods for later analysis.
- Continue documenting important project decisions and limitations.


## 2026-10-06 — Seller EDA, Customer EDA, and Initial Baseline Analysis

### Progress
- Completed seller-level exploratory data analysis using `seller_metrics.csv`.
- Examined seller order volume, items sold, total sales, product/category variety, freight, review scores, late-delivery rates, observation counts, and seller geography.
- Confirmed that seller activity and monetary measures are strongly right-skewed.
- Completed customer-experience EDA using `customer_experience.csv`.
- Examined review score in relation to delivery status, delivery delay, order value, freight percentage, product category, seller characteristics, and geography.
- Identified delivery performance as the clearest descriptive relationship with customer review score.
- Reviewed candidate statistical methods based on the distributions and variable types observed during EDA.
- Completed an initial customer-experience baseline using delivery status and delivery delay.
- Completed an initial seller-performance baseline using total sales and selected seller characteristics.
- Documented the baseline results and limitations in `09_methods_and_baseline.ipynb`.

### Findings
- Seller activity is highly concentrated among a relatively small number of sellers. Median seller order count is 6, compared with a maximum of 1,854.
- Median seller total sales are about 821 BRL, while the maximum exceeds 229,000 BRL.
- Seller review scores are generally high, with a median seller average review of about 4.24.
- Seller late-delivery rates are generally low, but review and delivery measures can be unstable for sellers with limited transaction histories.
- 1,329 sellers have fewer than 5 reviewed orders and 1,353 have fewer than 5 valid delivery observations.
- Most sellers are relatively specialized: the median seller offers 4 products and operates in 1 product category.
- Seller geography is highly concentrated in São Paulo, which contains 1,849 of the 3,095 sellers.
- Customer review scores have a mean of 4.09 and median of 5.
- On-time orders average about 4.29 review points compared with 2.57 for late orders.
- The customer baseline showed a 1.72-point average review difference between on-time and late orders.
- A Mann-Whitney U test found a statistically significant difference in review-score distributions between on-time and late orders.
- Delivery delay and review score had a Spearman correlation of -0.176, indicating a relatively weak negative monotonic relationship.
- Product category showed some variation in customer reviews, including an average of about 4.46 for `books_general_interest` and 3.63 for `office_furniture` among categories with at least 500 orders.
- Order value showed some variation across review groups, while freight percentage showed comparatively little.
- Same-state customer/seller orders averaged about 4.23 compared with 4.06 for different-state orders.
- Seller total sales had strong positive Spearman relationships with seller order count (0.853) and product count (0.786), and moderate relationships with category count (0.506) and average item value (0.490).

### Next Steps
- Prepare PSD4 using the strongest EDA findings and the initial baseline results.
- Continue evaluating which relationships are important enough to carry into formal analysis.
- Compare future improved methods against the simple customer-experience and seller-performance baselines.
- Consider sensitivity analyses using minimum seller observation thresholds when review or late-delivery rates are central to the analysis.
- Continue documenting limitations related to skewness, geographic imbalance, small seller sample sizes, and non-causal interpretation.
