# Athena-Glue-DataProcess-from-S3 

This project contains a setup for processing data in Amazon S3 using AWS Glue, querying it with Amazon Athena, and utilizing Glue Crawler for automatic schema discovery. It includes two main S3 buckets - one for Athena Glue query and the other for input data. The goal is to efficiently process data stored in Amazon S3, allowing users to query and analyze the data seamlessly.

<p align="center">
  <img src="https://github.com/Jaylakhani37/Athena-Glue-DataProcess/assets/88767949/66698341-4236-4199-9704-98ddfd5c6569" alt="Setup Diagram">
</p>
<p align="center">
  <i>Image 1.0: Diagram of AWS Steup for this project</i>
</p>

## Prerequisites

1. AWS Account: Ensure you have an AWS account with the necessary permissions to create and manage Glue jobs, Athena queries, Glue Crawlers, and S3 buckets.

## Setup

### 1. Create S3 Buckets

- Create two S3 buckets in the AWS S3 Console:
  - Bucket 1: For Athena Glue Query (e.g., `athena-glue-query-bucket`)
  - Bucket 2: For Input Data (e.g., `input-data-bucket`)

<p align="center">
  <img src="https://github.com/Jaylakhani37/Athena-Glue-DataProcess/assets/88767949/011e5179-66fb-4a77-b25f-0ea59ada414a" alt="S3 Buckets">
</p>
<p align="center">
  <i>Image 1.1: S3 Buckets created for Athena Glue Query and Input Data</i>
</p>

### 2. Upload CSV File

- Upload your CSV file(s) to the `input-data-bucket`.

<p align="center">
  <img src="https://github.com/Jaylakhani37/Athena-Glue-DataProcess/assets/88767949/ff1a9bdd-1d64-4310-8b62-3cfbe672528f" alt="Upload CSV">
</p>
<p align="center">
  <i>Image 1.2: CSV files uploaded to the `input-data-bucket`</i>
</p>

### 3. Configure Athena Workgroup

- Open the Amazon Athena Console.
- Create a new Workgroup:
  - Choose "Settings" -> "Workgroups" -> "Add Workgroup".
  - Configure the workgroup settings, including query execution settings.
  - Change the Workgroup from default to 'YOUR_WG' from Query editor tabs.

<p align="center">
  <img src="https://github.com/Jaylakhani37/Athena-Glue-DataProcess/assets/88767949/dc7e865a-03ee-4de1-87fb-059a8fea3e5b" alt="Configure Athena Workgroup">
</p>
<p align="center">
  <i>Image 1.3: Configuring Athena Workgroup settings</i>
</p>

### 4. Configure AWS Glue Crawler

- Open the AWS Glue Console.
- Create a new Crawler:
  - Choose "Crawlers" -> "Add Crawler".
  - Configure the data store as your S3 input bucket.
  - Choose a target for the crawler output, e.g., a new database and table in the AWS Glue Data Catalog or default.
  - Choose Crawler schedule Frequency, e.g., On-demand.
  - Run the crawler to automatically discover and catalog the schema of your data.
  - In Athena Query editor tabs, refresh it and choose the database and datasource (default - AWSDataDatalog).

<p align="center">
  <img src="https://github.com/Jaylakhani37/Athena-Glue-DataProcess/assets/88767949/fdcdbb03-9c58-4518-93a0-9ef1273dc338" alt="Configure Glue Crawler">
</p>
<p align="center">
  <i>Image 1.4: Configuring AWS Glue Crawler for schema discovery</i>
</p>

### 5. Run Queries in Athena

- Select the created Workgroup in the query editor tab.
- Use the Athena Console to run queries on the processed data within the specified Workgroup.

<p align="center">
  <img src="https://github.com/Jaylakhani37/Athena-Glue-DataProcess/assets/88767949/de7bb5db-7ba4-4822-90e7-1a43028d65fa" alt="Run Queries in Athena">
</p>
<p align="center">
  <i>Image 1.5: Running queries in Athena</i>
</p>

## Example Query

```sql
SELECT *
FROM your_database.your_output_table
WHERE your_condition;

-- Example
-- SELECT * FROM "test-db-delete-db"."inputetljobs" LIMIT 10
