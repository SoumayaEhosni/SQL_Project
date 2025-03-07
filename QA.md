What are your risk areas? Identify and describe them.

## Data Integrity Issues:
Inconsistent or missing values (product_quantity, product_revenue) can lead to inaccurate analysis.
## Primary Key Conflicts: 
Duplicates in visit_id and other fields required additional handling to maintain referential integrity.
## Foreign Key Constraints:
Ensuring all referenced product_sku values exist in the products table before linking with sales_by_sku.

## Large Data Processing:
Query performance could be impacted due to large datasets, requiring indexing and optimization.

## Data Cleaning Complexity:
Handling noisy data from CSV files required significant preprocessing before analysis.


QA Process:
## Check for duplicates in primary key fields
# all_session table
   SELECT visit_id, COUNT(*)
   FROM all_sessions
   GROUP BY visit_id
   HAVING COUNT(*)>1;
   
ALTER TABLE all_sessions
ADD COLUMN id SERIAL PRIMARY KEY;
# analytics table
SELECT visit_id, COUNT(*)
FROM analytics
GROUP BY visit_id
HAVING COUNT(*) > 1;

ALTER TABLE analytics
ADD COLUMN id_analytics SERIAL PRIMARY KEY;

## Verify Foreign Key integrity
SELECT s.product_sku 
FROM sales_by_sku s
LEFT JOIN products p ON s.product_sku = p.product_sku
WHERE p.product_sku IS NULL;

ALTER TABLE sales_by_sku 
ADD CONSTRAINT fk_sales_by_sku_product_sku
FOREIGN KEY (product_sku) REFERENCES products(product_sku);

SELECT * FROM products WHERE product_sku = 'GGOEYAXR066128';

DELETE FROM sales_by_sku WHERE product_sku NOT IN (SELECT product_sku FROM products);

## Check for data consistency across tables
SELECT a.visit_id, s.transaction_id 
FROM all_sessions s
LEFT JOIN analytics a ON s.visit_id = a.visit_id
WHERE a.visit_id IS NULL;

## Handle Missing Values
UPDATE all_sessions
SET 
    total_transaction_revenue = CASE 
                                  WHEN total_transaction_revenue IS NULL THEN 0 
                                  ELSE total_transaction_revenue 
                                  END,
    transactions = CASE 
                  WHEN transactions IS NULL THEN 0 
                  ELSE transactions 
                  END,
	product_refund_amount = Case
								When product_refund_amount IS NULL THEN 0
								ELSE product_refund_amount
								END,
	time_on_site = Case
								When time_on_site IS NULL THEN 0
								ELSE time_on_site
								END,					
session_quality_dim = Case
								When session_quality_dim IS NULL THEN 0
								ELSE session_quality_dim
								END,					
item_quantity = Case
								When item_quantity IS NULL THEN 0
								ELSE item_quantity
								END;	







