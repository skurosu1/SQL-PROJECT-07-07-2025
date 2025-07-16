What are your risk areas? Identify and describe them.

Risk include incomplete data and null values that are so significant as could potentially skew any inferences to be made by the data available.

Duplicate or erroneous data.

QA Process:
Describe your QA process and include the SQL queries used to execute it.

REMOVING DUPLICATES:

Step 1: Check for duplicate values based on visit_id

SELECT visit_id, COUNT(*) AS count
FROM all_sessions
GROUP BY visit_id
HAVING COUNT(*) > 1;

Step 2: Create copy of all_sessions table with duplicates of visit_id filtered out

CREATE TABLE all_sessions_clean AS
SELECT DISTINCT ON (visit_id) *
FROM all_sessions;

Step 3: Delete original all_sessions table

DROP TABLE all_sessions;

Step 4: Rename copy of all_sessions to it's original name.

ALTER TABLE all_sessions_clean RENAME TO all_sessions;



REMOVING ERRONEOUS DATA:

Step 1: Check for erronoeus data, by each column name

{this can be extracted for convenience/ ergonomics with the following query:

SELECT column_name
FROM information_schema.columns
WHERE table_name = 'all_sessions'
  AND table_schema = 'public'
ORDER BY ordinal_position;

}

SELECT *
FROM all_sessions
WHERE
  full_visitor_id IS NULL OR full_visitor_id::TEXT ILIKE '%not%' OR
  channel_grouping IS NULL OR channel_grouping::TEXT ILIKE '%not%' OR
  time IS NULL OR time::TEXT ILIKE '%not%' OR
  country IS NULL OR country::TEXT ILIKE '%not%' OR
  city IS NULL OR city::TEXT ILIKE '%not%' OR
  total_transaction_revenue IS NULL OR total_transaction_revenue::TEXT ILIKE '%not%' OR
  transactions IS NULL OR transactions::TEXT ILIKE '%not%' OR
  time_on_site IS NULL OR time_on_site::TEXT ILIKE '%not%' OR
  pageviews IS NULL OR pageviews::TEXT ILIKE '%not%' OR
  session_quality_dim IS NULL OR session_quality_dim::TEXT ILIKE '%not%' OR
  date IS NULL OR date::TEXT ILIKE '%not%' OR
  visit_id IS NULL OR visit_id::TEXT ILIKE '%not%' OR
  type IS NULL OR type::TEXT ILIKE '%not%' OR
  product_refund_amount IS NULL OR product_refund_amount::TEXT ILIKE '%not%' OR
  product_quantity IS NULL OR product_quantity::TEXT ILIKE '%not%' OR
  product_price IS NULL OR product_price::TEXT ILIKE '%not%' OR
  product_revenue IS NULL OR product_revenue::TEXT ILIKE '%not%' OR
  product_sku IS NULL OR product_sku::TEXT ILIKE '%not%' OR
  v2_product_name IS NULL OR v2_product_name::TEXT ILIKE '%not%' OR
  v2_product_category IS NULL OR v2_product_category::TEXT ILIKE '%not%' OR
  product_variant IS NULL OR product_variant::TEXT ILIKE '%not%' OR
  currency_code IS NULL OR currency_code::TEXT ILIKE '%not%' OR
  item_quantity IS NULL OR item_quantity::TEXT ILIKE '%not%' OR
  item_revenue IS NULL OR item_revenue::TEXT ILIKE '%not%' OR
  transaction_revenue IS NULL OR transaction_revenue::TEXT ILIKE '%not%' OR
  transaction_id IS NULL OR transaction_id::TEXT ILIKE '%not%' OR
  page_title IS NULL OR page_title::TEXT ILIKE '%not%' OR
  search_keyword IS NULL OR search_keyword::TEXT ILIKE '%not%' OR
  page_path_level1 IS NULL OR page_path_level1::TEXT ILIKE '%not%' OR
  ecommerce_action_type IS NULL OR ecommerce_action_type::TEXT ILIKE '%not%' OR
  ecommerce_action_step IS NULL OR ecommerce_action_step::TEXT ILIKE '%not%' OR
  ecommerce_action_option IS NULL OR ecommerce_action_option::TEXT ILIKE '%not%';


Step 2: Delete all erroneous data

  DELETE FROM all_sessions
WHERE
  full_visitor_id IS NULL OR full_visitor_id::TEXT ILIKE '%not%' OR
  channel_grouping IS NULL OR channel_grouping::TEXT ILIKE '%not%' OR
  time IS NULL OR time::TEXT ILIKE '%not%' OR
  country IS NULL OR country::TEXT ILIKE '%not%' OR
  city IS NULL OR city::TEXT ILIKE '%not%' OR
  total_transaction_revenue IS NULL OR total_transaction_revenue::TEXT ILIKE '%not%' OR
  transactions IS NULL OR transactions::TEXT ILIKE '%not%' OR
  time_on_site IS NULL OR time_on_site::TEXT ILIKE '%not%' OR
  pageviews IS NULL OR pageviews::TEXT ILIKE '%not%' OR
  session_quality_dim IS NULL OR session_quality_dim::TEXT ILIKE '%not%' OR
  date IS NULL OR date::TEXT ILIKE '%not%' OR
  visit_id IS NULL OR visit_id::TEXT ILIKE '%not%' OR
  type IS NULL OR type::TEXT ILIKE '%not%' OR
  product_refund_amount IS NULL OR product_refund_amount::TEXT ILIKE '%not%' OR
  product_quantity IS NULL OR product_quantity::TEXT ILIKE '%not%' OR
  product_price IS NULL OR product_price::TEXT ILIKE '%not%' OR
  product_revenue IS NULL OR product_revenue::TEXT ILIKE '%not%' OR
  product_sku IS NULL OR product_sku::TEXT ILIKE '%not%' OR
  v2_product_name IS NULL OR v2_product_name::TEXT ILIKE '%not%' OR
  v2_product_category IS NULL OR v2_product_category::TEXT ILIKE '%not%' OR
  product_variant IS NULL OR product_variant::TEXT ILIKE '%not%' OR
  currency_code IS NULL OR currency_code::TEXT ILIKE '%not%' OR
  item_quantity IS NULL OR item_quantity::TEXT ILIKE '%not%' OR
  item_revenue IS NULL OR item_revenue::TEXT ILIKE '%not%' OR
  transaction_revenue IS NULL OR transaction_revenue::TEXT ILIKE '%not%' OR
  transaction_id IS NULL OR transaction_id::TEXT ILIKE '%not%' OR
  page_title IS NULL OR page_title::TEXT ILIKE '%not%' OR
  search_keyword IS NULL OR search_keyword::TEXT ILIKE '%not%' OR
  page_path_level1 IS NULL OR page_path_level1::TEXT ILIKE '%not%' OR
  ecommerce_action_type IS NULL OR ecommerce_action_type::TEXT ILIKE '%not%' OR
  ecommerce_action_step IS NULL OR ecommerce_action_step::TEXT ILIKE '%not%' OR
  ecommerce_action_option IS NULL OR ecommerce_action_option::TEXT ILIKE '%not%';


Step 3: Repeat step 1 in order to double check.
