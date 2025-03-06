Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
SELECT country, city, SUM(transaction_revenue) AS total_transaction_revenue
FROM all_sessions
GROUP BY country, city
ORDER BY total_transaction_revenue DESC;



Answer:
This returns the list countries, cities that have the highest total transaction revenue.



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
SELECT country, city, AVG(product_quantity) AS avg_products_ordered
FROM all_sessions
GROUP BY country, city
ORDER BY avg_products_ordered DESC;


Answer: This provides the average number of products ordered by visitors in each city and country.





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
SELECT country, city, product_category, COUNT(*) AS category_count
FROM all_sessions
GROUP BY country, city, product_category
ORDER BY country, city, category_count DESC;



Answer:
This showa the frequency of each product category ordered in each city and country. We can identify patterns by looking at:

1- Which product categories are most popular in certain regions.
2- Whether certain categories dominate sales in specific areas, which might indicate regional preferences or trends.





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

WITH RankedProducts AS (
    SELECT country, city, product_sku, product_name, SUM(product_revenue) AS total_revenue,
           ROW_NUMBER() OVER (PARTITION BY country, city ORDER BY SUM(product_revenue) DESC) AS rank
    FROM all_sessions
    GROUP BY country, city, product_sku, product_name
)
SELECT country, city, product_sku, product_name, total_revenue
FROM RankedProducts
WHERE rank = 1
ORDER BY country, city;

Answer: this displays the top-selling product in terms of revenue for each city and country.





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT country, city, SUM(transaction_revenue) AS total_revenue
FROM all_sessions
GROUP BY country, city
ORDER BY total_revenue DESC;

Answer:
This shows the total revenue generated from each city and country, ordered from the highest to the lowest. This allows to quickly see which cities and countries contribute the most to the overall revenue.

By analyzing this result, we can gain insights into:

1- Which cities or countries are the biggest revenue generators.
2- How the revenue is distributed geographically.
3- Identifying high-revenue areas that may require more resources or attention.






