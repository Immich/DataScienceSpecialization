# MODULE 3 QUIZ

1. Which of the following attributes distinguish a work-in-progress from a “polished” final query? (Select all that apply.)

##### R =
* Every column has a descriptive name
* The query is formatted consistently, or according to a style guide

2. In which of the following sections did we perform analysis to directly guide decision making?

##### R =
* Answering a question about reordering items

3. Which of the following are uses of a dates rollup table?
##### R =
* Efficiently computing aggregates over a rolling time period
* Creating dashboards with a complete set of dates

4. We've decided to only use the items and users tables to answer the following questions:
⋅⋅* How many items have been purchased?
⋅⋅* How many items do we have?
⋅⋅⋅Which join type and order will allow us to correctly compute the columns Item_count, items_ever_purchased_count?

```sql
SELECT *
FROM
  dsv1069.items
LEFT OUTER JOIN
  dsv1069.orders
ON
  items.id = orders.item
```

5. For this statement, fill in the __ with the appropriate inequality (<, <=, =, >=, >):

###### For days in any given week
###### Daily unique visitors _ Weekly Unique visitors

##### R = **<=**
Over a longer period of time there can only be more visitors.

6. Select the best definition of a windowing function?
##### R = It is a function that computes a value on a certain partition, or window, of the data that is specified in the PARTITION BY statement.


7. Folks at the company wonder if our product catalog is too small. What are some related questions that you could directly answer with our dataset? (Select all that apply.)
##### R =
* How many items have been viewed?
* How many items have been purchased?
* How many items have been viewed but not ordered?
* How many items do we have?

8. Which of the following tasks can be accomplished with a windowing function? (Select all that apply.)
##### R =
* Find the most expensive item per order
* Find the most recently viewed item

9. Let’s suppose we want to write a query to answer both of these questions:
⋅⋅* How many users have made a purchase?
⋅⋅* How many users do we have?
⋅⋅* Please choose the best set of columns for a final query that would answer these questions:

```sql
user_count
user_with_purchases
```

10. According to the methodology suggested in this module, which step comes **first**?
##### R = Identify the question you are trying to answer
##### Plan first, then code.

11. According to the methodology suggested in this module, which step comes **last**?
##### R = Present the data in the appropriate context





