What are your risk areas? Identify and describe them.

Describe your QA process and include the SQL queries used to execute it.
	QA PROCESS: 



Conducted a thorough examination of the dataset to identify potential issues.
Detect and handle NULL values, ensuring data completeness.
Identify and manage duplicate records to maintain data accuracy.
Verify that the primary key contains distinct and unique values.
Modify data types and values where necessary, ensuring uniformity and accuracy.

Evaluate dataset adequacy for addressing the questions at hand.
Determine if there's sufficient data volume to support predictive analyses.
Assess potential impacts on sales reporting and future marketing strategies.
Gauge the potential for providing meaningful insights to front-end teams.
Ensure data collection aligns with objectives, yielding the desired granularity.

Identify outliers and implement strategies for their replacement or correction.
Employ aggregate functions to compute minimum and maximum revenue values.



SELEECT totaltransactions FROM all_sessions 
WHERE totaltransactions IS NULL 

SELECT fullvisitorid FROM all_sessions 
WHERE total transactions IS NULL 


SELECT 'all_sessions' as table_name, 
        COUNT(*) AS count_rows, 
        COUNT(DISTINCT(full_visitor_id)) AS count_distinct_id 
FROM all_sessions


SELECT 'products' as table_name, 
       COUNT(*) AS count_rows, 
       COUNT(DISTINCT(product_sku)) AS count_distinct_id
FROM products



SELECT MAX (total_ordered) FROM customer_orders


SELECT MIN (total_ordered) FROM customer_orders 
