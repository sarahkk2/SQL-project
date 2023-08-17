Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:SELECT city,  country,  SUM("productPrice") AS total_revenue
FROM all_sessions
GROUP BY city,  country
ORDER BY total_revenue DESC;



Answer:Country: United States
CityL: Mountain View




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
SELECT al.city, al.country, SUM(ss.total_ordered) AS total_ordered
FROM all_sessions AS al
JOIN sales_by_sku AS ss
ON al.productsku = ss.productsku
GROUP BY al.country, al.city 
ORDER BY total_ordered DESC;



SELECT CITY, AVG(total_ordered) AS AVERAGE_PRODUCTS
FROM customer_orders
GROUP BY CITY;



SELECT COUNTRY, AVG(total_ordered) AS AVERAGE_PRODUCTS
FROM customer_orders
GROUP BY COUNTRY;

Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:SELECT city,country, "v2ProductCategory", COUNT(*) AS product_count
FROM all_sessions
GROUP BY  city, country, "v2ProductCategory"
ORDER BY city, country,product_count DESC;



Answer:I do not see a pattern as all the numbers are quite scattered.





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries: WITH RankedProducts AS (
    SELECT city, country,"v2ProductName", COUNT(*) AS product_count,
        ROW_NUMBER() OVER (PARTITION BY city, country ORDER BY COUNT(*) DESC) AS rank
    FROM all_sessions
    GROUP BY
        city,
        country,
        "v2ProductName"
)
SELECT
    city,
    country,
    "v2ProductName",
    product_count
FROM
    RankedProducts
WHERE
    rank = 1
ORDER BY
    city,
    country;




Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:SELECT city,country,  SUM("productPrice") AS total_revenue
FROM all_sessions
GROUP BY city, country
ORDER BY total_revenue DESC;


Answer:







