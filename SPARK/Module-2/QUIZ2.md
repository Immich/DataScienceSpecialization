# QUIZ MODULE 2

1. What are the different units of parallelism? (Select all that apply.)
  R =
  * Executor
  * Partition
  * Core
  * Task
  
2. What is a partition?
  R = A portion of a large distributed set of data.
  
3. What is the difference between in-memory computing and other technologies? (Select all that apply.)
  R =
  * In-memory operations were not realistic in older technologies when memory was more expensive
    * The price of memory has come down drastically enabling Spark to rely on in-memory calculations
  * In-memory operates from RAM while other technologies operate from disk
  * Computation not done in-memory (such as Hadoop) reads and writes from disk in between each step
    * Hadoop (the precursor to Spark) was much slower because it had to read from and write to disk between every step
    
4. Why is caching important?
  R = It stores data on the cluster to improve query performance.
  
5. Which of the following is a wide transformation? (Select all that apply.)
  R =
  * ORDER BY
  * GROUP BY
  
  
6. Broadcast joins...
  R = Transfer the smaller of two tables to the larger, minimizing data transfer
  
7. When is it appropriate to use a shuffle join?
  R = When both tables are moderately sized or large. Shuffle joins are more efficient when both tables are of similar, larger sizes.
  
8. Which of the following are bottlenecks you can detect with the Spark UI? (Select all that apply.)
  R =
  * Data Skew
  * Shuffle reads
  * Shuffle writes
  
9. What is a stage boundary?
  R = When all of the slots or aavailable units of processing have to sync with one another. A stage boundary is when all Spark tasks must come together to exchange a result.
  
10. What happens when Spark code is executed in local mode?
  R = The executor and driver are on the same machine. Local mode refers to when the executor and driver are the same machine, such as when prototyping Spark code on our laptop.
