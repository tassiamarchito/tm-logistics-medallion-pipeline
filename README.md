# 🚚 Lean Logistics: End-to-End Medallion Pipeline (Unity Catalog)

### 📊 Project Overview
This project implements a scalable and governed data pipeline for Supply Chain analysis using a **Lakehouse architecture**. Following **Lean principles**, we transform raw e-commerce data (Olist dataset) into high-performance business insights by combining the **Medallion Architecture** with professional **Unity Catalog** governance.

---

### 🛡️ Governance & Unity Catalog Implementation
The project utilizes **Unity Catalog** for full-cycle data governance, ensuring metadata and security are managed at scale:

- **Three-Level Namespace:** Data is organized as `catalog.schema.table` for production-grade isolation.
- **Data Discovery:** Implementation of **Discovery Tags** (`quality`, `domain`, `type`) for rapid table search.
- **Business Glossary:** 100% column-level documentation (Comments) ensuring the "Single Source of Truth" is understandable for business users.
- **Data Integrity:** Enforcement of `NOT NULL` constraints and `PRIMARY KEY (RELY)` to ensure referential integrity in the Gold layer.

---

### 🏗️ Data Architecture: The Medallion Approach

1. **Bronze (Raw Layer)**
    - **Logical Path:** `cat_tm_services_bronze.db_logistics.tb_[entity]`
    - **Process:** Automated ingestion into **Delta Lake** format.
    - **Quality Alert:** Identified critical issues like unescaped line breaks and column shifts in `tb_order_reviews`.
    - **Goal:** Full-fidelity history for auditing and re-processing.

2. **Silver (Refined Layer)**
    - **Logical Path:** `cat_tm_services_silver.db_logistics.tb_[entity]`
    - **Process:** Hardened data cleaning using `try_cast` and `try_to_date` to prevent pipeline failures from malformed API data.
    - **Standardization:** Strict naming conventions with prefixes (`cd_`, `ts_`, `dt_`, `vl_`, `nm_`).
    - **Structure:** 9 curated tables serving as the foundation for analytical modeling.

3. **Gold (Business Layer)**
    - **Logical Path (Star Schema):** `cat_tm_services_gold.db_logistics.dm_[dimension]` | `ft_[fact]`
    - **Logical Path (OBT):** `cat_tm_services_gold.db_logistics.obt_sales`
    - **Dimensional Modeling:** Built a professional Star Schema with Dimension (`dm_`) and Fact (`ft_`) tables.
    - **OBT (One Big Table) Strategy:** Final denormalization into `obt_sales` for maximum BI performance.
    - **KPIs:** Automated calculation of delivery performance (Estimated vs. Actual) and shipping metrics.

---

### 📂 Notebooks Glossary

Detailed list of notebooks developed for this pipeline, following execution order:

#### ⚙️ Setup & Ingestion
* **`nb_criacao_catalogos_schemas_unity`**: Provisioning of the logical three-level namespace infrastructure in Unity Catalog.
* **`nb_extracao_dados_kaggle_api`**: Automation script for raw data extraction via Kaggle API.

#### 🥉 Bronze (Raw)
* **`nb_db_logistics_bronze_ingestao`**: Initial load of source data into Delta format, maintaining full fidelity.

#### 🥈 Silver (Refined)
* **`nb_db_logistics_silver_tipificacao_dedup`**: Cleansing engine, deduplication, and fault-tolerant data typing.

#### 🥇 Gold (Business)
* **`nb_db_logistics_gold_dm_customers` / `products` / `sellers`**: Dimensions enriched with geolocation and MD5 hashing.
* **`nb_db_logistics_gold_ft_sales`**: Central fact table with logistics KPIs and performance metrics.
* **`nb_db_logistics_gold_obt_sales`**: Denormalized One Big Table for optimized BI consumption.

---

### 🛠️ Tech Stack
- **Data Engine:** Databricks (PySpark & Spark SQL)
- **Ingestion:** Kaggle API (Automated Python Script)
- **Governance:** Unity Catalog (Tags, Comments, Constraints)
- **Storage:** Delta Lake
- **Language:** Python & SQL
- **Architecture:** Medallion + Star Schema + OBT

---

### 🚀 Roadmap
- [x] Repository setup & Folder structure
- [x] Architectural Design (Medallion + Star Schema + OBT)
- [x] Automated Data Collection
- [x] Bronze Layer: Raw Data Processing & Issue Identification
- [x] Silver Layer: Fault-tolerant Cleaning & Standardization
- [x] Gold Layer: Dimensional Modeling & OBT Construction
- [ ] Logistics Insights Dashboard (Databricks AI/BI)
