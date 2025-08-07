# 🟫 Bronze Layer: Raw Data Ingestion (PostgreSQL)

This is the **Bronze Layer** of our data lake pipeline. It consists of raw ingested data loaded into PostgreSQL tables directly from CSV files, with minimal transformation and no business logic applied. This layer serves as the foundation for further processing into Silver and Gold layers.

---

## 📦 Datasets

### 1. `customer.csv`
| Column Name | Data Type | Description               |
|-------------|-----------|---------------------------|
| customer_ID | INT (PK)  | Unique customer ID        |
| DOB         | DATE      | Date of birth             |
| Gender      | TEXT      | Gender of the customer    |
| city_code   | INT       | Code representing city    |

---

### 2. `transactions.csv`
| Column Name        | Data Type | Description                                |
|--------------------|-----------|--------------------------------------------|
| transaction_id     | BIGINT (PK) | Unique transaction ID                    |
| cust_id            | INT       | Customer ID (can be FK to `customer_ID`)   |
| tran_date          | DATE      | Date of transaction                        |
| prod_subcat_code   | INT       | Product sub-category code (can be FK)      |
| prod_cat_code      | INT       | Product category code (can be FK)          |
| Qty                | INT       | Quantity of product bought                 |
| Rate               | DECIMAL   | Rate of product                            |
| Tax                | DECIMAL   | Tax applied                                |
| total_amt          | DECIMAL   | Final amount including tax                 |
| Store_type         | TEXT      | Store where purchase was made              |

📝 *Note:* No foreign key constraints are applied at this layer to keep ingestion flexible.

---

### 3. `prod_cat_info.csv`
| Column Name        | Data Type | Description                  |
|--------------------|-----------|------------------------------|
| prod_cat_code      | INT       | Product category code        |
| prod_cat           | TEXT      | Name of product category     |
| prod_sub_cat_code  | INT       | Product sub-category code    |
| prod_subcat        | TEXT      | Name of product sub-category |

---

## 📂 Purpose of Bronze Layer

- Capture raw data exactly as it is received.
- Preserve data fidelity and audit trail.
- Allow reprocessing from source if needed.

---

## 🧱 Table Creation Scripts

The SQL scripts to create these tables are inside the `/bronze_sql/` directory.

Each CSV file is mapped 1:1 with a corresponding table:
- `customer` table
- `transactions` table
- `prod_cat_info` table

---

## ⚙️ Ingestion Notes

- Tools like `COPY` or `psql \copy` are used to bulk load the CSVs.
- Data types were chosen to match real-world values and support future transformations.
- Constraints are minimal to avoid ingestion failure from raw source inconsistencies.

---

## 🔜 Next Steps

Move to the **Silver Layer**:
- Apply joins
- Add relationships
- Clean the data
- Standardize types

---

## 👨‍💻 Author

**Sujan Rai**  
Data Engineering Enthusiast | PostgreSQL First 💙  
