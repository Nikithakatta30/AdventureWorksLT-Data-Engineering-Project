## Azure Data Engineering Project

# Introduction:

This project demonstrates the implementation of a data engineering pipeline using the Medallion Architecture on Azure. The source data is derived from the AdventureWorksLT2014 dataset, which has been transformed and optimized for analytics using a variety of Azure services.

# Architecture:

The project leverages the Medallion Architecture, comprising three layers:

Bronze Layer: Contains raw, unprocessed data.
Silver Layer: Holds data that has undergone the first level of transformation, such as data type conversions.
Gold Layer: Stores refined and optimized data, ready for analytics.

![project architecture](https://camo.githubusercontent.com/37573774dd97aa2f646ce074d8c8c731a1f52285fa6c6a0694058dfacbd55151/68747470733a2f2f6d656469612e6c6963646e2e636f6d2f646d732f696d6167652f4435363232415148417847655043376e415a512f6665656473686172652d736872696e6b5f313238302f302f313730353932333931313530323f653d3137323637303430303026763d6265746126743d7a4e61702d383772316135563157636943485a737778333456664a626c65627148487955324177754b7767)

# Tools and Technology:

1. Languages: Python, PySpark, SQL
Azure Services: Azure SQL Database, Azure SQL Server, Azure Data Lake Storage Gen2 (ADLS Gen2), Azure Data Factory (ADF), Azure Key Vault, Azure Databricks, Azure Synapse Analytics

# Source:

The project uses the AdventureWorksLT2014 dataset, which includes various tables related to sales, such as customer and order information. This data is stored in Azure SQL Database.

# Data Ingestion Steps:

Data Storage: The data is stored in Azure SQL Database, with passwords securely stored in Azure Key Vault.
Azure Data Factory (ADF) Setup: Created ADF, connected it to ADLS Gen2, Azure SQL Database, and Key Vault via linked services. It’s crucial to publish Key Vault first to use it in other linked services.
Config File: Developed a config file as metadata, specifying source schema, source table name, sink container, and sink folder for ingesting multiple tables from SQL DB to ADLS Gen2.
Parameterization: Added parameters for both datasets to handle arguments like src_schema, src_table, sink_container, and sink_folder.
Pipeline Creation: Created datasets for ADLS Gen2 and SQL DB. Built a pipeline utilizing Lookup, For Each, and Copy activities for data ingestion.

# Data Transformation Steps:

Data transformation was conducted in Azure Databricks:

Notebook Creation: Three notebooks were created—for mounting, silver layer transformation, and gold layer transformation.
Mounting: Established connections between the Bronze layer in ADLS Gen2, and the Silver and Gold layers.
Silver Layer: Applied first-level transformations.
Gold Layer: Executed further transformations, such as converting column names to uppercase.

# Loading Data Into Synapse Analytics:

The data in the Silver and Gold layers is stored in Delta file format, which is not directly usable for analytics. To make it accessible:

Synapse Analytics Setup: Set up a serverless SQL pool named DB_0815.
Linked Services: Connected Synapse Analytics to the ADLS Gen2 Gold layer.
Stored Procedure: Created a stored procedure to convert Delta files into a tabular format suitable for Power BI analytics.
This transformed data is now ready for advanced analytics and reporting.


This data can be used for further analytics purposes.

