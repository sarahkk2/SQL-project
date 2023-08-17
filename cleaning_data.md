What issues will you address by cleaning the data?
Duplicate records, deleting columns and ensuring we can use the data for further analysis 




Queries:
Below, provide the SQL queries you used to clean your data.


1.  The column productRefundAmount, itemQuantity, searchKeyword in the table 'all_sessions' has all NULL values and doesnt seem relevant to the data analysis and therefore deleting the columns


ALTER TABLE all_sessions 
DROP COLUMN "productRefundAmount";



ALTER TABLE all_sessions 
DROP COLUMN "itemQuantity";

ALTER TABLE all_sessions
DROP COLUMN "searchKeyword";


ALTER TABLE analytics
DROP COLUMN userid;

2. The column 'socialEngagementTypes' from the table analytics has 'Not Socially Engaged' in every row and making it repetitive and therefore no need for it. 


ALTER TABLE analytics
DROP COLUMN "socialEngagementType";

 

There are 15134 rows in the table all_sessions using the query 

SELECT COUNT (*) FROM all_sessions 
 In the columns transactions and  totalTranactionRevenue  there are about 81 rows where the values are NOT NULL. Thats a 0.005 % of information, and therefore deleting the columns. There are also other columns with less than 1% of information inputted 


ALTER TABLE all_sessions
DROP COLUMN "totalTransactionRevenue"


ALTER TABLE all_sessions
DROP COLUMN "transactions"



ALTER TABLE all_sessions
DROP COLUMN "sessionQualityDim";


ALTER TABLE all_sessions
DROP COLUMN "productQuantity" ;



ALTER TABLE all_sessions
DROP COLUMN "eCommerceAction_option" ;

REMOVING DUPLICATES:

SELECT DISTINCT "productSKU" FROM products



DELETE FROM all_sessions 
WHERE (fullvisitorID) IN (
    SELECT fullvisitorid
    FROM your_table
    GROUP BY fullvisitorid
    HAVING COUNT(*) > 1







PART 2: 

1. the naming conventions for the table made it difficult to retrieve certain columns so I named all the columns in lowercase. 
Using the following queries:  

2.  Ive renamed columns to match the other one as they contain the same information. Ive renamed "SKU' in products to productSKU.

ALTER TABLE products
RENAME COLUMN "SKU" TO "productSKU";


3. Ive updated the column city in the table 'all_sessions' where the city is 'not available in data demoset' to NULL using the following query:


UPDATE all_sessions 
SET city = NULL
WHERE city = 'not available in demo dataset'

4. The unitcost and the productprice were divided by 1,000,000: 

- UPDATE all_sessions
SET "productPrice" = "productPrice"/1000000


UPDATE analytics
SET unit_price = unit_price/1000000

5. Once divided by 1,000,000 in the above step, I rounded it to two decimal places as it references money. 

ALTER TABLE all_sessions 
ALTER COLUMN "productPrice" TYPE decimal(10, 2);

ALTER TABLE analytics
ALTER COLUMN "unit_price" TYPE decimal(10, 2);

6. Ive renamed columns to match the other one as they contain the same information. Ive renamed "SKU' in products to productSKU.

ALTER TABLE products
RENAME COLUMN "SKU" TO "productSKU";

7.  In the products table, the first row has NULL values for the columns "sentimentScore" and "sentimentMagnitude". I noticed it hasnt been ordered and therefore could be why there is value for it.

8. I was unable alter the time in the all_sessions table so I created another column with the time values in it and set it to the correct format. I assumed the original time was in seconds , I then dropped the original time column.   

ALTER TABLE all_sessions
ADD COLUMN time_column TIME;



UPDATE all_sessions
SET time_column  = TIME '00:00:00' + time * INTERVAL '1 SECOND';

ALTER TABLE all_sessions
DROP COLUMN "time";

