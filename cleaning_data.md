What issues will you address by cleaning the data?
1. Dropping irrelevant column
2. Address missing or inconsistent data
3. Converting column to their appropriate datatypes where necessary
4. Replace NULL values where necessary




Queries:
Below, provide the SQL queries you used to clean your data.

**--Drop  Sentimentsore and sentimentmagnitude From product Table due to Unwanted or Irrelavent Observations**
ALTER TABLE products
DROP COLUMN sentimentscore;

ALTER TABLE products
DROP COLUMN sentimentmagnitude;

**--Drop Userid From analytics table due to NULL values**
ALTER TABLE analytics
DROP COLUMN userid;

**--UPDATE analytics table to convert NULL values to zero values on units_sold**
UPDATE analytics
SET units_sold = 0
WHERE units_sold IS NULL;


**-- COnvert visitstatrttime column  to TO_Timestamp data type**
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE timestamp
USING To_timestamp(visitstarttime);


**--Convert Timeonsite to Integer**
ALTER TABLE analytics ALTER COLUMN timeonsite TYPE integer USING (timeonsite::integer);


**--Drop Userid From analytics table due to NULL values**
ALTER TABLE analytics
DROP COLUMN userid;

**--UPDATE analytics table to convert NULL values to zero values on units_sold**
UPDATE analytics
SET units_sold = 0
WHERE units_sold IS NULL;




**--Convert Timeonsite to Integer**
ALTER TABLE analytics ALTER COLUMN timeonsite TYPE integer USING (timeonsite::integer);

--Drop socialengagementtype From analytics table
ALTER TABLE analytics
DROP COLUMN socialengagementtype


**--Drop productrefundamount AND itemrevenue as they both appear to have empty data**
ALTER TABLE all_sessions
DROP COLUMN transactionid

ALTER TABLE all_sessions
DROP COLUMN itemrevenue

**--Drop Userid From analytics table due to NULL values**
ALTER TABLE analytics
DROP COLUMN userid;

**--UPDATE analytics table to convert NULL values to zero values on units_sold**
UPDATE analytics
SET units_sold = 0
WHERE units_sold IS NULL;


**-- Convert visitstatrttime column  to TO_Timestamp data type**
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE timestamp
USING To_timestamp(visitstarttime);

**--Convert Timeonsite to Integer**
ALTER TABLE analytics ALTER COLUMN timeonsite TYPE integer USING (timeonsite::integer);

**--Drop socialengagementtype From analytics table**
ALTER TABLE analytics
DROP COLUMN socialengagementtype



**--Change Datatypes on unit_price in analytics table**
select
CAST((unit_price / 1000000.) AS DECIMAL (10,2))
from analytics
LIMIT 100

UPDATE analytics 
SET unit_price = CAST((unit_price / 1000000.) AS DECIMAL(10,2));

select * from analytics
LIMIT 100

select * from sales_report
Limit 100

--Check for duplicate
SELECT productsku, COUNT(*)
FROM sales_report
GROUP BY productsku
HAVING COUNT(*) > 1;

--Drop productrefundamount
--itemrevenue
transactionid
transactionrevenue


ALTER TABLE all_sessions
DROP COLUMN transactionid;

ALTER TABLE all_sessions
DROP COLUMN itemrevenue;

