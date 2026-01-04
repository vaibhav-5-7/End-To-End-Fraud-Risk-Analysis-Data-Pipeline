# End-To-End-Fraud-Risk-Analysis-Data-Pipeline

## Overview

This project implements an **end-to-end fraud risk analysis data pipeline** orchestrated using **Apache Airflow** and built using **AWS serverless services**.
The pipeline automates fraud data processing and validation using **Amazon S3, AWS Lambda, Amazon Athena, and IAM roles**, with Airflow managing scheduling and task dependencies.

The project focuses on **workflow orchestration, secure service integration, and automated execution**, aligned with real-world data engineering practices.

---

## Services Used

* **Apache Airflow** – Workflow orchestration and scheduling
* **Amazon S3** – Storage for raw and processed data
* **AWS Lambda** – Serverless ETL processing
* **Amazon Athena** – SQL-based data validation
* **AWS IAM Roles** – Secure role-based access

---

## End-to-End Architecture

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A-ozH3UNxCVRiNSDlqCdfyg.png)

```
Apache Airflow
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

* Airflow orchestrates and schedules the pipeline
* Lambda processes fraud transaction data
* S3 stores raw and processed datasets
* Athena validates processed data using SQL
* IAM roles ensure secure access between services

---

## Scheduling Strategy

The pipeline is scheduled using **Apache Airflow** to run **daily at 3:05 PM IST**.

Since Airflow uses UTC internally:

* **3:05 PM IST = 09:35 AM UTC**
* Cron expression:

```
35 9 * * *
```

---

## Pipeline Flow

### 1. Workflow Orchestration – Apache Airflow

![Image](https://airflow.apache.org/docs/apache-airflow/stable/_images/latest_only_with_trigger.png)

* Defines the workflow using a DAG
* Controls task execution order
* Triggers AWS Lambda and Athena tasks
* Monitors execution status and logs

---

### 2. Data Processing – AWS Lambda
![Image](https://www.cloudtechsimplified.com/content/images/2022/10/Read-S3-Obj-Prefix.png)

* Triggered by Apache Airflow
* Reads raw credit card transaction data from Amazon S3
* Applies fraud-related transformations
* Writes processed data back to Amazon S3

---

### 3. Storage Layer – Amazon S3

![Image](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/defining-bucket-names-data-lakes/images/data-lake-naming-diag-1.png)
* Stores raw transaction data
* Stores processed fraud datasets
* Acts as the central storage layer
* Serves as the data source for Athena

---

### 4. Data Validation – Amazon Athena
* Executes SQL queries on processed S3 data
* Validates record counts and data consistency
* Ensures data quality after ETL processing

---

### 5. Security & Access Control – IAM Roles
![Image](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2023/12/08/Figure-1.png)

* IAM roles enforce **least-privilege access**
* Secure access provided to:

  * Amazon S3
  * AWS Lambda
  * Amazon Athena
* No credentials are hardcoded

---

## Example Orchestration Logic (Conceptual)

```python
start >> lambda_etl_task >> athena_validation_task >> end
```

> This snippet illustrates task dependencies only.
> The focus of this project is orchestration and secure integration.

---

## Monitoring & Observability

* Pipeline execution monitored via Airflow UI
* Task-level logs available for debugging
* Failed tasks can be retried independently

---

## What This Project Demonstrates

* End-to-end pipeline orchestration using Apache Airflow
* Integration of Amazon S3, AWS Lambda, and Amazon Athena
* Secure service interaction using IAM roles
* Automated scheduling and dependency management
* Production-style data engineering workflow

---

## Summary

This project demonstrates how to design and orchestrate a **secure, scheduled, end-to-end fraud risk analysis data pipeline** using **Apache Airflow, Amazon S3, AWS Lambda, Amazon Athena, and IAM roles**.

---

## Project Status

**Completed**

