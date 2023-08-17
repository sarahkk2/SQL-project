Question 1: What is the percentage of visitors who actually make a purchase when visiting the site?

SQL Queries:

Answer: SELECT (COUNT(DISTINCT a.visitid) * 100.0) / NULLIF(COUNT(DISTINCT s.visitid), 0) AS purchase_percentage
FROM all_sessions AS s
LEFT JOIN analytics
AS a ON s.visitid = a.visitid;





Question 2: How does the average number of pages viewed per visitor correlate with revenue?

SQL Queries:

Answer: SELECT AVG(s.pageviews) AS avg_pages_viewed,
    SUM(a.revenue) AS total_revenue
FROMall_sessions AS s
LEFT JOIN analytics AS a 
ON s.visitid = a.visitid
GROUP BY  s.visitid;




Question 3: compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:

Answer:SELECT (COUNT(DISTINCT a.visitid) * 100.0) / NULLIF(COUNT(DISTINCT s.visitid), 0) AS purchase_percentage
FROM all_sessions AS s
LEFT JOIN analytics AS a ON s.visitid = a.visitid
WHERE  a.units_sold > 0;



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
