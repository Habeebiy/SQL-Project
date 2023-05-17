Question 1: Top 3 countries with the most visitors to the site

SQL Queries:

SELECT 
	country,
	COUNT(fullvisitorid) as num_visitor
FROM all_sessions
GROUP BY country
ORDER BY num_visitor DESC
Limit 3


Answer: 
"United States" 	7602
"India"         	668
"United Kingdom"	616



Question 2: What channelgrouping drives in most sales in each country?

SQL Queries:

SELECT
	als.country,
	als.city,
	als.channelgrouping,
	revenue
FROM all_sessions as als
JOIN analytics
USING (visitid)
WHERE revenue IS NOT NULL
--GROUP BY als.country, als.channelgrouping, revenue, als.city
ORDER BY als.channelgrouping DESC

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
