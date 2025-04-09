# [Delta Table](https://learn.microsoft.com/en-us/training/modules/work-delta-lake-tables-fabric/3-create-delta-tables)

## Delta Table Introduction
Tables in Microsoft Fabric lakehouses are Delta tables, signified by the triangular Delta (Δ) icon. For each delta table, the lakehouse stores the **parquet data file** and a **_delta_Log** folder in which transaction details are logged in JSON format. 


## Creating Delta Tables
Delta Tables can be created from different means.

### From DataFrame in Spark Framework
   
  ```
Load a file into a dataframe
df = spark.read.load('Files/mydata.csv', format='csv', header=True)

Save the dataframe as a delta table
df.write.format("delta").saveAsTable("mytable")
  ```

### From Spark SQL

   ```
  --%%sql
  
  CREATE TABLE salesorders
  (
      Orderid INT NOT NULL,
      OrderDate TIMESTAMP NOT NULL,
      CustomerName STRING,
      SalesTotal FLOAT NOT NULL
  )
  USING DELTA
  
   ```

### DeltaTableBuilder API

```
from delta.tables import *

DeltaTable.create(spark) \
  .tableName("products") \
  .addColumn("Productid", "INT") \
  .addColumn("ProductName", "STRING") \
  .addColumn("Category", "STRING") \
  .addColumn("Price", "FLOAT") \
  .execute()
```

### External Table (vs. Managed Table)

#### Managed Table
1. Table Definition & Data Files managed by Spark runtime in Fabric Lakehouse
2. Deleting the Table also deletes the underlying files found in the **Tables** storage location

#### External Table
1. Relational table definition in the metastore is mapped to an alternative file storage location
2. Table definition is stored in **Table** while the data file is stored in **file**
3. Deleting the Table **DOES NOT** delete the underlying data file


## Optimizing Delta Tables

Spark is a parallel-processing framework, with data stored on one or more worker nodes. It works with Parquet files which are immutable. As an result, new files written for every update or delete. 
This result in the `small file problem` in which Spark stores data in a large number of small files. It means that queries over large amounts of data can run slowly, or even fail to complete.

### OptimizeWrite Function
The OptimizeWrite function is a Delta Lake feature which reduces the number of small number being written. The `small file problem` is mitigated by writing fewer larger files, instead of writing many small files.

<img src="https://github.com/user-attachments/assets/dfaf8822-35ae-4561-ba9b-3e26b652249f" width = "500"></img>

### Optimize
Optimize is a table maintenance feature, consolidating small Parquet files into fewer large files in large tables. This results in:

* fewer larger files
* better compression
* efficient data distribution across nodes

<img src="https://github.com/user-attachments/assets/d33828ef-be71-446a-9f7b-9c2dc72d8887" width = "500"></img>

### V-Order Function
When you run Optimize, you can optionally run V-Order, which is designed for the Parquet file format in Fabric. V-Order enables lightning-fast reads, with in-memory-like data access times.
It also improves cost efficiency as it reduces network, disk, and CPU resources during reads.

V-Order incurs a small overhead of about 15% making writes a little slower. However, it enables faster reads from the Microsoft Fabric compute engines, such as Power BI, SQL, Spark, and others.

### Vacuum Function
The VACUUM command enables you to remove old data files. Every time an update or delete is done, a new Parquet file is created and an entry is made in the transaction log. 
Old Parquet files are retained to enable time travel, which means that Parquet files accumulate over time.

## Partitioning Delta Table
Delta Lake allows you to organize data into partitions. This might improve performance by enabling data skipping, which boosts performance by skipping over irrelevant data objects based on an object's metadata.
e.g. You could partition sales data by year. The partitions are stored in subfolders named "year=2021", "year=2022", etc. 
If you only want to report on sales data for 2024, then the partitions for other years can be skipped, which improves read performance.

Partitioning of small amounts of data can degrade performance, however, because it increases the number of files and can exacerbate the "small files problem."

Use partitioning when:

* You have very large amounts of data.
* Tables can be split into a few large partitions.

Don't use partitioning when:

* Data volumes are small.
* A partitioning column has high cardinality, as this creates a large number of partitions.
* A partitioning column would result in multiple levels.

<img src="https://github.com/user-attachments/assets/101ac25c-e171-44d5-8f4c-12b8fc68f28a" width = "500"></img>

## Working with Delta Table in Spark

### Using Spark SQL
The most common way to work with data in delta tables in Spark is to use Spark SQL.

```
spark.sql("INSERT INTO products VALUES (1, 'Widget', 'Accessories', 2.99)")
```

```
%%sql

UPDATE products
SET Price = 2.49 WHERE ProductId = 1;
```

### Delta API
Create an instance of a DeltaTable from a folder location containing files in delta format, and then use the API to modify the data in the table.

```
from delta.tables import *
from pyspark.sql.functions import *

# Create a DeltaTable object
delta_path = "Files/mytable"
deltaTable = DeltaTable.forPath(spark, delta_path)

# Update the table (reduce price of accessories by 10%)
deltaTable.update(
    condition = "Category == 'Accessories'",
    set = { "Price": "Price * 0.9" })
```
## Working Streaming Data in Delta Table



