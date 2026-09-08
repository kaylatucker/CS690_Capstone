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
