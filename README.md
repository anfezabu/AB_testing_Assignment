 # AB TESTING FINAL ASSIGNMENT

 Hi all! In this repository you're going to find the answer and the sql code of final assignment of the Data Wrangling, Analysis and AB Testing with SQL course.
 
##### 1. We are running an experiment at an item-level, which means all users who visit will see the same page, but the layout of different item pages may differ. Compare this table to the assignment events we captured for user_level_testing. Does this table have everything you need to compute metrics like 30-day view-binary?
#### Answer: 
No, it doesn't. I need the test_start_date and the created_at variable.

##### Reformat the final_assignments_qa to look like the final_assignments table, filling in any missing values with a placeholder of the appropriate data type.
#### Answer:
I used the union function to create a table with the different tests inside rows and not columns. Futhermore, I assigned a different date to each test.

```
SELECT 
  item_id,
  test_a AS test_assignment,
  (CASE
       WHEN test_a IS NOT NULL THEN 'test_a'
       ELSE NULL
   END) AS test_number,
  (CASE
       WHEN test_a IS NOT NULL THEN CAST ('2020-06-01' AS DATE)
       ELSE NULL
   END) AS test_start_date
FROM 
  dsv1069.final_assignments_qa
UNION
SELECT
  item_id,
  test_b AS test_assignment,
  (CASE
       WHEN test_b IS NOT NULL THEN 'test_b'
       ELSE NULL
   END) AS test_number,
  (CASE
       WHEN test_b IS NOT NULL THEN CAST('2020-09-01' AS DATE)
       ELSE NULL
   END) AS test_start_date
FROM 
  dsv1069.final_assignments_qa
UNION
SELECT 
  item_id,
  test_c AS test_assignment,
  (CASE
       WHEN test_c IS NOT NULL THEN 'test_c'
       ELSE NULL
   END) AS test_number,
  (CASE
       WHEN test_c IS NOT NULL THEN CAST('2020-12-01' AS DATE)
       ELSE NULL
   END) AS test_start_date
FROM 
  dsv1069.final_assignments_qa
UNION
SELECT 
  item_id,
  test_d AS test_assignment,
  (CASE
       WHEN test_d IS NOT NULL THEN 'test_d'
       ELSE NULL
   END) AS test_number,
  (CASE
       WHEN test_d IS NOT NULL THEN CAST('2021-03-01' AS DATE)
       ELSE NULL
  END) AS test_start_date
FROM 
  dsv1069.final_assignments_qa
UNION
SELECT 
  item_id,
  test_e AS test_assignment,
  (CASE
       WHEN test_e IS NOT NULL THEN 'test_e'
       ELSE NULL
   END) AS test_number,
  (CASE
       WHEN test_e IS NOT NULL THEN CAST('2021-06-01' AS DATE)
       ELSE NULL
  END) AS test_start_date
FROM 
  dsv1069.final_assignments_qa
UNION
SELECT 
  item_id,
  test_f AS test_assignment,
  (CASE
       WHEN test_f IS NOT NULL THEN 'test_f'
       ELSE NULL
   END) AS test_number,
  (CASE
       WHEN test_f IS NOT NULL THEN CAST('2021-09-01' AS DATE)
       ELSE NULL
  END) AS test_start_date
FROM 
  dsv1069.final_assignments_qa;
```
<img width="1398" alt="AB testing 1" src="https://github.com/anfezabu/SQL_Projects/assets/164940373/70512ea3-5c40-4e0d-99e0-79039cd78e7c">
