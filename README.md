# 🏪 Online Retail Sales Data Pipeline  
**Medallion Architecture:** Bronze | Silver | Gold Layers  
Implemented with PostgreSQL  

---

## 📋 Project Overview

This project implements a data lake pipeline for Online Retail Sales data using the Medallion architecture:

- **Bronze Layer:** Raw ingested data, minimal transformation.  
- **Silver Layer:** Cleaned, integrated, and enriched data with relationships.  
- **Gold Layer:** Aggregated, business-level metrics and analytics-ready datasets.  

The datasets originate from Kaggle’s Online Retail Sales CSV files: Customers, Transactions, and Product Categories.

---

## 🟫 Bronze Layer — Raw Data Ingestion

### Purpose
Capture raw data exactly as provided to preserve fidelity and enable reprocessing.

### Tables and Datasets

| Table          | Source File        | Description                                  |
|----------------|--------------------|----------------------------------------------|
| `customer`     | customer.csv       | Customer demographic details                  |
| `transactions` | transactions.csv   | Transactional sales data                       |
| `prod_cat_info`| prod_cat_info.csv  | Product categories and subcategories          |

### Table Details
- Minimal constraints — no foreign keys to prevent ingestion failure.
- Data types reflect raw data formats.
- Data loaded via PostgreSQL `COPY` command or `psql \copy`.

---

## 🧱 Silver Layer — Cleaned and Integrated Data

### Purpose
- Apply data cleaning (handle missing, invalid data).  
- Enforce relationships with foreign keys.  
- Standardize formats and types (e.g., date formatting).  
- Create dimension tables (e.g., `gender`, `city`, `store_type`, `calendar`).  
- Split wide tables into normalized structures.  

### New Tables (examples)

| Table           | Description                        |
|-----------------|----------------------------------|
| `customers`     | Cleaned customer data with FK to `gender`, `city`  |
| `transactions`  | Cleaned and linked to customers, products, calendar, store types |
| `product_category`  | Categories dimension            |
| `product_subcategory` | Subcategories linked to categories |
| `gender`         | Lookup table for genders          |
| `city`           | Lookup table for cities           |
| `store_type`     | Lookup for store types            |
| `calendar`       | Date dimension with year, month, day, quarter, week |

### Transformations
- Convert text-based categories to IDs referencing lookup tables.  
- Normalize `Store_type`, `Gender`, `City` into separate dimension tables.  
- Validate and parse date fields, link transactions to calendar.  
- Add missing dates to calendar dimension for full date coverage.

---

## 🏆 Gold Layer — Aggregations and Analytics

### Purpose
- Provide business-ready datasets and metrics.  
- Implement star schema or dimensional modeling for BI tools.  
- Pre-aggregate metrics like sales totals, average order size, customer lifetime value.

### Examples of Gold Tables / Views

| Table / View       | Description                                       |
|--------------------|-------------------------------------------------|
| `daily_sales`      | Aggregated sales per day, product category, store type |
| `customer_lifetime_value` | Total spend and transactions per customer   |
| `product_performance` | Sales volume, revenue by product and subcategory |
| `monthly_revenue`   | Monthly sales and growth trends                   |
| `store_performance` | Sales by store type and geography                  |

### Analytics Queries Examples

- Total transactions and revenue over time.  
- Top-selling product categories/subcategories.  
- Customer segmentation by purchase frequency and value.  
- Store type sales comparison.  
- Identify sales seasonality and trends using calendar data.

---

## 📂 Folder Structure (suggested)

/project-root
│
├── /bronze_sql # SQL scripts for Bronze layer (raw tables)
/silver_sql # SQL scripts for Silver layer (cleaned, FK constraints, lookups)
/gold_sql # SQL scripts for Gold layer (aggregations, views)
/data # Raw CSV files
/etl_scripts # Python/SQL ETL scripts for transformations and data loads
/README.md # This documentation file



---

## ⚙️ How to Run

1. Create and set up PostgreSQL database.  
2. Run Bronze layer SQL scripts to create raw tables.  
3. Use `COPY` or ETL scripts to load CSV data into Bronze tables.  
4. Run Silver layer scripts to create clean tables and lookup dimensions, and transform raw data.  
5. Run Gold layer scripts to create analytics views and aggregated tables.  
6. Use BI tools or SQL queries to analyze the Gold layer data.

---

## 📈 Next Steps & Improvements

- Automate ETL pipelines with Airflow or cron jobs.  
- Add incremental loading and CDC for updates.  
- Implement advanced analytics like churn prediction or basket analysis.  
- Integrate dashboards with tools like PowerBI, Tableau, or Metabase.

---

## 👤 Author

Sujan Rai  
Data Engineering Enthusiast | PostgreSQL Advocate  

---

## 📜 References

- Kaggle Dataset: [Online Retail Sales](https://www.kaggle.com/datasets/tanushagarwal01/online-retail-sales-analysis)  
- Medallion Architecture concepts  
- PostgreSQL official docs  

---

