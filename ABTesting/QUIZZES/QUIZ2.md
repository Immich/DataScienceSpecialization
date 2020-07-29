# MODULE 2 QUIZ

1. Which step should happen first in data analysis?

##### R = Collecting Data

2. TROUBLESHOOT THIS ERROR by selecting appropriate actions to remedy this specific query:
Kat ran 9 lines of MySQL (finished in 112ms):

```sql
--------------
CREATE TABLE
example_table
(
column1  DATE,
column2  VARCHAR(30),
column3  INT
)
--------------
```
```
ERROR 1050 (42S01) at line 1: Table 'example_table' already exists

Bye

mysql>
```

##### R = RUN DESCRIBE TABLE table_example to see if the existing table_example is structured aappropriately

3. Based on the code snippet below, which statements are definitely true (select all that apply):

```sql
CREATE TABLE table_x AS
SELECT
 dates_rollup.date,
 COUNT(*)
FROM
 Dates_rolluop
JOIN
 Table_y
ON
dates_rollup.date = table_y.date
GROUP BY
 date
```

##### R =
* table_x is dependent on table_y and dates_rollup
* table_x is dependent on table_y

4. Based on what you know about the orders table for this class, which of the following columns have a suitable datatype?

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz2.1.png "QUIZ2 IMG1")

##### R =
* item_name
* invoice_id
* user_id

5. For this class, we are using Mode on a dataset specifically created for this course. Which of these circumstances could be different in a real world situation? (Select all that apply.)

##### R =
* The specific dialect of SQL
* How frequently the data is updated

6. Based on what you know about the **items** table for this class, which of the following columns have a suitable datatype? (Select all that apply.)

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz2.2.png "QUIZ2 IMG2")

##### R =
* category
* name


7. Which of the following table methods allows you to specify data types?

##### R = This table method allows you to specify data types.

```sql
SELECT *
FROM
  example_table
AS...
```

8. When creating a user info table we used a variable in place of which column?

##### R = The date
In our table, the date was replaced by a variable.


9. Suppose in a table, you find a column called email which contains the value **user@domain.com**. What is the correct data type category for this column?

##### R = String


10. In this module, we created a table specifically of item view events. What level of the hierarchy of data does this belong on?

##### R = Explore and Transform

11. Suppose in a table you find a column called event_id, which contains the value **z87df6ab4waoa756b3**. What is the correct data type category for this column?

##### R = String
