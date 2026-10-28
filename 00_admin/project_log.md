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

## 2026-10-14 — Baseline Implementation, Evaluation, and Checkpoint

### Progress
- Completed the formal baseline implementation and evaluation in `09_methods_and_baseline.ipynb`.
- Added a rank-biserial effect size to the on-time versus late customer-review comparison.
- Created a compact customer baseline summary and baseline visualization.
- Evaluated whether the delivery/review relationship remained consistent within major product categories and customer states.
- Incorporated instructor feedback from the Data Information and Quality Report by checking the delivery relationship within category and geographic subgroups.
- Completed a seller sensitivity analysis comparing the full seller population with sellers having at least 10 orders.
- Documented baseline limitations and identified what the later improved analysis will need to address.

### Findings
- The customer baseline contains 95,830 orders with valid review and delivery-status information.
- On-time orders averaged 4.29 review points compared with 2.57 for late orders, a difference of 1.72 points.
- The on-time/late comparison had a rank-biserial effect size of 0.554, supporting practical importance beyond statistical significance.
- The delivery/review relationship remained consistent across all 19 product categories that met the analysis thresholds; category review gaps ranged from 1.21 to 1.99 points.
- On-time orders also had higher average reviews in all 14 qualifying customer states; state review gaps ranged from 1.39 to 2.11 points.
- The seller sensitivity analysis retained 1,271 sellers with at least 10 orders.
- Seller order count remained strongly related to total sales in the sensitivity sample (`rho = 0.753`).
- Product count remained positively related to sales but weakened from 0.786 to 0.558.
- Category count weakened substantially from 0.506 to 0.245.
- Average item value remained moderately related to sales and increased slightly from 0.490 to 0.532.
- The seller results show that some full-sample relationships are influenced by the large number of low-volume sellers.

### Next Steps
- Begin the mid-semester presentation on October 19 using the strongest project findings developed so far.
- Select the strongest preliminary visuals for the presentation.
- Present the current project story, baseline results, limitations, and next analytical steps clearly.
- Prepare for the next TA meeting and PSD5.
- Begin improved analysis only after the mid-semester presentation block, according to the project timeline.

## 2026-10-28 — Mid-Semester and PSD5 Feedback

### Progress
- Reviewed instructor feedback from PSD5 and the mid-semester presentation.
- Confirmed that the customer-experience analysis should move into a multivariable modeling stage.
- Identified changes needed for how seller performance is defined and reported.
- Clarified how the delivery-delay correlation should be described in the final report.
- Identified an additional figure to create from the category/state robustness results.

### Feedback and Direction
- The seller relationship between total sales and order count should not be presented as a major finding because total sales is calculated across orders, making the relationship expected by construction.
- Seller performance should be represented using measures that are less mechanically tied to order volume, such as average order value, late-delivery rate, or average review score.
- For the improved customer-experience analysis, model low review scores or the ordered review-score outcome using delivery delay along with controls such as product category, region, and freight.
- Report the effect of delivery delay using an odds ratio with a confidence interval.
- Show predicted probabilities or shares of low reviews at selected delivery-delay values so the practical size of the effect is easier to interpret.
- When reporting the original Mann-Whitney baseline, include the group medians and effect size rather than relying on the p-value alone.
- Clarify that the existing delivery-delay Spearman correlation uses all orders with valid delivery information, including early, on-time, and late deliveries.
- Create a dedicated visual showing that on-time reviews were higher across all 19 qualifying product categories and all 14 qualifying customer states.

### Next Steps
- Refine the seller-performance measures before final analysis.
- Implement the improved customer-experience regression analysis.
- Compare the improved model with the baseline and interpret practical effect sizes.
- Create the category/state robustness figure.
- Keep the final presentation deadline of December 6 and written report deadline of December 11 visible in the remaining project schedule.
- Treat SQL or dashboard work as optional and only pursue it after the analysis and report are secure.
