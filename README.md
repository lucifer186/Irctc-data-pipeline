# IRCTC-data-pipeline

## Overview
This project is designed to process and transform IRCTC data using Google Cloud services. The pipeline captures real-time data changes, applies transformations using Python UDFs, and loads the final results into Google BigQuery for analytics.

## Data Flow
![image](https://github.com/user-attachments/assets/46370405-788b-422d-aab3-c9c575869da6)

1. Data Ingestion:
    1. Source data comes from IRCTC mock data as python script.
    2. Data is published to a Google Cloud Pub/Sub Topic (irctc_data).

3. Data Processing via DataFlow:
    1. Reads data from Pub/Sub.
    2. Applies Python User-Defined Functions (UDFs) stored in Google Cloud Storage.

4. Ensures fault tolerance during transformations.
     1. Loading Data into BigQuery:
     2. Processed data is inserted into BigQuery Table (irctc_dwh.irctc_stream_tb).

The data is structured for analytics, reporting, and further processing.

## Tools & Technologies Used

Google Cloud Pub/Sub – Real-time messaging for event-driven processing. \
Google Cloud DataFlow – Managed service for ETL (Extract, Transform, Load). \\
Google Cloud Storage – Stores Python transformation scripts. /
Google BigQuery – Data Warehouse for analytics.//
Python – Used for data transformation (UDFs).

## Prerequisites

Before running the pipeline, ensure the following:
1. Google Cloud Project: A GCP project with billing enabled.
2. Pub/Sub Setup: Create a Pub/Sub topic (irctc_data).
3. Cloud Storage: Upload the transformation script (transformation_udf.py) to a GCS bucket.
4. BigQuery Dataset & Table: Create the dataset irctc_dwh and table irctc_stream_tb with the following schema:
`CREATE TABLE `irctc_dwh.irctc_stream_tb` (
  row_key STRING,
  name STRING,
  age INT64,
  email STRING,
  join_date DATE,
  last_login TIMESTAMP,
  loyalty_points INT64,
  account_balance FLOAT64,
  is_active BOOL,
  inserted_at TIMESTAMP,
  updated_at TIMESTAMP,
  loyalty_status STRING,
  account_age_days INT64
);`

5. Enable Required APIs:
  Cloud Pub/Sub API
  DataFlow API
  BigQuery API
  Cloud Storage API

6. Install Required Packages (If running locally): `pip install google-cloud-pubsub google-cloud-storage google-cloud-bigquery apache-beam`

## Monitoring & Debugging
1. Check DataFlow Jobs: `gcloud dataflow jobs list --region=<your-region>`
2. View BigQuery Table Data: `SELECT COUNT(*) FROM `irctc_dwh.irctc_stream_tb``
3. View Pub/Sub Messages: `gcloud pubsub subscriptions pull <your-subscription> --limit=10`

This pipeline enables real-time data ingestion, transformation, and loading into BigQuery for analytics. It supports fault tolerance, scalability, and automated data processing using GCP services.


