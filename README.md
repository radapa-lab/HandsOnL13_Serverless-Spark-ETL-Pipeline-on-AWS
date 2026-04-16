# Serverless Spark ETL Pipeline on AWS

## Overview

This lab demonstrates the implementation of a serverless ETL pipeline using AWS services. The pipeline processes customer review data automatically by triggering data transformation when a file is uploaded to Amazon S3. The processed data is then analyzed using Amazon Athena to generate insights.

## Objective

The objective of this lab is to build an event-driven data pipeline that performs data ingestion, transformation, and analysis using AWS Lambda, AWS Glue, and Amazon Athena.

## Step-by-Step Implementation

### Step 1: Create S3 Buckets

Two S3 buckets were created. One bucket was used as the landing bucket to store raw input data, and another bucket was used to store processed data and Athena query results.

### Step 2: Create AWS Glue Job

An AWS Glue job was created to process the dataset. The job reads raw data from the landing bucket, performs data cleaning and transformation using Spark, and writes the processed output to the processed S3 bucket.

### Step 3: Create Lambda Function

A Lambda function named start_glue_job_trigger was created using Python runtime. This function is responsible for starting the Glue job whenever it is triggered.

### Step 4: Configure Lambda Permissions

The Lambda execution role was updated by adding an inline IAM policy. This policy grants permission to start the Glue job using the glue:StartJobRun action.

### Step 5: Add S3 Trigger to Lambda

An S3 trigger was configured for the Lambda function. This ensures that whenever a new file is uploaded to the landing bucket, the Lambda function is automatically invoked.

### Step 6: Upload Dataset and Trigger Pipeline

The input dataset reviews.csv was uploaded to the landing S3 bucket after completing all configurations. This upload triggered the Lambda function, which in turn started the Glue job automatically. The Glue job processed the dataset and stored the output in the processed S3 bucket.

### Step 7: Monitor Execution

The execution was monitored using CloudWatch logs to verify Lambda execution and the AWS Glue console to check job run status.

### Step 8: Query Processed Data using Athena

Athena queries were executed on the processed dataset to generate analytical outputs. The results were stored automatically in the processed S3 bucket under the Athena Results folder.

## Output Description

After successful execution, the pipeline generated both cleaned data and analytical outputs. The cleaned dataset is stored in the processed-data folder. The Athena query results are stored in the Athena Results folder, where each query result is placed inside its own subfolder, and each subfolder contains the corresponding output file generated during execution.

## Output Files

The pipeline generated the following outputs:

Rating Distribution shows the number of reviews for each rating value.
Date-wise Review Count shows how many reviews were submitted on each date.
Top 5 Customers identifies the customers who have provided the highest number of reviews.
Average Rating represents the overall average rating calculated from the dataset.

## Repository Contents

Glue ETL Script.py contains the Spark-based ETL logic used in AWS Glue.
lambda function.py contains the Lambda function code used to trigger the Glue job.
reviews.csv is the input dataset used for processing.
HandsOnL13_Outputs contains all the output files downloaded from S3 for submission.

## Screenshots

Only one sample output screenshot is included here to demonstrate the result format. The remaining output files are provided in the HandsOnL13_Outputs folder and have been converted into .csv format for better readability and evaluation.

<img width="975" height="542" alt="image" src="https://github.com/user-attachments/assets/f17f750e-2d48-4d49-9bf9-1b717e03a84d" />
<img width="975" height="544" alt="image" src="https://github.com/user-attachments/assets/785150f5-0b13-4804-a718-519f29a73ad4" />
<img width="975" height="544" alt="image" src="https://github.com/user-attachments/assets/8fadc2de-cc11-42a0-8ccf-2d8a548cd5d3" />
<img width="975" height="542" alt="image" src="https://github.com/user-attachments/assets/1b5d0781-fc36-4d83-bb2c-faf98569829e" />
<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/f1753aca-1fe4-413c-ac52-c923f5fbfbf7" />
<img width="975" height="545" alt="image" src="https://github.com/user-attachments/assets/342aca69-5edf-4acc-8029-0e03435732a1" />
<img width="975" height="547" alt="image" src="https://github.com/user-attachments/assets/5b6197a6-3043-400f-b5c9-f25c282ebb27" />
<img width="975" height="290" alt="image" src="https://github.com/user-attachments/assets/5e1bb1d6-5241-4c80-a784-992edcd8cc72" />

## Conclusion

This lab demonstrates how AWS serverless services can be integrated to build a fully automated ETL pipeline. The system processes incoming data, performs transformations, and generates analytical insights in an efficient and scalable manner without requiring manual intervention.
