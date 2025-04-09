# Fabric_DataEng_Learning

## [Lakehouse - (Data Lake + Data Warehouses)](https://learn.microsoft.com/en-us/training/modules/get-started-lakehouses/2-fabric-lakehouse)
Fabric Lakehouse is a combination of a Data Lake and Data warehouse. It features the inexpensive scalability and flexbility of Data storage (in a Data Lake) while providing the analytical capabilities of SQL engine(of a Data Warehouse).

<img src="https://github.com/user-attachments/assets/aa69e4a5-d765-4e46-b462-cf26d358ba87" width="500"/>

### Data Ingestion 
The process of Data Ingestion refers to uploading your Data into your storage (or Lakehouse in this context). Fabric Lakehouse supports a wide range of common data formats from varying sources (e.g. local files, database or apis). Fabric `shortcut` connect to data hosted externally (e.g. Azure Data Lake Store Gen2 or OneLake)

Ingested Data can be transformed with ETL Techniques with Apache Sparks (with notebooks as a medium) or Dataflow Gen2

### Data Exploration & Transformation

Transform and load data

Most data requires transformations before loading into tables. You might ingest raw data directly into a lakehouse and then further transform and load into tables. Regardless of your ETL design, you can transform and load data simply using the same tools to ingest data. Transformed data can then be loaded as a file or a Delta table.

* Notebooks are favored by data engineers familiar with different programming languages including PySpark, SQL, and Scala.
* Dataflows Gen2 are excellent for developers familiar with Power BI or Excel since they use the PowerQuery interface.
* Pipelines provide a visual interface to perform and orchestrate ETL processes. Pipelines can be as simple or as complex as you need.

Analyze and visualize data in a lakehouse

After data is ingested, transformed, and loaded, it's ready for others to use. Fabric items provide the flexibility needed for every organization so you can use the tools that work for you.

* Data scientists can use notebooks or Data wrangler to explore and train machine learning models for AI.
* Report developers can use the semantic model to create Power BI reports.
* Analysts can use the **SQL analytics endpoint** to query, filter, aggregate, and otherwise explore data in lakehouse tables.

By combining the data visualization capabilities of Power BI with the centralized storage and tabular schema of a data lakehouse, you can implement an end-to-end analytics solution on a single platform.

