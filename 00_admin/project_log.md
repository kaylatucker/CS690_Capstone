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
