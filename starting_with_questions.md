Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:

SELECT s.country, s.city, SUM(a.unit_price) AS revenue
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
GROUP BY s.country, s.city
ORDER BY revenue DESC;



Answer:

The United States and then the UK and Canada had the highest level of transaction revenue. Null data aside, we see that Mountain View had the highest level of transaction revenue in a city.


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT s.country, AVG(s.product_quantity) AS avg_qty
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
WHERE s.product_quantity IS NOT NULL
GROUP BY s.country
ORDER BY avg_qty DESC;

SELECT s.country, AVG(s.product_quantity) AS avg_qty
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
WHERE s.product_quantity IS NOT NULL
GROUP BY s.country
ORDER BY avg_qty DESC;


Answer: (in BIGINT)

"United States"	"New York"	2.0000000000000000
"United States"	"Houston"	2.0000000000000000
"United States"	"(not set)"	1.00000000000000000000
"United States"	"Ann Arbor"	1.00000000000000000000
"United States"	"Dallas"	1.00000000000000000000
"United States"	"Detroit"	1.00000000000000000000
"United States"	"Mountain View"	1.00000000000000000000
"United States"	"not available in demo dataset"	1.00000000000000000000
"United States"	"Seattle"	1.00000000000000000000
"France"	"not available in demo dataset"	1.00000000000000000000
"United States"	"Sunnyvale"	1.00000000000000000000
"Ireland"	"Dublin"	1.00000000000000000000


"United States"	1.1538461538461538
"France"	1.00000000000000000000
"Ireland"	1.00000000000000000000

Lack of other cities/countires due to Null data


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT s.country, s.city, s.v2_product_category, COUNT (*) AS count
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
GROUP BY s.country, s.city, s.v2_product_category
ORDER BY count DESC;

SELECT s.country, s.city, s.v2_product_category, COUNT (*) AS count
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
GROUP BY s.country, s.city, s.v2_product_category
ORDER BY s.country, count DESC;


Answer:

Countries like Croatia or Costa Rica had no city data for their product sales, or counties like the Czech Republic had no city sale data outside the capital.

China made for a suprisingly low share of the market. and only for brandware.




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT s.country, s.city, s.v2_product_name, SUM(s.product_quantity) AS total
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
WHERE s.product_quantity IS NOT NULL
GROUP BY s.country, s.city, s.v2_product_name
ORDER BY total DESC;


Answer: (in BIGINT)

"United States"	"New York"	"Nest® Protect Smoke + CO White Wired Alarm-USA"	2
"United States"	"Houston"	"Google Sunglasses"	2
"United States"	"(not set)"	"Android Wool Heather Cap Heather/Black"	1
"United States"	"Ann Arbor"	"Google Men's Vintage Badge Tee Black"	1
"United States"	"Dallas"	"YouTube Leatherette Notebook Combo"	1
"United States"	"Detroit"	"Google 22 oz Water Bottle"	1
"United States"	"Mountain View"	"Google Men's Bike Short Sleeve Tee Charcoal"	1
"United States"	"Mountain View"	"Google Women's Convertible Vest-Jacket Black"	1
"United States"	"not available in demo dataset"	"Nest® Cam Indoor Security Camera - USA"	1
"United States"	"not available in demo dataset"	"Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel"	1
"United States"	"not available in demo dataset"	"Nest® Protect Smoke + CO White Wired Alarm-USA"	1
"United States"	"Seattle"	"Nest® Cam Indoor Security Camera - USA"	1
"France"	"not available in demo dataset"	"Android Wool Heather Cap Heather/Black"	1
"United States"	"Sunnyvale"	"Nest® Cam Outdoor Security Camera - USA"	1
"Ireland"	"Dublin"	"Google Laptop Backpack"	1

Home automation products were espectially popular such as Google Security Cameras and similar products and smoke alarms and such.



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT s.country, s.city, SUM(a.unit_price * s.product_quantity) AS total_revenue
FROM all_sessions s
JOIN analytics a ON s.visit_id = a.visit_id
WHERE s.product_quantity IS NOT NULL
GROUP BY s.country, s.city
ORDER BY total_revenue DESC;


Answer:

"United States"	"New York"	398000000.00
"United States"	"not available in demo dataset"	322990000.00
"United States"	"Sunnyvale"	199000000.00
"United States"	"Seattle"	119000000.00
"United States"	"(not set)"	109990000.00
"France"	"not available in demo dataset"	39990000.00
"United States"	"Ann Arbor"	16990000.00
"Ireland"	"Dublin"	13990000.00
"United States"	"Detroit"	12990000.00
"United States"	"Dallas"	1990000.00
"United States"	"Houston"	0.00
"United States"	"Mountain View"	0.00

We can use Mountain View as an example to see that the highest number of sales of a certain product in an area does not equate to that region generating the most revenue overall.



