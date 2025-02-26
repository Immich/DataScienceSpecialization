# MODULE 1 QUIZ

1. Based on the dataset for this course, what does this query count?

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.1.png "QUIZ IMG1")

##### R = Counts the number of rows in the orders table.
All of the orders have a user_id, and every user is in the user's table, so this will return the one row for every entry in the orders table.


2. Assume you have no information about the data in the example table.
When I run the query below, no rows are returned, but there are no error messages. What are possible reasons for this? (Select all that apply.)

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.2.png "QUIZ IMG2")


##### R =
* There are no rows in the example_table - it's empty
* There are no rows with null id


3. In the events table, (dsv1069.events) for this class, how many rows exist per event_id?
##### R = One per parameter name


4. When you encounter a new dataset, which of the following can you assume? (Select all that apply.)
##### R =
* Test usage is unfiltered
* The table is empty
* There are duplicated rows
* The data is out-of-date


5. TROUBLESHOOT THIS ERROR:
##### Based on your exploration of the tables in the course dataset. Why are the results to this specific query empty?

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.3.png "QUIZ IMG3")

##### R = There are no parent_user_ids that satisfy the WHERE clause


6. TROUBLESHOOT THIS ERROR:
##### Why are the results for this specific query empty?

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.4.png "QUIZ IMG4")

##### R = There are no events with this event_name



7. What does this query do? Select all true statements.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.5.png "QUIZ IMG5")

##### R = The query counts the number of rows corresponding to view_item events
Count(*) counts rows not unique events, and because of this where clause it counts the number of view_item event rows.


8. Consider the following query:

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.6.png "QUIZ IMG6")

##### R = Each row with a null value is joined to every row in table_beta where table_beta.column is null.



9. Which of the following are problems with the query below?

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz1.7.png "QUIZ IMG7")

##### R = Count(*) counts rows not unique users
So although we received no error message, we must be sure we correctly querying for the correct results.




10. In the users table, the column parent_user_id is __________________.

##### R = Sometimes NULL









