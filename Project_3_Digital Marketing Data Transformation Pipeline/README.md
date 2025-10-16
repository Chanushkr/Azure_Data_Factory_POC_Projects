# 📊 Digital Marketing Data Transformation using Azure Data Factory (ADF)

### 🎯 Business Use Case

A digital marketing agency, **AdNova Analytics**, wants to streamline and clean its campaign performance data stored in their CSV file.  
The objective is to create an automated data pipeline that performs **data ingestion, cleaning, and transformation** before preparing it for reporting and analysis.

The raw marketing data contains:
- Missing (null) values in key columns like `Revenue_USD` and `Spend_USD`
- Extra irrelevant columns like `CTR (%)`, `CPC (USD)`, and `Analyst_Notes`.
- Add a derived column `ROI = (Revenue_USD - Spend_USD) / Spend_USD`.

---

### 🧩 Project Objective

The goal of this project is to:
1. **Ingest** digital marketing data files (in CSV format) from local storage into **Azure Data Lake Storage Gen2 (ADLS Gen2)**.
2. **Transform** the raw files using **Azure Data Factory Data Flows** by:
   - Handling null values  
   - Removing unnecessary columns  
   - Adding a calculated column called ROI
3. **Store** the cleaned and final dataset in a separate “report-ready” container for visualization tools like Power BI.

---

### 🏗️ Azure Resource Setup

| Resource Type | Name | Description |
|----------------|------|--------------|
| **Resource Group** | `RG-Digital-Marketing-ADF` | Organizes all related Azure services |
| **Storage Account (ADLS Gen2)** | `sadigitalmarketingdl` | Acts as a Data Lake for raw, transformed, and report-ready data |
| **Data Factory Resource** | `ADF-DigitalMarketing-Lab` | Orchestrates all data movement and transformation pipelines |

---

### 🗂️ Data Lake Container Structure

| Container Name | Purpose | Example Files |
|----------------|----------|----------------|
| **raw-files** | Stores unprocessed CSV files uploaded from local system | `fact_digital_marketing_performance.csv` |
| **transformed-files** | Holds intermediate, cleaned data after transformations | `part-00000-85883f28-021b-4590-a27e-40a2d350ebf6-c000.csv` |
| **report-ready-files** | Contains the final, analytics-ready dataset | `DigitalMarketingPerformance.csv` |

> This layered approach maintains clear separation between raw, transformed, and curated data zones.

---

### ⚙️ Pipelines Overview

| Pipeline Name | Description |
|----------------|-------------|
| `pl_transform_marketing_data` | Uses a **Data Flow** to handle null values, remove extra columns `(CTR (%)`, `CPC (USD)`, and `Analyst_Notes`), and standardize the dataset |
| `pl_prepare_report_ready_data` | Moves the cleaned and processed dataset from `transformed-files` to the `report-ready-files` container for analysis |

---

### 🔄 Data Flow Transformations

Within the **Data Flow** activity:
- ✅ **Source:** `raw-files` container  
- 🧹 **Transformations:**
  - Handle null values (replace or remove)
  - Drop extra columns not required for analytics
  - Add a new column (ROI)
- 💾 **Sink:** `transformed-files` container

---

### 🧠 Key Learning Outcomes

- Hands-on understanding of **ETL process using Azure Data Factory**
- Working with **Azure Data Lake Storage Gen2** for organizing data layers
- Practical experience in **data cleaning and transformation pipelines**
- Exposure to **schema drift** and handling data structure variations

---

### 📸 Supporting Files

- 📂 **Source_Data** → Contains all the input CSV files used in the project  
- 🖼️ **Screenshots** → Step-by-step visuals of pipeline configuration and execution results  

---

### 🏁 Summary

This project demonstrates how **Azure Data Factory** can be effectively used for **data ingestion, cleaning, and transformation** in a **digital marketing analytics** context.  
It follows a structured approach with **layered data storage** (raw → transformed → report-ready), ensuring scalability and clarity for enterprise data engineering practices.

---

📦 **Author:** *Chanush KR*  
📧 **LinkedIn:** *https://www.linkedin.com/in/chanush-kr/*  
👉 [View Full Project on GitHub](https://github.com/Chanushkr/Azure_Data_Factory_POC_Projects/tree/main/Project_3_Digital_Marketing_Data_Transformation)
