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
                  END;
