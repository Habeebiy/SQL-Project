What issues will you address by cleaning the data?





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


**-- Convert visitstatrttime column  to TO_Timestamp data type**
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE timestamp
USING To_timestamp(visitstarttime);



**--Convert Timeonsite to Integer**
ALTER TABLE analytics ALTER COLUMN timeonsite TYPE integer USING (timeonsite::integer);

--Drop socialengagementtype From analytics table
ALTER TABLE analytics
DROP COLUMN socialengagementtype


**----Drop productrefundamount AND itemrevenue as they both appear to have empty data**
ALTER TABLE all_sessions
DROP COLUMN transactionid

ALTER TABLE all_sessions
DROP COLUMN itemrevenue
