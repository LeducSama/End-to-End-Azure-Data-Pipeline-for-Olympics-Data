# End-to-End-Azure-Data-Pipeline-for-Olympics-Data

This document outlines an end-to-end data engineering project built on the Microsoft Azure cloud platform. The project demonstrates a practical data pipeline for ingesting, processing, and analyzing data from the Tokyo 2021 Olympics.

##  Project Overview

The main objective of this project was to construct a complete data pipeline using various Azure services. The process involved extracting raw data from an external source, transforming it into a clean and usable format, and loading it into an analytics service to uncover insights.

## 🏛️ Architecture

The project followed a standard data engineering workflow, moving data through several distinct stages:

1.  **Data Source**: The initial dataset, consisting of several CSV files, was sourced from a public GitHub repository.
2.  **Ingestion**: `Azure Data Factory` was used to create a pipeline that copied the raw data from the source.
3.  **Raw Data Storage**: The copied raw data was stored in 'Azure Data Lake Storage Gen2'.
4.  **Transformation**: `Azure Databricks` was used to run an Apache Spark code. This step involved cleaning the data, such as correcting data types and renaming columns.
5.  **Transformed Data Storage**: The cleaned data was loaded back into a separate folder within `Azure Data Lake Storage Gen2`.
6.  **Analytics & Warehousing**: `Azure Synapse Analytics` was used to query the transformed data with SQL, making it available for analysis.
7.  **Visualization**: The final, structured data is ready to be connected to a business intelligence tool like Power BI or Tableau for creating dashboards.

## 🛠️ Technologies Used

* **Cloud Platform**: Microsoft Azure 
* **Data Ingestion**: `Azure Data Factory` 
* **Data Storage**: `Azure Data Lake Storage Gen2` 
* **Data Transformation**: `Azure Databricks` & `Apache Spark` 
* **Data Analytics**: `Azure Synapse Analytics` 

## 📋 Project Execution Steps

The project was implemented in three main phases:

### 1. Data Ingestion

* An `Azure Data Factory` instance was created.
* A pipeline was built with **Copy data** activities to fetch five distinct CSV files (`athletes`, `coaches`, `medals`, `teams`, and `entries_gender`) from a GitHub repository via HTTP.
* Each file was loaded into a `raw-data` folder created within `Azure Data Lake Storage`.

### 2. Data Transformation

* An `Azure Databricks` workspace was set up and a Spark cluster was configured.
* The `Azure Data Lake Storage` was mounted to the Databricks workspace to allow direct access to the files.
* A Spark code was created to perform the transformations:
    * The raw CSV files were read into Spark DataFrames.
    * The schema was inspected, and transformations like correcting data types (e.g., converting columns from `string` to `integer`) were applied.
    * The transformed DataFrames were written back to a `transformed-data` folder in the data lake.

### 3. Data Analysis

* An `Azure Synapse Analytics` workspace was created.
* A new SQL database was created within Synapse.
* Tables were created in the database directly from the transformed data files stored in the data lake.
* SQL queries were executed in Synapse Studio to perform analysis, such as:
    * **Athlete Distribution**: A query was written to count the number of athletes from each country and order the results to find which nations sent the most participants. The United States had the highest count with 615 athletes.
    * **Medal Tally by Country**: The total sum of gold, silver, and bronze medals was calculated for each country. The results were ordered by the number of gold medals to create a ranked tally, with the United States at the top.
    * **Gender Distribution by Discipline**: A query was performed to calculate the average number of male and female participants for each Olympic discipline, allowing for an analysis of gender balance across different sports.
    * **Quick Visualization**: The built-in charting feature in Synapse Studio was used to create bar and line charts directly from the SQL query results for immediate visual analysis.

### Learnings
Through this project, I gained practical experience in building a foundational data pipeline on Azure, using services like Data Factory, Databricks, and Synapse to move data from ingestion to analysis. While this provided a solid overview of the workflow, it did not cover more advanced, real-world challenges such as pipeline automation, robust security implementation, or handling complex data quality issues, which remain key areas for my continued learning






