Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

**--COUNTRY**
SQL Queries:
SELECT 
    Country,
    SUM(totaltransactionrevenue) AS total
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY country
ORDER BY total DESC;

**--CITY**
SELECT 
    city,
    SUM(totaltransactionrevenue) AS total
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY city
ORDER BY total DESC;


Answer:

**COUNTRY**

"United States"	    5876960000
"Israel"	        602000000
"Australia"	        358000000
"Canada"	        150150000
"Switzerland"	    16990000



**CITY**
"San Francisco"	    1251130000
"Sunnyvale"	        872230000
"Palo Alto"	        608000000



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







