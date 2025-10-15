# 🎬 Online Movie Streaming Platform Analytics (Azure Data Factory POC)

## 📘 Project Overview
This Proof of Concept (POC) project demonstrates how **Azure Data Factory (ADF)** can be leveraged to build an **end-to-end data integration pipeline** for a global online streaming platform — **StreamFlix**.  

The goal is to centralize and process raw data from multiple sources into a **report-ready format** for analytics and insights, simulating a real-world **Data Engineering workflow** using **Azure Data Lake Storage Gen2 (ADLS Gen2)**.

---

## 🎯 Business Scenario
A global streaming company, **StreamFlix**, wants to consolidate its raw data from multiple sources to perform **content performance and viewer behavior analysis**.

The company collects:
- 👤 User demographics and subscription details  
- 🎞️ Movie and genre information  
- 📈 Daily viewing logs (fact data)

### Project Objectives:
1. Ingest raw data (both user and content data) from multiple sources into the **Data Lake**.  
2. Copy **dimension tables** (like Users, Movies, Genres, Subscriptions) from the `raw-files` container directly to the `report-ready-files` container.  
3. Copy **yearly viewing log files** (like `View_2021.csv`, `View_2022.csv`, etc.) from **GitHub → raw-files** container.  
4. Move the yearly viewing log files into a **staging container**, perform a **consolidation (append)**, and create a final file — `Consolidated_View_Log.csv` — in the **report-ready-files** container.

---

## 🧩 Data Structure Overview

### 🗂️ 1. Dimension Tables  
*(Moved directly from `raw-files` → `report-ready-files`)*

| File Name | Description |
|------------|-------------|
| **Users.csv** | Information about users (user_id, name, age, country, subscription_id) |
| **Movies.csv** | Information about movies (movie_id, title, genre_id, release_year, rating) |
| **Genres.csv** | Genre mapping (genre_id, genre_name) |
| **Subscriptions.csv** | Subscription plans (subscription_id, plan_name, monthly_fee, quality) |

---

### 📈 2. Fact Tables  
*(Copied from `GitHub → raw-files → view-staging-files → report-ready-files`)*

| File | Description |
|------|-------------|
| **View_2021.csv** | View log data for 2021 |
| **View_2022.csv** | View log data for 2022 |
| **View_2023.csv** | View log data for 2023 |
| **View_2024.csv** | View log data for 2024 |

The final consolidated file created after transformation:
- ✅ **Consolidated_View_Log.csv**

---

## ⚙️ Pipeline Details

| Pipeline Name | Purpose |
|----------------|----------|
| **pl_copy_git_hub_view_logs** | Copies all view log files from the GitHub repository to the ADLS Gen2 `raw-files` container |
| **pl_move_non_view_files_2_report_ready_container** | Copies all non-view (dimension) files from `raw-files` to the `report-ready-files` container |
| **pl_copy_view_logs_to_staging_container** | Moves all yearly view log files from the `raw-files` container to the `view-staging-files` container |
| **pl_consolidate_all_view_logs** | Concatenates all yearly view log files from the `view-staging-files` container and copies the final consolidated file to the `report-ready-files` container |

---

## ☁️ Azure Resources Created

| Resource Type | Name | Description |
|----------------|------|-------------|
| **Resource Group** | `RG-Movie-Streaming-Platform-Analysis` | Logical grouping of all resources |
| **Azure Data Factory** | `ADF-Movie-Streaming-Analysis-Lab` | Main data integration service used for pipeline creation |
| **Azure Data Lake Storage Gen2** | `samoviestreamingproject` | Storage account used to store raw, staging, and report-ready files |
| **Containers Created** | `raw-files`, `view-staging-files`, `report-ready-files` | Logical containers inside the Data Lake for each data zone |

---

## 🔄 Step-by-Step Workflow Summary

1. **Upload Dimension Files:**  
   Uploaded the dimension table CSV files from the local computer to the `raw-files/CSV_Files` folder.  

2. **Copy Dimension Data:**  
   Used the `pl_move_non_view_files_2_report_ready_container` pipeline to move dimension tables to the `report-ready-files/CSV_Files` folder.  

3. **Copy View Log Files (from GitHub):**  
   Used the `pl_copy_git_hub_view_logs` pipeline to copy `View_2021.csv`, `View_2022.csv`, `View_2023.csv`, and `View_2024.csv` into the `raw-files` container.  

4. **Move View Logs to Staging:**  
   Used the `pl_copy_view_logs_to_staging_container` pipeline to copy the view log files from `raw-files` → `view-staging-files`.  

5. **Consolidate View Logs:**  
   Used the `pl_consolidate_all_view_logs` pipeline to merge all yearly view log files into one — `Consolidated_View_Log.csv` — and copy it into the `report-ready-files` container.  

---

## 📂 Project Structure

📁 StreamFlix-ADF-Project
│
├── 📁 Source_Data # Contains all source CSV files (dimension + yearly view logs)
├── 📁 Screenshots # Contains screenshots of pipelines, triggers, linked services, and dataflow steps
├── README.md # Project documentation
│
└── 📄 License / other metadata files


---

## 📸 Screenshots to Refer

All related screenshots are available inside the **`Screenshots`** folder, including:
- Linked Services setup (GitHub, ADLS Gen2)
- Datasets configuration
- Pipelines and activities (Copy Data, Move, Append)
- Trigger runs and monitoring view
- Final consolidated file in the `report-ready-files` container

---

## 🧠 Key Learning Outcomes

- Building and organizing **data pipelines** in Azure Data Factory  
- Working with **multiple containers** (Raw, Staging, Report-Ready) in ADLS Gen2  
- Integrating **external sources** (GitHub) with Azure services  
- Performing **data movement and transformation** at scale  
- Structuring a **real-world project workflow** for data engineering interviews  

---

## 🏁 Conclusion
This POC demonstrates a practical end-to-end **data ingestion, transformation, and consolidation workflow** using **Azure Data Factory** and **Azure Data Lake Storage Gen2**, applicable to any analytics-based domain — from streaming services to e-commerce and beyond.

---

📦 **Author:** *Chanush KR*  
📧 **LinkedIn:** *https://www.linkedin.com/in/chanush-kr/*  
🔗 **GitHub Repository:** *https://github.com/Chanushkr/Azure_Data_Factory_POC_Projects/tree/main/Project_2_StreamFlix%20Data%20Pipeline%20(ADF%20POC)*  
