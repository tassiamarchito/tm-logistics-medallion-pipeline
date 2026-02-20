# 🚚 Lean Logistics: End-to-End Medallion Pipeline

### 📊 Project Overview
This project aims to build a robust data pipeline for Supply Chain and Logistics analysis. Following a **Lean** approach, we transform raw operational data into strategic business insights using a **Medallion Architecture** (Bronze, Silver, Gold).

---

### 🏗️ Architecture & Tools
- **Cloud/Processing:** Databricks (Spark/PySpark)
- **Architecture:** Medallion (Bronze/Silver/Gold)
- **Storage:** Delta Lake
- **Visualization:** Power BI / Databricks AI/BI
- **Metastore:** Unity Catalog (where applicable)

---

### 📂 Pipeline Structure
1.  **Bronze (Raw):** Direct ingestion of source CSVs into Delta format.
2.  **Silver (Refined):** Data cleaning, schema enforcement, and deduplication.
3.  **Gold (Business):** Final dimensional modeling (Star Schema) optimized for Logistics KPIs like **OTIF** and **Lead Time**.

---

### 🚀 Status
- [x] Repository setup & Folder structure
- [ ] Data Ingestion (Bronze Layer)
- [ ] Data Transformation (Silver Layer)
- [ ] Business Modeling (Gold Layer)
- [ ] Dashboard Development
