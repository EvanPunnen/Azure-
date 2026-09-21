# Azure Data Engineering Projects

A collection of hands-on **Azure Data Engineering projects** covering data integration, cloud storage, ETL/ELT pipelines, Azure Data Factory, Azure Databricks, Apache Spark, PySpark, SQL, and analytics workflows.

This repository contains **three main projects** along with supporting documentation, notebooks, pipeline references, dashboards, and project reports.

---

## 📁 Repository Structure

```text
Azure-/
│
├── ADF/
│   └── Azure Data Factory learning materials and references
│
├── Databricks/
│   │
│   ├── ADLS to Databricks.pdf
│   │
│   ├── AdventureWorks Sales Dashboard.pdf
│   ├── AdventureWorks_Databricks_Project_Report.pdf
│   ├── AdventureWorks_Sales_Analytics_README.md
│   └── nb-1.zip
│
├── Retail-Data-Integration-Platform-using-Azure-Data-Factory/
│   ├── README.md
│   ├── Retail_Data_Integration_Platform_Full_Project_Report.pdf
│   ├── Retail_Data_Integration_Steps_with_Screenshots.pdf
│   └── SalesSummary.csv
│
└── README.md
```

---

# 🚀 Projects

## 1. Retail Data Integration Platform using Azure Data Factory

**Location:** `Retail-Data-Integration-Platform-using-Azure-Data-Factory/`

An end-to-end retail data integration project developed using **Azure Data Factory, Azure Data Lake Storage Gen2, Azure SQL Database, REST/JSON data, and Mapping Data Flows**.

The project demonstrates how data can be ingested from multiple sources, stored in raw and processed zones, transformed and aggregated, and finally loaded into Azure SQL Database.

### 🔹 Main Technologies

- Azure Data Factory
- Azure Data Lake Storage Gen2
- Azure SQL Database
- Azure Storage
- REST / JSON
- SQL
- Mapping Data Flow

### 🔹 Data Sources

The project integrates three source types:

```text
SQL Orders
     │
     ├── Orders data
     │
REST / JSON Products
     │
     ├── Product catalog
     │
Blob / CSV Stores
     │
     └── Store master data
```

### 🔹 Pipeline Architecture

```text
PL_00_Master_Orchestrator
            │
            ▼
PL_01_Ingest_RawZone
            │
            ▼
PL_02_Transform_ProcessedZone
            │
            ▼
PL_03_Load_CuratedZone
```

### 🔹 Raw Zone

Source data is ingested into Azure Storage:

```text
raw/
├── dbo.Orders.csv
├── Products.csv
└── Stores.csv
```

### 🔹 Transformation

The Mapping Data Flow performs:

- Data cleansing
- Null filtering
- Data standardization
- Product joining
- Store joining
- Sales aggregation

The transformation produces:

```text
SalesDate
StoreID
StoreName
ProductID
ProductName
Category
Ordercount
TotalQuantity
TotalSales
```

### 🔹 Curated Output

The processed Sales Summary is stored in:

```text
processed/SalesSummary.csv
```

and loaded into:

```text
dbo.SalesSummary
```

in Azure SQL Database.

### 🔹 Validation

The project also includes:

- Row-count validation
- Conditional validation
- Failure handling
- Pipeline orchestration
- Incremental loading / watermark concepts
- Upsert handling

### 📚 Documentation

Detailed project documentation is available in:

- `Retail_Data_Integration_Platform_Full_Project_Report.pdf`
- `Retail_Data_Integration_Steps_with_Screenshots.pdf`

---

# 2. AdventureWorks Sales Analytics — Azure Databricks

**Location:** `Databricks/`

An Azure Databricks project focused on processing and analyzing **AdventureWorks sales data** using Apache Spark and PySpark.

The project demonstrates a cloud-based data processing workflow using Databricks notebooks and Spark transformations.

### 🔹 Main Technologies

- Azure Databricks
- Apache Spark
- PySpark
- Spark SQL
- Azure Data Lake Storage
- SQL
- Data visualization

### 🔹 Main Data Engineering Concepts

- Data ingestion
- DataFrame operations
- Data cleaning
- Data transformation
- Data aggregation
- Spark SQL
- Analytical processing
- Data visualization
- Azure cloud integration

### 🔹 Project Workflow

```text
AdventureWorks Data
        │
        ▼
Azure Data Lake Storage
        │
        ▼
Azure Databricks
        │
        ▼
PySpark / Spark SQL
        │
        ▼
Data Cleaning & Transformation
        │
        ▼
Sales Analysis
        │
        ▼
Dashboard / Reporting
```

### 🔹 Outputs

The project includes:

- AdventureWorks Databricks project report
- AdventureWorks Sales Dashboard
- Databricks notebook ZIP
- Project README/documentation

### 📚 Documentation

Available files:

```text
AdventureWorks Sales Dashboard.pdf
AdventureWorks_Databricks_Project_Report.pdf
AdventureWorks_Sales_Analytics_README.md
nb-1.zip
```

---

# 3. ADLS to Databricks Data Engineering Project

**Location:** `Databricks/`

This project demonstrates the process of connecting **Azure Data Lake Storage (ADLS)** with **Azure Databricks** and working with cloud-based data using Spark.

The project focuses on the integration between Azure storage and Databricks for data engineering workflows.

### 🔹 Main Technologies

- Azure Data Lake Storage
- Azure Databricks
- Apache Spark
- PySpark
- Azure cloud services

### 🔹 Workflow

```text
Azure Data Lake Storage
          │
          ▼
Azure Databricks
          │
          ▼
Spark / PySpark
          │
          ▼
Data Processing
          │
          ▼
Analysis / Output
```

### 📚 Documentation

The repository contains:

```text
ADLS to Databricks.pdf
```

which documents the ADLS-to-Databricks integration workflow.

---

# 🔄 Overall Data Engineering Architecture

The three projects collectively demonstrate different stages of a modern Azure Data Engineering workflow.

```text
                     DATA SOURCES
                          │
             ┌────────────┼────────────┐
             │            │            │
            SQL          REST         CSV
             │            │            │
             └────────────┼────────────┘
                          │
                          ▼
                Azure Data Factory
                          │
                    Data Ingestion
                          │
                          ▼
              Azure Data Lake Storage
                          │
              ┌───────────┴───────────┐
              │                       │
             Raw                  Processed
              │                       │
              └───────────┬───────────┘
                          │
                          ▼
                  Azure Databricks
                          │
                    Spark / PySpark
                          │
                          ▼
                 Transform / Analyze
                          │
                          ▼
                  Curated Data
                          │
                          ▼
                  SQL / Dashboard
```

---

# 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Azure Data Factory | Data integration and pipeline orchestration |
| Azure Data Lake Storage | Cloud data storage |
| Azure SQL Database | Relational data storage |
| Azure Databricks | Data processing and analytics |
| Apache Spark | Distributed data processing |
| PySpark | Python-based Spark development |
| Spark SQL | Data querying and transformation |
| REST / JSON | External data ingestion |
| SQL | Database operations and analytics |
| GitHub | Source control and documentation |

---

# 📌 Skills Demonstrated

These projects demonstrate practical experience with:

- Azure Data Engineering
- ETL / ELT
- Data ingestion
- Data integration
- Azure Data Factory
- Azure Databricks
- Azure Data Lake Storage
- Azure SQL Database
- Apache Spark
- PySpark
- Spark SQL
- SQL
- Mapping Data Flows
- Data cleansing
- Data transformation
- Data aggregation
- Batch processing
- Incremental loading
- Watermark concepts
- Upsert processing
- Data validation
- Pipeline orchestration
- Cloud storage integration
- Data analytics
- Git and GitHub

---

# 📂 Project Documentation

Each project contains supporting documentation.

### Retail Data Integration Platform

```text
Retail-Data-Integration-Platform-using-Azure-Data-Factory/
│
├── README.md
├── Retail_Data_Integration_Platform_Full_Project_Report.pdf
├── Retail_Data_Integration_Steps_with_Screenshots.pdf
└── SalesSummary.csv
```

### AdventureWorks Databricks

```text
Databricks/
│
├── AdventureWorks Sales Dashboard.pdf
├── AdventureWorks_Databricks_Project_Report.pdf
├── AdventureWorks_Sales_Analytics_README.md
└── nb-1.zip
```

### ADLS to Databricks

```text
Databricks/
│
└── ADLS to Databricks.pdf
```

---

# ▶️ How to Explore the Repository

## Azure Data Factory Project

1. Open the `Retail-Data-Integration-Platform-using-Azure-Data-Factory` folder.
2. Read the project `README.md`.
3. Review the full project report.
4. Review the beginner step-by-step guide with screenshots.
5. Check the generated `SalesSummary.csv`.
6. Review the ADF pipeline architecture and implementation.

## AdventureWorks Databricks Project

1. Open the `Databricks` folder.
2. Read `AdventureWorks_Sales_Analytics_README.md`.
3. Review the Databricks project report.
4. Review the Sales Dashboard.
5. Import `nb-1.zip` into an Azure Databricks workspace if required.
6. Configure the required storage access.
7. Run the notebook and review the transformations and analysis.

## ADLS to Databricks Project

1. Open `ADLS to Databricks.pdf`.
2. Review the ADLS connection workflow.
3. Review how Databricks accesses the cloud data.
4. Recreate the configuration in an Azure Databricks workspace if required.

---

# 🔐 Security

Sensitive credentials should never be committed to GitHub.

Do not commit:

- Azure Storage account keys
- Passwords
- Access tokens
- Client secrets
- API keys
- Database credentials
- Connection strings containing credentials

For production implementations, use:

- Azure Key Vault
- Managed Identity
- Secure linked services
- Environment-specific configuration

---

# 📈 Future Enhancements

Possible future improvements across these projects include:

- CI/CD using GitHub Actions or Azure DevOps
- Azure Key Vault integration
- Metadata-driven pipelines
- Advanced incremental loading
- Change Data Capture (CDC)
- Delta Lake
- Unity Catalog
- Data quality frameworks
- Automated monitoring
- Automated alerting
- Power BI integration
- Advanced logging
- Production-grade error handling
- Automated testing

---

# 👨‍💻 Author

**Evan Punnen**

B.Tech – Computer Science and Engineering

GitHub: [EvanPunnen](https://github.com/EvanPunnen)

---

⭐ These projects demonstrate hands-on experience in Azure Data Engineering, cloud data integration, distributed data processing, and analytics.
