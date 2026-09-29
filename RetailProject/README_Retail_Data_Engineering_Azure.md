# End-to-End Retail Data Engineering & Analytics Platform on Azure

An end-to-end retail data engineering project using **Azure SQL, Azure Data Factory, ADLS Gen2, Azure Databricks, Unity Catalog, Databricks SQL Warehouse, and Power BI**.

## 📌 Project Overview

This project demonstrates how retail data can be collected from different sources, ingested into Azure, transformed using Databricks, organized into analytics-ready datasets, and visualized in Power BI.

```text
Azure SQL + Customer JSON
          ↓
Azure Data Factory
          ↓
ADLS Gen2 – Bronze
          ↓
Azure Databricks
          ↓
Silver → Gold
          ↓
Unity Catalog
          ↓
Databricks SQL Warehouse
          ↓
Power BI
          ↓
Retail Sales Dashboard
```

## 🎯 Objectives

- Build an end-to-end Azure data engineering pipeline.
- Ingest structured retail data from Azure SQL.
- Ingest customer data in JSON format.
- Store raw data in ADLS Gen2.
- Clean and transform data using Databricks/PySpark.
- Create Silver and Gold data layers.
- Organize analytics tables with Unity Catalog.
- Serve data through Databricks SQL Warehouse.
- Build a Retail Sales Dashboard in Power BI.

## 🛠️ Technologies

| Technology | Purpose |
|---|---|
| Azure SQL Database | Source for products, stores and transactions |
| Azure Data Factory | Data ingestion and orchestration |
| ADLS Gen2 | Cloud data lake |
| Azure Databricks | Data transformation |
| PySpark / SQL | Data processing |
| Unity Catalog | Data organization and governance |
| Databricks SQL Warehouse | BI/SQL serving layer |
| Power BI | Dashboard and visualization |

## 📂 Data Sources

### Products
- `product_id`
- `product_name`
- `category`
- `price`

**Expected records: 10**

### Stores
- `store_id`
- `store_name`
- `location`

**Expected records: 5**

### Transactions
- `transaction_id`
- `customer_id`
- `product_id`
- `store_id`
- `quantity`
- `transaction_date`

**Expected records: 30**

### Customers

Customer JSON contains fields such as:

- `customer_id`
- `first_name`
- `last_name`
- `email`
- `phone`
- `city`
- `registration_date`

**Expected records: 50**

## 🏗️ ADLS Structure

```text
bronze/
├── customers/
├── products/
├── stores/
└── transactions/

silver/
├── customers/
├── products/
├── stores/
└── transactions/

gold/
├── dim_customer/
├── dim_date/
├── dim_product/
├── dim_store/
└── fact_sales/
```

## 🔄 Azure Data Factory

ADF is responsible for moving source data into the Bronze layer.

Main activities:

```text
Copy_Products
Copy_Stores
Copy_Transactions
```

The pipeline also handles customer JSON ingestion.

## 🥉 Bronze Layer

Bronze stores the ingested source data with minimal transformation.

Example:

```text
bronze/
├── customers/customers.json
├── products/products.parquet
├── stores/stores.parquet
└── transactions/transactions.parquet
```

## 🥈 Silver Layer

Databricks cleans and validates Bronze data.

Transformations include:

- Removing duplicates
- Trimming text fields
- Handling required/null fields
- Correcting data types
- Converting dates
- Validating relationships
- Writing cleaned datasets

Expected counts:

```text
Products      : 10
Stores        : 5
Transactions  : 30
Customers     : 50
```

## 🥇 Gold Layer

The analytics model uses a star-schema approach:

```text
dim_customer
       ↓
dim_product → fact_sales ← dim_store
                    ↑
                 dim_date
```

### Main tables

- `dim_customer`
- `dim_date`
- `dim_product`
- `dim_store`
- `fact_sales`

Additional reporting tables can include:

- `gold_customer_sales`
- `gold_product_sales`
- `gold_store_sales`

## 🗂️ Unity Catalog

The analytics tables are organized under the Databricks catalog/schema.

Example:

```text
evandb_7405605640633254
└── default
    ├── dim_customer
    ├── dim_date
    ├── dim_product
    ├── dim_store
    ├── fact_sales
    ├── gold_customer_sales
    ├── gold_product_sales
    └── gold_store_sales
```

## ⚡ SQL Warehouse

A Databricks SQL Warehouse provides the SQL endpoint used by Power BI.

Power BI requires:

- Server Hostname
- HTTP Path
- Appropriate authentication

## 📊 Power BI Dashboard

The final dashboard is named **Retail Sales Dashboard**.

### KPIs

- Total Sales / Revenue
- Total Transactions

### Visuals

- Store-wise sales bar chart
- Sales trend over time
- Category-wise sales donut chart
- Formatted dashboard title and layout

Reference results:

```text
Total Sales       : 134.57K
Transactions      : 30
```

### Important KPI Note

For transaction count, use:

```text
Count(transaction_id)
```

Do **not** use:

```text
Sum(transaction_id)
```

because summing IDs would produce `465` for IDs 1–30 instead of the correct transaction count of `30`.

## 🔍 Data Quality Checks

The project validates:

- Duplicate records
- Null values
- Data types
- Product references
- Store references
- Customer references
- Transaction dates
- Expected record counts

## 🚀 Implementation Steps

1. Create Azure resources.
2. Create ADLS Gen2 storage.
3. Create Bronze/Silver/Gold containers.
4. Create Azure SQL tables.
5. Load and validate source data.
6. Create ADF linked services and datasets.
7. Build SQL-to-Bronze Copy activities.
8. Ingest customer JSON.
9. Configure Databricks access to ADLS.
10. Read Bronze data in Databricks.
11. Clean and validate data.
12. Write Silver data.
13. Build Gold/star-schema datasets.
14. Register analytics tables in Unity Catalog.
15. Create/start Databricks SQL Warehouse.
16. Connect Power BI to Databricks.
17. Load the required tables.
18. Build the Retail Sales Dashboard.
19. Validate KPIs and visuals.

## 📁 Suggested Repository Structure

```text
End-to-End-Retail-Data-Engineering-Analytics-Platform/
│
├── README.md
├── ADF/
│   ├── Pipelines/
│   ├── Datasets/
│   └── Linked_Services/
│
├── Databricks/
│   ├── Notebooks/
│   ├── Bronze/
│   ├── Silver/
│   └── Gold/
│
├── SQL/
│   ├── Products.sql
│   ├── Stores.sql
│   └── Transactions.sql
│
├── PowerBI/
│   └── Retail_Sales_Dashboard.pbix
│
├── Documentation/
│   └── Project_Report.docx
│
└── Screenshots/
```

## 🔐 Security

Never commit these to GitHub:

- Passwords
- Azure SQL credentials
- Databricks access tokens
- Client secrets
- API keys
- Connection secrets

Use managed identities, Azure Key Vault, environment variables, or other appropriate secret-management methods.

## 🎤 Interview Explanation

> I built an end-to-end retail data engineering and analytics platform on Azure. Azure SQL and JSON were used as sources, Azure Data Factory handled ingestion, ADLS Gen2 acted as the data lake, and Databricks performed Bronze-to-Silver-to-Gold transformations. I organized the analytics data using Unity Catalog, served it through a Databricks SQL Warehouse, and connected Power BI to create a Retail Sales Dashboard showing revenue, transaction count, store performance, category sales and sales trends.

## 📈 Project Outcome

The project demonstrates the complete cloud data engineering lifecycle:

```text
Source
  ↓
Ingestion
  ↓
Data Lake
  ↓
Transformation
  ↓
Data Quality
  ↓
Analytics Model
  ↓
SQL Serving
  ↓
Business Dashboard
```

## 👨‍💻 Author

**Evan Punnen**

**Technology Stack:** Azure | ADF | ADLS Gen2 | Databricks | PySpark | Unity Catalog | SQL | Power BI
