# Spotify Data Pipeline – End‑to‑End AWS Data Engineering Project

## 📌 Project Overview

This project implements an **end‑to‑end cloud‑native data engineering pipeline on AWS**, using the **Spotify Web API** as a data source. It demonstrates how real‑world analytics pipelines are designed, scheduled, monitored, transformed, and consumed using **serverless and managed AWS services**.

The pipeline follows a modern **ELT/ETL hybrid approach**

---

## 🎯 Business Problem

Music streaming platforms generate massive volumes of user engagement data. Business teams need **daily, reliable, and analytics‑ready datasets** to:

* Track artist and track popularity trends
* Identify top‑performing genres and regions
* Enable BI dashboards for decision‑making

This project simulates how such data can be ingested from an external API, processed at scale, and delivered to analytics tools.

---

## 🏗️ AWS Architecture (Image‑Ready Description)

![Spotify ETL Architecture Cloud](https://github.com/user-attachments/assets/d16f8c0e-7977-43a4-bef0-f77c82302133)

![Spotify ETL Architecture Cloud-Glue](https://github.com/user-attachments/assets/446de2a8-b2fb-44ca-afd6-0a3d30397a25)


### High‑Level Flow

```
Spotify API
   |
   v
Amazon CloudWatch (Daily Schedule)
   |
   v
AWS Lambda – Extract Layer (Python)
   |
   v
Amazon S3 (Raw Zone)
   |
   v
S3 Event Trigger
   |
   v
AWS Glue (Apache Spark – Transform Layer)
   |
   v
Amazon S3 (Curated / Transformed Zone)
   |
   v
Snowpipe → Snowflake
   |
   v
Power BI Dashboards
```

### Key Design Principles

* **Serverless & Scalable**: No infrastructure management
* **Event‑Driven**: S3 object creation triggers downstream processing
* **Separation of Zones**: Raw vs Transformed data
* **Analytics‑Ready Output**: Optimized for BI consumption

---

## 🛠️ AWS Services Used

| Layer          | Service             | Purpose                               |
| -------------- | ------------------- | ------------------------------------- |
| Scheduling     | Amazon CloudWatch   | Triggers daily pipeline execution     |
| Extraction     | AWS Lambda (Python) | Calls Spotify API and stores raw data |
| Storage        | Amazon S3           | Raw & transformed data lake           |
| Transformation | AWS Glue (Spark)    | Cleansing, normalization, enrichment  |
| Loading        | Snowpipe            | Automated ingestion into Snowflake    |
| Analytics      | Power BI            | Reporting & visualization             |

---

## ⚙️ Pipeline Breakdown

### 1️⃣ Extract – AWS Lambda

* Triggered daily via CloudWatch
* Authenticates with Spotify API
* Pulls artists, albums, tracks & popularity metrics
* Stores raw JSON data in **S3 Raw Zone**

**Why Lambda?**

* Serverless, cost‑efficient
* Ideal for API‑based ingestion

---

### 2️⃣ Transform – AWS Glue (Apache Spark)

* Triggered automatically on S3 object creation
* Reads raw JSON from S3
* Performs:

  * Schema normalization
  * Deduplication
  * Data quality checks
  * Enrichment (timestamps, derived metrics)
* Writes curated datasets back to S3

**Why Glue?**

* Managed Spark
* Scales automatically
* Industry‑standard for big data transformations

---

### 3️⃣ Load – Snowflake via Snowpipe

* Snowpipe continuously ingests curated data
* Minimal latency between S3 and Snowflake
* Enables fast BI queries

---

## 👶 Beginner Version (Learning‑Focused)

**Ideal for newcomers to Data Engineering**

* Python scripts run locally
* Extract Spotify API data
* Transform using Pandas
* Store data as CSV files
* No cloud dependency

**Skills Learned**:

* API ingestion
* Pandas transformations
* Basic ETL concepts

---

## 🚀 Advanced Version (Production‑Ready)

**Cloud‑native & interview‑grade**

* AWS Lambda for extraction
* S3‑based data lake (raw & curated zones)
* AWS Glue Spark transformations
* Event‑driven orchestration
* Snowflake + Power BI analytics

**Skills Demonstrated**:

* Serverless design
* Distributed data processing
* Cloud architecture
* Real‑world ETL patterns

---

## 📊 Sample Analytics Use Cases

* Top 10 trending artists (daily / weekly)
* Genre popularity growth
* Artist consistency vs virality
* New release performance tracking

---

## 🔮 Future Enhancements

* Airflow orchestration
* Data quality checks with Great Expectations
* Partitioned S3 data (date‑based)
* CI/CD for Lambda & Glue jobs
* Cost monitoring & optimization

---

## 📬 Author

**Yogesh**
⭐ If this project helped you, please star the repository!
