# End-To-End-Fraud-Risk-Analysis-Data-Pipeline

![Image](https://d2908q01vomqb2.cloudfront.net/b6692ea5df920cad691c20319a6fffd7a4a766b8/2024/04/16/image001-2.png)

![Image](https://docs.aws.amazon.com/images/mwaa/latest/userguide/images/mwaa-architecture.png)

![Image](https://media.licdn.com/dms/image/v2/D4D12AQFpnFTSa52oLA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1706447756944?e=2147483647\&t=wX3dedYcVFzuyVaj0KBcbh6yeg0vDhQNxOxxpfhnR-I\&v=beta)

# Credit-Card-Fraud-Risk-Analysis

## Overview

This project demonstrates the design and orchestration of a **scheduled credit card fraud risk analysis data pipeline** using **Apache Airflow** and **AWS serverless services**.
The pipeline automates data ingestion, processing, validation, and monitoring using **S3, AWS Lambda, Athena, and IAM roles**, following real-world data engineering practices.

The primary focus of the project is **workflow orchestration and system integration**, rather than complex analytics or machine learning.

---

## Problem Statement

Fraud analytics pipelines must:

* Ingest transaction data reliably
* Execute processing jobs on a fixed schedule
* Validate processed data before consumption
* Enforce secure access between services
* Be monitored and recoverable in case of failures

This project addresses these requirements using Apache Airflow as the orchestration layer and AWS-managed services for processing and analytics.

---

## Architecture Overview

The pipeline follows a serverless and orchestrated architecture:

```
Apache Airflow (Orchestration)
        |
        v
AWS Lambda (ETL Processing)
        |
        v
Amazon S3 (Processed Data)
        |
        v
Amazon Athena (Validation Queries)
```

* **Apache Airflow** controls execution order and scheduling
* **AWS Lambda** performs ETL processing
* **Amazon S3** stores raw and processed datasets
* **Amazon Athena** is used for SQL-based validation
* **IAM Roles** manage secure access between services

---

## Technologies Used

* **Apache Airflow** – Workflow orchestration and scheduling
* **Amazon S3** – Data storage (raw and processed layers)
* **AWS Lambda** – Serverless ETL processing
* **Amazon Athena** – SQL-based data validation and analysis
* **AWS IAM** – Role-based access control
* **Python** – DAG definitions and Lambda logic

---

## Scheduling Strategy

The pipeline is scheduled to run **daily at 3:05 PM IST** using Apache Airflow.

Since Airflow operates in UTC:

* **3:05 PM IST = 09:35 AM UTC**
* Cron expression used:

```
35 9 * * *
```

This ensures automated, time-based execution without manual intervention.

---

## Workflow Description

### 1. Start

Marks the beginning of the pipeline execution.

### 2. Data Ingestion & ETL (AWS Lambda)

* Triggered by Apache Airflow
* Reads raw transaction data from Amazon S3
* Applies transformations and basic fraud-related logic
* Writes processed data back to Amazon S3

### 3. Data Validation (Amazon Athena)

* Executed after ETL completion
* Runs SQL queries on processed datasets
* Validates record counts and data consistency

### 4. End

Marks successful completion of the pipeline.

---

## IAM and Security

* IAM roles are used to provide **least-privilege access**
* Airflow-triggered jobs assume roles to access:

  * Amazon S3
  * AWS Lambda
  * Amazon Athena
* No hardcoded credentials are used

---

## Example Orchestration Logic (Illustrative Only)

```python
start >> lambda_etl_task >> athena_validation_task >> end
```

> This snippet represents task dependencies only.
> Detailed processing logic is intentionally abstracted to focus on orchestration.

---

## Monitoring and Observability

* Pipeline execution is monitored via Airflow UI
* Task-level logs are available for debugging
* Failures can be retried without re-running the entire workflow

---

## What This Project Demonstrates

* End-to-end data pipeline orchestration using Apache Airflow
* Integration of AWS serverless services in data workflows
* Secure service-to-service access using IAM roles
* Automated scheduling and dependency management
* Production-style pipeline design and monitoring

---

## Interview Summary

This project showcases the ability to design and orchestrate a **secure, scheduled fraud analytics pipeline** using Apache Airflow and AWS services, emphasizing automation, reliability, and best practices in data engineering.

---

## Project Status

Completed

This project is suitable for **Data Engineer portfolios, GitHub showcasing, and technical interviews**.

---

If you want next, I can:

* Convert this into **resume bullet points**
* Map this exactly to **L1/L2 Data Engineer interview questions**
* Align wording for **AWS Data Engineer roles**
* Create a **GitHub description + tags**

Just tell me what you want 👍
