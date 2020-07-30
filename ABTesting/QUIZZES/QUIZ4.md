# MODULE 4 QUIZ

1. Which of the following are the purpose of AB testing? (Select all that apply).
##### R =
* Provide evidence for or disprove a hypothesis
* Learn from data

2. Which of the following are necessary components of a user-level test assignment table? (Select all that apply).
##### R =
* The user_id
* The date or time of assignment
* A test name or number
* The assignment (treatment or control?)

3. Which of the following are necessary components of an item-level test assignment table? (Select all that apply).
##### R =
* The item id
* The date or time of assignment
* A test name or number
* The assignment (treatment or control?)

4. In the final project we’ll be doing AB testing at an item level. Check out the table final_assignment_qa. What other pieces of data will you need to compute the 30-day order binary. (Select all that apply).

###### Please note: 30-day order binary means show a 1 if the item was ordered at any point the 30 day period after treatment, and 0 if the item was never ordered.
##### R =
* The orders table
* I'm still missing something (The thing we are still missing is the date of the assignment)

5. Use this AB testing calculator. Enter the numbers seen in the image, and use the results to determine if the results are statistically significant.
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz4.1.png "AB Testing tool test1")

Are the results statistically significant?

##### R = No. The p-value is 0.97 and the true mean is likely to be between -25% and 27%. This result is not statistically significant.

6. Use this AB testing calculator. Enter the numbers seen in the image, and select all the correct interpretations of the data.
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz4.1.png "AB Testing tool test1")

##### R =
* There is no detectable change in this metric
* We have not collected enough samples to be able to detect statistically significant lift of 1%

7. Use this AB testing calculator. Enter the numbers seen in the image. In this calculation, what is the observed success **rate in control**?
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz4.2.png "AB Testing tool test1")
##### R = 8.5%

8. Use this AB testing calculator. Enter the numbers seen in the image. In this calculation, what is the observed success **rate in treatment**?
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz4.2.png "AB Testing tool test1")
##### R = 14%

9. Use this AB testing calculator. Enter the numbers seen in the image. In this calculation, what is the observed relative lift in success rate between control and treatment?
#####
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz4.2.png "AB Testing tool test1")
##### R = 61%

10. Use this AB testing calculator. Enter the numbers seen in the image. In this calculation, what is the range of improvement that is likely to have been caused by the treatment?
#####
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/ABTesting/quiz_imgs/quiz4.2.png "AB Testing tool test1")
##### R = 40% to 81%

11. Which of the following queries would meet the coding standards for the final project?
##### R =
```sql
SELECT
COUNT(*) AS user_count
FROM dsv1069.users
```
