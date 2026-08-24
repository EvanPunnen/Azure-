# Azure Data Factory 

A hands-on **Microsoft Azure Data Engineering project** demonstrating ETL and data integration using **Azure Data Factory, Azure Blob Storage, and Azure SQL Database**.

The project covers the complete workflow from creating Azure resources and storing source data to building pipelines, transforming data, moving data between services, monitoring executions, and verifying the final output.

## Technologies Used

* Microsoft Azure
* Azure Data Factory
* Azure Blob Storage
* Azure SQL Database
* Azure Resource Manager
* ETL / Data Integration
* Data Flow
* SQL
* Copy Data Activity

## Project Workflow

```text
Azure Resource Group
        ↓
Azure Storage Account
        ↓
Azure Blob Storage
        ↓
Source Container
        ↓
Azure Data Factory
        ↓
Linked Services & Datasets
        ↓
Copy Data / Delete Operations
        ↓
Pipeline Validation & Debugging
        ↓
Variables & Get Metadata
        ↓
Azure SQL Database
        ↓
Mapping Data Flow
        ↓
Filter / Sort / Join
        ↓
Blob Storage Sink
        ↓
Output Verification
```

## Key Features

### Azure Resource & Storage Setup

* Created an Azure Resource Group
* Created an Azure Storage Account
* Created source and destination Blob Storage containers
* Uploaded source files to the source container
* Configured storage resources for data integration

### Azure Data Factory

* Created an Azure Data Factory instance
* Configured linked services
* Created source and destination datasets
* Built ETL pipelines
* Configured Copy Data activity
* Configured Delete activity with logging
* Validated and debugged pipelines
* Monitored pipeline execution and activity status

### Copy Data Pipeline

* Configured the source dataset and source file path
* Configured the destination dataset and container
* Mapped source and destination columns
* Verified column data types
* Executed the Copy Data pipeline
* Verified successfully transferred data in the destination

### Delete Operation

* Added Delete activity to the pipeline
* Configured the source file path
* Enabled logging for the Delete activity
* Executed the deletion operation
* Verified the deletion log

### Pipeline Variables & Metadata

* Used **Append Variable** activity
* Used **Set Variable** activity
* Created and configured pipeline variables
* Used **Get Metadata** activity
* Retrieved file metadata
* Used **Execute Pipeline** activity
* Passed and verified pipeline values
* Validated and monitored pipeline execution

### Azure SQL Database

* Created an Azure SQL Server
* Created an Azure SQL Database
* Configured database connectivity
* Used SQL Query Editor
* Created an employee data table
* Inserted employee records
* Executed SQL queries
* Created an Azure SQL linked service in Azure Data Factory
* Used Azure SQL data as a Data Flow source

### Mapping Data Flow

The project also demonstrates data transformation using Azure Data Factory Mapping Data Flow.

**Transformations performed:**

* **Source** – Read data from Azure SQL Database
* **Filter** – Filtered records based on required conditions
* **Sort** – Sorted the filtered records
* **Join** – Combined data from multiple sources
* **Sink** – Exported transformed data to Blob Storage

## ADF Activities Used

| Activity         | Purpose                                    |
| ---------------- | ------------------------------------------ |
| Append Variable  | Appends values to an array variable        |
| Set Variable     | Stores values in pipeline variables        |
| Get Metadata     | Retrieves metadata from source data        |
| Execute Pipeline | Executes another pipeline                  |
| Copy Data        | Copies data between source and destination |
| Delete           | Deletes files from the configured location |
| Data Flow        | Performs data transformation and movement  |

## Data Flow Transformations

| Transformation | Purpose                                  |
| -------------- | ---------------------------------------- |
| Source         | Reads data from the source               |
| Filter         | Selects records based on conditions      |
| Sort           | Orders records based on selected columns |
| Join           | Combines records from multiple sources   |
| Sink           | Writes processed data to the destination |

## Pipeline Monitoring

Pipeline execution was validated using Azure Data Factory's **Validate** and **Debug** options.

The output and monitoring sections were used to:

* Check pipeline execution status
* Verify activity status
* Identify successful executions
* Check Data Flow output
* Verify generated files
* Confirm successful data movement and transformation

## Project Outcome

The project demonstrates an end-to-end Azure data integration workflow:

**Data Ingestion → Data Movement → Data Transformation → Data Storage → Validation → Monitoring**

It provides practical experience with Azure Data Factory pipelines, Blob Storage, Azure SQL Database, linked services, datasets, variables, metadata operations, ETL workflows, and Mapping Data Flow.

## Repository Contents

```text
Azure-Data-Factory/
│
├── ADF-2/
│   └── Copy Data & Delete Operations
│
├── ADF-3/
│   └── Variables, Metadata, SQL & Data Flow
│
├── README.md
```

## Skills Demonstrated

* Azure Data Factory
* ETL Pipeline Development
* Data Integration
* Azure Blob Storage
* Azure SQL Database
* SQL
* Mapping Data Flow
* Data Transformation
* Pipeline Variables
* Metadata Handling
* Linked Services
* Dataset Configuration
* Pipeline Debugging
* Pipeline Monitoring
* Data Validation

## Conclusion

This project demonstrates practical implementation of **ETL and data integration pipelines in Microsoft Azure**, covering both basic data movement and more advanced pipeline and Data Flow operations using Azure Data Factory.
