# Retail Data Integration Platform using Azure Data Factory

## Overview

End-to-end retail ETL/data integration project using Azure Data Factory, ADLS Gen2 and Azure SQL Database.

### Architecture

```text
SQL Orders ───────────────┐
REST Products ────────────┼──> PL_01_Ingest_RawZone
Blob Stores ──────────────┘              |
                                         v
                                  ADLS raw/
                                         |
                                         v
                         PL_02_Transform_ProcessedZone
                    Filter → Standardize → Product Join
                         → Store Join → Aggregate
                                         |
                                         v
                              processed/SalesSummary.csv
                                         |
                                         v
                              PL_03_Load_CuratedZone
                                Copy + Upsert
                                         |
                                         v
                              dbo.SalesSummary
                                         |
                                         v
                              PL_00_Master_Orchestrator
                                         |
                                         v
                                  Daily Trigger
```

## Azure Resources

| Resource | Name |
|---|---|
| Resource Group | `Evan_DE` |
| Storage Account | `evande` |
| Containers | `raw`, `processed` |
| Data Factory | `evan-df` |
| SQL Server | `evanserver` |
| SQL Database | `evandb` |

## SQL Tables

### Orders

```sql
CREATE TABLE dbo.Orders
(
    OrderID INT NOT NULL,
    OrderDate DATETIME NOT NULL,
    ProductID INT NOT NULL,
    StoreID INT NOT NULL,
    Quantity INT NOT NULL,
    UnitPrice DECIMAL(18,2) NOT NULL,
    OrderStatus VARCHAR(50) NULL,
    CONSTRAINT PK_Orders PRIMARY KEY (OrderID)
);
```

### WatermarkControl

```sql
CREATE TABLE dbo.WatermarkControl
(
    SourceID INT IDENTITY(1,1) PRIMARY KEY,
    SourceName VARCHAR(100) NOT NULL,
    SourceType VARCHAR(20) NOT NULL,
    LastLoadTimestamp DATETIME2 NULL,
    IsActive BIT NOT NULL DEFAULT 1
);
```

### SalesSummary

```sql
CREATE TABLE dbo.SalesSummary
(
    SalesDate DATE NOT NULL,
    StoreID INT NOT NULL,
    StoreName VARCHAR(200) NULL,
    ProductID INT NOT NULL,
    ProductName VARCHAR(200) NULL,
    Category VARCHAR(100) NULL,
    Ordercount INT NULL,
    TotalQuantity INT NULL,
    TotalSales DECIMAL(18,2) NULL,
    CONSTRAINT PK_SalesSummary PRIMARY KEY (SalesDate, StoreID, ProductID)
);
```

## Linked Services

Create:

- `AzureDataLakeStorage1` → storage account `evande`
- `LS_SQL_SOURCE` → `evandb`
- `LS_SQL_TARGET` → `evandb`
- `RestService1` → Products JSON source

## Datasets

Create:

- `DS_SQL_Orders`
- `DS_REST_Products`
- `DS_BLOB_Stores`
- `DS_RAW_Orders`
- `DS_RAW_Products`
- `DS_PROCESSED_SalesSummary`
- `DS_SQL_SalesSummary`

## PL_01 — Ingest Raw Zone

### Activities

```text
Lookup_ActiveSources
       |
ForEach_Source
       |
Switch_SourceType
  /       |       \
SQL      REST     Blob
```

Lookup query:

```sql
SELECT *
FROM dbo.WatermarkControl
WHERE IsActive = 1;
```

ForEach items:

```text
@activity('Lookup_ActiveSources').output.value
```

### REST mapping

Collection:

```text
$['products']
```

Fields:

```text
['ProductID']
['ProductName']
['Category']
['UnitPrice']
```

Do not use `[0]`, because it returns only the first product.

## PL_02 — Transform Processed Zone

Data Flow:

```text
SourceOrders
     |
FilterValidRecords
     |
DerivedStandardize
     |
JoinProducts <----- SourceProducts
     |
JoinStores   <----- SourceStores
     |
AggregateSales
     |
SinkProcessed
```

### Important Product ID issue

Orders use numeric ProductIDs such as:

```text
101, 102, 103...
```

Products use:

```text
P001, P002, P003...
```

Normalize the Product ID inside the data flow before the Product join. Do not modify the raw source just to make the join work.

### AggregateSales

Group by:

```text
SalesDate
StoreID
ProductID
StoreName
ProductName
Category
```

Aggregations:

```text
TotalQuantity = sum(toInteger(Quantity))
TotalSales = configured quantity × unit-price expression
Ordercount = count()
```

The completed sample transformation produced 10 rows.

### Sink

Use:

```text
Container/path: processed
File name option: Output to single file
File name: SalesSummary.csv
```

Output columns:

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

## PL_03 — Load Curated Zone

Copy:

```text
DS_PROCESSED_SalesSummary
        ↓
dbo.SalesSummary
```

Use:

```text
Linked service: LS_SQL_TARGET
Write behavior: Upsert
```

Keys:

```text
SalesDate
StoreID
ProductID
```

Upsert is required so reruns do not fail with a duplicate primary-key error.

## Row Count Validation

Lookup:

```sql
SELECT COUNT(*) AS TotalRows
FROM dbo.SalesSummary;
```

Enable:

```text
First row only = ON
```

If `TotalRows > 0`:

```text
Validation_Success
```

Otherwise:

```text
Fail_No_Rows
```

## PL_00 — Master Orchestrator

Run pipelines in order:

```text
PL_01_Ingest_RawZone
        ↓ Success
PL_02_Transform_ProcessedZone
        ↓ Success
PL_03_Load_CuratedZone
```

Enable **Wait on completion** for each Execute Pipeline activity.

## Daily Trigger

Create:

```text
TR_Daily_Master
```

Schedule:

```text
Every 1 day
```

Attach it to:

```text
PL_00_Master_Orchestrator
```

Publish the trigger and verify it under:

```text
Monitor → Trigger runs
```

## End-to-End Test

1. Run PL_01 and verify raw files.
2. Run PL_02 and refresh Data Preview.
3. Confirm AggregateSales contains 10 sample rows.
4. Verify `processed/SalesSummary.csv`.
5. Run PL_03.
6. Verify `dbo.SalesSummary`.
7. Run PL_03 again to test Upsert.
8. Run PL_00.
9. Confirm PL_01, PL_02 and PL_03 all succeed.
10. Confirm the daily trigger is enabled.

## Troubleshooting

| Problem | Fix |
|---|---|
| Products has only one row | Remove `[0]`; use `$['products']` |
| Product columns blank | Use `['ProductID']`, `['ProductName']`, `['Category']`, `['UnitPrice']` |
| JoinProducts = 0 rows | Normalize P001-style IDs to the numeric Orders key |
| Store join type mismatch | Make both StoreID columns the same numeric type |
| `processed/SalesSummary.csv` not found | Sink → Output to single file → `SalesSummary.csv` |
| Duplicate SQL primary key | Use Upsert with SalesDate + StoreID + ProductID |
| SQL connection failure | Check SQL networking/IP/Azure services and linked service |
| Validation query error | Use `SELECT COUNT(*) AS TotalRows FROM dbo.SalesSummary;` |

## Final Checklist

- [x] Resource Group
- [x] ADLS Gen2
- [x] raw container
- [x] processed container
- [x] Azure SQL
- [x] SQL tables
- [x] Linked services
- [x] Datasets
- [x] PL_01 ingestion
- [x] PL_02 transformation
- [x] Product ID normalization
- [x] Joins
- [x] Aggregation
- [x] Processed CSV
- [x] SQL Upsert
- [x] Row-count validation
- [x] Master orchestrator
- [x] Daily trigger
- [x] Published
- [x] End-to-end test

## Technologies

Azure Data Factory, Azure Data Lake Storage Gen2, Azure SQL Database, SQL, REST/JSON, Mapping Data Flow, ETL, Upsert, validation and pipeline orchestration.

## Interview Summary

> I built a retail data integration platform using Azure Data Factory. Orders were ingested from Azure SQL, Products from REST JSON and Stores from ADLS/Blob storage. I created a raw zone, used Mapping Data Flow for cleansing, Product ID normalization, joins and sales aggregation, then loaded the curated data into Azure SQL using Upsert. I added row-count validation, a master orchestrator and a daily schedule trigger.
