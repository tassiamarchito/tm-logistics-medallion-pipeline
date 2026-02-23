# 🚚 Lean Logistics: End-to-End Medallion Pipeline (Unity Catalog)

### 📊 Project Overview
This project implements a scalable and governed data pipeline for Supply Chain analysis using a **Lakehouse architecture**. Following **Lean principles**, we transform raw e-commerce data (Olist dataset) into high-performance business insights by combining the **Medallion Architecture** with professional **Unity Catalog** governance and automated Data Quality (QA) gates.

---

### 🛡️ Governance & Automated Data Quality (QA)
This pipeline implements **Data Observability** and **Governance-as-Code** through Unity Catalog and a custom QA framework, ensuring 100% reliability for business decisions:

- **Three-Level Namespace:** Managed as `catalog.schema.table` for production-grade isolation.
- **Automated QA Gates:** Every Gold notebook features a validation engine that monitors:
    - **Primary Key Integrity:** 0% duplication verified across all Dimensions and the Fact table.
    - **Spatial Accuracy:** Achieved a **99.72%** match rate for customers and **99.77%** for sellers, ensuring precise logistics mapping.
    - **Revenue Reconciliation:** **99.99% integrity** between item-level prices and total order payments.
- **Business Glossary:** 100% column-level documentation (Comments) and **Discovery Tags** (`quality`, `domain`, `type`) for rapid data search and cataloging.
- **Referential Integrity:** Enforcement of `NOT NULL` constraints and `PRIMARY KEY (RELY)` to optimize the Spark Catalyst engine.

---

### 🏗️ Data Architecture: The Medallion Approach

1. **Bronze (Raw Layer)**
    - **Logical Path:** `cat_tm_services_bronze.db_logistics.tb_[entity]`
    - **Process:** Automated ingestion into **Delta Lake** maintaining full historical fidelity.
    - **Resilience:** Handled unescaped line breaks and malformed characters in `tb_order_reviews` to prevent ingestion crashes.

2. **Silver (Refined Layer)**
    - **Logical Path:** `cat_tm_services_silver.db_logistics.tb_[entity]`
    - **Process:** Hardened cleaning using `try_cast` and `try_to_date` to handle malformed API strings.
    - **Standardization:** Strict naming conventions with business prefixes (`cd_`, `ts_`, `dt_`, `vl_`, `nm_`).
    - **Optimization:** Deduplicated geolocation master data (reducing redundancy by ~28%) to stabilize downstream spatial joins.

3. **Gold (Business Layer)**
    - **Logical Path:** `cat_tm_services_gold.db_logistics.dm_[dimension]` | `ft_[fact]`
    - **Dimensional Modeling:** Built a professional Star Schema optimized for analytical performance.
    - **Grain Management:** Resolved a critical **7,088 duplicate composite key** issue in `ft_sales` through pre-join aggregation, ensuring 1:1 transaction integrity.
    - **OBT (One Big Table):** Final denormalization into `obt_sales` optimized with **Z-ORDER** for sub-second BI dashboard latency.
    - **KPIs:** Automated calculation of **Lead Time** and **SLA Performance** (Estimated vs. Actual).

---

### 📊 Data Model (Star Schema)
The Gold layer is structured in a Star Schema to optimize analytical performance:
* **Fact Table:** `ft_sales` (Sales metrics and logistics KPIs).
* **Dimension Tables:** `dm_customers`, `dm_products`, `dm_sellers`.

> **Note on Data Reliability:** The pipeline implements automated schema enforcement and malformed record handling (using `try_cast` and logic filters) to ensure only 100% compliant data reaches the Silver and Gold layers.

---

### 📂 Notebooks Glossary

Detailed list of notebooks developed for this pipeline, following execution order:

#### ⚙️ Setup & Ingestion
* **`nb_criacao_catalogos_schemas_unity`**: Provisioning of the logical three-level namespace infrastructure.
* **`nb_extracao_dados_kaggle_api`**: Automation script for raw data extraction.

#### 🥉 Bronze (Raw)
* **`nb_db_logistics_bronze_ingestao`**: Load of source data into Delta format with full auditing capabilities.

#### 🥈 Silver (Refined)
* **`nb_db_logistics_silver_tipificacao_dedup`**: Cleansing engine and fault-tolerant data typing.

#### 🥇 Gold (Business)
* **`nb_db_logistics_gold_dm_customers` / `products` / `sellers`**: Dimensions enriched with spatial aggregation and automated QA Match Rate tests.
* **`nb_db_logistics_gold_ft_sales`**: Central fact table with aggregated metrics and verified composite PKs.
* **`nb_db_logistics_gold_obt_sales`**: Denormalized OBT for maximum BI consumption speed.

---

### 🔄 Orchestration & IaC (Databricks Workflows)
The entire pipeline is orchestrated via **Databricks Workflows**, ensuring a reliable and observable execution DAG:

* **Infrastructure as Code (IaC):** Full job configuration versioned in YAML for DevOps best practices.
* **Parallel Execution:** Dimension tables are processed concurrently to optimize compute resources.
* **Dependency Management:** Fact and OBT layers only trigger after upstream data quality validations are 100% successful.
  
<img width="1802" height="381" alt="image" src="https://github.com/user-attachments/assets/690e6b42-2165-4077-ad7f-1c66c2a0ef2c" />

---

### 🏃 How to Run
1. **Infrastructure:** Run `nb_criacao_catalogos_schemas_unity` to provision the Unity Catalog environment.
2. **One-Click Execution:** Trigger the **`jb_db_logistics_orq`** Workflow in Databricks.

---

### 🌿 Git Flow & Contribution Policy

To ensure pipeline stability and full traceability of changes within the Lakehouse, this project follows a strict branching and commit policy inspired by **GitHub Flow**:

#### **Branching Strategy**
* **`main`**: Protected and stable branch. It contains only production-ready, tested, and validated code.
* **`dev`**: Integration branch for new features before they are merged into production.
* **`feat/feature-name`**: Temporary branches for developing new notebooks, Gold layer tables, or specific business logic.
* **`fix/bug-name`**: Dedicated branches for fixing critical issues identified in the Silver or Gold layers.

#### **Commit Guidelines**
* **Atomic Commits**: Each commit must represent a single logical change (e.g., avoid mixing Silver layer cleaning logic with Gold layer KPI adjustments in the same commit).
* **Conventional Commits**: Commit messages must follow the industry standard:
    * `feat(scope)`: Introduction of a new feature (e.g., `feat(gold): create dm_products table`).
    * `fix(scope)`: Bug fixes or data typing corrections (e.g., `fix(silver): correct try_cast on review_score`).
    * `docs(scope)`: Documentation-only changes (README updates, comments).
    * `refactor(scope)`: Code improvements for performance or readability without changing business rules.

#### **Limits & Reviews**
* **Pull Requests (PR)**: All changes targeting the `main` branch must go through a PR process to ensure data integrity and architectural alignment.
* **Commit Limit**: We recommend a maximum of 10-15 commits per feature branch to keep Code Reviews manageable and avoid complex merge conflicts.

---

### 🛠️ Tech Stack
- **Data Engine:** Databricks (PySpark & Spark SQL)
- **Ingestion:** Kaggle API (Automated Python Script)
- **Governance:** Unity Catalog (Tags, Comments, Constraints, RELY)
- **Quality:** Automated Python-based Data Quality Framework
- **Storage:** Delta Lake
- **Language:** Python & SQL
- **Architecture:** Medallion + Star Schema + OBT

---

### 🚀 Roadmap
- [x] Repository setup & Folder structure
- [x] Architectural Design (Medallion + Star Schema + OBT)
- [x] Automated Data Collection (Kaggle API)
- [x] Automated QA Gates & Data Observability
- [x] Bronze Layer: Raw Data Processing & Issue Identification
- [x] Silver Layer: Fault-tolerant Cleaning & Standardization
- [x] Gold Layer: Dimensional Modeling & OBT Construction
- [x] Workflow Orchestration (IaC)
- [ ] Logistics Insights Dashboard (Databricks AI/BI)
