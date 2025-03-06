# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The goal of this project is to design and structure a relational database that consolidates data from multiple sources, ensuring data integrity, creating appropriate relationships among tables, and enabling efficient queries for analysis. The primary objectives include:

### Creating Tables:
Create tables for data such as all_sessions, sales_by_sku, sales_report, products, and analytics.
Define the necessary fields and their data types, ensuring they meet the requirements for the project.

### Importing Noisy Data from CSV Files:
Import data from CSV files, which may contain noisy or inconsistent information.
Clean up and transform the data during the import process, addressing missing values, duplicates, and any incorrect data.

### Setting Primary and Foreign Keys:
Assign primary keys to tables like all_sessions and analytics using an id column for unique identification.
Set up foreign keys to create relationships between the tables, such as linking product_sku from all_sessions and sales_by_sku to the products table.

### Data Cleaning:
Clean the data by handling duplicates, missing values, and ensuring consistency across tables.
Make necessary updates and transformations to ensure data fits the required schema (e.g., altering data types or resolving duplicate rows).

### SQL Queries and Reporting:
Write SQL queries to summarize and analyze the data across multiple tables.
Generate reports based on business needs (e.g., top-selling products, revenue analysis, city/country comparisons).

### Process
I've reviewed the project instructions.
I've set up my repository.
I've downloaded the .csv files.
I've created the e-commerce database in PGAdmin.
I've created five tables within the e-commerce database.
CREATE TABLE all_sessions (
    full_visitor_id NUMERIC(20,0),
    channel_grouping TEXT,
    visit_time INT,
    country TEXT,
    city TEXT,
    total_transaction_revenue BIGINT,
    transactions INT,
    time_on_site INT,
    pageviews INT,
    session_quality_dim INT,
    visit_date DATE,
    visit_id BIGINT,
    visit_type TEXT,
    product_refund_amount BIGINT,
    product_quantity INT,
    product_price BIGINT,
    product_revenue BIGINT,
    product_sku VARCHAR(255), 
    product_name TEXT,
    product_category TEXT,
    product_variant TEXT,
    currency_code TEXT,
    item_quantity INT,
    item_revenue BIGINT,
    transaction_revenue BIGINT,
    transaction_id TEXT,
    page_title TEXT,
    search_keyword TEXT,
    page_path_level1 TEXT,
    ecommerce_action_type INT,
    ecommerce_action_step INT,
    ecommerce_action_option TEXT
);

CREATE TABLE sales_by_sku (
    product_sku VARCHAR(255),  
    total_ordered INT
);
CREATE TABLE sales_report (
    product_sku VARCHAR(255),
    total_ordered INT,
    name VARCHAR(255),
    stockLevel INT,
    restock_in_gLeadTime INT,
    sentiment_Score DECIMAL(20,10),
    sentiment_magnitude DECIMAL(20,10),
    ratio DECIMAL(20,10)
);
CREATE TABLE products (
    product_sku VARCHAR(255),
    name VARCHAR(255),
    ordered_Quantity INT,
    stockLevel INT,
    restock_in_gLeadTime INT,
    sentiment_Score DECIMAL(10, 10),
    sentiment_magnitude DECIMAL(10, 10)
);

-- update sentiment_Score
ALTER TABLE products
ALTER COLUMN sentiment_Score TYPE DECIMAL(20, 10);

-- Update sentiment_magnitude
ALTER TABLE products
ALTER COLUMN sentiment_magnitude TYPE DECIMAL(20, 10);
CREATE TABLE analytics (
    visitnumber INT,
    visitid BIGINT,
    visitstarttime BIGINT,
    date VARCHAR (25),
    fullvisitorid BIGINT,
    userid VARCHAR(255),
    channelgrouping VARCHAR(50),
    socialengagementtype VARCHAR(50),
    units_sold INT,
    pageviews INT,
    timeonsite INT,
    bounces INT,
    revenue BIGINT,
    unit_price BIGINT
);


### I've exported the .csv files into my tables.
### The data in the tables has been cleaned.
## I have set the primary/Foreign keys for the table:
ALTER TABLE products 
ADD PRIMARY KEY (product_sku);

ALTER TABLE sales_report 
ADD PRIMARY KEY (product_sku);

ALTER TABLE sales_report 
ADD CONSTRAINT fk_sales_report_product_sku
FOREIGN KEY (product_sku) REFERENCES products(product_sku);

ALTER TABLE sales_by_sku 
ADD PRIMARY KEY (product_sku);

ALTER TABLE sales_by_sku 
ADD CONSTRAINT fk_sales_by_sku_product_sku
FOREIGN KEY (product_sku) REFERENCES products(product_sku);

ALTER TABLE analytics
ADD COLUMN all_sessions_id INT;

ALTER TABLE analytics
ADD CONSTRAINT fk_analytics_all_sessions_id
FOREIGN KEY (all_sessions_id) REFERENCES all_sessions(id);


## Results
The analysis revealed key insights into top-selling products, regional revenue trends, and customer behavior. By linking data across tables, I identified which cities and countries generated the highest revenue, discovered regional sales patterns, and pinpointed popular product categories. Additionally, the customer behavior analysis showed trends in engagement, helping to optimize marketing and sales strategies. SQL queries were used to aggregate and clean the data, ensuring accurate insights that can guide future business decisions.

## Challenges 
Handling Missing or Inconsistent Data: One of the major challenges I faced was dealing with missing or inconsistent data in certain fields like city, country, and product_sku. To solve this, I had to clean the data by filling in missing values and ensuring that data was standardized for accurate analysis. In some cases, default values like "Not Set" or "Not Available" were used where information was missing.

Dealing with Duplicates: The presence of duplicate records, especially in visit_id and product_sku, made it challenging to aggregate and perform accurate analysis. I had to write SQL queries to identify duplicates and clean up the data, either by removing them or handling them in a way that wouldn't distort the analysis.

Complex Joins Between Tables: The data was spread across multiple tables, and joining these tables to get a complete picture was sometimes difficult. Ensuring that the right keys were linked (like product_sku in sales_report, sales_by_sku, and all_sessions) and correctly matching records was a challenge.

Creating and Managing Primary Keys: One of the significant challenges I encountered was establishing primary keys for tables, especially in the all_sessions and analytics tables. I had to ensure that the fields I selected for primary keys were unique and that there were no duplicates. In some cases, I faced issues like duplicated visit_id in the all_sessions table. Since the visit_id had duplicate entries, but the information for those duplicates was different, I couldn't remove them. To resolve this, I created a new column called id as the primary key in both the all_sessions and analytics tables. This allowed me to uniquely identify each record while keeping the existing data intact. This added complexity to the process of structuring the database and enforcing referential integrity.


Handling Large Volumes of Data: Some tables, especially all_sessions, contained a large volume of data, missing values like product_quantity and product_revenue.



## Future Goals
Improved Data Cleaning and Preprocessing: If I had more time, I would focus on further improving the data cleaning process. This would involve identifying and handling missing, inconsistent, or outlier data more thoroughly. I could also automate some of these cleaning tasks to save time and ensure consistent data quality.

Database Optimization: Given more time, I would work on optimizing the database performance. This could involve adding more indexes, partitioning large tables, or improving query performance to handle larger datasets more efficiently.

Better Linkage Between Tables: I could spend more time refining the relationships between tables, adding additional foreign keys where needed, and ensuring that all relationships are well-defined and optimized for efficient querying.
