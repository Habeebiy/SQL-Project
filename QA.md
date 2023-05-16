What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.


-- Determine the Data types

SELECT *
FROM information_schema.tables
WHERE table_schema = 'public';

SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'analytics';


SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'all_sessions';

SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'products';

SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'sales_by_sku';

SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'sales_report';

--Determine the unique values and remove duplicates

SELECT COUNT(DISTINCT fullvisitorid )
FROM all_sessions;

SELECT fullVisitorID, COUNT(*)
FROM all_sessions
GROUP BY fullVisitorID
HAVING COUNT(*) > 1;


DELETE FROM all_sessions
WHERE (fullVisitorID) IN (
  SELECT fullVisitorID
  FROM all_sessions
  GROUP BY fullVisitorID
  HAVING COUNT(*) > 1
);

--Remove column with empty input

SELECT *
FROM all_sessions
WHERE fullVisitorID IS NULL;

ALTER TABLE all_sessions
DROP COLUMN productrefundamount

ALTER TABLE all_sessions
DROP COLUMN searchkeyword


--UPDATE analytics table to convert NULL values to zero values on units_sold
UPDATE analytics
SET units_sold = 0
WHERE units_sold IS NULL;


















