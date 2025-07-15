Question 1: SQL Queries: How many unique_visitors were there?

SELECT COUNT(DISTINCT full_visitor_id)::INTEGER AS unique_visitors
FROM all_sessions;


Answer:

14223

Question 2: What is the average revenue per visitor?

SQL Queries:

SELECT 
  AVG(product_quantity * unit_price) AS avg_visitor_revenue
FROM all_sessions
JOIN analytics ON all_sessions.visit_id = analytics.visit_id;



Answer:

82328666.666666666667

Question 3: How many unique visitors ordered more than 1 product?

SQL Queries:

SELECT COUNT(DISTINCT full_visitor_id) AS visitors_multiple_products
FROM all_sessions
WHERE product_quantity > 1;


Answer:

8


Question 4: How many products were sold in total?

SQL Queries:

 SELECT SUM(product_quantity) AS total_products_sold
FROM all_sessions;

Answer:

189

Question 5: 



SQL Queries: Which city had the most visitors?

SELECT city, COUNT(DISTINCT full_visitor_id) AS total_visitors
FROM all_sessions
GROUP BY city
ORDER BY total_visitors DESC
LIMIT 1;

Answer: (as BIGINT)

7857