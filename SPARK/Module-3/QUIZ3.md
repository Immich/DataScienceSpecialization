# QUIZ MODULE 3

1. Decoupling storage and compute means storing data in one location and processing it using a separate resource. What are the benefits of this design principle? (Select all that apply.)
##### R =
* It maked updates to new software versions easier
  * New database and computation versions can be installed on new hardware due to the ephemeral nature of the underlying data.
* It allows for elastic resources so larger storage or compute resources are used only when needed
  * Decoupled resources that aren't utilized can easily be shut down
* Resources are isolated and therefore more manageable and debuggable
  * With each component of the architecture responsible for specific tasks, debugging is significantly easier
  
2. You want to run a report entailing summary statistics on a large dataset sitting in a database. What is the main resource limitation of this task?
##### R = IO: the transfer of data is more demanding than the computation

3. Processing virtual shopping cart orders in real time is an example of...
##### R = Online Transaction Processing (OLTP)

4. When are BLOB stores an appropriate place to store data? (Select all that apply.)
##### R =
* For storing large files
* For a "data lake" of largely unstructured data
* For cheap storage

5. JDBC is the standard protocol for interacting with databases in the Java environment. How do parallel connections work between Spark and a database using JDBC?
##### R = Specify a column, number of partitions, and the column's minimum and maximum values. Spark then divides that range of values between parallel connections. Spark uses the max and min of a range of values to know which connection should receive which data.

6. What are some of the advantages of the file format Parquet over CSV? (Select all that apply.)
##### R =
* Compression
  * Parquet is compressed by default and has many additional compression options
* Parallelism
  * Parquet easily parallelized so one file is written per Spark connection
* Columnar
  * Parquet is a column-based rather than a row-based format
  
7. SQL is normally used to query tabular (or "structured") data. Semi-structured data like JSON is common in big data environments. Why? (Select all that apply.)
##### R =
* It allows for data change over time
  * JSON allows for schema evolution over time
* It allows for complex data types
  * Complex types like arrays are allowed in JSON
* It does not need a formal structure
  * No formal structure is needed to be declared in advance like with relational tables
* It allows for missing data
  * JSON does not require all keys to appear in a dataset
  
8. Data writes in Spark can happen in serial or in parallel. What controls this parallelism?
##### R = The number of data partitions in DataFrame

9. Fill in the blanks with the appropriate response below:
##### A _______ table manages _______and a DROP TABLE command will result in data loss.
##### R =
Managed, both the data and metadata such as the schema and data location. When dropping a managed table, the underlying data will be deleted too.


