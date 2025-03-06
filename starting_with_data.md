Question 1: Display information from both tables where product_sku matches in both tables.

SQL Queries:
SELECT 
    sr.product_sku, 
    sr.name, 
    sr.total_ordered, 
    sr.stockLevel AS stockLevel_report, 
    sr.restock_in_gLeadTime AS restock_ing_LeadTime_report, 
    sr.sentiment_Score AS sentiment_Score_report, 
    sr.sentiment_magnitude AS sentiment_magnitude_report,
    sr.ratio,
    p.ordered_Quantity, 
    p.stockLevel AS stockLevel_product,
    p.restock_in_gLeadTime AS restock_ing_LeadTime_product,
    p.sentiment_Score AS sentiment_Score_product,
    p.sentiment_magnitude AS sentiment_magnitude_product
FROM sales_report sr
JOIN products p 
ON sr.product_sku = p.product_sku;

Answer: This joins the sales_report and products tables on the product_sku column and displays several fields from both tables.


Question 2: Select Products with Low Stock Level (stockLevel < 100)

SQL Queries:
SELECT 
    sr.product_sku, 
    sr.name, 
    sr.stockLevel AS stockLevel_report, 
    p.stockLevel AS stockLevel_product
FROM sales_report sr
INNER JOIN products p 
    ON sr.product_sku = p.product_sku
WHERE sr.stockLevel < 100 OR p.stockLevel < 100;

Answer:This returns products that have a low stock level in either of the tables.



Question 3: Select Products Not in sales_report

SQL Queries:
SELECT 
    p.product_sku, 
    p.name
FROM products p
LEFT JOIN sales_report sr 
    ON p.product_sku = sr.product_sku
WHERE sr.product_sku IS NULL;

Answer: This returns products that are not in the sales report.



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
