# NOTES FROM SPARK COURSE (MODULE 4) :book:
## MACHINE LEARNING, APPLICATIONS OF SPARK

### APPLICATIONS OF MACHINE LEARNING

Businesses commonly go through a series of stages as their use of data matures:
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/databusinessovertime.png "Data use on business over time")

## MACHINE LEARNING FUNDAMENTALS

### What is Machine Learning?
A broad array of techniques that learns patterns and data, without being explicitly programmed.

### Types of Machine Learning
* Supervised
  * Labeled data points
  * Task is to predict that label
  * Can be further broken down into two groups
    * Classification
      * Predicts a discrete set of categories
        * Binary classification
        * Multiclass classification
    * Regression
      * Predict a continuous value
        * Finalcial Forecasting
        * Unbounded number rather than a category
* Unsupervised
  * No label to predict
  * Learning the natural structure of the data
  * E.g.: Clustering
* Reinforcement
* Semi-supervised


## LINEAR REGRESSION
### Model Training Life Cycle
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/modellifecycle.png "Model Training Life Cycle")
Here our training set is comprised of features and a single label. The features are the independent variables that we use to predict our dependent label.

### How do we determine what model to choose?
* Ask key stakeholders
* Explain what independent variables contributed to the end prediction
* You must understand why the algorithm made the precition

Some models are inherently very interpretable such as:
* Linear regression
* Decision trees
 
While other models, such as **neural networks** are very accurate but at a cost of interpretability.
 
### Accounting for Assumptions
 
Another factor is that different algorithms have different assumptions about the underlying distribution of the data.

* In terms of the underlying assumptions of linear regression, there is a linear relationship between the input features and the output.

### Lineal Regression

![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/lr.png "Linear regression")

### Multivariate Regression
![alt text](https://github.com/Immich/DataScienceSpecialization/blob/master/SPARK/imgs/MultivariateRegression.png "Multivariate LR")


### APPLYING MACHINE LEARNING WITH UDFs

#### Create UDF
MLflow can create a User Defined Function for us to use in PySpark or SQL. This allows for custom code (that is, functionality not in core Spark) to be run on Spark.

You can use `spark.udf.register` to register this Python UDF in the SQL namespace and call it predictUDF.
```sql
%python
try:
  import mlflow
  from mlflow.pyfunc import spark_udf

  model_path = "/dbfs/mnt/davis/fire-calls/models/firecalls_pipeline"
  predict = spark_udf(spark, model_path, result_type="string")

  spark.udf.register("predictUDF", predict)
except:
  print("ERROR: This cell did not run, likely because you're not running the correct version of software. Please use a cluster with `DBR 5.5 ML` rather than `DBR 5.5` or a different cluster version.")
```



## READINGS
* [Linear Regression](https://www.khanacademy.org/math/ap-statistics/bivariate-data-ap/least-squares-regression/v/regression-residual-intro)
* [Logistiv Regression](https://towardsdatascience.com/logistic-regression-detailed-overview-46c4da4303bc)
* [Confusion Matrix](https://en.wikipedia.org/wiki/Confusion_matrix)
* [Detecting Financial Fraud at Scale with Decision Trees and MLflow on Databricks](https://databricks.com/blog/2019/05/02/detecting-financial-fraud-at-scale-with-decision-trees-and-mlflow-on-databricks.html)
* [Managed MLflow on Databricks now in public preview](https://databricks.com/blog/2019/03/06/managed-mlflow-on-databricks-now-in-public-preview.html)
* [Accelerating the Machine Learning Lifecycle with MLflow 1.0](https://www.youtube.com/watch?v=QJW_kkRWAUs&feature=youtu.be&t=1377)
