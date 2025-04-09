# Data Pipeline

## Pipeline Introduction

Pipeline refers to a series of activities that perform data movement and processing tasks
* e.g. define data transfer and transformation activities
* orchestrate these activities through control flow activities that manage branching, looping, and other typical processing logic. 

## Core Concepts

### Activities
Activities are the executable tasks, which may be sequencially connected in a pipeline.
The outcome of a particular activity (success, failure, or completion) can be used to direct the flow to the next activity in the sequence.

#### Data Transformation Activities
Activities that encapsulate data transfer operations, including simple Copy Data activities that extract data from a source and load it to a destination.
Complex Data Flow activities that encapsulate dataflows (Gen2) that apply transformations to the data as it is transferred. 

Other Activities include
* Notebook activities to run a Spark notebook
* Stored procedure activities to run SQL code
* Delete data activities to delete existing data

#### Control Flow Activities
Activities that you can use to implement loops, conditional branching, or manage variable and parameter values. 
The wide range of control flow activities enables you to implement complex pipeline logic to orchestrate data ingestion and transformation flow.

### Parameters
Pipelines can be parameterized, enabling you to provide specific values to be used each time a pipeline is run. For example, you might want to use a pipeline to save ingested data in a folder, 
but have the flexibility to specify a folder name each time the pipeline is run. Using parameters increases the reusability of your pipelines, 
enabling you to create flexible data ingestion and transformation processes.

### Pipeline runs
Each time a pipeline is executed, a data pipeline run is initiated. Runs can be initiated on-demand in the Fabric user interface or scheduled to start at a specific frequency. 
Use the unique run ID to review run details to confirm they completed successfully and investigate the specific settings used for each execution.

## Copy Data Activity
* one of the most common uses of a data pipeline.
* Commonly used to ingest data from an external source into a lakehouse file or table.

Use the Copy Data activity when you need to copy data directly between a supported source and destination without applying any transformations, 
or when you want to import the raw data and apply transformations in later pipeline activities.

If you need to apply transformations to the data as it is ingested, or merge data from multiple sources, consider using a Data Flow activity to run a dataflow (Gen2). 
You can use the Power Query user interface to define a dataflow (Gen2) that includes multiple transformation steps, and include it in a pipeline.
