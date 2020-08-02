# NOTES FROM SPARK COURSE (MODULE 2) :book:
## SPARK TERMINOLOGY

### SPARK LOCAL MODE

A Spark cluster is made up of one driver and one or more executors. But if you want to keep costs down and you want a prototype with Spark you can use something called Spark Local Mode in which case the driver and the executor *are on the same physical machine*.
In this case, when trying to do any Spark queries, the driver tells the executor what to do then it turns around and actually does it itself.

### Unit of parallelism within a Spark cluster

* Spark operates on a cluster of machines
* Each of those machines can have multiple cores
* Each of those cores can have multiple threads

To calculate the units of parallelism for their cluster configuration.

MCT: machines * cores * threads

#### We denote the smallest unit of parallelism, whether it is a core or a thread, as a slot.

* Units of parallelism for data are called *Partitions*
* Partitions are part of a large distributed dataset

4 executors * 2 slots = 8 units of parallelism

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/diagram1.png "parallelism")

### Determining the number of Partitions 

* Size of dataset
    * The larger the dataset, the more partitions
* Underlying partitioning of data by some other deatures
* Cluster configurations – What happens if I add more partitions?


### Caching
This means that this data isn't serialized, so it'll be much faster to query later on because we don't have to pay the cost of deserializing it. However, it will take up more space than the corresponding serialized table.

```SQL
CACHE TABLE fireCalls
```

This means is it will only cache the data as it's required. It's only going to cache the data once we query it.

```SQL
CACHE LAZY TABLE fireCalls
```

### Shuffle Partitions in SPARK

#### Narrow Transformation
Is any transformation to your data that can be done on each partition in parallel.
We don't need any information about the data stored in the other partitions to perform this operation. *We can filter the data locally*.

For example, when working with the San Francisco Fire Calls dataset, we can filter out for specific call type such as medical, and we don't need any information about the data stored in the other partitions to perform this operation.
##### e.g.: select, where, etc.

#### Wide Transformation
Requires information from other partitions.

For example, what if we wanted to know which neighborhood had the most calls? In this case, we would have to aggregate our information by neighborhood and then count the number of calls. This would involve communicating data across our executors in our cluster, since not all the data for given neighborhood reside in the same partition. 
**Data Shuffle Required**
##### e.g.: group by, order by, etc.

However, with wide transformations, the number of post shuffle partitions is set to 200. It doesn't matter if your data is small or large or if your cluster configuration has 20 executors, it is still 200. Luckily, you can change this parameter depending on your needs.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/shufflePartitions.png "shuffle partitions")

The reason why the default is 200 is from real-world experience that was found to be a very good default.

##### The parameter that controls the parallelism that results from a shuffle is a parameter called **spark.sql.shuffle.partitions**. You can set this either within your notebook:
```sql
SET spark.sql.shuffle.partitions=8
```

##### Or you can set it at time of cluster creation:
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/sqlConf.png "parameter shuffle partitions")


The difference between these two methods is if you take this approach and set it when you create the cluster, that parameter is set for every notebook that gets attached to that cluster.

##### A *stage boundary* occurs when all of your slots or available units of processing have to sync up with each other. So Spark is also known as a bulk synchronous processing engine.

### Boadcasting Joins

In a standard join, all the data is shuffled and we'd have to join all of your data locally. And then you're going to have to shuffle it across the cluster to get all of the reds together for dataset A and dataset B. But this is very expensive.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/standardjoin.png "standar join")


An alternate way of joining our datasets is doing something called a broadcast join. If we have two datasets and one is significantly smaller than the other, instead of partitioning it up across our three workers, we instead broadcast an entire copy of that dataset to every worker. So we can do those joins locally. This will be a lot more efficient.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/broascastjoin.png "broadcast join")


We can join these two datasets and examine the physical plan (how data is physically affected) using `EXPLAIN`.

```sql
EXPLAIN 
  SELECT * 
  FROM fireCalls 
  JOIN fireCallsParquet on fireCalls.`Call Number` = fireCallsParquet.`Call_Number`
```
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/mergejoin.png "merge join plan")

##### Automatic and Manual broadcasting
* Depending on size of the data that is being loaded into Spark, Spark uses internal heuristics to decide how to join that data to other data.
* Automatic broadcast depends on `spark.sql.autoBroadcastJoinThreshold`
    * The setting configures the maximum size in bytes for a table that will be broadcast to all worker nodes when performing a join
    * Default is 10MB
* A `broadcast` function can be used in Spark to instruct Catalyst that it should probably broadcast one of the tables that is being joined.

If the `broadcast` hint isn't used, but one side of the join is small enough (i.e., its size is below the threshold), that data source will be read into the Driver and broadcast to all Executors.

```python
%python
spark.conf.get("spark.sql.autoBroadcastJoinThreshold")
```

Now take a look at the physical plan when we broadcast one of the datasets. The broadcast join hint is going to operate like a SQL hint, but Spark will still parse this even though it is commented out.

```sql
EXPLAIN 
  SELECT /*+ BROADCAST(fireCalls) */ * 
  FROM fireCalls 
  JOIN fireCallsParquet on fireCalls.`Call Number` = fireCallsParquet.`Call_Number`
```

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/broadcastjoinplan.png "broadcast join plan")


