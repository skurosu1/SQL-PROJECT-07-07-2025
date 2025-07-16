What issues will you address by cleaning the data?

Data Cleaning = What You Fixed

QA (Quality Assurance) = What You Checked

Fixing the data will render it more useful for analytical purposes by removing erroneous data that would skew the ability to make accurate inferences.

Queries:
Below, provide the SQL queries you used to clean your data.

For example, even though I included all the columns in my query, I would use a query like this to delete null data for these columns.

DELETE FROM all_sessions
WHERE city ILIKE '%not%' 
   OR country ILIKE '%not%' 
   OR v2_product_name IS NULL;

Another example is using BIGINT to identify certain colums in order to render the analysis more easy to interpret at a glance.
