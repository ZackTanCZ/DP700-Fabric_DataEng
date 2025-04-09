# Medallion Architecture

## Medallion Architecture
Within the ACID framework, the medallion architecture is a recommended data design pattern used to organize data in a lakehouse logically and improve data quality.
The architecture typically has three layers – bronze (raw), silver (validated), and gold (enriched), each representing higher data quality levels.

<img src = "https://github.com/user-attachments/assets/1f66d05c-e473-49f0-8856-11887aa7a5b5" width = "500"></img>

### Bronze Layer
* Landing zone for all data (unstructured, semi-structured or structured)
* Stored in original format with no changes made

### Silver Layer
* Validate and refine data
* e.g. combining & merging data, enforcing validation rules (removing nulls and duplicates)
* Data is stored in consistent format and easily accessible
  
### Gold Layer
* Refine data to align with business/analytical objective
* e.g. aggregating data to a particular granularity, such as daily or hourly, or enriching it with external information.
* Ready for downstream analytics

### Summary
* Bronze to ingest your data
* Silver to transform data
* Gold to present your data and insights

## Data Transformation vs. Data Orchestration

### Data Transformation
* Altering the structure or content of data to meet specific requirements
* Tools for data transformation in Fabric include Dataflows (Gen2) and notebooks
* Dataflows -> smaller semantic models and simple transformations.
* Notebooks -> larger semantic models and more complex transformations.
* Notebooks also allow you to save your transformed data as a managed Delta table in the lakehouse, ready for reporting. 

### Data Orchestration
* Coordination and management of multiple data-related processes, working together to achieve a desired outcome
* The primary tool for data orchestration in Fabric is pipelines.

## Special Consideration

### Tailoring Medallion Layers
* Tailoring medallion layers to different needs allows you to optimize data processing and access for specific use cases. 
* Ensure that each layer's structure and organization align with the requirements of different user groups, improving performance, ease of use, and data relevance for diverse stakeholders.
* Multiple Gold layers tailored for diverse audiences or domains highlights the flexibility of the medallion architecture.

