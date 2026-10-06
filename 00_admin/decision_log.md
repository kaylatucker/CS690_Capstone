## 2026-09-07

- Keep the main project focus on seller performance and customer experience.
- Use review score as the primary customer-experience measure for now.
- Treat orders, order items, reviews, sellers, products, and customers as core tables.
- Treat category translation and geolocation as supporting tables.
- Keep payments optional unless they add meaningful value later.
- Do not assume `review_id` is unique and do not remove duplicated review IDs
  until their structure is investigated further.
- Do not join the raw geolocation table directly to sellers or customers because
  ZIP-code prefixes occur many times.
- Keep raw CSV files unchanged in `02_data/raw/`.
- Defer background/literature research for now and return to it later.
- Prioritize a cohesive business-analysis project rather than adding tools only
  for the sake of using more tools.

## 2026-09-22

- Keep order-level, item-level, and seller-level datasets separate where appropriate rather than creating one universal joined table.
- Aggregate reviews and payments to the order level before joining when order-level analysis is required.
- Reduce geolocation to one representative latitude/longitude per ZIP prefix before geographic joins.
- Use only single-seller orders when attributing order-level review scores to individual sellers.
- Preserve both Portuguese and English product-category fields.
- Manually map `pc_gamer` and `portateis_cozinha_e_preparadores_de_alimentos` because they are missing from the provided translation table.
- Leave products with no original product category as missing rather than assigning an artificial category.
- Retain valid zero freight values because they may represent free shipping.
- Flag unusual payment, product-weight, and timestamp values for later review rather than automatically deleting or correcting them.
- Treat logically impossible delivery durations as missing when creating duration-based features.
- Leave late-delivery status missing when an actual delivery date is unavailable rather than classifying the order as not late.
- Keep extreme delivery times and freight percentages for EDA before deciding whether any outlier treatment is necessary.

## 2026-09-29

- Use `review_score` aggregated to one value per order as the primary customer-experience outcome.
- Keep the customer-experience analysis dataset at one row per order.
- Represent order-level product characteristics with product count, category count, and a representative primary category rather than joining raw item rows directly.
- Keep `category_count` separately so the representative primary category is not interpreted as meaning an order contained only one category.
- Assign seller characteristics only to single-seller orders; leave seller-specific fields missing for multi-seller orders.
- Do not use `seller_average_review` as a predictor in the customer-experience dataset because it is derived from the same review outcome and could create circularity.
- Do not use seller-level late-delivery rate as a main customer-experience predictor when order-level delivery measures are already available.
- Retain orders with missing reviews, item records, delivery dates, or seller attribution rather than deleting them from the master customer-experience dataset.
- Keep customer and seller geography primarily at the state level for now; more detailed geographic measures can be added later if they provide analytical value.
- Treat the customer-experience and seller-performance datasets as separate analysis-ready tables rather than combining them into one universal dataset.
- For report visualization only, rounded order-level average review scores may be displayed on the original 1–5 scale; the underlying unrounded values remain unchanged.
- Use the average review score by delivery status as the main exploratory chart for the Data Information and Quality Report because it directly relates to the research question.
- Use a compact data-quality issues table in the report rather than including every cleaning result or anomaly.
- Keep unusual values and outliers for later EDA unless analysis provides a documented reason for exclusion.

## 2026-10-06

- Keep `review_score` as the primary customer-experience outcome.
- Treat delivery performance as a primary customer-experience factor because it showed the clearest relationship with review score during EDA.
- Use nonparametric methods where appropriate because review scores are ordinal and many project variables are strongly skewed.
- Use Mann-Whitney U for the initial two-group comparison of on-time and late review-score distributions.
- Use Spearman correlation for initial continuous-variable relationships because it is less dependent on normality and linear relationships.
- Use `seller_total_sales` as the initial seller-performance baseline outcome.
- Treat seller order count, product count, category count, and average item value as baseline seller characteristics.
- Keep the customer baseline intentionally simple so later multivariable methods can be compared against it.
- Retain all sellers in descriptive EDA rather than automatically excluding low-volume sellers.
- For analyses that rely heavily on seller average review or late-delivery rate, consider sensitivity analyses requiring at least 5 or 10 eligible observations.
- Do not treat statistically significant results as automatically important; consider effect size, descriptive differences, sample size, and business relevance.
- Do not interpret EDA, correlations, or baseline comparisons as causal relationships.
- Use median values when describing heavily skewed variables such as order value and freight percentage where appropriate.
- Restrict category/state comparisons to groups with sufficient observations when necessary to avoid emphasizing unstable averages from very small groups.
- Carry delivery performance, order value, category, seller characteristics, and geography forward as candidate explanatory factors for later multivariable analysis.
