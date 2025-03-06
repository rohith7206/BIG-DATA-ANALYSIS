# BIG-DATA-ANALYSIS

**COMPANY**: CODETECH IT SOLUTIONS

**NAME**:SULAKE ROHITH

**INTERN ID**:CODHC116

**DOMAIN**:DATA ANALYSIS

**DURATION**:8 WEEKS

**MENTOR**:NEELA SANTOSH

Performing data analysis on a large dataset using pyspark library 

🔹 INSTALLATION OF PYSPARK

Install PySpark: pip install pyspark

🔹 IMPORTING THE LIBRARIES:

SparkSession: Required to initialize a Spark environment.

StructType & StructField: Define a custom schema for the dataset.

col, count, mean: Functions used for column operations and aggregations.

🔹INITIALIZING THE SPARK SESSION :

Starts a SparkSession, which acts as an entry point for interacting with Spark.

The application is named "IrisDatasetAnalysis".

🔹DEFINING SCHEMA FOR THE DATASET:

We define a structured schema to ensure proper data types:

DoubleType() for numeric columns (sepal & petal dimensions).

StringType() for the species column.

Setting True allows null values.

🔹LOADING THE DATA:

read the iris dataset as a dataframe.

🔹PRINT SCHEMA AND COMPUTE STATISTICS:

getting an overview of data distribution and counting the missing values , filling the missing values and count each species type.

🔹STOPPING THE SPARK SESSION:

releases resources after processing. 

# Big Data Analytics using PySpark: Iris Dataset Analysis

## Introduction
This document provides a detailed explanation of the **Iris Dataset Analysis** using **Apache Spark** and **PySpark**. The objective of this task is to analyze the dataset, handle missing values, and perform basic statistical operations using the distributed computing capabilities of PySpark. Additionally, it highlights the advantages of using PySpark for big data analytics.

---

## 1. Prerequisites
Before executing the script, ensure the following:
- **Apache Spark** is installed.
- **PySpark** is installed (`pip install pyspark`).
- **Jupyter Notebook** (optional, for interactive execution).
- The dataset `iris.csv` is available in the specified path.
- A basic understanding of **Python** and **SQL** is helpful.

---

## 2. Importing Required Libraries
```python
from pyspark.sql import SparkSession
from pyspark.sql.types import StructType, StructField, DoubleType, StringType
from pyspark.sql.functions import col, count, mean, stddev, max, min
```
### Explanation:
- `SparkSession`: Initializes the Spark environment.
- `StructType` & `StructField`: Define the dataset schema.
- `DoubleType`, `StringType`: Data types for numeric and categorical columns.
- `col`, `count`, `mean`, `stddev`, `max`, `min`: Functions for column-based operations and aggregations.

---

## 3. Initializing Spark Session
```python
spark = SparkSession.builder.appName("IrisDatasetAnalysis").getOrCreate()
```
### Explanation:
- Creates a Spark session named **IrisDatasetAnalysis** to process the dataset.
- Spark provides **distributed computing**, enabling efficient handling of large datasets.

---

## 4. Defining Schema
```python
schema = StructType([
    StructField("sepal_length", DoubleType(), True),
    StructField("sepal_width", DoubleType(), True),
    StructField("petal_length", DoubleType(), True),
    StructField("petal_width", DoubleType(), True),
    StructField("species", StringType(), True)
])
```
### Explanation:
- Defines a structured schema to ensure correct data types.
- **DoubleType()** for numerical columns and **StringType()** for the species column.
- The `True` parameter allows null values in columns.
- Enforcing schema prevents errors and ensures consistency in data processing.

---

## 5. Loading the Dataset
```python
df = spark.read.csv("/content/iris.csv", header=True, schema=schema)
```
### Explanation:
- Reads the `iris.csv` file as a **Spark DataFrame**.
- `header=True` ensures that the first row is treated as column names.
- The defined `schema` is applied to ensure consistency.
- Using **Spark DataFrame API** allows optimized operations on large datasets.

---

## 6. Displaying Schema
```python
df.printSchema()
```
### Explanation:
- Prints the schema of the dataset to verify column names and data types.
- Ensures proper data type assignment before processing.

---

## 7. Generating Basic Statistics
```python
df.describe().show()
```
### Explanation:
- Computes summary statistics (count, mean, std dev, min, max) for numerical columns.
- Provides an overview of the data distribution.
- Helps identify potential **outliers** or **data inconsistencies**.

---

## 8. Counting Missing Values
```python
missing_counts = df.select([count(col(c)).alias(c) for c in df.columns])
missing_counts.show()
```
### Explanation:
- Counts the number of **non-null** values for each column.
- If a column has fewer values than expected, it contains **missing data**.
- Helps in making decisions regarding data cleaning strategies.

---

## 9. Handling Missing Values
```python
numeric_cols = [c for c, t in df.dtypes if t == 'double']
mean_values = df.select([mean(col(c)).alias(c) for c in numeric_cols]).collect()[0]
df = df.fillna({col_name: mean_values[col_name] for col_name in numeric_cols})
```
### Explanation:
- Identifies numeric columns (`double` type).
- Computes **column-wise mean values**.
- Uses `fillna()` to replace missing values with the **mean of the column**.
- Ensures that no missing values remain in numeric columns.
- This approach prevents **bias in machine learning models** and maintains data integrity.

---

## 10. Grouping Data by Species
```python
grouped_df = df.groupBy("species").agg(count("*").alias("count"))
grouped_df.show()
```
### Explanation:
- Groups data by **species**.
- Uses `count("*")` to count occurrences of each species.
- Helps analyze species distribution in the dataset.
- Useful for **classification models and clustering algorithms**.

---

## 11. Additional Data Analysis (Optional)
```python
df.select(mean("sepal_length"), stddev("sepal_length"), max("sepal_length"), min("sepal_length")).show()
```
### Explanation:
- Computes **mean, standard deviation, max, and min** for `sepal_length`.
- Helps in understanding the **spread and range** of the data.
- Similar operations can be applied to other numerical columns.

---

## 12. Stopping the Spark Session
```python
spark.stop()
```
### Explanation:
- Properly shuts down the Spark session to free up resources.

---

## Summary of Analysis
| **Step**            | **Purpose** |
|---------------------|------------|
| Import Libraries   | Load required PySpark modules. |
| Start SparkSession | Initialize Spark for processing. |
| Define Schema      | Ensure proper data types. |
| Load Data          | Read the Iris dataset as a DataFrame. |
| Print Schema       | Verify data structure. |
| Compute Statistics | Get an overview of data distribution. |
| Count Missing Data | Identify missing values. |
| Fill Missing Data  | Replace NaN values with mean. |
| Group by Species   | Count each species type. |
| Additional Analysis | Compute mean, stddev, max, min. |
| Stop Spark Session | Release resources after processing. |

---

## Key Learnings
- **Schema enforcement** ensures data integrity.
 
- **Basic statistics** help in understanding dataset distribution.
 
- **Handling missing values** prevents errors in analysis.
 
- **Aggregations (groupBy, count, mean, stddev, etc.)** are useful for data summarization.
 
- **Spark DataFrame API is highly efficient** for handling large-scale datasets.
 
 Big Data Analytics: An Overview

Big Data Analytics is the process of examining large, complex datasets (Big Data) to uncover hidden patterns, correlations, market trends, customer preferences, and other useful business insights. It helps organizations make data-driven decisions by analyzing structured, semi-structured, and unstructured data.


🔹 What is Big Data?

Big Data refers to massive volumes of data that cannot be processed efficiently using traditional databases or software. It is characterized by the 5 Vs:


Volume – Huge amounts of data generated daily (terabytes, petabytes).

Velocity – Data is generated at high speed (real-time data streams, IoT).

Variety – Data comes in multiple formats (structured, unstructured, semi-structured).

Veracity – Data quality and reliability must be ensured.

Value – The insights extracted from data provide business benefits.

🔹 Types of Big Data Analytics

Descriptive Analytics – Summarizes past data to understand what happened.


Example: Sales reports, customer purchase history.

Diagnostic Analytics – Analyzes past data to determine why something happened.


Example: Root cause analysis of a system failure.

Predictive Analytics – Uses statistical models & machine learning to predict future trends.


Example: Forecasting stock prices, customer churn prediction.

Prescriptive Analytics – Provides recommendations to optimize decision-making.


Example: AI-powered medical diagnosis, automated financial trading.

🔹 How Does Big Data Analytics Work?

Data Collection – Gather data from multiple sources (social media, sensors, transactions).

Data Storage – Store data in databases, data lakes (Hadoop, AWS S3).

Data Processing – Process large-scale data using Hadoop, Spark, SQL, NoSQL.

Data Analysis – Use machine learning, statistics, and AI to extract insights.

Data Visualization – Present insights using dashboards, charts (Tableau, Power BI).

🔹 Tools Used in Big Data Analytics

Category	Popular Tools

Big Data Processing	Apache Spark, Hadoop, PySpark

Databases	MongoDB, Cassandra, HBase, Amazon Redshift

Machine Learning	TensorFlow, Scikit-learn, PyTorch

Data Visualization	Tableau, Power BI, Matplotlib, Seaborn

🔹 Applications of Big Data Analytics

✅ Healthcare – Disease prediction, personalized medicine.

✅ Finance – Fraud detection, algorithmic trading.

✅ Retail – Customer segmentation, recommendation engines.

✅ Manufacturing – Predictive maintenance, quality control.

✅ Social Media – Sentiment analysis, trend prediction.

✅ Cybersecurity – Threat detection, anomaly detection.









