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
