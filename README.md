# DataBricks--- Social-Media-Engagement-Project
This project demonstrates an end-to-end Databricks Lakehouse pipeline using a Social Media Engagement dataset. The pipeline is designed following the Medallion architecture (Bronze → Silver → Gold) and incorporates Delta Lake optimizations, orchestration, Unity Catalog governance, and ML model training.

Key goals:

Ingest raw social media data in a governed way

Clean and transform data using business rules

Build BI-ready aggregated tables

Train and track an ML model to predict engagement

Automate the workflow using Databricks Jobs

📂 Dataset

Source: Social Media Engagement Dataset (Kaggle)

Key Columns:

post_id

platform

impressions

likes

comments

shares

timestamp

🏗️ Architecture (Medallion Model)
+-----------------------------+
|        Bronze Layer         |
|-----------------------------|
| Raw CSV Ingestion           |
| Table: social_media_raw    |
+-----------------------------+
              |
              v
+-----------------------------+
|        Silver Layer         |
|-----------------------------|
| Cleaning & Business Rules   |
| Feature Engineering         |
| Table: social_media_clean  |
+-----------------------------+
              |
              v
+-----------------------------+
|         Gold Layer          |
|-----------------------------|
| Aggregations & BI Tables    |
| - platform_performance     |
| - content_type_performance |
| - daily_engagement         |
+-----------------------------+
              |
              v
+-----------------------------+
|        MLflow Model         |
|-----------------------------|
| Engagement Rate Prediction |
+-----------------------------+

🧱 Medallion Layers Explained
🥉 Bronze Layer

Raw data ingestion from Unity Catalog Volumes

No transformations applied

Metadata added:

ingestion_timestamp

_metadata.file_path

Stored as Delta tables for ACID compliance

🥈 Silver Layer

Data cleaning and validation

Business rules applied:

Filter invalid impressions

Standardize platform names

Feature engineering:

engagement_rate

post_date (DATE)

post_hour

Schema evolution handled using mergeSchema

Optimized using OPTIMIZE and ZORDER

🥇 Gold Layer

Aggregated, analytics-ready tables

Designed for BI tools and dashboards

Example outputs:

Platform-level performance

Content-type engagement

Daily engagement trends

⚙️ Delta Lake Features

ACID Transactions

Schema Enforcement & Evolution

Time Travel

File Compaction (OPTIMIZE)

Data Skipping (ZORDER BY platform, post_date)

🔄 Orchestration (Databricks Jobs)

The pipeline is orchestrated using Databricks Jobs with task dependencies.

Job Flow
Bronze Ingestion
      ↓
Silver Transformation
      ↓
Gold Aggregations
      ↓
ML Model Training

Tasks

Bronze ingestion from UC Volume

Silver transformation with business rules

Gold aggregations for analytics

ML model training with MLflow

Retries and logs are enabled for monitoring.

🔐 Governance (Unity Catalog)

Data managed under a single catalog: social_media_catalog

Schemas:

bronze

silver

gold

Public DBFS access disabled

Metadata captured using _metadata.file_path

Note: This is a demo project, so permissions are granted only to the project user.

📊 Analytics & Insights

Example insights generated:

Engagement comparison across platforms

Best-performing content types

Daily engagement trends over time

Peak posting hours

Gold tables can be queried via:

Databricks SQL

Power BI / other BI tools (via Databricks connector)

🤖 Machine Learning (MLflow)

Objective: Predict engagement rate of social media posts.

Features: platform, post_type, impressions, post_hour

Target: engagement_rate

Model: Regression model (baseline)

Experiments tracked using MLflow

Parameters, metrics, and models logged

▶️ How to Run the Project

Upload CSV file to Unity Catalog Volume

Run Bronze ingestion notebook

Run Silver transformation notebook

Run Gold aggregation notebook

Run ML training notebook

(Optional) Schedule pipeline using Databricks Jobs

🔮 Future Enhancements

Add data quality checks

Implement incremental ingestion

Add alerting and monitoring

Build interactive dashboards

Extend ML to classification or time-series forecasting
