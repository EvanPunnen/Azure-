# AdventureWorks Sales Analytics — Azure Databricks

## Project Overview

This project implements an end-to-end data engineering solution using the **Medallion Architecture** in Azure Databricks.

Raw AdventureWorks data is ingested into the **Bronze** layer, cleaned and transformed in the **Silver** layer, and modeled into a business-ready **Gold star schema**. Unity Catalog is used for data governance, and an Azure Databricks AI/BI Dashboard is used for business reporting.

### Architecture

```text
AdventureWorks CSV Data
          |
          v
      Bronze Layer
      Raw Data
          |
          v
      Silver Layer
   Clean + Transform
          |
          v
       Gold Layer
     Star Schema
          |
     +----+----+
     |         |
     v         v
Unity Catalog  AI/BI Dashboard
```

---

## Technologies Used

- Azure Databricks
- Azure Data Lake Storage Gen2 (ADLS Gen2)
- Apache Spark / PySpark
- SQL
- Unity Catalog
- Delta Lake
- Parquet
- Databricks AI/BI Dashboard

---

## Storage Architecture

### Azure Storage Account

```text
evanpunnen
```

### Containers

```text
bronze/
silver/
gold/
```

---

## 1. Bronze Layer

The Bronze layer contains the original AdventureWorks CSV files. The raw data is preserved without changing the source data.

### Source Datasets

```text
AdventureWorks_Calendar.csv
AdventureWorks_Customers.csv
AdventureWorks_Products.csv
AdventureWorks_Product_Categories.csv
AdventureWorks_Product_Subcategories.csv
AdventureWorks_Returns.csv
AdventureWorks_Sales*.csv
AdventureWorks_Territory.csv
```

### Unity Catalog Bronze Tables

```text
evandb_7405616343397725.bronze.calendar
evandb_7405616343397725.bronze.customers
evandb_7405616343397725.bronze.products
evandb_7405616343397725.bronze.product_categories
evandb_7405616343397725.bronze.product_subcategories
evandb_7405616343397725.bronze.returns
evandb_7405616343397725.bronze.sales
evandb_7405616343397725.bronze.territories
```

---

## 2. Silver Layer

The Silver layer contains cleaned and transformed data stored as Parquet.

### Silver Tables

```text
calendar/
customer/
products/
product_categories/
product_subcategories/
returns/
sales/
territories/
```

### Unity Catalog Silver Tables

```text
evandb_7405616343397725.silver.calendar
evandb_7405616343397725.silver.customer
evandb_7405616343397725.silver.products
evandb_7405616343397725.silver.product_categories
evandb_7405616343397725.silver.product_subcategories
evandb_7405616343397725.silver.returns
evandb_7405616343397725.silver.sales
evandb_7405616343397725.silver.territories
```

### Main Transformations

#### Calendar
- Converted `Date` to date type
- Added `Year`
- Added `Month`

#### Customer
- Created `Full_Name`
- Calculated customer age
- Created `AgeGroup`

#### Products
- Split product SKU and product name information

#### Sales
- Converted `StockDate` to timestamp
- Standardized `OrderNumber`

---

## 3. Gold Layer

The Gold layer organizes the data into a business-friendly **star schema**.

### Gold Tables

#### Dimensions

```text
dim_date
dim_customer
dim_product
dim_territory
```

#### Facts

```text
fact_sales
fact_returns
```

### Star Schema

```text
                    dim_customer
                         |
                         |
dim_date -------- fact_sales -------- dim_product
                         |
                         |
                   dim_territory


                    dim_product
                         |
                         |
dim_date -------- fact_returns ------- dim_territory
```

---

## 4. Gold Dimension Tables

### dim_date

Contains calendar attributes used for time-based analysis.

```text
DateKey
Date
Year
Quarter
Month
MonthName
YearMonth
DayName
WeekOfYear
IsWeekend
```

`DateKey` is generated in `yyyyMMdd` format.

### dim_customer

Contains customer information and derived attributes.

```text
CustomerKey
FullName
Age
AgeGroup
```

### dim_product

Combines product, subcategory, and category information.

```text
ProductKey
ProductSKU
ProductName
ModelName
ProductColor
ProductSize
ProductStyle
SubcategoryName
CategoryName
ProductCost
ProductPrice
MarginPct
```

### dim_territory

Contains territory information.

```text
TerritoryKey
Region
Country
Continent
```

---

## 5. Gold Fact Tables

### fact_sales

The sales fact table contains one record for each sales order line.

```text
OrderNumber
OrderLineItem
OrderDateKey
StockDateKey
CustomerKey
ProductKey
TerritoryKey
OrderQuantity
UnitPrice
UnitCost
ExtendedRevenue
ExtendedCost
GrossProfit
OrderYear
```

### Calculated Measures

```text
ExtendedRevenue = OrderQuantity × UnitPrice

ExtendedCost = OrderQuantity × UnitCost

GrossProfit = ExtendedRevenue − ExtendedCost
```

### fact_returns

The returns fact table contains return information.

```text
ReturnDateKey
ProductKey
TerritoryKey
ReturnQuantity
ReturnValue
```

### Calculated Measure

```text
ReturnValue = ReturnQuantity × ProductPrice
```

---

## 6. Unity Catalog

### Catalog

```text
evandb_7405616343397725
```

### Schemas

```text
bronze
silver
gold
```

Unity Catalog is used to organize and govern the Bronze, Silver, and Gold datasets.

---

## 7. Data Validation

Data-quality checks were performed before building the dashboard.

### Validation Checks

- Row count validation
- Duplicate checks
- Null-value checks
- Orphan foreign-key checks
- Dimension uniqueness checks
- Fact-table integrity checks

### Validation Results

| Check | Result |
|---|---:|
| Products | 293 / 293 distinct |
| Customers | 18,148 / 18,148 distinct |
| Territories | 10 / 10 distinct |
| Dates | 912 / 912 distinct |
| Missing Product Keys | 0 |
| Missing Customer Keys | 0 |
| Missing Territory Keys | 0 |
| Missing Order Dates | 0 |

---

## 8. Business Analysis

The Gold layer supports the following business questions:

- What is the total revenue?
- What is the gross profit?
- How many units were sold?
- How does revenue change by year?
- Which product categories generate the most revenue?
- What is the return rate?
- Which categories have higher return rates?
- Who are the top customers by revenue?

---

## 9. AI/BI Dashboard

### Dashboard

**AdventureWorks Sales Dashboard**

### KPI Visuals

1. Total Revenue
2. Gross Profit
3. Units Sold

### Analytical Visuals

4. Revenue by Year
5. Revenue by Category
6. Return Rate
7. Return Rate by Category
8. Top 10 Customers by Revenue

### Key Results

```text
Total Revenue  ≈ 24.91M
Gross Profit   ≈ 10.46M
Units Sold     = 84,174
```

The dashboard provides a business-facing view of the Gold-layer data.

---

## 10. Project Structure

```text
AdventureWorks-Sales-Analytics/
│
├── README.md
│
├── notebooks/
│   ├── Bronze_to_Silver
│   └── Silver_to_Gold
│
├── bronze/
│   └── Raw AdventureWorks CSV data
│
├── silver/
│   ├── calendar/
│   ├── customer/
│   ├── products/
│   ├── product_categories/
│   ├── product_subcategories/
│   ├── returns/
│   ├── sales/
│   └── territories/
│
└── gold/
    ├── dim_date/
    ├── dim_customer/
    ├── dim_product/
    ├── dim_territory/
    ├── fact_sales/
    └── fact_returns/
```

---

## 11. End-to-End Data Flow

```text
Raw CSV Files
     |
     v
+----------------+
| Bronze Layer   |
| Raw Data       |
+----------------+
     |
     | PySpark Transformations
     v
+----------------+
| Silver Layer   |
| Cleaned Data   |
+----------------+
     |
     | Data Modeling
     v
+----------------+
| Gold Layer     |
| Star Schema    |
+----------------+
     |
     +-------------------+
     |                   |
     v                   v
+------------+     +-------------+
| Unity      |     | AI/BI       |
| Catalog    |     | Dashboard   |
+------------+     +-------------+
```

---

## 12. Project Completion Status

| Component | Status |
|---|---|
| Bronze Layer | Completed |
| Silver Layer | Completed |
| Gold Layer | Completed |
| Star Schema | Completed |
| Unity Catalog | Completed |
| Data Validation | Completed |
| Business Queries | Completed |
| AI/BI Dashboard | Completed |
| Job Automation | Skipped |

### Note on Job Automation

Databricks Job automation was treated as an optional next step and was intentionally skipped for this project. The completed project includes the Bronze, Silver, Gold, Unity Catalog, validation, business analysis, and dashboard components.

---

## 13. Key Learning Outcomes

Through this project, the following data engineering concepts were implemented:

- Medallion Architecture
- Azure Data Lake Storage Gen2
- PySpark data transformation
- Parquet data storage
- Delta Lake
- Star schema modeling
- Fact and dimension tables
- Data-quality validation
- Referential-integrity checks
- Unity Catalog
- Azure Databricks
- Business-oriented data modeling
- AI/BI dashboard development

---

## 14. Conclusion

The AdventureWorks Sales Analytics project demonstrates an end-to-end Azure Databricks data engineering workflow.

Raw AdventureWorks data was transformed through Bronze, Silver, and Gold layers, modeled into a star schema, governed using Unity Catalog, validated for data quality, and exposed through an AI/BI dashboard for business analysis.

The final solution provides a structured foundation for analyzing sales, revenue, profit, returns, products, customers, and territories.
