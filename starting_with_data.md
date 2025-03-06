Question 1: 

SQL Queries:Display information from both tables where product_sku matches in both tables.

Answer: 

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



Question 2: 

SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
