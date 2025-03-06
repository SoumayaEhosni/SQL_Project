What issues will you address by cleaning the data?





Queries:
--to clean analytics table
UPDATE analytics
SET unit_price = unit_price / 1000000;

--to clean products table
UPDATE products
SET sentiment_magnitude = 0
WHERE sentiment_magnitude IS NULL;

--to clean all_sessions table
UPDATE all_sessions
SET product_price = product_price / 1000000;

UPDATE all_sessions
SET city = country
WHERE city IN ('(not set)', 'not available in demo dataset');

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
								 WHEN  time_on_site IS NULL THEN 0
								ELSE time_on_site
								END,					
    session_quality_dim = Case
								WHEN  session_quality_dim IS NULL THEN 0
								ELSE session_quality_dim
								END,					
     item_quantity = Case
								 WHEN  item_quantity IS NULL THEN 0
								ELSE item_quantity
								END;
--To clean from sales_by_sku products that are not in product
DELETE FROM sales_by_sku WHERE product_sku NOT IN (SELECT product_sku FROM products);
