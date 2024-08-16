## Azure Data Engineering Project

# Introduction:

This project showcases the implementation of a data engineering pipeline using the Medallion Architecture on Azure. The source data is based on the AdventureWorksLT2014 dataset, which has been transformed and optimized for analytics using various Azure services.

# Architecture:

Medalian architecture is used in this project which consists of Gold, Silver and Bronze layer. In bronze layer there is a raw data, in silver layer first level of transformed data and in gold layer there is refined data.

![project architecture](https://camo.githubusercontent.com/37573774dd97aa2f646ce074d8c8c731a1f52285fa6c6a0694058dfacbd55151/68747470733a2f2f6d656469612e6c6963646e2e636f6d2f646d732f696d6167652f4435363232415148417847655043376e415a512f6665656473686172652d736872696e6b5f313238302f302f313730353932333931313530323f653d3137323637303430303026763d6265746126743d7a4e61702d383772316135563157636943485a737778333456664a626c65627148487955324177754b7767)

# Tools and Technology:

1. Languages: Python, Pyspark, SQL
2. Azure Services: Azure SQL Databases, Azure SQL Server, Azure Data Lake Storage Gen2,Azure Data Factory, Azure Key Vault, Azure Databricks, Azure Synapse Analytics

# Source:

In this project we used AdventureWorksLT data, which consists of multiple tables related to sales such as information related to customers and orders. This data is stored in SQL Databases.

# Steps Involved For Data Ingestion:

1. Data is stored in Azure SQL Database, stored the password in the key vault in secrets for the privacy.
2. Created a Azure Data Factory, using linked services connected to the ADLSGEN2, Azure SQL DB and Key vault and published. Most important, to use key vault in other linked services. First key vault should be created and published then only it can be used.
3. Created Dataset for a configfile. Ingesting multiple tables from SQL DB to ADLSGEN2, so using configfile which is the metadata which consists of source schema, source table name, sink container and sink folder.
4. Created parameters for both the datasets to the arguments src_schema, src_table, sink_container, sink_folder
5. Created Dataset for ADLSGEN2 and SQL DB also. Created a pipeline with Lookup activity, for each activity and copy activity.

# Steps Involved For Data Transformation:

For transforming the data we used databricks, created a compute and 3 notebooks for mount, silver layer and gold layer. In mount, created a connection between bronze layer in adlsgen2, silver layer and gold layer.
Used silver layer for first level transformations, gold layer for further transformations.

# Steps Involved In Loading Data To Synapse Analytics:

All the data in silver and gold layer is in delta file format. As this file format cannot be used for analytics purposes. To do this, used synapse analytics. created a serverless pool names DB_0815. Next created linked services to ADLSGEN2 gold layer.
Created a view using the sql script for converting the 

