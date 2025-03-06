What issues will you address by cleaning the data?





Queries:
Queries to clean analytics table
UPDATE analytics
SET unit_price = unit_price / 1000000;

Queries to clean products table
UPDATE products
SET sentiment_magnitude = 0
WHERE sentiment_magnitude IS NULL;
