Question 1: Top 3 countries with the most visitors to the site

SQL Queries:

SELECT 
	country,
	COUNT(fullvisitorid) as num_visitor
FROM all_sessions
GROUP BY country
ORDER BY num_visitor DESC
Limit 3


**Answer:** 

"United States" 	7602
"India"         	668
"United Kingdom"	616



Question 2: What channelgrouping drives in most sales in each country?

SQL Queries:

SELECT COUNT(*), channelgrouping 
FROM(
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
) As sub
Group By channelgrouping
ORDER BY COUNT(*) DESC;

**Answer:**

42	"Referral"
12	"Organic Search"
9	"Direct"
8	"Display"
1	"Paid Search"


Question 3: --3.Most product in stock

SQL Queries:

SELECT 
	sku,
	name,
	stocklevel
FROM products
ORDER BY stocklevel DESC

**Answer:**

"GGOEGDHC018299"	" 22 oz Water Bottle"	19678
"GGOEGAAX0074"		" 22 oz Water Bottle"	15607
"GGOEGAAX0037"		" Sunglasses"	6805



Question 4: 
--5. Most expensive product.

SQL Queries:

SELECT 
	v2productname,
	ROUND((unit_price / 1000000.0),2) As unit_price
FROM analytics
JOIN all_sessions USING(visitid)
GROUP BY v2productname, unit_price
ORDER BY unit_price DESC
Limit 3

**Answer:**
"Nest® Learning Thermostat 3rd Gen-USA - White"			395.00
"SPF-15 Slim & Slender Lip Balm"				316.00
"Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel"	298.00


Question 5: 
-- 5. Percentage of revenue by each city

SQL Queries:

SELECT 	
	als.country,
	als.city,
	revenue,
	sum(revenue) OVER (PARTITION BY country) AS country_total,
	ROUND(revenue / SUM(revenue) OVER (PARTITION BY country),4) AS Ptc
FROM all_sessions as als
JOIN analytics
USING (visitid)
WHERE revenue IS NOT NULL
GROUP BY country, city, revenue;

**Answer:**

"Israel"		"Tel Aviv-Yafo"		12500000	32990000	0.3789
"Israel"		"Tel Aviv-Yafo"		20490000	32990000	0.6211
"Switzerland"		"Zurich"		16990000	16990000	1.0000
"United States"		"Chicago"		306000000	4646286658	0.0659
"United States"		"Mountain View"		3990000		4646286658	0.0009
"United States"		"Mountain View"		5990000		4646286658	0.0013
"United States"		"Mountain View"		7000000		4646286658	0.0015
"United States"		"Mountain View"		11130000	4646286658	0.0024
"United States"		"Mountain View"		12400000	4646286658	0.0027
"United States"		"Mountain View"		15690000	4646286658	0.0034
"United States"		"Mountain View"		16990000	4646286658	0.0037
"United States"		"Mountain View"		17990000	4646286658	0.0039
"United States"		"Mountain View"		35990000	4646286658	0.0077
"United States"		"Mountain View"		37390000	4646286658	0.0080
"United States"		"Mountain View"		71190000	4646286658	0.0153
"United States"		"Mountain View"		244000000	4646286658	0.0525
"United States"		"New York"		5350000		4646286658	0.0012
"United States"		"New York"		17490000	4646286658	0.0038
"United States"		"New York"		29490000	4646286658	0.0063
"United States"		"New York"		57990000	4646286658	0.0125
