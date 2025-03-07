What are your risk areas? Identify and describe them.

## Data Integrity Issues:
Inconsistent or missing values (product_quantity, product_revenue) can lead to inaccurate analysis.
## Primary Key Conflicts: 
Duplicates in visit_id and other fields required additional handling to maintain referential integrity.
## Foreign Key Constraints:
Ensuring all referenced product_sku values exist in the products table before linking with sales_by_sku.

## Large Data Processing
Query performance could be impacted due to large datasets, requiring indexing and optimization.

## Data Cleaning Complexity
Handling noisy data from CSV files required significant preprocessing before analysis.


QA Process:
Describe your QA process and include the SQL queries used to execute it.
