# 🚚 Lean Logistics: End-to-End Medallion Pipeline

### 📊 Project Overview
This project builds a scalable data pipeline for Supply Chain analysis using a **Lakehouse architecture**. Driven by **Lean principles**, we focus on transforming raw operational data into high-performance insights by combining the **Medallion Architecture** with **Unity Catalog** for governance and an **OBT (One Big Table)** delivery strategy.

---

### 🛡️ Governance & Metastore (Implementation Note)
This project is designed with **Enterprise Governance** in mind. Although implemented in the **Databricks Community Edition** (using `hive_metastore`), the architecture mimics the naming conventions and logical isolation of **Unity Catalog**:

- **Logical Catalogs (Simulated):**
    - `cat_tm_services_bronze`: Raw data ingestion and history.
    - `cat_tm_services_silver`: Refined and standardized entities.
    - `cat_tm_services_gold`: Business-ready OBT.
- **Sustainability:** Developed using the **Free Edition** to ensure the project remains cost-free and accessible for portfolio display.

---

### 🏗️ Data Architecture: The Medallion Approach

1.  **Bronze (Raw Layer):**
    - **Process:** Automated data collection via **Kaggle API** directly into **Delta Lake** format.
    - **Logical Path:** `cat_tm_services_bronze.logistics` (Simulated)
    - **Goal:** Maintain a full-fidelity history of source data for auditing and re-processing without manual uploads.

2.  **Silver (Refined Layer):**
    - **Process:** Data cleaning, deduplication, handling null values, and schema enforcement.
    - **Logical Path:** `cat_tm_services_silver.logistics` (Simulated)
    - **Goal:** Provide a "Single Source of Truth" for cleansed and standardized entities (Orders, Products, Payments).

3.  **Gold (Business Layer - OBT Strategy):**
    - **Model:** **OBT (One Big Table)**.
    - **Process:** Final denormalization joining multiple silver entities into a flat structure.
    - **Logical Path:** `cat_tm_services_gold.logistics` (Simulated)
    - **Goal:** Maximum performance for BI (Power BI/Databricks AI/BI) and simplified data discovery for business KPIs like **OTIF** and **Lead Time**.

---

### 🛠️ Tech Stack
- **Data Engine:** Databricks Community (PySpark)
- **Ingestion:** Kaggle API (Automated Python Script)
- **Storage:** Delta Lake
- **Language:** Python (PySpark) & SQL
- **Visualization:** Power BI / Databricks AI/BI

---

### 🚀 Roadmap
- [x] Repository setup & Folder structure
- [x] Architectural Design (Medallion + OBT + Governance Simulation)
- [ ] Automated Data Collection (Kaggle API Notebook)
- [ ] Bronze Layer: Raw Data Processing
- [ ] Silver Layer: Data Cleaning & Standardization
- [ ] Gold Layer: OBT Construction
- [ ] Logistics Insights Dashboard
