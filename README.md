# 🚚 Lean Logistics: End-to-End Medallion Pipeline

### 📊 Project Overview
This project builds a scalable data pipeline for Supply Chain analysis using a **Lakehouse architecture**. Driven by **Lean principles**, we focus on transforming raw operational data into high-performance insights by combining the **Medallion Architecture** with **Unity Catalog** for governance and an **OBT (One Big Table)** delivery strategy.

---

### 🛡️ Governance & Metastore (Unity Catalog)
The project implements a multi-catalog governance strategy for strict environment isolation:

- **Catalogs:**
    - `cat_tm_services_bronze`: Raw data storage and initial ingestion.
    - `cat_tm_services_silver`: Refined data with enforced schemas.
    - `cat_tm_services_gold`: Business-level OBT (One Big Table).
- **Namespaces:** Each catalog contains a `logistics` schema to group all related assets.

---

### 🏗️ Data Architecture: The Medallion Approach

1.  **Bronze (Raw Layer):**
    - **Process:** Direct ingestion of source CSVs into **Delta Lake** format.
    - **Unity Catalog Path:** `cat_tm_services_bronze.logistics`
    - **Goal:** Maintain a full-fidelity history of source data for auditing and re-processing.

2.  **Silver (Refined Layer):**
    - **Process:** Data cleaning, deduplication, handling null values, and schema enforcement.
    - **Unity Catalog Path:** `cat_tm_services_silver.logistics`
    - **Goal:** Provide a "Single Source of Truth" for cleansed and standardized entities (Orders, Products, Payments).

3.  **Gold (Business Layer - OBT Strategy):**
    - **Model:** **OBT (One Big Table)**.
    - **Process:** Final denormalization joining multiple silver entities into a flat structure.
    - **Unity Catalog Path:** `cat_tm_services_gold.logistics`
    - **Goal:** Maximum performance for BI (Power BI/Databricks AI/BI) and simplified data discovery for business KPIs like **OTIF** and **Lead Time**.

---

### 🛠️ Tech Stack
- **Data Engine:** Databricks (PySpark)
- **Storage:** Delta Lake
- **Governance:** Unity Catalog
- **Language:** Python (PySpark) & SQL
- **Visualization:** Power BI / Databricks AI/BI

---

### 🚀 Roadmap
- [x] Repository setup & Folder structure
- [x] Architectural Design (Medallion + OBT + Unity Catalog)
- [ ] Data Ingestion (Bronze Layer)
- [ ] Silver Layer Refinement
- [ ] Gold OBT Construction
- [ ] Logistics Insights Dashboard
