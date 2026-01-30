<div align="center">

# Customer Trust and Churn Risk Dashboard [![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white&labelColor=grey)](https://databricks.com)

</div>

<img width="1570" alt="Dashboard Preview" src="https://github.com/user-attachments/assets/438a161c-0e5c-4f87-a9e7-fd291ed64509" />

## Executive Summary

Customer churn is influenced by complex behavioral, transactional, and operational factors that are often difficult to capture with static rule-based systems. This project implements an end-to-end Databricks Lakehouse solution designed to identify churn risk and quantify customer trust signals.

**Customer Churn:** Customer churn is when a customer stops using a company's product or service.

**Example:** If a customer cancels their subscription and no longer uses the service, that customer is considered churned.

By leveraging a Medallion Architecture (Bronze, Silver, Gold), the solution transforms raw data into actionable insights, enabling retention teams to proactively target high-risk users. The pipeline integrates data engineering, machine learning, and business intelligence into a unified workflow.

---

## Architecture and Workflow

The solution is built on a production-grade architecture designed for scalability and governance:

* **Medallion Architecture:** Implements a structured data flow from raw ingestion (Bronze) to cleaned business logic (Silver) and aggregation for ML (Gold).
* **Delta Lake:** Utilizes Delta tables to ensure ACID compliance, schema enforcement, and time-travel capabilities.
* **Machine Learning:**
  * **Churn Model:** A baseline classification model to predict attrition probability.
  * **Trust Scoring:** A specialized scoring model to quantify customer sentiment and relationship health.
* **MLflow:** Used for full experiment tracking, model registry, and version control.
* **Orchestration:** Automated pipelines managed via Databricks Jobs.
* **Visualization:** Insights are delivered through SQL-driven KPI tiles and an interactive dashboard.

---

## Project Structure

The repository is organized to reflect the data lifecycle from ingestion to visualization:

```text
Customer_Trust_and_Churn_Risk/
├── data/
│   └── customer_churn_dataset.csv          # Source dataset (CSV)
│
├── 01_ingestion/
│   └── bronze_ingestion                    # Raw data ingestion logic
│
├── 02_silver_transformation/
│   └── silver_customer_churn               # Data cleaning and business rules application
│
├── 03_gold_features/
│   └── gold_customer_churn                 # Feature engineering for Machine Learning
│
├── 04_model_1_base_ml/                     # Baseline Churn Model
│   ├── 01_train_model_1
│   └── 02_evaluate_model_1
│
├── 05_model_2_trust_ml/                    # Trust Scoring Model
│   ├── 01_create_trust_dataset
│   └── 02_train_trust_model
│
├── 06_inference_scoring/
│   └── inference_and_trust_scoring         # Batch inference and writing predictions
│
├── 07_jobs_orchestration/
│   └── trust_scoring_job                   # Databricks Workflow definitions
│
├── 08_core_kpi_tiles_and_dashboard/
│   └── trust_scoring_and_churn_dashboard   # SQL logic for dashboard visualization
│
└── docs/
    └── project_documentation.md            # Detailed project documentation
```

---

## Key Insights and Performance

The pipeline processed **64,374** customer records, yielding the following segmentation:

| Metric | Value |
| :--- | :--- |
| **Total Customers** | 64,374 |
| **High-Risk Segment** | 22,881 (35.5%) |
| **Low-Risk Segment** | 41,493 (64.5%) |
| **Avg. Prediction Confidence** | 0.474 |

### Observed Risk Drivers

* **Demographics:** Higher churn probability among customers aged 60+.
* **Subscription Tier:** Standard and Basic plans show higher risk than Premium.
* **Operational Signals:** Strong correlation between churn, payment delays, and frequent support interactions.

---

## Business Value

* **Early Identification:** Detects at-risk customers early for timely intervention.
* **Strategic Segmentation:** Optimizes marketing spend by targeting high-risk users.
* **Operational Efficiency:** Delivers decision-ready datasets, reducing manual analysis.
* **Trust Quantification:** Goes beyond binary prediction to score relationship health.

---

## Tech Stack

**Data Platform:** Databricks Lakehouse Platform – Unified environment for data engineering, ML, and analytics | Apache Spark (PySpark & Spark SQL) – Distributed data processing and transformations | Delta Lake – ACID-compliant storage layer for Bronze, Silver, and Gold tables

**Data Architecture & Governance:** Medallion Architecture (Bronze → Silver → Gold) – Structured, scalable data pipeline design | Unity Catalog – Data governance, access control, and schema management

**Machine Learning:** Scikit-learn – Baseline churn and trust classification models | MLflow – Experiment tracking, model versioning, and reproducibility | Databricks ML Runtime – Optimized environment for ML workflows

**Orchestration & Automation:** Databricks Jobs – Automated pipeline execution and batch inference workflows

**Analytics & Visualization:** Spark SQL – KPI computation and analytical queries | Databricks Dashboards – Interactive visualization of churn risk and trust metrics

<div align="center">

<table>
<tr>
<td align="center" width="140">
<img src="https://www.vectorlogo.zone/logos/databricks/databricks-icon.svg" width="48" height="48" alt="Databricks"/>
<br><sub><b>Databricks</b></sub>
</td>
<td align="center" width="140">
<img src="https://www.vectorlogo.zone/logos/apache_spark/apache_spark-icon.svg" width="48" height="48" alt="Apache Spark"/>
<br><sub><b>Apache Spark</b></sub>
</td>
<td align="center" width="140">
<img src="https://www.vectorlogo.zone/logos/python/python-icon.svg" width="48" height="48" alt="Python"/>
<br><sub><b>Python</b></sub>
</td>
<td align="center" width="140">
<img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" width="48" height="48" alt="Scikit-learn"/>
<br><sub><b>Scikit-learn</b></sub>
</td>
<td align="center" width="140">
<img src="https://www.vectorlogo.zone/logos/numpy/numpy-icon.svg" width="48" height="48" alt="NumPy"/>
<br><sub><b>NumPy/Pandas</b></sub>
</td>
<td align="center" width="140">
<img src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/sql/sql.png" width="48" height="48" alt="SQL"/>
<br><sub><b>Spark SQL</b></sub>
</td>
</tr>
</table>

</div>

---

## Usage and Reproducibility

1. **Data Setup:** Upload the source dataset from `data/` to DBFS or Volume.
2. **Execution:** Run notebooks `01` through `06` sequentially to process data and train models.
3. **Automation:** Import the job definition from `07_jobs_orchestration` to run as a scheduled workflow.
4. **Dashboard:** Create insightful dashboard using queries from `08_core_kpi_tiles_and_dashboard` to visualize churn risk and trust metrics.

---

## Acknowledgments

This project was developed as part of the **Databricks 14-days challenge**, followed by **7 days of Build With Databricks: Hands-On Project Challenge**, with **700+ Participants**. I sincerely appreciate the initiative, guidance, and learning opportunity provided by **[Databricks](https://databricks.com/)**, **[Codebasics](https://codebasics.io/)**, and the **[Indian Data Club](https://www.linkedin.com/company/indian-data-club/)**, for support.
