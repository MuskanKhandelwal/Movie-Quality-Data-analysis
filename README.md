# Movie Data Quality Analysis

This project performs data quality analysis on movie ratings using AWS services. The steps involve setting up an S3 bucket, using AWS Glue for data extraction and loading, connecting to Redshift Serverless for data storage, performing ETL processes for data quality checks, and using EventBridge and SNS for monitoring and notifications.

## Overview

The main components of the project are:
1. Amazon S3
2. AWS Glue
3. Amazon Redshift Serverless
4. EventBridge
5. Amazon SNS

## Steps Involved

### 1. Creating an S3 Bucket

#### Bucket Creation
Created an S3 bucket named `movie-analysis-bucket` to store all the data files related to the project.

#### Folder Structure
Inside the S3 bucket, the following folders were created:
- `input/`: To store the input data files.
- `badrecords/`: To store records that do not meet quality checks.
- `history/`: To store historical data and processed files.
- `output/`: To store processed and clean data files.

### 2. Uploading Data to S3
Uploaded the initial movie ratings data file to the `input/` folder in the S3 bucket.

### 3. Creating an AWS Glue Crawler

#### Crawler Configuration
Created an AWS Glue crawler named `movie-ratings-crawler` and configured it to source data from the `input/` folder in the S3 bucket.

#### Running the Crawler
Ran the crawler to automatically infer the schema of the movie ratings data and create a table in the AWS Glue Data Catalog.

### 4. Connecting AWS Glue to Redshift Serverless

#### Setting Up Redshift Serverless
Created a Redshift Serverless cluster to store the processed movie ratings data.

#### Creating a Connection in AWS Glue
Created a connection in AWS Glue to connect to the Redshift Serverless cluster by providing the necessary details such as cluster endpoint, port, database name, username, and password.

### 5. Creating a Table in Redshift

#### Table Creation
Created a table in Redshift to store the movie ratings data:

### 6. Visual ETL for Data Quality Checks

#### ETL Workflow Creation
Used AWS Glue Studio to create a visual ETL workflow to extract data from S3, perform data transformations, and load data into Redshift.

#### Data Quality Checks
Implemented data quality checks to validate movie ratings:
- Ensured ratings are within the acceptable range (> 8.5).
- Checked for missing or invalid data.
- Applied transformation rules to manipulate data that did not meet quality checks.

#### Handling Bad Records
Bad records that failed the quality checks were saved in JSON format in the `badrecords/` folder in the S3 bucket.

#### Loading Updated Data into Redshift
The cleaned and validated data was loaded into the Redshift table, replacing or updating the existing records.

### 7. Monitoring with EventBridge and SNS

#### EventBridge Configuration
Set up EventBridge rules to monitor the ETL workflow and data quality checks:
- Configured rules to trigger notifications or actions based on specific events (e.g., job completion, failure).

#### SNS for Notifications
Created an SNS topic for sending notifications:
- Subscribed to the SNS topic with email and SMS endpoints.
- Configured EventBridge to send notifications to the SNS topic upon specific events, such as the completion of data quality checks or detection of bad records.

## Conclusion
This project demonstrates a comprehensive workflow for analyzing and ensuring the quality of movie ratings data using AWS services. By leveraging S3, AWS Glue, Redshift Serverless, EventBridge, and SNS, we can automate data processing, perform quality checks, and monitor the entire pipeline effectively.

