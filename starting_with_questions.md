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

SELECT
    als.country,
    AVG(a.units_sold)::NUMERIC(10,2) AS average_units_sold
FROM all_sessions AS als
JOIN analytics AS a USING (visitid)
GROUP BY als.country
ORDER BY average_units_sold DESC
LIMIT 100;




Answer:

"Maldives"	0.09
"Egypt"	0.05
"Bulgaria"	0.04
"Chile"	0.02
"Hong Kong"	0.01
"Austria"	0.01
"Ireland"	0.01
"Israel"	0.01
"United States"	0.01
"Canada"	0.01
"Romania"	0.01
"Sweden"	0.01
"Vietnam"	0.01




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT
    als.country,
    --als.city,
    v2productcategory,
    COUNT(*) AS order_count
FROM all_sessions AS als
-- JOIN analytics AS a USING (visitid)
-- JOIN products AS p ON a.product_id = p.product_id
GROUP BY als.country, v2productcategory
ORDER BY order_count DESC  --als.country, order_count DESC
LIMIT 100;



Answer:

"United States"	"Home/Apparel/Men's/Men's-T-Shirts/"	810
"United States"	"Home/Shop by Brand/YouTube/"	765
"United States"	"Home/Electronics/"	500
"United States"	"Home/Apparel/"	457
"United States"	"(not set)"	414
"United States"	"Home/Shop by Brand/Google/"	413
"United States"	"Home/Apparel/Men's/Men's-Outerwear/"	361
"United States"	"Home/Nest/Nest-USA/"	352
"United States"	"Home/Office/"	319
"United States"	"Home/Drinkware/"	259
"United States"	"Home/Bags/"	252
"United Kingdom"	"Home/Shop by Brand/YouTube/"	242
"United States"	"Home/Apparel/Women's/Women's-T-Shirts/"	234
"United States"	"Home/Apparel/Men's/"	225
"India"	"Home/Shop by Brand/YouTube/"	206





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT
    als.country,
    --als.city,
    v2productname,
    COUNT(*) AS order_count
FROM all_sessions AS als
-- JOIN analytics AS a USING (visitid)
-- JOIN products AS p ON a.product_id = p.product_id
GROUP BY als.country, v2productname
ORDER BY order_count DESC  --als.country, order_count DESC
LIMIT 100;



Answer:

"United States"	"Google Men's 100% Cotton Short Sleeve Hero Tee White"	152
"United States"	"22 oz YouTube Bottle Infuser"	94
"United States"	"YouTube Twill Cap"	85
"United States"	"Google Men's 100% Cotton Short Sleeve Hero Tee Navy"	84
"United States"	"Google Men's 100% Cotton Short Sleeve Hero Tee Black"	84
"United States"	"Galaxy Screen Cleaning Cloth"	76
"United States"	"YouTube Men's Short Sleeve Hero Tee Black"	76
"United States"	"YouTube Men's Short Sleeve Hero Tee Charcoal"	75
"United States"	"YouTube Custom Decals"	71
"United States"	"Google Men's Watershed Full Zip Hoodie Grey"	70
"United States"	"Google Snapback Hat Black"	67
"United States"	"Google Laptop and Cell Phone Stickers"	66
"United States"	"YouTube Leatherette Notebook Combo"	65




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT 
	country,
	city,
	SUM(revenue) AS rev
FROM analytics
JOIN all_sessions USING (visitid)
WHERE revenue IS NOT NULL AND city != 'not available in demo dataset'
GROUP BY country,city
ORDER BY rev DESC
LIMIT 100



Answer:

"United States"	"New York"	1142730000
"United States"	"Sunnyvale"	672229992
"United States"	"Mountain View"	500750000
"United States"	"Seattle"	358000000
"United States"	"Chicago"	306000000
"United States"	"San Francisco"	300489998
"United States"	"San Jose"	153000000
"United States"	"Palo Alto"	151000000
"Israel"	"Tel Aviv-Yafo"	32990000
"Switzerland"	"Zurich"	16990000





