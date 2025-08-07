
## Project Overview

This project is trying to  implement  Medallion Architecture (Bronze → Silver → Gold) converting raw data into gold layer(curated analytical layers).It uses Azure-native tools to achieve the same.
---
## 🔧Tools & Technologies Used
- Microsoft Azure Data Factory
- Azure SQL Database
- Azure Delta Lake
- Azure Databricks (Unity Catalog)
- PySpark
- Delta Live Tables
- Slowly Changing Dimensions (SCD Type 1)
- Star Schema Modelling
---
## ⚙️ Project Architecture/ Pipeline Design

### 1. **Bronze Layer – Raw Ingestion**
Bronze Layer (Raw Ingest) This is where raw, unfiltered data lands — often directly from source systems, IoT streams, or APIs. Think of it as your immutable source of truth.
- Data is **pulled from Azure SQL Database** into **Azure Delta Lake (Bronze)** using Azure Data Factory.
- In real time we do a one time real load and then incremental loading of data.For this we have used the concept of change date capture.

### 2. **Silver Layer – Cleansed & Transformed** 
Silver Layer (Cleansed & Enriched) This layer applies cleansing, joins, type casting, and business rules. Now the data is trusted and queryable
- Data from the Bronze layer is processed in **Azure Databricks**.
- **Unity Catalog** is used to manage schemas and access control.
- Data is transformed using business logic and stored in the **Silver schema**.

### 3. **Gold Layer – Dimensional Modeling** 🥇
 This is your curated data, ready for dashboards, ML models, and downstream analytics. Often aggregated, filtered, or denormalized based on use cases. 
- Created **dimension tables** and **fact tables** from transformed Silver data.
- Applied **SCD Type 1** logic to track changes over time in both dimensions and fact tables.
- Designed a **Star Schema** with proper relationships for efficient analytics and reporting.
---

##  Key Concepts 
- ⏱️ Incremental Data Loads
- 🛠️ SCD Type 1 Implementation
- 🧱 Medallion Architecture (Bronze/Silver/Gold)
- 🔒 Unity Catalog for Governance
- 💫 Star Schema Dimensional Model

