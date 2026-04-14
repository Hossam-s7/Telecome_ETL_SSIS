# 📡 Telecome_ETL_SSIS

An ETL (Extract, Transform, Load) pipeline built using **SQL Server Integration Services (SSIS)** for processing and loading Telecom data into a structured data warehouse.

---

## 📌 Project Overview

This project automates the extraction of raw telecom data, applies transformation logic, handles errors, and loads the clean data into a SQL Server data warehouse. It follows a dimensional modeling approach with fact and dimension tables.

---

## 🗂️ Project Structure

```
Telecome_ETL_SSIS/
│
├── ETL_SSIS/                          # SSIS Project Files
│   ├── bin/Development/               # Compiled output binaries
│   ├── obj/Development/               # Build object files
│   ├── Package.dtsx                   # Main ETL SSIS package
│   ├── Package 1.dtsx                 # Secondary SSIS package
│   ├── Integration Services Project3.dtsx
│   ├── Integration Services Project3.dtp
│   ├── Integration Services Project3.database
│   └── Project.params                 # Project-level parameters
│
└── SQL/
    └── sql_files/                     # SQL scripts (run in order)
        ├── 01. Create database.sql
        ├── 02. Create fact transaction table.sql
        ├── 03. Create error destination output.sql
        ├── 04. Create dim imsi.sql
        ├── 05. Create error source output.sql
        ├── 51_create_dim_audit.sql
        ├── 52_usp_insert_dim_audit.sql
        └── 99_ssis_sql_tasks.sql
```

---

## 🛠️ Technologies Used

| Tool | Purpose |
|------|---------|
| **SSIS** (SQL Server Integration Services) | ETL pipeline orchestration |
| **SQL Server** | Data warehouse & staging database |
| **T-SQL** | Database creation, stored procedures, transformations |
| **Visual Studio** | SSIS project development environment |

---

## ⚙️ Setup & How to Run

### 1️⃣ Prerequisites
- SQL Server (2016 or later recommended)
- SQL Server Management Studio (SSMS)
- Visual Studio with SSIS extension installed

### 2️⃣ Database Setup
Run the SQL scripts **in order**:

```
01. Create database.sql
02. Create fact transaction table.sql
03. Create error destination output.sql
04. Create dim imsi.sql
05. Create error source output.sql
51_create_dim_audit.sql
52_usp_insert_dim_audit.sql
99_ssis_sql_tasks.sql
```

### 3️⃣ Run the SSIS Package
1. Open **Visual Studio**
2. Load `Integration Services Project3`
3. Configure connection strings in `Project.params`
4. Execute `Package.dtsx`

---

## 🏗️ Data Warehouse Design

| Table | Type | Description |
|-------|------|-------------|
| `fact_transaction` | Fact | Core telecom transaction records |
| `dim_imsi` | Dimension | Subscriber identity (IMSI) info |
| `dim_audit` | Dimension | ETL audit trail and logging |
| `error_destination_output` | Error | Records that failed loading |
| `error_source_output` | Error | Records with source extraction issues |

---

## 📋 ETL Flow

```
[Source Data]
     ↓
[Extract - SSIS Package]
     ↓
[Transform - Data cleaning & mapping]
     ↓        ↘
[Load - DWH]  [Error Tables - for bad records]
     ↓
[Audit Log - dim_audit]
```
