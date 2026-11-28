# References

## Dataset:

Brazilian E-Commerce Public Dataset by Olist

Dataset page: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Notes:
- Contains approximately 100,000 e-commerce orders.
- Covers orders from 2016–2018.
- Includes information about orders, customers, sellers, products, payments,
  freight, reviews, and geography.
- Olist states that this is real commercial data.
- The dataset has been anonymized.
- Identifying references to companies and partners in review text were replaced.

---

## Planned research topics
1. Olist dataset provenance, public-use status, anonymization, and limitations
2. E-commerce customer satisfaction and online review scores
3. Delivery performance / delivery delay and customer satisfaction
4. Seller performance and marketplace KPIs
5. Freight/shipping cost and customer experience
6. Product/category effects in e-commerce
7. Geographic/logistics factors in marketplace performance
8. Statistical methods for analyzing seller performance and review outcomes

---

Impact of delivery performance on online review ratings: the role of temporal distance of ratings
- https://pmc.ncbi.nlm.nih.gov/articles/PMC9115748/
- Ravula, Prashanth. "Impact of Delivery Performance on Online Review Ratings: The Role of Temporal Distance of Ratings." Journal of Marketing Analytics, vol. 11, no. 2, 2022, p. 149, https://doi.org/10.1057/s41270-022-00168-5. Accessed 10 Nov. 2026. 
- Ravula (2022) examined how delivery performance influences online customer review ratings, particularly whether customers respond differently to early and late deliveries. Using e-commerce transaction data and Bayesian ordinal logistic regression on matched observations, the study found that late deliveries were associated with substantially lower ratings, while early deliveries produced relatively smaller improvements. Average ratings were 4.41 for early deliveries, 4.16 for on-time deliveries, and 3.45 for late deliveries. This supports the idea of *loss aversion*, where customers react more negatively to unmet delivery expectations than positively to deliveries that exceed expectations. The study also found that customers who waited longer after a late delivery before submitting a review tended to provide higher ratings, although this relationship was not statistically significant for early deliveries.
- These findings support my capstone's results showing that delivery reliability is strongly associated with customer satisfaction. My analysis similarly found that late deliveries corresponded with lower review scores, while the nonlinear logistic regression showed that dissatisfaction increased more sharply with severe delays. Ravula's research provides a theoretical explanation for these patterns and supports recommending that e-commerce businesses prioritize preventing late deliveries rather than simply delivering orders earlier than promised. The findings also highlight review timing as a possible influence on ratings, which my current models do not examine. However, because the study relied on observational data, its findings should be interpreted as associations rather than definitive evidence of causation.

Logistics Performance, Ratings, and Its Impact on Customer Purchasing Behavior and Sales in E-Commerce Platforms
- https://doi.org/10.1287/msom.2021.1045 
-Deshpande and Pendem (2022) examined how delivery performance affects logistics ratings, customer purchasing decisions, and third-party seller sales on e-commerce platforms. Using more than 15 million customer orders from Alibaba's Tmall platform and Cainiao logistics network, the researchers found that customers had strong expectations regarding delivery speed. Even without an explicitly promised delivery deadline, customers tended to give lower logistics ratings when deliveries took longer than two days. Customers who were promised one- or two-day delivery also gave lower ratings when those expectations were not met. The researchers estimated that reducing delivery times from three days to two days for affected orders could increase average daily third-party seller sales by 13.3% on the studied platform. These findings suggest that delivery performance influences not only customer satisfaction but also purchasing behavior and seller revenue.
- This research supports my capstone's findings that delivery reliability is an important factor associated with customer satisfaction and seller performance. My analysis found that higher seller late-delivery rates were consistently associated with lower average customer reviews, while the customer model showed increasing dissatisfaction as delivery delays became more severe. Deshpande and Pendem's findings provide additional business context by demonstrating how logistics ratings can influence purchasing decisions and sales. However, their research examined delivery speed and logistics-specific ratings, whereas my project primarily examines delays relative to estimated delivery dates and overall customer review scores. Additionally, my seller-sales regression had limited explanatory power, meaning my results cannot establish that faster deliveries increase seller revenue. Nevertheless, this research supports recommending that e-commerce platforms improve delivery reliability and evaluate its potential benefits alongside logistics costs.

Customer Satisfaction with E-Retailers: The Role of Product Type in the Relative Importance of Attributes Only abstract
- https://doi.org/10.1080/15332861.2016.1212314
- The study *Customer Satisfaction with E-Retailers: The Role of Product Type in the Relative Importance of Attributes* examines whether different aspects of e-retailer service contribute equally to customer satisfaction across product categories. Using neural networks, the researchers investigated the relative importance of service attributes while accounting for the fact that customer ratings of these attributes are often highly correlated. The study found that the importance of service attributes varies across convenience, shopping, and specialty goods. This suggests that customer satisfaction cannot necessarily be explained using the same priorities for every product category, and that retailers should consider product differences when allocating resources to improve customer experiences.
- These findings help explain the product-category differences observed in my Olist capstone analysis. My adjusted spline model found that office furniture had higher odds of receiving low reviews than several other product categories, even after accounting for delivery delay, freight percentage, and customer geography. The study provides a foundation for interpreting these differences because customers may evaluate their purchasing experiences differently depending on the products they buy. However, the article examines the relative importance of service attributes rather than the specific low-review probabilities measured in my project. Its findings support recommending that e-commerce businesses investigate category-specific customer expectations instead of applying identical improvement strategies across all product categories.

Understanding online product ratings: A customer satisfaction model
- https://doi.org/10.1016/j.jretconser.2015.07.010 
- Engler, Winter, and Schulz (2015) examined whether online product ratings primarily reflect product quality or broader customer satisfaction. Using a customer satisfaction model tested on two datasets of digital cameras and televisions from Amazon's German website, the researchers found that both customers' expectations before purchasing and actual product performance significantly influenced online ratings. Their findings suggest that ratings do not simply represent objective product quality but instead reflect how well a product meets customer expectations. The researchers also identified indications of reporting and behavioral biases, highlighting that online ratings contain information that cannot be fully explained by observable product characteristics.
- These findings are relevant to my Olist capstone because customer review scores serve as the primary measure of customer experience. My analysis found that delivery delays, product categories, and customer geography were associated with differences in review outcomes, but these factors do not explain every aspect of satisfaction. Engler and colleagues' research supports interpreting review scores as measures of perceived satisfaction rather than direct measures of product quality or delivery performance alone. This distinction is especially important when discussing the higher low-review odds observed for office furniture and other product categories, since customers' expectations and product experiences may also contribute to these differences. However, the study examined product-specific ratings, while my project uses overall order reviews, so its findings provide supporting context rather than a directly equivalent comparison.


Controlling the False Discovery Rate: A Practical and Powerful Approach to Multiple Testing
- https://doi.org/10.1111/j.2517-6161.1995.tb02031.x 
- Benjamini and Hochberg (1995) introduced the false discovery rate (FDR) correction to address the increased risk of false-positive findings when conducting multiple statistical tests. Unlike traditional methods that attempt to prevent any false positives, their approach controls the expected proportion of false discoveries among statistically significant results. This method provides a practical balance between identifying meaningful relationships and limiting incorrect conclusions. Although the research was published in 1995, it remains relevant as the foundational work establishing a statistical correction commonly used in modern research.
- This method was applied during the validation stage of my Olist capstone to assess the reliability of product-category and geographic differences in customer satisfaction. Because the adjusted logistic regression examined numerous categories and customer states, some statistically significant relationships could have occurred by chance. After applying the Benjamini–Hochberg correction to the adjusted spline model, 9 of 26 product-category comparisons and 6 of 17 customer-state comparisons remained statistically significant. These results helped distinguish stronger findings from less reliable associations and provided additional support for the product and geographic conclusions presented in the project. However, statistical significance after correction does not establish causation.

## Writing and Editing Tools

- **Grammarly.** (2026). [_Grammarly_](https://www.grammarly.com/). [Writing Assistant]

Used to polish text produced through speech-to-text dictation, improving grammar, punctuation, clarity, and readability. The original ideas, analysis, interpretations, and conclusions are my own.

- **Google.** (2026). [_Gemini_](https://gemini.google.com/) [Large language model]. 

Google Gemini was used to assist with drafting and formatting some Markdown cells in this notebook. I reviewed and edited the generated text before including it. I also used Google Colab’s code-completion/autocomplete feature when it suggested portions of code that matched what I intended to write. All code, analyses, and results were reviewed and verified by me.


- **GitHub.** (2026). [_GitHub Copilot_](https://github.com/features/copilot) [AI coding assistant].

Used to assist with debugging, writing some commit messages, resolving code errors, and adapting Jupyter notebooks from Google Colab to run locally in Visual Studio Code. This included updating file paths, addressing dependency issues, and improving code portability and reproducibility. All suggested changes were reviewed, tested, and verified by me to ensure consistency with the original analytical results.



