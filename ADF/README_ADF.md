# Azure Data Factory (ADF) Projects & Learning Repository

This repository contains hands-on work, practice implementations, and reference documentation related to **Azure Data Factory (ADF)** and Azure data integration.

The `ADF` folder contains practical examples covering data ingestion, transformation, incremental loading, conditional processing, metadata-driven operations, and pipeline orchestration.

---

## 📁 Repository Structure

```text
Azure-/
│
├── ADF/
│   ├── ADF.pdf
│   ├── ADf - Data Ingestion.pdf
│   ├── Append Variable, Get Metadata, Joins, Data Flow, Execute Pipeline.pdf
│   ├── Filtration (IF Condition).pdf
│   ├── Incremental Data Loading.pdf
│   └── Mapping, Deletion, Trigger & Set Variable (Finding Area) in ADF.pdf
│
├── Databricks/
│
└── README.md
```

---

# 🚀 Azure Data Factory

**Azure Data Factory (ADF)** is a cloud-based data integration and orchestration service used to create data pipelines for moving, transforming, and processing data from different sources.

This repository demonstrates important ADF concepts through practical pipeline development and documentation.

---

## 🧩 Topics Covered

### 1. Data Ingestion

The repository includes practical work related to ingesting data from external sources and loading it into Azure storage.

Key concepts:

- Source and sink configuration
- Copy Data Activity
- REST API ingestion
- Azure Storage integration
- Linked Services
- Datasets
- Pipeline configuration

**Reference:** `ADf - Data Ingestion.pdf`

---

### 2. Copy Data Operations

ADF Copy Data Activity is used to move data between different sources and destinations.

Examples include:

- Source → Azure Storage
- REST API → Azure Storage
- File-based ingestion
- Database-to-storage movement
- Raw data ingestion

**Reference:** `ADF.pdf`

---

### 3. Incremental Data Loading

Incremental loading is implemented to process only newly added or modified records instead of loading the complete dataset every time.

Important concepts:

- Watermark column
- Watermark table
- Incremental pipeline
- Dynamic queries
- Lookup Activity
- Stored procedures
- Pipeline parameters
- Data filtering

**Reference:** `Incremental Data Loading.pdf`

### Typical Flow

```text
Source Database
      │
      ▼
Read Previous Watermark
      │
      ▼
Filter New/Updated Records
      │
      ▼
Copy Incremental Data
      │
      ▼
Update Watermark
```

---

### 4. Filter / IF Condition

ADF conditional activities can be used to control pipeline execution based on a condition.

Examples:

- Check whether data exists
- Validate pipeline parameters
- Route processing based on conditions
- Execute different activities depending on the result

**Reference:** `Filtration (IF Condition).pdf`

Example flow:

```text
                 ┌── True  → Process Data
Condition ───────┤
                 └── False → Alternative / Skip
```

---

### 5. Get Metadata Activity

The **Get Metadata** activity retrieves information about files, folders, and datasets.

Common use cases:

- Check whether a file exists
- Retrieve file names
- Get folder contents
- Validate input data
- Build metadata-driven pipelines

**Reference:** `Append Variable, Get Metadata, Joins, Data Flow, Execute Pipeline.pdf`

---

### 6. Variables and Append Variable

ADF variables allow values to be stored and reused during pipeline execution.

The repository includes examples involving:

- Set Variable
- Append Variable
- Dynamic values
- Passing values between activities
- Building dynamic pipeline logic

---

### 7. Data Flow

ADF Mapping Data Flows provide a visual way to transform data without managing the underlying Spark infrastructure.

Covered concepts include:

- Data transformation
- Source and sink
- Joins
- Derived columns
- Filtering
- Mapping
- Transformation pipelines

**Reference:** `Append Variable, Get Metadata, Joins, Data Flow, Execute Pipeline.pdf`

---

### 8. Joins

ADF data transformation workflows can combine data from multiple sources using joins.

Common join types include:

- Inner Join
- Left Outer Join
- Right Outer Join
- Full Outer Join
- Cross Join

Joins are useful when integrating related datasets before loading them into a destination.

---

### 9. Execute Pipeline

The **Execute Pipeline** activity allows one pipeline to call another pipeline.

This is useful for creating modular and reusable pipeline architectures.

Example:

```text
Master Pipeline
      │
      ├── Pipeline 1: Ingestion
      │
      ├── Pipeline 2: Transformation
      │
      └── Pipeline 3: Loading
```

---

### 10. Mapping

Mapping is used to define how source fields correspond to destination fields.

It is especially useful when:

- Source and destination column names differ
- Data structures need alignment
- Only selected columns should be loaded
- Schema transformation is required

**Reference:** `Mapping, Deletion, Trigger & Set Variable (Finding Area) in ADF.pdf`

---

### 11. Delete Operations

ADF supports deletion-related operations as part of data processing workflows.

These can be used for:

- Removing old files
- Cleaning temporary data
- Maintaining storage zones
- Implementing data retention logic

---

### 12. Triggers

Triggers determine when an ADF pipeline should execute.

Common trigger types include:

- Schedule Trigger
- Tumbling Window Trigger
- Event-based Trigger
- Manual Trigger

Triggers can be used to automate recurring data integration workflows.

---

### 13. Set Variable

The Set Variable activity is used to assign or update values during pipeline execution.

Typical use cases:

- Store dynamic paths
- Store timestamps
- Store pipeline parameters
- Maintain control values
- Support conditional processing

---

# 🏗️ Typical ADF Pipeline Architecture

A practical data integration workflow can be structured as:

```text
                ┌─────────────────┐
                │   Data Source   │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │  ADF Pipeline   │
                └────────┬────────┘
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
       Copy / Ingestion       Metadata Check
              │                     │
              └──────────┬──────────┘
                         ▼
                ┌─────────────────┐
                │ Transformation  │
                │  / Data Flow    │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │  Azure Storage  │
                │  / Database     │
                └─────────────────┘
```

---

# 🛠️ Technologies & Services

The work in this repository focuses on:

- **Azure Data Factory**
- **Azure Storage**
- **REST APIs**
- **Azure SQL / SQL concepts**
- **ETL / ELT**
- **Data Integration**
- **Pipeline Orchestration**
- **Incremental Data Loading**
- **Data Transformation**
- **Metadata-driven Processing**

---

# 📚 Documentation

| File | Description |
|---|---|
| `ADF.pdf` | Azure Data Factory copy/data operation examples |
| `ADf - Data Ingestion.pdf` | Data ingestion and REST API pipeline implementation |
| `Append Variable, Get Metadata, Joins, Data Flow, Execute Pipeline.pdf` | Advanced ADF activities and pipeline operations |
| `Filtration (IF Condition).pdf` | Conditional and filtering logic |
| `Incremental Data Loading.pdf` | Incremental loading using watermark concepts |
| `Mapping, Deletion, Trigger & Set Variable (Finding Area) in ADF.pdf` | Mapping, deletion, triggers, and variable operations |

---

# 🎯 Learning Objectives

This repository demonstrates practical understanding of:

1. Creating Azure Data Factory pipelines
2. Configuring linked services and datasets
3. Moving data using Copy Data Activity
4. Ingesting data from REST APIs
5. Working with Azure Storage
6. Implementing incremental data loading
7. Using watermark-based processing
8. Applying conditional logic
9. Working with variables and parameters
10. Using Get Metadata
11. Performing data transformations
12. Joining datasets
13. Calling child pipelines
14. Configuring triggers
15. Building reusable data integration workflows

---

# 💡 Key Data Engineering Concepts

### Full Load

Loads the complete dataset during every execution.

```text
Source → Complete Dataset → Destination
```

### Incremental Load

Loads only newly added or modified records.

```text
Source
  │
  ▼
Watermark / Last Modified Value
  │
  ▼
New or Updated Records
  │
  ▼
Destination
```

Incremental loading reduces unnecessary data movement and is commonly used in production data pipelines.

---

# 📌 Repository Purpose

This repository serves as a practical reference for **Azure Data Factory and Data Engineering concepts**, combining hands-on pipeline development with supporting documentation.

It can be used for:

- Learning ADF
- Data Engineering practice
- Interview preparation
- Project reference
- Demonstrating Azure data integration skills
- Understanding common ADF pipeline patterns

---

## 👨‍💻 Author

**Evan Punnen**

B.Tech – Computer Science & Engineering

GitHub: [EvanPunnen](https://github.com/EvanPunnen)

---

## ⭐ Technologies

`Azure Data Factory` · `Azure Storage` · `REST API` · `SQL` · `ETL` · `Data Integration` · `Data Engineering`
