My project began with acquiring a large CSV file containing financial transactions from a bank in the Netherlands.

The data was quite messy, featuring many missing values, incorrect entries, and issues with indexes.

To manage this data, I first stored it in a RAW folder within Azure Data Lake Storage (ADLS gen2).

I discovered Unity Catalog in Databricks, which provides enhanced governance, management, and security for data within Databricks. I connected this feature using the Azure Databricks Access Connector for Azure Storage.

To orchestrate the jobs in my project, I utilized Azure Data Factory (ADF). I implemented activities to copy the data from the RAW folder to a BRONZE folder, converting it into Parquet format.

Parquet.

In the BRONZE layer, I introduced a process to capture the output data for further processing.

I then validated the data using the Great Expectations library along with PySpark DataFrames. This validation step was essential to ensure data quality before proceeding.

I saved the cleaned data to the SILVER tier as well.

In the SILVER tier, I read the DataFrame from the external table and applied several transformations, including renaming columns and creating dimension tables. I then saved these dimension tables to the GOLD tier in Parquet format, as they would no longer require edits.

Finally, I created a fact table in the GOLD tier by joining relevant tables. I saved this fact table as an external table using Delta Lake. With the cleaned and structured data in the GOLD tier,

I connected it to Power BI, where I visualized the insights derived from the dataset.
