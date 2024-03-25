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

##### 2.Use the final_assignments table to calculate the view binary, and average views for the 30 day window after the test assignment for item_test_2. (You may include the day the test started)
#### Answer:
```
SELECT 
  test_assignment,
  COUNT(DISTINCT item_id) AS total_items,
  SUM(orders_binary) AS items_ordered_within_30_days
FROM
  (SELECT 
    item_id,
    test_assignment,
    test_number,
    test_start_date,
    created_at,
    MAX(CASE
          WHEN created_at > test_start_date
          AND DATE_PART('day', created_at - test_start_date) <= 30 THEN 1
          ELSE 0
          END) AS orders_binary
  FROM 
    (SELECT 
      f.*,
      DATE(o.created_at) AS created_at
    FROM 
      dsv1069.final_assignments f
    LEFT JOIN 
      dsv1069.orders o
    ON 
    o.item_id = f.item_id
    WHERE 
      test_number = 'item_test_2') AS item_test_2
  GROUP BY 
    item_id,
    test_assignment,
    test_number,
    test_start_date,
    created_at) AS item_test_2_part_2<img width="504" alt="AB testing 2" src="https://github.com/anfezabu/SQL_Projects/assets/164940373/8a51412b-bcee-49ff-8b45-8861b3e6d281">

GROUP BY 
  test_assignment
```
<img width="504" alt="AB testing 2" src="https://github.com/anfezabu/SQL_Projects/assets/164940373/0a2fe6c6-46e9-465b-8882-62d09ebf484e">
