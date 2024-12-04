# Project Summary: Sparkify Data Warehouse ETL Pipeline
This project provides an ETL pipeline designed to load and transform Sparkify's music streaming data into an AWS Redshift Data Warehouse. The primary goal is to enable Sparkify to answer critical business questions, such as identifying popular songs, understanding user behavior, and optimizing their service offerings. The pipeline runs on an hourly basis, orchestrated and managed using Apache Airflow, which ensures maintainable, testable, and collaborative workflows.

**Project Overview**
Purpose:

The database consolidates Sparkify's song and log data, enabling analytics and reporting.
It helps answer business questions, such as:
Which songs or artists are the most popular?
What times of the day experience the highest traffic?
Technology Stack:

Airflow: Schedules and orchestrates the ETL pipeline as a DAG (Directed Acyclic Graph).
AWS Redshift: Serves as the destination for processed data.
S3: Provides the raw data source in the form of song and log files.
Python: Used for the ETL logic, leveraging libraries for data manipulation.
Database Design
The pipeline uses a Star Schema, which simplifies data queries and improves aggregation performance. The schema consists of:

**Fact Table:**
songplays: Stores records of song plays (log data).
Dimension Tables:
users: User information.
songs: Song details.
artists: Artist details.
time: Timestamps of log events for detailed time-based analysis.


ETL Pipeline
Data Sources:

Song Data: Contains metadata about songs and artists.
Log Data: Tracks user activity, such as song plays.
Transformation:

Song data is loaded into the songs and artists dimension tables.
Log data is processed to populate the users, time, and songplays tables.
Pipeline Stages:

Data is staged in Redshift from S3 using the COPY command.
Fact and dimension tables are populated through SQL transformations.
Workflow
The pipeline is defined as a DAG in Airflow, with the following steps:

Start: Begin execution.
Create Tables: Create staging, fact, and dimension tables in Redshift.
Stage Data: Load raw data from S3 into Redshift staging tables.
Load Fact Table: Populate the songplays fact table.
Load Dimension Tables: Populate the users, songs, artists, and time tables.
Data Quality Checks: Validate data consistency and integrity.
End: Complete the process.


Setup and Dependencies
Prerequisites:

Install Apache Airflow: pip install apache-airflow.
```pip install airflow```
Start the Airflow webserver:
```airflow webserver -p 8080```

Configuration:

Add AWS credentials in the Airflow UI under Admin > Connections.
Configure the Redshift connection in the Airflow UI.
Execution:

Enable the sparkify_music_dwh_dag in the Airflow UI to trigger the pipeline.
Key Benefits
Automates data ingestion and transformation for consistent, reliable analytics.
Leverages Airflow’s powerful scheduling and monitoring capabilities.
Reduces query complexity and enhances performance with a Star Schema design.
Enables Sparkify to gain valuable insights into user behavior and song popularity.
