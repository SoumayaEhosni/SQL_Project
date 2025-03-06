# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
(fill in your description and goals here)

## Process
### I've read the project instructions
### I've created my repository
### I've downloded the .csv files 
### I've created my e-commerce database in PGAdmin
### I've created my five tables under e-commerce database
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


### I've exported the .csv files to my tables


## Results
(fill in what you discovered this data could tell you and how you used the data to answer those questions)

## Challenges 
(discuss challenges you faced in the project)

## Future Goals
(what would you do if you had more time?)
