AWS S3 + Athena Data Lake Project
Project Overview

This project demonstrates how to build a basic cloud data lake architecture using AWS services. The goal of the project is to ingest raw data in CSV format, convert it into an optimized columnar storage format (Parquet), store it in Amazon S3, and query the data using Amazon Athena.

The project simulates a typical data engineering workflow, where raw data is processed and stored in a data lake for efficient analytical querying.

A public dataset (IPL cricket dataset) was used to demonstrate the complete pipeline from raw data ingestion to query-based analysis.
Architecture Diagram :
<img width="1536" height="1024" alt="arch" src="https://github.com/user-attachments/assets/ae95d4f5-b540-458a-a4d5-28632175f061" />

Architecture Explanation
1. Data Source

A public dataset containing IPL match information was downloaded in CSV format. CSV files are commonly used for raw data ingestion but are not optimized for analytical workloads.

2. Data Processing Layer (Python)

Python was used to transform the raw CSV file into a Parquet format, which is a columnar storage format designed for analytical processing.

Libraries used:

Pandas for data handling

PyArrow for Parquet conversion

Benefits of Parquet:

Columnar storage

Faster query performance

Reduced storage size

Lower query costs in Athena

3. Data Lake Storage (Amazon S3)

Amazon S3 acts as the central storage layer for the data lake.

The dataset is organized into structured folders inside the S3 bucket to simulate a real-world data lake environment.

Example folder structure:

s3://aws-data-engineering-project/

raw-data/
    matches.csv

processed-data/
    matches.parquet

query-results/

This structure allows separation of:

Raw ingested data

Processed analytical data

Query outputs

4. Query Layer (Amazon Athena)

Amazon Athena is a serverless query engine that allows SQL queries to be executed directly on data stored in Amazon S3.

An external table was created in Athena that references the Parquet file stored in the S3 bucket.

Athena reads the schema and allows querying using standard SQL without requiring a database server.

Example Athena table creation:

CREATE EXTERNAL TABLE ipl_matches (
    id INT,
    city STRING,
    date STRING,
    player_of_match STRING,
    venue STRING,
    team1 STRING,
    team2 STRING,
    toss_winner STRING,
    toss_decision STRING,
    winner STRING
)
STORED AS PARQUET
LOCATION 's3://aws-data-engineering-project/processed-data/';
