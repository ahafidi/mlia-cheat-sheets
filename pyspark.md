# PySpark Cheat Sheet

## Table of Contents

- [1. Initialization](#1-initialization)
- [2. DataFrame Creation](#2-dataframe-creation)
- [3. DataFrame Operations](#3-dataframe-operations)
- [4. Data Manipulation](#4-data-manipulation)
- [5. Aggregations and Analysis](#5-aggregations-and-analysis)
- [6. Data Input/Output](#6-data-inputoutput)
- [7. Advanced Features](#7-advanced-features)
- [8. Performance Optimization](#8-performance-optimization)

## 1. Initialization

```python
from pyspark.sql import SparkSession

# Create Spark session
spark = SparkSession.builder \
    .appName("AppName") \
    .getOrCreate()
```

## 2. DataFrame Creation

```python
from pyspark.sql import Row

# From List of Tuples
data = [(1, "Alice", 29), (2, "Bob", 35), (3, "Cathy", 25)]
columns = ["id", "name", "age"]
df = spark.createDataFrame(data, columns)

# From RDD
rdd = spark.sparkContext.parallelize(data)
df_from_rdd = spark.createDataFrame(rdd, columns)

# From Files
df_json = spark.read.json("data.json")
df_csv = spark.read.csv("data.csv", header=True, inferSchema=True)
df_parquet = spark.read.parquet("data.parquet")
```

## 3. DataFrame Operations

```python
# Viewing Data
df.show()                    # Show top 20 rows
df.show(5)                   # Show top 5 rows
df.printSchema()             # Print schema
df.columns                   # List column names
df.describe().show()         # Summary statistics
df.count()                   # Count rows

# Selecting Data
df.select("name", "age").show()
df.select(*columns).show()   # Select multiple columns

# Filtering Data
df.filter(df.age > 30).show()
df.where(df.name == "Alice").show()
df.filter((df.age > 25) & (df.name != "Bob")).show()
```

## 4. Data Manipulation

```python
from pyspark.sql.functions import col

# Column Operations
df.withColumn("age_plus_10", col("age") + 10).show()
df.withColumnRenamed("name", "full_name").show()

# Handling Missing Data
df.na.drop()                         # Drop rows with null values
df.na.fill("unknown")                # Fill missing values
df.na.fill({"age": 30})              # Fill specific column
```

## 5. Aggregations and Analysis

```python
from pyspark.sql.functions import avg, count, sum

# Grouping and Aggregation
df.groupBy("age").count().show()
df.groupBy("age").agg(
    avg("id").alias("avg_id"),
    count("*").alias("count")
).show()

# Sorting
df.orderBy("age").show()
df.orderBy(col("age").desc()).show()

# Joins
df1.join(df2, df1.id == df2.id, "inner")  # Inner Join
df1.join(df2, df1.id == df2.id, "left")   # Left Join
df1.join(df2, df1.id == df2.id, "right")  # Right Join
df1.join(df2, df1.id == df2.id, "outer")  # Full Outer Join
```

## 6. Data Input/Output

```python
# Writing Data
df.write.mode("overwrite").csv("output.csv", header=True)
df.write.mode("overwrite").json("output.json")
df.write.mode("overwrite").parquet("output.parquet")
```

## 7. Advanced Features

```python
from pyspark.sql.functions import udf
from pyspark.sql.types import IntegerType

# User-Defined Functions (UDFs)
def age_double(age):
    return age * 2

udf_double = udf(age_double, IntegerType())
df.withColumn("double_age", udf_double(col("age"))).show()

# RDD Operations
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
rdd.map(lambda x: x * 2).collect()      # [2, 4, 6, 8, 10]
rdd.filter(lambda x: x % 2 == 0).collect() # [2, 4]
rdd.reduce(lambda a, b: a + b)          # 15
```

## 8. Performance Optimization

```python
# Caching
df.cache()                  # Cache DataFrame
df.persist()                # Persist DataFrame in memory/disk
df.unpersist()              # Remove from cache

# Configuration
spark.conf.set("spark.sql.shuffle.partitions", 100)   # Adjust shuffle partitions
spark.conf.get("spark.sql.shuffle.partitions")        # Get current setting
```
