# Azure Data Factory POC: Healthcare CSV Files Copy Project

This project is a **Proof of Concept (POC)** for learning **Azure Data Factory (ADF)**. It demonstrates how to move healthcare-related CSV files from a **source folder** to a **destination folder** in **Azure Data Lake Storage (ADLS Gen2)** using ADF pipelines.

---

## 🏗️ Project Use Case

**Scenario:**  
The healthcare team provides multiple CSV files in a **raw-files** folder. Our goal is to:

1. Copy **all CSV files** from the `raw-files` container to the `processed-files` container.  
2. Later, move specific files (e.g., sales data) from the processed folder to a `reporting-ready-files` folder for analytics.  

**Purpose:**  
- Learn how to **ingest data** into Azure Data Lake using ADF.  
- Practice **data orchestration and movement** workflows.  
- Prepare data for downstream usage by **Power BI or other analytics tools**.

---

## 📂 Azure Resources Used

| Resource Type        | Name                                    | Description |
|---------------------|-----------------------------------------|-------------|
| Resource Group       | `RG-Healthcare-ADF`                     | Contains all project resources |
| Storage Account      | `sahealthcaredataproject`               | ADLS Gen2 storage account |
| Containers           | `raw-files`, `processed-files`, `reporting-ready-files` | Folders for source, processed, and reporting-ready data |
| ADF Resource         | `ADF-Healthcare-Lab`                     | Azure Data Factory instance |
| Linked Service       | `ADLS_Healthcare_LS`                     | Connects ADF to the ADLS Gen2 storage |
| Pipeline             | `pl_copy_healthcare_files`               | Pipeline to copy CSV files from source to destination |

---

## 📁 Folder Structure in ADLS Gen2

- `raw-files` → Source folder containing **original healthcare CSV files** (uploaded by stakeholders).  
- `processed-files` → Destination folder where **all raw files are copied**.  
- `reporting-ready-files` → Folder for **filtered files** (like sales-related CSVs) for reporting/analytics.

---

## 🔧 Workflow in ADF

1. **Create Linked Service**  
   - Connect ADF (`ADF-Healthcare-Lab`) to ADLS Gen2 (`sahealthcaredataproject`).  
   - Name: `ADLS_Healthcare_LS`  

2. **Create Source Dataset**  
   - Connect to the `raw-files` container inside ADLS Gen2.  
   - Dataset Name: `ds_healthcare_raw`  

3. **Create Destination Dataset**  
   - Connect to the `processed-files` container.  
   - Dataset Name: `ds_healthcare_processed`  

4. **Create Pipeline**  
   - Name: `pl_copy_healthcare_files`  
   - Add **Copy Activity** to move data from `raw-files` → `processed-files`  
   - Configure **Source** and **Sink** using the datasets created above.  
   - Use **Wildcard File Path** (`*`) to copy **all CSV files** from the folder.

5. **Debug & Run Pipeline**  
   - Click **Debug** to test the pipeline.  
   - Once successful, all files from `raw-files` will appear in `processed-files`.

---

## 📸 Screenshots

- Screenshots for every step (Resource Group, Storage Account, Linked Service, Datasets, Pipeline) are included in the repository folders:  

---

## ✅ Output

After running the pipeline:

- `processed-files` folder contains **all the healthcare CSV files** originally in `raw-files`.  
- Ready for further processing or filtering for reporting purposes.  

---

## 💡 Key Takeaways

- **ADF Pipelines** help move data efficiently across storage locations in Azure.  
- **Linked Services** act as connectors between ADF and storage.  
- **Datasets** define the specific files or folders to work with.  
- **Wildcard paths** allow bulk copying of all files in a folder.  
- **Containers** in ADLS Gen2 help organize source, processed, and reporting-ready data effectively.

---

**This POC project helps beginners practice the core capabilities of Azure Data Factory and Azure Data Lake for real-world data workflows. 🚀**
