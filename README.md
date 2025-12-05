# 🚖 NYC Taxi Data Engineering Project 2024 | Azure Medallion Architecture

## 📌 Project Overview
This end-to-end data engineering project implements a **Medallion Architecture (Bronze → Silver → Gold)** on **Microsoft Azure** using **NYC Taxi & Limousine Commission (TLC) Trip Record Data** for the year 2024. The pipeline automates data ingestion, transformation, and visualization for actionable insights.

**Live Data Source:** [NYC TLC Trip Record Data 2024](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

---

## 🏗️ Architecture
<img width="1232" height="701" alt="nyc_data_architecture" src="https://github.com/user-attachments/assets/8484803d-806f-44de-9e4a-2253f2401041" />


### **Tech Stack**
| Component        | Technology Used                          |
|------------------|------------------------------------------|
| **Ingestion**    | Azure Data Factory (ADF)                 |
| **Storage**      | Azure Data Lake Gen2 (Bronze, Silver, Gold) |
| **Transformation**| Azure Databricks (PySpark)              |
| **Orchestration**| ADF Pipelines + Parameters               |
| **Data Format**  | Parquet (Bronze, Silver), Delta Lake (Gold) |
| **Visualization**| Power BI                                 |
| **Version Control**| GitHub                                 |

---

## 📂 Repository Structure
📁 nyc-taxi-data-engineering-2024/
│

├── 📁 Architecture/ # Architecture diagram

│ └── nyc_data_architecture.png

│

├── 📁 Data_ingestion/ # ADF pipeline screenshot

│ └── adf_pipeline.png

│

├── 📁 Databricks-Notebooks/ # Transformation notebooks

│ └── Gold_Notebook.py

│

├── 📁 Sample_Data/ # Static/lookup files

│ ├── trip_type.csv

│ └── trip_zone_lookup.csv

├── 📄 README.md # Project documentation

└── 📄 LICENSE # MIT License

---

## 🔧 Implementation Steps

### **1. Azure Setup & Resource Creation**
- Created a **Resource Group** in Azure.
- Provisioned:
  - **Azure Data Lake Gen2 Storage Account** with three containers:
    - `bronze` – raw data
    - `silver` – cleaned data
    - `gold` – curated data (Delta format)
  - **Azure Data Factory** – for orchestration
  - **Azure Databricks Workspace** – for transformation

### **2. Data Ingestion (ADF Pipeline)**
- Built an **ADF pipeline** to ingest 12 months of NYC taxi trip data (2024) via **REST API** from TLC website.
- Used:
  - **Copy Data Activity** to fetch monthly Parquet files.
  - **ForEach Loop** to iterate over months.
  - **If Condition** to handle URL formatting differences (months 01–09 vs 10–12).
- Manually uploaded two static lookup files:
  - `trip_type.csv`
  - `trip_zone_lookup.csv`
- All raw data landed in **Bronze container** in Parquet format.

### **3. Data Transformation (Databricks)**
#### **Silver Layer – Cleaning & Enrichment**
- Created a **Silver Notebook** in Databricks.
- Read raw Parquet files from Bronze.
- Performed:
  - Schema validation & correction
  - Null handling
  - Date/time formatting
  - Joining with lookup files
- Saved cleaned data to **Silver container** in Parquet format.

#### **Gold Layer – Business-ready Aggregations**
- Created a **Gold Notebook** in Databricks.
- Read Silver Parquet files.
- Created **Delta tables** in Databricks metastore:
  - `trip_type` (lookup)
  - `trip_zone_lookup` (lookup)
  - `trips_2024_data` (fact table)
- Applied:
  - Aggregations (e.g., trips per month, revenue trends)
  - Partitioning by `year_month`
  - Delta Lake optimizations (Z-ordering, VACUUM)
- Saved final dataset to **Gold container** in Delta format.

### **4. Visualization (Power BI)**
- Generated **Databricks Access Token** for secure connectivity.
- Connected **Power BI Desktop** directly to Databricks Gold tables.
- Built interactive dashboards for:
  - Monthly trip trends
  - Revenue analysis
  - Zone-wise trip distribution
  - Peak hour identification

---

## 📊 Results & Insights
- **Processed 12 months of trip data** (~10M+ records) efficiently.
- **Achieved data reliability** with Delta Lake (ACID transactions, time travel).
- **Enabled self-service BI** with Power BI dashboards.
- **Implemented a scalable, cloud-native pipeline** ready for incremental loads.

---

## 🧠 Key Learnings
- Hands-on experience with **Medallion Architecture** in Azure.
- **Parameterized ADF pipelines** for dynamic ingestion.
- **Delta Lake** for performance and reliability.
- **Databricks + Power BI integration** for real-time analytics.
- **End-to-end project lifecycle** from ingestion to visualization.

---
## 📣 Author

**Tushar Ahlawat**

Aspiring Data Engineer | Azure & Databricks Enthusiast


