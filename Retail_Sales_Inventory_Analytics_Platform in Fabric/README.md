# Retail Sales & Inventory Analytics Platform

An end-to-end retail data engineering and analytics project built using
**Microsoft Fabric, OneLake, PySpark, Fabric Lakehouse, and Power BI**.

The project follows a **Bronze → Silver → Gold** architecture to
transform raw retail data into business-ready product KPIs and an
interactive Power BI dashboard.

------------------------------------------------------------------------

## 📌 Project Overview

This project processes three major retail datasets:

-   **Orders**
-   **Returns**
-   **Inventory**

The data is first stored in the **Bronze** layer, cleaned and
standardized in the **Silver** layer, transformed into business KPIs in
the **Gold** layer, and finally visualized in **Power BI**.

### Architecture

``` text
                 ┌────────────────────┐
                 │   Raw Retail Data  │
                 │ Orders / Returns / │
                 │     Inventory      │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │      BRONZE        │
                 │    Raw Data        │
                 │     OneLake        │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │      SILVER        │
                 │ Cleaned & Standard │
                 │      Data          │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │       GOLD         │
                 │ Product KPI Table  │
                 │ gold_product_kpis  │
                 └─────────┬──────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │      POWER BI      │
                 │ Interactive Report │
                 └────────────────────┘
```

------------------------------------------------------------------------

## 🛠️ Technologies Used

  Technology         Purpose
  ------------------ ----------------------------------------
  Microsoft Fabric   End-to-end data platform
  OneLake            Central data storage
  Fabric Lakehouse   Data storage and analytical tables
  Fabric Notebook    PySpark development and transformation
  PySpark            Data cleaning, joining and aggregation
  Power BI           Dashboard and visualization

------------------------------------------------------------------------

## 📂 Project Structure

The Lakehouse uses the following OneLake Files structure:

``` text
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

The main analytical tables include:

``` text
Tables
└── dbo
    ├── silver_orders
    ├── silver_returns
    ├── silver_inventory
    └── gold_product_kpis
```

------------------------------------------------------------------------

# 🔄 Data Engineering Workflow

## 1. Bronze Layer --- Raw Data

The Bronze layer is the raw landing area.

### Datasets

-   Orders
-   Returns
-   Inventory

The purpose of this layer is to retain the incoming data before applying
business transformations.

### Beginner explanation

Think of Bronze as:

> **"The original data as it arrived."**

No major business calculations should be performed here.

------------------------------------------------------------------------

## 2. Silver Layer --- Data Cleaning

The Silver layer contains cleaned and standardized data.

### Orders Cleaning

The Orders data is cleaned by:

-   Standardizing column names
-   Cleaning Customer IDs
-   Cleaning product names
-   Converting quantity to numeric format
-   Converting order amount to numeric format
-   Parsing order dates
-   Standardizing email addresses
-   Standardizing payment mode
-   Standardizing delivery status
-   Cleaning addresses
-   Removing invalid records
-   Removing duplicate Order IDs

### Returns Cleaning

The Returns source contains generic `Prop_*` columns, so the fields are
mapped to meaningful names such as:

``` text
ReturnID
OrderID
CustomerID
Product
ReturnReason
ReturnDate
RefundStatus
PickupAddress
ReturnAmount
```

The cleaning process includes:

-   Removing the accidental header row
-   Cleaning IDs
-   Parsing return dates
-   Converting return amounts to numeric values
-   Standardizing refund status
-   Removing duplicate Return IDs

### Inventory Cleaning

Inventory fields are standardized into:

``` text
ProductID
ProductName
Stock
LastStocked
Warehouse
CostPrice
Available
```

------------------------------------------------------------------------

# 🥇 3. Gold Layer --- Business KPIs

The Gold layer combines the cleaned datasets and produces a
business-ready product KPI dataset.

The final table is:

``` text
gold_product_kpis
```

## Main Transformations

### Returns Aggregation

Returns are first aggregated by `OrderID` before being joined with
Orders.

This prevents multiple return records for one order from incorrectly
duplicating order revenue.

### Inventory Join

Inventory information is joined with Orders using the cleaned:

``` text
ProductName
```

### COGS

Cost of Goods Sold is calculated as:

``` text
COGS = Quantity × Cost Price
```

### Net Profit

Net profit is calculated as:

``` text
Net Profit = Order Amount − COGS
```

### Profit Status

The project also creates:

``` text
Profit_Status
```

Possible statuses include:

-   Profit
-   Loss
-   Cost Data Missing
-   Quantity Missing

The status helps explain why a product's profit value may be positive,
negative, or unavailable.

------------------------------------------------------------------------

# 📊 Gold KPIs

The `gold_product_kpis` table contains business metrics including:

-   `ProductName`
-   `Total_Orders`
-   `Unique_Customers`
-   `Total_Quantity_Sold`
-   `Total_Revenue`
-   `Avg_Order_Value`
-   `Total_COGS`
-   `Avg_Cost`
-   `Net_Profit`
-   `Total_Returns`
-   `Returned_Orders`
-   `Total_Return_Amount`
-   `Current_Stock`
-   `Return_Rate_Percent`
-   `Profit_Status`

### Return Rate

The product-level return rate is calculated as:

``` text
Return Rate % =
(Returned Orders / Total Orders) × 100
```

------------------------------------------------------------------------

# 📈 Power BI Dashboard

The Gold dataset is connected to Power BI to create an interactive
retail analytics dashboard.

## KPI Cards

The dashboard contains:

-   **Total Revenue**
-   **Total Orders**
-   **Unique Customers**
-   **Net Profit**
-   **Return Rate %**
-   **Total Quantity Sold**
-   **Total COGS**

## Filters / Slicers

-   **Product**
-   **Profit Status**

## Charts

### Revenue Analysis

**Revenue by Product**

Shows revenue generated by each product.

### Profitability Analysis

**Net Profit by Product**

Shows the calculated profit or loss for each product.

### Returns Analysis

**Returns by Product**

Shows the number of returns associated with each product.

**Return Amount by Product**

Shows the financial value associated with returns.

### Inventory Analysis

**Current Stock by Product**

Shows current inventory levels.

### Sales Analysis

**Quantity Sold by Product**

Shows the quantity sold for each product.

### Profit Status

**Products by Profit Status**

Shows the distribution of products across profit/loss and data-quality
statuses.

------------------------------------------------------------------------

# 🧑‍💻 How to Reproduce the Project

## Step 1 --- Create a Microsoft Fabric Workspace

1.  Open Microsoft Fabric.
2.  Create or open a workspace.
3.  Create a Lakehouse.
4.  Create a Notebook.

Example:

``` text
Lakehouse: Retail_LH
Notebook: Retail_NB
```

------------------------------------------------------------------------

## Step 2 --- Create OneLake Folders

Create:

``` text
Files/
├── Bronze/
│   ├── Orders/
│   ├── Returns/
│   └── Inventory/
│
├── Silver/
│   ├── Orders/
│   ├── Returns/
│   └── Inventory/
│
└── Gold/
    └── Product_KPIs/
```

------------------------------------------------------------------------

## Step 3 --- Upload Raw Data

Place the raw Orders, Returns and Inventory files into their respective
Bronze folders.

Example:

``` text
Files/Bronze/Orders
Files/Bronze/Returns
Files/Bronze/Inventory
```

------------------------------------------------------------------------

## Step 4 --- Load Data in the Notebook

Open the Fabric Notebook and load the source files into PySpark
DataFrames.

Inspect:

``` python
df_order
df_returns
df_inventory
```

Always check:

``` python
df_order.columns
df_returns.columns
df_inventory.columns
```

and display sample records before transforming the data.

------------------------------------------------------------------------

## Step 5 --- Clean the Silver Data

Apply the cleaning and standardization rules to each dataset.

Save the results as:

``` text
silver_orders
silver_returns
silver_inventory
```

Verify the schema and sample records after saving.

------------------------------------------------------------------------

## Step 6 --- Create the Gold Dataset

Load:

``` text
silver_orders
silver_returns
silver_inventory
```

Then:

1.  Aggregate Returns by Order ID.
2.  Join Returns with Orders.
3.  Join Inventory using ProductName.
4.  Calculate COGS.
5.  Calculate Net Profit.
6.  Create Profit_Status.
7.  Aggregate product-level KPIs.
8.  Calculate Return Rate.
9.  Save the Gold dataset.

Final output:

``` text
gold_product_kpis
```

------------------------------------------------------------------------

## Step 7 --- Connect Power BI

1.  Open Power BI in the Fabric workspace.
2.  Connect the report to the Gold dataset.
3.  Refresh the model after schema changes.
4.  Confirm `gold_product_kpis` appears in the Data/Fields pane.
5.  Create KPI cards.
6.  Add slicers.
7.  Add product-level charts.
8.  Format the dashboard.

------------------------------------------------------------------------

# ⚠️ Important Data Validation

The project calculates profit from the available Order Amount, Quantity
and Cost Price.

Therefore, some products can legitimately show negative profit when:

``` text
Order Amount < Quantity × Cost Price
```

Do not artificially change negative profit values to positive values.
The dashboard should represent the calculated result from the source
data.

Also, when displaying `Return_Rate_Percent` as a single KPI from
product-level records, use an appropriate aggregation such as
**Average** rather than simply summing all product percentages.

------------------------------------------------------------------------

# 📌 Final Dashboard Flow

``` text
KPI Cards
    ↓
Product & Profit Status Filters
    ↓
Revenue Analysis
    ↓
Profitability Analysis
    ↓
Returns Analysis
    ↓
Inventory Analysis
    ↓
Quantity Sold Analysis
    ↓
Profit Status Analysis
```

------------------------------------------------------------------------

# 🎯 Project Outcome

This project demonstrates an end-to-end retail data engineering workflow
using Microsoft Fabric.

It covers:

-   Data ingestion
-   OneLake storage
-   Bronze/Silver/Gold architecture
-   PySpark data cleaning
-   Data transformation
-   Dataset joins
-   KPI calculation
-   Lakehouse tables
-   Power BI data modeling
-   Interactive dashboard development

------------------------------------------------------------------------

# 💼 Resume Description

**Retail Sales & Inventory Analytics Platform \| Microsoft Fabric,
PySpark, Power BI**

Built an end-to-end retail analytics platform using Microsoft Fabric and
OneLake, implementing Bronze-Silver-Gold data architecture. Cleaned and
transformed Orders, Returns and Inventory data using PySpark, created
product-level KPIs including revenue, COGS, net profit, returns and
inventory, and developed an interactive Power BI dashboard for retail
performance analysis.

------------------------------------------------------------------------

# 🗣️ Interview Explanation

> "I built a retail analytics platform using Microsoft Fabric. I stored
> raw Orders, Returns and Inventory data in OneLake using a Bronze,
> Silver and Gold architecture. I used PySpark in a Fabric Notebook to
> clean and standardize the data, join the datasets, calculate COGS and
> Net Profit, and create a product-level Gold KPI table. Finally, I
> connected the Gold dataset to Power BI and created an interactive
> dashboard for revenue, orders, customers, profitability, returns,
> inventory and quantity sold."

------------------------------------------------------------------------

## 📁 Suggested Repository Structure

``` text
Retail-Sales-Inventory-Analytics-Platform/
│
├── README.md
│
├── notebooks/
│   └── Retail_NB
│
├── data/
│   ├── Bronze/
│   ├── Silver/
│   └── Gold/
│
├── powerbi/
│   └── Retail_Analytics_Dashboard
│
├── documentation/
│   └── Retail_Sales_Inventory_Analytics_Platform_Project_Report.docx
│
└── screenshots/
    ├── fabric/
    ├── lakehouse/
    └── powerbi/
```

------------------------------------------------------------------------

## 👤 Author

**Evan Punnen Jacob**

B.Tech --- Computer Science & Engineering

**Project:** Retail Sales & Inventory Analytics Platform

**Technologies:** Microsoft Fabric \| OneLake \| PySpark \| Power BI

