 # AB TESTING FINAL ASSIGNMENT

 Hi all! In this repository you're going to find the answer and the sql code of final assignment of the Data Wrangling, Analysis and AB Testing with SQL course.
 
##### 1. We are running an experiment at an item-level, which means all users who visit will see the same page, but the layout of different item pages may differ. Compare this table to the assignment events we captured for user_level_testing. Does this table have everything you need to compute metrics like 30-day view-binary?
#### Answer: 
No, it doesn't. I need the test_start_date and the created_at variable.

##### Reformat the final_assignments_qa to look like the final_assignments table, filling in any missing values with a placeholder of the appropriate data type.
#### Answer:
I used the union function to create a table with the different tests inside rows and not columns. Futhermore, I assigned a different date to each test.
