# Bank-Customer-Churn-Feature-Engineering-Pipeline

A complete end-to-end Feature Engineering Pipeline built on the Databricks Lakehouse Platform using PySpark, Delta Lake, and AWS S3.
This project transforms raw customer data into clean, validated, feature-rich, ML-ready datasets to support churn prediction and customer retention strategies.

# Project Overview

This pipeline processes customer churn data following a structured Bronze → Silver → Gold → ML architecture.
It includes:

Automated batch ingestion

Data cleaning & standardization

Data quality checks

Feature engineering

Delta Lake optimization

KPI-based validation tests

Monitoring dashboards

The final output is a production-ready feature store for churn analytics and ML modeling.

# Objectives

The main goals of the pipeline are:

Convert raw data into trustworthy ML features

Detect data anomalies through DQ logging

Optimize Delta tables for fast analytics

Generate business-friendly churn indicators

Enable Data Scientists to build churn models easily

Provide continuous monitoring and batch scheduling

# Dataset

Source: Kaggle – Bank Customer Churn Dataset
Stored in: AWS S3 (raw zone)

Contains:

CustomerID

Geography

Gender

Credit Score

Balance

Tenure

Salary

Churn Label

Activity indicators

# Lakehouse Architecture


| Layer        | Table                         | Description                             |
| ------------ | ----------------------------- | --------------------------------------- |
| **Bronze**   | `raw.customer_data`           | Raw ingestion from S3                   |
| **Silver**   | `processed.customer_profiles` | Cleaned, validated customer records     |
| **Gold**     | `analytics.churn_features`    | Business & ML-oriented features         |
| **ML Ready** | `analytics.churn_ml_ready`    | Encoded numerical features for modeling |
| **Logs**     | `logs.data_quality`           | Data quality issue tracking             |

# Pipeline Flow

## 1.Bronze Layer – Raw Data Ingestion
### Notebook: 01_bronze_ingestion

Reads raw CSV from S3

Infers schema

Removes corrupt rows

Stores as Delta table

# 2.Silver Layer – Cleaning & Standardization

## Notebook: 02_silver_cleaning
### Transformations include:

Remove duplicate customers

Trim string fields

Validate age range

Replace negative salary/balance

Convert categorical Yes/No → 1/0

Ensure null-safe columns

*Output* → processed.customer_profiles

# 3.Data Quality Logging

## Notebook: 03_data_quality_logging
Checks:

Null values

Duplicate IDs

Invalid ages

Negative balances or salaries

Issues stored in:

logs.data_quality

# 4.Gold Layer – Feature Engineering

## Notebook: 04_gold_feature_engineering
Generated features:

Age Groups (Young, Adult, Middle Age, Senior)

Balance Category

Tenure Bucket

Activity Score

High-Risk Churn Flag

Recommendation Message for Retention Team

Output Partitioned by Country → analytics.churn_features

# 5.Delta Optimization

## Notebook: 05_delta_optimization
Includes:

OPTIMIZE for improving performance

ZORDER (customer_id) for faster filtering

VACUUM for cleanup

Table history & statistics

# 6.ML Preparation Layer

## Notebook: 06_ml_preparation

Purpose:
Convert categorical features into numeric encoded features required by ML models.

Example outputs:

gender_index

age_group_index

balance_category_index

tenure_bucket_index

Final table → analytics.churn_ml_ready

# 7.Monitoring Dashboard

## Notebook: 07_monitoring_dashboard
Dashboard views:

Row counts per layer

Latest DQ issues

High-risk customers by geography

Age distribution

Balance category distribution

# 8.KPI Validation Tests

## Notebook: 08_kpi_tests
Critical Stop-Pipeline Tests:

No null churn values

Age within valid range

No negative balances

If any KPI fails → pipeline stops automatically.

# Workflow Orchestration

A scheduled Databricks Job runs the entire pipeline daily at 1:00 AM.

## Task Order:

Bronze Ingestion

Silver Cleaning

Data Quality Logging

Feature Engineering

Delta Optimization

ML Preparation

Monitoring Dashboard

KPI Tests

# Business Impact

Enables early detection of churn-risk customers

Helps banks take proactive retention actions

Improves customer segmentation

Supports machine learning model development

Ensures high-quality data for decision-making

Reduces customer loss and increases revenue

# Tools & Technologies

Databricks Notebooks

PySpark

Delta Lake

AWS S3

Spark SQL

Databricks Jobs (Workflows)

GitHub Version Control

# Repository Structure

Bank-Customer-Churn-Feature-Engineering-Pipeline/
│
├── 01_bronze_ingestion.py
├── 02_silver_cleaning.py
├── 03_data_quality_logging.py
├── 04_gold_feature_engineering.py
├── 05_delta_optimization.py
├── 06_ml_preparation.py
├── 07_monitoring_dashboard.py
├── 08_kpi_tests.py
└── README.md

# Team Access

The pipeline is built on Databricks, and team members can access:

Workspace Folder

Delta Tables

Logs

Dashboards

GitHub Repository

Access Type: Read / Edit (based on permissions)

# Conclusion

This project demonstrates a complete real-world data engineering pipeline for churn analytics. It follows industry-standard architecture, quality checks, and orchestration, making the data reliable for downstream machine learning and business insights.
