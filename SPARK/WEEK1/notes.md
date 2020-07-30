# NOTES FROM SPARK COURSE :book:

## WHY DISTRIBUTING COMPUTING?

### BIG DATA DEFINED

More data that can fit on any one machine. This can range from:
* Gigabytes
* Terabytes
* Tetabytes

### QUALITIES OF BIG DATA

1. Volume
2. Velocity
3. Variety
4. Veracity

### APACHE SPARK
Provide the first unified analytics engine. Before Spark there were lots of tools available but they were hard to piece together.

### SPARK SUPPORTS MANY LANGUAGES
* SQL
* Python
* Scala
* Java
* R

Using any of these languages, data analysts can run queries and reports. Data scientists can train and deploy machine learning models, and data engineers can use Scala to work with live streams of incoming data and to clean new data with nightly jobs.

### WHY SPARK IS POPULAR

* Reads and processes data from many disparate sources, including databases, BLOB stores, data warehouses, and files like CSVs.

## DISTRIBUTING COMPUTING AND PARALLELISM

* Scaling workloads to increasingly larger datasets

In computer science, we refer to this process of distributing computation as parallelism.

### Amdahl's law is the law that governs parallelism.

At a high level, it states that the amount of speedup we would see from parallelizing a given task is a function of how much of that task can be computed in parallel.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/WEEK1/img/amdahlslaw.png "Amdahl's Law")

Spark works so well because it is able to achieve what's called linear scalability, where it divides tasks across a cluster of machines so well that we continue to see improvements up to thousands of machines.


### WHEN AND WHERE USE SPARK

* When you need to Scale out
* When you need to Speed up

You need to scale out if you have too much data to process on a single machine. Even if your data can't fit on a single machine, you might benefit from speeding up your query by adding more compute resources.


## SPARK DATAFRAMES

Explain the difference between RDD and Dataframe API within spark

### WHAT DATAFRAMES ARE NOT
* SPARK is not a database
###### * It's a compute engine that can read from databses
###### * Data is ephemeral
* DataFrames are not SQL tables, Excel files, etc.
###### * They are abstractions on top of these underlying data sources

DataFrames inherits RDD properties (resilient (fault tolerant) + distributed(computed accross multiple nodes)) **plus** metadata.

##### Metadata
⋅⋅* Number of columns
⋅⋅* Data types

### Depth into one of the optimizers for Spark DataFrames called Catalyst.
When you're using the DataFrame API, you specify what you want to be done not how you want it to be done. It's declarative as opposed to imperative. 

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/WEEK1/img/catalyst.png "Spark DataFrame execution")
(Original from: https://mapr.com/blog/how-spark-runs-your-applications/)

1. Whether you write your query in SQL, or in Python, or Scala, it's going to go through the step called the **unresolved logical plan**
2. It's then going to look up in the data catalog, what your data sources are that you're operating on and different data types
3. And it's going to resolve them and create a **logical plan**.
4. Then if Catalyst notices that you're doing something a little bit funky, you could've joined earlier up, or later on, it can go ahead and actually rearrange your query plan.
5. Then it'll generate one or more physical plans, because there's many different ways you can execute the same query
6. Then it's run through this expected cost model
⋅⋅* You pick the one with the lowest expected cost and that's your selected physical plan


## DATABRICKS ENVIRONMENT

### WHAT IS DATABRICKS?

* Unified Analytics Platform
* Enables users to run all analytics in one place

### Capabilities

* Running reports
* Powering dashboards
* Running ETL jobs
* Machine Learning and Streaming jobs
* Databricks is more optimized than Apache Spark

### The platform

KEY COMPONENTS:
* Hosted notebook environment
* Allows real-time interaction with data running cells of code on Databricks server
* Eases installation and setup of networked machines

Databricks runtime is open-source Spark plus a number of optimizations, and additional functionality.

### Optimizations
Runs on multiple cloud servers:
* Amazon Web Services (AWS)
* Microsoft Azure

### Colaboration and Sharing

1. Go to Databricks
2. Start a new cluster
We call it "My First Cluster"
3. Runtime 5.5ML (I set it to 7.0ML) python3
4. Click Home
4.1. Click on my user email
4.2. Click on import
4.3. Import by URL (https://files.training.databricks.com/courses/davis/Lessons.dbc)

If we click the directory, we'll see that we have four different folders.
* One for each module in our course.
* The *Includes* folder, this is just some background logic that'll help make sure all of the data is where it needs to be, and do a few other things to configure the environment.

### CREATE NOTEBOOK

With Databricks Community Edition, you can invite up to three different people to be part of your workspace.


### SQL in Databricks

Create a database and a table, compute aggregate statistics against a dataset, and create visualizations.
Before we can do that, We need to mount some data. A mount is simply a pointer to a remote storage location, typically AWS or Azure, so we can access that data from within Databricks. 

########## Check what a %fs is

### SLOT
At a high level, a slot is a unit of parallelism.
