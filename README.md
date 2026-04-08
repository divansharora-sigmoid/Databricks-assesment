
# 🚀 HR & Payroll Lakehouse Platform (Databricks)

## 📌 Overview

This project implements an **end-to-end HR & Payroll data platform** using the **Databricks Lakehouse architecture**. It processes batch and streaming data, applies transformations, enforces governance, and delivers analytics via dashboards.

---

## 🏗️ Architecture

* **Bronze Layer** → Raw data ingestion from DBFS
* **Silver Layer** → Data cleaning, joins, SCD Type 2
* **Gold Layer** → Aggregated views for analytics
* **Streaming** → Auto Loader for incremental updates
* **Governance** → Unity Catalog (masking + row filters)

---

## 📊 Dashboard

Includes:

* **Total Monthly Payroll by Department (Bar Chart)**
* **Headcount vs Budget (Table)**

---

## ⚙️ Tech Stack

* Databricks
* PySpark
* Delta Lake
* Unity Catalog
* Auto Loader
* SQL

---

## 📁 Project Structure

```bash
├── bronze/
│   ├── employees_ingestion.py
│   ├── salaries_ingestion.py
│   └── departments_ingestion.py
│
├── silver/
│   ├── employees_enrichment.py
│   └── scd_type2.py
│
├── gold/
│   ├── payroll_summary.sql
│   └── headcount_analysis.sql
│
├── streaming/
│   └── salary_stream.py
│
├── governance/
│   └── security.sql
│
└── README.md
```

---

## 🔄 Data Pipeline

### 1. Bronze Layer

* Ingest CSV data from DBFS (`/FileStore/hr_divansh/raw/`)
* Add metadata:

  * `_ingested_at`
  * `_source_file`
* Store as Delta tables

---

### 2. Silver Layer

* Clean and transform data
* Compute:

  * `tenure_years`
  * `total_monthly_compensation`
* Apply:

  * Window functions (latest salary)
  * **SCD Type 2** for job history
* Enable **Change Data Feed (CDF)**

---

### 3. Gold Layer

* Create analytics views:

  * `dept_payroll_summary`
  * `headcount_vs_budget`

---

### 4. Streaming Pipeline

* Auto Loader ingests new salary files
* Features:

  * Schema enforcement
  * Watermark
  * Checkpointing
  * Idempotency

---

### 5. Workflow (Jobs)

* Monthly scheduled job
* Tasks:

  * Bronze ingestion
  * Silver transformation
  * Gold aggregation
* Includes:

  * Retry mechanism
  * Failure notifications

---

### 6. Governance (Unity Catalog)

* Column masking:

  * `full_name`, `email`
* Row-level filtering:

  * Department-based access
* RBAC:

  * `hr_admin`
  * `hr_analytics`
  * `pii_hr_access`

---

## 🔥 Key Features

* Delta Lake (ACID transactions)
* Time Travel
* Change Data Feed
* Auto Loader (Streaming)
* Medallion Architecture
* Data Governance & Security

---

## 📈 Sample Queries

```sql
SELECT * FROM hr_catalog_divansh.gold.dept_payroll_summary;

SELECT * FROM hr_catalog_divansh.gold.headcount_vs_budget;
```

---

## 🚀 How to Run

1. Upload data to:

```bash
/FileStore/hr_divansh/raw/
```

2. Run notebooks in order:

* Bronze → Silver → Gold → Streaming

3. Create dashboard from Gold views

4. Set up Workflow in Databricks Jobs

---

## 📌 Results

* Real-time payroll updates
* Department-wise analytics
* Secure data access with masking
* Scalable Lakehouse architecture

---

## 📷 Dashboard

<img width="1297" height="635" alt="Screenshot 2026-04-08 at 12 01 33 PM" src="https://github.com/user-attachments/assets/80a120e1-322d-47bf-8963-9a063e843d45" />


---

## 👨‍💻 Author

Divansh Arora

---

