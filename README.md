# Azure Data Engineering Projects

A collection of hands-on Azure and Microsoft Fabric Data Engineering projects covering **data integration, cloud storage, ETL/ELT pipelines, Azure Data Factory, Azure Databricks, Apache Spark, PySpark, SQL, Microsoft Fabric Lakehouse, OneLake, and Power BI analytics**.

These projects demonstrate practical data engineering workflows from **raw data ingestion and transformation to curated datasets, analytics, dashboards, and documentation**.

---

## 📂 Repository Structure

```text
Azure-/
│
├── ADF/
│   ├── ADF.pdf
│   ├── ADf - Data Ingestion.pdf
│   ├── Append Variable ,Get Metadata ,Joins, Data Flow , Execute Pipeline ,...
│   ├── Filtration (IF Condition).pdf
│   ├── Incremental Data Loading.pdf
│   ├── Mapping ,Deletion ,Trigger & Set Variable(Finding Area) in ADF.pdf
│   └── README_ADF.md
│
├── Databricks/
│   ├── ADLS to Databricks.pdf
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
├── RetailProject/
│   ├── End-to-End_Retail_Data_Engineering_Analytics_Platform_Azure.pdf
│   ├── README_Retail_Data_Engineering_Azure.md
│   ├── customers.json
│   └── Retail_Sales_Inventory_Analytics_Platform in Fabric/
│       ├── README.md
│       └── Retail_Sales_Inventory_Analytics_Platform_Project_Report in Fabric.pdf
│
├── Retail_Sales_Inventory_Analytics_Platform/
│   ├── README.md
│   └── Retail_Sales_Inventory_Analytics_Platform_Project_Report in Fabric.pdf
│
└── README.md
```

---

# 1. Azure Data Factory (ADF)

📁 **Folder:** `ADF/`

The `ADF/` folder contains hands-on Azure Data Factory learning materials and practical pipeline exercises covering data ingestion, transformations, control flow, metadata operations, incremental loading, triggers, variables, and pipeline orchestration.

## 📄 ADF Contents

```text
ADF/
├── ADF.pdf
├── ADf - Data Ingestion.pdf
├── Append Variable ,Get Metadata ,Joins, Data Flow , Execute Pipeline ,...
├── Filtration (IF Condition).pdf
├── Incremental Data Loading.pdf
├── Mapping ,Deletion ,Trigger & Set Variable(Finding Area) in ADF.pdf
└── README_ADF.md
```

> The `Append Variable...` filename is displayed truncated by GitHub in the repository view; the README keeps the visible filename rather than inventing the hidden portion.

## 🔹 Topics Covered

- Azure Data Factory fundamentals
- Data ingestion pipelines
- Copy Data operations
- Variables and Append Variable
- Get Metadata activity
- Joins
- Mapping Data Flow
- Execute Pipeline activity
- Filter / IF Condition
- Incremental Data Loading
- Watermark-based loading concepts
- Mapping and deletion operations
- Triggers
- Set Variable
- Finding areas/features in ADF
- Pipeline orchestration

## 🛠 Technologies

- Azure Data Factory
- Azure Storage
- Azure Data Lake Storage
- REST/API data ingestion
- SQL
- Mapping Data Flow
- Pipeline activities
- Incremental loading
- Control flow

---

# 2. Retail Data Integration Platform using Azure Data Factory

📁 **Folder:** `Retail-Data-Integration-Platform-using-Azure-Data-Factory/`

An end-to-end retail data integration project demonstrating ingestion, transformation, incremental loading, orchestration, and curated reporting using Azure Data Factory.

## 🛠 Technologies

- Azure Data Factory
- Azure Data Lake Storage Gen2
- Azure SQL Database
- Azure Storage
- REST/JSON
- SQL
- Mapping Data Flow

## 📥 Data Sources

The project integrates data from multiple sources:

- SQL Orders data
- REST/JSON Products data
- Blob/CSV Stores data

## 🔄 Pipeline Architecture

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

## 🗂 Data Zones

### Raw Zone

```text
raw/
├── dbo.Orders.csv
├── Products.csv
└── Stores.csv
```

### Transformation

Mapping Data Flow is used for:

- Data cleansing
- Null filtering
- Standardization
- Product joins
- Store joins
- Sales aggregation

### Curated Output

The final dataset contains fields such as:

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

The curated data is stored as:

```text
processed/SalesSummary.csv
dbo.SalesSummary
```

## ✅ Validation and Engineering Features

- Row-count validation
- Conditional validation
- Failure handling
- Pipeline orchestration
- Incremental loading
- Watermark-based processing
- Upsert operations

---

# 3. AdventureWorks Sales Analytics — Azure Databricks

📁 **Folder:** `Databricks/`

This project demonstrates data processing and sales analytics using Azure Databricks and Apache Spark with AdventureWorks data.

## 🛠 Technologies

- Azure Databricks
- Apache Spark
- PySpark
- Spark SQL
- Azure Data Lake Storage
- SQL
- Data visualization

## 🔄 Workflow

```text
AdventureWorks
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

## 📄 Supporting Files

- `AdventureWorks Sales Dashboard.pdf`
- `AdventureWorks_Databricks_Project_Report.pdf`
- `AdventureWorks_Sales_Analytics_README.md`
- `nb-1.zip`

---

# 4. ADLS to Databricks Data Engineering Project

📁 **Folder:** `Databricks/`

This project demonstrates the process of connecting Azure Data Lake Storage with Databricks and processing data using Spark and PySpark.

## 🔄 Workflow

```text
ADLS
 │
 ▼
Databricks
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

## 🛠 Technologies

- Azure Data Lake Storage
- Azure Databricks
- Apache Spark
- PySpark
- Azure Cloud

📄 Documentation:

`ADLS to Databricks.pdf`

---

# 5. Retail Sales & Inventory Analytics Platform — Microsoft Fabric

📁 **Folder:** `RetailProject/` and the Fabric project folder

This is an end-to-end retail analytics platform built using **Microsoft Fabric**, following a **Bronze → Silver → Gold → Power BI** architecture.

## 🏗 Architecture

```text
Raw Retail Data
      │
      ▼
   Bronze
      │
      ▼
   Silver
      │
      ▼
    Gold
      │
      ▼
   Power BI
```

## 🛠 Technologies

- Microsoft Fabric
- OneLake
- Fabric Lakehouse
- Fabric Notebook
- PySpark
- Delta Lake
- SQL
- Power BI

## 🏠 Lakehouse

```text
Retail_LH
```

Notebook:

```text
Retail_NB
```

## 📁 OneLake File Structure

```text
Files
├── Bronze
│   ├── Orders
│   ├── Returns
│   └── Inventory
│
├── Silver
│   ├── Orders
│   ├── Returns
│   └── Inventory
│
└── Gold
    └── Product_KPIs
```

## 🗄 Lakehouse Tables

```text
dbo
├── silver_inventory
├── silver_orders
├── silver_returns
└── gold_product_kpis
```

---

## 🥉 Bronze Layer

The Bronze layer stores the source data in its raw form.

Main datasets:

- Orders
- Returns
- Inventory

Example source structures include:

### Orders

```text
Order_ID
cust_id
Product_Name
Qty
Order_Date
Order_Amount$
Delivery_Status
Payment_Mode
Ship_Address
Email
Promo_Code
Feedback_Score
```

### Inventory

```text
product_id
productName
stock
last_stocked
warehouse
cost_price
available
```

### Returns

The returns source is transformed from its raw property-based structure into meaningful business columns such as:

```text
Return_ID
Order_ID
Customer_ID
Product
Return_Reason
Return_Date
Refund_Status
Pickup_Address
Return_Amount
```

---

# 🥈 Silver Layer

The Silver layer contains cleaned and standardized data.

Main tables:

```text
silver_orders
silver_returns
silver_inventory
```

Typical processing includes:

- Column renaming
- Data type conversion
- Date standardization
- Null handling
- Data cleansing
- Schema standardization
- Product and customer field standardization

The Silver layer provides reliable datasets for downstream analytics.

---

# 🥇 Gold Layer

The Gold layer contains business-ready analytics.

Main table:

```text
gold_product_kpis
```

The Gold layer combines order, return, and inventory information to calculate retail KPIs.

## 📊 Main KPIs

- Total Orders
- Unique Customers
- Total Quantity Sold
- Total Revenue
- Average Order Value
- Total COGS
- Average Cost
- Net Profit
- Total Returns
- Returned Orders
- Total Return Amount
- Return Rate %
- Current Stock
- Profit Status

## 💰 Business Calculations

### COGS

```text
COGS = Quantity × Cost Price
```

### Net Profit

```text
Net Profit = Order Amount − COGS
```

### Return Rate

```text
Return Rate % =
(Returned Orders / Total Orders) × 100
```

### Profit Status

The project categorizes records using:

```text
Profit
Loss
Cost Data Missing
Quantity Missing
```

---

# 📊 Power BI Dashboard

The Gold dataset is connected to Power BI for interactive retail analytics.

## KPI Cards

- Total Revenue
- Total Orders
- Unique Customers
- Net Profit
- Return Rate %
- Total Quantity Sold
- Total COGS

## Filters / Slicers

- Product Name
- Profit Status

## Visualizations

- Revenue by Product
- Net Profit by Product
- Returns by Product
- Return Amount by Product
- Current Stock by Product
- Quantity Sold by Product
- Products by Profit Status

The dashboard provides a business-facing view of sales, profitability, returns, and inventory.

---

# 6. End-to-End Retail Data Engineering Platform — Azure

📁 **Folder:** `RetailProject/`

The `RetailProject/` folder also contains supporting documentation and source files for the broader retail data engineering implementation.

## 📄 Supporting Files

```text
RetailProject/
├── End-to-End_Retail_Data_Engineering_Analytics_Platform_Azure.pdf
├── README_Retail_Data_Engineering_Azure.md
├── customers.json
└── Retail_Sales_Inventory_Analytics_Platform in Fabric/
    ├── README.md
    └── Retail_Sales_Inventory_Analytics_Platform_Project_Report in Fabric.pdf
```

These files provide project documentation, retail source data, and detailed project reports.

---

# 🔧 Core Data Engineering Concepts Demonstrated

Across the repository, the projects demonstrate practical knowledge of:

### Data Integration

- Data ingestion
- REST/API integration
- SQL data sources
- CSV/JSON processing
- Azure Storage
- ADLS Gen2
- OneLake

### ETL / ELT

- Extract
- Transform
- Load
- Data cleansing
- Data standardization
- Data validation
- Aggregation

### Azure Data Factory

- Pipelines
- Activities
- Linked Services
- Datasets
- Parameters
- Variables
- Get Metadata
- Filter / IF Condition
- Execute Pipeline
- Triggers
- Mapping Data Flow
- Incremental loading
- Watermark concepts
- Pipeline orchestration

### Databricks / Spark

- Apache Spark
- PySpark
- Spark SQL
- DataFrames
- Data transformation
- ADLS integration
- Lakehouse processing

### Microsoft Fabric

- Fabric Lakehouse
- OneLake
- Fabric Notebook
- Bronze/Silver/Gold architecture
- Delta tables
- PySpark transformations
- Power BI integration

### Analytics

- KPI development
- Revenue analysis
- Profit analysis
- Return analysis
- Inventory analysis
- Power BI dashboards

---

# 🧱 Overall Architecture

The repository contains projects representing different stages of a modern cloud data engineering workflow.

```text
                    DATA SOURCES
                         │
          ┌──────────────┼──────────────┐
          │              │              │
         SQL            REST          CSV/JSON
          │              │              │
          └──────────────┼──────────────┘
                         ▼
              Azure Data Factory
                         │
                         ▼
                 Azure Storage / ADLS
                         │
              ┌──────────┴──────────┐
              │                     │
         Databricks          Fabric Lakehouse
              │                     │
          PySpark              Bronze Layer
              │                     │
              │                Silver Layer
              │                     │
              │                 Gold Layer
              │                     │
              └──────────┬──────────┘
                         ▼
                     Power BI
                         │
                         ▼
                   BI / Analytics
```

---

# 📚 Project Documentation

Each major project includes supporting documentation where available, including:

- Project README files
- Step-by-step guides
- Project reports
- Screenshots
- Notebook files
- Dashboard documentation
- Sample datasets

---

# 🎯 Skills Demonstrated

```text
Azure Data Factory
Azure Data Lake Storage Gen2
Azure Storage
Azure SQL
Microsoft Fabric
OneLake
Fabric Lakehouse
Azure Databricks
Apache Spark
PySpark
Spark SQL
SQL
ETL / ELT
Data Integration
Data Cleaning
Incremental Loading
Watermarking
Mapping Data Flow
Delta Lake
Bronze / Silver / Gold Architecture
Power BI
Data Analytics
```

---

# 👨‍💻 Author

**Evan Punnen**

B.Tech Computer Science & Engineering

Interested in:

- Data Engineering
- Cloud Data Platforms
- Azure
- Microsoft Fabric
- Databricks
- PySpark
- SQL
- Data Analytics
- Power BI

---

⭐ If you find these projects useful, feel free to explore the individual project folders and documentation.
