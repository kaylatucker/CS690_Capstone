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
