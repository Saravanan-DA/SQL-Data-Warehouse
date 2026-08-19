# SQL Data Warehouse – Medallion Architecture

A SQL-based Data Warehouse built using the Medallion Architecture, integrating data from CRM and ERP source systems and transforming it into analytics-ready business data.

## 🥉 Bronze Layer – Raw Data

The Bronze layer acts as the raw landing zone for CRM and ERP data.

* Created DDL tables for all source datasets.
* Loaded CSV files using `BULK INSERT`.
* Automated ingestion using the `bronze.load_bronze` stored procedure.
* Added load logging, execution timing, and error handling.
* Preserved source data structure for traceability.

## 🔍 Data Quality

Performed data quality checks before transformation:

* Duplicate and NULL checks
* Unwanted space detection
* Data standardization checks
* Negative and invalid value detection
* Date validation
* Sales, quantity, and price consistency checks

## 🥈 Silver Layer – Cleaned & Transformed Data

The Silver layer converts raw Bronze data into clean, standardized, and trusted data.

* Standardized names, gender, marital status, countries, and product lines.
* Removed duplicates using `ROW_NUMBER()`.
* Converted invalid and integer-based dates into proper `DATE` values.
* Handled NULL, negative, and inconsistent sales values.
* Derived product category IDs and product end dates.
* Integrated CRM and ERP data.
* Automated transformations using the `silver.load_silver` stored procedure.
* Implemented transactions, logging, timing, and error handling.

## 🥇 Gold Layer – Business-Ready Data

The Gold layer provides a business-friendly analytical model using dimension and fact views.

### Dimensions

* `gold.dim_customers`
* `gold.dim_products`

### Fact

* `gold.fact_sales`

The Gold layer enables:

* Customer and product analysis
* Sales and revenue reporting
* Product/category performance
* Geographic analysis
* Business intelligence dashboards
* Trend and performance analysis

## 🏗️ Architecture

```text
CRM ──┐
      ├──> Bronze ──> Silver ──> Gold
ERP ──┘       Raw       Clean      Business
              Data      Data       Data
```

Technologies: SQL Server • T-SQL • Stored Procedures • BULK INSERT • Views • Medallion Architecture

