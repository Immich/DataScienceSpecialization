# NOTES FROM SPARK COURSE (MODULE 3) :book:

## ENGINEERING DATA PIPELINES

### Pipelining
The processof moving data throug an application

### Data ecosystems
* Legacy data warehouses
* Databases
* Data lakes

##### Spark offers a unified way of accessing data where it lives.

## SPARK AS A CONNECTOR

This is an example of a common big data architecture:

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/bigdataarchitecture.png "big data architecture")

### Architecture needs:
* Scalability
  * A sacalable way to receive data
* ETL process
  * Raw data :arrow_right: usable data
* Transactional database
* Ad hoc queries
  * For instance, we might need to have data analysts and scientists running queries to discover something about our data. These are called ad-hoc queries or queries that were not incorporated in the original design of the application.
* Machine Learning
* Reporting
* Scalable data lake


### Core design principle: Decoupled Storage and Compute
* No data stays on the cluster
* Resources are elastic
* Updates are easy

By spinning up a Spark cluster when it's needed, connecting to data where it lives and shutting it down afterwards, not only can you save resources but you don't have to worry about updating your cluster to the latest version of Spark. 

### Two types of bottlenecks on computing tasks: IO vs. CPU Bound Problems

* IO stands for input-output (network/data transfer)
  * For instance, if you're reading 10 gigabytes of data from a database and then counting the records, the limiting factor on that task is the transfer of data from the database to the cluster as the computation that you're doing is quite trivial.
* CPU is computation (processing data)
  * For instance, we might need to do complex operations across a large amount of data such as training a machine learning model. Here we're not bound by the data transfer as much as the processing we need to do on that data.
* Data transfer is usually the bottleneck for tasks
* Spark solves this colocating your storage

### Online Analytical Processing (OLAP)

These types of workloads are in the broader category of business intelligence or how to analyze data for business needs.

* Reporting
* Ad hoc Analysis
* Blob stores
* Data warehouse

### Online Transaction Process (OLTP)

This involves some sort of transaction executed against a database.

* Databases
* Web traffic
* Streaming

The main difference between OLAP and OLTP workloads is whether the work needs to occur in real time. While most of an analyst's responsibilities fall under the category of OLAP, work with Spark is used for OLTP as well.

## ACCESING DATA

Connecting to two common data sources:

1. BLOB
  * A common way of storing large amounts of data
2. JDBC
  * Is an application programming interface or API for Java environments

Spark works well with JDBC, including a functionality called predicate push down, where aspects of SQL queries such as filter operations, can be done by the database itself transferring that data into the Spark cluster. This saves a lot of network transfer.


## FILE FORMATS

The ideal file format in distributed systems is Parquet.

* CSV files: row based
* Parquet: column based

Parquet is a lot faster. This is for a number of reasons:
1. It's able to compress our data so we have less data actually moving across the network
2. It also stores enough of the metadata so that we don't have to worry about the schema inference which was part of the big cost associated with reading this data
3. Highly splittable "file format"
4. Free & Open Source
5. Increased query performance over row-based data stores
6. Designed for performance on large data sets
7. Supports limited schema evolution
8. A Column-Oriented data store

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/comparisonparquetcsv.png "Comparison between parquet vs. csv")

### Reading Tables
* `spark.read.table(..)`
* The Databricks platform allows us to register a huge variety of data sources as tables via the Databricks UI
* Any DataFrame (from CSV, Parquet, whatever) can be registered as a temporary view
* Tables/Views can be loaded via the `DataFrameReader` to produce a `DataFrame`
* Tables/Views can be used directly in SQL statements

### Reading JSON
* `spark.read.json(..)`
* JSON represents complex data types unlike CSV's flat format
* Has many of the same limitations as CSV (needing to read the entire file to infer the schema)
* Like CSV has a lot of options allowing control on date formats, escaping, single vs. multiline JSON, etc.

### Reading Text
* `spark.read.text(..)`
* Reads one line of text as a single column named `value`
* Is the basis for more complex file formats such as fixed-width text files

### Reading JDBC
* `spark.read.jdbc(..)`
* Requires one database connection per partition
* Has the potential to overwhelm the database
* Requires specification of a stride to properly balance partitions


## SCHEMAS AND TYPES

### Why schemas matter?

* Schemas are at the heart of data structures in Spark.
* A schema describes the structure of your data by naming columns and declaring the type of data in that column.
* Rigorously enforcing schemas leads to significant performance optimizations and reliability of code.

### Schemas with Semi-Structured JSON Data
* **Tabular data**, such as that found in CSV files or relational databases, has a formal structure where each observation, or row, of the data has a value (even if it's a NULL value) for each feature, or column, in the data set.
* **Semi-structured data** does not need to conform to a formal data model. Instead, a given feature may appear zero, once, or many times for a given observation.

Semi-structured data storage works well with hierarchical data and with schemas that may evolve over time. One of the most common forms of semi-structured data is JSON data, which consists of attribute-value pairs.

### Read the JSON File
The command to read in JSON looks very similar to that of CSV.
In addition to reading the JSON file, we will also print the resulting schema.

```sql
CREATE OR REPLACE TEMPORARY VIEW fireCallsJSON
USING JSON 
OPTIONS (
    path "/mnt/davis/fire-calls/fire-calls-truncated.json"
  )
```
### Review: Reading from JSON w/ InferSchema
While there are similarities between reading in CSV & JSON there are some key differences:

* We only need one job even when inferring the schema
* There is no header which is why there isn't a second job in this case - the column names are extracted from the JSON object's attributes
* Unlike CSV which reads in 100% of the data, the JSON reader only samples the data

Note: In Spark 2.2 the behavior was changed to read in the entire JSON file.

### User-Defined Schemas
Spark infers schemas from the data, as detailed in the example above. Challenges with inferred schemas include:

* Schema inference means Spark scans all of your data, creating an extra job, which can affect performance
* Consider providing alternative data types (for example, change a Long to a Integer)
* Consider throwing out certain fields in the data, to read only the data of interest
* Just like CSV, providing the schema avoids the extra jobs
* The schema allows us to rename columns and specify alternate data types
* Can get arbitrarily complex in its structure

```sql
CREATE OR REPLACE TEMPORARY VIEW fireCallsJSON ( 
  `Call Number` INT,
  `Unit ID` STRING,
  `Incident Number` INT,
  `Call Type` STRING,
  `Call Date` STRING,
  `Watch Date` STRING,
  `Received DtTm` STRING,
  `Entry DtTm` STRING,
  `Dispatch DtTm` STRING,
  `Response DtTm` STRING,
  `On Scene DtTm` STRING,
  `Transport DtTm` STRING,
  `Hospital DtTm` STRING,
  `Call Final Disposition` STRING,
  `Available DtTm` STRING,
  `Address` STRING,
  `City` STRING,
  `Zipcode of Incident` INT,
  `Battalion` STRING,
  `Station Area` STRING,
  `Box` STRING,
  `Original Priority` STRING,
  `Priority` STRING,
  `Final Priority` INT,
  `ALS Unit` BOOLEAN,
  `Call Type Group` STRING,
  `Number of Alarms` INT,
  `Unit Type` STRING,
  `Unit sequence in call dispatch` INT,
  `Fire Prevention District` STRING,
  `Supervisor District` STRING,
  `Neighborhooods - Analysis Boundaries` STRING,
  `Location` STRING,
  `RowID` STRING
)
USING JSON 
OPTIONS (
    path "/mnt/davis/fire-calls/fire-calls-truncated.json"
)
```
### Primitive and Non-primitive Types
The Spark `types` package provides the building blocks for constructing schemas.

A primitive type contains the data itself. The most common primitive types include:
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/primitivetypes.png "primitive types")

Non-primitive types are sometimes called reference variables or composite types. Technically, non-primitive types contain references to memory locations and not the data itself. Non-primitive types are the composite of a number of primitive types such as an Array of the primitive type `Integer`.

* The two most common composite types are `ArrayType` and `MapType`.

These types allow for a given field to contain an arbitrary number of elements in either an Array/List or Map/Dictionary form.

## WRITING DATA

Writing to a database in Spark differs from other tools largely due to its distributed nature. There are a number of variables that can be tweaked to optimize performance, largely relating to how data is organized on the cluster. Partitions are the first step in understanding performant database connections.

**A partition is a portion of your total dataset**, which is divided into many of these portions so Spark can distribute your work across a cluster.

The other concept needed to understand Spark's computation is a slot (also known as a core). **A slot/core is a resource available for the execution of computation in parallel**. In brief, a partition refers to the distribution of data while a slot refers to the distribution of computation.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/partitionslot.png "partitions")

As a general rule of thumb, the number of partitions should be a multiple of the number of cores. For instance, with 5 partitions and 8 slots, 3 of the slots will be underutilized. With 9 partitions and 8 slots, a job will take twice as long as it waits for the extra partition to finish.

### Controlling concurrency

In the context of JDBC database writes, the number of partitions determine the number of connections used to push data through the JDBC API. There are two ways to control this parallelism:

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/concurrency.png "concurrency")

Create a new temporary view that coalesces all of our data to a single partition. This can be done using a hint.

```sql
CREATE OR REPLACE TEMPORARY VIEW fireCallsCSV1p
  AS
SELECT /*+ COALESCE(1) */ * 
FROM fireCallsCSV
```

```python
%python
sql("SELECT * FROM fireCallsCSV1p").rdd.getNumPartitions()
```
Out[6]: 1

```sql
CREATE OR REPLACE TEMPORARY VIEW fireCallsCSV8p
  AS
SELECT /*+ REPARTITION(8) */ * 
FROM fireCallsCSV
```

```python
%python
sql("SELECT * FROM fireCallsCSV8p").rdd.getNumPartitions()
```
Out[6]: 8

#### Saving the results:
```python
%python
sql("SELECT * FROM fireCallsCSV8p").write.mode("OVERWRITE").csv(username + "/fire-calls-repartitioned.csv")
```

### Summary
* Note that coalesce means something different in ANSI SQL (that is, to return the first non-null value)
* Files like CSV and Parquet might look like single files, but Spark saves them as a folder of different parts

## MANAGED AND UNMANAGED TABLES

Data on the SPARK cluster disappears upon termination, unless it is saved elsewhere.

* **A managed table** is a table that manages both the data itself as well as the metadata.
  * In this case, a `DROP TABLE` command removes both the metadata for the table as well as the data itself.
* **Unmanaged tables** manage the metadata from a table such as the schema and data location, but the data itself sits in a different location, often backed by a blob store like the Azure Blob or S3.
  * Dropping an unmanaged table drops only the metadata associated with the table while the data itself remains in place.

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/managedandunmanaged.png "Managed and Unmanaged Tables")

### Summary
* Use external/unmanaged tables when you want to persist your data once the cluster has shut down
* Use managed tables when you only want ephemeral data

## Readings

* [Why You Should Care about Data Layout in the Filesystem](https://databricks.com/session/why-you-should-care-about-data-layout-in-the-filesystem)
* [Lessons From the Field: Applying Best Practices to Your Apache Spark Applications](https://www.youtube.com/watch?v=iwQel6JHMpA)
* [Working with Complex Data Formats with Structured Streaming in Apache Spark 2.1](https://databricks.com/blog/2017/02/23/working-complex-data-formats-structured-streaming-apache-spark-2-1.html)

